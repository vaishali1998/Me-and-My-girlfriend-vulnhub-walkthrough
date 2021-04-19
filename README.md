# Me-and-My-girlfriend-vulnhub-walkthrough
This is walkthrough of vulnhub CTF Me and My girlfriend. Difficulty Level: Beginner



## Scanning

**nmap target-ip**

![Me%20and%20My%20Girlfriend%201002e8110f6c4cd49ad194e4ded13f4c/Untitled.png](Me%20and%20My%20Girlfriend%201002e8110f6c4cd49ad194e4ded13f4c/Untitled.png)

Service Version scan - **nmap -sV -A target-ip**

![Me%20and%20My%20Girlfriend%201002e8110f6c4cd49ad194e4ded13f4c/Untitled%201.png](Me%20and%20My%20Girlfriend%201002e8110f6c4cd49ad194e4ded13f4c/Untitled%201.png)

## Enumeration

PORT 80

open in browser http://target-ip

![Me%20and%20My%20Girlfriend%201002e8110f6c4cd49ad194e4ded13f4c/Untitled%202.png](Me%20and%20My%20Girlfriend%201002e8110f6c4cd49ad194e4ded13f4c/Untitled%202.png)

Open view-source page

![Me%20and%20My%20Girlfriend%201002e8110f6c4cd49ad194e4ded13f4c/Untitled%203.png](Me%20and%20My%20Girlfriend%201002e8110f6c4cd49ad194e4ded13f4c/Untitled%203.png)

There is some hint for using x-forwarded-for

Intercept request on burp.

![Me%20and%20My%20Girlfriend%201002e8110f6c4cd49ad194e4ded13f4c/Untitled%204.png](Me%20and%20My%20Girlfriend%201002e8110f6c4cd49ad194e4ded13f4c/Untitled%204.png)

Add **x-forwarded-for:localhost** and forward request.

![Me%20and%20My%20Girlfriend%201002e8110f6c4cd49ad194e4ded13f4c/Untitled%205.png](Me%20and%20My%20Girlfriend%201002e8110f6c4cd49ad194e4ded13f4c/Untitled%205.png)

Again open browser. Now it shows login and register page.

![Me%20and%20My%20Girlfriend%201002e8110f6c4cd49ad194e4ded13f4c/Untitled%206.png](Me%20and%20My%20Girlfriend%201002e8110f6c4cd49ad194e4ded13f4c/Untitled%206.png)

click on register link, fill the form and click on login button.

![Me%20and%20My%20Girlfriend%201002e8110f6c4cd49ad194e4ded13f4c/Untitled%207.png](Me%20and%20My%20Girlfriend%201002e8110f6c4cd49ad194e4ded13f4c/Untitled%207.png)

It is redirecting to login page. Now Login with username and password.

![Me%20and%20My%20Girlfriend%201002e8110f6c4cd49ad194e4ded13f4c/Untitled%208.png](Me%20and%20My%20Girlfriend%201002e8110f6c4cd49ad194e4ded13f4c/Untitled%208.png)

After login, We noticed that user_id is passed in url. So we try to change user id.

**user_id=5**

![Me%20and%20My%20Girlfriend%201002e8110f6c4cd49ad194e4ded13f4c/Untitled%209.png](Me%20and%20My%20Girlfriend%201002e8110f6c4cd49ad194e4ded13f4c/Untitled%209.png)

Intercept request on burp.

![Me%20and%20My%20Girlfriend%201002e8110f6c4cd49ad194e4ded13f4c/Untitled%2010.png](Me%20and%20My%20Girlfriend%201002e8110f6c4cd49ad194e4ded13f4c/Untitled%2010.png)

We found password for user alice: **4lic3**

Connecting to ssh using **alice:4lic3**

![Me%20and%20My%20Girlfriend%201002e8110f6c4cd49ad194e4ded13f4c/Untitled%2011.png](Me%20and%20My%20Girlfriend%201002e8110f6c4cd49ad194e4ded13f4c/Untitled%2011.png)

***Successfully connected.

**ls -al**

**cd .my_secret**

**ls -al**

![Me%20and%20My%20Girlfriend%201002e8110f6c4cd49ad194e4ded13f4c/Untitled%2012.png](Me%20and%20My%20Girlfriend%201002e8110f6c4cd49ad194e4ded13f4c/Untitled%2012.png)

We got flag1.txt

![Me%20and%20My%20Girlfriend%201002e8110f6c4cd49ad194e4ded13f4c/Untitled%2013.png](Me%20and%20My%20Girlfriend%201002e8110f6c4cd49ad194e4ded13f4c/Untitled%2013.png)

## Privilege escalation

cd /var/www/html

cd config

There is config.php file 

**cat config.php**

![Me%20and%20My%20Girlfriend%201002e8110f6c4cd49ad194e4ded13f4c/Untitled%2014.png](Me%20and%20My%20Girlfriend%201002e8110f6c4cd49ad194e4ded13f4c/Untitled%2014.png)

Found password for root user. **root:ceban_corp** 

**su root**

Enter password and we got shell for root user.

cd /root

![Me%20and%20My%20Girlfriend%201002e8110f6c4cd49ad194e4ded13f4c/Untitled%2015.png](Me%20and%20My%20Girlfriend%201002e8110f6c4cd49ad194e4ded13f4c/Untitled%2015.png)

***Found flag2.txt

![Me%20and%20My%20Girlfriend%201002e8110f6c4cd49ad194e4ded13f4c/Untitled%2016.png](Me%20and%20My%20Girlfriend%201002e8110f6c4cd49ad194e4ded13f4c/Untitled%2016.png)
