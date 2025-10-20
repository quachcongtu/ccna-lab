# Xem cấu hình hiện tại của Switch cùng với tổng số lượng interface Fastethernet, GigabitEthernet, số line vty cho telnet…..

> Switch#show running-config

# Trên tất cả SW Cisco đều có interface mặc định là VLAN1 dùng để quản lý SW từ xa thông qua việc đặt ip cho interface này, xem đặt điểm interface vlan 1

> Switch#show interface vlan1
```
Vlan1 is administratively down, line protocol is down
  Hardware is CPU Interface, address is 0002.17d8.2a4e (bia 0002.17d8.2a4e)
  MTU 1500 bytes, BW 100000 Kbit, DLY 1000000 usec,
     reliability 255/255, txload 1/255, rxload 1/255
  Encapsulation ARPA, loopback not set
  ARP type: ARPA, ARP Timeout 04:00:00
  Last input 21:40:21, output never, output hang never
  Last clearing of "show interface" counters never
  Input queue: 0/75/0/0 (size/max/drops/flushes); Total output drops: 0
  Queueing strategy: fifo
  Output queue: 0/40 (size/max)
  5 minute input rate 0 bits/sec, 0 packets/sec
  5 minute output rate 0 bits/sec, 0 packets/sec
     1682 packets input, 530955 bytes, 0 no buffer
     Received 0 broadcasts (0 IP multicast)
     0 runts, 0 giants, 0 throttles
     0 input errors, 0 CRC, 0 frame, 0 overrun, 0 ignored
     563859 packets output, 0 bytes, 0 underruns
     0 output errors, 23 interface resets
     0 output buffer failures, 0 output buffers swapped out
```

Thông tin Interface VLAN 1
Tên giao diện: VLAN1
- Trạng thái:
Administratively down (bị tắt thủ công bằng lệnh shutdown)
Line protocol is down (giao thức lớp 2 cũng tắt theo)
Địa chỉ MAC: 0002.17d8.2a4e
(bia 0002.17d8.2a4e nghĩa là địa chỉ MAC gốc của cổng này)
Địa chỉ IP: (Không có thông tin IP trong đầu ra, có thể chưa được gán bằng lệnh ip address)
MTU: 1500 bytes
Băng thông (Bandwidth): 100000 Kbit/s (100 Mbps)
Độ trễ (Delay): 1000000 µs (1 giây)

> Switch#show interface fa0/1 -> tình trạng interface fastethernet 0/1
```
FastEthernet0/1 is down, line protocol is down (disabled)
  Hardware is Lance, address is 0002.4a08.3901 (bia 0002.4a08.3901)
 BW 100000 Kbit, DLY 1000 usec,
     reliability 255/255, txload 1/255, rxload 1/255
  Encapsulation ARPA, loopback not set
  Keepalive set (10 sec)
  Half-duplex, 100Mb/s
  input flow-control is off, output flow-control is off
  ARP type: ARPA, ARP Timeout 04:00:00
  Last input 00:00:08, output 00:00:05, output hang never
  Last clearing of "show interface" counters never
  Input queue: 0/75/0/0 (size/max/drops/flushes); Total output drops: 0
  Queueing strategy: fifo
  Output queue :0/40 (size/max)
  5 minute input rate 0 bits/sec, 0 packets/sec
  5 minute output rate 0 bits/sec, 0 packets/sec
     956 packets input, 193351 bytes, 0 no buffer
     Received 956 broadcasts, 0 runts, 0 giants, 0 throttles
     0 input errors, 0 CRC, 0 frame, 0 overrun, 0 ignored, 0 abort
     0 watchdog, 0 multicast, 0 pause input
     0 input packets with dribble condition detected
     2357 packets output, 263570 bytes, 0 underruns
     0 output errors, 0 collisions, 10 interface resets
     0 babbles, 0 late collision, 0 deferred
     0 lost carrier, 0 no carrier
     0 output buffer failures, 0 output buffers swapped out
```

Thông tin chi tiết Interface FastEthernet0/1
Thuộc tính	Giá trị / Trạng thái
Tên cổng	FastEthernet0/1
Trạng thái vật lý (Physical Status)	Down (cổng đang tắt)
Trạng thái giao thức (Line Protocol)	Down (disabled) (giao thức lớp 2 không hoạt động)
Nguyên nhân	Interface bị tắt thủ công bằng lệnh shutdown, hoặc chưa có thiết bị nào cắm vào cổng này
Địa chỉ MAC	0002.4a08.3901
Tốc độ (Bandwidth)	100000 Kbit/s (100 Mbps)
Chế độ truyền	Half-duplex
Encapsulation	ARPA (chuẩn Ethernet)
Keepalive	Mặc định 10 giây
Gói tin nhận/gửi	- Nhận: 956 gói
- Gửi: 2357 gói |
| Lỗi đầu vào/đầu ra | 0 lỗi (CRC, frame, collision, carrier đều 0) |
| Reset giao diện | 10 lần (interface resets) – thường do bị tắt/mở lại hoặc cáp kết nối không ổn định |

