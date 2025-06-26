# 🔍 Lab: Blind OS Command Injection with Output Redirection

**Category:** OS Command Injection  
**Difficulty:** Practitioner  


##  Description

This lab contains a **blind OS command injection vulnerability** in the feedback form. The output of injected commands is not directly returned in the response. However, the server has a **writable directory**: /var/www/images
By redirecting command output to a file inside this folder, we can retrieve it using the image loading functionality of the application.


##  Objective

> Execute the `ls` command and retrieve its output via the application.


## Exploitation Steps

1. **Intercept the feedback submission request** using **Burp Suite**.
2. Modify the `email` parameter to inject the command and redirect output:
    email=example@tech.com || ls>/var/www/images/filename.txt

3. **Forward the request**
4. Intercept the image loading request.
5. Modify the `filename` parameter to load the output of file:(filename.txt)
6.  **Forward the request** and observe the response. The command output will be displayed 

 or

https://<LAB-ID>.web-security-academy.net/image?filename=filename.txt

##  Payloads Used

### Feedback submission payload:
```bash
email=example@tech.com||ls>/var/www/images/output.txt||
