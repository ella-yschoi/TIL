# UseCallback

## 1.useCallback이란?

- `useCallback` 또한 useMemo와 마찬가지로 메모이제이션 기법을 이용한 Hook
- `useMemo`는 값의 재사용을 위해 사용하는 Hook이라면, `useCallback`은 **함수의 재사용을 위해 사용하는 Hook**임

    ```javascript
    import React, { useCallback } from "react"; // import 필요

    function Caculator({x, y}){
        const add = useCallback(() => x + y, [x, y]);

        return <>
            <div>
                {add()}
            </div>
        </>;
    }
    ```

- `useCallback` Hook을 사용하면 그 함수가 의존하는 값들이 바뀌지 않는 한 **기존 함수를 계속해서 반환**함. 즉 위의 예시에서 x와 y값이 동일하다면 다음 렌더링 때 이 함수를 다시 사용함.
- 단, `useCallback`만 사용한다면 `useMemo`에 비해 괄목할 만한 최적화를 느낄 수는 없음
- `useCallback`은 함수를 호출을 하지 않는 Hook이 아니라, **그저 메모리 어딘가에 함수를 꺼내서 호출하는 Hook**이기 때문
- 따라서 단순히 컴포넌트 내에서 함수를 반복해서 생성하지 않기 위해 `useCallback`을 사용하는 것보다, **자식 컴포넌트의 props로 함수를 전달해 줄 때** 사용하기 좋음.

<br/>

## 2. useCallback과 참조 동등성

- `useCallback`은 참조 동등성에 의존함.
- React는 JavaScript 언어로 만들어진 오픈소스 라이브러리이기에 기본적으로 JavaScript의 문법을 따라감.
- JavaScript에서 함수는 객체인데, 객체는 메모리에 저장할 때 값을 저장하는 게 아니라 **값의 주소를 저장**하기 때문에, 반환하는 값이 같을지라도 일치연산자로 비교했을 때 **false가 출력**됨.
- React도 마찬가지. React는 리렌더링 시 함수를 새로이 만들어서 호출을 하며, 새로이 만들어 호출된 함수는 기존의 함수와 같은 함수가 아님
- 그러나 **`useCallback`을 이용해 함수 자체를 저장해서 다시 사용**하면 **함수의 메모리 주소 값을 저장했다가 다시 사용**하는 것.
- 따라서 React 컴포넌트 함수 내에서 다른 함수의 인자로 넘기거나 자식 컴포넌트의 prop으로 넘길 때 예상치 못한 성능 문제를 막을 수 있음.