# Xem thông tin về phiên bản hệ điều hành, dung lượng bộ nhớ RAM, NVRAM, Flash 

> Switch#show version 
```
Cisco IOS Software, C2960 Software (C2960-LANBASEK9-M), Version 15.0(2)SE4, RELEASE SOFTWARE (fc1)
Technical Support: http://www.cisco.com/techsupport
Copyright (c) 1986-2013 by Cisco Systems, Inc.
Compiled Wed 26-Jun-13 02:49 by mnguyen

ROM: Bootstrap program is C2960 boot loader
BOOTLDR: C2960 Boot Loader (C2960-HBOOT-M) Version 12.2(25r)FX, RELEASE SOFTWARE (fc4)

Switch uptime is 39 minutes
System returned to ROM by power-on
System image file is "flash:c2960-lanbasek9-mz.150-2.SE4.bin"


This product contains cryptographic features and is subject to United
States and local country laws governing import, export, transfer and
use. Delivery of Cisco cryptographic products does not imply
third-party authority to import, export, distribute or use encryption.
Importers, exporters, distributors and users are responsible for
compliance with U.S. and local country laws. By using this product you
agree to comply with applicable laws and regulations. If you are unable
to comply with U.S. and local laws, return this product immediately.

A summary of U.S. laws governing Cisco cryptographic products may be found at:
http://www.cisco.com/wwl/export/crypto/tool/stqrg.html

If you require further assistance please contact us by sending email to
export@cisco.com.

cisco WS-C2960-24TT-L (PowerPC405) processor (revision B0) with 65536K bytes of memory.
Processor board ID FOC1010X104
Last reset from power-on
1 Virtual Ethernet interface
24 FastEthernet interfaces
2 Gigabit Ethernet interfaces
The password-recovery mechanism is enabled.

64K bytes of flash-simulated non-volatile configuration memory.
Base ethernet MAC Address       : 00:02:17:D8:2A:4E
Motherboard assembly number     : 73-10390-03
Power supply part number        : 341-0097-02
Motherboard serial number       : FOC10093R12
Power supply serial number      : AZS1007032H
Model revision number           : B0
Motherboard revision number     : B0
Model number                    : WS-C2960-24TT-L
System serial number            : FOC1010X104
Top Assembly Part Number        : 800-27221-02
Top Assembly Revision Number    : A0
Version ID                      : V02
CLEI Code Number                : COM3L00BRA
Hardware Board Revision Number  : 0x01


Switch Ports Model              SW Version            SW Image
------ ----- -----              ----------            ----------
*    1 26    WS-C2960-24TT-L    15.0(2)SE4            C2960-LANBASEK9-M


Configuration register is 0xF
```

Thành phần	Thông tin
Model thiết bị	Cisco Catalyst WS-C2960-24TT-L
Loại CPU	PowerPC405
Phiên bản IOS	15.0(2)SE4
File hệ điều hành (System image)	flash:c2960-lanbasek9-mz.150-2.SE4.bin
Dung lượng RAM	65536K bytes (~64 MB)
Dung lượng NVRAM (Non-volatile config memory)	64K bytes
Số cổng vật lý	24 cổng FastEthernet + 2 cổng GigabitEthernet
Trạng thái password recovery	Đang bật
Configuration register	0xF (mặc định, khởi động từ flash)
Địa chỉ MAC cơ sở	00:02:17:D8:2A:4E


# Nội dung bộ nhớ Flash
Switch#show flash:
```
Directory of flash:/

    1  -rw-     4670455          <no date>  2960-lanbasek9-mz.150-2.SE4.bin

64016384 bytes total (59345929 bytes free)
```

- Thông tin chi tiết bộ nhớ Flash
Thuộc tính	Giá trị
Tên file trong Flash	2960-lanbasek9-mz.150-2.SE4.bin
Kích thước file	4,670,455 bytes (~4.46 MB)
Tổng dung lượng Flash	64,016,384 bytes (~64 MB)
Dung lượng còn trống	59,345,929 bytes (~59.3 MB)
Tỷ lệ sử dụng	Chỉ dùng ~7% dung lượng flash
Ngày tạo	<no date> → Do thiết bị không có đồng hồ thời gian thực (chưa set clock) nên không hiển thị ngày giờ chính xác
- Giải thích ý nghĩa

