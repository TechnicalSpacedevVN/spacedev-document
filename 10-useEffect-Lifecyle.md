# useEffect và Lifecyle trong React

# useEffect

## Cách sử dụng: 

`useEffect(callback, dependencyList)`

* `callback`: là hàm được thực hiện sau khi component được render, re-render

* `dependencyList`: Là mảng các giá trị, khi component được `re-render`, react sẽ so sánh giá trị cũ và giá trị mới xem có sự thay đổi hay không, nếu có sẽ thực hiện lại `callback`, nếu không sẽ ko làm gì cả.


## **Demo**: Mõi lần button được click, `state` được gán lại và tăng lên 1. sau đó, `document.title` sẽ được update lại


```jsx
    import React, { useState, useEffect } from 'react';

    function Example() {
        const [count, setCount] = useState(0);

        useEffect(() => {
            document.title = `You clicked ${count} times`;
        });

        return (
            <div>
            <p>You clicked {count} times</p>
            <button onClick={() => setCount(count + 1)}>
                Click me
            </button>
            </div>
        );
    }
```

## Các bước chạy của code

- Bước 1: Component được khởi tạo với giá trị count = 0

- Bước 2: Khi code gặp `useEffect`, `callback` sẽ không được chạy trong thời điểm đó mà được để sau quá trình render

- Bước 3: React sẽ render ra UI khi `return` được gọi

- Bước 4: `callback` của `useEffect` sẽ được chạy khi quá trình render kết thúc và thực hiện thay đổi `title` của page

- Bước 5: Khi user click vào button `Click me`, setState sẽ được gọi và quá trình `re-render` được kích hoạt, state sẽ mang giá trị mới

## useEffect là gì?
- Là những hiệu ứng (slide effect) trong quá trình thực hiện component. Nó có thể là data fetching, thao tác trực tiếp với DOM

- `useEffect` sẽ luôn luôn được gọi lần đầu khi khởi tạo

- Tùy thuộc vào `dependencyList` mà `callback` sẽ được thực hiện ở lần `re-render`

- Trong `callback` có thể `return` về 1 `function` khác, function đó sẽ được run `trước` mõi callback được `run lại` hoặc khi component được hủy (khi component không được render ra giao diện)

- `callback` sẽ không được chạy ngay tại thời điểm `useEffect` được chạy, nó chỉ được chạy sau quá trình `render`

- `callback` không được là `function async`

- Khi trong `useEffect` có sử dụng `state` nên lưu ý để `state` đó vào  `dependencyList`, nếu không giá trị sử dụng trong `callback` sẽ luôn luôn là giá trị ban đầu

- Mõi component có quyền khai báo nhiều `useEffect`

## Code demo và các kiểu sử dụng useEffect

### Cách 1: không `dependencyList`
- `callback` sẽ thực hiện lại sau mõi lần render, re-render

- Thường dùng cho việc thực thi code mõi lần component được render

```jsx
    useEffect(() => {
        document.title = `Code run every time component re-render`;
    });
```

### Cách 2: `dependencyList` là mảng rỗng
- `callback` chỉ được thực hiện 1 lần khi component render lần đầu, ở lần `re-render` callback sẽ không được thực hiện

- Thường dùng để call api lấy data khi vào component, và không lấy lại khi component re-render

```jsx
    useEffect(() => {
        document.title = `Code run only at the first time component render`;
    },[]);
```

### Cách 3: `dependencyList` là mảng có giá trị
- `callback` sẽ được thực thi khi mõi lần render và tùy thuộc vào việc có giá trị `dependency` nào thay đổi hay không

- Thường dùng để lắng nghe sự thay đổi của 1 giá trị nào đó mõi lần re-render, và thực thi logic

- `dependencyList` có thể là state, prop hoặc bất kỳ giá trị nào

```jsx
    const [count, setCount] = useState(0)

    useEffect(() => {
        document.title = `You clicked ${count} times`;
    },[count]);
```


### Cách 3: `callback` có trả về `function`

- Thường dùng để dọn dẹp khi component được hủy hoặc chạy trước mõi lần `callback` tiếp theo được chạy

