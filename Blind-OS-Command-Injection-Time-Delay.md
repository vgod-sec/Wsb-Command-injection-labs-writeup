# Lab: Blind OS Command Injection with Time Delays

> **Level**: Practitioner  
> **Lab Type**: Web Security Academy – OS Command Injection  
> **Vulnerability**: Blind OS Command Injection (Time-Based)


## Description

This lab demonstrates a Blind OS Command Injection vulnerability in a web application’s feedback functionality. The server executes a shell command using user-supplied input without proper sanitization. Since the output of the command is not returned in the response, we use **time-based techniques** to confirm successful injection.

The goal is to trigger a 10-second delay in the response by injecting a command that causes a delay, confirming code execution on the server.


##  Exploitation Steps

1. Intercept the feedback request using **Burp Suite**.
2. Modify the `email` parameter to include a delay-inducing command.
3. Inject the following payload:

   ```bash
   email=example@tech.com||ping+-c+10+127.0.0.1||

4. Forword the request and observe the response delay.
5. if delay occurs the lab is solved.


## Mitigation

- Avoid using user input in system commands; use safe APIs instead.  
- Validate and sanitize all inputs using allow-lists.  
- Use least privilege principle and apply a Web Application Firewall (WAF).
