## **✅** ​Basic Usage Workflow

```
# 1. Import the script
Import-Module .\SharpHound.ps1

# 2. Run the collection
Invoke-BloodHound -CollectionMethod All -Domain yourdomain.local -ZipFileName data.zip
```

---

## **🛠️** 

## **Common CollectionMethod Options**

|**Method**|**Description**|
|---|---|
|All|All below methods (default)|
|Default|GroupMembership, LocalAdmin, Session, Trusts|
|GroupMembership|Enumerate group membership recursively|
|LocalAdmin|Find users/groups with local admin rights on hosts|
|Session|Enumerate active sessions|
|LoggedOn|Like Session, but includes disconnected accounts (if admin)|
|Trusts|Discover AD trust relationships|
|ACL|Collect ACLs on objects|
|ObjectProps|Object properties like OS, description|
|RDP|RDP-enabled systems|
|Dcom|DCOM-enabled systems|
|PSRemote|PowerShell Remoting-enabled systems|
|ComputerOnly|Only enumerate computer objects|

---

## **🎯** 

## **Example Commands**

  

### **1. All default collection (recommended initial run)**

```
Invoke-BloodHound -CollectionMethod Default -Domain CONTOSO.LOCAL -ZipFileName default.zip
```

### **2. Target specific computer(s)**

```
Invoke-BloodHound -CollectionMethod All -ComputerName "DC01","Server01"
```

### **3. Specific methods**

```
Invoke-BloodHound -CollectionMethod ACL,Trusts,Session
```

### **4. Avoid touching the disk (OpSec)**

```
Invoke-BloodHound -CollectionMethod All -NoSaveCache -Stealth
```

---

## **🔐** 

## **OpSec-Safe Flags**

|**Flag**|**Purpose**|
|---|---|
|-NoSaveCache|Prevents writing to disk|
|-Stealth|Disables potentially high-noise enumeration like Session or RDP|
|-RandomDelay|Introduces random delay between requests|
|-Throttle|Introduces fixed delay (in milliseconds) between requests|

---




OR go easy with sharphound.exe 

`SharpHound.exe -c all`