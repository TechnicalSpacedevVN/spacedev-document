# Git và cách sử dụng git

# 1. Git là gì?
<br />
_ 1 Dự án thường có nhiều lập trình viên phát triển song song. Vì vậy họ cần một hệ thống theo đỗi nỗi dung và đảm bảo không có sự xung đột trong code khi nhiều lập trình viên làm việc với nhau
<br />
<br />
_ Git là một phần mềm kiểm soát phiên bản nguồn mở, miễn phí 
<br />
<br />
_ Làm việc nhóm hiệu quả, mọi thay đổi sẽ được ghi lại với tên của người thay đổi
<br />
<br />
_ Ngoài ra các yêu cầu trong dự án thường thay đổi thường xuyên. Vì vậy một hệ thống quản lý code sẽ cho phép họ quay lại version cũ của code
<br />
<br />

---------
# 2. Cài đặt git
- **Bước 1** : Cài đặt phần mềm git : https://git-scm.com/downloads

- **Bước 2** : Cài đặt thông tin cá nhân

  - `git config --global user.name "Nguyen Van A"`
  - `git config --global user.email "nguyenvana@gmail.com"`

<br />
<br />

--------
# 3. Cách Git hoạt động

- Nếu chúng ta muốn bắt đầu sử dụng Git, chúng ta cần biết nơi lưu trữ các repository của mình. (Repository là nơi lưu trữ code). Có 2 loại Repo là Local repo (code trên máy tính đang sử dụng) và Remote repo (Code lưu trữ trực tuyến trên internet)


- Có nhiều nơi trực tuyến dùng để lưu trữ code vd: Github, Gitlab, BitBucket,...

- Khi làm việc, lập trình viên sẽ làm việc trên Local Repo của mỗi người. Và sau khi code xong 1 chức năng nào đó, họ sẽ push code lên Remote Repo để các lập trình viên khác có thể pull về.


* Push: Đẩy code từ máy cá nhân lên Remote Repo.

* Pull: Lấy code từ Remote repo xuống máy cá nhân.

* Clone: Lấy nguyên source code từ remote repo về local repo
<br />
<br />

--------
# 3. Sử dụng và các câu lệnh cơ bản
<br />

## 1. Tạo kho lưu trữ git trên mạng (Github)
Truy cập link và tạo 1 Repository để lưu trữ code dự án: https://github.com/
<br />
<br />

## 2. Cài đặt git cho code local: 
Truy cập vào folder dự án, chạy lệnh `git init`


--> Tạo Local Repo trên dự án, một tập tin ẩn `.git` sẽ được thêm vào mã nguồn của code. Kể từ lúc này, mọi thay đổi trên  code sẽ được theo dỗi và ghi vào tập folder `.git`


<br />
<br />

## 3. Thêm Remote Repo cho dự án: 
`git remote add [repo-name] [link-repo]`


--> Khi làm việc nhóm, và code được lưu trữ trên internet thông qua một Repo. Thì chúng ta phải thêm Repo đó vào dự án code hiện tại.\
vd: `git remote add origin https://github.com/dangthuyenvuong/cfd-template`

-- `origin` tên của repo chúng ta tự đặt, nhưng thường sẽ có một repo chính tên là `origin`

--> Kiểm tra repo đang được remote

`git remote -v`

<br />
<br />


## 4. Commit code
--> Khi code xong 1 chức năng nào đó, chúng ta có nhu cầu update sự thay đổi đó vào Local Repo:

- **B1**: Kiểm tra trạng thái của những file có thay đổi: 
- 
`git status`

- **B2**: Thêm tất cả những file có thay đổi vào hàng đợi: 
- 
`git add .`


  --> Trong trường hợp muốn thêm cụ thể 1 file nào đó: `git add [tên file]`
  
- **B3**: Đưa code vào trong git: 

`git commit -m "[comment]"`

<br />
<br />

## 5. Tạo branch cho git
`git branch [branch-name]`

`git checkout [branch-name]`

--> Branch là những nhánh của code, mõi git sẽ có nhiều branch. Tùy thuộc vào cách chia branch của leader mà mình có thể tạo nhiều branch với những tên khác nhau. Từ khi checkout branch mới, mọi code được commit sẽ được lưu ở branch đang checkout \
<br />
--> Các cách chia branch:
1. Mõi lập trình viên lập trình trên mõi branch khác nhau
2. Mõi chức năng mới sẽ lập trình trên mõi branch khác nhau
3. Sẽ luôn luôn có 1 branch làm branch chính (có thể là `master` hoặc `main`)
<br />
<br />


## 6. Push code lên Remote Repo
- Hiện tại, mọi sự thay đổi chỉ diễn ra ở Local Repo, những lập trình viên khác vẫn chưa nhận được thông báo về sự thay đổi đó. Bạn cần push code từ Local Repo lên Remote Repo để thông báo sự thay đổi đó cho các lập trình viên khác.\
`git push [repo-name] [branch-name]`
- Khi code được push lên remote repo, bạn phải tạo Merge Request (MR) vào branch master để thông báo cho leader (chủ của repo) merge code của bạn vào code trên repo. Sau bước này, code trên nhánh master ở remote repo sẽ được thay đổi, các thành viên khác có thể pull code mới về
<br />
<br />

# Lưu ý:
1. Nên ghi rõ comment của mỗi commit để biết được code đó thay đổi để làm gì
2. Trước mõi ngày bắt đầu code, cần pull code mới từ nhánh master về nhánh đang làm: `git pull [repo-name] [branch-name]`
3. Trước khi push code lên Remote Repo phải pull code từ master về, trong trường hợp có xung đột code với người khác, cần merge code thủ công `git pull [repo-name] [branch-name]`
4. Merge request khi code xong
5. Tạo file `.gitignore` để đưa những file không cần theo dỗi vd: node_modules
