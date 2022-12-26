# React Component
# Component trong ReactJS là gì?
_ **Components** giúp phân chia các UI (giao diện người dùng) thành các phân nhỏ để dễ dàng quản lý và tái sử dụng. Giả sử mình có một website gồm nhiều phần bố cục khác nhau và mình muốn chia nhỏ các phần ra để dễ quản lý.

## Cách khai báo 1 component
---

Cách 1: Sử dụng class (Không khuyến khích)
```jsx
import { Component } from 'react'

class ComponentA extends Component {

    render(){
        return <div>Nội dung component</div>
    }
}

export default ComponentA

```

Cách 2: Sử dụng hook
```jsx
export default function ComponentA(){
    return <div>Nội dung Component</div>
}
```
Hoặc arrow function
```jsx
const ComponentA = () => {
    return <div>Nội dung Component</div>
}

export default ComponentA
```
--> Tùy thuộc vào bạn chọn hook hay class mà chọn cho mình cách khai báo phù hợp, nên sử dụng cách arrow function vì nó ngắn gọn

## Cách sử dụng
----
```jsx
const ComponentA = () => {
    return <div>Nội dung Component A</div>
}
const ComponentB = () => {
    return <div>Nội dung Component A</div>
}

const App = () => {
    return (
        <div>
            <ComponentA />
            <ComponentB />
            <ComponentA />
        </div>
    )
}

export default App
```

# Prop trong component
- Props là dữ liệu được truyền từ component cha vào component con khi sử dụng
- Props có thể là 1 biến string, number, boolean, object.... function. Hoặc cũng có thể là một component khác
- Props không thể thay đổi trong component được truyền

## Cách khai báo và sử dụng
```jsx
const ComponentA = (props) => {
    const { name } = props
    return <div>Xin chào {name}</div>
}

const App = () => {
    return (
        <div>
            <ComponentA name="Đặng Thuyền Vương" />
        </div>
    )
}
```
## Lưu ý:
1. Sẽ luôn luôn có 1 props mặc định trong mõi component là `children` chính là phần nội dung giữa 2 tag
```jsx
const ComponentA = (props) => {
    const { name, children } = props
    return (
        <div>
            <h1>Xin chào {name}</h1>
            {children}
        </div>
    )
}

const App = () => {
    return (
        <div>
            <ComponentA name="Đặng Thuyền Vương">
                Nội dung ở giữa component
            </ComponentA>
        </div>
    )
}
```
2. Không được thay đổi giá trị của prop trong component con (sử dụng từ khóa const cho khai báo khi cần thiết)

