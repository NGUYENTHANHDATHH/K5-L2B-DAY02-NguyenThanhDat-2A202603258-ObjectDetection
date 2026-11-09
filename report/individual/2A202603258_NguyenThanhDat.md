# Báo cáo cá nhân — Ngày 2 Object Detection

Đổi tên file theo `MSSV_HoTen.md`, ví dụ `20241234_NguyenVanAn.md`. Điền kết quả thật, xóa dòng hướng dẫn khi nộp. Xem [quy định nộp](../../SUBMISSION.md).

## 1. Thông tin học viên

- Họ tên: Nguyễn Thành Đạt
- MSSV: 2A202603258
- Email: nguyenthanhdatvn2005@gmail.com
- Lớp: L2B
- Link repo bài làm: https://github.com/NGUYENTHANHDATHH/K5-L2B-DAY02-NguyenThanhDat-2A202603258-ObjectDetection
- Link Colab đã chạy: https://colab.research.google.com/drive/1jjpzUGoG22-1IXcKFXUhrvNXKZg4Odvb?usp=sharing

## 2. Schema và mini guideline

Dẫn tới [GUIDELINE_MINI.md](../../GUIDELINE_MINI.md). Tóm tắt ba ca mơ hồ đã quyết định, cách áp dụng schema và phần cần giảng viên làm rõ.

## 3. Annotation và self-QC

- Số file nhãn train: 50
- Kết quả checker và lỗi đã xử lý: 38/50
- Danh sách ít nhất 10 ảnh đã rà bằng mắt: drive_001->drive_050
- Lỗi bỏ sót/box/class phát hiện khi rà và cách sửa: lỗi thừa box tại các drive_001->050. Sửa bằng cách loại bớt box thừa.
- Commit khóa nhãn ban đầu: Commit id: e0fe8a91c1204d75527b877a9aa81627eabce291, comment: "update data annotation"

## 4. Gold QC và rework

| Chỉ số              | Trước sửa | Sau sửa nếu có |
| ------------------- | --------: | -------------: |
| TP                  |       430 |            653 |
| FP                  |       440 |            178 |
| FN                  |       223 |              0 |
| Precision           |    0.4943 |         0.7858 |
| Recall              |    0.6585 |            1.0 |
| F1                  |    0.5647 |         0.8801 |
| mean_iou_of_matches |    0.8383 |         0.8935 |
| passed              |     false |           true |

Dẫn tới `outputs/annotation_evaluation.json` trong repo. Nếu rework, ghi ảnh, lỗi đã kiểm, quyết định sửa/giữ và lý do. Không suy nguyên nhân chỉ từ FP/FN. Không có rework thì ghi rõ.

## 5. Kết quả YOLO

- Runtime, GPU/CPU, phiên bản Ultralytics và Torch:
- Các tham số thay đổi so với notebook nếu có và lý do:
- Đường dẫn best checkpoint trong phiên chạy:

| Chỉ số trên 10 ảnh eval |             Giá trị |
| ----------------------- | ------------------: |
| Precision               |    0.53359014294716 |
| Recall                  |  0.5180851063829788 |
| mAP50                   |  0.5657289024990622 |
| mAP50–95                | 0.38896359013842996 |

Đặt cả 2 folder `assets/eval_predictions/` và `assets/yolo26_runs/` (giải nén từ `day2_colab_outputs.zip`) cạnh báo cáo và dẫn link tương đối. Không chỉ ghi số; chỉ ra ít nhất một ảnh và vật thể cụ thể.

Trả lời bốn câu hỏi cuối notebook:

1. Lớp nào recall thấp nhất là lớp truck. Tải ảnh drive_052
2. Nếu mAP50 cao nhưng mAP50–95 thấp, cần kiểm điều gì trên box? Cần kiểm tra box có lỏng không
3. Lỗi class nào có thể liên quan guideline? Dữ kiện nào hỗ trợ nhận xét? Lớp có khả năng liên quan guideline là truck. Recall của truck thấp nhất trong kết quả YOLO, trong khi mini guideline chưa nêu tiêu chí rõ để phân biệt truck với van/car.
4. Vì sao không dùng 10 ảnh eval để train? Vai trò validation của chúng trong notebook là gì? ảnh eval dùng để đánh giá model dựa trên dữ liệu chưa biết giúp biết các chỉ số chính xác hơn và không bị overfitting.

## 6. Khó khăn và cách xử lý

| Bước/thời điểm | Lỗi quan sát | Cách đã thử | Kết quả/còn thiếu |
| -------------- | ------------ | ----------- | ----------------- |
| Gold QC sau khi khóa nhãn | Nhiều box thừa và bỏ sót box; F1 ban đầu 0.5647, FP 440, FN 223 | Đối chiếu từng file với gold, xóa box thừa và bổ sung box thiếu trong `dataset/labels/train/` | F1 tăng lên 0.8801, FP còn 178, FN còn 0; mean IoU đạt 0.8935 |
| Train/eval YOLO trên 10 ảnh eval | Recall của lớp `truck` thấp nhất; mAP50 cao hơn mAP50–95 | Kiểm tra khả năng box bị lỏng, class imbalance và các trường hợp truck/van/car dễ nhầm theo guideline | Đã ghi nhận trong phần kết quả; còn thiếu confusion matrix/ảnh dự đoán để xác định chính xác lớp bị nhầm |

## 7. Tự đánh giá theo rubric

- Đã có: 50 file nhãn YOLO đúng basename; mini guideline có định nghĩa bốn lớp, quy tắc box và các ca mơ hồ; gold-set QC sau rework đạt F1 `0.8801` và mean IoU `0.8935`; pipeline có metrics trên 10 ảnh eval.
- Đã có một phần: đã ghi nhận lỗi bỏ sót/box thừa, recall thấp nhất của `truck`, và chênh lệch giữa mAP50 với mAP50–95.
- Còn thiếu/chưa kiểm được: chưa điền runtime, GPU/CPU, phiên bản Ultralytics/Torch và đường dẫn checkpoint; chưa bổ sung thư mục ảnh prediction, confusion matrix và ảnh vật thể cụ thể để minh họa phân tích lỗi.
- Không dùng `eval` để train và không sửa `gold_train_labels`; cần kiểm tra lại các file đầu ra trước khi nộp để hoàn thiện phần pipeline và phân tích.

## 8. Công cụ AI và tài liệu tham khảo

Ghi công cụ đã dùng, dùng ở bước nào và phần đã tự kiểm tra; không dùng thì ghi rõ. Liệt kê nguồn ngoài repo được sử dụng. Không ghi mật khẩu/token hoặc đính kèm gold train.
