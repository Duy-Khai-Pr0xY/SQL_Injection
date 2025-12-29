# SQL_Injection
#### Untrusted data sẽ rơi vào câu lệnh query
#### có thể sử dụng dấu ; để thực thi nhiều câu lệnh query cùng lúc trong mysql 
#### mysql_query chỉ thực hiện được 1 câu lệnh query thôi, cùng tùy vào phiên bản
#### tùy vào câu lệnh mà dev dùng ta có thể sử dụng '-- - hoặc or 1 = '1 có thể sửu dụng dấu ' hoặc "
#### có thể trong câu lệnh truy vấn dev kh cùng (select username,passwd from user where username = "$username" and passwd = "$passwd") mà lại dùng (select username,passwd from user where username = "$username" sau đó mới đi so sánh passwd sau) thì lúc này dấu -- - và dấu OR vô nghĩa
#### thao túng (làm giả) kết quả trả về có thể dùng select a,b union select 1,2,.....
