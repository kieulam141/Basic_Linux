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

## 3.find
Sử dụng để tìm và định vị các file, thư mục theo các tham số mà bạn chỉ định ( permission, users, groups, file types, date, size)
- Tìm file tại thư mục đang làm việc: `find . -name test.txt`
- Tìm tất cả file ở thư mục home: `fine /home -name test.txt`
