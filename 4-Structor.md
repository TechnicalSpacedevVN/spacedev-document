# Cấu trúc của một dự án Reactjs
# 1. public
1. index.html -> Toàn bộ request sẽ được điều hướng đến file index.html
2. Những file assets dạng external, index.html có thể truy cập được tất cả những file nằm trong public, không thể truy cập trong src
# 2. src
- Nơi chứa toàn bộ logic chính của react, những file trong src sẽ không thể truy cập các file public và ngược lại
- index.js file React chính, từ file này sẽ import các component cần thiết
# 3. components
- Những component dùng chung trong hệ thống
# 4. pages
- Component riêng cho page
# 5. layout
- Chứa các component dạng layout
# 6. constant
- Những biến dạng const sử dụng trong toàn hệ thống
- Path
- Api
# 7. services
- Các service chứa các lệnh gọi api
# 8. assets
- Chứa các file assets chung, chỉ được sử dụng trong src
- Có 1 file style chứa các biến chung, tất cả các component phải import file này
# 9. hooks
- Chứa các custom hook

<br />
<br />
