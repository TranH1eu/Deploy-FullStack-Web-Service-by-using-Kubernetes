## 1. Triển khai dự án

### 1.1. Tạo file YAML deployment
Tạo file deployment cho `frontend` và `backend` bằng cách kéo image từ Private Registry (`Harbor`).

<p align="center">
  <img src="https://github.com/user-attachments/assets/d45069cc-a980-4ad8-8cdf-b0afe551afa1" width="80%" alt="Harbor Registry">
  <br>
  <i> Đã push thành công image frontend và backend lên Harbor Private Registry</i>
</p>




---

### 1.2. Tạo Service & Ingress để truy cập Web
Cấu hình các tài nguyên `Service` và `Ingress` trên cluster.

<p align="center">
  <img src="https://github.com/user-attachments/assets/f6a0c1fe-a73c-4f20-8d32-c0f952f2ab79" width="80%" alt="Harbor Registry">
  <br>
  <i> Tạo ingress để truy cập service đã tạo</i>
</p>

<p align="center">
  <img src="https://github.com/user-attachments/assets/59000b87-fcb7-4f82-913f-d87391412148" width="80%" alt="Harbor Registry">
  <br>
  <i> Web service khi truy cập dựa trên đường link đã tạo từ ingress</i>
</p>



---

### 1.3. Tạo file configmap 
Cập nhật code trực tiếp trên rancher, đồng thời sử dụng secret để lưu các thông tin tăng tính bảo mật(localhost, port, tài khoản, mật khẩu, ...)

<p align="center">
  <img src="https://github.com/user-attachments/assets/d8635069-b587-4d36-be08-0acc69dfa2c6" width="80%" alt="Harbor Registry">
  <br>
  <i> sử dụng configmap để cấu hình trực tiếp trên rancher kết hợp secret để hỗ trợ bảo mật</i>
</p>

---

### 1.4. Cấu hình hpa (horizontal pod autoscale) 
Xử lý những khi bị quá tải pod sẽ scale để giảm tải trên pod cố định

<p align="center">
  <img src="https://github.com/user-attachments/assets/0afbc9db-cfbb-48cc-ba1d-3d866a1c6c41" width="80%" alt="Harbor Registry">
  <br>
  <i> Giả lập quá tải cpu để giảm tải cho 1 cluster nhất định</i>
</p>

## 2. Monitoring

### 2.1. Prometheus
Kéo dữ liệu , quét các thông số về tốc độ hoạt động của web

<p align="center">
  <img src="https://github.com/user-attachments/assets/836178b7-e963-4fbd-b460-db349b10897e" width="80%" alt="Harbor Registry">
  <br>
  <i> Danh sách các exporter và trạng thái kết nối</i>
</p>

---

### 2.2. Grafana:
Hiển thị chính xác các thông số liên quan đến network, cpu, ram, bộ nhớ 

<p align="center">
  <img src="https://github.com/user-attachments/assets/6031772f-f312-48b5-a283-c39f7c24cffd" width="80%" alt="Harbor Registry">
  <br>
  <i> Grafana hiển thị thông số về cpu và bộ nhớ được sử dụng của dự án ecommerce trên cluster với pods fe,be</i>
</p>

---

### 2.3. Uptime-kuma:
Theo dõi tình trạng uptime/downtime của web từ đó gửi thông báo về telegram

<p align="center">
  <img src="https://github.com/user-attachments/assets/70644bcd-fe6d-42e7-b1c2-353e903202ea" width="80%" alt="Harbor Registry">
  <br>
  <i> Theo dõi trạn thái web theo chu kỳ và khi có thay đổi sẽ gửi thông báo về telegram</i>
</p>


## 3. Backup

### 3.1. Minio:
Để lưu lại các bản backup dữ liệu và các bản restore

<p align="center">
  <img src="https://github.com/user-attachments/assets/ea33eec2-5f30-4b37-8d6b-296158e3b7b0" width="80%" alt="Harbor Registry">
  <br>
  <i> Folder gồm các file backup và đã được restore của namespace ecommerce</i>
</p>

---

### 3.2. Velero:
Được sử dụng trên cluster để liên kết giữa minio và k8s (thực hiện lưu trữ hoặc restore)

<p align="center">
  <img src="https://github.com/user-attachments/assets/57aa2ba5-8971-41e6-8664-562ae160b40b" width="80%" alt="Harbor Registry">
  <br>
  <i> Ví dụ lưu trữ dự án với namespace ecommerce</i>
</p>

### Về cấu trúc:

#### Đầu tiên ở phần triển khai bằng cách tạo file yaml với:
 ##### Deployment: triển khai bằng Dockerfile được pull từ private registry
 ##### Service: để cân bằng tải, cho phép truy cập từ trong cụm k8s
 ##### Ingress: để truy cập web dựa trên port mà service đã tạo
 ##### ConfigMap: Chèn dữ liệu trực tiếp trên k8s 
 ##### Secret: Tăng tính bảo mật của web thông qua mã hóa các tham số trực tiếp ví dụ localhost, port, user, password
 ##### HorizontalPodAutoscale: Để kiểm soát khi có lượng truy cập lớn, tránh downtime (giảm tải cho pod nhất định)
#### Tiếp theo ở phần monitoring:
  ##### Các ứng dụng monitoring được triển khải dựa trên helm chart với mô hình pv-pvc-storageClass
#### Cuối cùng backup với velero:
  ##### Từ việc liên kết với minio qua accessKey và secretkey, minio sẽ là nơi được lưu và lấy dữ liệu để restore.


