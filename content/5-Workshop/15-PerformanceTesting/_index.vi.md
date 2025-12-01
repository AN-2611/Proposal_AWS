
+++
title = "Kiểm thử hiệu suất"
date = 2022
weight = 16
chapter = false
pre = "<b>15. </b>"
+++
1. Chúng ta sẽ sử dụng System Manager để kết nối với các phiên bản **web-sg** như bước **14. Kiểm tra kết quả**
2. Cập nhật hệ thống và cài đặt Java:
```bash
sudo yum update -y
sudo dnf update -y
sudo yum install -y java-11-amazon-corretto
```
3. Tải xuống phiên bản JMeter mới nhất (kiểm tra trang web chính thức để có liên kết mới nhất):
```bash
sudo cd /home/ssm-user
sudo mkdir jmeter_tests
sudo cd jmeter_tests
sudo wget https://dlcdn.apache.org//jmeter/binaries/apache-jmeter-5.6.3.tgz
```
4. Giải nén tệp
```bash
sudo tar -xzf apache-jmeter-5.6.3.tgz
```
5. Cách dễ nhất là tạo kế hoạch kiểm thử trên máy tính cục bộ của bạn bằng GUI JMeter và sau đó tải nó lên máy chủ. Bạn nên tham khảo các bài viết sau:
   - [Cài đặt Java trên Windows, Linux và macOS](https://www.geeksforgeeks.org/linux-unix/download-install-java-windows-linux-macos/)
   - [Cài đặt Apache JMeter trên Windows](https://www.geeksforgeeks.org/installation-guide/how-to-install-apache-jmeter-on-windows/)
6. Trên máy cục bộ của bạn, mở JMeter. Tạo một **Kế hoạch kiểm thử** đơn giản:
   - Nhấp chuột phải vào Test Plan -> **Add** -> **Threads (Users)** -> **Thread Group.**
     - **Number of Threads (users):** Số lượng người dùng đồng thời (ví dụ: 100).
     - **Ramp-up period (seconds):** Thời gian để khởi động tất cả các luồng (ví dụ: 10).
     - **Loop Count:** Số lần mỗi luồng sẽ chạy thử nghiệm. Chọn **Infinite** (Vô hạn)
![Nhóm luồng](/images/15-PerformanceTesting/01-ThreadGroup.png)
   - Nhấp chuột phải vào Thread Group -> **Add** -> **Sampler** -> **HTTP Request.**
     - **Protocol:** http hoặc https.
     - **Server Name or IP:** Dán tên miền của bạn **test.name.vn**. Không sử dụng IP của một phiên bản riêng lẻ.
     - **Path:** Điểm cuối API hoặc trang bạn muốn kiểm thử. Trong trường hợp này, để mặc định
![Nhóm luồng](/images/15-PerformanceTesting/03-HTTPRequest.png)
7. Lưu Kế hoạch kiểm thử dưới dạng tệp .jmx (ví dụ: web-service-test.jmx).
8. Điều hướng đến **S3** để tạo một bucket có tên: `testing-plan-946` sau đó tải tệp lên
![Tạo Bucket](/images/15-PerformanceTesting/04-CreateBucket.png)
9. Từ phiên SSM Session Manager trên EC2, tải tệp từ S3:
```bash
sudo aws s3 cp s3://testing-plan-946/web-service-test.jmx /home/ssm-user/jmeter_tests
```
10. Trong phiên SSH của bạn trên EC2, điều hướng đến thư mục bin của JMeter.
```bash
cd /home/ssm-user/jmeter_tests/apache-jmeter-5.6.3/bin/
```
11. Chạy thử nghiệm bằng chế độ non-GUI:
```bash
./jmeter -n -t /home/ssm-user/jmeter_tests/web-service-test.jmx -l /home/ssm-user/jmeter_tests/web-service-results.csv
```
12. Với 748.324 lưu lượng truy cập, CPU tăng vọt nhanh chóng 99.05%
![CPU cao](/images/15-PerformanceTesting/05-HighCPU.png)
13. Bạn cũng có thể xem biểu đồ trong Bảng điều khiển CloudWatch
![Bảng điều khiển CloudWatch](/images/15-PerformanceTesting/06-CWDashboard-2.png)
14. Ngay sau đó bạn sẽ nhận được một email cảnh báo
![Email cảnh báo](/images/15-PerformanceTesting/07-Email.png)