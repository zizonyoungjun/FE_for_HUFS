# Week 7-1. React Hooks #1. useState

생성일: June 9, 2024 2:46 AM

> 이번 세션에서는 지난 세션에서 잠시 배운 useState를 비롯한 3가지 Hooks에 대해 배워보겠습니다! Hook이 뭐냐하면,, 훅을 사용하면 컴포넌트에서 다양한 React 기능을 사용할 수 있습니다(라고 공식문서에 나와있네요). **React의 여러 기능들을 제대로 사용하려면 Hook을 꼭 알아야 한다**는 뜻이겠죠? 그럼 useState부터 바로 배워보겠습니다👻
> 

## 문자열 state

지난 세션에서 배운 것처럼 숫자 타입의 state는 세터함수에 숫자를 증가/감소/변경 하는 코드 등을 전달해 state를 업데이트할 수 있었습니다. 그럼 문자열 state는 어떻게 업데이트를 해야할까요? `<input>`태그로 state를 입력받아 업데이트해주는 코드를 작성해보겠습니다.

### App.js

```jsx
import React, { useState } from 'react';

function App() {
	**const [name, setName] = useState('');**

	**function handleChange(e) {
		console.log(e);
		setName(e.target.value);
	};**

  return (
    <div>
			**<input
				value={name}
				onChange={handleChange}
			/>**
			<h2>{name}</h2>
    </div>
  );
}

export default App;
```

**e(event)란?
어떠한 사건**을 의미하며, 사용자가 웹페이지와 상호작용 시(버튼 클릭, 입력, 스크롤 등) 브라우저는 이 이벤트를 감지하고 알려줍니다.

