# Week 5-3. Components

생성일: June 9, 2024 2:46 AM

> 컴포넌트는 React의 핵심 개념 중 하나로서 사용자 인터페이스(UI)를 구축하는 기반이 됩니다. 버튼, 배너, 검색창 등 웹(앱) 페이지를 이루는 모든 요소들이 컴포넌트로서 만들어집니다. 컴포넌트를 사용하면 어떠한 효과가 있는지, 또 컴포넌트를 어떻게 활용할 수 있는지에 대해 배워보겠습니다 🚀
> 

## What’s Component?

다음과 같이 작성된 코드가 있다고 해봅시다.

### App.js

```jsx
import React from 'react';

function App() {
  
  return (
    <div>
        <div>
          <h1>My First Component</h1>
          <h3>외대를 만나면 세계가 보인다</h3>
        </div>
    </div>
  );
}

export default App;
```

![스크린샷 2023-05-28 오후 5.52.56.png](Week%205-3%20Components%209aa11e5a0a304c1a85ce70b915ad2fdc/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-05-28_%25E1%2584%258B%25E1%2585%25A9%25E1%2584%2592%25E1%2585%25AE_5.52.56.png)

이러한 코드를 컴포넌트화 한다면 다음과 같이 작성할 수 있는데요

### App.js

```jsx
import React from 'react';

function FirstComponent() {
	return(
		<div>
      <h1>My First Component</h1>
      <h3>외대를 만나면 세계가 보인다</h3>
    </div>
		)
}

function App() {
  
  return (
    <div>
       <FirstComponent/>
    </div>
  );
}

export default App;
```

FirstComponent라는 함수를 선언해서 재사용 가능한 컴포넌트로서 만들어 준 코드입니다. 이렇게 컴포넌트로 만들어주면 필요할 때마다 편하게 재사용을 할 수 있는 장점이 있습니다.

### App.js

```jsx
import React from 'react';

function FirstComponent() {
	return(
		<div>
      <h1>My First Component</h1>
      <h3>외대를 만나면 세계가 보인다</h3>
    </div>
		)
}

function App() {
  
  return (
    <div>
       <FirstComponent/>
       <FirstComponent/>
       <FirstComponent/>
    </div>
  );
}

export default App;
```

![스크린샷 2023-05-28 오후 6.45.46.png](Week%205-3%20Components%209aa11e5a0a304c1a85ce70b915ad2fdc/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-05-28_%25E1%2584%258B%25E1%2585%25A9%25E1%2584%2592%25E1%2585%25AE_6.45.46.png)

## 컴포넌트 export-import

하지만 이런 식으로 하나의 파일에 여러 컴포넌트가 선언된다면, 기능이 추가됨에 따라 코드가 점점 길어지고 가독성이 떨어지게 됩니다. 이를 방지하기 위해 컴포넌트를 다른 파일에 독립시켜서 필요할 때 가져다 쓸 수가 있습니다.

우선 src 폴더 안에 FirstComponent.jsx 라는 파일을 만들어 아래와 같이 코드를 작성해볼까요?

### FirstComponent.jsx

```
import React from 'react';

export default function FirstComponent() {
    return (
        <div>
            <h1>My First Component</h1>
            <h3>외대를 만나면 세계가 보인다</h3>
        </div>
    );
}
```

여기서 export default는 “이 컴포넌트를 다른 곳에서 쓸 수 있도록 내보내겠다” 라는 의미입니다. 이어서 function 구문을 통해 컴포넌트를 선언해줍니다.

이제 다시 App.js로 돌아와 코드를 이렇게 수정해주세요

### App.js

```jsx
import React from 'react';
import FirstComponent from './FirstComponent';

function App() {
  
  return (
    <div>
      <article>
        <FirstComponent/>
      </article>
    </div>
  );
}

export default App;
```

App.js 처럼 여러 컴포넌트가 모이는 파일을 루트 컴포넌트 파일이라고 부릅니다.

컴포넌트라는 여러 종류의 블럭을 만들어, App.js 라는 루트 컴포넌트 파일에 모아 하나의 성을 짓는 과정과 비슷한거죠 🏰 

## 컴포넌트에 Props 전달하기

동대문구 3개 대학의 화합을 위해 “경희대를 만나면 세계가 보인다”, “시립대를 만나면 세계가 보인다” 구문도 추가하고싶다고 가정해봅시다. 그럼 대학 이름 부분만 바뀌는 건데 각각의 새로운 컴포넌트를 만들어줘야 할까요? 이럴 때는 컴포넌트에 props를 전달함으로써 해결할 수 있습니다. FirstComponent.jsx를 다음과 같이 수정해봅시다.

### FirstComponent.jsx

```
import React from 'react';

export default function FirstComponent({univ}) {
    return (
        <div>
            <h1>My First Component</h1>
            <h3>{univ}를 만나면 세계가 보인다</h3>
        </div>
    );
}
```

함수명 옆의 괄호는 어떠한 props를 전달 받을 지를 표기하는 자리입니다. 이렇게 작성해줌으로써 FirstComponent 라는 컴포넌트는 univ 라는 props를 전달 받을 것이라고 알려주는 거죠. 그렇게 전달 받은 univ에 따라 구문을 달리 띄워주도록 <h3> 태그 내부를 수정했습니다.

이제 App.js 를 다음과 같이 작성해볼게요.

### App.js

