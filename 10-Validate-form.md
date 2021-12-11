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

- **Bước 1**: Bắt sự kiện `submit` của form hoặc `onClick` của button submit

```javascript
    
```

- **Bước 2**: Lấy dữ liệu từ form và đưa vào 1 `object`

- **Bước 3**: Tiến hành validate data từ `object` đó

- **Bước 4**: Tiến hành `show error` nếu có data lỗi

- **Bước 5**: Nếu data không lỗi, tiến hành `submit` lên BE