## II. Thiết Lập & Chạy Thử Dự Án

### 1. Cài Đặt Thư Viện Phụ Thuộc

Trước khi chạy dự án, bạn cần đảm bảo tất cả các thư viện và gói phụ thuộc đã được cài đặt đầy đủ. 

*   **Đối với dự án .NET:**
    *   **Lệnh:** `dotnet restore`
    *   **Giải thích:** Lệnh này sẽ khôi phục các gói NuGet (NuGet packages) đã được liệt kê trong file dự án (`.csproj`, `.fsproj`, `.vbproj`). Nó sẽ tải về tất cả các dependencies cần thiết cho dự án từ các nguồn cấp gói (package sources) đã cấu hình.
    *   **Cú pháp:** Đảm bảo bạn đang ở thư mục gốc của dự án hoặc thư mục chứa file `.sln` (solution file) hoặc `.csproj` trước khi chạy lệnh này.
    *   **Lưu ý:** Bạn cần có .NET SDK được cài đặt trên hệ thống của mình để sử dụng lệnh `dotnet`.

*   **Đối với dự án Node.js:**
    *   **Lệnh:** `npm install` hoặc `yarn install`
    *   **Giải thích:**
        *   `npm install`: Lệnh này được sử dụng để cài đặt tất cả các gói Node.js (Node.js packages) được liệt kê trong file `package.json` của dự án. Các gói này sẽ được tải về và lưu trữ trong thư mục `node_modules`.
        *   `yarn install`: Tương tự như `npm install`, nhưng sử dụng Yarn làm trình quản lý gói. Yarn thường được biết đến với tốc độ nhanh hơn và quản lý dependency tốt hơn trong một số trường hợp.
    *   **Cú pháp:** Chạy lệnh này trong thư mục gốc của dự án nơi có file `package.json`.
    *   **Lưu ý:** Bạn cần cài đặt Node.js và npm (thường đi kèm với Node.js) hoặc Yarn trên hệ thống của mình. Nếu bạn muốn sử dụng `yarn`, bạn cần cài đặt nó riêng biệt (`npm install -g yarn`).

### 2. Thiết Lập File Cấu Hình

Các dự án thường sử dụng các file cấu hình để lưu trữ các thông tin nhạy cảm (như chuỗi kết nối cơ sở dữ liệu, khóa API) hoặc các cài đặt môi trường khác nhau (phát triển, kiểm thử, sản xuất).

*   **Đối với dự án .NET:**
    *   **File:** `appsettings.json` (hoặc `appsettings.Development.json`, `appsettings.Production.json`)
    *   **Giải thích:** Đây là file cấu hình tiêu chuẩn trong các ứng dụng .NET Core/.NET 5+. Nó sử dụng định dạng JSON để lưu trữ các key-value. Bạn có thể có nhiều file `appsettings.{Environment}.json` để quản lý cấu hình theo môi trường (ví dụ: `appsettings.Development.json` cho môi trường phát triển).
    *   **Cú pháp:** File này thường nằm ở thư mục gốc của dự án. Bạn cần chỉnh sửa các giá trị trong file này cho phù hợp với môi trường của bạn (ví dụ: cập nhật chuỗi kết nối cơ sở dữ liệu, cổng API).
    *   **Lưu ý:** Không nên commit các thông tin nhạy cảm (như mật khẩu, khóa API) trực tiếp vào file `appsettings.json` khi đẩy lên các hệ thống quản lý mã nguồn công khai (ví dụ: GitHub). Thay vào đó, hãy sử dụng biến môi trường (environment variables) hoặc Azure Key Vault/AWS Secrets Manager.

*   **Đối với dự án Node.js:**
    *   **File:** `.env` (hoặc các biến môi trường trực tiếp)
    *   **Giải thích:** File `.env` là một cách phổ biến để lưu trữ các biến môi trường cho ứng dụng Node.js. Các biến này thường được tải vào `process.env` khi ứng dụng khởi động thông qua các thư viện như `dotenv`.
    *   **Cú pháp:** File `.env` thường nằm ở thư mục gốc của dự án. Mỗi dòng trong file là một cặp `KEY=VALUE`. Ví dụ: `DATABASE_URL=your_database_connection_string`.
    *   **Lưu ý:** Luôn thêm file `.env` vào `.gitignore` để tránh đẩy các thông tin nhạy cảm lên Git. Các thông tin cấu hình cho các môi trường khác nhau (dev, staging, prod) nên được quản lý qua các file `.env` riêng biệt hoặc thông qua hệ thống quản lý biến môi trường của nền tảng triển khai (ví dụ: Heroku Config Vars, Kubernetes Secrets).

