# Week 5-1. What’s React?

생성일: June 9, 2024 2:46 AM

![react-meme1_.png](Week%205-1%20What%E2%80%99s%20React%2092ad0ad6e2c548308572b456a8de75de/react-meme1_.png)

> JavaScript를 통해 성공적인 첫 걸음을 내딛으신 FE 트랙 여러분 반갑습니다. 이제 프론트엔드 개발의 초석이 되는 React에 대해 공부해 볼텐데요. 오늘은 React가 무엇인지 알아보고, JS와 닮은 듯 다른 JSX 문법, 그리고 React 코드의 핵심인 Components에 대해 배워보겠습니다. 그럼 레츠 고🧚‍♂️
> 

## What’s React?

![react-js.png](Week%205-1%20What%E2%80%99s%20React%2092ad0ad6e2c548308572b456a8de75de/react-js.png)

React(React.js)는 SPA(Single Page Application)을 위한 사용자 인터페이스(UI)를 구축하는 데 사용되는 오픈 소스 JavaScript 입니다. 여기서 SPA란 최초 한번 전체 페이지를 다 불러온 후, 필요시 페이지 특정 부분만 불러와서 변경해주는 방식을 의미합니다. 

[화면 기록 2023-05-26 오후 5.44.02.mov](Week%205-1%20What%E2%80%99s%20React%2092ad0ad6e2c548308572b456a8de75de/%25E1%2584%2592%25E1%2585%25AA%25E1%2584%2586%25E1%2585%25A7%25E1%2586%25AB_%25E1%2584%2580%25E1%2585%25B5%25E1%2584%2585%25E1%2585%25A9%25E1%2586%25A8_2023-05-26_%25E1%2584%258B%25E1%2585%25A9%25E1%2584%2592%25E1%2585%25AE_5.44.02.mov)

네이버 홈페이지를 한 번 볼까요? 화면에 변화가 생겼음에도 페이지가 새로고침 되지 않는 것을 보실 수 있습니다. 이건 페이지 구성요소 중 필요한 부분만 새로 불러올 수 있기 때문에 가능한 모습입니다. 이러한 성질 때문에 React를 사용하면 페이지를 다시 로드하지 않고도 데이터를 변경할 수 있는 대규모 웹 애플리케이션을 만들 수 있습니다(서버의 과부하를 줄여주는 프론트 라이브러리라니 .. 인류애적이죠). 

또한 UI는 버튼, 텍스트, 이미지와 같은 여러 작은 단위로 구성되는데요, React를 사용하면 이들을 재사용 가능하고 중첩 가능한 요소로서 결합하여 사용할 수 있게됩니다. 이러한 구조를 component 기반 구조라고 부르는데요, 프론트엔드 개발자가 웹 및 모바일 앱의 view layer를 만들 때 높은 생산성을 가져다줍니다.

### 그럼 이런 멋진 라이브러리를 한 번 사용해볼까요 ?👨‍🎨

> React 프로젝트를 실행하기 전에 두 가지 항목을 우선 설치 해주셔야합니다.
> 

### **Node.js**

Windows 의 경우엔, [Node.js 공식 홈페이지](https://nodejs.org/) 에서 좌측에 나타나는 LTS 버전을 설치해주세요.

macOS / Linux 의 경우엔, [nvm](https://github.com/nvm-sh/nvm) 이라는 도구를 사용하여 Node.js 를 설치하시는 것을 권장드립니다.

```
$ curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.33.8/install.sh | bash
$ nvm install --lts

```

### **Yarn**

만약 npm 이 이미 익숙하고, yarn 을 설치하기 귀찮다면 생략을 하셔도 상관없습니다.

yarn 설치는 Yarn 공식 홈페이지의 [Install Yarn](https://yarnpkg.com/en/docs/install) 페이지를 참고하세요.

## **새 프로젝트 만들어보기**

새로운 리액트 프로젝트를 만들어봅시다. 새 폴더를 생성하여 VS Code로 연 뒤, 터미널에서 다음 명령어를 실행해보세요.

```
$ npx create-react-app begin-react
```

그러면 begin-react 라는 디렉터리가 생기고 그 안에 리액트 프로젝트가 생성됩니다. 생성이 끝나면 cd 명령어를 사용하여 해당 디렉터리에 들어간 다음 `yarn start` 명령어를 입력해보세요 (yarn 이 없다면 `npm start`).

```
$ cd begin-react
$ yarn start
```

이 명령어를 실행하고 나면 다음과 같이 브라우저에 [http://localhost:3000/](http://localhost:3000/) 이 열리고, 돌아가는 리액트 아이콘이 보일 것입니다. 자동으로 페이지가 열리지 않는다면 브라우저에 주소를 직접 입력하여 들어가세요.

![https://i.imgur.com/6Mw3rve.png](https://i.imgur.com/6Mw3rve.png)

![https://i.imgur.com/E6DgKVH.png](https://i.imgur.com/E6DgKVH.png)

> 이렇듯 React app을 성공적으로 실행 해보았습니다. 그럼 이 React app을 어떤 방식으로 채워줄 것인지 이어서 배워볼까요?🏃
>