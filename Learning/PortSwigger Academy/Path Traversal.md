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

