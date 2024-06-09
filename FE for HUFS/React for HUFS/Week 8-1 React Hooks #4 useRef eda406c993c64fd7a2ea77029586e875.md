# Week 8-1. React Hooks #4. useRef

생성일: June 9, 2024 2:46 AM

이번 시간엔 useRef를 배워봅시다.

## useRef란 무엇인가?

우리가 React로 크고 작은 컴포넌트를 만들고 연결해 웹페이지를 만들 때, 앞서 배웠던 state를 조작하는 Hook들로는 컴포넌트 외부에 영향을 미치는 작업을 다루기 어려울 수 있습니다. 예를 들어 input DOM을 조작하는 것을 `useState`로 하게 된다면 state에 변화가 일어날 때마다 리렌더링이 발생하기 때문에 원치않는 새로고침으로 사용자의 input을 제대로 입력받을 수 없게 되죠. 따라서 특정 요소 혹은 데이터의 변화를 리렌더링 없이 추적하고 싶을 때 우리는 `useRef`를 사용하게 됩니다.

`useState`와 `useRef`는 그 쓰임새가 굉장히 비슷합니다. 따라서 React를 처음 배울 때에는 `useRef`의 정확한 사용 목적이 와닿지 않을 수 있고 ‘그냥 `useState` 쓰면 똑같이 구현되는거 아니야?’라고 생각할 수 있습니다. 이 글을 쓰는 저도 그러했구요.

하지만 `useRef`는 `useState`와 구별되는 뚜렷한 쓰임새가 있습니다. `useState` Hook은 말그대로 state를 하나 만들어서 그 상태에 여러가지 액션들을 ‘걸고’, 한 상태에 변화가 생길 때마다 해당 상태에 연결돼있는 요소들에 변화를 주는 방식입니다. `useRef`는 이 Hook의 naming에서처럼 내가 추적하고 싶은 요소에 ‘Reference’란 일종의 ‘태그’를 달아놓는 것으로 이해하시면 됩니다. `useState`에 비해 좀 더 구체적이고 명확하죠. 이 둘 사이의 차이점을 아래 React 공식문서를 들여다보면서 이해해봅시다.

[https://react-ko.dev/learn/referencing-values-with-refs](https://react-ko.dev/learn/referencing-values-with-refs)

[https://react-ko.dev/learn/manipulating-the-dom-with-refs](https://react-ko.dev/learn/manipulating-the-dom-with-refs)

자, 어떤가요? 이제 `useRef`와 `useState`의 차이점을 이해하시겠나요?

한 번 더 보기 쉽게 정리하자면, 아래와 같습니다.

| useState | useRef |
| --- | --- |
| const [ 상태명, set상태함수 ] = useState(initialState) | const 변수명 = useRef(initialValue)
// return { current: initialValue } |
| 변경 시 리렌더링을 촉발함 | 값이 변경되어도 리렌더링을 촉발하지 않음 |
| ‘Immutable’ - state를 직접 수정해선 안됨(React가 인식하지 못하는 변경은 금지). 대신 set 함수를 사용해 state 자체를 교체해 리렌더링을 대기열에 추가함. | ‘Mutable’ - 렌더링 프로세스와 독립적인 공간에서 ref의 current 값을 얼마든지 변경할 수 있음. state처럼 특별한 React 요소가 아닌 일반 Javascript 객체라고 생각하는게 편함. |
| state가 변경될 시 snapshot이 찍히고 리렌더링은 그 스냅샷을 기준으로 발동됨. | 별도의 snapshot이 존재하지 않고 리렌더링 되는 시점의 current 값을 기준으로 발동됨. |
| 컴포넌트 내부에서 동작하도록 최적화돼있음. | 컴포넌트 외부의 요소들을 추적하는데 최적화돼있음. |

`useRef`를 잘 활용한다면 불필요한 리렌더링을 줄이고 내가 추적하고자 원하는 요소에 알맞은 값을 수정하거나 저장할 수 있습니다. 모든게 그렇듯 이론보다 중요한 것은 실제 경험입니다. 각자의 토이프로젝트에 `useRef`를 직접 적용해보면서 무슨 역할을 하는 Hook인지 체험해보세요! 다음 시간은 `useEffect`를 배워보도록 하겠습니다.