# Render có điều kiện

- Trong React, để render 1 dữ liệu ra DOM ta để biến vào trong dâu ngoặc `{ }`, biểu thức sẽ được tính toán và render ra UI 

- Những dữ liệu được render là những kiểu dữ liệu nguyên thủy hoặc array đơn giản

- Khi muốn render dữ liệu là `array`, ta dùng hàm `map` và truyền vào `key` cho mỗi Element được render, React sẽ dựa theo key để quản lý sự render của Element đó

- Khi muốn dựa theo điều kiện nào đó để render, ta dùng điều kiện 3 ngôi trong html hoặc có thể tạo biến phía trên return và sử dụng ở phía dưới html

- Không được render nguyên 1 object (sẽ bị lỗi)

