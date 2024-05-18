Dưới đây là hướng dẫn chi tiết từng bước để deploy Docker container của bạn lên AWS Elastic Beanstalk, kèm theo hình ảnh cấu trúc thư mục dự án của bạn.

### Bước 1: Đăng ký và thiết lập AWS CLI

1. **Đăng ký tài khoản tại AWS**: Truy cập [AWS](https://aws.amazon.com/) và tạo tài khoản nếu bạn chưa có.

2. **Cài đặt AWS CLI**: Sử dụng pip để cài đặt AWS CLI.
   ```bash
   pip install awscli
   ```

3. **Cấu hình AWS CLI**:
   ```bash
   aws configure
   ```
   Nhập AWS Access Key ID, Secret Access Key, Region và Output Format theo yêu cầu.

### Bước 2: Cài đặt Elastic Beanstalk CLI

1. **Cài đặt Elastic Beanstalk CLI**:
   ```bash
   pip install awsebcli
   ```

### Bước 3: Tạo tệp `Dockerrun.aws.json`

Trong thư mục gốc của dự án của bạn (thư mục chứa các tệp như `Dockerfile`, `package.json`, v.v.), tạo một tệp mới có tên `Dockerrun.aws.json` với nội dung sau:

```json
{
  "AWSEBDockerrunVersion": "1",
  "Image": {
    "Name": "corentinth/it-tools:latest",
    "Update": "true"
  },
  "Ports": [
    {
      "ContainerPort": 80,
      "HostPort": 8080
    }
  ]
}
```

### Bước 4: Khởi tạo Elastic Beanstalk

1. **Mở Terminal** và điều hướng đến thư mục gốc của dự án của bạn:
   ```bash
   cd /path/to/your/project
   ```

2. **Khởi tạo Elastic Beanstalk**:
   ```bash
   eb init -p docker your-app-name
   ```
   Làm theo các hướng dẫn để cấu hình ứng dụng. Chọn khu vực và tạo một khoá SSH nếu cần.

3. **Tạo một môi trường Elastic Beanstalk**:
   ```bash
   eb create dev-tools-env
   ```
   xoá nó nếu lỗi
   eb terminate dev-tools-env

### Bước 5: Deploy ứng dụng

1. **Deploy ứng dụng lên Elastic Beanstalk**:
   ```bash
   eb deploy
   ```

2. **Kiểm tra trạng thái**:
   ```bash
   eb status
   ```

Sau khi deploy thành công, bạn sẽ nhận được một URL cho ứng dụng của bạn.

### Bước 6: Gắn domain từ Namecheap

1. **Đăng nhập vào tài khoản Namecheap của bạn**.

2. **Chọn domain bạn muốn trỏ**.

3. **Trong phần "Advanced DNS"**, thêm một bản ghi mới:
   - Type: CNAME Record
   - Host: @
   - Value: URL từ Elastic Beanstalk
   - TTL: Automatic

### Tóm tắt các bước
1. **Thiết lập AWS CLI và Elastic Beanstalk CLI**.
2. **Tạo tệp `Dockerrun.aws.json`**.
3. **Khởi tạo Elastic Beanstalk và tạo môi trường**.
4. **Deploy ứng dụng và kiểm tra trạng thái**.
5. **Gắn domain từ Namecheap**.

Với các bước trên, bạn có thể deploy ứng dụng của mình lên AWS Elastic Beanstalk và sử dụng domain từ Namecheap để trỏ đến ứng dụng của bạn.



```
docker tag it-tools:latest nghiahsgs/dev-tools:latest
docker push nghiahsgs/dev-tools:latest
```