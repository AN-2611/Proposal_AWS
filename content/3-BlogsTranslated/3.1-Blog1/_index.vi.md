---
title: "Blog 1"
date: "2025-09-08"
weight: 1
chapter: false
pre: " <b> 3.1. </b> "
---


# Lập trình thông minh trong tầm tay bạn: Giới thiệu trải nghiệm lập trình chủ động trong môi trường phát triển tích hợp (IDE)


Tác giả: Brian Beach | ngày 05 tháng 05, 2025 | trong [Amazon Q](https://aws.amazon.com/blogs/devops/category/amazon-q/), [Amazon Q Developer](https://aws.amazon.com/blogs/devops/category/amazon-q/amazon-q-developer/), [Announcements](https://aws.amazon.com/blogs/devops/category/post-types/announcements/) | [Permalink](https://aws.amazon.com/blogs/devops/amazon-q-developer-agentic-coding-experience/) | 

Vào tháng Ba vừa qua, tôi đã viết về [trải nghiệm lập trình chủ động (agentic coding) mới trong Amazon Q Developer CLI](https://aws.amazon.com/blogs/devops/introducing-the-enhanced-command-line-interface-in-amazon-q-developer/). Gần đây, [Amazon Q Developer](https://aws.amazon.com/q/developer/) đã công bố rằng [họ đã tích hợp trải nghiệm tương tự vào môi trường phát triển tích hợp (IDE)](https://aws.amazon.com/about-aws/whats-new/2025/05/amazon-q-developer-agentic-coding-experience-ide/). Lập trình chủ động trong IDE cho phép bạn làm việc với Amazon Q Developer để đọc và ghi tệp cục bộ, chạy các lệnh bash, xây dựng mã và nhiều hơn nữa gần như theo thời gian thực thông qua các cuộc hội thoại bằng ngôn ngữ tự nhiên. Trải nghiệm mới này tái định nghĩa cách bạn viết, chỉnh sửa và duy trì mã bằng cách tận dụng khả năng hiểu ngôn ngữ tự nhiên để thực thi liền mạch các quy trình phức tạp. Trải nghiệm lập trình chủ động mới hiện đã có mặt trên VS Code và sẽ sớm hỗ trợ các IDE khác.


## Bối cảnh 
Trước khi tôi giải thích về trải nghiệm lập trình chủ động mới, hãy dành một chút thời gian để xem lại các khả năng trò chuyện hiện có trong Amazon Q Developer IDE. Đúng như tên gọi, trò chuyện truyền thống cho phép tôi trò chuyện với Q Developer. Đây là một lựa chọn tuyệt vời khi tôi đang học hỏi và lên kế hoạch. Nó cung cấp một cuộc đối thoại tự nhiên qua lại. Cá nhân tôi thích sử dụng trò chuyện truyền thống trong giai đoạn lập kế hoạch của vòng đời phát triển phần mềm (SDLC). Tôi có thể trò chuyện với Q Developer để thảo luận về kiến trúc và các đánh đổi giữa các thiết kế khác nhau trước khi bắt đầu làm việc.
Tuy nhiên, khi tôi chuyển sang giai đoạn xây dựng của SDLC, tôi lại thích trải nghiệm lập trình chủ động mới. Trong trải nghiệm này, Q Developer có thể làm được nhiều hơn là chỉ trò chuyện. Nó có thể tương tác trực tiếp với môi trường phát triển, đọc và ghi tệp, sử dụng các công cụ phát triển khác nhau, và thậm chí truy vấn tài nguyên AWS. Điều này cho phép quy trình lập trình trở nên năng động và thực tế hơn nhiều so với giao diện trò chuyện truyền thống.
Thay vì chỉ thảo luận về yêu cầu, tác nhân chủ động có thể thực hiện hành động trực tiếp để triển khai chúng. Nó có thể tạo khung cho các dự án mới, cập nhật mã hiện có, và cung cấp bản tóm tắt từng bước về tiến trình của nó – tất cả đều thông qua giao diện hội thoại liền mạch ngay trong IDE. Tin vui là giờ đây tôi có cả hai lựa chọn. Tôi có thể dễ dàng chuyển đổi giữa trò chuyện truyền thống trong giai đoạn lập kế hoạch và lập trình chủ động trong giai đoạn xây dựng.
## Hướng dẫn từng bước 
Hãy cùng đi qua một ví dụ đơn giản sử dụng [AWS Cloud Development Kit (CDK)](https://aws.amazon.com/cdk/). Tôi rất thích CDK và sử dụng nó thường xuyên trong công việc của mình. Tuy nhiên, hãy giả sử rằng tôi chưa có nhiều kinh nghiệm và muốn tìm hiểu thêm về CDK trước khi bắt đầu sử dụng. Vì tôi chỉ muốn học hỏi, tôi sẽ bắt đầu với trải nghiệm trò chuyện truyền thống và hỏi Q Developer: “Làm thế nào để tạo một ứng dụng CDK mới?” Như bạn có thể thấy trong hình ảnh dưới đây, Q Developer bắt đầu hướng dẫn tôi về CDK. Bên cạnh các hướng dẫn, Q còn cung cấp các lệnh mà tôi có thể sao chép và dán vào shell để bắt đầu.
![.](/images/3-Blogs/Blog-1/ide-agentic-coding-01.png)

Mặc dù điều này rất hữu ích, nhưng tôi đã quen thuộc với CDK. Tôi không cần học cách tạo một ứng dụng mới nữa. Tôi đã sẵn sàng để bắt đầu xây dựng! Vì vậy, tôi sẽ chuyển từ chế độ trò chuyện truyền thống sang chế độ lập trình chủ động bằng cách nhấp vào cặp dấu ngoặc nhọn ở góc dưới bên trái của cửa sổ trò chuyện. Sau đó, tôi sẽ yêu cầu Q Developer: “Tạo một ứng dụng CDK mới trong thư mục này bằng TypeScript.” Trước tiên, hãy chú ý rằng lần này tôi không đặt câu hỏi như trước, mà tôi đang đưa ra một lệnh. Trong hình ảnh sau, bạn có thể thấy rằng Q Developer đang thực hiện theo lệnh của tôi thay vì hướng dẫn tôi phải làm gì.

![.](/images/3-Blogs/Blog-1/ide-agentic-coding-02.png)

Đây chính là sức mạnh của trải nghiệm lập trình chủ động mới. Nó không chỉ đơn thuần là hướng dẫn tôi cách tạo một ứng dụng CDK — mà Amazon Q Developer đang trực tiếp tạo ứng dụng đó cho tôi. Có một vài điểm quan trọng mà tôi muốn nhấn mạnh ở đây. Thứ nhất, Amazon Q Developer có thể sử dụng các công cụ khi đang chạy ở chế độ lập trình chủ động. Trong ví dụ này, Q đang sử dụng một loạt các lệnh shell — như <span class="highlight-code"> mkdir, cd, npx, npm, etc.</span> — để tạo ứng dụng CDK. Tôi sẽ thảo luận thêm về các công cụ khác trong phần sau của bài viết. Thứ hai, Q Developer sẽ hỏi ý kiến tôi trước khi thực thi các lệnh này. Điều này giúp tôi giữ quyền kiểm soát đối với quy trình phát triển. Tôi sẽ nhấp vào nút “Run” và cho phép Q tạo ứng dụng mới, kết quả là cấu trúc dự án như sau. 

![.](/images/3-Blogs/Blog-1/ide-agentic-coding-03.png)

Thật dễ để bỏ qua sức mạnh của việc cho phép Q Developer sử dụng các công cụ. Bằng cách sử dụng các lệnh shell, nó có thể tạo ra dự án bằng mẫu mới nhất và cài đặt các gói phụ thuộc cho tôi. Việc chạy các lệnh shell chỉ là một trong nhiều thay đổi trong trải nghiệm lập trình chủ động. Tiếp theo, hãy cùng xem cách tạo mã hoạt động trong chế độ lập trình chủ động.
## Tạo mã nguồn 
Amazon Q Developer đã có khả năng tạo mã kể từ khi [ra mắt vào tháng 6 năm 2022](https://aws.amazon.com/about-aws/whats-new/2022/06/aws-announces-amazon-codewhisperer-preview/). Kể từ đó, Q Developer đã không ngừng phát triển, bổ sung nhiều tính năng mới theo thời gian. Việc tạo mã bắt đầu với các [gợi ý nội tuyến](https://docs.aws.amazon.com/amazonq/latest/qdeveloper-ug/inline-suggestions.html), sau đó là [trò chuyện](https://docs.aws.amazon.com/amazonq/latest/qdeveloper-ug/q-in-IDE-chat.html), và tiếp theo là [trợ lý hỗ trợ phát triển phần mềm](https://aws.amazon.com/blogs/devops/amazon-q-developers-new-context-features/). Trải nghiệm lập trình chủ động mới một lần nữa tái định nghĩa cách tạo mã. Trong ví dụ sau, tôi sẽ thêm một hàm Lambda vào CDK stack mà Q Developer đã tạo trước đó. Tôi yêu cầu Q Developer: “Thêm một hàm Lambda mới được kích hoạt khi có tệp được tải lên một bucket S3 hiện có.”

![.](/images/3-Blogs/Blog-1/ide-agentic-coding-04.png)

Có nhiều điểm quan trọng đã xảy ra trong ví dụ này mà tôi muốn giải thích. Thứ nhất, hãy chú ý rằng Q Developer đã chỉnh sửa CDK Stack để thêm hàm AWS Lambda mới. Thứ hai, Q Developer đã sử dụng một lệnh shell để tạo một thư mục mới. Thứ ba, Q đã tạo một tệp mới cho hàm AWS Lambda. Thứ tư, nó đã cập nhật tệp README. Q đã thực hiện cả bốn hành động này chỉ từ một lời nhắc duy nhất. Ngoài ra, hãy lưu ý rằng Q Developer cung cấp phần so sánh thay đổi (diff) cho từng chỉnh sửa, giúp tôi dễ dàng xem lại các thay đổi. Bạn có thể thấy một ví dụ về các thay đổi trong tệp README.md ở hình ảnh sau. Cuối cùng, hãy lưu ý rằng tôi có thể hoàn tác bất kỳ thay đổi nào mà Q Developer đã thực hiện trong quá trình này.

![.](/images/3-Blogs/Blog-1/ide-agentic-coding-05.png)

## Mô tả tài nguyên AWS 
Hãy nhớ rằng tôi đang xây dựng một ứng dụng được kích hoạt khi có tệp mới được tải lên một bucket [Amazon Simple Storage Service (Amazon S3)](https://aws.amazon.com/s3/) hiện có. Trong ví dụ trước, bạn có thể thấy rằng tôi cần truyền tên của bucket vào tham số <span class="highlight-code">ExistingBucketName</span> khi triển khai stack.
Giả sử tôi đã quên tên của bucket mà mình muốn sử dụng. Trải nghiệm lập trình chủ động mới cũng có thể giúp tôi trong trường hợp này. Trong ví dụ sau, tôi yêu cầu Q: “Liệt kê các bucket S3 của tôi trong vùng ca-central-1?” Một lần nữa, Q Developer yêu cầu quyền sử dụng shell. Sau khi tôi chấp thuận, Q Developer sử dụng AWS CLI và liệt kê các bucket mà tôi có sẵn ở Canada (ca-central-1).

![.](/images/3-Blogs/Blog-1/ide-agentic-coding-06.png)

Với tên của bucket đã có, tôi đã sẵn sàng triển khai stack của mình. Tất nhiên, vẫn còn nhiều việc phải làm, nhưng tôi sẽ để dành cho một bài viết khác.
## Kết luận 
Trải nghiệm lập trình chủ động mới trong Amazon Q Developer IDE đánh dấu một bước tiến quan trọng trong việc tích hợp các khả năng mạnh mẽ do AI điều khiển trực tiếp vào quy trình làm việc của lập trình viên. Bằng cách cho phép tác nhân lập trình đọc, ghi và thực thi mã cục bộ, truy cập các công cụ và tương tác với tài nguyên AWS, Q Developer hứa hẹn sẽ đơn giản hóa và nâng cao đáng kể quá trình lập trình. Bạn có thể truy cập [Hướng dẫn sử dụng Amazon Q Developer](https://docs.aws.amazon.com/amazonq/latest/qdeveloper-ug/getting-started-q-dev.html) để cài đặt IDE và bắt đầu sử dụng tính năng trò chuyện tác nhân mới hoàn toàn miễn phí. Hãy thử ngay và chia sẻ cảm nhận của bạn nhé


