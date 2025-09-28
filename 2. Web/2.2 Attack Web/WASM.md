---
{"dg-publish":true,"permalink":"/1-hack-like-a-script-kiddie/web/wasm/","noteIcon":"","created":"2025-04-15T14:11:19.610-04:00"}
---

Change to a readable format
```
wasm2wat file.wasm -o file.wat

```


Or Ghidra with extension
```
https://github.com/nneonneo/ghidra-wasm-plugin
```

Dump it with wasm-objdump

```
wasm-objdump -x file.wasm
```


Load it on node.js or a browser

```
const fs = require('fs');
const wasmBuffer = fs.readFileSync('./file.wasm');

WebAssembly.instantiate(wasmBuffer).then(wasmModule => {
  console.log(wasmModule.instance.exports);
});
```


## WASM? 
BLUF: `.wasm` files are often used in web apps to **hide logic**, **improve performance**, or **implement crypto/math**. 

Reverse engineer the logic, find **hidden vulnerabilities**, or bypass security controls.

---

## What to do?

###  1. **Understand what the `.wasm` is doing**

- Is it client-side validation?
    
- Is it doing crypto like key gen, hash checks, token validation?
    
- Is it hiding API secrets, user logic, or anti-debug checks?
    

###  2. **Break it or bypass it**

- Can you bypass validation the `.wasm` is doing?
    
- Can you extract a hardcoded secret?
    
- Can you hijack WebAssembly memory or corrupt it?
    
- Can you mess with JS ↔ WebAssembly interaction?
    

### 🧠 3. **Map the attack surface**

- What does it export?
    
- What does it import?
    
- What JS calls it?
    
- What arguments does it take?
    

---

##  Workflow for Bug Bounty with `.wasm`

###  Step 1: Decompile to readable format

```bash
wasm2wat file.wasm -o file.wat
```

Or use:

- [WebAssembly Explorer](https://mbebenita.github.io/WasmExplorer/)
    
- [Wabt](https://github.com/WebAssembly/wabt)
    

### 🔎 Step 2: Inspect it

Look for:

- Exported functions (`_validateToken`, `decrypt`, `verifyPin`)
    
- Hardcoded strings, base64 blobs
    
- Unusual logic (manual hashing, signature checks)
    
- Dangerous behavior like raw memory reads/writes
    

### Step 3: Rebuild and Patch

Modify logic in the `.wat`, then rebuild:

```bash
wat2wasm file.wat -o patched.wasm
```

Then serve it back in your browser using:

- Tampermonkey script
    
- Burp Repeater/Proxy
    
- DevTools override
    

###  Step 4: Abuse the logic

- Call exported functions directly from DevTools:
    

```js
fetch('file.wasm')
  .then(r => r.arrayBuffer())
  .then(buf => WebAssembly.instantiate(buf, { env: {} }))
  .then(mod => {
    console.log(mod.instance.exports);
    // try mod.instance.exports.checkPin(1234)
  });
```

- Patch it to skip logic like:
    

```wat
;; original
if (condition) then
  call $fail

;; patch: remove fail call or flip the logic
```

---

##  Real-World Bug Bounty Wins

|Example|Description|
|---|---|
|**Bypassing PIN validation**|`.wasm` checks PIN locally — patch to always return true.|
|**Extracting API secrets**|A secret or key hardcoded in `.wasm` used for HMAC/auth.|
|**Reversing challenge-response**|`.wasm` does challenge math to verify token — now you mimic it.|
|**Breaking license checks**|`.wasm` validates a license — you flip the check.|

