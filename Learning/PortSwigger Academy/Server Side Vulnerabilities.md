Table of Contents : - 
1. [[#Path Traversal]]
2. [[#Access Control]]
3. [[#Authentication Vulnerabilities]]
4. [[#Server-Side Request Forgery]]
5. [[#File Upload Vulnerability]]
6. [[#OS Command Injection]]
7. [[#SQL Injection (SQLi)]]




## Path Traversal
Read arbitrary files on the server that is running an application.
In some cases the attacker might be able to write and take full control.

Common Method = ../../../../../etc/passwd

Different Methods Learnt : - 
1. You might be able to use an absolute path from the filesystem root, such as `filename=/etc/passwd`, to directly reference a file without using any traversal sequences.
2. You might be able to use nested traversal sequences, such as `....//` or `....\/`. These revert to simple traversal sequences when the inner sequence is stripped.
3. In some contexts, such as in a URL path or the `filename` parameter of a `multipart/form-data` request, web servers may strip any directory traversal sequences before passing your input to the application. You can sometimes bypass this kind of sanitization by URL encoding, or even double URL encoding, the `../` characters. This results in `%2e%2e%2f` and `%252e%252e%252f` **For Burp Suite Professional users, Burp Intruder provides the predefined payload list Fuzzing - path traversal. This contains some encoded path traversal sequences that you can try.**
4. An application may require the user-supplied filename to start with the expected base folder, such as `/var/www/images`. In this case, it might be possible to include the required base folder followed by suitable traversal sequences. For example: `filename=/var/www/images/../../../etc/passwd`.
5. An application may require the user-supplied filename to end with an expected file extension, such as `.png`. In this case, it might be possible to use a null byte to effectively terminate the file path before the required extension. For example: `filename=../../../etc/passwd%00.png`.

Prevention : -
Avoid passing user-supplied input to the APIs all together. If it cannot be avoided then use a two layer defence with final layer as checking the canonical and the base directory.


## Access Control

**Access control** determines whether the user is allowed to carry out the action that they are attempting to perform.

1. Unprotected Admin functionalities : - The admin pages do not impose some sort of protection then it can be used by the non-administrative users as well.
	Security by obscurity is used in some cases by giving less predictable url. However, sometimes they make the UI functionality available in the code itself which doesn't impose a strict check on the website and hence can be accessed.

2. Parameter-based access control methods : - Sometimes the parameter such as `admin = True` is added or perhaps a cookie decides if a user is admin or not, or a request header. This approach also can cause the issue.

3. Insecure direct object reference (IDOR) : - This type of vulnerability arises where user-controller parameter values are used to access resources or functions directly.


There are two types of privilege escalation : - 
1. Vertical Privilege Escalation
2. Horizontal Privilege Escation
3. Horizontal to Vertical Privilege Escalation

## Authentication Vulnerabilities 

Username enumeration and password brute-force attacks are mentioned here. 
Along with that **Bypassing two-factor authentication** is something to check.
If the user is first prompted to enter a password, and then prompted to enter a verification code on a separate page, the user is effectively in a "logged in" state before they have entered the verification code. In this case, it is worth testing to see if you can directly skip to "logged-in only" pages after completing the first authentication step. Occasionally, you will find that a website doesn't actually check whether or not you completed the second step before loading the page.

## Server-Side Request Forgery
Server-side request forgery is a web security vulnerability that allows an attacker to cause the server-side application to make requests to an unintended location.
In an SSRF attack against the server, the attacker causes the application to make an HTTP request back to the server that is hosting the application, via its loopback network interface. This typically involves supplying a URL with a hostname like `127.0.0.1` (a reserved IP address that points to the loopback adapter) or `localhost` (a commonly used name for the same adapter).
The kind of trust relationships, where requests originating from the local machine are handled differently than ordinary requests, often make SSRF into a critical vulnerability.
```
POST /product/stock HTTP/1.0 
Content-Type: application/x-www-form-urlencoded 
Content-Length: 118 
stockApi=http://192.168.0.68/admin`
```

## File Upload Vulnerability

From a security perspective, the worst possible scenario is when a website allows you to upload server-side scripts, such as PHP, Java, or Python files, and is also configured to execute them as code.
So a simple web shell like : - 
``<?php echo system($_GET['command']); ?>``

There is something called **Flawed file type validation**. So like by changing the Content-Type we can sometimes make it upload a file which shouldn't be possible.

`application/x-www-form-url-encoded` ---> `multipart/form-data` 

More ways would include :- 
1. Changing the file extension to make it look like .png or something eg. image.png.php
2. Changing the magic number of the file using the hexeditor like xxd
3. Or by checking which other type of file extension can run like some support php7 but not php.

## OS Command Injection

If the application implements no defenses against OS command injection, so an attacker can submit the following input to execute an arbitrary command:

`& echo aiwefwlguh &`
Placing the additional command separator `&` after the injected command is useful because it separates the injected command from whatever follows the injection point. This reduces the chance that what follows will prevent the injected command from executing.

Take a little help from ChatGPT to generate necessary payload and use it.

## SQL Injection (SQLi)

SQL injection (SQLi) is a web security vulnerability that allows an attacker to interfere with the queries that an application makes to its database.

You can detect SQL injection manually using a systematic set of tests against every entry point in the application. To do this, you would typically submit:

- The single quote character `'` and look for errors or other anomalies.
- Some SQL-specific syntax that evaluates to the base (original) value of the entry point, and to a different value, and look for systematic differences in the application responses.
- Boolean conditions such as `OR 1=1` and `OR 1=2`, and look for differences in the application's responses.
- Payloads designed to trigger time delays when executed within a SQL query, and look for differences in the time taken to respond.
- OAST payloads designed to trigger an out-of-band network interaction when executed within a SQL query, and monitor any resulting interactions.
**Alternatively, you can find the majority of SQL injection vulnerabilities quickly and reliably using Burp Scanner.**

Also here, you can take the help ChatGPT to generate some SQL payloads. 

It can be used to bypass the password checks by commenting out the password check in its own.