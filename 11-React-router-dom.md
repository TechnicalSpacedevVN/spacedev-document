# react-router-dom : Thư viện làm single page application

# React-router-dom là gì?

- React-router-dom là thư viện quản lý router (các link trên website) giúp tạo ra 1 trang Single Page Application (SPA) - bấm link không đổi trang 1 cách dễ dàng

## Cài đặt:

> <font size="5">yarn add react-router-dom</font>

## Cách sử dụng

- Bước 1: Gắn Provider `App.js`

- Bước 2: Những page sẽ nằm trong 1 `Route`

- Bước 3: Những tag `a` sẽ thay bằng component `Link`

- Bước 4: Sử dụng `Switch` để chọn 1 page duy nhất được render

```jsx
    import React from "react";
    import {
        BrowserRouter as Router,
        Switch,
        Route,
        Link,
        useParams,
        useRouteMatch
    } from "react-router-dom";

    export default function App() {
        return (
            <Router>
                <div>
                    <ul>
                        <li>
                            <Link to="/">Home</Link>
                        </li>
                        <li>
                            <Link to="/about">About</Link>
                        </li>
                        <li>
                            <Link to="/dashboard">Dashboard</Link>
                        </li>
                    </ul>
                    <hr />
                    <Switch>
                        <Route exact path="/">
                            <Home />
                        </Route>
                        <Route path="/about">
                            <About />
                        </Route>
                        <Route path="/dashboard">
                            <Dashboard />
                        </Route>

                        <Route path="/about">
                            <Profile />
                        </Route>

                        {/* Router params */}
                        <Route path="/:id" children={<Child />} />

                        {/* Nesting routers */}
                        <Route path="/topics">
                            <Topics />
                        </Route>
                    </Switch>
                </div>
            </Router>
        );
    }

    // You can think of these components as "pages"
    // in your app.

    function Home() {
        return (
            <div>
                <h2>Home</h2>
            </div>
        );
    }

    function About() {
        return (
            <div>
                <h2>About</h2>
            </div>
        );
    }

    function Dashboard() {
        return (
            <div>
                <h2>Dashboard</h2>
            </div>
        );
    }

    function Profile() {
        const [login, setLogin] = useState(false)
        if(!login) return <Redirect />
        return (
            <div>
                <h2>Profile</h2>
            </div>
        );
    }

    function Child() {
        // Lấy id từ param url
        let { id } = useParams();

        return (
            <div>
            <h3>ID: {id}</h3>
            </div>
        );
    }

    function Topics() {
        // The `path` lets us build <Route> paths that are
        // relative to the parent route, while the `url` lets
        // us build relative links.
        let { path, url } = useRouteMatch();

        return (
            <div>
            <h2>Topics</h2>
            <ul>
                <li>
                    <Link to={`${url}/rendering`}>Rendering with React</Link>
                </li>
                <li>
                    <Link to={`${url}/components`}>Components</Link>
                </li>
                <li>
                    <Link to={`${url}/props-v-state`}>Props v. State</Link>
                </li>
            </ul>

            {/* child router */}
            <Switch>
                <Route exact path={path}>
                    <h3>Please select a topic.</h3>
                </Route>
                <Route path={`${path}/:topicId`}>
                    <Topic />
                </Route>
            </Switch>
            </div>
        );
    }
```