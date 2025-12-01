+++
title = "Bật Phiên gắn kết (Sticky Sessions)"
date = 2022
weight = 5
chapter = false
pre = "<b>7.4 </b>"
+++
1. Trong ngăn điều hướng bên trái, dưới mục **Load Balancing**, nhấp vào **Target Groups.**
![Bảng điều khiển EC2](/images/7-ALB/7.4-EnableStickySessions/01-EC2Dashboard.png)
2. Từ danh sách các nhóm đích, chọn hộp kiểm bên cạnh **web-tg** của bạn. Nhấp vào menu thả xuống Actions ở trên cùng bên phải. Chọn **Edit attributes.**
![Hộp kiểm web-tg](/images/7-ALB/7.4-EnableStickySessions/02-webtgActionDropdown.png)
3. Trên trang **Edit attributes**, tìm phần **Stickiness**.
   - Chọn hộp để **Turn on stickiness** (Bật tính năng gắn kết).
   - **Stickiness duration** (Thời gian gắn kết): Nhập 1 và chọn days (ngày) từ menu thả xuống.
   - **Stickiness type** (Loại gắn kết): Load balancer generated cookie (Cookie do bộ cân bằng tải tạo).
   - Nhấp vào nút **Save changes** (Lưu thay đổi).
![Bật tính năng gắn kết](/images/7-ALB/7.4-EnableStickySessions/03-TurnOnStickiness.png)