### 2.1 Cấu Trúc Thư Mục Dự Án Thường Gặp & Vị Trí File Cấu Hình

#### Dự án .NET (ví dụ Web API / MVC)

```
MyDotnetApp/
├── src/                    # (tuỳ chọn) Thư mục chứa mã nguồn chính
│   ├── MyDotnetApp.csproj  # File dự án chính
│   ├── Program.cs          # Điểm khởi chạy (entry point)
│   ├── Startup.cs          # (ASP.NET Core <6) cấu hình services & middleware
│   ├── Controllers/        # API Controllers
│   ├── Models/             # Các lớp mô hình (Entity / DTO)
│   ├── Services/           # Business logic layer
│   └── ...
├── tests/                  # (tuỳ chọn) Unit / Integration tests
├── appsettings.json        # Cấu hình mặc định (production / common)
├── appsettings.Development.json # Cấu hình cho môi trường Development
├── appsettings.Staging.json     # (tuỳ chọn) cấu hình staging
├── *.sln                   # Solution file (nếu dùng nhiều project)
└── README.md
```

* **File cấu hình đặt ở đâu?**  
  `appsettings*.json` thường đặt ngay **thư mục gốc** của project (chung cấp với `Program.cs`). Khi publish, các file này được copy vào thư mục build nhờ cấu hình trong `.csproj`.
* **Mẹo:** Với môi trường development, có thể dùng **User Secrets** (`dotnet user-secrets`) để lưu thông tin nhạy cảm thay vì commit vào `appsettings.*.json`.

#### Dự án Node.js (ví dụ REST API dùng Express)

```
MyNodeApp/
├── src/                 # (tuỳ chọn) mã nguồn chính
│   ├── index.js         # File khởi chạy chính
│   ├── routes/          # Định nghĩa các route
│   ├── controllers/     # Xử lý logic cho route
│   ├── models/          # Định nghĩa schema (ORM) hoặc lớp mô hình
│   ├── middlewares/     # Middleware tuỳ chỉnh
│   └── utils/           # Hàm tiện ích
├── config/              # (tuỳ chọn) tập tin cấu hình JS/JSON (ví dụ: config.js, default.json)
├── .env                 # Biến môi trường (dotenv)
├── package.json         # Khai báo dependencies & script
├── package-lock.json / yarn.lock
├── node_modules/        # (tự tạo) thư viện cài đặt
└── README.md
```

* **File cấu hình đặt ở đâu?**  
  - Biến môi trường thường nằm trong file `.env` ở **thư mục gốc**.  
  - Nếu dùng thư viện `config` hoặc `convict`, các file YAML/JSON JS cấu hình sẽ nằm trong **thư mục `config/`** với các profile `default.js`, `production.js`, `test.js`,…  
  - Các khoá bí mật (secret) trên production nên được cung cấp qua **environment variables** của nền tảng (Docker/Kubernetes/Cloud provider) thay vì commit vào repo.

### 2.2 So sánh dự án Node.js và .NET

| Khía cạnh khác biệt | Node.js | .NET (.NET Core) |
|---------------------|---------|------------------|
| Mô hình xử lý | Event-loop đơn luồng, non-blocking I/O – **tối ưu tác vụ I/O nhiều kết nối** | Đa luồng, Thread-pool, async/await – **tối ưu tác vụ CPU-bound & song song** |
| Ngôn ngữ & type-safety | JavaScript (động) / TypeScript (tùy chọn, bán tĩnh) – **học nhanh, linh hoạt** | C# (tĩnh, mạnh) – **type-safe, phù hợp code quy mô lớn** |
| Hệ sinh thái ưu thế | NPM packages đa dạng, cập nhật nhanh – **thích hợp prototyping, web realtime** | Thư viện enterprise, hỗ trợ lâu dài – **phù hợp hệ thống nghiệp vụ phức tạp** |
| Độ "khởi động nhanh" | Nhẹ, thời gian start-up ngắn, RAM thấp | Khởi động chậm hơn, footprint RAM lớn hơn một chút |
| Hỗ trợ cloud/PaaS | Phổ biến trên Vercel, Heroku, Serverless (AWS Lambda, Cloud Functions) | Tích hợp sâu Azure, hỗ trợ container & serverless (AWS Lambda .NET, Azure Functions) |
| Công cụ IDE chính | VS Code (nhẹ), WebStorm | Visual Studio (đầy đủ), Rider |

