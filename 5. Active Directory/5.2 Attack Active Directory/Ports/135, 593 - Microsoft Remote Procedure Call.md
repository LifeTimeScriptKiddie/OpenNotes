
![](attachment/Pasted%20image%2020240813083649.png)
https://0xffsec.com/handbook/images/msrpc.png

The Microsoft Remote Procedure Call (MSRPC) protocol, a client-server model enabling a program to request a service from a program located on another computer without understanding the network's specifics, was initially derived from open-source software and later developed and copyrighted by Microsoft.

https://book.hacktricks.xyz/network-services-pentesting/135-pentesting-msrpc

# Tools
```
# Get information without information
impacket-rpcdump <ip> <port>

# with valid creds
impacket-dcomexec 

https://github.com/mubix/IOXIDResolver
```


## Notable RPC interfaces

- **IFID**: 12345778-1234-abcd-ef00-0123456789ab
    
- **Named Pipe**: `\pipe\lsarpc`
    
- **Description**: LSA interface, used to enumerate users.
    
- **IFID**: 3919286a-b10c-11d0-9ba8-00c04fd92ef5
    
- **Named Pipe**: `\pipe\lsarpc`
    
- **Description**: LSA Directory Services (DS) interface, used to enumerate domains and trust relationships.
    
- **IFID**: 12345778-1234-abcd-ef00-0123456789ac
    
- **Named Pipe**: `\pipe\samr`
    
- **Description**: LSA SAMR interface, used to access public SAM database elements (e.g., usernames) and brute-force user passwords regardless of account lockout policy.
    
- **IFID**: 1ff70682-0a51-30e8-076d-740be8cee98b
    
- **Named Pipe**: `\pipe\atsvc`
    
- **Description**: Task scheduler, used to remotely execute commands.
    
- **IFID**: 338cd001-2244-31f1-aaaa-900038001003
    
- **Named Pipe**: `\pipe\winreg`
    
- **Description**: Remote registry service, used to access and modify the system registry.
    
- **IFID**: 367abb81-9844-35f1-ad32-98f038001003
    
- **Named Pipe**: `\pipe\svcctl`
    
- **Description**: Service control manager and server services, used to remotely start and stop services and execute commands.
    
- **IFID**: 4b324fc8-1670-01d3-1278-5a47bf6ee188
    
- **Named Pipe**: `\pipe\srvsvc`
    
- **Description**: Service control manager and server services, used to remotely start and stop services and execute commands.
    
- **IFID**: 4d9f4ab8-7d1c-11cf-861e-0020af6e7c57
    
- **Named Pipe**: `\pipe\epmapper`
    
- **Description**: DCOM interface, used for brute-force password grinding and information gathering via WM.
    



# Resource
https://www.cyber.airbus.com/the-oxid-resolver-part-1-remote-enumeration-of-network-interfaces-without-any-authentication/

https://github.com/mubix/IOXIDResolver

[hacktricks](https://book.hacktricks.xyz/network-services-pentesting/135-pentesting-msrpc#identifying-ip-addresses)

[https://www.cyber.airbus.com/the-oxid-resolver-part-1-remote-enumeration-of-network-interfaces-without-any-authentication/](https://www.cyber.airbus.com/the-oxid-resolver-part-1-remote-enumeration-of-network-interfaces-without-any-authentication/)
    
[https://www.cyber.airbus.com/the-oxid-resolver-part-2-accessing-a-remote-object-inside-dcom/](https://www.cyber.airbus.com/the-oxid-resolver-part-2-accessing-a-remote-object-inside-dcom/)

[https://0xffsec.com/handbook/services/msrpc/](https://0xffsec.com/handbook/services/msrpc/)