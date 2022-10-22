# Style

# Style trong React

- Có 4 loại style trong Reactjs là:

## 1. Inline styling

- Cách code trực tiếp css trong tag html

- Dùng trong những trường hợp muốn gắn css cho element đặc biệt nào đó

- Attribute được đặt tên theo quy tắc `camelCased`

- Có thể tạo 1 JavaScript Object ở bên ngoài rồi sử dụng lại bên trong element

```jsx
    const style = {
        title: {
            fontSize: 14,
            border: '1px solid #ccc',
            paddingTop: 10,
            paddingBottom: 10,
            paddingLeft: 10,
            paddingRight: 10,
            // padding: '10px 10px 10px 10px'
        },
        content: {
            fontSize: 14,
            padding: '10px 10px 10px 10px',
            
        }
    }
    
    const Accordion = ({ title, children }) => {
        return (
            <divn className="accordion">
                <h3 className="title" style={style.title}>{title}</h3>
                <div className="content" style={style.content}>{children}</div>
            </divn>
        )
    }
```
## 2. CSS Stylesheet

```css
    /* style.css */
    .accordion .title{
        font-size: 14px;
        border: 1px solid #ccc;
        padding-top: 10px 10px 10px 10px;
    }

    .accordtion .content{
        font-size: 14px;
        padding-top: 10px 10px 10px 10px;
    }
    
```

```jsx
    import './style.css'

    const Accordion = ({ title, children }) => {
        return (
            <divn className="accordion">
                <h3 className="title" >{title}</h3>
                <div className="content" >{children}</div>
            </divn>
        )
    }
```


## 3. CSS Modules

```css
    /* style.module.css */
    .title{
        font-size: 14px;
        border: 1px solid #ccc;
        padding-top: 10px 10px 10px 10px;
    }

    .content{
        font-size: 14px;
        padding-top: 10px 10px 10px 10px;
    }
    
```

```jsx
    import styles from './style.css'

    const Accordion = ({ title, children }) => {
        return (
            <divn className="accordion">
                <h3 classNames={styles.title}>{title}</h3>
                <div classNames={styles.content}>{children}</div>
            </divn>
        )
    }
```

--> React sẽ tự động generate class title_[mã code] để đảm bảo không có class trùng

## 4. Styled-components 

- Styled-components là một thư viện dành cho React và React Native cho phép bạn viết style ở cấp độ component trong ứng dụng của bạn.

- Đầu tiên ta phải cài đặt thư viện styled-components:

    > <font size="5"> npm install styled-components --save</font>

- Bây giờ chúng ta có thể sử dụng styled-component để tạo cho style các component html quen thuộc

```jsx
    import React from 'react';
    import styled from 'styled-components';

    // Tạo một react component <Title> mà sẽ render ra thẻ <h1> mà text ở giữa, cỡ chữ 1.5em và màu chữ là palevioletred
    const Title = styled.h3`
        font-size: 14px;
        border: 1px solid #ccc;
        padding-top: 10px 10px 10px 10px;
    `;

    // Tạo một react component nữa là <Wrapper>, render ra thẻ <section> với padding và nền papayawhip
    const Content = styled.div`
        font-size: 14px;
        padding-top: 10px 10px 10px 10px;
    `;

    const Accordion = ({ title, children }) => {
        // Cuối cùng sử dụng các component vừa tạo như các React component khác ngoại trừ việc các component này đã được "styled"

        return (
            <divn className="accordion">
                <Title className="title" >{title}</Title>
                <Content className="content">{children}</Content>
            </divn>
        )
    }
```

# Tổng kết:

- Tất cả những phương pháp trên đều có những ưu điểm và nhược điểm, vì vậy hãy suy nghĩ, tính toán trước về độ phức tạp của ứng dụng cũng như sở thích của bạn để chọn ra phương pháp hợp lý và hiệu quả nhất.
