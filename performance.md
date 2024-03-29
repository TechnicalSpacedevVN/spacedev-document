# useMemo, memo, useCallback

# Tối ưu dự án Reactjs

- Là quá trình tối ưu dự án Reactjs bằng cách sử dụng những kỹ thuật nâng cao nhầm hạn chế số lần re-render không cần thiết của 1 component hoặc việc tạo ra các biến dư thừa trong mỗi lần component được re-render


# React.memo

- Khi component re-render sẽ kéo theo component con re-render, mặc dù sẽ có những component con không cần re-render (prop không thay đổi)

- Sử dụng React.memo giãm lượt re-render không cần thiết



```jsx
    import Header from 'components/Header'

    export const App = () => {
        const [count, setCount] = useState(0)
        const [count2, setCount2] = useState(0)

        useEffect(() => {
            setTimeout(() => {
                setCount(count + 1)
            }, 1000)
        }, [count])
        console.log('App re-render')

        return (
            <div>
                <Header count={count2}/>
                {count} <br />
                <Button onClick={() => setCount2(count2 + 1)}>Count2 +</Button>
            </div>
        )
    }
```

```jsx
    // components/Header

    const Header = ({ count }) => {
        console.log('Header re-render')
        return <div>Header count: {count}</div>
    }

    export default React.memo(Header)
```

- Khi component App re-render do count, Header sẽ không cần re-render lại bởi vì việc re-render đó là không cần thiết 

- Khi component App re-render do count2, Header cần re-render lại để cập nhất giá trị prop mới truyền vào

- React.memo sẽ tự động kiểm tra tất cả các prop truyền vào và so sánh với giá trị cũ, nếu khác nhau sẽ tiến hành re-render và ngược lại

# useMemo

- Sử dụng khi muốn cache một giá trị nào đó có tính toán nhiều trong 1 component

- Việc run lại phụ thuộc vào dependencyList có thay đổi hay không

```jsx

    import { useMemo, useState } from 'react'

    export const Count = () => {
        const [count, setCount] = useState(0)
        const [count2, setCount2] = useState(0)

        const fibonaciFn = (number) => {
            let n1 = 0, n2 = 1, nextTerm;
            let res = []
            for (let i = 1; i <= number; i++) {
                console.log(n1)
                res.push(n1)
                nextTerm = n1 + n2;
                n1 = n2;
                n2 = nextTerm;
            }
        }

        const fibonaci = useMemo(() => {
            return fibonaciFn(count)
        }, [count])


        return (
            <div>
                Count: {count} <br />
                Fibonaci: {fibonaci.join(', ')}  <br />
                <Button onClick={() => setCount(count2 + 1)}>Count +</Button>

                Count2: {count2} <br />
                <Button onClick={() => setCount2(count2 + 1)}>Count2 +</Button>
            </div>
        )
    }
```

- Khi giá trị count được thay đổi, fibonaci sẽ được tính toán lại

- Khi giá trị count2 được thay đổi, fibonaci không được tính toán lại mà sử dụng giá trị cũ 

- Lưu ý khi sử dụng: nếu state không được đưa vào dependencyList, thì giá trị state sử dụng trong hàm đó luôn luôn là giá trị cũ



# useCallback

- Sử dụng khi muốn cache một function trong 1 component

- Việc run lại phụ thuộc vào dependencyList có thay đổi hay không


```jsx

    import { useCallback, useState } from 'react'

    export const Count = () => {
        const [count, setCount] = useState(0)
        const [count2, setCount2] = useState(0)

        const fibonaci = useCallback(() => {
            let n1 = 0, n2 = 1, nextTerm;
            let res = []
            for (let i = 1; i <= count; i++) {
                console.log(n1)
                res.push(n1)
                nextTerm = n1 + n2;
                n1 = n2;
                n2 = nextTerm;
            }
        }, [count])


        return (
            <div>
                Count: {count} <br />
                Fibonaci: {fibonaci.join(', ')}  <br />
                <Button onClick={() => setCount(count2 + 1)}>Count +</Button>

                Count2: {count2} <br />
                <Button onClick={() => setCount2(count2 + 1)}>Count2 +</Button>
            </div>
        )
    }
```

- Nếu 1 hàm không được khai báo bằng useCallback, hàm đó sẽ được define lại mỗi lần re-render gây hao tổn bộ nhớ không cần thiết. Việc sử dụng useCallback sẽ tránh được việc

- Lưu ý khi sử dụng: nếu state không được đưa vào dependencyList, thì giá trị state sử dụng trong hàm đó luôn luôn là giá trị cũ


# useLayoutEffect



# Bài tập


- Làm các component sau trong dự án:

    - Breadcrumbs

    ```jsx
        import React from "react"
        import { Link } from "react-router-dom"
        import './style.scss'

        export const Breadcrumbs = ({ children }) => {

            const len = React.Children.count(children)
            return (
                <div className="breadcrumbs">
                    <ul>
                        {
                            React.Children.map(children, (child, index) => <li>{child}{index < len - 1 ? '>' : ''}</li>)
                        }
                    </ul>
                </div>
            )
        }

        export const BreadcrumbsItem = ({ children, to }) => {
            return (
                <Link to={to} className="item">{children}</Link>
            )
        }
    ```

    - Paginate

    ```jsx
        import { useDispatch } from "react-redux"
        import { Link, useLocation, useNavigate } from "react-router-dom"
        import { urlQueryToObject, objectToUrlQuery } from "utils/urlQueryToObject"
        import './style.scss'


        const Paginate = ({ totalPage }) => {
            const { pathname } = useLocation()
            const navigate = useNavigate()
            const dispatch = useDispatch()

            const query = urlQueryToObject({ page: '1' })

            query.page = parseInt(query.page)
            const renderItem = () => {
                let list = []
                let start = parseInt(query.page) - 2
                let end = parseInt(query.page) + 2

                for (let i = start; i <= end; i++) {
                    list.push(<Link
                        to={`${pathname}?${objectToUrlQuery({ page: i })}`}
                    >{i}</Link>)
                }
                return list
            }
            console.log(query.page)
            return (
                <div className="Paginate">
                    {
                        parseInt(query.page) - 2 > 1 &&  <Link to={`${pathname}?${objectToUrlQuery({ page: query.page - 1 })}`} >{'<'}</Link>
                    }
                
                    {renderItem()}
                    {
                        parseInt(query.page) + 2 < totalPage && <Link to={`${pathname}?${objectToUrlQuery({ page: query.page + 1 })}`} >{'>'}</Link>
                    }

                </div>
            )
        }

        export default Paginate
    ```

    ```jsx
        // utils/urlQueryToObject
        export function urlQueryToObject(defaultValues = {}) {
            try {
                var search = window.location.search.substring(1);
                const obj = JSON.parse('{"' + decodeURI(search).replace(/"/g, '\\"').replace(/&/g, '","').replace(/=/g, '":"') + '"}')
                return {...defaultValues, ...obj}
            } catch (err) {
                return defaultValues
            }
        }

        export const objectToUrlQuery = function (obj) {
            var str = [];
            for (var p in obj)
                if (obj.hasOwnProperty(p)) {
                    str.push(encodeURIComponent(p) + "=" + encodeURIComponent(obj[p]));
                }
            return str.join("&");
        }
    ```
    
    - Filter sản phẩm
