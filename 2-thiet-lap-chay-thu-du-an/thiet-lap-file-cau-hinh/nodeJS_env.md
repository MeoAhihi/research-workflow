# THIẾT LẬP FILE CẤU HÌNH NODEJS

Trong Node.js, file cấu hình thường được sử dụng để lưu trữ các thiết lập quan trọng như thông tin kết nối cơ sở dữ liệu, cài đặt server, biến môi trường, và nhiều thứ khác.

Có nhiều cách để thiết lập cấu hình NodeJS, nhưng phổ biến nhất là file `.env`

## File `.env`

File .env trong Node.js được sử dụng để lưu trữ biến môi trường, giúp quản lý các thông tin nhạy cảm

Bạn có thể tạo một file `.env` trong thư mục gốc của dự án và khai báo các biến như sau:

    NODE_ENV=development
    PORT=3000
    DATABASE_URL=mongodb://localhost:27017/mydb

Các quy tắc đặt biến trong `.env`:

1. **Tên biến phải viết hoa**: Điều này giúp dễ phân biệt với các biến thông thường trong mã nguồn.
1. **Không có dấu cách xung quanh dấu `=`**: Nếu có dấu cách, giá trị có thể bị lỗi khi đọc.
1. **Giá trị có thể được đặt trong dấu nháy** nếu chứa ký tự đặc biệt:

        SECRET_KEY="my-secret-key"

1. **Không sử dụng dấu `#` trong giá trị** vì nó được hiểu là comment.
1. **Không commit file `.env` vào Git**: Hãy thêm `.env` vào `.gitignore` để tránh lộ thông tin nhạy cảm.

Có thể có nhiều file `.env` theo môi trường: 
        
        .env.development
        .env.production
        .env.test

- `.env.development` → Dùng cho môi trường phát triển, thường chứa thông tin dành cho lập trình viên

- `.env.production` → Dành cho môi trường sản xuất (production), thường chứa thông tin bảo mật hơn

- `.env.test` → Dùng khi chạy test, giúp tạo môi trường kiểm thử độc lập

Khi dự án được chia sẽ cho nhiều developers, bạn cũng cần chia sẽ file `.env` nhưng vẫn giữ bí mật thông tin nhạy cảm. Bạn có thể dùng `.env.example` để làm việc này. Hãy tạo một file `.env.example` với các biến môi trường nhưng không có giá trị thực:

```
DATABASE_URL=
PORT=
SECRET_KEY=
```


## Đọc biến môi trường trong NodeJS

Để đọc file `.env` trong Node.js, bạn có thể sử dụng thư viện `dotenv`, hoặc tận dụng tính năng mới của Node.js để load trực tiếp file `.env`. Dưới đây là hai cách phổ biến:

### **1. Sử dụng thư viện `dotenv`**
Thư viện `dotenv` giúp bạn dễ dàng load các biến môi trường từ file `.env` vào `process.env`. Các bước thực hiện:

- **Cài đặt thư viện**:
  ```
  npm install dotenv
  ```

- **Tạo file `.env`**:
  ```
  PORT=3000
  DATABASE_URL=mongodb://localhost:27017/mydb
  ```

- **Sử dụng trong mã nguồn**:
  ```javascript
  require('dotenv').config();
  console.log(process.env.PORT); // 3000
  ```

### **2. Sử dụng `--env-file` của Node.js**
Từ phiên bản Node.js 20, bạn có thể sử dụng tham số `--env-file` để load file `.env` mà không cần thư viện `dotenv`:

- **Tạo file `.env`**:
  ```
  PORT=3000
  ```

- **Chạy ứng dụng với file `.env`**:
  ```
  node --env-file=.env app.js
  ```

- **Có thể load nhiều file `.env`**:
  ```
  node --env-file=.env --env-file=.development.env app.js
  ```

