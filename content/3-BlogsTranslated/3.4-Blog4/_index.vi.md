---
title: "Blog 4"
date: "2025-09-08"
weight: 1
chapter: false
pre: " <b> 3.4. </b> "
---

# Cải thiện khả năng giám sát mạng với các chỉ số mới của AWS Outposts rack
<span class="meta-info">Tác giả: Adam Duffield | ngày: 06 tháng 08, 2025 | in</span> [Advanced (300)](https://aws.amazon.com/blogs/compute/category/learning-levels/advanced-300/), [Announcements](https://aws.amazon.com/blogs/compute/category/post-types/announcements/), [AWS Outposts](https://aws.amazon.com/blogs/compute/category/compute/aws-outposts/), [AWS Outposts rack](https://aws.amazon.com/blogs/compute/category/compute/aws-outposts/aws-outposts-rack/)  | [Permalink](https://aws.amazon.com/blogs/publicsector/integrate-ai-powered-coding-assistance-in-secure-environments-using-continue-and-amazon-bedrock/) 

Với [AWS Outposts racks](https://aws.amazon.com/outposts/rack/), bạn có thể mở rộng hạ tầng, dịch vụ, API và các công cụ AWS đến các địa điểm tại chỗ. Việc đảm bảo kết nối mạng hiệu suất cao, ổn định và có khả năng phục hồi giữa vùng AWS chính và mạng nội bộ là điều thiết yếu để duy trì dịch vụ không bị gián đoạn. 
Việc ra mắt hai chỉ số mới của [Amazon CloudWatch](https://aws.amazon.com/cloudwatch/) metrics, <span class='highlight-code'>VifConnectionStatus</span> and <span class='highlight-code'>VifBgpSessionState</span>, giúp bạn có cái nhìn rõ ràng hơn về trạng thái hoạt động của các kết nối mạng Outposts. Trong bài viết này, chúng tôi sẽ trình bày cách sử dụng các chỉ số này để nhanh chóng xác định sự cố mạng, đồng thời khai thác thêm các điểm dữ liêu cổ sung nhằm rút ngắn thời gian khắc phục sự cố. 


## Tổng quan về kết nối mạng Outposts
Khi kết nối với một Outposts với vị trí trung tâm dữ liệu mà bạn đã chọn, các kết nối mạng sẽ được thiết lập với thiết bị mạng Outposts (ONDs) và thiết bị mạng của khách hàng (CNDs). Những kết nối này đều được hỗ trợ cả kết nối [Service Link](https://docs.aws.amazon.com/outposts/latest/userguide/region-connectivity.html) kết nối trở về vùng AWS chính được chọn, cũng như kết nối mạng nội bộ tại chỗ thông qua[Local Gateway](https://docs.aws.amazon.com/outposts/latest/userguide/outposts-local-gateways.html). [First-generation Outposts racks](https://aws.amazon.com/blogs/aws/aws-outposts-now-available-order-your-racks-today/) bao gồm tối thiểu hai thiết bị mạng để đảm bảo khả năng phục hồi, trong khi các [second-generation Outposts racks](https://aws.amazon.com/blogs/aws/announcing-second-generation-aws-outposts-racks-with-breakthrough-performance-and-scalability-on-premises/) thì bao gồm bốn thiết bị mạng.

[Virtual interfaces (VIFs)](https://docs.aws.amazon.com/outposts/latest/network-userguide/vif-vif-groups.html) được sử dụng để thiết lập kết nối mạng IP giữa Outposts và CNDs, sử dụng giao thức Border Gateway (BGP) để định tuyến động. Bạn có thể xem chi tiết các VIF này trong bảng điều khiển Outposts bằng cách chọn nhóm tổng hợp liên kết Link aggregation groups (LAGs) trong bảng điều hướng và truy cập sâu vào thông tin VIF của service link và local gateway cụ thể. Với mỗi kết nối giữa một OND và một CND, hai phiên BGP sẽ được thiết lập: một phiên để hỗ trợ lưu lượng service link và một phiên để hỗ trợ lưu lượng local gateway.

Sơ đồ sau đây minh họa một ví dụ về cách kết nối mạng của Outposts rack thế hệ đầu tiên.

![Figure 1: First-Generation Outposts Rack network connections](/images/3-Blogs/Blog-4/image-1-29.png)
<span class="meta-info">*Hình 1: Kết nối mạng của Outposts rack thế hệ đầu tiên*</span>

Trong cấu hình này, tổng cộng có bốn giao diện ảo (VIFs) được thiết lập thành hai nhóm tổng hợp liên kết (LAGs): mỗi OND có một nhóm dành riêng cho VIF của service link và một nhóm dành cho VIF của local gateway.

## Hiểu về các chỉ số CloudWatch mới dành cho Outposts
Khả năng quan sát trạng thái hoạt động của Outposts rack — bao gồm cả trạng thái và hiệu suất của kết nối mạng — rất quan trọng để bạn có thể nhanh chóng xác định và điều tra các sự cố tiềm ẩn. Với việc bổ sung hai chỉ số mới <span class='highlight-code'>VifConnectionStatus</span> và <span class='highlight-code'>VifBgpSessionState</span>  trong CloudWatch, bạn có cái nhìn rõ ràng hơn về trạng thái kết nối giữa Outposts rack và các thiết bị mạng của khách hàng (CNDs). fConnectionStatuslà chỉ số được cung cấp theo từng VIF, áp dụng cho cả VIF của local gateway và service link. Chỉ số này phản ánh trạng thái của VIF thông qua hai giá trị:

- Giá trị 1 chỉ ra rằng VIF đã kết nối thành công với CND, phiên BGP đã được thiết lập và có thể truyền dữ liệu.
- Giá trị 0 chỉ ra rằng VIF không ở trạng thái hoạt động do có sự cố bên trong.

<span class='highlight-code'>VifBgpSessionState</span> đi sâu hơn vào trạng thái kết nối BGP giữa mỗi VIF của Outposts và CND. Một phiên BGP có thể nằm trong một trong các trạng thái sau, mỗi trạng thái cung cấp thông tin về vị trí có thể xảy ra sự cố:

1. IDLE – Trạng thái khởi đầu; ONDs đang chờ sự kiện bắt đầu.
2. Connect – Outposts rack đang chờ hoàn tất kết nối TCP.
3. Active – Outposts rack đang cố gắng khởi tạo kết nối TCP.
4. OpenSent – Router đã gửi thông điệp OPEN và đang chờ phản hồi.
5. OpenConfirm – Router đã nhận thông điệp OPEN và đang chờ phản hồi KEEPALIVE.
6. Established – Kết nối BGP đã được thiết lập hoàn chỉnh, ONDs và CNDs có thể trao đổi thông tin định tuyến.

Với các chỉ số này hiện đã có mặt trong CloudWatch, bạn có thể cấu hình [Amazon CloudWatch alarms](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/AlarmThatSendsEmail.html) để thông báo khi giá trị của chỉ số cho thấy có sự cố tiềm ẩn. Bạn cũng có thể kết hợp [CloudWatch metrics for Outposts](https://docs.aws.amazon.com/outposts/latest/userguide/outposts-cloudwatch-metrics.html) với các chỉ số mới này để bổ sung ngữ cảnh và tăng cường khả năng quan sát trạng thái kết nối mạng.
## Sử dụng các chỉ số CloudWatch để điều tra sự cố kết nối mạng của Outposts
Khi xảy ra sự cố kết nối mạng, điều quan trọng là phải hiểu cách sử dụng các chỉ số này để hỗ trợ quá trình điều tra và xác định nguyên nhân tiềm ẩn khi phát hiện sự suy giảm kết nối. Trước tiên, cần kiểm tra trạng thái cấu hình (Configuration state) của các VIF. Mỗi VIF có thể nằm trong một trong bốn trạng thái sau:

- Pending – VIF ở trạng thái này kể từ khi được tạo trong một [VIF group](https://docs.aws.amazon.com/outposts/latest/network-userguide/vif-vif-groups.html)  cho đến khi nó hoạt động trên OND
- Available – VIF đang hoạt động trên OND
- Deleting – VIF chuyển sang trạng thái này ngay sau khi có yêu cầu xóa
- Deleted – VIF đã bị xóa

Để kiểm tra trạng thái của một VIF cụ thể trên bảng điều khiển Outposts, hãy chọn Networking, sau đó chọn Link aggregation groups (LAGs) trong bảng điều hướng. Các VIF của service link và local gateway liên kết với một LAG cụ thể sẽ được hiển thị, và khi bạn chọn một LAG cụ thể, trạng thái cấu hình của các VIF liên quan sẽ hiện ra.

![Figure 2: AWS Outposts console showing VIF configuration details](/images/3-Blogs/Blog-4/image-2-23.png)
<span class="meta-info">*Hình 2: Bảng điều khiển AWS hiện thi chi tiết cấu hình VIF*</span>

Bạn cũng có thể truy xuất các thông tin này thông qua lập trình. Ví dụ, hãy sử dụng lệnh sau của [AWS Command Line Interface (AWS CLI)](http://aws.amazon.com/cli) để kiểm tra trạng thái cấu hình của một service link VIF có ID <span class='highlight=code'>sl-vif-087faf21db43ba723</span>:
```
aws ec2 describe-service-link-virtual-interfaces /
--service-link-virtual-interface-id sl-vif-087faf21db43ba723
{
    "ServiceLinkVirtualInterfaces": [
        {
            "ServiceLinkVirtualInterfaceId": "sl-vif-087faf21db43ba723",
            "ServiceLinkVirtualInterfaceArn": "arn:aws:ec2:us-west-2:111122223333:service-link-virtual-interface/sl-vif-087faf21db43ba723",
            "OutpostId": "op-07f6f537e0607d3f1",
            "OutpostArn": "arn:aws:outposts:us-west-2:111122223333:outpost/op-07f6f537e0607d3f1",
            "OwnerId": "280066404755",
            "LocalAddress": "XX.XX.XX.XX/XX",
            "PeerAddress": " XX.XX.XX.XX/XX ",
            "PeerBgpAsn": 65000,
            "Vlan": 2006,
            "OutpostLagId": "op-lag-03782b844d7da1afc",
            "Tags": [],
            "ConfigurationState": "available"
        }
    ]
}
```
Sau khi xác nhận trạng thái cấu hình (Configuration state), bạn có thể sử dụng chỉ số <span class='highlight-code'>VifConnectionStatus</span>  để xác định trạng thái kết nối mạng của từng VIF. Khi hoạt động bình thường và xử lý lưu lượng, giá trị của chỉ số này là 1. Nếu giá trị này chuyển sang 0, điều đó cho thấy có sự cố kết nối đối với VIF giữa Outpost và các thiết bị mạng của khách hàng (CNDs).

Để hiểu rõ hơn về nguyên nhân tiềm ẩn của giá trị VifConnectionStatus, bạn có thể sử dụng chỉ số VifBgpSessionState. Trong trạng thái hoạt động bình thường, giá trị của chỉ số này là 6, cho thấy phiên BGP đã được thiết lập và lưu lượng có thể được gửi và nhận. Tuy nhiên, nếu giá trị này chuyển sang 1–5, điều đó cho thấy có vấn đề. Để bắt đầu điều tra nguyên nhân, bạn nên xem lại cấu hình VIF cả trên bảng điều khiển Outposts lẫn thông qua lập trình. Điều này bao gồm các giá trị được thiết lập trên OND như VLAN, địa chỉ local và peer, và ASN của BGP. Các giá trị này có thể được đối chiếu với cấu hình trên các thiết bị CND tại chỗ nếu cần.

Ngoài ra, bạn có thể sử dụng giá trị của chỉ số VifBgpSessionState để xác định nguyên nhân tiềm ẩn:

- Nếu giá trị là 1, hãy xác thực các giá trị của BGP ASN và địa chỉ peer
- Nếu giá trị là 2, có thể là do sự cố về cổng hoặc địa chỉ IP
- Nếu giá trị là 3, có thể là do không tương thích phiên bản BGP
- Nếu giá trị là 4 hoặc 5, điều này liên quan đến sự cố đường truyền mạng

Bằng cách kết hợp các chỉ số này, bạn có thể hiểu rõ hơn về sự cố mạng tiềm ẩn mà không cần liên hệ với AWS hoặc các nhóm hỗ trợ bên thứ ba.
Bạn có thể xem và truy vấn các chỉ số này trên bảng điều khiển CloudWatch. Trong bảng điều hướng, chọn All metrics, sau đó chọn Outposts trong phần AWS namespaces. Namespace của Outposts chỉ có thể được xem bởi tài khoản chủ sở hữu, trừ khi đã cấu hình [cross-account observability](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/CloudWatch-Unified-Cross-Account.html) của CloudWatch. Các chỉ số mới <span class='highlight-code'>VifConnectionStatus</span> và <span class='highlight-code'>VifBgpSessionState</span> có thể được tìm thấy dưới các chiều <span class='highlight-code'>OutpostsID</span>, <span class='highlight-code'>VirtualInterfaceGroupId</span>, <span class='highlight-code'>VirtualInterfaceIInterfaceId</span>.

![Figure 3: Amazon CloudWatch metrics for AWS Outposts](/images/3-Blogs/Blog-4/image-3-2.png)
<span class="meta-info">*Hình 3: Các chỉ số Amazon CloudWatch dành cho AWS Outposts*</span>

Để biết thêm thông tin về cách làm việc với các chỉ số, hãy xem [Metrics in Amazon CloudWatch](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/working_with_metrics.html). Để tạo cảnh báo dựa trên các chỉ số mới này và giá trị của chúng, hãy tham khảo [Using Amazon CloudWatch alarms](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/AlarmThatSendsEmail.html).

Thiết kế có khả năng phục hồi nhờ sử dụng nhiều OND cho cả lưu lượng service link và local gateway cho phép các khối lượng công việc tiếp tục chạy ngay cả khi một VIF gặp sự cố kết nối. Ví dụ, một VIF của service link có thể báo là bị gián đoạn, nhưng các VIF còn lại vẫn hoạt động bình thường. Trong trường hợp này, service link vẫn duy trì chức năng và kết nối, mặc dù có thể giảm khả năng phục hồi và dung lượng. Điều này có thể được xác minh thông qua chỉ số ConnectedStatus, với giá trị là 1.

## Kết luận
Bài viết này đã cung cấp thông tin chi tiết về hai chỉ số CloudWatch mới dành cho Outposts rack:
<span class='highlight-code'>VifConnectionStatus</span> and VifBgpSessionState, cùng cách sử dụng chúng để điều tra các sự cố kết nối tiềm ẩn. Để biết thêm thông tin về các mô hình Networking của Outposts rack, hãy xem phần[Networking](https://docs.aws.amazon.com/whitepapers/latest/aws-outposts-high-availability-design/networking.html) trong tài liệu Outposts High Availability Design and Architecture Considerations whitepaper. Để biết thêm về các chỉ số CloudWatch bổ sung hiện có, hãy tham khảo tài liệu CloudWatch metrics for AWS Outposts documentation for [second-generation Outposts racks](https://docs.aws.amazon.com/outposts/latest/network-userguide/outposts-cloudwatch-metrics.html) và [first-generation Outposts racks](https://docs.aws.amazon.com/outposts/latest/userguide/outposts-cloudwatch-metrics.html).