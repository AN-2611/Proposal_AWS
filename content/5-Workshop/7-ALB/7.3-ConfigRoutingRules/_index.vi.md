
+++
title = "Cấu hình Quy tắc định tuyến"
date = 2022
weight = 4
chapter = false
pre = "<b>7.3 </b>"
+++
1. Quay lại chi tiết Load Balancer: **advanced-alb**.
   - Chọn hộp kiểm **HTTPS:443**
   - Chọn **Manage rules** từ menu thả xuống
   - Chọn **Edit rule**
![Bảng điều khiển EC2](/images/7-ALB/7.3-ConfigRoutingRules/01-ALBDashboard.png)
   - Chọn **Add rule**
2. Trong trang **Add rule**:
   - Chọn **Path** từ **Add Conditions**: `/api/*`
   - **Hành động định tuyến (Routing action)**: Chuyển tiếp đến các nhóm đích (target groups)
   - **Nhóm đích (Target group)**: api-tg
   - Chọn **Next**
![Thêm quy tắc API](/images/7-ALB/7.3-ConfigRoutingRules/03-AddAPIRule.png)
3. Tiếp tục tạo một quy tắc khác:
   - Chọn **Host header** từ **Add Conditions**: `ws.test.name.vn`
   - **Hành động định tuyến (Routing action)**: Chuyển tiếp đến các nhóm đích (target groups)
   - **Nhóm đích (Target group)**: websocket-tg
   - Chọn **Next**
![Thêm quy tắc API](/images/7-ALB/7.3-ConfigRoutingRules/04-HostHeaderRule.png)

