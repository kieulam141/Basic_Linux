# Toàn bộ các lệnh làm việc với file hoặc folder
## 1.cd ( Change Directory )
- di chuyển tới thư mục bất kì: `cd /etc/usr`
- di chuyển tới thư mục cha: `cd ..`
- di chuyển tới thư mục ngay trước đấy, trước khi sử dụng command *cd*: `cd --`

## 2.cp
Copy file hoặc thư mục.
- Cú pháp:
```sh
cp [options] -T SOURCE DEST
cp [options] Source directory
cp [options] -t directory source
```
- VD:
- `cp originalfile newfile` ( copy file ngay tại thư mục làm việc).Lưu ý là nếu file đích *newfile* đã tồn tại thì nó sẽ viết đè lên mà không cần hỏi.
- Nếu bạn muốn được hỏi trước khi viết đè thì thêm tùy chọn *-i*: `cp -i oldfile newfile`
- Copy file sang thư mục khác và sẽ có cùng tên với file được copy:`cp origfile /directory/subdirectory` ( nếu muốn tên file # chỉ việc thêm tên file vào sau thư mục đấy:`cp origfile /directory/subdirectory/newfile`)
- Copy nhiều file : `cp file* /directory/subdirectory`
- `cp -R /one/two /three/four` : copy toàn bộ nội dung thư mục *two* vào trong thư mục đích, nếu thư mục đích chưa có thì sẽ tạo.
- Tạo symbol link thay bằng việc copy dữ liệu, giống với lệnh `ln` nhưng có thể tạo nhiều link 1 lúc: `cp -s file.txt file2.txt`
- Lưu ý: để tạo symbol link vào thư mục khác, bạn cần chỉ rõ full pathname, bao gồm tên directory đầy đủ 

## 3.find-locate
Sử dụng để tìm và định vị các file, thư mục theo các tham số mà bạn chỉ định ( permission, users, groups, file types, date, size)
- Tìm file tại thư mục đang làm việc: `find . -name test.txt`
- Tìm tất cả file ở thư mục home: `fine /home -name test.txt`
- Tìm kiếm file theo tên không đầy đủ: `find / -name test*`
- Tìm kiếm file với phần mở rộng: `find /home -name *.php`
- Tìm kiếm file ẩn: `find / -type f -name ".*"`
- Tìm kiếm file có owner/group là *LamKT*: `find /home -user(-group) LamKT`
- Tìm kiếm file được phân quyền 777: `find . -type f -perm 777`
- Tìm file chỉ có quyền read: `find / -perm /u=r`
- Tìm kiếm file rỗng: `find /tmp -type f -empty`
- Tìm kiếm file được chỉnh sửa trong vòng 50 ngày: `find / -mtime 50`
- Tìm kiếm file được chỉnh sửa trong vòng 50 - 100 ngày: `find / -mtime +50 -mtime -100`
- Tìm kiếm file vừa được tạo ra trong vòng 1 giờ: `find / -cmin -60`
- Tìm kiếm file có dung lượng 50M: `find / -size 50M`
- Tìm kiếm file có dung lượng lớn hơn 50M nhỏ hơn 100M: `find / -size +50M -size -100M`
- Tìm thư mục có tên LamKT: `find / -type d -name LamKT`
- Tìm kiếm trên nhiều thư mục: `find /opt /usr /var -name test.txt -type f`
### 3.1.Tìm kiếm nâng cao, kết hợp với lệnh khác (rm, exec, cp, grep,..)
- Tìm và xoá file có dung lượng trên 100M: `find / -size +100M -exec rm -rf {} \;`
- Tìm và chmod 644 file có phần mở rộng là .html: `find / -type f -name "*.html" -exec chmod 644 {} \;`
- Tìm file có phần mở rộng là .mp3 và copy file đó đến thư mục /tmp/MusicFiles: `find / -type f -name "*.mp3" -exec cp /tmp/MusicFiles \;`
- Tìm file có chứa nội dụng LamKT: `find / -type f -exec grep -l 'vinahost' {} \;`
- Tìm file theo tên hoặc phần mở rộng hoặc kích thước (-o = OR): `find / \(-name '*.txt*' -o -name 'doc*' -o -size +10M\)`

### 3.2.Sử dụng locate
- Cài đặt:`yum install mlocate`
- update it’s ‘internal database’: `updatedb`
- command: `locate httpd.conf`


## 4.Grep
- 
