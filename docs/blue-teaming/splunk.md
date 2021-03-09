# SPLUNK RESEARCH

## ĐÁNH GIÁ SPLUNK

[https://securitydaily.net/splunk-cong-cu-toan-nang-cho-cac-chuyen-gia-giam-sat-an-ninh-mang/](https://securitydaily.net/splunk-cong-cu-toan-nang-cho-cac-chuyen-gia-giam-sat-an-ninh-mang/)

LƯU Ý: Splunk mạnh về khả năng phân tích và cảnh báo tuy nhiên nó lại không mạnh và không đảm bảo về việc thu thập và truyền tải log. Cụ thể là nó chưa có cơ chế bảo mật trên đường truyền, không phù hợp với những hệ thống đòi hỏi bảo mật cao. Để phát huy hết được sức mạnh của Splunk cần có thời gian tìm hiểu và sử dụng. Splunk chưa có cơ chế giúp tự động phát hiện ra các tấn công hay các vấn đề từ bên ngoài. Những điều này phụ thuộc vào kinh nghiệm sử dụng và vốn hiểu biết về bảo mật của người quản trị.

Tuy nhiên Splunk làm không tốt việc tập trung Log từ các Server hay thiết bị khác. Vì thế chúng ta cần sử dụng một số công cụ khác để thực hiện việc tập trung Log và về Splunk Server. Cụ thể là ta có thể kết hợp với syslog, Snare (for Windows), sử dụng qua Heroku ….

Splunk có thể cấu hình dễ dàng bằng giao diện web tại địa chỉ [http://localhost:8000/](http://localhost:8000/).

[https://blog.botbie.io/2016/09/04/splunk-vs-elastic-stack-ban-chon-bo-cong-cu-nao-de-quan-ly-logs](https://blog.botbie.io/2016/09/04/splunk-vs-elastic-stack-ban-chon-bo-cong-cu-nao-de-quan-ly-logs)

Đánh giá khách quan mà nói ELK Stack định hướng tương lai về kiến trúc và nền tảng ổn hơn rất nhiều Splunk.

Để tổng quan theo mình ae nào nghiên cứu chuyên sâu có thể tham vấn một số thông tin sau:

1) Giải pháp Splunk và ELK kiến trúc logic hoạt động như thế nào

2) Giống và khác nhau giữ Splunk và ELK (cấu phần "web, app, db", cách hoạt động của chúng ra sao.

3) Tính mở rộng và customize của từng sản phẩm

## CÀI ĐẶT SPLUNK ENTERPRISE

Download Splunk tại trang [https://www.splunk.com](https://www.splunk.com/).

Cài đặt Splunk trên Ubuntu:

- Download file cài đặt cho Linux.
- Tại thư mục chứa file cài đặt, chạy lệnh `dpkg –i <tên file cài đặt>`. Splunk sẽ được cài đặt vào thư mục mặc định là /opt/splunk.
- Chạy lệnh `/opt/splunk/bin/splunk –accept-license` để chấp nhận giấy phép tự động.
- Splunk đã có thể được khởi động bằng lệnh `/opt/splunk/bin/splunk start`.