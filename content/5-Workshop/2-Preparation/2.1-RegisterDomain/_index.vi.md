---
title : "Đăng ký tên miền với Amazon Route 53"
date : "2025-10-10"
weight : 1
chapter : false
pre : " <b> 2.1 </b> "
---
1. Đăng nhập vào [AWS Management Console](https://aws.amazon.com/console/).
2. Trên thanh tìm kiếm phía trên, nhập `Route 53` và chọn dịch vụ **Route 53** từ kết quả tìm kiếm.

![search-route53](/images/2-Preparation/2.1-RegisterDomain/01-searchRoute53.png)

3. Trong bảng điều khiển Route 53, nhấp vào **Registered domains** trong menu điều hướng bên trái.
4. Nhấp vào nút **Register domain**.
![Route53-Dashboard](/images/2-Preparation/2.1-RegisterDomain/02-Route53Dashboard.png)

5. Trong trường **Choose a domain name**:
    - Nhập tên miền bạn muốn đăng ký. Trong bài lab này, chúng tôi sử dụng tên miền `test.name.vn`.
    - Nhấp vào nút **Search** để kiểm tra xem tên miền có khả dụng không.
    - Nếu tên miền khả dụng, nó sẽ xuất hiện trong danh sách **Search result** cùng với giá đăng ký hàng năm. Nhấp vào **Proceed to checkout**.
![Register-Domain](/images/2-Preparation/2.1-RegisterDomain/03-RegisterDomains.png)
6. Trong trường **Checkout**, hãy nhớ tắt tính năng **Auto-renew** nếu bạn không muốn trả bất kỳ khoản phí nào sau khi tên miền của bạn hết hạn. Nhấp vào **Next** để chuyển sang bước tiếp theo.

![Pricing](/images/2-Preparation/2.1-RegisterDomain/04-CheckoutPricing.png)

7. Trên trang **Contact details for your domain**, điền thông tin.
    {{% notice info %}} 💡**Quan trọng**: Đảm bảo bạn nhập một địa chỉ email hợp lệ và có thể truy cập được. AWS sẽ gửi một liên kết xác minh bắt buộc đến địa chỉ này.
    {{% /notice %}}

![Contact-Information](/images/2-Preparation/2.1-RegisterDomain/05-ContactInfo.png)

8. Trên trang **Review and complete your order**:
    - Kiểm tra cẩn thận xem thông tin của bạn có sai sót không
    - Chọn hộp kiểm để xác nhận bạn đã đọc và đồng ý với **Điều khoản và điều kiện**
    - Nhấp vào **Submit** để hoàn tất mua hàng.
    - Ngay sau khi hoàn tất đơn hàng, AWS sẽ gửi một email xác minh đến địa chỉ của bạn. Mở email này và nhấp vào liên kết xác minh bên trong.
![Contact-Information](/images/2-Preparation/2.1-RegisterDomain/06-ReviewInfo.png)
9. Khi bạn đăng ký tên miền thành công, AWS sẽ tự động tạo một **Hosted Zone** công khai
    - Trong khung điều hướng Route 53, nhấp vào **Hosted zones**.
    - Bạn sẽ thấy một Hosted Zone công khai mới với tên giống như tên miền bạn vừa đăng ký.
