# Week 8-2. React Hooks #5. useEffect

생성일: June 9, 2024 2:46 AM

## useEffect란 무엇인가?

`useEffect` 훅은 여러분들이 리액트 중급자가 된다면 꽤나 자주 쓰게 될 훅입니다. 자세히 살펴보기 전 가볍게 이해하자면 `useEffect` 훅을 사용하면 렌더링 발생 이후에 실행되어야 하는 “사이드 이펙트”를 의도적으로 지연시킨 뒤 실행시킬 수 있습니다.

공식문서를 살펴보면 알게 되겠지만 `useEffect` 훅을 사용할 때엔 설정해줘야하는 조건들이 꽤나 있습니다. `useEffect`가 발동될 조건을 나타내는 “의존성 배열”, 불필요하게 남아있는 사이드 이펙트를 꺼줄 수 있는 “클린업 함수” 등이 있죠.

이제 공식문서를 살펴보면서 `useEffect` 훅에 대해 개괄적으로 알아보고, 이 훅을 사용하면 무엇을 할 수 있는지 알아봅시다.

[https://react-ko.dev/learn/synchronizing-with-effects](https://react-ko.dev/learn/synchronizing-with-effects)

어떤가요? useEffect 가 어떤 훅인지 감이 잡히시나요?

페이지가 처음 로드될 때 일괄적으로 Cascading 순서로 위에서부터 아래까지 렌더링이 될 때, useEffect를 사용하면 첫 렌더링 시 실행되지 않고 렌더링 이후 - 커밋 이전 타이밍으로 실행 순서를 유보할 수 있습니다. 또한 의존성 배열을 사용하면 항상 사이드 이펙트가 실행되는 것이 아니라 정말 필요할 때만 조건적으로 실행시킬 수도 있죠.

그래서 useEffect를 남발하는 시기가 찾아옵니다. 저 또한 useEffect를 무분별하게 사용했던 적이 있었구요, 무분별하게 사용하다보면 소위 ‘무한루프’에 빠지는 경험을 하게 됩니다. ‘응? 내 예상대로라면 한 번만 호출되고 끝나야하는데 왜 물리고 물려서 무한 렌더링이 일어나는거지?’ 하며 진땀을 빼게 되죠.

그럴 때 비로소 useEffect의 Lifecycle과 의존성 배열, clean-up 함수의 필요성을 느끼게 되고, React 공식문서의 다른 useEffect 아티클을 읽을 시기가 된 것입니다. 필요하다면 공식문서를 읽어보세요. 장담컨데 구글링해서 찾을 수 있는 그 어떤 블로그 내용보다 정돈돼있으면서 여러분이 필요한 지식들이 모두 잘 정리돼있습니다. 일단 한 번 써보시고, 부딫혀본 다음 궁금증을 해소해나가는 방식으로 접근해보세요!

[https://react-ko.dev/learn/lifecycle-of-reactive-effects](https://react-ko.dev/learn/lifecycle-of-reactive-effects)