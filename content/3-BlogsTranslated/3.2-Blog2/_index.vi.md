---
title: "Blog 2"
date: "2025-09-08"
weight: 1
chapter: false
pre: " <b> 3.2. </b> "
---


# Những hiểu biết và bài học từ Amazon Q trong Connect tại NatWest
Tác giả: Prabhakar Rajasekar, Abhay Kumar, Georgina Williams, and Prateek Guleria | ngày 02 tháng 04, 2025 | in [Amazon Connect](https://aws.amazon.com/blogs/contact-center/category/messaging/amazon-connect/), [Amazon Q](https://aws.amazon.com/blogs/contact-center/category/amazon-q/), [Customer Solutions](https://aws.amazon.com/blogs/contact-center/category/post-types/customer-solutions/), [Generative AI](https://aws.amazon.com/blogs/contact-center/category/artificial-intelligence/generative-ai/), [Intermediate (200)](https://aws.amazon.com/blogs/contact-center/category/learning-levels/intermediate-200/), [Thought Leadership](https://aws.amazon.com/blogs/contact-center/category/post-types/thought-leadership/) | [Permalink](https://aws.amazon.com/blogs/contact-center/insights-and-learning-of-amazon-q-in-connect-at-natwest/)

Nhân viên tổng đài là thành phần quan trọng trong bất kỳ trung tâm liên lạc nào, và điều thiết yếu là các tổ chức phải cung cấp cho họ những công cụ phù hợp để thành công. Bằng cách hỗ trợ nhân viên một cách hiệu quả, các công ty không chỉ cải thiện trải nghiệm làm việc của họ mà còn nâng cao trải nghiệm của khách hàng cuối.

Để đáp ứng nhu cầu này, Amazon Connect cung cấp [Amazon Q in Connect](https://aws.amazon.com/connect/q/), một trợ lý AI tạo sinh, có khả năng đưa ra các đề xuất cá nhân hóa theo thời gian thực nhằm giúp nhân viên thực hiện công việc một cách hiệu quả và chính xác hơn.

Để triển khai hỗ trợ nhân viên bằng AI tạo sinh, bạn cần cân nhắc nhiều yếu tố như chiến lược thử nghiệm và tác động đến trải nghiệm của nhân viên. Trong bài viết này, bạn sẽ tìm hiểu cách NatWest Group, một tổ chức tài chính lớn, đã triển khai Amazon Q in Connect. Chúng tôi sẽ tập trung vào những thách thức cụ thể gặp phải trong quá trình kiểm thử chấp nhận người dùng (UAT). Những thách thức này bao gồm việc lựa chọn các “ý định” (intents) phù hợp để thử nghiệm, tích hợp với hệ thống tri thức cũ, và đánh giá mức độ thành công của giai đoạn thử nghiệm. Chúng tôi cũng sẽ chia sẻ các giải pháp đã được thiết kế để vượt qua một số thách thức này.

## Giải quyết các vấn đề kinh doanh cốt lõi bằng AI tạo sinh
[NatWest Group](https://www.natwestgroup.com/) là một ngân hàng tập trung tại Vương quốc Anh, phục vụ hơn 19 triệu khách hàng, hoạt động trong các lĩnh vực ngân hàng bán lẻ, thương mại và ngân hàng tư nhân.

Bằng cách tận dụng [Amazon Q in Connect](https://youtu.be/zbrLI6ktTcg?t=2623), NNatWest đặt mục tiêu cung cấp kết quả hoặc quyết định phù hợp cho khách hàng một cách nhanh chóng, với trọng tâm đặc biệt vào việc tuân thủ quy trình của nhân viên và giảm thời gian xử lý trung bình mỗi tương tác (Average Handle Time – AHT). Việc triển khai chiến lược này mang lại nhiều lợi ích:

Lợi ích tức thời:
  - Giải quyết yêu cầu của khách hàng nhanh hơn
  - Giảm thời gian xử lý cho mỗi tương tác
  - Xử lý yêu cầu khách hàng hiệu quả hơn
  - Tăng cường tuân thủ các quy trình và hướng dẫn chuẩn của nhân viên, giúp giảm sai sót và khiếu nại từ khách hàng

Tác động dài hạn:
  - Cải thiện Chỉ số hài lòng khách hàng (Net Promoter Score – NPS) nhờ nâng cao trải nghiệm
  - Mang lại trải nghiệm khách hàng tổng thể tốt hơn

Để đánh giá hiệu quả của Amazon Q in Connect, NatWest đã lựa chọn một nhóm giới hạn gồm các nhân viên giàu kinh nghiệm nhất trong một bộ phận kinh doanh duy nhất để tiến hành thử nghiệm ban đầu.

## Tích hợp quản lý tri thức
Amazon Q in Connect cung cấp khả năng tích hợp liền mạch với nhiều hệ thống backend thông qua các kết nối dựng sẵn, bao gồm hỗ trợ gốc cho Salesforce và tích hợp với các trang web dành cho khách hàng. Trong trường hợp của NatWest, mặc dù họ vẫn duy trì hệ thống quản lý tri thức riêng, nhưng trong giai đoạn thử nghiệm ban đầu, họ đã chọn cách tiếp cận đơn giản hơn bằng cách sử dụng Amazon S3 làm kho lưu trữ tri thức liên kết với Amazon Q in Connect.


## Cách NatWest kiểm thử Amazon Q in Connect
Các tổ chức có thể sử dụng Amazon Q in Connect trong không gian làm việc của tác nhân trên Amazon Connect, trên các nền tảng đối tác (như Salesforce), hoặc trong bảng điều khiển liên hệ khách hàng (Customer Contact Control Panel – CCP). NatWest đã quyết định điều chỉnh CCP hiện có của họ để tích hợp Amazon Q in Connect, cho phép họ nhanh chóng thử nghiệm và cải tiến trên giao diện máy tính mà các tác nhân đang sử dụng.

![/](/images/3-Blogs/Blog-2/Picture-1.png)


## Intent identification and mapping methodology
Phương pháp xác định và ánh xạ ý định (Intent)
Do có quá nhiều loại yêu cầu tiềm năng từ khách hàng, nên việc kiểm thử tất cả các tình huống trong giai đoạn thử nghiệm ban đầu là điều không khả thi. Vì vậy, cần có một cách tiếp cận chiến lược để xác định và ưu tiên các “ý định” của khách hàng.

NatWest đã áp dụng phương pháp tập trung như sau:
  - Sử dụng [Amazon Lex](https://aws.amazon.com/lex/) để phân tích và xác định 10 lý do phổ biến nhất khiến khách hàng gọi đến (ý định)
  - Sử dụng [Amazon Connect Contact Lens](https://aws.amazon.com/connect/contact-lens/) để xác định các bản ghi hội thoại tương ứng phục vụ cho kiểm thử
  - Chọn các ý định có tần suất cao làm trường hợp thử nghiệm chính
  - Ánh xạ có hệ thống các bài viết tri thức phù hợp với từng ý định đã xác định

Quy trình này gồm hai bước chính:
  - Phân tích dữ liệu cuộc gọi để xác định và ưu tiên các loại yêu cầu phổ biến nhất từ khách hàng
  - Ánh xạ chiến lược các bài viết tri thức phù hợp với từng ý định đã được ưu tiên

Cách tiếp cận có mục tiêu này giúp kiểm thử và tối ưu hóa hệ thống một cách hiệu quả, đồng thời tập trung vào các tình huống khách hàng có tác động lớn nhất.


## Tối ưu hóa bài viết tri thức
Các bài viết tri thức truyền thống thường được thiết kế dành riêng cho nhân viên tổng đài. Tuy nhiên, Amazon Q in Connect có cách tiếp cận toàn diện hơn bằng cách phân tích động lực hội thoại từ cả hai phía — theo dõi các cụm từ và từ khóa kích hoạt từ cả phía khách hàng và phản hồi của nhân viên — để tạo ra hỗ trợ theo ngữ cảnh, theo thời gian thực.

Để tối ưu hóa khả năng này, các bài viết tri thức cần được điều chỉnh để hoạt động hiệu quả với Amazon Q in Connect. Việc tuân thủ các thực hành tốt nhất về bài viết tri thức của Amazon Q giúp các tổ chức tái cấu trúc nội dung hiện có theo cách tối đa hóa khả năng của AI trong việc cung cấp hỗ trợ phù hợp, kịp thời trong các tương tác với khách hàng.

Việc chuyển đổi này đảm bảo nội dung được định dạng và cấu trúc đúng cách để tận dụng tối đa các công cụ hỗ trợ nhân viên dựa trên AI tạo sinh.

## Cân bằng giữa hỗ trợ AI và quy trình hướng dẫn từng bước
Mặc dù AI tạo sinh hỗ trợ nhân viên tổng đài rất mạnh mẽ, nhưng một số yêu cầu từ khách hàng lại đòi hỏi cách tiếp cận có cấu trúc hơn thông qua các quy trình hướng dẫn từng bước. [Các hướng dẫn này](https://docs.aws.amazon.com/connect/latest/adminguide/step-by-step-guided-experiences.html) đặc biệt hữu ích khi xử lý các tình huống phức tạp hoặc các quy trình bị ràng buộc bởi quy định, yêu cầu tuân thủ chính xác từng bước.

Do đó, điều quan trọng là phải đánh giá và xác định bài viết tri thức nào phù hợp để chuyển đổi thành hướng dẫn có cấu trúc, và bài viết nào nên được xử lý bằng phản hồi hỗ trợ từ AI. Giải pháp tối ưu là kết hợp cả hai cách tiếp cận:
  - AI hỗ trợ cho các yêu cầu đơn giản, linh hoạt
  - Hướng dẫn từng bước cho các quy trình phức tạp, nhạy cảm về tuân thủ

Amazon Q in Connect hỗ trợ hiệu quả mô hình kết hợp này bằng cách tích hợp liền mạch với các hướng dẫn từng bước trong Amazon Connect. Sự tích hợp này tạo ra một hệ thống hỗ trợ toàn diện, kết hợp sự linh hoạt của AI với độ chính xác của quy trình có cấu trúc, mang đến bộ công cụ tối ưu để nhân viên xử lý yêu cầu khách hàng một cách hiệu quả và chính xác.



## Đánh giá hiệu quả thử nghiệm PoC (Proof of Concept)
Mặc dù mục tiêu cuối cùng của việc triển khai hỗ trợ nhân viên là giảm thời gian xử lý cuộc gọi, tăng mức độ tuân thủ quy trình và cải thiện điểm NPS, nhưng việc đo lường các chỉ số này trong một thử nghiệm quy mô nhỏ lại gặp nhiều thách thức.
Để giải quyết vấn đề này, NatWest Group đã chọn cách đánh giá thủ công kết quả sau mỗi cuộc gọi. Tuy nhiên, thay vì tiếp tục đánh giá thủ công sau từng cuộc gọi, họ đã triển khai hệ thống báo cáo tự động.

Chiến lược báo cáo tự động này giúp NatWest:
  - Theo dõi các chỉ số hiệu suất một cách khách quan
  - Thu thập dữ liệu có giá trị trong giai đoạn thử nghiệm
  - Đánh giá tác động của giải pháp mà không làm tăng khối lượng công việc cho nhân 

![s](/images/3-Blogs/Blog-2/2025-03-31_11-03-26.png)

Bằng cách phát triển các khả năng báo cáo tùy chỉnh bên cạnh khả năng giám sát của Amazon Q trong Connect, NatWest đã tạo ra một phương pháp tiếp cận có hệ thống và dựa trên dữ liệu hơn để đo lường mức độ thành công của việc triển khai hỗ trợ tác nhân, ngay cả trong phạm vi hạn chế của giai đoạn thử nghiệm.

## Kiến trúc báo cáo khách hàng 

Báo cáo là yếu tố thiết yếu trong việc triển khai AI tạo sinh nhằm giám sát cả chất lượng và độ an toàn của các phản hồi do AI tạo ra, đảm bảo tính chính xác đồng thời phát hiện sớm các vấn đề tiềm ẩn. Không giống như phần mềm truyền thống với hành vi có thể dự đoán, các hệ thống AI tạo sinh đòi hỏi phải được giám sát liên tục để đảm bảo chúng mang lại giá trị trong các giới hạn chấp nhận được. Báo cáo toàn diện cung cấp các chỉ số quan trọng để chứng minh hiệu quả đầu tư (ROI), xác định cơ hội tối ưu hóa và theo dõi xu hướng sử dụng. Cuối cùng, báo cáo tốt giúp các tổ chức duy trì quyền kiểm soát trong khi tối đa hóa lợi ích từ khoản đầu tư vào AI.

![s](/images/3-Blogs/Blog-2/CustomReportingBlog.png)

Một số điểm chính cần lưu ý về kiến trúc này như sau:

  1. Giao diện người dùng tùy chỉnh (custom UX) trên trình duyệt của tác nhân gọi Amazon Q trong Connect API để lấy truy vấn của khách hàng và các đề xuất từ Amazon Q
  2. Giao diện người dùng tùy chỉnh gọi endpoint REST của API Gateway để gửi dữ liệu đã thu thập
  3. API Gateway gọi một hàm AWS Lambda và truyền dữ liệu vào
  4. Hàm AWS Lambda gọi dịch vụ Amazon Comprehend để loại bỏ thông tin nhận dạng cá nhân (PII) và các dữ liệu nhạy cảm, sau đó ghi dữ liệu đã được xử lý vào bảng Amazon DynamoDB
  5. Lambda báo cáo (Reporting Lambda) lấy dữ liệu từ bảng
  6. Lambda báo cáo gửi email kèm theo báo cáo đính kèm

## Triển khai Amazon Q in Connect thành công ở quy mô lớn
![s](/images/3-Blogs/Blog-2/2025-03-31_10-53-52-1.png)

Quy trình này phác thảo các bước chính và những yếu tố cần cân nhắc để mở rộng hiệu quả việc triển khai Amazon QiC nhằm hỗ trợ tác nhân và dịch vụ tự động.

## Kết luận 
Việc NatWest Group thử nghiệm Amazon Q in Connect trong môi trường sản xuất cho thấy các tổ chức tài chính có thể tận dụng hiệu quả AI tạo sinh để nâng cao hoạt động của trung tâm liên lạc. Thông qua cách tiếp cận có phương pháp trong thử nghiệm và triển khai, NatWest đã chứng minh rằng thành công phụ thuộc vào một số yếu tố then chốt: lựa chọn mục tiêu chiến lược, quản lý tri thức tối ưu và khả năng đo lường mạnh mẽ.

Kinh nghiệm của họ nhấn mạnh tầm quan trọng của:
  - Tiếp cận thử nghiệm có trọng tâm với các tác nhân giàu kinh nghiệm
  - Cấu trúc bài viết tri thức một cách phù hợp để AI có thể xử lý
  - Cân bằng giữa hỗ trợ AI và quy trình hướng dẫn cho các tình huống phức tạp
  - Triển khai phương pháp đo lường có hệ thống thông qua báo cáo

Khi các tổ chức tìm cách triển khai các giải pháp tương tự, hành trình của NatWest mang lại những góc nhìn giá trị về cách tiếp cận việc triển khai, thử nghiệm và mở rộng các công cụ hỗ trợ tác nhân dựa trên AI trong môi trường trung tâm liên lạc.

## Tác giả

{{< author-bio img="/images/3-Blogs/Blog-2/Prateek-copy.jpg" name="Prateek Guleria" >}}
 **Prateek Guleria** là Trưởng nhóm DevOps tại NatWest. Được giao nhiệm vụ thực hiện các quy trình tự động hóa, giám sát việc phát triển và triển khai các pipeline CI/CD, và duy trì hạ tầng điện toán đám mây trên nền tảng AWS.
{{< /author-bio >}}

{{< author-bio img="/images/3-Blogs/Blog-2/Georgina.jpeg" name="Georgina Williams" >}}
Đóng vai trò là Chuyên gia Chính về Trải nghiệm Khách hàng (CXE) tại London, **Georgina Williams** hỗ trợ các tổ chức toàn cầu lớn trong việc chuyển đổi chiến lược trải nghiệm khách hàng. Ngoài công việc, cô thích dành thời gian cùng hai cô con gái nhỏ để thực hiện các dự án thủ công.
{{< /author-bio >}}

{{< author-bio img="/images/3-Blogs/Blog-2/Prabha.png" name="Prateek Guleria" >}}
**Prabhakar Rajasekar** là Kiến trúc sư Giải pháp Chuyên biệt về Trải nghiệm Khách hàng (CXE) tại Amazon Web Services cho WWSO ở Aachen, Đức. Ngoài việc hỗ trợ khách hàng trong hành trình chuyển đổi số, bạn sẽ thấy anh ấy dành thời gian cùng các con trong vườn hoặc trong rừng.
{{< /author-bio >}}
{{< author-bio img="/images/3-Blogs/Blog-2/Abhay-copy.jpeg" name="Prateek Guleria" >}}
**Abhay Kumar** là Giám đốc Kỹ thuật tại NatWest. Anh chịu trách nhiệm về Kiến trúc, Phát triển, Bảo trì, Chất lượng và Bảo mật của Nền tảng Tổng đài Liên hệ Khách hàng.

{{< /author-bio >}}