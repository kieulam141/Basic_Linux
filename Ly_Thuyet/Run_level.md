# Change Runlevels and Shut Down or Reboot System

### 1.Boot the System
- Các loại boot loader như LILO (Linux Loader) hay GRUB (Grand Unified BootLoader), để khởi động kernel Linux.

#### 1.1.Boot-time Kernel Parameters
- Set trong file cấu hình boot loader của bạn (/etc/lilo.conf hoặc /boot/grub/menu.lst và /boot/grub/grub.conf hoặc /boot/grub2/grub.cfg(Cent7))
- Tuy nhiên Linux kernel có thể được tùy chỉnh khi khởi động bằng command-line interface.

#### 1.2.Introduction to Kernel Module Configuration
- Linux kernel là 1 dạng module
- Nó có thể được chèn hoặc xóa bởi superuser nếu cần thiết ( sử dụng command insmod và rmmod )
- Các thông điệp Linux kernel khi khởi động:
<ul>
  <li>Khi Linux Kernel khởi động, nó sẽ show ra các trạng thái chi tiết của các tiến trình trong các bản tin console: Kernel identification, thông tin CPU và Ram, thông tin về hardware, thiết lập network...</li>
  <li>Để xem các bản tin từ lần boot cuối cùng: `dmesg | more` </li> 
</ul>
- Bạn cũng có thể xem lại các log về system : */var/log/messages*

### 2.Change Runlevels and Shut Down or Reboot System
- Chỉ định các cách khác nhau để sử dụng hệ thống bằng việc controll các service nào chạy.
- Các mức level của Runlevel:0-6
| Runlevel | Description |
| --- | --- |
| 0 | Dừng hệ thống.Runlevel 0 là 1 trạng thái chuyển tiếp dặc biệt được sử dụng bởi admin để shutdown hệ thống ngay lập tức.|
| 1 , s , S | Chế độ Single-user, hay còn gọi là chế độ bảo trì.Các dịch vụ hệ thống như network interface, web server và file không được chạy.|
| 2 | Chế đô Multi-user.Trên hệ thống Debian-base thì là runlevel mặc định.Trên Redhat thì là mode multi-user ko có NFS hoặc GUI.|
| 3 | Trên Redhad thì là runlevel mặc định.level 3,4,5 k có trên debian.|
| 4 | không dùng |
| 5 | Trên hệ thống Redhat thì là chế độ multi-user với GUI login.|
| 6 | Reboot lại hệ thống |

#### 2.1.Single-User Mode
- Runlevel 1 mục đích cho bảo trì hệ thống.
- Remote logins, network bị disabled và đa số các deamon ko đc chạy.
- lý do để sử dụng mode này là để fix lỗi filesystem mà hệ thống k thể xử lý tự động.
- Để chuyển sang mode này : `init 1`

#### 2.2.Overview of the /etc Directory Tree and the init Process
- Khi hệ thống Linux chạy, nó sẽ chạy các scripts ở /etc để thực hiện các cấu hình hệ thống và chuyển giữa các runlevel.
- /etc/rc.sysinit và /etc/init.d/rcS :
<ul>
  <li>Hệ thống thực thi script.</li>
  <li>Script được chạy bởi init khi khởi động.</li>
  <li>Script được thiết kế để chạy trước khi bất kì daemons nào chạy</li>
</ul>
- /etc/rc.local 
<ul>
  <li>Được gọi sau tất cả những script init khác.</li>
  <li>Bao gồm các tùy chỉnh local tác động tới việc khởi động hệ thống và cung cấp 1 sự luân phiên để chỉnh sửa các init script khác.</li>
  <li>Các admin thường tránh việc thay đổi /etc/init.d hoặc /etc/rc.d vì những thay đổi sẽ bị mất nếu upgrade hệ thống.còn thay đổi ở /etc/rc.local k bị mất.</li>
</ul>
- /etc/rc: file script này để chuyển giữa các runlevel.
- /etc/init.d:
<ul>
  <li>Thư mục bao gồm các script startup/shutdown riêng biệt cho mỗi dịch vụ.</li>
  <li>Các tham số: start, stop, restart, status, reload.</li>
</ul>

#### 2.3.Setting the Default Runlevel
- Để quyết định runlevel mặc định khi khởi động, init đọc cấu hình ở file /etc/inittab: `id:N:initdefault:`
- N là giá trị runlvel thường là 3.
- Không được đổi N thành 0 hoặc 6.

#### 2.4.Determining Your System’s Runlevel
- Sử dụng command `runlevel`
- Nó sẽ show ra runlevel trước và hiện tại bằng số và tách bằng dấu cách

### 3.Reset Root Password
#### 3.1.Cent6~
- Khởi động lại hệ thống
- Khi đang boot ở GRUB, bấm các phím di chuyển hoặc phím cách để làm gián đoạn.
- Nhập "a" để tùy chỉnh các tham số kernel.
- Thêm số `1` vào cuối *rhgb quiet* để boot vào mode single user.
- Sau khi vào được hệ thống với mode single user, bạn gõ lệnh `passwd` để đổi password cho root.

#### 3.2.Cent7
- Khởi động lại hệ thống
- Khi đang boot ở GRUB, bấm phím `e`
- Tiếp tục tìm đến đoạn có chứ ro và thay ro= rw init=/sysroot/bin/sh.
- Bấm CTRL + x để bắt đầu chế độ single user.
- Truy cập vào hệ thống bằng command `chroot /sysroot`
- thay đổi password root: `passwd root`
- Update Selinux: `touch /.autorelabel`
- Exit và reboot.
