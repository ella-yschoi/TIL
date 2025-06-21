# Custom Hooks

## 1. Custom Hooks이란?

- 개발자가 스스로 커스텀한 훅을 의미
- 이를 이용해 **반복되는 로직을 함수로 뽑아내어 재사용** 가능

### (1) Custom Hooks을 사용하는 경우

- 여러 url을 fetch할 때,
- 여러 input에 의한 상태 변경 등 반복되는 로직을 동일한 함수에서 작동하게 하고 싶을 때.

### (2) Custom Hooks의 장점

- 상태관리 로직의 **재활용**이 가능
- 클래스 컴포넌트보다 **적은 양의 코드로 동일한 로직**을 구현할 수 있으며
- 함수형으로 작성하기 때문에 보다 **명료하다**는 장점이 있음 (e.g. `useSomething`)

<br/>

## 2. Custom Hooks 사용 예시

- 예를 들어, 아래와 같은 컴포넌트가 있다면,
  
  ```javascript
    // FriendStatus : 친구가 online인지 offline인지 return하는 컴포넌트
    function FriendStatus(props) {
    const [isOnline, setIsOnline] = useState(null);
    useEffect(() => {
        function handleStatusChange(status) {
        setIsOnline(status.isOnline);
        }
        ChatAPI.subscribeToFriendStatus(props.friend.id, handleStatusChange);
        return () => {
        ChatAPI.unsubscribeFromFriendStatus(props.friend.id, handleStatusChange);
        };
    });

    if (isOnline === null) {
        return 'Loading...';
    }
    return isOnline ? 'Online' : 'Offline';
    }

    // FriendListItem : 친구가 online일 때 초록색으로 표시하는 컴포넌트
    function FriendListItem(props) {
    const [isOnline, setIsOnline] = useState(null);
    useEffect(() => {
        function handleStatusChange(status) {
        setIsOnline(status.isOnline);
        }
        ChatAPI.subscribeToFriendStatus(props.friend.id, handleStatusChange);
        return () => {
        ChatAPI.unsubscribeFromFriendStatus(props.friend.id, handleStatusChange);
        };
    });

    return (
        <li style={{ color: isOnline ? 'green' : 'black' }}>
        {props.friend.name}
        </li>
    );
    }
  ```

- 두 컴포넌트에서 사용하기 위해 동일하게 사용되고 있는 **로직을 분리하여 함수 `useFriendStatus` 사용** → Custom Hook을 정의할 때는 아래와 같은 규칙이 필요
  - (1) Custom Hook을 정의할 때는 **함수 이름 앞에** `use`를 붙이기
  - (2) 대개의 경우 **프로젝트 내의 hooks 디렉토리에 Custom Hook을 위치**시키기
  - (3) Custom Hook으로 만들 때 함수는 **조건부 함수가 아니어야 함**. 즉 return 하는 값은 조건부여서는 안 됨. 때문에 위의 이 `useFriendStatus` Hook은 온라인 상태의 여부를 boolean 타입으로 반환하고 있음.

- 이렇게 만들어진 Custom Hook은 Hook 내부에 `useState`와 같은 React 내장 Hook을 사용하여 작성 가능
- 일반 함수 내부에서는 React 내장 Hook을 불러 사용할 수 없지만 Custom Hook에서는 가능함.

- `useFriendStatus` Hook을 두 컴포넌트에 적용한 코드

    ```javascript
    function FriendStatus(props) {
        const isOnline = useFriendStatus(props.friend.id); // useFriendStatus Hook 적용

        if (isOnline === null) {
            return 'Loading...';
        }
        return isOnline ? 'Online' : 'Offline';
    }

    function FriendListItem(props) {
        const isOnline = useFriendStatus(props.friend.id);

        return (
            <li style={{ color: isOnline ? 'green' : 'black' }}>
                {props.friend.name}
            </li>
        );
    }
    ```

- 로직을 분리해 Custom Hook으로 만들었기 때문에 두 컴포넌트는 더 직관적으로 확인이 가능해짐.
- 그러나 같은 Custom Hook을 사용했다고 해서 두 개의 컴포넌트가 같은 state를 공유하는 것은 아님. 그저 **로직만 공유할 뿐, state는 컴포넌트 내에서 독립적으로 정의**되어 있음.
