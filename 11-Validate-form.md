# Validate Form trong Reactjs

# Validate Form là gì?

- Validate form là quá trình kiểm tra dữ liệu được nhập vào trong form có đúng hay không trước khi được submit lên BE

- Validate nên là bắt buộc trước khi submit data lên BE

# Các rule validate thường gặp

1. required: trường bắt buộc điền

2. pattern (email, url, phone): Trường phải nhập theo định dạng nào đó

3. min/max: Độ dài của trường phải đạt điều kiện min/max

4. confirm: Giá trị của trường này phải giống với trường kia (Confirm Password)

5. Những rule đặc biệt.... 

# Các bước thực hiện validate

- **Bước 1**: Bắt sự kiện `submit` của form hoặc `onClick` của button gửi dữ liệu

- **Bước 2**: Lấy dữ liệu từ form và đưa vào 1 `object`

- **Bước 3**: Tiến hành validate data từ `object` đó

- **Bước 4**: Tiến hành `show error` nếu có data lỗi

- **Bước 5**: Nếu data không lỗi, tiến hành `submit` lên BE


```jsx
    import Button from 'components/Button'
    import TextField from 'components/TextField'
    import React, { useState } from 'react'
    import { delay } from 'utils/delay'
    import './style.scss'

    const emailRegexp = /^(([^<>()[\]\\.,;:\s@"]+(\.[^<>()[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/

    export const Checkout = () => {

        const [isFetching, setIsFetching] = useState(false)

        const [form, setForm] = useState({
            username: '',
            password: ''
        })

        const [error, setError] = useState({})

        const submit = async (ev) => {
            ev.preventDefault()
            let errorObj = {}
            if (!form.username.trim()) {
                errorObj.username = 'Username khong duoc de trong'
            } else if (!emailRegexp.test(form.username)) {
                errorObj.username = 'Username phai la Email'
            }

            if (!form.password) {
                errorObj.password = 'Password khong duoc de trong'
            } else if (form.password.length < 6 || form.password.length > 32) {
                errorObj.password = 'Password phai tu 6-32 ky tu'
            }

            setError(errorObj)

            if (Object.keys(errorObj).length === 0) {
                setIsFetching(true)
                await delay(3000)
                setIsFetching(false)
            }
        }

        const _onChange = (name) => (ev) => {
            setForm({
                ...form,
                [name]: ev.currentTarget.value
            })
        }

        return (
            <div className="checkout-page">
                <div className="container">
                    <div className="form-wrap">
                        <h1>Login</h1>
                        <form onSubmit={submit} >
                            <TextField
                                label="Username"
                                value={form.username}
                                onChange={_onChange('username')}
                                placholder="Example@gmail.com"
                                errorText={error.username}
                            />
                            <TextField
                                label="Password"
                                value={form.passowrd}
                                onChange={_onChange('password')}
                                placholder="Password"
                                type="password"
                                errorText={error.password}
                            />
                            <label>
                                <div className="label">Username</div>
                                <input type="text" value={form.username} onChange={_onChange('username')} />
                                <p className="error-text">{error.username}</p>
                            </label>
                            <label>
                                <div className="label">Password</div>
                                <input type="password" value={form.password} onChange={_onChange('password')} />
                                <p className="error-text">{error.password}</p>
                            </label>
                            <Button loading={isFetching}>Submit</Button>
                        </form>
                    </div>
                </div>
            </div>
        )
    }

    export default Checkout
```


# Bài tập trên lớp

- Tạo một form đăng ký với các field và rule sau đây:

1. username: Băt buộc điền, là email

3. Password: Bắt buộc điền, min: 6, max:32. Bao gồm ký tự số, viết hoa, đặc biệt, viết thường

5. Confirm Passowd: điền giống password

7. Name: Bắt buộc có 2 ký tự

9. customer is: Select chọn lựa từ các option có sẵn, bắt buộc phải chọn gồm các option sau: IT, Designer, Devops, Other. Khi chọn Other phải thêm 1 text field ở dưới và bắt buộc điền

11. age: Bắt buộc trên 18 tuổi

13. Checkbox: đồng ý với các điều khoản (Bắt buộc)

15. Button Click. Giả trạng thái loading. Khi bấm vào button thì set loading, 3s sau sẽ tắt


# Bài tập về nhà

- Hoàn thành trang checkout với đầy đủ các rule validate
