
+++
title = "Tạo bảng điều khiển CloudWatch"
date = 2022
weight = 5
chapter = false
pre = "<b>11.3 </b>"
+++
1. Trong menu CloudWatch, nhấp vào **Dashboards** (Bảng điều khiển).
2. Nhấp vào **Create dashboard** (Tạo bảng điều khiển).
![Bảng điều khiển CW](/images/11-CW/11.3-CreateCloudWatchDashboard/01-CWDashboard.png)
3. Tên bảng điều khiển: `Application-Health-Dashboard`. Chọn **Create dashboard** (Tạo bảng điều khiển).
4. Thêm **Widget**:
    - Nhấp vào **Add widget** (Thêm widget). Chọn biểu đồ **Line** (Đường). Nhấp vào **Configure** (Cấu hình).
    - Chọn **Metrics** (Chỉ số), sau đó điều hướng đến **ApplicationELB** > **Per AppELB, per TG Metrics** (Mỗi AppELB, mỗi chỉ số TG).
    - Chọn **RequestCountPerTarget**
    - Trong tab **Graphed metrics** (Chỉ số được vẽ biểu đồ), thay đổi **Statistic** (Thống kê) thành **Sum** (Tổng).
![Bảng điều khiển CW](/images/11-CW/11.3-CreateCloudWatchDashboard/02-ChangeStatistic.png)
1. Nhấp vào nút **+** để thêm widget CPU Utilization:
![Bảng điều khiển CW](/images/11-CW/11.3-CreateCloudWatchDashboard/03-Button.png)
    - **Widget type** (Loại widget): Line
    - Chọn **Next** (Tiếp theo)
    - Đi tới **EC2** > By **Auto Scaling Group.** (Theo Nhóm Tự động điều chỉnh). Chọn chỉ số **CPUUtilization** cho cả ba Nhóm Tự động điều chỉnh của bạn.
    - Nhấp vào **Create widget** (Tạo widget).
![Bảng điều khiển CW](/images/11-CW/11.3-CreateCloudWatchDashboard/04-ChooseASG.png)

1. Tiếp tục nhấp vào nút **+** để thêm Widget Healthy Hosts
    - **Widget type** (Loại widget): Line
    - Đi tới **ApplicationELB** > By **Per AppELB, Per TG Metrics.** (Theo Mỗi AppELB, Mỗi Chỉ số TG).
    - Chọn chỉ số **UnHealthyHostCount** cho cả ba nhóm đích của bạn.
    - Nhấp vào **Create widget** (Tạo widget).
1. Chúng tôi đã tạo bảng điều khiển cho widget RequestCountPerTarget, UnHealthyHostCount, CPUUtilization
![Bảng điều khiển CW](/images/11-CW/11.3-CreateCloudWatchDashboard/05-Result.png)