#### Khi nào nên chọn **Node.js**?
* Ứng dụng realtime (chat, WebSocket, IoT) cần xử lý nhiều kết nối I/O đồng thời.
* Startup cần **TTM (time-to-market)** nhanh, đội ngũ đã quen JavaScript trên cả frontend & backend.
* Microservice nhỏ, serverless function, prototyping hoặc API nhẹ.

#### Khi nào nên chọn **.NET**?
* Hệ thống doanh nghiệp, nghiệp vụ phức tạp đòi hỏi **tính toàn vẹn kiểu dữ liệu mạnh** và kiến trúc nhiều tầng.
* Dịch vụ yêu cầu hiệu năng cao ở tác vụ CPU-bound (xử lý ảnh, tính toán) hoặc cần tận dụng **đa luồng**.
* Tổ chức đã đầu tư vào **Microsoft stack / Azure** hoặc cần hỗ trợ lâu dài, bảo mật enterprise.

### 3. Chạy Thử Project

Sau khi đã cài đặt dependencies và cấu hình dự án, bạn có thể chạy thử ứng dụng của mình.

*   **Đối với dự án .NET:**
    *   **Lệnh:** `dotnet run` hoặc `F5` trong Visual Studio
    *   **Giải thích:**
        *   `dotnet run`: Lệnh này sẽ biên dịch (compile) và chạy ứng dụng .NET của bạn. Nó sẽ tự động tìm kiếm file khởi động của dự án và thực thi nó.
        *   `F5` trong Visual Studio: Nếu bạn đang sử dụng Visual Studio, nhấn `F5` sẽ biên dịch và khởi chạy dự án trong chế độ Debug, cho phép bạn đặt breakpoint và theo dõi luồng thực thi của ứng dụng.
    *   **Cú pháp:** Chạy `dotnet run` từ thư mục gốc của dự án hoặc thư mục chứa file `.csproj`.
    *   **Lưu ý:** Nếu có lỗi biên dịch, hãy kiểm tra output của console hoặc cửa sổ Output trong Visual Studio để xem chi tiết lỗi. Đảm bảo rằng tất cả các lỗi đã được khắc phục trước khi chạy.

*   **Đối với dự án Node.js:**
    *   **Lệnh:** `npm start` hoặc `node app.js` (hoặc file khởi động chính)
    *   **Giải thích:**
        *   `npm start`: Đây là một script được định nghĩa trong file `package.json` (mục `scripts`). Thường thì script `start` sẽ gọi lệnh để khởi chạy ứng dụng (ví dụ: `node server.js` hoặc `nodemon index.js`). Đây là cách khuyến nghị để chạy ứng dụng Node.js vì nó có thể bao gồm các bước tiền xử lý khác.
        *   `node app.js`: Lệnh này sẽ trực tiếp thực thi file JavaScript `app.js` (hoặc bất kỳ file JavaScript nào bạn chỉ định) bằng Node.js runtime. `app.js` thường là file khởi tạo chính của ứng dụng.
    *   **Cú pháp:** Chạy `npm start` hoặc `node <your_main_file.js>` từ thư mục gốc của dự án.
    *   **Lưu ý:** Kiểm tra file `package.json` để biết script `start` được định nghĩa như thế nào. Đối với các ứng dụng web Node.js, sau khi chạy lệnh, bạn có thể truy cập ứng dụng qua trình duyệt tại địa chỉ và cổng đã cấu hình (ví dụ: `http://localhost:3000`).

### 3.5 Các lệnh khác với `dotnet` và `node`

#### Lệnh CLI phổ biến cho .NET (`dotnet`)

