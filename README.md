# SQL_Injection
#### Untrusted data sẽ rơi vào câu lệnh query
#### có thể sử dụng dấu ; để thực thi nhiều câu lệnh query cùng lúc trong mysql 
#### mysql_query chỉ thực hiện được 1 câu lệnh query thôi, cùng tùy vào phiên bản
#### tùy vào câu lệnh mà dev dùng ta có thể sử dụng '-- - hoặc or 1 = '1 có thể sửu dụng dấu ' hoặc "
#### có thể trong câu lệnh truy vấn dev kh cùng (select username,passwd from user where username = "$username" and passwd = "$passwd") mà lại dùng (select username,passwd from user where username = "$username" sau đó mới đi so sánh passwd sau) thì lúc này dấu -- - và dấu OR vô nghĩa
#### thao túng (làm giả) kết quả trả về có thể dùng select a,b union select 1,2,.....
# String concatenation
  Oracle 	'foo'||'bar'
  Microsoft 	'foo'+'bar'
  PostgreSQL 	'foo'||'bar'
  MySQL 	'foo' 'bar' 
  CONCAT('foo','bar')
# Substring
  Oracle 	SUBSTR('foobar', 4, 2)
  Microsoft 	SUBSTRING('foobar', 4, 2)
  PostgreSQL 	SUBSTRING('foobar', 4, 2)
  MySQL 	SUBSTRING('foobar', 4, 2) 
# Comments
  Oracle      --comment
  Microsoft 	--comment
              /*comment*/
  PostgreSQL 	--comment
              /*comment*/
  MySQL 	#comment
          -- comment 
          /*comment*/
 # version
Oracle 	SELECT banner FROM v$version
        SELECT version FROM v$instance
Microsoft 	SELECT @@version
PostgreSQL 	SELECT version()
MySQL 	SELECT @@version 
# Database contents
Oracle 	SELECT * FROM all_tables
        SELECT * FROM all_tab_columns WHERE table_name = 'TABLE-NAME-HERE'
Microsoft 	SELECT * FROM information_schema.tables
            SELECT * FROM information_schema.columns WHERE table_name = 'TABLE-NAME-HERE'
PostgreSQL 	SELECT * FROM information_schema.tables
            SELECT * FROM information_schema.columns WHERE table_name = 'TABLE-NAME-HERE'
MySQL 	SELECT * FROM information_schema.tables
        SELECT * FROM information_schema.columns WHERE table_name = 'TABLE-NAME-HERE'
