
Its an open source software, a framework for making websites easily and its easy to make these websites.
Its a CMS (Content Management System).

It powers one third of all the websites present on the internet. 

**A CMS is made up of two key components:

- A Content Management Application (CMA) - the interface used to add and manage content.
- A Content Delivery Application (CDA) - the backend that takes the input entered into the CMA and assembles the code into a working, visually appealing website.**


*Word press requires LAMP stack (Linux operating system, Apache HTTP Server, MySQL database, and the PHP programming language).*

**Key Wordpress directories : - The ==wp-content== and the ==uploads== directories should be enumerated carefully as they contain sensitive data that could lead to Remote Code Execution or Exploitation of other vulnerabilities or misconfigurations.**

The various roles that Wordpress have are as follows : - 
Administrator, Editor, Author, Contributor, Subscriber.

### Version Enumeration

First we try to find the version so that we can look for default passwords and the vulnerabilities related to that particular version. So for this we look for the page's source code. And then we look for the **meta-generator**.
In older WordPress versions, another source for uncovering version information is the `readme.html` file in WordPress's root directory.

#### Plugins and Themes Enumeration
In the response header from the plugins and themes we can find the version of the website from there.
Here can enumerate both passively and actively. In active enumeration we try to directly access the resource using the curl.
We can use the following tools for it : -

==**WPScan**
**wfuzz**==

### Directory Indexing
We can look for the security issues in the deactivated plugins. We can view the directory listing using the curl and convert the HTML output to a nice readable format using **html2text**.
This is called Directory Indexing.
So here there was a lab given. In this lab, I first ran a curl command and looked for the different endpoints related to the plugins and used some advanced methods to grab them. 


### User Enumeration

There are two methods for the user enumeration as we need it for checking the default password and hacking by brute forcing the password etc.

1. By the use of the curl command we can manually check by author id = 1 etc.
2. By using the curl on the json for users which is valid for all versions before 4.7.1

### Login
This attack can be performed via the login page or the `xmlrpc.php` page. We will do a POST request on that page.
So its just an Information

### WPScan Enumeration
It is an automated Wordpress scanner and enumeration tool. It determines if the various themes and plugins used by a WordPress site are outdated or vulnerable.

We use `--enumerate` flag to enumerate various components such as plugins, themes and users. By default, it looks for vulnerable plugins, themes, media, users and backup.
We can get the api key for the https://wpvulndb.com/ which will be helpful for better enumeration.

API key = `zbQOIqqesfaNZy1gknb2unng2zS6qmJOlBZxRQzTHpw`

# Exploitation

As we using the WPscan in order to figure out the version of the Wordpress and we have identified the vulnerable plugins. 
We then found out that there are three users from the Wpscan of the website. And on those users we tried to find the password by using the rockyou.txt
Now we can do the theme edit to get a web shell and once the webshell is up then just access it. You will need to encode the commands and put them on the link on the curl.

#### Attacking Wordpress using Metasploit

We can use `wp_admin` 
This module can 