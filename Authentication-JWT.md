# Authentication - Authorization

# Authentication là gì?

- Authentication (xác thực): là quá trình kiểm tranh danh tính 1 tài khoản đang vào hệ thống hiện tại thông qua một hệ thống xác thực. Đây là bước đầu tiên của mọi hệ thông có yếu tố xác thực người dùng.

- Hiểu đơn giản Authen là đi tìm câu trả lời cho câu hỏi "Bạn là ai?"

## Tại sao cần có Authentication

- Nếu không có bước xác thực này, hệ thống sẽ không biết được người đang truy cập vào hệ thống là ai để có các phản hồi phù hợp.

- Quá trình này rất thông dụng trong hầu hết các hệ thống thông tin có mang tính cá nhân vd: Facebook, google, Twitter,...


## Các phương thức authentication

- **Single-Factor Authentication**: Phương thức đơn giản nhất, sử dụng username + password để xác thực người dùng.

- **Two-Factor Authentication**: Thường sử dụng cho các hệ thống cần độ bảo mật cao: vd ATM. Như tên của nó, quá trình xác thực diễn ra gồm 2 bước, không chỉ username + password mà còn 1 thông tin khác mà chỉ user biết.

    - Bước 1: Nhập thông tin đăng nhập username + password. 
    
    - Bước 2: Nhập thông tin bí mật mà chỉ người dùng biết

- **Multi-Factor Authentication**: Là phương thức authentication tiên tiến và bảo mật nhất. Thường dùng cho các hệ thống cần bảo mật thông tin cao như Ngân hàng. Tất cả các yếu tố phải đọc lập với nhau để loại bỏ bấy kỳ lỗ hỏng nào trong hệ thống.

    - Bước 1: Nhập thông tin đăng nhập (username + password, số điện thoại)

    - Bước 2: Mã verify code sẽ được gửi thông qua 1 hệ thống độc lập khác (SMS, email, facebook, ....), các hệ thống phải đảm bảo tách biệt với hệ thống đăng nhập ở Bước 1.


# Authorization là gì?

- Mặt khác, Authorization xảy ra sau khi hệ thống của bạn được authentication (xác thực) thành công, cuối cùng cho phép bạn toàn quyền truy cập các tài nguyên như thông tin, file, cơ sở dữ liệu, quỹ, địa điểm, hầu hết mọi thứ.

- Nói một cách đơn giản, authorization xác định khả năng của bạn để truy cập hệ thống và ở mức độ nào. Khi danh tính của bạn được hệ thống xác minh sau khi xác thực thành công, bạn sẽ được phép truy cập tài nguyên của hệ thống.



|Authentication | Authorization
-----------|-------------
Authentication xác nhận danh tính của bạn để cấp quyền truy cập vào hệ thống. | Authorization xác định xem bạn có được phép truy cập tài nguyên không.
Đây là quá trình xác nhận thông tin đăng nhập để có quyền truy cập của người dùng. | Đó là quá trình xác minh xem có cho phép truy cập hay không.
Nó quyết định liệu người dùng có phải là những gì anh ta tuyên bố hay không. | Nó xác định những gì người dùng có thể và không thể truy cập.
Authentication thường yêu cầu tên người dùng và mật khẩu. | Các yếu tố xác thực cần thiết để authorization có thể khác nhau, tùy thuộc vào mức độ bảo mật.
Authentication là bước đầu tiên của authorization vì vậy luôn luôn đến trước. | Authorization được thực hiện sau khi authentication thành công.
Ví dụ, sinh viên của một trường đại học cụ thể được yêu cầu tự xác thực trước khi truy cập vào liên kết sinh viên của trang web chính thức của trường đại học. Điều này được gọi là authentication. | Ví dụ, authorization xác định chính xác thông tin nào sinh viên được phép truy cập trên trang web của trường đại học sau khi authentication thành công.


# Jsonwebtoken

- Jsonwebtoken là là hình thức xác thực được sử dụng cho các hệ thống được đặt trên những server khác nhau (FE - BE)

![!](./img/1_IqAodJn46th31XLkU5Qf1w.jpeg)

Giải thích:

