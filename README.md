1.	Triển khai dự án

1.1	Tạo file yaml deployment cho frontend,be với việc kéo dockerfile từ private registry (harbor)
<img width="945" height="498" alt="image" src="https://github.com/user-attachments/assets/0272c678-54b7-4cd3-b235-28a947678d42" />

1.2	Tạo service, ingress để truy cập web

<img width="945" height="450" alt="image" src="https://github.com/user-attachments/assets/61c2f648-94ae-4bb5-b155-7dbad8a17ff5" />

<img width="945" height="445" alt="image" src="https://github.com/user-attachments/assets/8124e964-82d9-42ec-ad2b-34ad9c1cd3b1" />

1.3 Tạo file yaml configmap để cập nhật file code dev ngay trên rancher, đồng thời sử dụng secret để lưu thông tin cần bảo mật (ví dụ như thông số của file cấu hình hay tài khoản, mật khẩu database, …)
