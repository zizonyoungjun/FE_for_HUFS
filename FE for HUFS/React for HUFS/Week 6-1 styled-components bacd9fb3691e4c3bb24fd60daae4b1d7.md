# Week 6-1. styled-components

생성일: June 9, 2024 2:46 AM

## styled-components란?

![Untitled](Week%206-1%20styled-components%20bacd9fb3691e4c3bb24fd60daae4b1d7/Untitled.png)

React 컴포넌트를 스타일링하는 방법은 여러가지가 있습니다. (inline, css-module, CSS-in-JS 등등…)

그 중 **CSS-in-JS**은 말 그대로 JavaScript코드에서 CSS를 작성하는 방식을 말합니다. 

CSS-in-JS은 **class 중복 방지**, **js와 css사이 상태 값 공유** 등 많은 장점 때문에 많은 개발자들이 사용하고 있는데요, 그 중 제일 많이 쓰이는 **styled-components** 라이브러리에 대해 알아보겠습니다.

먼저 터미널을 열고 프로젝트 경로로 가서 styled-components를 설치해줍시다!

```jsx
$ yarn add styled-components
```

설치 후 package.json 파일로 들어가보면 

![Untitled](Week%206-1%20styled-components%20bacd9fb3691e4c3bb24fd60daae4b1d7/Untitled%201.png)

요렇게 styled-components 의존성이 추가된 걸 보실 수 있습니다!

### App.js

```jsx
import React from 'react';

function App() {
  return (
    <div>
      <SecondComponent>짱멋사</SecondComponent>
    </div>
  );
}

export default App;
```

이 코드를 실행해보면 SecondComponent라는 컴포넌트가 정의되어 있지 않기 때문에 에러가 나는 것을 볼 수 있습니다. 그런데 styled-components를 사용하면 **스타일을 적용하는 동시에 해당 스타일을 가진 컴포넌트를 만들 수 있습니다**. 

그럼 styled-components로 SecondComponent라는 컴포넌트를 만들어볼게요!

### App.js

```jsx
import React from 'react';
**import styled from 'styled-components';

const SecondComponent = styled.div`
	display: flex;
	justify-content: center;
	align-items: center;
	width: 200px;
	height: 100px;
	background-color: yellow;
`;**

function App() {
  return (
    <div>
      <SecondComponent>짱멋사</SecondComponent>
    </div>
  );
}

export default App;
```

![Untitled](Week%206-1%20styled-components%20bacd9fb3691e4c3bb24fd60daae4b1d7/Untitled%202.png)

> **1. 변수명은 무조건 대문자로 정의!
2. `styled.tagName` 형식으로 원하는 태그를 넣은 뒤 백틱 안에 css 코드 작성!
3. 컴포넌트 형식으로 사용!**
> 

이렇게 styled-components를 통해 기존 HTML의 모든 태그에 스타일을 적용함과 동시에 컴포넌트를 생성할 수 있습니다!!

## props 전달하기

그런데 만약 배경색만 다른 박스를 여러개 만들고 싶다면 각자 다른 컴포넌트로 선언해서 만들어줘야 할까요???
이것도 지난 세션에서 배운 props를 사용해 해결할 수 있습니다!!

### App.js

```jsx
import React from 'react';
import styled from 'styled-components';

****const SecondComponent = styled.div`
	display: flex;
	justify-content: center;
	align-items: center;
	width: 200px;
	height: 100px;
	**background-color: ${(props) => props.color};**
`;

function App() {
  return (
    <div>
      <SecondComponent **color="yellow"**>짱멋사</SecondComponent>
			<SecondComponent **color="lightgreen"**>짱멋사</SecondComponent>
			<SecondComponent **color="lightblue"**>짱멋사</SecondComponent>
    </div>
  );
}

export default App;
```

![Untitled](Week%206-1%20styled-components%20bacd9fb3691e4c3bb24fd60daae4b1d7/Untitled%203.png)

### App.js

```jsx
import React from 'react';
import styled from 'styled-components';

****const SecondComponent = styled.div`
	display: flex;
	justify-content: center;
	align-items: center;
	width: 200px;
	height: 100px;
	**background-color: ${(props) => props.color || "yellow"};**
`;

function App() {
  return (
    <div>
      <SecondComponent>짱멋사</SecondComponent>
			<SecondComponent>짱멋사</SecondComponent>
			<SecondComponent **color="lightblue"**>짱멋사</SecondComponent>
    </div>
  );
}

export default App;
```

![Untitled](Week%206-1%20styled-components%20bacd9fb3691e4c3bb24fd60daae4b1d7/Untitled%204.png)

이런 식으로 연산자를 사용해 props 값을 설정해주었을 때만 해당 값으로 변경하도록 설정해줄 수도 있습니다.

### App.js

```jsx
import React from 'react';
**import styled, { css } from 'styled-components';**

const SecondComponent = styled.div`
	display: flex;
	justify-content: center;
	align-items: center;
	width: 200px;
	height: 100px;
	background-color: ${(props) => props.color || "yellow"};
  **${props =>
    props.small &&
    css`
      width: 100px;
      height: 50px;
    `}**
`;

function App() {
  return (
    <div>
      <SecondComponent>짱멋사</SecondComponent>
			**<SecondComponent small={true} color="lightgreen">짱멋사</SecondComponent>**
			<SecondComponent color="lightblue">짱멋사</SecondComponent>
    </div>
  );
}

export default App;
```

![Untitled](Week%206-1%20styled-components%20bacd9fb3691e4c3bb24fd60daae4b1d7/Untitled%205.png)

이렇게 특정 속성 뿐만 아니라 props를 통해 여러 속성을 한번에 변경시켜 적용해줄 수도 있습니다. 

## 선택자

css에서 선택자를 통해 특정 요소를 선택해 스타일을 적용할 수 있는 것처럼 styled-components 에서도 동일하게 사용이 가능합니다!

### App.js

```jsx
import React from 'react';
import styled, { css } from 'styled-components';

const SecondComponent = styled.div`
	display: flex;
	justify-content: center;
	align-items: center;
	width: 200px;
	height: 100px;
	background-color: ${(props) => props.color || "yellow"};
  ${props =>
    props.size &&
    css`
      width: 100px;
      height: 50px;
    `}

  **div {
    display: flex;
    justify-content: center;
    align-items: center;
    width: 100px;
    height: 50px;
    background-color: pink;
  }**
`;

function App() {
  return (
    <div>
      **<SecondComponent>
        <div>
          짱멋사
        </div>
      </SecondComponent>**
			<SecondComponent size={true} color="lightgreen">짱멋사</SecondComponent>
			<SecondComponent color="lightblue">짱멋사</SecondComponent>
    </div>
  );
}

export default App;
```

![Untitled](Week%206-1%20styled-components%20bacd9fb3691e4c3bb24fd60daae4b1d7/Untitled%206.png)

위의 코드는 SecondComponents의 후손 선택자인 div에 대해 스타일을 지정해 준 것임을 알 수 있습니다! 

- `&` → 현재의 요소, 즉 자기자신을 의미! (생략 가능)