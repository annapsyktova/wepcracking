# WEP Cracking
## WEP là gì :
- là một giao thức bảo mật trong kết nối wifi. Wep mã hóa bằng key, sử dụng một đoạn IV 24 bit và mã hóa bằng phương thức RC4.
- WEP có thể bị phá vì nhiều lí do bảo mật khác nhau :
  - WEP sử dụng IV 24 bit, khá là nhỏ khi so sánh với số lượng gói tin được truyền, khi đến một thời điểm nhất định thì IV sẽ bị trùng 
  - RC4 là một phương thức mã hóa khá yếu, dễ bị bẻ khóa
  - Checksum của gói tin không được mã hóa đúng cách, dẫn đến có thể tạo gói tin giả mạo (fake authentication) 
## Workflow khi crack WEP
