# Week 7-2. React Hooks #2. useReducer

생성일: June 9, 2024 2:46 AM

## useReducer란?

`useReducer`는 useState를 대체할 수 있는 React Hook 입니다. 지금까지 배운 `useState`는 컴포넌트 내부에서 상태 업데이트가 이루어졌습니다. 하지만 useReducer를 사용하면 **상태를 업데이트하는 로직을 컴포넌트로부터 분리**할 수 있습니다. 그렇기 때문에 **더욱 복잡한 state를 관리**할 수 있습니다. 

> **Q. useReducer를 언제 쓰나요?
A. 
- 관리해야 할 state가 여러 개일 때
- state 구조가 복잡할 때
- 여러 state가 서로 관련되어 있을 때
- ….**
> 

## useReducer 사용하기

state를 증가/감소/초기화하는 액션을 구현한다고 해봅시다. useState를 사용하면 액션을 각각 별도의 함수로 만들어야 하는 불편함이 있습니다. 

### App.js

```jsx
import React, { useState } from 'react';

function App() {
	const [count, setCount] = useState(0);

	**function handleIncrement() {
		setCount(count + 1);
	}

	function handleDecrement() {
		setCount(count - 1);
	}

	function handleReset() {
		setCount(0);
	}**

  return (
		<div>
      <h2>{count}</h2>
      <div>
        **<button onClick={handleIncrement}>증가</button>
        <button onClick={handleDecrement}>감소</button>
        <button onClick={handleReset}>초기화</button>**
      </div>
    </div>
  );
}

export default App;
```

이와 같은 상황에서 useReducer를 사용한다면 컴포넌트 내에서 state를 업데이트하는 로직을 분리시켜 간편하게 구현할 수 있습니다.

### App.js

```jsx
**import React, { useReducer } from 'react';**

**const reducer = (state, action) => {
  switch (action.type) {
    case "INCREMENT":
      return state + 1;
    case "DECREMENT":
      return state - 1;
    case "RESET":
      return 0;
    default:
      return state;
  }
};**

function App() {
  **const [count, dispatch] = useReducer(reducer, 0);**

  return (
    <div>
      <h2>{count}</h2>
      <div>
        **<button onClick={() => dispatch({type: 'INCREMENT'})}>증가</button>
        <button onClick={() => dispatch({type: 'DECREMENT'})}>감소</button>
        <button onClick={() => dispatch({type: 'RESET'})}>초기화</button>**
      </div>
    </div>
  );
};

export default App;
```

## useReducer의 구조

```jsx
**const reducer = (state, action) => {
  switch (action.type) {
    case "액션명":
      return 업데이트된 state;
    default:
      return state;
  }
};**

**const [state, dispatch] = useReducer(reducer, initialState);**
```

- state: 현재 상태
- dispatch: action을 발생시키는(reducer를 호출하는) 함수
- reducer: state와 action을 받아 새로운 state를 반환하는 사용자 정의 함수
- initialState: 초기값

먼저 reducer는 현재 **state와 action을 파라미터로 받아와서 새로운 state로 반환해주는 함수**입니다. **일반적으로 switch를 사용**하지만 if-else를 사용해서 구현해도 전혀 문제가 없습니다. 

useState와 달리 useReducer는 인자가 두개입니다!  **첫번째 인자로 state를 업데이트할 함수로 전달**하고 **두번째 인자로 state의 초기값을 전달**합니다. dispatch는 특정 action과 함께 reducer 함수를 실행하도록 하는 함수입니다. 

## useReducer 왜 쓰나요…

“useState라는 hook이 존재하는데 굳이 useReducer가 필요한가요..?” 라는 의문을 품으셨나요?? 사실 useState만 가지고 상태관리를 해도 전혀 문제가 없기 때문에 꼭 필요하지 않을뿐더러 이제 막 React를 입문하는 단계에서는 더욱 더 사용할 일이 없을 것입니다… 때문에 useReducer를 이해하기 위해 고통받지 않으셔도 됩니다 😀

언제 useState를 사용해야 하고 언제 useReducer를 사용해야 하는지 정답은 없으므로 각각의 상황에 맞게 적절하게 골라서 사용하면 됩니다.