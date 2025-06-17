# YARN INSTALL

## 1. Cài đặt Yarn

Vì Yarn không được cài đặt chung với NodeJS như npm, ta phải cài đặt thêm nó để sử dụng.

Có thể sử dụng npm để cài đặt Yarn như các thư viện khác:

    npm install --global yarn

## 2. Thêm dependancy bằng Yarn

Để thêm một thư viện mới vào dự án bằng Yarn, bạn có thể sử dụng lệnh sau trong terminal:

    yarn add [package]

Trong đó:

- [package] là tên của thư viện.

Câu lệnh này sẽ cài đặt thư viện được yêu cầu cùng với các thư viện khác mà nó phụ thuộc

Ví dụ, nếu bạn muốn thêm thư viện `lodash`, bạn chỉ cần chạy:

    yarn add lodash

Ngoài ra, câu lệnh sau trong Yarn được sử dụng để cài đặt một phiên bản cụ thể của một thư viện vào dự án. Cấu trúc của lệnh:

    yarn add [package]@[version]

Trong đó:

- [package] là tên của thư viện.
- [version] là phiên bản cụ thể mà bạn muốn sử dụng.

Ví dụ, nếu bạn muốn cài đặt phiên bản 4.17.21 của thư viện lodash, bạn sẽ chạy:

    yarn add lodash@4.17.21

Lưu ý:

- Bạn có thể dùng các ký hiệu như `^` hoặc `~` để xác định phạm vi phiên bản. Ví dụ, `lodash@^4.17.0` sẽ cài phiên bản mới nhất từ `4.17.0` trở lên nhưng không lên phiên bản `5.x.x`.

Lệnh sau cho phép bạn cài đặt một thư viện với một tag cụ thể thay vì chỉ định phiên bản chính xác. Cấu trúc:

    yarn add [package]@[tag]

Trong đó:

- [package] là tên của thư viện.
- [tag] là một nhãn (tag) do nhà phát triển thư viện đặt để chỉ định một phiên bản cụ thể.

Ví dụ, nếu bạn muốn cài đặt phiên bản beta của thư viện react, bạn có thể chạy:

    yarn add react@beta

Một số tag phổ biến:

- `latest` – Cài đặt phiên bản mới nhất (mặc định của Yarn).
- `next` – Thường là phiên bản thử nghiệm tiếp theo.
- `beta` hoặc `alpha` – Phiên bản chưa chính thức, thường dùng để thử nghiệm.
- `lts` – Phiên bản hỗ trợ dài hạn (Long-Term Support), nếu thư viện có cung cấp.

## 3. Các flag thường dùng với `yarn add`

Lệnh yarn add có nhiều flag hữu ích giúp bạn kiểm soát cách cài đặt thư viện. Dưới đây là một số flag phổ biến:

- `--dev` hoặc `-D`: Cài đặt thư viện vào `devDependencies` (chỉ dùng trong môi trường phát triển).

        yarn add typescript --dev

- `--peer` hoặc `-P`: Cài đặt thư viện vào `peerDependencies`, thường dùng cho thư viện chia sẻ.

        yarn add react --peer

- `--optional` hoặc `-O`: Cài đặt thư viện vào `optionalDependencies`, không bắt buộc để chạy ứng dụng.

        yarn add some-package --optional

- `--exact` hoặc `-E`: Cài đặt đúng phiên bản cụ thể của một package mà không tự động cập nhật lên phiên bản mới hơn. Điều này giúp đảm bảo tính ổn định của dependencies trong dự án.

        yarn add lodash@4.17.21 --exact
        // hoặc
        yarn add lodash@^4.17.21

- `--tilde` hoặc `-T`: Cài đặt phiên bản gần nhất trong cùng nhánh nhỏ của một package. Điều này có nghĩa là nếu bạn chỉ định một phiên bản cụ thể, Yarn sẽ cài đặt phiên bản mới nhất trong phạm vi đó, nhưng không nâng cấp lên phiên bản lớn hơn.

        yarn add lodash@ --tilde
        // hoặc
        yarn add lodash@~4.17.0

## 4. So sánh npm vs. yarn

Dưới đây là bảng so sánh giữa **npm** và **Yarn**:

| **Tiêu chí**            | **npm**                                  | **Yarn**                                         |
| ----------------------- | ---------------------------------------- | ------------------------------------------------ |
| **Tốc độ**              | Cài đặt tuần tự, chậm hơn                | Cài đặt song song, nhanh hơn                     |
| **Quản lý phiên bản**   | Sử dụng `package-lock.json`              | Sử dụng `yarn.lock`, đảm bảo đồng nhất phiên bản |
| **Bảo mật**             | Kiểm tra cơ bản                          | Có cơ chế kiểm tra tính toàn vẹn                 |
| **Cách hoạt động**      | Tải và cài đặt trực tiếp từ npm registry | Sử dụng bộ nhớ cache để tăng hiệu suất           |
| **Giao diện dòng lệnh** | Cú pháp đơn giản, phổ biến               | Có nhiều tùy chọn nâng cao                       |
