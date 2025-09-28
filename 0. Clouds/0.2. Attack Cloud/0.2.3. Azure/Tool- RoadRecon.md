---
{"dg-publish":true,"permalink":"/1-hack-like-a-script-kiddie/clouds/azure/tool-road-recon/","noteIcon":"","created":"2025-04-15T14:11:19.597-04:00"}
---







So roadrecon didn't work on my host. I had some compatibility issue with legacy code. Instead installing roadrecon on my host, I installed in virtual environment. 


https://www.freecodecamp.org/news/how-to-setup-virtual-environments-in-python/


```
pip install virtualenv
python3 -m venv <venv name>

mkdir venv       
cd venv                 
python3 -m venv env        
source env/bin/activate

deactivate

```

roadrecon was well working in virtual environment. 
```


pip install roadrecon


roadrecon auth -u matteus@megabigtech.com -p SUMMERDAZE1!
Tokens were written to .roadtools_auth
┌──(env)─(kali㉿kali)-[~/Documents/pwnedlabs/venv]
└─$ roadrecon gather                                         
Starting data gathering phase 1 of 2 (collecting objects)
Starting data gathering phase 2 of 2 (collecting properties and relationships)
ROADrecon gather executed in 11.03 seconds and issued 1823 HTTP requests.
┌──(env)─(kali㉿kali)-[~/Documents/pwnedlabs/venv]
└─$ roadrecon gui   
 * Serving Flask app 'roadtools.roadrecon.server'
 * Debug mode: off
WARNING: This is a development server. Do not use it in a production deployment. Use a production WSGI server instead.
 * Running on http://127.0.0.1:5000
Press CTRL+C to quit


```
