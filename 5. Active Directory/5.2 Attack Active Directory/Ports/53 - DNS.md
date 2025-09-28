


# dig

https://book.hacktricks.xyz/network-services-pentesting/pentesting-dns
```
dig ANY @<DNS_IP> <DOMAIN>     #Any information
dig A @<DNS_IP> <DOMAIN>       #Regular DNS request
dig AAAA @<DNS_IP> <DOMAIN>    #IPv6 DNS request
dig TXT @<DNS_IP> <DOMAIN>     #Information
dig MX @<DNS_IP> <DOMAIN>      #Emails related
dig NS @<DNS_IP> <DOMAIN>      #DNS that resolves that name
dig -x 192.168.0.2 @<DNS_IP>   #Reverse lookup
dig -x 2a00:1450:400c:c06::93 @<DNS_IP> #reverse IPv6 lookup

#Use [-p PORT]  or  -6 (to use ivp6 address of dns)
```


# nslookup
```
nslookup
> SERVER <IP_DNS> #Select dns server
> 127.0.0.1 #Reverse lookup of 127.0.0.1, maybe...
> <IP_MACHINE> #Reverse lookup of a machine, maybe...
```

# automation
```
dnsenum --dnsserver <DNS_IP> --enum -p 0 -s 0 -o subdomains.txt -f <WORDLIST> <DOMAIN>
```


# nmap
```
nmap -n --script "(default and *dns*) or fcrdns or dns-srv-enum or dns-random-txid or dns-random-srcport" <IP>
```


# dnsrecon automation
```
dnsrecon -r 127.0.0.0/24 -n <IP_DNS>  #DNS reverse of all of the addresses
dnsrecon -r 127.0.1.0/24 -n <IP_DNS>  #DNS reverse of all of the addresses
dnsrecon -r <IP_DNS>/24 -n <IP_DNS>   #DNS reverse of all of the addresses
dnsrecon -d active.htb -a -n <IP_DNS> #Zone transfer
```




# DNS - Subdomains BF

```
dnsenum --dnsserver <IP_DNS> --enum -p 0 -s 0 -o subdomains.txt -f subdomains-1000.txt <DOMAIN>
dnsrecon -D subdomains-1000.txt -d <DOMAIN> -n <IP_DNS>
dnscan -d <domain> -r -w subdomains-1000.txt #Bruteforce subdomains in recursive way, https://github.com/rbsec/dnscan
```

# Active Directory servers

```
dig -t _gc._tcp.lab.domain.com
dig -t _ldap._tcp.lab.domain.com
dig -t _kerberos._tcp.lab.domain.com
dig -t _kpasswd._tcp.lab.domain.com

nslookup -type=srv _kerberos._tcp.<CLIENT_DOMAIN>
nslookup -type=srv _kerberos._tcp.domain.com

nmap --script dns-srv-enum --script-args "dns-srv-enum.domain='domain.com'"
```

# DNSSec

```
 #Query paypal subdomains to ns3.isc-sns.info
 nmap -sSU -p53 --script dns-nsec-enum --script-args dns-nsec-enum.domains=paypal.com ns3.isc-sns.info
```

# IPv6

Brute force using "AAAA" requests to gather IPv6 of the subdomains.

```
dnsdict6 -s -t <domain>
```

Bruteforce reverse DNS in using IPv6 addresses

```
dnsrevenum6 pri.authdns.ripe.net 2001:67c:2e8::/48 #Will use the dns pri.authdns.
```