| Lệnh | Mục đích | Ghi chú |
|------|----------|---------|
| `dotnet new console` | Tạo một project console mới | Thêm `-n <TenProject>` để đặt tên, `--framework net8.0` để chỉ rõ framework |
| `dotnet build` | Biên dịch (compile) toàn bộ solution hoặc project | Tạo thư mục `bin/Debug` hoặc `bin/Release` |
| `dotnet clean` | Xóa thư mục build (`bin`, `obj`) | Giúp "sạch" trước khi build/publish lại |
| `dotnet test` | Chạy toàn bộ bộ kiểm thử (unit/integration tests) | Cần có project test (*.Tests.csproj) |
| `dotnet publish -c Release -o ./publish` | Đóng gói và xuất bản ứng dụng | Thêm `--self-contained` để tạo bản tự-chứa (self-contained) |
| `dotnet add package <PackageName>` | Thêm NuGet package vào project | Tự động cập nhật file *.csproj |
| `dotnet remove package <PackageName>` | Gỡ bỏ NuGet package | – |
| `dotnet tool install -g dotnet-ef` | Cài đặt .NET Global Tool (ví dụ Entity Framework CLI) | Dùng `dotnet tool update -g <tool>` để nâng cấp |
| `dotnet watch run` | Tự động biên dịch & chạy lại khi mã nguồn thay đổi | Rất hữu ích khi phát triển API/web |
| `dotnet --info` | Hiển thị thông tin SDK & runtime đã cài đặt | Giúp debug các vấn đề version |

#### Lệnh CLI phổ biến cho Node.js (`node`, `npm`, `npx`)

| Lệnh | Mục đích | Ghi chú |
|------|----------|---------|
| `npm init -y` | Khởi tạo nhanh file `package.json` mặc định | Sửa các trường sau nếu cần |
| `npm install <pkg>` | Cài đặt package production | Thêm `-D` / `--save-dev` để cài dev-dependency |
| `npm uninstall <pkg>` | Gỡ bỏ package khỏi `package.json` | – |
| `npm run <script>` | Chạy script định nghĩa trong `package.json` | Ví dụ: `npm run build`, `npm run lint` |
| `npm test` | Thực thi script `test` | Chuẩn hoá cho unit test |
| `npm outdated` | Kiểm tra các package đã lỗi thời cần nâng cấp | – |
| `npm install -g <pkg>` | Cài đặt package toàn cục (global) | Cần quyền admin trên Windows hoặc sudo trên Unix |
| `npx <pkg>` | Chạy package tạm thời mà không cần cài đặt toàn cục | Ví dụ: `npx create-react-app` |
| `node --inspect index.js` | Khởi chạy Node với chế độ debug qua Chrome DevTools | Thêm `--inspect-brk` để dừng ở dòng đầu tiên |
| `nodemon index.js` | Tự động reload ứng dụng khi mã nguồn thay đổi | Cần `npm install -D nodemon` hoặc cài global |

### 4. Test API

Sau khi ứng dụng đã chạy, bạn cần kiểm tra các API cơ bản để đảm bảo chúng hoạt động đúng.

*   **Công cụ:** Postman hoặc Swagger UI
    *   **Postman:**
        *   **Giải thích:** Postman là một công cụ phổ biến cho việc phát triển, kiểm thử và tài liệu hóa API. Nó cung cấp một giao diện người dùng thân thiện để gửi các request HTTP (GET, POST, PUT, DELETE, v.v.) và xem phản hồi từ server.
        *   **Cách dùng:** Mở Postman, tạo một request mới, chọn phương thức HTTP, nhập URL của API endpoint (ví dụ: `http://localhost:5000/api/users`), và gửi request để xem kết quả.
    *   **Swagger UI (OpenAPI UI):**
        *   **Giải thích:** Swagger UI (hoặc OpenAPI UI) là một công cụ dựa trên web tự động tạo tài liệu và giao diện người dùng tương tác cho các API được mô tả bằng đặc tả OpenAPI (trước đây là Swagger). Nó cho phép bạn dễ dàng xem các API endpoint, mô hình dữ liệu, và thậm chí gửi request trực tiếp từ trình duyệt.
        *   **Cách dùng:** Nếu dự án của bạn đã tích hợp Swagger UI, bạn có thể truy cập nó qua trình duyệt (thường là `http://localhost:your_port/swagger` hoặc `http://localhost:your_port/api-docs`). Từ giao diện Swagger UI, bạn có thể chọn một endpoint, nhập các tham số cần thiết và "Execute" để kiểm tra API.
    *   **Lưu ý:**
        *   **Kiểm tra trạng thái (Status Codes):** Luôn chú ý đến mã trạng thái HTTP (ví dụ: 200 OK, 201 Created, 400 Bad Request, 401 Unauthorized, 404 Not Found, 500 Internal Server Error) để hiểu kết quả của request.
        *   **Kiểm tra dữ liệu trả về:** Đảm bảo dữ liệu trả về từ API đúng định dạng và nội dung như mong đợi.
        *   **Thử nghiệm các trường hợp khác nhau:** Kiểm tra với dữ liệu hợp lệ, dữ liệu không hợp lệ, trường hợp thiếu dữ liệu, v.v., để đảm bảo API xử lý đúng mọi tình huống.

