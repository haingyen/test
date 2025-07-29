# Triển khai ứng dụng nodejs lên k8s cluster (minikube)

## Mô tả
## Tech Stack
## Đánh giá


1. Chuẩn bị
- Server (ec2)
- Cài docker lên server
- Cài minikube lên server
- Cài kubectl lên server
- Chạy Jenkins Container cùng mạng với minikube
2. Chuẩn bị ứng dụng và cấu hình manifest k8s
- deployment.yaml
- service.yaml - test với NodePort
4. CI/CD
- Cấu hình kết nối Jenkins với K8s dùng kubeconfig nếu jenkins ngoài cluster ngược lại dùng service account