

# The First Step
### Enumeration
In this step focus on the following : - 
1. OS Version
2. Kernel Version
3. Running Services
4. Installed Packages and Version
5. Logged in users
6. User Home Directories : - This can give the ssh_keys if the user have it in his home dir. Also have a look for the **history**. 
7. Sudo Privileges : - Check for `sudo -l` . This command will List User's Privileges. 
8. Configuration Files : - Check for extensions as .conf and .config
9. Readable Shadow File :  Check if the shadow file can be accessed for the passwords
10. Passwords in /etc/passed : - This can happen in embedded devices and routers.
11. Cron Jobs : - This can be leveraged to run a privilege escalation when misconfiguration happens.
12. Unmounted File Systems and Additional Drives : - This can be used to check the backup and others.
13. SETUID and SETGID Permissions : - Binaries are set with these permissions to allow a user to run a command as root, without the grant of root level access. Many binaries contain functionality which can be exploited to get a root shell.
14. Writable Directories : - Its important to discover writable directories cuz if we want to download tools and write scripts on the exploited PC then its important.
15. Writable Files :- If we find a file like this and we write a shell so the next time it is executed with a higher permission we can get the shell or something.


### Environment Enumeration
Scripts like : - Linpeas and LinEnum for enumeration
