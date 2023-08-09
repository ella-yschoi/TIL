# UseMemo

## 1. useMemo의 역할

- 컴포넌트는 상태가 변경되거나 부모 컴포넌트가 렌더링이 될 때마다 리렌더링을 하는 구조로 이루어졌음
- 하지만 너무 잦은 리렌더링은 앱에 좋지 않은 성능을 끼침
- React Hook은 함수 컴포넌트가 상태를 조작하고 및 최적화 기능을 사용할 수 있게끔 하는 메소드
- 그중 **렌더링 최적화를 위한 Hook**도 존재 → useCallback과 useMemo가 바로 그 역할을 하는 Hook

<br/>

## 2. useMemo란?

- useMemo은 특정 값(value)을 재사용하고자 할 때 사용하는 Hook임.
- 예를 들어, 아래 컴포넌트는 props로 넘어온 value값을 calculate라는 함수에 인자로 넘겨서 result 값을 구한 후, `<div>` 엘리먼트로 출력하는 코드가 있다면,
  
  ```javascript
  function Calculator({value}) {
    const result = calculate(value);
    return <>
        <div>
            {result}
        </div>
    </>;
  }
  ```

- 만약 위 calculate가 return에 오랜 시간이 걸린다면, **컴포넌트는 렌더링을 할 때마다 이 함수를 계속해서 호출**하면서 로딩시간이 늘어날 것이고, 결국 사용자에게 좋지 않은 경험을 줄 수 있음
  
  ```javascript
  import { useMemo } from "react";
  const result = useMemo(() => calculate(value), [value]);
    return <>
        <div>
            {result}
        </div>
    </>;
  
  ```

- 위 Calculator 컴포넌트의 value는 일종의 값으로서, 렌더링을 할 때마다 이 value값이 계속 바뀌는 게 아니라면 & 값을 어딘가에 저장을 해뒀다가 다시 꺼내서 쓸 수만 있다면 굳이 calculate 함수를 호출할 필요도 없을 것임
- 여기서 useMemo Hook을 사용할 수 있음.
- useMemo를 호출하여 calculate를 감싸주면, **이전에 구축된 렌더링과 새로이 구축되는 렌더링을 비교해 value값이 동일할 경우 → 이전 렌더링의 value값 재활용 가능(Memoization)**

<br/>

## 3. Memoization 이란?

- **기존에 수행한 연산의 결과값을 메모리에 저장**을 해두고, **동일한 입력이 들어오면 재활용**하는 프로그래밍 기법
- 이 메모이제이션을 적절히 사용한다면 굳이 중복 연산 할 필요가 없으므로 앱 성능 최적화 가능 → useMemo가 활용
- 직접 메모이제이션 개념을 이용해 로직 구현이 가능하나, useMemo Hook 호출 시 로직 구현을 대신해 주기에 훨씬 간편함.