```jsx
import React from 'react';
import FirstComponent from './FirstComponent';

function App() {
  
  return (
    <div>
      <article>
        <FirstComponent univ="외대"/>
        <FirstComponent univ="경희대"/>
        <FirstComponent univ="시립대"/>
      </article>
    </div>
  );
}

export default App;
```

각 <FirstComponent /> 내부에 전달할 props 값을 알려준 것인데요, 이렇게 전달해주면 props에 따라 다른 문구를 띄워줄 겁니다.

![스크린샷 2023-05-28 오후 6.58.15.png](Week%205-3%20Components%209aa11e5a0a304c1a85ce70b915ad2fdc/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-05-28_%25E1%2584%258B%25E1%2585%25A9%25E1%2584%2592%25E1%2585%25AE_6.58.15.png)

이렇듯 props를 사용하여 각 상황에 따라 달리 활용할 수 있게 함으로써 컴포넌트의 재사용성을 극대화할 수 있습니다.

props의 default 값을 설정해 둘 수도 있는데요, 다음과 같이 작성해주면 됩니다.

### FirstComponent.jsx

```
import React from 'react';

export default function FirstComponent({univ ="외대"}) {
    return (
        <div>
            <h1>My First Component</h1>
            <h3>{univ}를 만나면 세계가 보인다</h3>
        </div>
    );
}
```

### App.js

```jsx
import React from 'react';
import FirstComponent from './FirstComponent';

function App() {
  
  return (
    <div>
      <article>
        <FirstComponent/>
        <FirstComponent univ="경희대"/>
        <FirstComponent univ="시립대"/>
      </article>
    </div>
  );
}

export default App;
```

![스크린샷 2023-05-28 오후 7.04.36.png](Week%205-3%20Components%209aa11e5a0a304c1a85ce70b915ad2fdc/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-05-28_%25E1%2584%258B%25E1%2585%25A9%25E1%2584%2592%25E1%2585%25AE_7.04.36.png)

## 중첩 컴포넌트

때로는 컴포넌트끼리 중첩하여 사용하고 싶을 수도 있습니다. 이러한 경우, 부모 컴포넌트는 children 이라는 형태의 prop으로 자식 컴포넌트를 전달 받게 됩니다.

### App.js

```jsx
import React from 'react';
import FirstComponent from './FirstComponent';

function Box({ children }) {
  return (
    <div style={{ display: "flex", flexDirection: "column" , backgroundColor:"orange"}}>
      {children}
    </div>
  );
}

function App() {
  
  return (
    <div>
      <Box>
        <FirstComponent />
        <FirstComponent univ="경희대"/>
        <FirstComponent univ="시립대"/>
      </Box>
    </div>
  );
}

export default App;
```

![스크린샷 2023-05-28 오후 7.17.02.png](Week%205-3%20Components%209aa11e5a0a304c1a85ce70b915ad2fdc/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-05-28_%25E1%2584%258B%25E1%2585%25A9%25E1%2584%2592%25E1%2585%25AE_7.17.02.png)

`<Box>`는 children 내부에서 무엇이 렌더링되는지 알아야 할 필요가 없습니다. 전달하는 내용물을 명시해가며 설명해주지 않아도 유연하게 잘 받아먹는 것이죠. 이러한 중첩 컴포넌트는 각 컨텐츠를 감싸는 Wrapper 컴포넌트 등에서 자주 사용됩니다.

## 조건부 렌더링

만약 어떤 조건에 따라 그것을 만족하는 컴포넌트만 띄워주려면 어떻게 해야할까요? 일단 if-else문을 사용하여 구현하는 방법이 있습니다.

### FirstComponent.jsx

```
import React from 'react';

export default function FirstComponent({univ = '외대'}) {
    if(univ === '시립대') {
        return null
    }
    else{
        return (
            <div>
                <h1>My First Component</h1>
                <h3>{univ}를 만나면 세계가 보인다</h3>
            </div>
        );
    }
}
```

이렇게 코드를 작성하면, props 값에 따라 렌더링의 여부를 달리 할 수 있습니다.

![스크린샷 2023-05-28 오후 7.52.33.png](Week%205-3%20Components%209aa11e5a0a304c1a85ce70b915ad2fdc/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-05-28_%25E1%2584%258B%25E1%2585%25A9%25E1%2584%2592%25E1%2585%25AE_7.52.33.png)

삼항 연산자를 사용해서도 조건부 렌더링이 가능한데요, 삼항 연산자를 사용하면 다음과 같이 작성할 수 있습니다.

### FirstComponent.jsx

```
import React from 'react';

export default function FirstComponent({univ = '외대'}) {
    
    return (
        <div>
            <h3>{(univ==="시립대") ? null : `${univ}를 만나면 세계가 보인다`}</h3>
        </div>
    );
}
```

![스크린샷 2023-05-28 오후 8.00.29.png](Week%205-3%20Components%209aa11e5a0a304c1a85ce70b915ad2fdc/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-05-28_%25E1%2584%258B%25E1%2585%25A9%25E1%2584%2592%25E1%2585%25AE_8.00.29.png)

> 이번 챕터에서는 뛰어난 재사용성으로 개발자의 생산성을 올려주는 컴포넌트와, 이들의 활용성을 극대화 할 수 있도록 해주는 props, 조건부 렌더링에 대해 배워보았습니다. 앞서 말씀 드렸듯이 컴포넌트는 리액트 코드의 핵심이기 때문에 잘 이해하고 넘어갈 수 있도록 복습해주시길 권장드립니다. 수고 많으셨습니다 !
>