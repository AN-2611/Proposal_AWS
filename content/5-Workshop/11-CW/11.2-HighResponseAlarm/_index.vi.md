
+++
title = "Tạo báo động số lượng yêu cầu"
date = 2022
weight = 4
chapter = false
pre = "<b>11.2 </b>"
+++
1. Cuộn xuống **Metrics** (Chỉ số) từ menu thả xuống, nhấp vào **All metrics** (Tất cả chỉ số)
    - Điều hướng đến **ApplicationELB** > **Per AppELB, per TG Metrics** (Mỗi AppELB, mỗi chỉ số TG)
    - Tìm **web-tg** của bạn và chọn chỉ số **RequestCountPerTarget**
    - Chọn **Create alarms** (Tạo báo động)
![Chỉ số EC2](/images/11-CW/11.2-HighResponseAlarm/01-CWDashboard.png)
1. Điều kiện:
    - **Threshold type** (Loại ngưỡng): Static
    - **Whenever RequestCountPerTarget is...** (Bất cứ khi nào RequestCountPerTarget là...): Greater (Lớn hơn)
    - **than...** (hơn...) 1000
![Chỉ số EC2](/images/11-CW/11.2-HighResponseAlarm/02-SpecifyMetric-2.png)
1. Nhấp vào **Next** (Tiếp theo), cấu hình hành động để gửi thông báo đến chủ đề SNS **alb-alerts** của bạn, đặt tên báo động là `Web-Request-Count-Alarm` và tạo nó.
![Chỉ số EC2](/images/11-CW/11.2-HighResponseAlarm/03-AddAlarmDetails-2.png)
1. Lặp lại các bước này nếu cần cho các nhóm đích API và WebSocket của bạn.
