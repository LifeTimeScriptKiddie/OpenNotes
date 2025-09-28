---
{"dg-publish":true,"permalink":"/1-hack-like-a-script-kiddie/web/deserialization-net/white-box-approach/","noteIcon":"","created":"2025-04-15T14:11:19.602-04:00"}
---

















Sure, let's tie these concepts to practical examples for both white box and black box testing scenarios.

### White Box Testing Examples:

1. **Identifying Deserialization Functions:**
   - **Example:** Suppose you are reviewing a C# codebase. You find the following code that uses `XmlSerializer`:
   - The following Items can be serialized using XmlSerializer
	   - Public read/write properties and fields of public classes.
	   - Classes that implement ICollection or IEnumerable
     ```csharp
     public T Deserialize<T>(string xml)
     {
         XmlSerializer serializer = new XmlSerializer(typeof(T));
         using (StringReader reader = new StringReader(xml))
         {
             return (T)serializer.Deserialize(reader);
         }
     }
     ```
     **Action:** Highlight this function and trace where the `xml` parameter originates. Check if it’s directly influenced by user input.

2. **Examining Input Sources:**
   - **Example:** You discover a method that reads data from an HTTP request:
     ```csharp
     public void ProcessRequest(HttpRequest request)
     {
         string xmlData = request.Form["data"];
         MyObject obj = Deserialize<MyObject>(xmlData);
         // Further processing...
     }
     ```
     **Action:** Investigate how `request.Form["data"]` is validated before being deserialized. Lack of validation indicates a potential vulnerability.

3. **Reviewing Object Creation:**
   - **Example:** You find the following code:
     ```csharp
     Type objType = Type.GetType(request.Form["type"]);
     object obj = Activator.CreateInstance(objType);
     ```
     **Action:** Check if `request.Form["type"]` is properly validated against a whitelist of allowed types. If not, it might allow arbitrary object creation.

4. **Checking for Security Controls:**
   - **Example:** You see that `XmlSerializer` is used without any type checks:
     ```csharp
     XmlSerializer serializer = new XmlSerializer(typeof(MyObject));
     ```
     **Action:** Recommend using a safer deserialization library or implementing strict type checks.
