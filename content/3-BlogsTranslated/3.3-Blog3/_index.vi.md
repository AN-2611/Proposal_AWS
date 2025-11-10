---
title: "Blog 3"
date: "2025-09-08"
weight: 1
chapter: false
pre: " <b> 3.3. </b> "
---

# Tích hợp trợ lý lập trình sử dụng AI trong môi trường bảo mật bằng Continue và Amazon Bedrock
<span class="meta-info">Tác giả: Keith Boaman và Andrew Istfan | ngày 01 tháng 05, 2025 | in </span> [Amazon API Gateway](https://aws.amazon.com/blogs/publicsector/category/application-services/amazon-api-gateway-application-services/), [Amazon Bedrock](https://aws.amazon.com/blogs/publicsector/category/artificial-intelligence/amazon-machine-learning/amazon-bedrock/), [Amazon Q](https://aws.amazon.com/blogs/publicsector/category/amazon-q/), [Amazon Q Developer](https://aws.amazon.com/blogs/publicsector/category/amazon-q/amazon-q-developer/), [Artificial Intelligence](https://aws.amazon.com/blogs/publicsector/category/artificial-intelligence/), [AWS Cloud Development Kit](https://aws.amazon.com/blogs/publicsector/category/developer-tools/aws-cloud-development-kit/), [AWS GovCloud (US)](https://aws.amazon.com/blogs/publicsector/category/public-sector/government/aws-govcloud-us/), [AWS Identity and Access Management (IAM)](https://aws.amazon.com/blogs/publicsector/category/security-identity-compliance/aws-identity-and-access-management-iam/), [AWS PrivateLink](https://aws.amazon.com/blogs/publicsector/category/networking-content-delivery/aws-privatelink/), [AWS Security Hub](https://aws.amazon.com/blogs/publicsector/category/security-identity-compliance/aws-security-hub/), [Developer Tools](https://aws.amazon.com/blogs/publicsector/category/developer-tools/), [Foundation models](https://aws.amazon.com/blogs/publicsector/category/artificial-intelligence/generative-ai/foundation-models/), [Government](https://aws.amazon.com/blogs/publicsector/category/public-sector/government/), [Public Sector](https://aws.amazon.com/blogs/publicsector/category/public-sector/), [Security, Identity, & Compliance](https://aws.amazon.com/blogs/publicsector/category/security-identity-compliance/), [Technical How-to](https://aws.amazon.com/blogs/publicsector/category/post-types/technical-how-to/) | [Permalink](https://aws.amazon.com/blogs/publicsector/integrate-ai-powered-coding-assistance-in-secure-environments-using-continue-and-amazon-bedrock/) 

![w](/images/3-Blogs/Blog-3/2..png)

Các tổ chức áp dụng các hoạt động phát triển phần mềm hiện đại tiếp tục tận dụng lợi thế của AI và các [mô hình ngôn ngữ lớn (LLMs)](https://aws.amazon.com/what-is/large-language-model/), tối đa hóa năng suất của các nhà phát triển. [Amazon Q Developer](https://aws.amazon.com/q/developer/) cung cấp cho bạn một trợ lý lập trình AI, cho phép các nhà phát triển truy cập trực tiếp vào trợ lý AI ngay trong môi trường phát triển tích hợp [(IDE)](https://aws.amazon.com/what-is/ide/).

Việc truyền ngữ cảnh của mã liên quan từ IDE sang công cụ AI trong quá trình phát triển phần mềm mang lại lợi ích lớn về năng suất. Tuy nhiên, điều này cũng mở ra nguy cơ rò rỉ dữ liệu hoặc tiết lộ thông tin độc quyền nếu không có các biện pháp phòng ngừa thích hợp. Các tổ chức triển khai trong môi trường có quy định nghiêm ngặt, thường là trong các [Regions](https://docs.aws.amazon.com/glossary/latest/reference/glos-chap.html#region) của [Amazon Web Services (AWS)](https://aws.amazon.com/) GovCloud (US) [Regions](https://docs.aws.amazon.com/glossary/latest/reference/glos-chap.html#region), are looking for a way for their developers to securely use approved models outside Amazon Q that have appropriate guardrails and have the potential for customization.

Trong bài viết này, chúng tôi sẽ hướng dẫn bạn một ví dụ có thể sử dụng, tận dụng sức mạnh của [Amazon Bedrock](https://aws.amazon.com/bedrock/) để cung cấp trợ lý lập trình trong IDE của bạn.

## Tổng quan kiến trúc 
Tại thời điểm bài viết này được xuất bản, Amazon Q vẫn chưa khả dụng trong các vùng AWS GovCloud (US). Tuy nhiên, các tổ chức có thể triển khai một giải pháp thay thế mạnh mẽ bằng cách kết hợp trợ lý mã nguồn mở [Continue](https://www.continue.dev/) wivới khả năng suy luận không máy chủ của Amazon Bedrock, cả hai đều được hỗ trợ đầy đủ trong các vùng AWS GovCloud (US). Kiến trúc này sử dụng khung mở rộng của Continue để giao tiếp với Amazon Bedrock nhằm tạo ra một trợ lý lập trình AI bảo mật và tuân thủ trực tiếp trong IDE của bạn. Mặc dù không được thảo luận hoặc đánh giá trong ví dụ này, các công cụ lập trình AI thay thế như Cline hoặc Aider cũng có thể được lựa chọn.

Ví dụ này mang lại một số lợi ích chính:

  - Chủ quyền dữ liệu hoàn toàn trong các vùng AWS GovCloud (US)
  - Tùy chỉnh kỹ thuật nhắc lệnh và lựa chọn mô hình
  - Tích hợp với quy trình làm việc IDE hiện có
  - Khả năng triển khai các biện pháp kiểm soát bảo mật bổ sung và ghi nhật ký kiểm toán
  - Hỗ trợ môi trường cách ly thông qua các điểm cuối API riêng

Bằng cách kết hợp các thành phần này, các tổ chức có thể cung cấp cho nhóm phát triển của họ khả năng lập trình hỗ trợ AI trong khi vẫn duy trì các yêu cầu nghiêm ngặt về bảo mật và tuân thủ của môi trường vùng AWS GovCloud (US).

Xác thực được thực hiện thông qua tệp cấu hình AWS tiêu chuẩn trên máy chủ của bạn. Ví dụ này sử dụng
 [AWS Identity and Access Management (IAM) Roles Anywhere](https://aws.amazon.com/iam/roles-anywhere/)  để cung cấp quản lý thông tin xác thực tự động và bảo mật. Bằng cách sử dụng chứng chỉ X.509 và cơ quan chứng thực riêng (CA), các nhà phát triển có thể nhận được thông tin xác thực AWS tạm thời mà không cần can thiệp thủ công.

Trong cấu hình sau, chúng tôi trình bày Visual Studio Code (VS Code) được cài đặt trên máy trạm cục bộ. Ngoài ra, IDE có thể được cài đặt trên môi trường ảo bên trong AWS, chẳng hạn như[Amazon AppStream 2.0](https://aws.amazon.com/appstream2/) hoặc [Amazon Workspaces](https://aws.amazon.com/workspaces/)  để có một môi trường được cấu hình sẵn và có khả năng mở rộng cho các nhà phát triển hoặc quản trị viên hệ thống.


![Figure 1. High-level example architecture](/images/3-Blogs/Blog-3/1-10.png)
Figure 1. High-level example architecture

## Yêu cầu trước khi triển khai
Để triển khai ví dụ này, bạn cần có quyền truy cập vào [Amazon Bedrock foundation models (FMs)](https://aws.amazon.com/what-is/foundation-models/), quyền này không được cấp mặc định. Bạn chỉ có thể yêu cầu hoặc chỉnh sửa quyền truy cập thông qua  [Amazon Bedrock console](https://console.aws.amazon.com/bedrock/). 

Thực hiện theo các bước sau:
  1. Đăng nhập vào tài khoản AWS mục tiêu với vai trò IAM có đủ [quyền để quản lý quyền](https://docs.aws.amazon.com/bedrock/latest/userguide/model-access-permissions.html) truy cập vào các mô hình nền tảng.
  2. Làm theo hướng dẫn tại mục [Thêm hoặc xóa quyền truy cập vào các mô hình nền tảng của Amazon Bedrock](https://docs.aws.amazon.com/bedrock/latest/userguide/model-access-modify.html).
  3. Đối với bài viết này, hãy bật quyền truy cập vào Claude 3.0 Haiku của Anthropic và [Amazon Titan Text Express](https://aws.amazon.com/bedrock/amazon-models/titan/).

## Hướng dẫn triển khai 
Để triển khai ví dụ, hãy sử dụng các hướng dẫn trong các phần sau.
### Triển khai IAM Roles Anywhere 
Bạn có thể sử dụng mã  Amazon Cloud Development Kit (AWS CDK)  viết bằng Typescript trên GitHub để triển khai các cấu hình cho AWS Private Certificate Authority, AWS Certificate Manager (ACM), IAM và IAM Roles Anywhere. Mã được cung cấp là một khung ban đầu có thể được điều chỉnh khi cần thiết. Tiếp theo, chúng tôi sẽ xem xét một số phần của mã.

Trong ví dụ này, AWS Private CA cho phép tạo ra các Cơ quan Chứng thực (CA) gốc và cấp dưới mà không cần đầu tư và chi phí bảo trì khi vận hành CA tại chỗ. Cấu hình chứng chỉ gốc trong Private CA có thể được thiết lập theo các thông số cụ thể của tổ chức bạn.


![s](/images/3-Blogs/Blog-3/1.png)

Từ chứng chỉ gốc trong AWS Private CA, AWS CDK sẽ tạo một chứng chỉ máy khách ví dụ có thể được cài đặt trên thiết bị máy khách. Chứng chỉ máy khách này sẽ được truyền qua công cụ hỗ trợ thông tin xác thực IAM Roles Anywhere để cho phép máy khách đảm nhận vai trò đã được cấu hình như một phần của IAM Roles Anywhere.

![j](/images/3-Blogs/Blog-3/3.png)

Dưới đây là hướng dẫn để điều chỉnh và triển khai mã ví dụ:
  1. Sao chép hoặc tải xuống kho mã về máy cục bộ.
  2. Điều hướng đến thư mục VSCodeBedrock.
![p](/images/3-Blogs/Blog-3/2-11.png)
  3. Điều chỉnh các thiết lập trong tệp lib/vs_code_ai-stack.ts: 
    
     * **Region:**
       * Đặt thành ‘us-gov-west-1’ làm ví dụ nhưng có thể thay đổi sang vùng mục tiêu mong muốn.n.

     * **Root Certificate:**
       * templateARN: Thay đổi phân vùng nếu triển khai ngoài GovCloud
       * validity value: Điều chỉnh theo yêu cầu về thời hạn chứng chỉ
     * **Client Certificate:**
       * domainName: Thay thế ‘your-domain.com’ bằng tên miền mong muốn
       * subjectAlternativeNames: thêm bất kỳ tên thay thế nào nếu cần
       * keyAlgorithm: Thiết lập tùy chọn, mặc định là RSA_2048
     * **Trust Policy cho IAM Roles Anywhere**
       * String Condition: được đặt thành giá trị chuỗi cho phân vùng aws-us-gov, thay đổi nếu triển khai ở phân vùng khác
     * **Profile cho IAM Roles Anywhere:**
       * durationSeconds: thời gian trước khi phiên xác thực hết hạn. Điều chỉnh theo yêu cầu.
     * **Triển khai CDK bằng lệnh ‘cdk deploy’ **

Chứng chỉ riêng được tạo và khóa riêng liên quan có thể được xuất sang kho chứng chỉ của thiết bị máy khách mà bạn muốn thiết lập kết nối đến Amazon Bedrock. Trong ví dụ này, chúng tôi sử dụng [OpenSSL](https://www.openssl.org/) một thư viện phần mềm mã nguồn mở dành cho giao tiếp Secure Sockets Layer (SSL). Thực hiện theo các bước sau
  1. Trên bảng [ACM console](https://console.aws.amazon.com/certificate-manager/), chọn chứng chỉ riêng để sử dụng trên máy trạm cục bộ.
the private certificate to use on the local workstation.
  2. Đặt mật mã mã hóa riêng và tạo mã hóa Privacy Enhanced Mail (PEM).
  3. Tải xuống phần thân chứng chỉ đã xuất, chuỗi chứng chỉ và khóa riêng.
  4. Giải mã khóa riêng bằng OpenSSL tại máy cục bộ. [[OpenSSL Compilation and Installation](https://wiki.openssl.org/index.php/Compilation_and_Installation)]

<span class="highlight-code">
openssl ec --passin pass:<encryptionpassphrase> -in private_key.pem -out private_key_decrypt.pem
</span>

Chúng tôi sẽ cho phép người dùng cuối đảm nhận một vai trò IAM thông qua IAM Roles Anywhere và giới hạn quyền của phiên làm việc chỉ để gọi các API cần thiết cho trường hợp sử dụng cụ thể này. Phần dưới đây của mã CDK thiết lập vai trò và cho phép vai trò được đảm nhận bởi IAM Roles Anywhere:

![i](/images/3-Blogs/Blog-3/4.png)

### Thiết lập Continue 
Để thiết lập Continue, hãy thực hiện các bước sau:

  1. Tải plugin Continue cho VS Code hoặc JetBrains từ trang chủ của Continue.
  2. Sau khi cài đặt plugin Continue, mở tệp cấu hình tại <span class="highlight-code">~/.configure/config.json</span>. Tệp cấu hình cũng có thể được truy cập bằng cách mở plugin Continue, chọn biểu tượng cài đặt, và chọn “Open configuration file” ở đầu màn hình, như minh họa trong ảnh chụp màn hình sau.
![s](/images/3-Blogs/Blog-3/3-10-566x1024.png)
  3. Trong tệp cấu hình, hãy chỉnh sửa đối tượng “models” để chứa các mô hình Amazon Bedrock phù hợp mà bạn muốn sử dụng. Để biết thêm thông tin về cách cấu hình Amazon Bedrock làm nhà cung cấp mô hình cho plugin, hãy tham khảo mục Amazon Bedrock trong phần Model providers ở thanh điều hướng bên trái của [Continue documentation](https://docs.continue.dev/customize/model-providers/bedrock).

![w](/images/3-Blogs/Blog-3/5.png)

### Bật quyền truy cập AWS 
Để bật quyền truy cập AWS, hãy thực hiện các bước sau:

  1. Cài đặt công cụ hỗ trợ thông tin xác thực AWS IAM Roles Anywhere từ mục Get temporary security credentials from IAM Roles Anywhere. Công cụ hỗ trợ này có sẵn cho Windows, macOS và Linux. Các mã kiểm tra SHA26 được cung cấp để xác minh tính toàn vẹn của tệp tải xuống
  2. Tạo một hồ sơ cấu hình trong ~/.aws/credentials sử dụng công cụ ký vừa cài đặt theo định dạng sau. Continue sẽ thực hiện xác thực với AWS bằng thông tin xác thực nằm trong tệp này. Vì ví dụ sử dụng IAM Roles Anywhere, công cụ hỗ trợ thông tin xác thực này sẽ tự động trả về thông tin xác thực đã xoay vòng mỗi khi cần xác thực, giúp bạn tránh được việc phải sửa đổi tệp thông tin xác thực mỗi khi token hết hạn.

![p](/images/3-Blogs/Blog-3/6.png)
  3. Xác minh kết nối thành công bằng cách chọn mô hình bạn muốn sử dụng và gửi câu hỏi đầu tiên thông qua Continue.

### Thích ứng với môi trường của bạn 
Mặc dù ví dụ hiện tại cung cấp nền tảng vững chắc cho hỗ trợ lập trình AI bảo mật, khách hàng có thể mong muốn các biện pháp bảo mật mạng bổ sung để tăng cường bảo vệ trong các môi trường có quy định nghiêm ngặt như AWS GovCloud (US):

  1. [AWS PrivateLink](https://aws.amazon.com/privatelink/) có thể được sử dụng để tạo kết nối mạng riêng, được mã hóa giữa đám mây riêng ảo (VPC) của bạn và Amazon Bedrock. Theo tài liệu [Securely Access Services Over AWS PrivateLink](https://docs.aws.amazon.com/whitepapers/latest/aws-privatelink/aws-privatelink.html) cách tiếp cận này mang lại các lợi ích sau:
     * Loại bỏ truy cập internet trực tiếp đến các dịch vụ AI
     * Giảm bề mặt tấn công tiềm ẩn
     * Cung cấp thêm một lớp cách ly mạng
  2. [Amazon API Gateway](https://aws.amazon.com/api-gateway/)có thể được sử dụng để triển khai các tính năng bảo mật nâng cao sau:
     * Request [throttling](https://docs.aws.amazon.com/apigateway/latest/developerguide/api-gateway-request-throttling.html) để ngăn chặn lạm dụng dịch vụ
     * Kiểm soát và quản lý quyền truy cập
     * Tích hợp với AWS WAF
  3. Tận dụng các kiểm soát từ AWS Security Hub controls liên quan đến các dịch vụ đã triển khai

Những điều chỉnh này có thể giúp các tổ chức đáp ứng các yêu cầu bảo mật nghiêm ngặt, bao gồm các tiêu chuẩn của [National Institute of Standards and Technology (NIST)](https://aws.amazon.com/compliance/nist/), [Federal Risk and Authorization Management Program (FedRAMP)](https://aws.amazon.com/compliance/fedramp/), và Bộ Quốc phòng Hoa Kỳ (DoD) bằng cách cung cấp:

  * Kiểm soát truy cập theo nguyên tắc tối thiểu
  * Ghi nhật ký và giám sát toàn diện
  * Giao tiếp dịch vụ được mã hóa

Bằng cách áp dụng các cải tiến bảo mật mạng được đề xuất này, bạn có thể phát triển một phương pháp tiếp cận mạnh mẽ và an toàn hơn cho lập trình hỗ trợ AI trong các môi trường có quy định nghiêm ngặt.

## Kết luận 
Ví dụ này minh họa một cách tiếp cận thực tiễn để tích hợp hỗ trợ lập trình sử dụng AI trong các môi trường bảo mật cao như AWS GovCloud (US). Bằng cách kết hợp Continue, Amazon Bedrock và IAM Roles Anywhere, bạn có thể xây dựng một khung làm việc cân bằng giữa năng suất tiên tiến và các yêu cầu bảo mật nghiêm ngặt.

Kiến trúc này cung cấp cho các tổ chức một lộ trình để sử dụng công nghệ AI một cách an toàn, giúp các nhà phát triển nâng cao năng suất trong khi vẫn duy trì chủ quyền dữ liệu toàn diện và tuân thủ quy định. Khi AI tiếp tục thay đổi cách phát triển phần mềm, những kiến trúc như thế này sẽ đóng vai trò quan trọng trong việc kết nối giữa đổi mới và bảo mật.


Để tìm hiểu thêm, hãy truy cập[AWS in the Public Sector](https://aws.amazon.com/government-education/). Để được hướng dẫn thêm, hãy kết nối với kiến trúc sư giải pháp AWS của bạn hoặc liên hệ với chúng tôi ngay hôm nay!

TAGS: [Amazon API Gateway](https://aws.amazon.com/blogs/publicsector/tag/amazon-api-gateway/), [Artificial Intelligence](https://aws.amazon.com/blogs/publicsector/tag/artificial-intelligence/), [AWS GovCloud (US)](https://aws.amazon.com/blogs/publicsector/tag/aws-govcloud-us/), [AWS GovCloud (US) Region](https://aws.amazon.com/blogs/publicsector/tag/aws-govcloud-us-region/), [AWS IAM](https://aws.amazon.com/blogs/publicsector/tag/aws-iam/), [AWS PrivateLink](https://aws.amazon.com/blogs/publicsector/tag/aws-privatelink/), [AWS Public Sector](https://aws.amazon.com/blogs/publicsector/tag/aws-public-sector/), [government](https://aws.amazon.com/blogs/publicsector/tag/government/), [security](https://aws.amazon.com/blogs/publicsector/tag/security/), [technical how-to](https://aws.amazon.com/blogs/publicsector/tag/technical-how-to/)

![p](/images/3-Blogs/Blog-3/7.png)
<span class="highlight-code">

</span>