```jsx
    const [count, setCount] = useState(0)

    useEffect(() => {
        const timer = setTimeout(() => {
            alert()
        }, 1000)

        // sẽ được run khi useEffect được run lại hoặc component được hủy
        return () => {
            cleartTimeout(timer)
        }
        
    },[count]);
```


# Lifecyle (Vòng đời của Component)

# Class component

- Lifecyle là vòng đời của 1 component từ khi khởi tạo đến khi được hủy sẽ trãi qua các quá trình (hàm): Khởi tạo (Mouting) - Thay đổi (Updating) - Hủy (Unmounting)


![Vòng đời của component!](./img/Screen-Shot-2018-10-31-at-1.44.28-PM.png)

(Ảnh minh họa)

## Khởi tạo (Mounting): Là quá trình component được tạo ra, sẽ trãi qua các quá trình (hàm):

- `constructor` : hàm `constructor` của class, sẽ được gọi ở lần đầu tiên component được render
- `getDerivedStateFromProps` : Là static function vì thế bạn không thể gọi `this` bên trong hàm này. Dùng để truyền các prop vào trong component, nếu có sẽ `return state` ngược lại sẽ `return null`
- `render` : return về 1 DOM Element, sau đó UI sẽ được cập nhật mới dựa theo giá trị return
- `componentDidMount` : Được gọi sau khi render và duy nhất ở quá trình mounting


## Thay đổi (Updating): Là quá trình component thay đổi và cập nhật lại giao diện (re-render). Khi state hoặc props thay đổi, hoặc có thể gọi hàm `forceUpdate` để ép buộc quá trình updating

- 1 trong 3 điều kiện sau xẩy ra sẽ xẩy ra quá trình updating: Props nhận giá trị mới, state thay đổi hoặc forceUpdate được gọi

- `getDerivedStateFromProps` : Là static function vì thế bạn không thể gọi `this` bên trong hàm này. Dùng để truyền các prop vào trong component, nếu có sẽ `return state` ngược lại sẽ `return null`

- `shouldComponentUpdate`: Hàm này sẽ nhận vào `new props` và `new state`. Hàm cần `return` về giá trị `true` hoặc `false`, nếu `true` thì component sẽ xẩy ra quá trình `re-render`, ngược lại `false` sẽ không làm gì cả

- Gọi ngay trước khi render xuống DOM, cho phép lấy một số thông tin của DOM (ví dụ vị trí thanh scroll), các giá trị return từ hàm này sẽ đưa cho `componentDidUpdate()`

- `componentDidUpdate(prevProps, prevState, snapshot)`: Sau khi quá trình `updating` hoàn tất. Đây có thể là nơi để tạo call api request khi so sánh `prop` hiện tại với `prop` thời điểm trước đó

## Hủy component (Unmounting): Là quá trình component được hủy. Có thể sử dụng để remove các listener, các hàm setInterval, cancel network request


# Function component

- Vì sự phức tạp trong lifecyle của class component, chúng ta có thể hiện thực nó thông qua hook (useEffect) một cách dễ dàng

| Class Component  | Function Component 
|------------------|--------------------
| state, setState  | useState
| componentDidMount | useEffect(() => {}, [])
| componentDidUpdate | useEffect(() => {}, [...depencyList])
| shouldComponentUpdate | React.memo(Component, () => {})
| componentWillUnmount | useEffect(() => { return () => {} }, [])

# Tổng kết

- `callback` sẽ luôn được chạy lần đầu tiên khi component render lần đầu

- Không truyền `dependyList` : `callback` luôn được run khi re-render

- `dependencyList` = []: Run 1 lần duy nhất khi khởi tạo

- `dependencyList` = [...dependencyList]: Run khi 1 trong các giá trị thay đổi

- `callback` có return về 1 function: `function` đó sẽ được run trước mõi lần re-render hoặc khi component được hủy

# Các usecase thường sử dụng

- Gọi call api khi vào component

- Bắt sự kiên DOM bằng javascript thuần, hủy sự kiện trong function return

- Lắng nghe sự thay đổi của 1 biến mõi lần re-render