---
title : "Yêu cầu SSL Certificate"
date : "2025-10-10"
weight : 4
chapter : false
pre : " <b> 4.1 </b> "
---

### Hướng dẫn chi tiết yêu cầu SSL Certificate trên AWS ACM

Dưới đây là các bước chi tiết để yêu cầu và cấu hình SSL Certificate sử dụng AWS Certificate Manager (ACM):

**1. Tìm kiếm và truy cập AWS Certificate Manager (ACM)**
- Trong thanh tìm kiếm của AWS Management Console, nhập `Certificate` và chọn **ACM**.
![Tìm ACM](/images/4-ACM/01-Find.png)

**2. Yêu cầu chứng chỉ**
- Nhấp vào **Request a certificate**.
- Trong phần **Request certificate**, chọn **Request a public certificate** và nhấp **Next**.
![Yêu cầu chứng chỉ](/images/4-ACM/02-RequestCert.png)

**3. Nhập tên miền**
- Trong phần **Request public certificate**:
  - Dưới **Fully qualified domain name**, nhập tên miền chính của bạn.
  - Nhấp vào **Add another name** để thêm wildcard (ví dụ: `*.yourdomain.com`), giúp bảo mật tất cả các subdomain dưới tên miền chính.
![Tên miền](/images/4-ACM/03-DomainName.png)

**4. Hoàn tất yêu cầu**
- Giữ nguyên các tùy chọn mặc định và nhấp **Request**.

**5. Tạo bản ghi trong Route 53**
- Nhấp vào chứng chỉ vừa tạo để xem chi tiết.
- Chọn **Create record in Route 53** để tự động thêm các bản ghi CNAME cần thiết vào hosted zone của bạn.
![Chi tiết chứng chỉ](/images/4-ACM/04-DetailsCert.png)

**6. Xác nhận và tạo bản ghi**
- Một trang xác nhận sẽ xuất hiện. Xem lại các bản ghi và nhấp **Create records**.
![Xem lại bản ghi](/images/4-ACM/05-ReviewRecords.png)

**7. Hoàn tất xác thực**
- Khi AWS xác thực thành công các bản ghi DNS, trạng thái của chứng chỉ sẽ chuyển từ **Pending validation** sang **Issued** (màu xanh lá cây).
![Thành công](/images/4-ACM/06-Success.png)