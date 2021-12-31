# API

# API là gì?

- API là viết tắt của Application Programming Interface – phương thức trung gian kết nối các ứng dụng và thư viện khác nhau.

- Nó cung cấp khả năng truy xuất đến các dữ liệu, từ đó có thể trao đổi dữ liệu giữa các ứng dụng.

- API là những gì (dữ liệu) phía BE cung cấp cho FE để FE sử dụng và render ra giao diện. Là những hành động cơ bản như lấy ra, thêm, xóa, sữa data

# 4 đặc điểm nổi bật của API

- Nó cung cấp khả năng truy xuất đến một tập các hàm hay dùng, từ đó có thể trao đổi dữ liệu giữa các ứng dụng.

- API có khả năng đáp ứng đầy đủ các thành phần HTTP: URI, request/response headers, caching, versioning, content forma…. Bạn có thể sử dụng các host nằm trong phần ứng dụng hoặc trên IIS.

- Hỗ trợ RESTful đầy đủ các phương thức như: GET, POST, PUT, DELETE các dữ liệu

- Được đánh giá là một trong những kiểu kiến trúc hỗ trợ tốt nhất với các thiết bị có lượng băng thông bị giới hạn như smartphone, tablet…

# Giới thiệu về `fetch` gọi api từ phái BE

- Javascript cung cấp hàm `fetch` với đầy đủ các tính năng để có thể thao tác với api từ phía BE cung cấp

- `fetch` hỗ trợ đầy đủ các phương thức: GET (lấy ra), POST (thêm vào), PUT (chỉnh sửa), DELETE (xóa),...

- `fetch` cũng cung cấp các bổ sung cho header như cache, form data (gửi file), custom header (Bổ sung các variable cho header)

# Code demo

- Lấy danh sách data từ api
- Lấy 1 data cụ thể
- Thêm data
- Chỉnh sửa 1 data
- Delete data

# Bài tập

- Gọi api lấy danh sách bài posts và render ra giao diện: GET

- Thêm bài post sử dụng phương thức POST

- Update post sử dụng phương thức PUT

- Delete post sử dụng DELETE


Link api demo:

https://61cedbf665c32600170c7dd9.mockapi.io/products

https://61cedbf665c32600170c7dd9.mockapi.io/users

https://61cedbf665c32600170c7dd9.mockapi.io/posts