![Untitled](Week%207-1%20React%20Hooks%20#1%20useState%20561ed3eae2204485962f6396175d1ea2/Untitled.png)

e를 콘솔에 출력해보면 이런 이벤트 객체가 출력되는 걸 볼 수 있습니다. `e.target`은 이벤트가 발생한 대상 객체를 의미하며 위의 코드에서 `e.target`은 input 입니다. 
`setName(e.target.value)` 은 name state를 input의 value으로 설정해준다는 의미겠죠?

## state 일괄처리

### App.js

```jsx
**import React, { useState } from 'react';**

function App() {
	**const [count, setCount] = useState(0);**

	function handleClick() {
		**setCount(count + 1);
		console.log(count);**
	}

  return (
    <div>
      <button onClick={handleClick}>버튼</button>
      <div>버튼을 {count}번 눌렀습니다!</div>
    </div>
  );
}

export default App;
```

지난 세션에서 보았던 버튼 누른 횟수를 state를 통해 표시해주는 코드입니다. 추가로 이벤트 핸들러 함수 내부에 setCount 호출 후 count값을 콘솔에 출력하도록 코드를 수정해주었습니다. 

코드를 실행해보면, 화면에 보여지는 count값과 콘솔에 출력되는 count값이 같지 않습니다. 콘솔은 실제 count값보다 1 적은 수를 출력하고 있습니다. 왜일까요??

React는 state 업데이트를 하기 전에 **이벤트 핸들러의 모든 코드가 실행될 때까지 기다린 후 실행을 마치면 state 업데이트를 처리**합니다. 이 코드에서는 handleClick 함수의 호출이 완료된 다음에 state이 업데이트 되는거죠. 이벤트 핸들러 내부에서 setCount를 호출한 다음에 콘솔에 state를 출력했어도 아직 state가 업데이트되지 않은 상태에서 출력이 되기 때문에 오차가 생겼던 것입니다. 이를 **일괄처리 혹은 배칭(batching)** 이라고 합니다. 

## state 여러 번 업데이트하기

### App.js

```jsx
import React, { useState } from 'react';
****
function App() {
	const [count, setCount] = useState(0);
****
	function handleClick() {
		**setCount(count + 1);
		setCount(count + 1);**
	}

  return (
    <div>
      <button onClick={handleClick}>버튼</button>
      <div>버튼을 {count}번 눌렀습니다!</div>
    </div>
  );
}

export default App;
```

동일한 이유로 이벤트 핸들러 내에서 이와 같이 count를 1 증가시키는 setCount함수를 두번 호출해도 실제로는 count가 2만큼 증가하지 않습니다. 코드 실행 도중에는 state가 업데이트되지 않기 때문에 `setCount(0 + 1)`을 두번 호출하는 것과 똑같은 결과가 나옵니다. 

### App.js

```jsx
import React, { useState } from 'react';
****
function App() {
	const [count, setCount] = useState(0);
****
	function handleClick() {
		**setCount(a => a + 1);
		setCount(a => a + 1);**
	}

  return (
    <div>
      <button onClick={handleClick}>버튼</button>
      <div>버튼을 {count}번 눌렀습니다!</div>
    </div>
  );
}

export default App;
```

이처럼 **업데이트 함수를 setCount에 전달**하면 코드가 의도대로 동작하는 것을 볼 수 있습니다. React는 업데이트 함수를 마주치면 **이벤트 핸들러 실행 후 처리할 수 있도록 일단 큐에 담은 후 리렌더링 시 큐를 순회하며 최종 state를 업데이트**합니다.

풀어서 설명하면 업데이트 함수는 `setCount(count + 1)` 처럼 state값을 직접 전달하는 게 아니라, **큐의 이전 state를 기반으로 state를 계산하라고 React에게 지시**를 하는 것입니다. 

1. 이전 count state(0)을 첫번째 업데이터 함수에 n 인수로 전달
2. 이전 업데이트 함수의 반환값(1)을 가져와 다음 업데이터 함수에 n 인수로 전달
3. React는 2를 최종 결과로 저장

## 객체 state 업데이트

state는 객체를 포함해서 모든 JavaScript값을 저장할 수 있습니다. 대신 **state에 있는 객체를 업데이트하기 위해서는 새로운 객체를 만들어서 교체해주어야 합니다**. 다시 말해서 state의 객체는 숫자나 불리언처럼 불변하는 것(읽기전용)으로 취급해야 합니다. 

### App.js

```jsx
import React, { useState } from 'react';

function App() {
	**const [name, setName] = useState({
		lastName: '곽',
		firstName: '멋사'
	});**

	**function handleClick() {
		name.firstName = '멋사짱';
		console.log(name.firstName);
	};**

  return (
    <div>
			<h2>{name.lastName + name.firstName}</h2>
			<button onClick={handleClick}>버튼</button>
    </div>
  );
}

export default App;
```

이렇게 객체에 직접 접근해 값을 변경하면 React는 객체가 업데이트되었다는 사실을 알지 못하기 때문에 아무 반응도 하지 않습니다. 

### App.js

```jsx
import React, { useState } from 'react';

function App() {
	const [name, setName] = useState({
		lastName: '곽',
		firstName: '멋사'
	});

	**function handleClick() {
		setName({
			...name,
			firstName: '멋사짱'
		});
	};**

  return (
    <div>
			<h2>{name.lastName + name.firstName}</h2>
			<button onClick={handleClick}>버튼</button>
    </div>
  );
}

export default App;
```

리렌더링을 촉발하기 위해서는 이렇게 새 객체를 생성하고 setName에 전달해주어야 합니다. 또한 위와 같이 객체의 일부 속성만 업데이트하고 다른 속성은 이전 값을 유지하고 싶을 땐 **`...` spread 연산자를 사용해서 이전 객체 복제 후 일부 속성만 덮어씌워**서 전달할 수 있습니다. 

## 배열 state 업데이트

배열도 객체와 마찬가지로 state에서 읽기전용으로 취급해야 하며, 배열을 직접 변경하거나 직접 `push()`, `pop()` 등 메서드도 사용해서는 안됩니다. 

### App.js (배열에 추가하기)

```jsx
import React, { useState } from 'react';

let nextId = 0;

function App() {
	**const [name, setName] = useState('');
	const [list, setList] = useState([]);**

	**function handleClick() {
		setList([
			...list,
			{ id: nextId++, name: name }
		]);
	};**

  return (
    **<div>
			<input
				value={name}
				onChange={e => setName(e.target.value)}
			/>
			<button onClick={handleClick}>추가</button>
			<ul>
				{list.map(item => (
          <li>{item.name}</li>
        ))}
      </ul>
    </div>**
  );
}

export default App;
```

입력받은 이름을 리스트로 띄워주는 코드를 작성해봅시다.  앞서 객체를 변경한 것처럼 배열에 항목을 추가할 때에도 spread 연산자를 사용해주면 기존 항목과 끝에 새 항목을 포함하는 새 배열을 만들어 setList에 전달해줄 수 있습니다. 

### App.js (배열에서 제거하기)

```
import React, { useState } from 'react';

let nextId = 0;

function App() {
	const [name, setName] = useState('');
	const [list, setList] = useState([]);

	function handleClick() {
		setList([
			...list,
			{ id: nextId++, name: name }
		]);
	};

  return (
    <div>
			<input
				value={name}
				onChange={e => setName(e.target.value)}
			/>
			<button onClick={handleClick}>추가</button>
			<ul>
        {list.map(item => (
          **<li>
						{item.name}
						<button onClick={() => {
							setList(
								list.filter(a => a.id !== item.id)
							);
						}}>제거</button>
					</li>**
        ))}
      </ul>
    </div>
  );
}

export default App;
```

배열에서 **특정 항목을 제거하는 가장 쉬운 방법은 필터링**하는 것입니다. 즉, 해당 항목을 포함하지 않는 새 배열을 생성해 setList에 전달해주면 됩니다. JavaScript의 array가 가진 `filter` 함수는 주어진 배열의 값들을 접근해 true를 반환하는 요소를 기준으로 신규 배열을 만들어 반환하는 기능을 합니다. 

여기서 **`list.filter(a => a.id !== item.id)`** 는 item의 id와 다른 id를 가진 item으로 구성된 새 배열을 생성한다는 의미겠죠?