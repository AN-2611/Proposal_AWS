+++
title = "Kiểm tra kết quả"
date = 2022
weight = 15
chapter = false
pre = "14. "
+++
Trong bước này, chúng ta sẽ kiểm tra kết quả cho các Dịch vụ Web, API, WebSocket sau đó đưa ra kết luận:

1. Kiểm tra Dịch vụ Web

   * **Điểm cuối đã kiểm tra:** https://test.name.vn/
   * **Quy tắc định tuyến:** Quy tắc mặc định chuyển tiếp đến Nhóm đích **web-tg**.
   * **Kết quả mong đợi:** Trình duyệt sẽ hiển thị trang chào mừng tĩnh được phục vụ bởi máy chủ web NGINX.

2. Kiểm tra Dịch vụ API

   * **Điểm cuối đã kiểm tra:** https://test.name.vn/api/
   * **Quy tắc định tuyến:** Quy tắc dựa trên đường dẫn (/api/\*) chuyển tiếp đến Nhóm đích **api-tg**.
   * **Kết quả mong đợi:** Trình duyệt sẽ hiển thị phản hồi JSON từ máy chủ API Node.js/Express.

3. Kiểm tra Dịch vụ WebSocket

   * **Điểm cuối đã kiểm tra:** wss://ws.test.name.vn
   * **Quy tắc định tuyến:** Quy tắc dựa trên máy chủ (ws.test.name.vn) chuyển tiếp đến Nhóm đích **websocket-tg**.
   * **Kết quả mong đợi:** Một ứng dụng khách kiểm tra WebSocket chuyên dụng sẽ thiết lập thành công kết nối liên tục và có thể gửi và nhận tin nhắn trong thời gian thực.
