# PortSwigger Lab: Simple OS Command Injection

Level: Apprentice  
Category: OS Command Injection  

##  Description

This lab demonstrates a basic OS command injection vulnerability in the product stock checker functionality of a web application.

The application executes a **shell command** that includes **user-supplied `productId` and `storeId` parameters**. The server executes this command and returns the raw command output in the HTTP response.

To solve the lab, we need to **inject the `whoami` command** and observe the username returned by the server. This confirms command execution on the target system.


## Steps to Exploit

1. **Intercept the Request** using **Burp Suite** when checking stock availability for a product.
2. **Locate the `storeId` parameter** in the request.
3. **Inject the payload**:
   ```
   1|whoami
   ```
   This uses the pipe `|` to append the `whoami` command to the original shell command.
4. **Forward the request** and observe the response.
5. If successful, the **response will contain the current system user**, confirming command execution.

---

## 💥 Vulnerable Parameter

- `storeId`

---

## 🧪 Example Payload

```
storeId=1|whoami
```

---

## ✅ Outcome

The injected `whoami` command runs on the server, and the output is displayed in the response — solving the lab.


## Learnings

- Basic command injection often occurs when user input is directly embedded into system commands without proper sanitization.
- The `|` operator chains additional commands in Unix-like systems.
- Always validate and sanitize user input before using it in system-level operations.

##  Mitigation

- Avoid direct execution of system commands with user input.
- Use safe APIs and parameterized methods.
- Sanitize input strictly using allow-lists.
- Employ Web Application Firewalls (WAFs) to detect injection patterns.
