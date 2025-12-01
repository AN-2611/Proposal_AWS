
+++
title = "Tạo Mẫu khởi chạy EC2"
date = 2022
weight = 8
chapter = false
pre = "<b>8.1 </b>"
+++
1. Trong Bảng điều khiển quản lý AWS, truy cập dịch vụ EC2.
2. Trong ngăn điều hướng bên trái, cuộn xuống và nhấp vào **Launch Templates** (Mẫu khởi chạy). Nhấp vào nút **Create launch template** (Tạo mẫu khởi chạy).
![Bảng điều khiển EC2](/images/8-EC2LaunchTemplates/8.1-CreateEC2LaunchTemplate/01-EC2Dashboard.png)
3. Cấu hình chi tiết Mẫu:
   - **Launch template name** (Tên mẫu khởi chạy): `web-service-template`
   - **Template version description** (Mô tả phiên bản mẫu): `Initial version for web servers`
   - Dưới Amazon Machine Image (AMI), tìm kiếm **Amazon Linux 2**.
![Loại AMI](/images/8-EC2LaunchTemplates/8.1-CreateEC2LaunchTemplate/02-AMI.png)
   - Dưới **Instance type** (Loại phiên bản), chọn **t3.medium** từ danh sách thả xuống.
   - Chọn một cặp khóa hiện có từ danh sách thả xuống. Nếu bạn chưa có, bạn sẽ cần tạo nó trước. Điều này rất cần thiết để truy cập các phiên bản của bạn qua SSH nếu cần.
![Cặp khóa](/images/8-EC2LaunchTemplates/8.1-CreateEC2LaunchTemplate/03-keypair.png)
{{% notice tip %}}
Không cần chỉ định trực tiếp Subnet hoặc Vùng sẵn sàng (AZ) trong chính Mẫu khởi chạy. Mẫu khởi chạy là một bản thiết kế có thể tái sử dụng. Tốt nhất là bỏ qua các chi tiết cụ thể về mạng như subnet. Thay vào đó, bạn sẽ chỉ định subnet nào sẽ sử dụng sau này khi bạn tạo Nhóm Tự động Thay đổi Kích thước (Auto Scaling Group) sử dụng mẫu này. Điều này làm cho mẫu của bạn linh hoạt hơn.
{{% /notice %}}

   - Dưới Network settings (Cài đặt mạng), đảm bảo bạn không chọn subnet nào. Để trống trường này.
   - Đối với **Security groups** (Nhóm bảo mật), không sử dụng mặc định. Thay vào đó, tìm kiếm và chọn **web-sg** mà bạn đã tạo trước đó.
![Mạng](/images/8-EC2LaunchTemplates/8.1-CreateEC2LaunchTemplate/04-Networking.png)
   - Mở rộng phần **Advanced details** (Chi tiết nâng cao) ở phía dưới.
   - Cuộn xuống để tìm IAM instance profile (Hồ sơ phiên bản IAM). Chọn **RoleForEC2MonitoringUsingCloudWatchAgent** mà bạn đã tạo trước đó từ danh sách thả xuống.
![Vai trò IAM](/images/8-EC2LaunchTemplates/8.1-CreateEC2LaunchTemplate/05-IAMProfile.png)
   - Xem lại bảng **Summary** (Tóm tắt) ở bên phải để đảm bảo tất cả các cài đặt của bạn đều chính xác.
   - Nhấp vào nút **Create launch template** (Tạo mẫu khởi chạy).
1. Điều hướng đến Launch Templates một lần nữa.
   - Chọn **web-service-template** ban đầu.
   - Nhấp vào **Actions** -> Modify template (Create new version) (Sửa đổi mẫu (Tạo phiên bản mới))
![Vai trò IAM](/images/8-EC2LaunchTemplates/8.1-CreateEC2LaunchTemplate/06-ReuseTemplate.png)
   - Sửa đổi hai trường sau:
     - **Launch template name:** `api-service-template`
     - **Template version description**: `Template for the backend API servers`
   - **Network settings:** Tìm kiếm và chọn **api-sg**.
1. Bây giờ, bạn sẽ lặp lại chính xác quy trình tương tự cho mẫu WebSocket.
2. Điều hướng đến **Launch Templates** một lần nữa.
   - Chọn **web-service-template** ban đầu.
   - Nhấp vào **Actions** -> **Create new template from selected** (Tạo mẫu mới từ mục đã chọn)
   - Sửa đổi hai trường sau:
     - **Launch template name:** `websocket-service-template`
     - **Template version description**: `Template for the backend Websocket servers`
     - **Security group:** Chọn **websocket-sg**.
3. Bây giờ, bạn có ba Mẫu khởi chạy.
![Vai trò IAM](/images/8-EC2LaunchTemplates/8.1-CreateEC2LaunchTemplate/07-Result.png)
