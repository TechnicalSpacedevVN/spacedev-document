# react-router-dom : Thư viện làm single page application

# React-router-dom là gì?

- React-router-dom là thư viện quản lý router (các link trên website) giúp tạo ra 1 trang Single Page Application (SPA) - bấm link không đổi trang 1 cách dễ dàng

## Cài đặt:

> <font size="5">yarn add react-router-dom</font>

## Cách sử dụng

- Bước 1: Gắn `BrowserRouter` vào `App.js`

- Bước 2: Những page sẽ nằm trong 1 `Route`

- Bước 3: Những tag `a` sẽ thay bằng component `Link`, `NavLink`

- Bước 4: Sử dụng `Routes` để chọn 1 page duy nhất được render

# Ví dụ tổng hợp

```jsx
    import { useState } from "react";
    import {
        BrowserRouter,
        Route,
        Routes,
        Navigate,
        useParams,
        Link,
        Outlet,
    } from 'react-router-dom'
    import NotFound from './pages/notFound'

    export default function App() {
        return (
            <BrowserRouter>
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
                        <li>
                            <Link to="/profile">Profile</Link>
                        </li>
                        <li>
                            <Link to="/32">URL Params</Link>
                        </li>
                        <li>
                            <Link to="/topics ">Topics</Link>
                        </li>
                    </ul>
                    <hr />
                    <Routes>
                        <Route path="/" element={<Home />} />
                        <Route element={<Layout />}>
                            <Route path="/about" element={<About />} />
                            <Route path="/dashboard" element={<Dashboard />} />
                            <Route path="/profile" element={<Profile />} />
                        </Route>

                        {/* Router params */}
                        <Route path="/:id" element={<Child />} />

                        {/* Nesting routers */}
                        <Route path="/topics/*" element={<Topics />} />

                        <Route path="*" element={<NotFound />} />
                    </Routes>
                </div>
            </BrowserRouter>
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
        const [login, setLogin] = useState(true)
        if (!login) return <Navigate to="/" />
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

    function Layout() {
        return <div>
            <div>Header</div>
                <Outlet />
            <div>Footer</div>
        </div>
    }

    function Topics() {
        // The `path` lets us build <Route> paths that are
        // relative to the parent route, while the `url` lets
        // us build relative links.

        return (
            <div>
                <h2>Topics</h2>
                <ul>
                    <li>
                        <Link to={`rendering`}>Rendering with React</Link>
                    </li>
                    <li>
                        <Link to={`components`}>Components</Link>
                    </li>
                    <li>
                        <Link to={`props-v-state`}>Props v. State</Link>
                    </li>
                </ul>
                <Outlet />
                {/* child router */}
                <Routes>
                    <Route index element={<h3>Please select a topic.</h3>} />
                    <Route path={`:topicId`} element={<Topics />} />
                </Routes>
            </div>
        );
    }
```


## Trên lớp 

- chia router theo site map sau:

    Home \
    |\
    About \
    |\
    Contact US \
    |\
    View Cart\
    |\
    Checkout\
    |\
    Checkout Success\
    |\
    Login\
    |\
    Register\
    |\
    Forgot password\
    |\
    Reset password\
    |\
    Profile\
    |    |_My profile\
    |    |_Order\
    |    |_Order Detail\
    |    |_Payment\
    |    |_Payment detail\
    |    |_Address\
    |    |_Address detail

## Về nhà

- Chia router cho các trang của dự án

- Cắt và hoàn thành trang chủ
