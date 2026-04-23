Edited README_aws.md
Viewed README_aws.md:281-300

Dưới đây là bản **Báo cáo ngắn** được viết dựa trên kết quả chạy của bạn để bạn có thể copy vào bài nộp:

---

**BÁO CÁO KẾT QUẢ BENCHMARK VÀ LÝ DO SỬ DỤNG CPU**

**1. Đánh giá kết quả Benchmark:**
- **Training Time & Độ chính xác:** Mô hình LightGBM khi chạy trên CPU `r5.2xlarge` (8 vCPU, 32GB RAM) xử lý dữ liệu dạng bảng (tabular) cực kỳ tối ưu. Thời gian training siêu tốc chỉ mất vỏn vẹn **1.11 giây** nhưng mô hình vẫn đạt độ chính xác xuất sắc với chỉ số **AUC-ROC lên tới 0.9367** và Accuracy 99.9%.
- **Inference Speed:** Tốc độ suy luận (inference latency) rất ấn tượng, mô hình mất chưa tới nửa mili-giây (**0.4277 ms**) để dự đoán 1 giao dịch, và có throughput cực tốt khi xử lý 1000 giao dịch chỉ tốn **0.5598 ms**.

**2. Lý do sử dụng CPU thay vì GPU:**
- **Rào cản AWS Quota:** Các tài khoản AWS mới hoặc Free Tier hiện nay bị giới hạn quota nghiêm ngặt (mặc định = 0 vCPU) đối với các dòng máy GPU (như `g4dn.xlarge`). Việc yêu cầu tăng quota thường tốn nhiều ngày chờ đợi hoặc bị từ chối.
- **Tính phù hợp của bài toán:** Đối với bài toán phân loại dữ liệu dạng bảng (Credit Card Fraud), thuật toán Gradient Boosting như LightGBM chạy cực kỳ nhanh và hiệu quả trên multi-core CPU. Do đó, việc sử dụng máy chủ CPU cấu hình cao như `r5.2xlarge` (với chi phí tương đương) là giải pháp thay thế hoàn hảo, giúp đáp ứng toàn bộ quy trình MLOps thực tế mà không cần phụ thuộc vào phần cứng GPU.

---