File 2960-lanbasek9-mz.150-2.SE4.bin là hệ điều hành Cisco IOS hiện đang chạy trên switch.
→ Nếu xóa file này, switch sẽ không khởi động được hệ điều hành (boot fail).

Flash còn gần 59 MB trống, nên bạn đủ dung lượng để lưu thêm 1 bản IOS khác nếu muốn nâng cấp phiên bản.

⚙️ Tóm tắt
Thành phần	Thông tin
Model	WS-C2960-24TT-L
IOS hiện tại	2960-lanbasek9-mz.150-2.SE4.bin
Phiên bản IOS	15.0(2)SE4
Dung lượng Flash	64 MB
Dung lượng còn trống	59 MB
Trạng thái bộ nhớ	Tốt, không đầy, hoạt động bình thường


# Xem cấu hình đang lưu trên Switch
> Switch#show startup-configure startup-config is not present

> S1#copy running-config startup-config
Lệnh này sao chép (copy) cấu hình đang chạy (running-config) → lưu vào bộ nhớ NVRAM dưới tên startup-config.

Thuật ngữ	    Nơi lưu	                                Khi nào dùng
running-config	RAM (bộ nhớ tạm)	                    Cấu hình đang hoạt động hiện tại trên switch
startup-config	NVRAM (bộ nhớ không mất khi tắt nguồn)	Cấu hình sẽ được tự động tải khi khởi động lại thiết bị


- Khi bạn cấu hình switch (ví dụ: đặt IP, VLAN, password, v.v.), các thay đổi chỉ nằm trong RAM → tức là running-config.
- Nếu bạn không lưu lại, khi tắt nguồn hoặc reboot, tất cả cấu hình sẽ mất hết.
- Vì vậy, bạn cần sao chép running-config sang startup-config để lưu cấu hình vĩnh viễn.



Lệnh	                                            Chức năng
copy running-config startup-config	                Lưu cấu hình hiện tại vào NVRAM
copy startup-config running-config	                Khôi phục cấu hình đã lưu để chạy ngay
show running-config	                                Xem cấu hình đang hoạt động
show startup-config	                                Xem cấu hình đã lưu trong NVRAM


# Mục đích của việc đặt mật khẩu

Việc đặt mật khẩu giúp ngăn người lạ hoặc người không được phép truy cập vào thiết bị mạng (switch/router).
Trên thiết bị Cisco, có 3 cấp độ truy cập chính, tương ứng với 3 loại mật khẩu:

Cấp độ	                        Chế độ truy cập                 Ví dụ prompt	    Mật khẩu bảo vệ
User EXEC mode	                Chế độ xem thông tin cơ bản	    Switch>	            Không có (hoặc bảo vệ bằng Console/Telnet password)
Privileged EXEC mode	        Chế độ cấu hình nâng cao	    Switch#	            enable secret
Global/Interface config mode	Cấu hình hệ thống	            Switch(config)#	    Chỉ truy cập được khi đã vào Privileged mode


# Giải thích từng loại mật khẩu trong ví dụ của bạn
a. Mật khẩu cho cổng Console

S1(config)# line console 0
S1(config-line)# password cisco
S1(config-line)# login
S1(config-line)# exit


- Mục đích:

Bảo vệ truy cập trực tiếp qua cổng console (tức là khi bạn cắm dây console vào switch).
Khi người dùng mở terminal console, hệ thống sẽ yêu cầu nhập mật khẩu này.

- Khi nên đặt:

Bắt buộc nên đặt trên tất cả thiết bị Cisco (switch, router, firewall).
Vì đây là cách truy cập vật lý trực tiếp – ai cắm dây là vào được.

b. Mật khẩu cho line VTY (Telnet/SSH)

S1(config)# line vty 0 4
S1(config-line)# password cisco
S1(config-line)# login
S1(config-line)# exit

- Mục đích:

Bảo vệ khi truy cập từ xa qua Telnet hoặc SSH.
Khi bạn kết nối từ máy tính khác bằng lệnh telnet 192.168.1.1, switch sẽ yêu cầu nhập mật khẩu này.

- Khi nên đặt:

Bắt buộc nên đặt, đặc biệt nếu bạn cho phép quản lý từ xa.
Nếu có thể, nên dùng SSH thay cho Telnet, vì SSH mã hóa dữ liệu còn Telnet thì không.

c. Mật khẩu enable secret

S1(config)# enable secret class

- Mục đích:

