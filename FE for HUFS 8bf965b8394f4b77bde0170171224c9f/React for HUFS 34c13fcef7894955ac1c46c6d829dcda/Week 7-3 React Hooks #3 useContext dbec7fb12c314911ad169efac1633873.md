# Week 7-3. React Hooks #3. useContext

생성일: June 9, 2024 2:46 AM

## Context란?

컴포넌트 간에 데이터를 전달하기 위해 props를 사용한다는 것을 배웠습니다. 일반적으로 부모 컴포넌트에서 자식 컴포넌트로 props를 통해 데이터를 전달하는데, 만약 여러개의 컴포넌트들이 중첩되어 있으면 어떻게 될까요? 

예를 들어 A, B, C, D, E, F 컴포넌트가 차례대로 중첩되어 있으면 A 컴포넌트에서 F 컴포넌트까지 데이터를 전달하기 위해 중간 컴포넌트를 계속해서 거쳐야 합니다. 이 과정에서 중복되는 코드를 작성하는 등 굉장히 비효율적인 일들이 발생합니다. 

좀 귀찮지만 그냥 전해주면 되는 거 아닌가..? 라고 생각할 수도 있지만 이보다 훨씬 많은 컴포넌트가 중첩될 수도 있고, 만약 그 과정에서 무언가 잘못되어 수정을 해야 한다면 중간 컴포넌트를 일일이 찾아서 코드를 수정해야 하고 그 중 하나라도 작동하지 않는다면 디버깅을 하는 데 시간을 허비해야 할 수도 있습니다. 

React에는 이러한 상황에서 사용할 수 있는 **Context**라는 개념이 존재합니다.

**Context**를 사용하면 단계마다 **일일이 props를 넘겨주지 않고도 컴포넌트 트리 전체에 데이터를 제공**할 수 있습니다. 즉 **부모 컴포넌트로부터 자식 컴포넌트로 전달되는 데이터의 흐름과 상관없이 전역적인 데이터를 다룰 수 있습니다**. 

## ContextAPI

React에서 Context를 사용하기 위해서는 ContextAPI를 사용해야 하는데, **createContext, Provider, Consumer** 이 세가지 개념만 알면 됩니다!

- `createContext` : context 객체를 생성
- `Provider` : 생성한 context를 하위 컴포넌트에 전달
- `Consumer` : context의 변화를 감시

Context를 직접 사용해보면서 개념들을 이해해봅시다. 

---

### App.js (Context 선언하기)

```jsx
**import React, { createContext } from 'react';**
**import Component from './Component';**

**export const AppContext = createContext();**

function App() {

	**const meal = {
		name: '팝콘',
		price: 5000
	};**

  return (
		**<AppContext.Provider value={meal}>
			<div>
				<Component/>
			</div>
		</AppContext.Provider>**
  );
};

export default App;
```

우선 최상위 컴포넌트인 App.js에 `createContext`로 AppContext라는 빈 Context객체를 생성해주었습니다. 그리고 Provider를 사용하여 하위 컴포넌트에 meal 객체를 전달했습니다. 
`<AppContext.Provider>`로 감싸준 모든 하위 컴포넌트들은 value로 넣어준 meal에 접근할 수 있게 됩니다!

### Component.jsx (Context 가져오기)

```jsx
import React from 'react';
**import { AppContext } from './App';**

function Component() {

  return (
    **<AppContext.Consumer>
      {meal => (
        <h2>{meal.name} - {meal.price}원</h2>
      )}
    </AppContext.Consumer>**
  );
};

export default Component;
```

하위 컴포넌트에서 Consumer를 통해(Consumer의 자식은 함수여야 합니다) 가장 가까운 Provider의 value를 가져와서 띄워주면 props를 사용하지 않고도 데이터가 하위 컴포넌트로 전달되는 것을 볼 수 있습니다. 

Provider 하위에서 Context를 구독하는 모든 컴포넌트는 Provider의 value값이 변경될 때마다 리렌더링됩니다.

## useContext

Consumer와 동일한 기능을 useContext라는 훅을 사용해서 훨씬 간편하게 구현할 수 있습니다. 

### Component.jsx (useContext 사용)

```jsx
**import React , { useContext } from 'react';**
import { AppContext } from './App';
****
function Component() {

  **const meal = useContext(AppContext);

  return (
    <h2>{meal.name} - {meal.price}원</h2>
  );**
};

export default Component;
```

useContext는 Context객체를 받아와서 현재값을 반환합니다. 또한 useContext를 호출한 컴포넌트는 Context값이 변경될 때마다(Provider의 value값이 변경될 때마다) 리렌더링됩니다. 

이처럼 useContext 훅을 사용하면 Consumer 없이 더욱 간결한 컴포넌트를 만들 수 있습니다. 

---

### App.js

```jsx
**import React, { createContext } from 'react';**
**import Component from './Component';**

**export const AppContext = createContext();**

function App() {

	**const meals = [
		{
			name: '핫도그',
			price: 5000
		},
		{
			name: '팝콘',
			price: 4500
		},
		{
			name: '나초',
			price: 3000
		}
	];**

  return (
		**<AppContext.Provider value={meals}>**
			**<div>
				<Component/>
			</div>**
		**</AppContext.Provider>**
  );
};

export default App;
```

### Component.jsx

```jsx
import React , { useContext } from 'react';
import { AppContext } from './App';

function Component() {
  
  **const meals = useContext(AppContext);**

  return (
    **<div>
    {meals.map(meal => (
      <h2>{meal.name} - {meal.price}원</h2>
    ))}
    </div>**
  );
}

export default Component;
```

이렇게 Context에 배열을 전달해 활용할 수도 있습니다.

### **⚠️ContextAPI를 사용할 때 주의점**

**Context.Provider는 value로 저장된 값이 변경되면 useContext를 사용하는 모든 하위 컴포넌트가 리렌더링**됩니다. 그래서 Context를 남발하면 안되며 리렌더링 방지를 위해 코드를 작성하면 자칫하다간 Provider 지옥에 빠져버릴 수 있습니다.. 
상황에 맞게(상태 변경이 잘 일어나지 않는 경우 등) 적절히 사용하는 것이 중요합니다.