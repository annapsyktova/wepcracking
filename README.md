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
  - Tiếp theo ta sẽ tấn công arp vào mạng để tăng traffic trong mạng,  rút ngắn thời gian bắt gói tin, trong đó -3 là option arp-request, -b là bssid của AP, -h là địa chỉ MAC của card mạng :
  
  ![arp replay](https://github.com/annapsyktova/wepcracking/blob/img/2.png)
  
2. Aircrack-ng
- Tổng quan : là công cụ để crack wep/wpa2.  Có thể sử dụng trên windows cũng như linux. Trên windows thì aircrack-ng có giao diện như thế này :

![aircrack-ng GUI windows](https://github.com/annapsyktova/wepcracking/blob/img/3.png)
![aircrack-ng GUI windows](https://github.com/annapsyktova/wepcracking/blob/img/4.png)
![aircrack-ng GUI windows](https://github.com/annapsyktova/wepcracking/blob/img/5.png)
- Trên kali thì aircrack-ng sẽ có giao diện như thế này :

![aircrack-ng kali](https://github.com/annapsyktova/wepcracking/blob/img/6.png)
3. Airodump-ng
- Tổng quan : là công cụ để bắt gói tin, bắt thông tin các mạng xung quanh, từ đây chúng ta có thể biết được các thông tin quan trọng như BSSID, channel, các client truy cập vào AP.
- Để thực hiện bắt gói tin bằng airodump :
  - Sử dụng câu lệnh airodump-ng wlan0mon :
  
  ![airodump-ng](https://github.com/annapsyktova/wepcracking/blob/img/7.png)
  - Sau khi có các thông tin như bssid và channel của AP,  ta tiếp tục sử dụng airodump-ng để bắt gói tin
  
  ![airodump-ng](https://github.com/annapsyktova/wepcracking/blob/img/8.png)
  ![airodump-ng](https://github.com/annapsyktova/wepcracking/blob/img/9.png)
4. Commview
- Là công cụ để bắt gói tin trên windows, tương tự như airodump-ng.
- Giao diện của Commview :

![Commview GUI](https://github.com/annapsyktova/wepcracking/blob/img/10.png)
- Cách bắt gói tin trên Commview :
- Đầu tiên ta sẽ sử dụng scanner mode để tìm kiếm wifi cần thực hiện phá mã.
- Khi tìm được rồi ta có thể chuyển sang single channel mode với channel trùng với channel của wifi cần tìm và bắt đầu quá trình bắt gói tin.
![Commview mode](https://github.com/annapsyktova/wepcracking/blob/img/11.png)

- Commview có chế độ lưu file log và ta có thể export ra file pcap để phục vụ cho việc crack gói tin bằng aircrack-ng :
![Commview packet capture](https://github.com/annapsyktova/wepcracking/blob/img/12.png)

5. Kismet
- Là công cụ bắt gói tin trên linux, giống như airodump-ng.
- để chạy Kismet, ta cần enable monitor mode của card mạng và chạy kismet. Web interface lúc đó sẽ sẵn sàng ở địa chỉ [localhost:2501](http:\\localhost:2501)