Bảo vệ chế độ Privileged EXEC (Switch#).
Khi bạn đang ở chế độ Switch> (User mode), muốn chuyển sang Switch#, bạn phải nhập mật khẩu này.

- Khi nên đặt:

Luôn luôn đặt! Đây là mật khẩu quan trọng nhất.
Nó mã hóa trong file cấu hình, nên an toàn hơn enable password.


# Interface là gì?

Interface (giao diện mạng) là cổng kết nối vật lý hoặc logic mà thiết bị dùng để gửi và nhận dữ liệu mạng.
Trên switch hoặc router, mỗi cổng Ethernet (FastEthernet, GigabitEthernet) được xem là một interface vật lý.
Ngoài ra còn có interface ảo (virtual) như:

- Vlan1 (interface VLAN)
- Loopback0
- Tunnel0
- Serial0/0/0 (nếu có module WAN)

# Interface vật lý (Physical Interface)

Ví dụ trên switch Cisco Catalyst 2960:

FastEthernet0/1
FastEthernet0/2
...
FastEthernet0/24
GigabitEthernet0/1
GigabitEthernet0/2


➡️ Mỗi dòng trên tương ứng một cổng mạng vật lý thật trên switch
(nơi bạn cắm dây mạng RJ-45 vào để kết nối đến máy tính, router, access point, v.v.)

✅ Kết luận:

Mỗi interface vật lý = 1 cổng thật trên thiết bị,
và mỗi cổng đó có thể kết nối với 1 thiết bị khác (máy tính, switch, router...).

# Interface ảo (Virtual Interface)

Một số interface không có cổng vật lý, mà là logic (ảo).

Ví dụ:

interface vlan1
 ip address 192.168.1.1 255.255.255.0
 no shutdown


→ Đây không phải là cổng thật, mà là interface ảo để switch có địa chỉ IP quản lý (dùng Telnet/SSH, Ping...).

📘 Trên switch layer 2 (như 2960):

Chỉ VLAN interface (SVI) có thể mang IP.
Các cổng vật lý (FastEthernet/GigabitEthernet) thường không có IP mà thuộc về VLAN nào đó.

# So sánh nhanh
Loại interface	    Ví dụ	            Kết nối với	                    Có IP được không?	Ghi chú
Vật lý	            FastEthernet0/1	    Máy tính, router, switch khác	❌(trên L2 switch)	Là cổng thật
VLAN (ảo)	        Vlan1	            Không kết nối vật lý	        ✅	                Dùng để quản lý switch
Loopback (ảo)	    Loopback0	        Không kết nối vật lý	        ✅	                Dùng test, quản lý router
Serial (vật lý)	    Serial0/0/0	        Router khác	                    ✅	                Trên router có cổng WAN

💡 Ví dụ thực tế:

Giả sử switch có 24 cổng:

- Cổng Fa0/1 nối đến PC1
- Cổng Fa0/2 nối đến PC2
- Cổng Fa0/24 nối đến router
→ Tất cả là interface vật lý riêng biệt.

Và switch có VLAN1 với IP 192.168.1.2 —
→ Đây là interface ảo dùng để bạn Telnet/SSH vào switch.

✅ Tóm lại:

Mỗi interface vật lý là một cổng mạng thật dành cho một thiết bị kết nối.
Ngoài ra còn có interface ảo (VLAN, Loopback) dùng để quản lý hoặc định tuyến logic.


# Tổng quan nhanh:

Trong mạng LAN có VLAN, mỗi thiết bị (PC) cần:

Địa chỉ IP riêng của chính nó
Default Gateway (cổng mặc định) để biết đường ra ngoài VLAN

⚙️ Ví dụ minh họa thực tế:

Giả sử có VLAN 10:
VLAN 10: 192.168.10.0/24

Switch layer 3 hoặc router có cấu hình:

interface vlan 10
 ip address 192.168.10.1 255.255.255.0


→ IP 192.168.10.1 là IP của VLAN 10, đồng thời là Gateway cho các máy trong VLAN đó.

🖥️ Cấu hình trên máy PC trong VLAN 10:
Thiết bị	IP	            Subnet Mask	    Default Gateway
PC1	        192.168.10.2	255.255.255.0	192.168.10.1
PC2	        192.168.10.3	255.255.255.0	192.168.10.1

➡️ Giải thích:

Mỗi PC có IP riêng biệt trong cùng dải mạng.
Gateway (192.168.10.1) là IP của VLAN 10 trên switch/router — dùng khi PC muốn gửi gói tin ra ngoài mạng (VD sang VLAN khác hoặc Internet).

📶 Tóm gọn lại:
Thành phần	        Chức năng
IP trên PC	        Định danh riêng cho máy trong mạng LAN
Gateway (VLAN IP)	Thiết bị trung gian (switch L3 hoặc router) giúp PC ra ngoài VLAN hoặc ra Internet
VLAN Interface IP	Đóng vai trò như Gateway cho tất cả PC trong VLAN đó
💡 Ghi nhớ nhanh:

🧩 “IP là của từng máy”
🧩 “Gateway là IP của interface VLAN (hoặc router)”
