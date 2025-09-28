---
{"dg-publish":true,"permalink":"/1-hack-like-a-script-kiddie/web/deserialization-net/debug-with-dnspy-dnn/","noteIcon":"","created":"2025-04-15T14:11:19.601-04:00"}
---


















 
 
# 1. Enable Debugger - dnn offsec
 
  To reduce the amount of optimization performed at runtime, we can change that attribute.

Right click and go to Edit Assembly Attributes

![](https://i.imgur.com/Bp1PiC9.png)

Delete 
```
[assembly: Debuggable(DebuggableAttribute.DebuggingModes.IgnoreSymbolStoreSequencePoints)]

```


Add
```
[assembly: Debuggable(DebuggableAttribute.DebuggingModes.Default | DebuggableAttribute.DebuggingModes.DisableOptimizations | DebuggableAttribute.DebuggingModes.IgnoreSymbolStoreSequencePoints | DebuggableAttribute.DebuggingModes.EnableEditAndContinue)]
```

![](https://i.imgur.com/hkGJsxe.png)

Then Save Module 
![](https://i.imgur.com/S48aPmK.png)


# 2. Attach Debugger

Pause the process by break all.
![](https://i.imgur.com/3u9Je7d.png)




Attach to process.
![](https://i.imgur.com/RXpwTF8.png)



Select w3wp.exe
	why? --> This is the IIS worker process under which our instance of DNN is running.
![](https://i.imgur.com/VpV7HDJ.png)

