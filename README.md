## 1. Triển khai dự án

### 1.1. Tạo file YAML deployment
Tạo file deployment cho `frontend` và `backend` bằng cách kéo image từ Private Registry (`Harbor`).

<p align="center">
  <img src="https://github.com/user-attachments/assets/d45069cc-a980-4ad8-8cdf-b0afe551afa1" width="80%" alt="Harbor Registry">
</p>




---

### 1.2. Tạo Service & Ingress để truy cập Web
Cấu hình các tài nguyên `Service` và `Ingress` trên cluster.

<p align="center">
  <img src="https://github.com/user-attachments/assets/f6a0c1fe-a73c-4f20-8d32-c0f952f2ab79" width="80%" alt="Harbor Registry">
  <br>
  <i> Đã push thành công image frontend và backend lên Harbor Private Registry</i>
</p>

<p align="center">
  <img src="https://github.com/user-attachments/assets/59000b87-fcb7-4f82-913f-d87391412148" width="80%" alt="Harbor Registry">
</p>



---

### 1.3. Tạo file configmap 
Cập nhật code trực tiếp trên rancher, đồng thời sử dụng secret để lưu các thông tin tăng tính bảo mật(localhost, port, tài khoản, mật khẩu, ...)

<p align="center">
  <img src="https://github.com/user-attachments/assets/d8635069-b587-4d36-be08-0acc69dfa2c6" width="80%" alt="Harbor Registry">
</p>