#### Bảng so sánh Postman và Swagger UI

| Tính năng / Đặc điểm | Postman | Swagger UI |
|----------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Mục đích chính**   | Công cụ độc lập để kiểm thử, phát triển và tài liệu hóa API. Rất linh hoạt, hỗ trợ nhiều loại request HTTP, môi trường, script test, và workflow phức tạp. | Giao diện người dùng được tạo tự động từ đặc tả OpenAPI (trước đây là Swagger) của API. Mục đích chính là tài liệu hóa API một cách tương tác và cho phép kiểm thử trực tiếp từ trình duyệt. |
| **Cách sử dụng**     | Cần cài đặt ứng dụng desktop hoặc sử dụng phiên bản web. Người dùng tự xây dựng và quản lý các request, collections, môi trường. Yêu cầu kiến thức về cấu trúc request HTTP. | Tích hợp trực tiếp vào ứng dụng web của bạn (thường thông qua thư viện). Truy cập qua trình duyệt web. Giao diện được tạo tự động dựa trên định nghĩa API, người dùng chỉ cần điền tham số và thực thi. |
| **Tích hợp với dự án**| Công cụ độc lập, không cần tích hợp vào mã nguồn dự án. Có thể sử dụng với bất kỳ API nào. | Yêu cầu tích hợp thư viện và cấu hình trong mã nguồn dự án để tạo ra giao diện người dùng dựa trên đặc tả OpenAPI. |
| **Khả năng kiểm thử** | Mạnh mẽ, linh hoạt. Hỗ trợ tạo các kịch bản kiểm thử tự động, chạy collection, pre-request scripts, test scripts, và tích hợp với CI/CD. | Chủ yếu là kiểm thử thủ công từng endpoint một thông qua giao diện. Hạn chế về khả năng tạo kịch bản test phức tạp hoặc tự động hóa. |
| **Tài liệu hóa**     | Cho phép tạo Collection, lưu request, thêm mô tả chi tiết cho API. Có thể xuất (export) tài liệu. | Tài liệu hóa tự động, trực quan và luôn đồng bộ với mã nguồn (nếu được cấu hình đúng). Cung cấp thông tin chi tiết về từng endpoint, tham số, phản hồi, và mô hình dữ liệu. |
| **Khả năng chia sẻ**  | Dễ dàng chia sẻ Collections, môi trường với các thành viên trong nhóm thông qua Postman Workspace hoặc export/import. | Giao diện web có thể được chia sẻ dễ dàng bằng cách cung cấp URL. Tài liệu luôn được cập nhật khi code thay đổi (nếu tích hợp CI/CD). |
| **Ưu điểm**           | Linh hoạt, mạnh mẽ, hỗ trợ nhiều tính năng nâng cao (mock servers, monitors, CI/CD integration). Phù hợp cho cả Dev và QA. | Tự động sinh tài liệu, luôn đồng bộ với code. Giao diện trực quan, dễ dùng cho việc khám phá và kiểm thử nhanh các API. Không cần cài đặt thêm phần mềm. |
| **Nhược điểm**        | Yêu cầu cài đặt ứng dụng. Có thể trở nên phức tạp với các workflow lớn. | Hạn chế về khả năng kiểm thử nâng cao và tự động hóa. Phụ thuộc vào việc API được định nghĩa đúng theo đặc tả OpenAPI. |
| **Phù hợp cho**      | Phát triển API chuyên sâu, kiểm thử tự động, quản lý workflow API phức tạp, chia sẻ trong nhóm. | Khám phá API, tài liệu hóa tương tác, kiểm thử nhanh các endpoint cơ bản, làm quen với API. |



