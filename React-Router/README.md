# 설치 방법

```bash
npm install react-router-dom
```

# BrowserRouter 컴포넌트
- src/index.js에서 
```js
import { BrowserRouter } from "react-router-dom";
```
하고 App컴포넌트를 감싼다.
```js
root.render(
  <BrowserRouter>
    <App />
  </BrowserRouter>
);
```

# Routing 하는 방법
```js
import { Route, Routes } from 'react-router-dom';

function App() {
  return (
    <React.Fragment className="App">
      <Routes>
        <Route path='/' element={<Home />} />
        <Route path='/about' element={
          <React.Fragment>
            <About />
            <MenuBar />
          </React.Fragment>
        } />
      </Routes>
    </React.Fragment>
  );
}
```
- `Route` 컴포넌트는 `Routes` 컴포넌트 하위에 넣어줘야 한다.


참고: https://reactrouter.com/en/main/components/routes

# Link 컴포넌트를 이용해서 다른 페이지로 이동하기
- `<a>` 태그보다 `<Link>` 컴포넌트를 사용하는것이 새로고침을 하지 않아 더 자원을 아낄수 있다.
```js
<Link to="/about">Go to about page</Link>
```

참고: https://reactrouter.com/en/main/components/link


# `Route` 컴포넌트를 nested 해서 사용하기
- `Route` 안에 `Route`를 입력하면 내부의 `Route` URL로 이동 할때 외부의 `Route`도 같이 랜더링 된다.
```js
<Routes>
<Route path='/' element={<NavBar />}>
    <Route path='/' element={<Home />} />
    <Route path='/about' element={<About />} />
</Route>
</Routes>
```

- 외부의 컴포넌트에서는 `Outlet` 컴포넌트를 마지막에 더해 줘야 한다.
```js

export default function NavBar() {
    return (
        <React.Fragment>
            <h1>Nav Bar</h1>
            <Outlet />
        </React.Fragment>
    );
}
```

- 참고: https://reactrouter.com/en/main/components/outlet


# Route된 URL이 발견되지 않았을 때 이동하는 페이지 만들기
```js
<Route path='*' element={<NotFound />} />
```
- 여기서 *은 등록되지 않은 모든 URL을 의미한다.

# `useParams`훅을 이용해서 사용자가 입력한 URL의 값을 받아오기
```js
import { useParams } from "react-router-dom";

export default function Profile() {
    const { username } = useParams()
    return (
        <React.Fragment>
            <h1>사용자명: {username}</h1>
        </React.Fragment>
    )
}
```

```js
function App() {
  return (
    <React.Fragment className="App">
      <Routes>
      <Route path='/:username' element={<Profile />} />
      </Routes>
    </React.Fragment>
  );
}
```

# `useNavigate` 훅을 이용하여 특정 페이지로 이동하는 자바스크립트 코드 만들기
- `Link` 컴포넌트와 같은 기능을 하지만, `Link`는 JSX 컴포넌트이고 `useNavigate`은 자바스크립트에서 사용할 수 있는 코드이다.

```js
import {useNavigate} from "react-router-dom"

setTimeout(() => {
    navigate("/about")
}, 3000); // 3초후 about 페이지로 이동
```

- 참고: https://reactrouter.com/en/main/hooks/use-navigate#usenavigate

# `Navigate` 컴포넌트를 이용해서 URL을 이동하기
- `useNavigate`훅과 같은 기능을 하지만 JSX이다.

```js
import { Navigate } from 'react-router-dom';

function App() {

  const [userName, setUserName] = useState("")
  const [loggedIn, setLoggedIn] = useState(false)

  return (
    <React.Fragment className="App">
      <Routes>
        <Route path='/account/:accountname' element={loggedIn ? <LoggedInPage username={userName} /> : <Navigate to={'/login'} />} />
      </Routes>
    </React.Fragment>
  );
}
```

- 참고: https://reactrouter.com/en/main/components/navigate


# routes.js를 만들어서 route하기
1) src 폴더에 `routes.js` 파일을 만든다
```js
const routeList = [
    {
        path: "/",
        component: Home,
        requiresAuth: false
    },
    {
        path: "/login",
        component: Login,
        requiresAuth: false
    }, {
        path: "/about",
        component: About,
        requiresAuth: false
    },
    {
        path: "*",
        component: NotFound,
        requiresAuth: false
    },
    {
        path: "/account/:username",
        component: Profile,
        requiresAuth: true
    }
]

export default routeList
```
2) `App.js`안의 `Routes` 안에 `routeList`를 map 하기
```js
import routeList from './routes';

function App() {

  const [userName, setUserName] = useState("")
  const [loggedIn, setLoggedIn] = useState(false)

  return (
    <Routes>
      {
        routeList.map((route) => {
          if (route.requiresAuth && !loggedIn) {
            return (<Route key={route.path} path={route.path} element={<Navigate to={"/login"} />} />)
          } else {
            return (<Route key={route.path} path={route.path} element={<route.component accountStatus={setLoggedIn} userName={setUserName} />} />)
          }
        })
      }
    </Routes>
  );
}
```

