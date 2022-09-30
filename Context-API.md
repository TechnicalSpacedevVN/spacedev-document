# Context API

# Vấn đề?

- Khi ứng dụng phát triển lớn hơn, các component cần truyền prop nhiều hơn. Trong trường hợp 2 component có dùng chung 1 state thì state đó phải được đặt vào parent chung nhất của 2 component đó và truyền prop xuống child

- Vấn đề xẩy ra khi cha chung của 2 component cách nhau quá nhiều cấp và khó để truyền và cập nhật khi cần thiết

- Khi thay đổi state thì toàn bộ ứng dụng sẽ được sử dụng state mới

# Giải quyết

- Cần có 1 nơi có thể giữ tất cả các state, function đó

- Khi component con cần sử dụng, chỉ cần gọi trực tiếp để lấy ra mà không cần phải thông qua prop từ parent truyền vào
# Context API là gì ?

- Context API là một chức năng mới được thêm vào React ở phiên bản 16.3 dùng để quản lý state (state management) ở cấp độ global

- Cho phép share state, function cho toàn bộ component con khi cần thiết mà không cần phải thông qua prop, tránh trường hợp "prop drilling" (1)

- Context API dễ tiếp cận hơn Redux


(1) prop drilling là việc truyền prop từ grandparent xuống component cháu thông qua component cha mặc dù component cha hoàn toàn không sử dụng nó
# Khi nào cần sử dụng Context API

- Khi data đó là data sử dụng chung, toàn bộ ứng dụng có thể cần đến nó

- Dữ liệu cần được cache, không call api nhiều lần

- Khi state, function cần dùng cho 2 component ở cách nhau quá xa trên cây component

# Cách sử dụng

- Bước 1: Tạo `Context`

- Bước 2: Tạo Sử dụng `Provider` để bao toàn bộ ứng dụng

- Bước 3: Tạo các state, function dùng chung và đưa vào `value` của `Provider`

- Bước 4: Ở những component con của Provider cần sử dụng thì sử dụng `useContext` và truyền vào cái `Context` muốn sử dụng


# Code demo

```jsx
    const { createContext, useContext, useState } = require("react");

    const PageContext = createContext()

    export const PageProvider = ({ children }) => {
        const [isOpenCart, setIsOpenCart] = useState(false)

        const openCart = () => setIsOpenCart(true)

        const closeCart = () => setIsOpenCart(false)

        return (
            <PageContext.Provider value={{ openCart, closeCart, isOpenCart }}>{children}</PageContext.Provider>
        )
    }

    export const usePage = () => useContext(PageContext)
```

# Bài tập trên lớp

- Thực hành tạo Context API cho chức năng Authen đặt tên là AuthContext

- Viết 1 custom hook cho Context đó và đặt tên là `useAuth`

- Viết chức năng login, logout có lưu `localStorage`

- Viết chức năng cart, đóng/mở cart
