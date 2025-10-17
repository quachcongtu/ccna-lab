# Yêu cầu:
- Chặn toàn bộ kết nối từ VLAN 99 (GUEST) tới các VLAN nội bộ
- VLAN GUEST vẫn kết nối được tới internet

### Những thứ tôi dùng trong phần lab này

- router 2811 (internet)
- router 2811 (R1)
- switch 2960 
- 3 PC-PT (PC1, PC2, PC3)

### Phần cấu hình của từng thành phần một

- Internet kết nối với R1: Fa0/1 - Fa0/1
- R1 kết nối với switch: Fa0/0 - Fa0/1
- Switch kết nối với PC: Fa0/2,3,4 - Fa0/0

Cấu hình Switch

```
enable
conf t

vlan 10
 name NV1
vlan 11
 name NV2
vlan 99
 name GUEST

interface range f0/2
 switchport mode access
 switchport access vlan 10

interface range f0/3
 switchport mode access
 switchport access vlan 11

interface range f0/4
 switchport mode access
 switchport access vlan 99

interface f0/1
 switchport mode trunk
 switchport trunk allowed vlan 10,11,99

end
wr

```

Cấu hình R1 (Gateway chính)

```
enable
conf t

! Tạo subinterface cho từng VLAN
interface fa0/0.10
 encapsulation dot1Q 10
 ip address 10.0.10.1 255.255.255.0

interface fa0/0.11
 encapsulation dot1Q 11
 ip address 10.0.11.1 255.255.255.0

interface fa0/0.99
 encapsulation dot1Q 99
 ip address 192.168.1.1 255.255.255.0

interface fa0/0
 no shutdown

! Kết nối ra Internet (internet)
interface fa0/1
 ip address 203.0.113.2 255.255.255.0
 no shutdown

! Định tuyến ra Internet
ip route 0.0.0.0 0.0.0.0 203.0.113.1

! ACL chặn Guest VLAN truy cập VLAN nội bộ
ip access-list extended BLOCK_GUEST
 deny ip 192.168.1.0 0.0.0.255 10.0.10.0 0.0.0.255
 deny ip 192.168.1.0 0.0.0.255 10.0.11.0 0.0.0.255
 permit ip any any

interface fa0/0.99
 ip access-group BLOCK_GUEST in

! Cấu hình NAT cho phép ra Internet
ip access-list standard NAT_INSIDE
 permit 10.0.10.0 0.0.0.255
 permit 10.0.11.0 0.0.0.255
 permit 192.168.1.0 0.0.0.255

ip nat inside source list NAT_INSIDE interface fa0/1 overload

! Xác định vùng NAT
interface fa0/0.10
 ip nat inside
interface fa0/0.11
 ip nat inside
interface fa0/0.99
 ip nat inside
interface fa0/1
 ip nat outside

end
wr

```

Cấu hình internet

```
enable
conf t
interface fa0/1
 ip address 203.0.113.1 255.255.255.0
 no shutdown

! Giả lập địa chỉ “Internet” bằng Loopback
interface loopback0
 ip address 8.8.8.8 255.255.255.255

end
wr

```

Cấu hình ip cho các PC

- PC1 (thuộc VLAN 10)
- Bấm đúp vào PC1
- Chọn tab Desktop → IP Configuration

Nhập thông tin như sau:

```
IP Address: 10.0.10.2
Subnet Mask: 255.255.255.0
Default Gateway: 10.0.10.1
DNS Server: (để trống)

```

- PC2 (thuộc VLAN 11)
- Bấm đúp vào PC2
- Chọn Desktop → IP Configuration

Nhập:

```
IP Address: 10.0.11.2
Subnet Mask: 255.255.255.0
Default Gateway: 10.0.11.1
DNS Server: (để trống)

```

- PC3 (thuộc VLAN 99 – Guest)
- Bấm đúp PC3
- Chọn Desktop → IP Configuration

Nhập:

```
IP Address: 192.168.1.2
Subnet Mask: 255.255.255.0
Default Gateway: 192.168.1.1
DNS Server: (để trống)

```

Sau khi config xong thì ta test:

Trên PC1 ping như sau

```
ping 10.0.11.2     # VLAN 10 ↔ VLAN 11 → OK
ping 192.168.1.2   # VLAN 10 ↔ VLAN 99 → OK
ping 8.8.8.8       # Internet → OK

```

Trên PC GUEST ping như sau

```
ping 10.0.10.2     # Bị chặn (ACL)
ping 8.8.8.8       # OK (NAT ra Internet)

```

Nếu ở PC1 ping không đến được PC GUEST mà 8.8.8.8 vẫn được sẽ fix như sau

Đầu tiên hãy kiểm tra: `show run | sec 0/0.99` trong R1

Nếu kết quả là:

```
interface FastEthernet0/0.99 
encapsulation dot1Q 99 
ip address 192.168.1.1 255.255.255.0 
ip access-group BLOCK_GUEST 
in ip nat inside

```

Thì sửa:

```
conf t
interface FastEthernet0/0.99
 no ip access-group BLOCK_GUEST in
 ip access-group BLOCK_GUEST out
end

```

Vì:

Interface FastEthernet0/0.99 (mạng 192.168.1.0/24) đang có:

ip access-group BLOCK_GUEST in


Điều này nghĩa là Access-list BLOCK_GUEST được áp dụng inbound
→ nó lọc tất cả gói tin đi vào router từ VLAN 99 (mạng Guest).

Mà trong ACL BLOCK_GUEST, bạn có dòng:

deny ip 192.168.1.0 0.0.0.255 10.0.10.0 0.0.0.255
deny ip 192.168.1.0 0.0.0.255 10.0.11.0 0.0.0.255


👉 tức là ngăn Guest truy cập đến mạng nội bộ 10.0.10.x và 10.0.11.x.
Điều này đúng với yêu cầu đề bài (Guest không được vào nội bộ).

Nhưng hiện tại, bạn đang gắn ACL này inbound ở cổng của Guest,
nên khi máy nội bộ ping ra 192.168.1.x, gói tin phản hồi từ Guest bị chặn quay ngược lại, do chiều "in" bị chặn luôn.
Thay vì chặn inbound, ta nên chặn outbound (ra khỏi router về Guest)
để chỉ ngăn Guest chủ động đi vào mạng nội bộ, mà vẫn cho nội bộ ping tới Guest.
