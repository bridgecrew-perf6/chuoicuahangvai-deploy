# Hướng dẫn cài đặt và triển khai hệ thống quản lý chuỗi cửa hàng bán vải lẻ bằng Docker
Hệ thống chuỗi cửa hàng vải lẻ được cài đặt và triển khai trên hệ điều hành Ubuntu phiên bản 18.04 LTS.
## Cài đặt
### Cài đặt Docker
Ta chạy tuần tự các lệnh sau để cài đặt Docker:
1. Xóa docker đã cài đặt (nếu có)
```
sudo apt-get remove docker docker-engine docker.io containerd runc
```
2. Cập nhật và cài đặt các ứng dụng cần thiết để cài đặt Docker
```
sudo apt-get update
```
```
sudo apt-get install \
    ca-certificates \
    curl \
    gnupg \
    lsb-release
```
3. Cài đặt Docker
```
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
```
```
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```
```
sudo apt-get update
```
```
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-compose-plugin
```
### Build hệ thống bằng Docker compose
Để đồng bộ dữ liệu (gồm database và file media), ta copy file database.sql và thư mục uploads tương ứng trong thư mục data.

Ta chạy lệnh sau để build hệ thống:
```
docker-compose build
```
## Triển khai
Ta sử dụng Docker compose để triển khai hệ thống đã build:

```
docker-compose down && docker-compose up -d
```