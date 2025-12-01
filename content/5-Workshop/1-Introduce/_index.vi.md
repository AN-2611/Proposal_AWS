---
title : "Giới thiệu "
date : "2025-10-10"
weight : 2
chapter : false
pre : " <b> 1. </b> "
---
Application Load Balancer (ALB) không chỉ đơn thuần là một bộ phân phối lưu lượng truy cập. Nó đóng vai trò như một cổng vào thông minh và an toàn cho các ứng dụng hiện đại, giữ một vai trò quan trọng trong việc kiến trúc hệ thống có khả năng mở rộng, phục hồi và hiệu suất cao. Mặc dù việc thiết lập một bộ cân bằng tải cơ bản khá đơn giản, để khai thác hết tiềm năng của nó đòi hỏi sự hiểu biết sâu hơn về các khả năng nâng cao.

Bài thực hành này được thiết kế để lấp đầy khoảng trống đó. Chúng ta sẽ vượt ra khỏi những kiến thức cơ bản và đi sâu vào các tính năng mạnh mẽ cho phép bạn xây dựng môi trường ứng dụng tinh vi, hiệu quả và vận hành xuất sắc. Bạn sẽ học cách định tuyến lưu lượng truy cập với độ chính xác cao, hỗ trợ các giao thức truyền thông hiện đại và tinh chỉnh cấu hình của mình để đạt được tình trạng và hiệu suất tối ưu.

Khi kết thúc bài thực hành này, bạn sẽ không chỉ hiểu các tính năng này về mặt lý thuyết mà còn đã triển khai chúng một cách thực tế trong một môi trường thực tế.

### Mục tiêu học tập

Sau khi hoàn thành bài thực hành này, bạn sẽ có thể:

  - Triển khai các quy tắc định tuyến dựa trên nội dung phức tạp bằng cách sử dụng host header và đường dẫn URL để hướng lưu lượng truy cập đến các microservice khác nhau.
  - Kích hoạt và kiểm tra các giao thức hiện đại như HTTP/2 và WebSockets để nâng cao hiệu suất ứng dụng và cho phép giao tiếp thời gian thực.
  - Cấu hình sticky sessions (phiên cố định) để xử lý chính xác các yêu cầu của ứng dụng có trạng thái (stateful).
  - Tinh chỉnh các tham số kiểm tra tình trạng (health check) để phát hiện lỗi chuyển đổi (failover) nhanh hơn và tăng khả năng phục hồi của ứng dụng.
  - Thiết lập giám sát, ghi nhật ký và cảnh báo mạnh mẽ bằng Amazon CloudWatch để có được cái nhìn tổng quan về hoạt động của lưu lượng truy cập và tình trạng ứng dụng của bạn.
  - Phân tích các tác động về chi phí của các cấu hình ALB khác nhau và khắc phục sự cố thường gặp một cách hiệu quả.