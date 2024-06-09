# Week 9-1. React Router

생성일: June 9, 2024 2:46 AM

오늘은 React를 사용하여 웹페이지를 개발할 때 생산성을 높여주는 라이브러리 중 선두주자인 React Router와 React Query를 배웁니다. 이번 시간에는 React Router를 먼저 배워봅시다.

# React Router란?

React Router는 웹에서 페이지 간 이동(라우팅) 기능을 구현하는데 큰 도움을 주는 라이브러리입니다. 이전에 JavaScript 세션 중 애플리케이션 개발 패러다임 중에서 MPA와 SPA를 배웠던 기억을 되살려봅시다. React Router는 SPA 패러다임을 가능케 하는 도구이며 다이나믹한 UX를 제공할 수 있게 도와줍니다. 백문이 불여일견, 바로 튜토리얼로 넘어갑시다.

## 튜토리얼

우리는 이번 시간 아래와 같이 자그마한 앱을 하나 만들어볼겁니다. 그러기 위해선 먼저 셋업이 필요합니다.

![Untitled](Week%209-1%20React%20Router%20b8f00590795d4e29b0bea9d55f57c95f/Untitled.png)

## Setup

우리는 이 튜토리얼에서 [Vite](https://vitejs.dev/guide/)를 번들러 및 dev 서버로 사용할 예정입니다. `npm` 커맨드를 사용하려면 [Node.js](https://nodejs.org/)가 설치돼있어야 합니다.

👉️ **터미널을 열고 Vite를 통한 새 React 앱을 만들어보세요:**

```
npm create vite@latest name-of-your-project -- --template react
# follow prompts
cd <your new project directory>
npm install react-router-dom localforage match-sorter sort-by
npm run dev

```

그러면 터미널에 프린트되는 URL을 접속할 수 있어야 합니다:

```
 VITE v3.0.7  ready in 175 ms

  ➜  Local:   http://127.0.0.1:5173/
  ➜  Network: use --host to expose
```

이번 튜토리얼은 디자인보다 React Router의 기능들을 경험하는데 집중하기 위해 미리 작성된 CSS를 사용하시기 바랍니다.

**👉 [여기서](https://gist.githubusercontent.com/ryanflorence/ba20d473ef59e1965543fa013ae4163f/raw/499707f25a5690d490c7b3d54c65c65eb895930c/react-router-6.4-tutorial-css.css) `src/index.css`에 붙여넣을 튜토리얼 CSS를 복붙하세요.**

이 튜토리얼은 데이터를 만들고/읽고/찾고/업데이트 혹은 지우는 작업을 할 것입니다. 일반적인 웹 앱은 아마 여러분의 웹서버 API를 가져와 사용하겠지만, 우리는 대신 브라우저 스토리지를 사용하고 네트워크 레이턴시를 임의로 만들어 사용할 것입니다. 예시 코드들은 React Router와 관련이 없으니 마음껏 복붙하셔도 됩니다.

**👉 [여기서](https://gist.githubusercontent.com/ryanflorence/1e7f5d3344c0db4a8394292c157cd305/raw/f7ff21e9ae7ffd55bfaaaf320e09c6a08a8a6611/contacts.js) `src/contacts.js`에 붙여넣을 튜토리얼 데이터 모듈을 복붙하세요.**

여러분이 src 폴더에 남겨놓을 파일은 `contacts.js`, `main.jsx` 그리고 `index.css`입니다. 나머지는 다 지워주세요(`App.js`나 `assets` 같은 파일 등등).

👉 **그래서 불필요한 파일들을 다 지운** **`src/` 폴더는 아래와 같아야 합니다:**

```
src
├── contacts.js
├── index.css
└── main.jsx
```

## Router 추가하기

가장 먼저 할 것은 [Browser Router](https://reactrouter.com/en/main/routers/create-browser-router)를 만드는 것이고 우리의 첫 route를 설정하는 것입니다. 이는 우리 웹앱에서 클라이언트 사이드 라우팅이 가능토록 해줍니다.

`main.jsx` 파일이 엔트리 포인트입니다. React Router를 결합하도록 `main.jsx` 를 열어보세요.

👉 **`main.jsx`를 열고 [browser router](https://reactrouter.com/en/main/routers/create-browser-router)를 아래와 같이 작성해보세요.**

```jsx
// src/main.jsx
import * as React from "react";
import * as ReactDOM from "react-dom/client";
**import {
  createBrowserRouter,
  RouterProvider,
} from "react-router-dom";**
import "./index.css";

**const router = createBrowserRouter([
  {
    path: "/",
    element: <div>Hello world!</div>,
  },
]);**

ReactDOM.createRoot(document.getElementById("root")).render(
  <React.StrictMode>
    **<RouterProvider router={router} />**
  </React.StrictMode>
);
```

방금 작성한 첫번째 route는 우리가 흔히 부르는 ‘root route’입니다. 우리가 작성할 나머지 route들이 이 안에서 렌더링되는 것이죠. 앞으로 작성할 route들은 중첩된(nested) 레이아웃처럼 작동되며, `main.jsx` 의 코드는 UI의 ‘root layout’처럼 작동할 것입니다.

## The Root Route

글로벌 레이아웃을 적용해볼까요?

**👉 `src/routes` 와 `src/routes/root.jsx`를 만들어보세요.**

```
mkdir src/routes
touch src/routes/root.jsx
(너드처럼 터미널에 커맨드라인을 입력하고 싶지 않으면, 마우스로 직접 파일을 생성하세요🤓)
```

**👉 root layout 컴포넌트를 만드세요.**

```jsx
// src/routes/root.jsx
export default function Root() {
  return (
    <>
      <div id="sidebar">
        <h1>React Router Contacts</h1>
        <div>
          <form id="search-form" role="search">
            <input
              id="q"
              aria-label="Search contacts"
              placeholder="Search"
              type="search"
              name="q"
            />
            <div
              id="search-spinner"
              aria-hidden
              hidden={true}
            />
            <div
              className="sr-only"
              aria-live="polite"
            ></div>
          </form>
          <form method="post">
            <button type="submit">New</button>
          </form>
        </div>
        <nav>
          <ul>
            <li>
              <a href={`/contacts/1`}>Your Name</a>
            </li>
            <li>
              <a href={`/contacts/2`}>Your Friend</a>
            </li>
          </ul>
        </nav>
      </div>
      <div id="detail"></div>
    </>
  );
}
```

**👉 `main.jsx`의 `<Root>`를 root route의 `element`로 설정하세요.**

```jsx
// src/main.jsx
/* existing imports */
**import Root from "./routes/root";**

const router = createBrowserRouter([
  {
    path: "/",
    **element: <Root />,**
  },
]);

ReactDOM.createRoot(document.getElementById("root")).render(
  <React.StrictMode>
    <RouterProvider router={router} />
  </React.StrictMode>
);
```

그러면 여러분의 페이지는 아래와 같이 보여져야 합니다. 나쁘지 않은 CSS같죠?

![Untitled](Week%209-1%20React%20Router%20b8f00590795d4e29b0bea9d55f57c95f/Untitled%201.png)

## Not Found 에러 핸들링하기

프로젝트에서 에러에 대처하는 방법을 알고 있는 것은 항상 좋은 아이디어입니다. 유저들에게 좋은 경험을 선사할 수 있을 뿐만 아니라, 개발 단계에서 여러분도 도움을 받을 수 있습니다.

React Router 팀에서 몇 개의 링크를 추가해놨는데, 그걸 클릭하면 어떤 일이 벌어지는지 한 번 봅시다.

**👉 사이드바에 있는 아무 블럭이나 클릭해보세요.**

![Untitled](Week%209-1%20React%20Router%20b8f00590795d4e29b0bea9d55f57c95f/Untitled%202.png)

와우! 이 화면은 React Router의 디폴트 에러 화면입니다. root element의 flex box 스타일 때문에 더 기괴해졌네요 😂

렌더링 중이거나, 데이터를 로딩하는 중이거나, 데이터 mutation 수행 등 여러 상황에서 여러분의 앱이 에러를 뱉어낼 때마다 React Router는 이를 캐치하고 에러 화면을 렌더링해줄 것입니다. 이제 우리만의 에러 페이지를 만들어봅시다.

👉 **error 페이지 컴포넌트를 만들어봅시다.**

```jsx
// touch src/error-page.jsx

import { useRouteError } from "react-router-dom";

export default function ErrorPage() {
  const error = useRouteError();
  console.error(error);

  return (
    <div id="error-page">
      <h1>Oops!</h1>
      <p>Sorry, an unexpected error has occurred.</p>
      <p>
        <i>{error.statusText || error.message}</i>
      </p>
    </div>
  );
}
```

👉 **`<ErrorPage>` 를 root route의 [`errorElement`](https://reactrouter.com/en/main/route/error-element) 로 설정해주세요.**

```jsx
/* src/main.jsx */
...
**import ErrorPage from "./error-page";**

const router = createBrowserRouter([
  {
    path: "/",
    element: <Root />,
    **errorElement: <ErrorPage />,**
  },
]);

ReactDOM.createRoot(document.getElementById("root")).render(
  <React.StrictMode>
    <RouterProvider router={router} />
  </React.StrictMode>
);
```

그럼 아래와 같은 화면이 나와야 합니다.

![Untitled](Week%209-1%20React%20Router%20b8f00590795d4e29b0bea9d55f57c95f/Untitled%203.png)

이 페이지에서 보이는 에러는 [`useRouteError`](https://reactrouter.com/en/main/hooks/use-route-error)가 반환한 에러란 점을 유의하세요. 유저가 존재하지 않는 route로 이동할 경우 여러분은 “Not Found”란 `statusText`로 이뤄진 [error response](https://reactrouter.com/en/main/utils/is-route-error-response)를 받게 됩니다. 추후 뒤에서 다른 에러들을 통해 더 자세히 이야기해보죠.

지금은 이 조치만으로도 여러분이 경험하는 대부분의 에러들을 해결할 수 있습니다(무한 로딩, unresponsive한 페이지나 텅 빈 스크린이 여러분을 기다리고 있습니다 🙌).

## The Contact Route UI

404 “Not Found” 페이지 대신에 우리는 제대로 링크된 렌더링을 할 예정입니다. 따라서 새로운 route를 만들어야 합니다.

👉 **contact route 모듈을 만들어보세요.**

```
touch src/routes/contact.jsx
```

👉 **contact 컴포넌트 UI를 추가해보세요.**

```jsx
// src/routes/contact.jsx

import { Form } from "react-router-dom";

export default function Contact() {
  const contact = {
    first: "Your",
    last: "Name",
    avatar: "https://placekitten.com/g/200/200",
    twitter: "your_handle",
    notes: "Some notes",
    favorite: true,
  };

  return (
    <div id="contact">
      <div>
        <img
          key={contact.avatar}
          src={contact.avatar || null}
        />
      </div>

      <div>
        <h1>
          {contact.first || contact.last ? (
            <>
              {contact.first} {contact.last}
            </>
          ) : (
            <i>No Name</i>
          )}{" "}
          <Favorite contact={contact} />
        </h1>

        {contact.twitter && (
          <p>
            <a
              target="_blank"
              href={`https://twitter.com/${contact.twitter}`}
            >
              {contact.twitter}
            </a>
          </p>
        )}

        {contact.notes && <p>{contact.notes}</p>}

        <div>
          <Form action="edit">
            <button type="submit">Edit</button>
          </Form>
          <Form
            method="post"
            action="destroy"
            onSubmit={(event) => {
              if (
                !confirm(
                  "Please confirm you want to delete this record."
                )
              ) {
                event.preventDefault();
              }
            }}
          >
            <button type="submit">Delete</button>
          </Form>
        </div>
      </div>
    </div>
  );
}

function Favorite({ contact }) {
  // yes, this is a `let` for later
  let favorite = contact.favorite;
  return (
    <Form method="post">
      <button
        name="favorite"
        value={favorite ? "false" : "true"}
        aria-label={
          favorite
            ? "Remove from favorites"
            : "Add to favorites"
        }
      >
        {favorite ? "★" : "☆"}
      </button>
    </Form>
  );
}
```

편하게 복붙하셔도 됩니다. 복붙을 끝내셨으면, 새 Route로 연결을 해봅시다.

👉 **contact 컴포넌트를 `main.jsx`에 Import하고 새 route를 만들어보세요.**

```jsx
// src/main.jsx

/* existing imports */
**import Contact from "./routes/contact";**

const router = createBrowserRouter([
  {
    path: "/",
    element: <Root />,
    errorElement: <ErrorPage />,
  },
  **{
    path: "contacts/:contactId",
    element: <Contact />,
  },**
]);

/* existing code */
```

그러면 이제 `/contacts/1`를 방문했을 때 아래와 같은 화면이 나타나게 됩니다!

![Untitled](Week%209-1%20React%20Router%20b8f00590795d4e29b0bea9d55f57c95f/Untitled%204.png)

하지만 이 컴포넌트는 root layout 안에 들어와있지 않네요 😠

## Nested Routes

우리는 아래와 같이 `<Root>` 레이아웃 안에 contact 컴포넌트가 들어와있기를 원합니다.

![Untitled](Week%209-1%20React%20Router%20b8f00590795d4e29b0bea9d55f57c95f/Untitled%205.png)

그렇게 하기 위해 contact route를 root route의 *child*로 만들어야 합니다.

👉 **contacts route를 root route의 child가 되도록 이동시켜보세요.**

```jsx
// src/main.jsx

const router = createBrowserRouter([
  {
    path: "/",
    element: <Root />,
    errorElement: <ErrorPage />,
    **children: [
      {
        path: "contacts/:contactId",
        element: <Contact />,
      },
    ],**
  },
]);
```

그러면 여러분은 오른쪽 텅 빈 화면이 있는 root layout을 보게 될 겁니다. 여러분은 root route에게 child routes가 *어디로* 렌더링되기를 원하는지 말해줘야 합니다. 그것을 `<Outlet>`으로 수행합니다.

`<div id="detail">`을 찾고 outlet을 안쪽에 삽입해주세요.

```jsx
// src/routes/root.jsx

**import { Outlet } from "react-router-dom";**

export default function Root() {
  return (
    <>
      {/* all the other elements */}
      <div id="detail">
        **<Outlet />**
      </div>
    </>
  );
}
```

## 클라이언트 사이드 라우팅

눈치채셨을지 모르겠지만, 우리가 사이드바의 링크를 클릭할 때 브라우저는 React Router를 사용하는 대신 document request를 통째로 수행하고 있습니다.

클라이언트 사이드 라우팅은 여러분의 앱이 서버로부터 또다른 document를 requesting하는 일 없이 URL을 업데이트하는 것을 가능하게 해줍니다. 대신 새 UI를 바로 렌더링할 수도 있습니다. `<Link>`와 함께 어떤 일이 벌어지는지 확인해봅시다.

**👉 사이드바의 `<a href>` 를 `<Link to>`으로 바꿔보세요.**

```jsx
// src/routes/root.jsx

**import { Outlet, Link } from "react-router-dom";**

export default function Root() {
  return (
    <>
      <div id="sidebar">
        {/* other elements */}

        <nav>
          <ul>
            <li>
              **<Link to={`contacts/1`}>Your Name</Link>**
            </li>
            <li>
              **<Link to={`contacts/2`}>Your Friend</Link>**
            </li>
          </ul>
        </nav>

        {/* other elements */}
      </div>
    </>
  );
}
```

개발자 도구에서 network 탭을 열어 document request가 불필요하게 일어나는지 확인해보세요.

---

## 이번 튜토리얼은 여기까지!

자, 어떤가요? React Router 라이브러리를 사용함으로써 귀찮은 설정들을 하지 않아도 알아서 작동하니 편하지 않나요? 나머지 튜토리얼은 여러분이 직접 도큐먼트를 읽으면서 따라가보세요! 절반 정도 왔으니 나머지 절반은 아마 금방 따라하실 수 있을겁니다. 좀 더 지엽적이고 구체적인 사용 사례가 나와있으니 React Router를 프로젝트에서 사용하다가 필요한 기능이 생길 때 와서 찾아보셔도 됩니다.

다음 시간에는 React Query를 배워봅시다.