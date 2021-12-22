# Refs, Portal trong Reactjs
# Ref là gì?

- Ref là cách Component cha lấy component con để thao tác

- Dùng để lấy DOM Element mà không cần sử dụng javascript thuần

- Component đặt ref có thể là 1 thẻ DOM element hoặc component React

- Sử dụng hook `useRef` được import từ `react`

- Value của ref sẽ được gắn vào `current` 

- Nếu `useRef` không được truyền `initValue` (giá trị khởi tạo) thì giá trị mặc định sẽ là `undefined` 

- Có 3 cách sử dụng ref được sử dụng trong React

## Cách 1: Ref đơn giản

- Ref được gắn trực tiếp vào DOM Element

- Thường dùng để lấy giá trị của input

- Thay đổi những thuộc tính của 1 DOM Element

- Uncontrolled thay vì controlled component

- Giá trị của ref tùy thuộc vào DOM Element được gắn ref (javascript thuần)

```jsx
    import { useRef } from "react" // import hook useRef

    const Form = () => {

        const inputRef = useRef()

        return (
            <form>
                <input ref={inputRef} />
                <button onClick={() => alert(inputRef.current?.value)}>Click</button>
            </form>
        )
    }

    export default Form
```

## Cách 2: forwardRef

- Ref được gắn vào 1 Component React mà ko phải là DOM Element

- Được sử dụng khi muốn gắn ref vào Component React con không phải DOM ELement, sau đó Component React con sẽ forward ref đó sang 1 DOM Element cụ thể khác

- Giá trị của `current` ref sẽ phụ thuộc vào nơi DOM Element được forward

- Khi 1 Component được khai báo forward ref nhưng ko gắn cụ thể vào 1 Element nào hết thì giá trị `current` sẽ là `initValue`

- Khi 1 Component không được khai báo forward ref nhưng lại gắn ref thì sẽ báo lỗi ở console và giá trị `current` sẽ là `initValue`


```jsx
    import { useRef } from "react"

    const Input = forwardRef((props, ref) => {
        return <input {...props} ref={ref} />
    })

    const Form = () => {
        const inputRef = useRef()
        return (
            <form onSubmit={(ev) => { ev.preventDefault() }}> {/* ngăn chặn sự kiện submit form */}
                <Input ref={inputRef} />
                <button onClick={() => console.log(inputRef.current?.value)}>Click</button> {/* mặc định button nằm trong form là button submit */}
            </form>
        )
    }

    export default Form
```

## Cách 3: forwardRef và trả về 1 thể hiện khác của ref

- Ref được gắn vào 1 Component React mà ko phải là DOM Element

- Ref sẽ không được gắn vào Element cụ thể, mà thay vào đó sẽ sử dụng hook `useImperativeHandle` để trả ra 1 thể hiện khác của ref

- Được sử dụng để truyền Ref vào 1 Component phức tạp để nhận 1 `thể hiện khác` giúp cho code đơn giản hơn


```jsx
    import { useRef } from "react"

    const Input = forwardRef((props, ref) => {
        return <input {...props} ref={ref} />
    })

    const Form = forwardRef((props, ref) => {

        useImperativeHandle(ref, () => {
            return {
                submit: () => {
                    console.log({
                        name: inputRef.current?.value
                    })
                },
                reset: () => {
                    inputRef.current.value = ''
                }
            }
        }, [])

        const inputRef = useRef()

        return (
            <form onSubmit={(ev) => { ev.preventDefault() }}>
                <Input ref={inputRef} />
            </form>
        )
    })

    function App() {
        const formRef = useRef()

        return (
            <div className="App">
                <Form ref={formRef}/>
                <button onClick={() => formRef.current?.submit()}>Submit</button>
                <button onClick={() => formRef.current?.reset()}>Reset</button>
            </div>
        );
    }

```

# Tổng kết

- Tùy thuộc vào mục đích mà chọn cách sử dụng `ref` cho phù hợp

- Có thể dùng javascript thuần để lấy ra Element cần thiết (không khuyến khích) thay vì sử dụng ref trong trường hợp bắt buộc

- Nên kiểm tra giá trị của `ref` trước khi sử dụng (Optional chaining `?.`) phòng trường hợp ref không được truyền vào Component


# Portal

- Portal là cách Component render ra HTML. Thông thường các component sẽ render ra HTML ở nơi mà nó được sử dụng. Có những Component bắt buộc phải được append vào con trực tiếp của body vd: Popup, tooltip, Modal,....

- Chúng ta sử dụng `createPortal` của `ReactDOM` để render ra HTML ở nơi mình mong muốn

```jsx
    import ReactDOM from 'react-dom'

    const ModalSearch = () => {
        return ReactDOM.createPortal(
            <div>
                Modal
            </div>,
            document.body // Nơi Element sẽ được append
        )
    }


    const App = () => {
        return (
            <div className="App">
                <ModalSearch />
            </div>
        )
    }
```