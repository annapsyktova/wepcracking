# WEP Cracking
## WEP là gì :
- là một giao thức bảo mật trong kết nối wifi. Wep mã hóa bằng key, sử dụng một đoạn IV 24 bit và mã hóa bằng phương thức RC4.
- WEP có thể bị phá vì nhiều lí do bảo mật khác nhau :
  - WEP sử dụng IV 24 bit, khá là nhỏ khi so sánh với số lượng gói tin được truyền, khi đến một thời điểm nhất định thì IV sẽ bị trùng 
  - RC4 là một phương thức mã hóa khá yếu, dễ bị bẻ khóa
  - Checksum của gói tin không được mã hóa đúng cách, dẫn đến có thể tạo gói tin giả mạo (fake authentication) 
## Workflow khi crack WEP
- Bước 1 : sử dụng một tool để bắt hoặc sniffing các gói tin 
- Bước 2 : làm tăng traffic của mạng, có thể là dùng device connect vào để gửi request, hoặc lợi dụng client có sẵn để fake authen và tấn công arp(mục tiêu vẫn là làm tăng traffic)
- Bước 3 : sử dụng tool để crack wep trên tập tin traffic thu được ( số gói tin thu được phải đủ lớn, khoảng 50k packet đối với wep 64 bit) 
## Các công cụ sử dụng :
1. Aireplay-ng
- Tổng quan : aireplay-ng là công cụ dùng để inject vào frames, chức năng chính là dùng để tạo traffic cho cracking wep và wpa2. ngoài ra còn có thể dùng các chức năng như deauthen, fake authen, arp request,…
- Để có thể bắt được nhiều IV trong một khoảng thời gian ngắn thì ta cần :
  - Fake authentication một client có sẵn để giao tiếp với AP bằng aireplay-ng, trong đó -a là bssid của AP,  còn -h là địa chỉ MACcủa card mạng sử dụng :
![fake authen](https://github.com/annapsyktova/wepcracking/blob/img/1.png)
  - Tiếp theo ta sẽ tấn công arp vào mạng để tăng traffic trong mạng,  rút ngắn thời gian bắt gói tin, trong đó -3 là option arp-request, -b là bssid của AP, -h là địa chỉ MAC của card mạng 
  ![arp replay](https://github.com/annapsyktova/wepcracking/blob/img/2.png)
  
