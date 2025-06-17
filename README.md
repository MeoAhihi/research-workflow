# Ý TƯỞNG CHUẨN BỊ NỘI DUNG

## Nội dung

Khuyến khích mọi người soạn nội dung theo dạng:

- **Q&A:** Mô tả câu hỏi và câu trả lời
- **Liệt kê:** Dùng danh sách đánh số, ko đánh số, hoặc bảng
- **Ngắn gọn:** Dễ học và trả lời nhanh nhất có thể

```
Q: Điểm khác nhau giữa RESTful và graphQL là gì?

A: RESTful API và GraphQL đều là cách tiếp cận để thiết kế API, nhưng chúng có những điểm khác biệt quan trọng:

- Endpoint: REST có nhiều endpoint cố định, GraphQL chỉ có một endpoint duy nhất.
- Truy vấn dữ liệu: REST trả về dữ liệu cố định, GraphQL cho phép lấy đúng dữ liệu cần thiết.
- Overfetching & Underfetching: REST có thể trả về quá nhiều hoặc quá ít dữ liệu, GraphQL tối ưu hóa truy vấn.
- Hiệu suất: GraphQL giảm số lượng request cần thiết, giúp tối ưu hiệu suất hơn REST.
- Cấu trúc: REST dựa trên tài nguyên và phương thức HTTP, GraphQL sử dụng schema và truy vấn dạng JSON.
```

## Cú pháp markdown cơ bản

- tiêu đề trang, h1: `# [heading 1]`
- đề mục, h2, h3: `## [heading 2]`, `### [heading 3]`
- liệt kê bullet: `- [content]`
- liệt kê đánh số: `1. [content]` (mỗi dòng cứ bắt đầu `1.`, file sẽ tự cập nhật số)
- kiểu chữ: `**Bold**`, `*Italic*`
- đóng khung: 
```
> [content]
>
> [content]
>
> [content]
```
- code:
```JavaScript
    ```[Language]
    [code]
    [code]
    ```
```
- bảng:
```
|Name|Age|City|
|---|---|---|
|Alice|25|New York|
|Bob|30|London|
|Eve|22|Tokyo|
```