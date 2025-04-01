
### Tools
Miscellaneous = find
Enumeration = LinEnum, LinPEAS



# Enumeration
We need to know what pieces of information to look for and to be able to perform enumeration manually. Check for following : - 

1. OS Version = Gives idea about tools and public exploits
2. Kernel Version = Public Exploits could be available
3. Running Services = Could have vulnerable versions
4. Installed Packages and Versions = Can have a privilege escalation vulnerability
5. Logged in Users = Other user activity can open ways for lateral movement and privilege escalation path.
6. User Home Directories = Could have ssh keys and can find credentials. At the minimum, check the ARP cache to see what other hosts are being accessed and cross-reference these against any useable SSH private keys. Also check the bash_history
7. Sudo Privileges = Check if user can run something as sudo
8. Configuration files = Can contain wealth of info like usernames etc, sometimes password and other secrets as well.
9. Readable Shadow File = Check if shadow file is readable
10. Password Hashes in /etc/passwd = The file is readable by all users and some devices like routers and embedded devices may have passwords contained in them.
11. Cron Jobs = It is like schedules Tasks. Could be leveraged to escalate privileges when schedules cron jobs run.
12. Unmounted File Systems and Additional Drivers = The unmounted file system could contain sensitive date and maybe backups as well which can be further used for the privilege escalation. 
13. SETUID and SETGID Permissions = Binaries have these permissions.
14. Writable Directories = Find writable directories where I can setup the tools and everything.
15. Writable Files = Check if any scripts of config files are world-writable. 


# Environment Enumeration
