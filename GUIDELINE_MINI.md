# Mini guideline — bài làm cá nhân

> Điền nội dung này trước khi bắt đầu gán nhãn. Giữ lại các quyết định sau khi self-QC.

## Định nghĩa lớp

| Lớp     | Định nghĩa của bạn                                                    | Ví dụ/điểm phân biệt            |
| ------- | --------------------------------------------------------------------- | ------------------------------- |
| `car`   | Xe con, kích thước nhỏ/vừa, thường chở người                          | Sedan, hatchback, SUV nhỏ       |
| `truck` | Xe tải dùng để chở hàng, thường có thùng hoặc cabin lớn               | Xe tải có thùng hàng            |
| `bus`   | Xe buýt chở nhiều hành khách, thân xe dài và cao                      | Xe buýt nội thành, xe khách lớn |
| `van`   | Xe thân hộp, kích thước nhỏ/vừa, thường có khoang chở người hoặc hàng | Minivan, xe van giao hàng       |

## Quy tắc chung

- Box bám sát vật thể nghĩa là: ôm sát phần thân xe nhìn thấy được, không lấy thêm mặt đường, trời hoặc xe bên cạnh.
- Vật thể bị che khuất: vẫn gán box quanh phần nhìn thấy được nếu còn đủ dấu hiệu nhận diện lớp.
- Vật thể bị cắt bởi rìa ảnh: box chạm đúng rìa ảnh, không đoán phần nằm ngoài ảnh.
- Vật thể rất nhỏ/mơ hồ: không tự đoán lớp; ghi lại ảnh và hỏi giảng viên.

## Ghi lại quyết định cho ít nhất ba ca mơ hồ

| Ảnh                               | Tình huống                        | Quyết định cuối                    | Lý do theo schema                               |
| --------------------------------- | --------------------------------- | ---------------------------------- | ----------------------------------------------- |
| `drive_002`                       | Box của bus trùng với box của car | Vẽ hai box riêng                   | Mỗi xe hợp lệ phải có một box riêng             |
| `drive_003`                       | Xe bị cắt bởi rìa ảnh             | Vẽ box đến đúng rìa ảnh            | Không đoán phần xe nằm ngoài ảnh                |
| `drive_006, drive_013, drive_015` | Xe car bị cắt bởi rìa ảnh         | Không vẽ box                       | Phần hiển thị không đủ để thể hiện lớp          |
| `drive_020`                       | Xe bị che khuất bởi cầu đi bộ     | Không vẽ box, hỏi giảng viên       | Không đoán phần xe bị che khuất                 |
| `drive_017`                       | Cam bị mờ khó phân biệt xe        | Tạm thời không gán, hỏi giảng viên | Không tự đoán khi không xác định chắc lớp       |
| `drive_025`                       | Xe bị mờ do tốc độ khung hình     | Không vẽ box, hỏi giảng biên       | Không gãn phần xe khi vật thể chưa đủ thông tin |
