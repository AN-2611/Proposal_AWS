
+++
title = "Tạo báo động CPU cao"
date = 2022
weight = 3
chapter = false
pre = "<b>11.1 </b>"
+++
1. Cuộn xuống **Metrics** (Chỉ số) từ menu thả xuống, nhấp vào **All metrics** (Tất cả chỉ số)
    - Điều hướng đến **EC2** > **Auto Scaling Group**
    - Tìm **web-service-asg** của bạn và chọn chỉ số **CPUUtilization**
    - Chọn **Create alarms** (Tạo báo động)
![Chỉ số EC2](/images/11-CW/11.1-HighCPUAlarm/06-CPUUtilization.png)
1. Điều kiện:
    - **Threshold type** (Loại ngưỡng): Static
    - **Whenever CPUUtilization is...** (Bất cứ khi nào CPUUtilization là...): Greater/Equal (Lớn hơn/Bằng)
    - **than...** (hơn...): 80 (%)
![Chỉ số EC2](/images/11-CW/11.1-HighCPUAlarm/07-ConfigCPUUtilization.png)
1. Nhấp vào **Next** (Tiếp theo), cấu hình hành động để gửi thông báo đến chủ đề SNS **alb-alerts** của bạn, đặt tên báo động là `Web-Service-High-CPU` và tạo nó.
![Chỉ số EC2](/images/11-CW/11.1-HighCPUAlarm/08-ConfigNoti.png)
1. Lặp lại các bước này nếu cần cho các nhóm đích API và WebSocket của bạn.
