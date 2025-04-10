

## Access Control

**Access control** determines whether the user is allowed to carry out the action that they are attempting to perform.

1. Unprotected Admin functionalities : - The admin pages do not impose some sort of protection then it can be used by the non-administrative users as well.
	Security by obscurity is used in some cases by giving less predictable url. However, sometimes they make the UI functionality available in the code itself which doesn't impose a strict check on the website and hence can be accessed.

2. Parameter-based access control methods : - Sometimes the parameter such as `admin = True` is added or perhaps a cookie decides if a user is admin or not, or a request header. This approach also can cause the issue.

3. Insecure direct object reference (IDOR) : - This type of vulnerability arises where user-controller parameter values are used to access resources or functions directly.


There are two types of privilege escalation : - 
1. Vertical Privilege Escalation
2. Horizontal Privilege Escation