- Browser thực hiện POST username + password lên server, dựa theo 2 thông tin này, BE sẽ kiểm tra trong database. Nếu có user đó, BE sẽ dùng generate 2 token (accessToken, refreshToken) dựa theo thông tin user đó và trả về cho browser.

- Browser nhận đc 2 token sẽ tiến hành lưu trữ dưới browser và khi refresh trang không bị mất (localStorage, indexDB,...)

- Khi user muốn thực hiện 1 thao tác có yêu cầu quyền truy cập, user sẽ gửi kèm accessToken kèm vào header lên BE, khi BE nhận được request, BE sẽ kiểm tra accessToken và tiến hành kiểm tra xem user có quyền đó hay không và tiến hành thực hiện yêu cầu

- BE trả response error hoặc success về cho user 

> ## Lưu ý

- accessToken có thời hạn ngắn (khoảng 15 phút đến 1 tiếng), khi hết thời hạn, accessToken sẽ không thể sử dụng được nữa, và bạn có thể nhận được status code `401 Unauthorized` khi cố gắng thực hiện

- Sử dụng refreshToken có thời hạn dài (khoảng 15 - 30 ngày) để refresh lại accessToken khi cần thiết

# Code demo

- Bước 1: Authentication - Login

```jsx

    fetch('..../login', {
        method: 'POST',
        headers: {
            'Content-Type': 'application/json'
        },
        body: JSON.stringify({
            username: 'nguyenvana@gmail.com',
            password: '123456789'
        })
    })
    .then(res => res.json())
    .then(res => {
        if(res.data){
            // res = {
            //     data: {
            //         accessToken: '......',
            //         refreshToken: '.....'
            //     }
            // }

            localStorage.setItem('login', res.data)       
        }
    })

```

- Bước 2: Authorization - Thực hiện 1 hành đồng có yêu cầu quyền truy cập

```jsx
    const token = JSON.parse(localStorage.getItem('login'))

    fetch('..../cart', {
        headers: {
            'Authorization': `Bearer ${token.accessToken}`
        }
    })
    .then(res => res.json())
    .then(res => {
        // response
    })

```

- Bước 3: Refresh token khi cần thiết


```jsx

    let token = JSON.parse(localStorage.getItem('login'))

    fetch('..../refresh-token', {
        method: 'POST',
        headers: {
            'Content-Type': 'application/json'
        },
        body: JSON.stringify({
            refreshToken: token.refreshToken
        })
    })
    .then(res => res.json())
    .then(res => {
        // res = {
        //     data: {
        //         accessToken: '......',
        //     }
        // }
        if (res.data.accessToken) {
            token.accessToken = res.data.accessToken
            localStorage.setItem('login', res.data)  
        }
    })
```

# Bài tập

- Viết Authentication - Authorization cho dự án (Login, Logout, register, get info, update info)

- Viết 1 function `callApiWithToken` với token được gắn kèm vào header, và có thực hiện refreshToken khi cần thiết

```jsx
    // utils/callApiWithToken
    import authService from "services/authService"

    export const callApiWithToken = async (url, options = {}) => {
        let token = JSON.parse(localStorage.getItem('token'))

        options = {
            ...options,
            headers: {
                ...options.headers,
                'Authorization': `Bearer ${token.accessToken}`
            }
        }

        const res = await fetch(url, options)

        if(res.status === 403){
            const refresh = await authService.refreshToken()
            if(refresh.data.accessToken){
                token.accessToken = refresh.data.accessToken 
                localStorage.setItem('token', JSON.stringify(token))

                options = {
                    ...options,
                    headers: {
                        ...options.headers,
                        'Authorization': `Bearer ${token.accessToken}`
                    }
                }
                return fetch(url, options).then(res => res.json())
            }
        }

        return res.json()
    }

```

- Gọi API lấy danh sách sản phẩm

- Viết custom hook để call api khi cần thiết `useQuery`


```jsx
    // hooks/useQuery
    import { useEffect, useState } from "react"

    export const useQuery = (promise, dependencyList = []) => {
        const [isFetching, setIsFetching] = useState(true)
        const [data, setData] = useState()
        
        useEffect( () => {
            (async () => {
                setIsFetching(true)
                const res = await promise()
                setData(res.data)
                setIsFetching(false)
            })()
        }, dependencyList)

        return {
            data,
            isFetching
        }
    }

```
