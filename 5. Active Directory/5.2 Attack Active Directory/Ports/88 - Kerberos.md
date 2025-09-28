# Get username

## nmap
```
 nmap -p 88 --script=krb5-enum-users --script-args krb5-enum-users.realm="{Domain_Name}",userdb={Big_Userlist} {IP}
```

# Get username or password with kerbrute
```
git clone https://github.com/ropnop/kerbrute.git 
./kerbrute -h
```

# Get Service Principal Name with impacket
```
 Name: With Creds
  Description: Attempt to get a list of user service principal names
  Command: GetUserSPNs.py -request -dc-ip {IP} active.htb/svc_tgs

```