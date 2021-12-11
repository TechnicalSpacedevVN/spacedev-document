# State trong React

# State là gì?

- `State` là trạng thái của 1 component. Mỗi component sẽ có quyền có state (`statefull component`) hoặc không có (`stateless component`), tùy thuộc vào mục đích của component

- State có thể thay đổi trong quá trình thực thi (component được render)

- Khi thay đổi state sử dụng `setState` của state đó, component sẽ được `re-render` lại, và logic sẽ được thực thi lại. Không init lại giá trị của state, lúc này state sẽ giữ giá trị mới --> update giao diện


```jsx
    const Accordion = ({ title, children }) => {
        
        const [isOpen, setIsOpen] = useState(false)

        const handleTitleClick = () => {
            setIsOpen(!setIsOpen)
        }

        return (
            <divn className={`accordion ${isOpen ? 'open' : 'hide'}`}>
                <h3 className="title" onClick={handleTitleClick}>{title}</h3>
                <div className="content">{children}</div>
            </divn>
        )
    }
```

---> Khi bất kỳ `setState` nào của component được gọi, component sẽ `re-render` (thực thi lại logic trong component). Và các quá trình `initState` sẽ không được thực hiện lại, lúc này state sẽ mang giá trị mới và react sẽ render ra giao diện với state mới


# Sự khác nhau giữa state và props

- **Props**: 

    - Không thể thay đổi trong quá trình thực thi
    
    - Được truyền từ component cha xuống con

    - Chỉ được thay đổi khi component cha re-render lại và truyền xuống 1 props mới

- **State**: 

    - Có thể thay đổi trong quá trình thực thi
    
    - Được khởi tạo trong chính component đó

    - Mõi lần `setState` thay đổi giá trị, chính bản thân component đó sẽ được re-render lại (thực thi lại logic trong component) và giá trị sẽ mang giá trị mới

# Bài tập

- Hướng dẫn làm bài tập
- Yêu cầu giao diện trong mõi bài tập, tìm UI cho mõi bài tập
- Chuẩn bị sẳn data nếu cần thiết

1. Tạo component Accordion
2. Tạo component Tab
3. Tạo component Menu
3. Tạo component Input
