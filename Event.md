# Event trong Reactjs
# Event là gì?
- Event là những sự kiện xẩy ra trong quá trình sử dụng website do người dùng tác động chủ động hoặc brower gọi tự động

- Event được chia thành nhiều nhóm:

    - ### **Nhóm mouse**

        | Tên event         | Giải thích |
        | -----------       | ----------- |
        | onMouseDown       | Khi click nhưng chưa nhả chuột       |
        | onMouseUp         | Khi click và nhả chuột ra        |
        | onMouseOver       | Di bắt đầu vào trong element        |
        | onMouseLeave      | Di chuyển ra khỏi element        |
        | onClick   | Khi click        |
        | onDbClick   | Double Click        |
        | onMouseMove   | Di chuyển hover trong element        |
        | onMouseEnter   | Khi chuột bắt đầu vào trong element        |
        | onMouseOut   | Khi chuột ra khỏi element        |
        | onContextMenu   | Khi bấm chuột phải        |

    <br>
    
    - ### **Nhóm key**

        | Tên event         | Giải thích |
        | -----------       | ----------- |
        | onKeyDown         | Khi nhấn key        |
        | onKeyUp       | Khi nhấn và nhả key      |
        | onKeyPress       | Khi nhấn key        |

    <br>

    - ### **Nhóm form, input**

        | Tên event         | Giải thích |
        | -----------       | ----------- |
        | onFocus         | Khi focus        |
        | onSubmit       | Khi submit form      |
        | onBlur       | Khi mất focus        |
        | onChange       | Khi thay đổi giá trị        |
    <br>

    - ### **Nhóm drag event**

        | Tên event         | Giải thích |
        | -----------       | ----------- |
        | onDrag         | Khi drag        |
        | onDragEnd       | Khi kêt thúc drag      |
        | onDragEnter       | Khi drag và enter vào element        |
        | onDragLeave       | Khi drag và rời khỏi        |
        | onDragOver       | Khi drag và di chuyển vào element     |
        | onDragStart       | Khi bắt đầu drag       |
        | onDrop       | Khi drop element       |
    <br>

# Cách bắt sự kiện trong React

```jsx
    const Accordion = ({ title, children }) => {
        
        const handleTitleClick = () => {
            console.log('....')
        }

        return (
            <divn className="accordion">
                <h3 className="title" onClick={handleTitleClick}>{title}</h3>
                <div className="content">{children}</div>
            </divn>
        )
    }
```
