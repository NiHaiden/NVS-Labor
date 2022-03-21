---
title: NVS Apache Protokoll
author: Niklas Haiden - 5BHIF
date: 20.12.2021
tableofcontent: true
lang: "en"
titlepage: true
titlepage-text-color: "ffffff"
logo: "logo.png"
logo-width: 100mm
toc-own-page: true
listings-disable-line-numbers: true
---
# Theory
## Apache 2
### ports.conf
Source: 
[How To Configure the Apache Web Server on an Ubuntu or Debian VPS | DigitalOcean](https://www.digitalocean.com/community/tutorials/how-to-configure-the-apache-web-server-on-an-ubuntu-or-debian-vps)

In this file, one can define the ports on which Apache will listen to. The two most important ports, 80 and 443 are already in there.
```XML
# If you just change the port or add more ports here, you will likely also
# have to change the VirtualHost statement in
# /etc/apache2/sites-enabled/000-default.conf

Listen 80

<IfModule ssl_module>
        Listen 443
</IfModule>

<IfModule mod_gnutls.c>
        Listen 443
</IfModule>

# vim: syntax=apache ts=4 sw=4 sts=4 sr noet
```

### apache2.conf
This is the main config file for the Apache Webserver. Almost all configuration can be done from within this file, although it is recommended to use separate, designated files for simplicity. This file will configure defaults and be the central point of access for the server to read configuration details.

This file is divided into three main sections: configuration for the global Apache server process, configuration for the default server, and configuration of Virtual Hosts.

In Ubuntu and Debian, the majority of the file is for global definitions, and the configuration of the default server and virtual hosts is handled at the end, by using the "Include ..." directive.

The "Include" directive allows Apache to read other configuration files into the current file at the location that the statement appears. The result is that Apache dynamically generates an overarching configuration file on startup.

If you scroll to the bottom of the file, there are a number of different "Include" statements. These load module definitions, the ports.conf document, the specific configuration files in the "conf.d/" directory, and finally, the Virtual Host definitions in the "sites-enabled/" directory.

### conf.d/
This directory is used for controlling specific aspects of the Apache configuration. For example, it is often used to define SSL configuration and default security choices.

### sites-available/
This directory contains all of the virtual host files that define different web sites. These will establish which content gets served for which requests. These are available configurations, not active configurations.

### sites-enabled/
This directory establishes which virtual host definitions are actually being used. Usually, this directory consists of symbolic links to files defined in the "sites-available" directory.

### mods-[enabled,available]/
These directories are similar in function to the sites directories, but they define modules that can be optionally loaded instead.

## HTTP Requests
Source: 
[Understand the Flow of a HTTP Request | by Aakash Yadav | Better Programming](https://betterprogramming.pub/understand-the-flow-of-a-http-request-1a268ec193f0)

![Image](Pasted image 20211217193825.png)

Source: [HTTP Requests](https://www.codecademy.com/article/http-requests)

When you type an address such as [www.codecademy.com](https://codecademy.com/) into your browser, you are commanding it to open a TCP channel to the server that responds to that URL (or Uniform Resource Locator, which you can read more about on [Wikipedia](https://en.wikipedia.org/wiki/Uniform_Resource_Locator)). A URL is like your home address or phone number because it describes how to reach you.

In this situation, your computer, which is making the request, is called the client. The URL you are requesting is the address that belongs to the server.

Once the TCP connection is established, the client sends a HTTP _GET_ request to the server to retrieve the webpage it should display. After the server has sent the response, it closes the TCP connection. If you open the website in your browser again, or if your browser automatically requests something from the server, a new connection is opened which follows the same process described above. GET requests are one kind of HTTP method a client can call. You can learn more about the other common ones (_POST_, _PUT_ and _DELETE_) in [this article](https://www.codecademy.com/articles/what-is-rest).

Let’s explore an example of how GET requests (the most common type of request) are used to help your computer (the client) access resources on the web.

Suppose you want to check out the latest course offerings from [http://codecademy.com](http://codecademy.com/). After you type the URL into your browser, your browser will extract the `http` part and recognize that it is the name of the network protocol to use. Then, it takes the domain name from the URL, in this case “codecademy.com”, and asks the internet Domain Name Server to return an Internet Protocol (IP) address.

Now the client knows the destination’s IP address. It then opens a connection to the server at that address, using the `http` protocol as specified. It will initiate a GET request to the server which contains the IP address of the host and optionally a data payload. The GET request contains the following text:

This identifies the type of request, the path on [www.codecademy.com](https://codecademy.com/) (in this case, “/“) and the protocol “HTTP/1.1.” HTTP/1.1 is a revision of the first HTTP, which is now called HTTP/1.0. In HTTP/1.0, every resource request requires a separate connection to the server. HTTP/1.1 uses one connection more than once, so that additional content (like images or stylesheets) is retrieved even after the page has been retrieved. As a result, requests using HTTP/1.1 have less delay than those using HTTP/1.0.

The second line of the request contains the address of the server which is `www.codecademy.com`. There may be additional lines as well depending on what data your browser chooses to send.

If the server is able to locate the path requested, the server might respond with the header:

This header is followed by the content requested, which in this case is the information needed to render [www.codecademy.com](https://codecademy.com/).

The first line of the header, `HTTP/1.1 200 OK`, is confirmation that the server understands the protocol that the client wants to communicate with (`HTTP/1.1`), and an [HTTP status code](https://en.wikipedia.org/wiki/List_of_HTTP_status_codes) signifying that the resource was found on the server. The second line, `Content-Type: text/html`, shows the type of content that it will be sending to the client.

If the server is not able to locate the path requested by the client, it will respond with the header:

```
HTTP/1.1 404 NOT FOUND
```

In this case, the server identifies that it understands the HTTP protocol, but the `404 NOT FOUND` status code signifies that the specific piece of content requested was not found. This might happen if the content was moved or if you typed in the URL path incorrectly or if the page was removed. You can read more about the 404 status code, commonly called a 404 error, [here](https://www.codecademy.com/articles/http-errors-404).

## CGI
Source: [Common Gateway Interface - Wikipedia](https://en.wikipedia.org/wiki/Common_Gateway_Interface)

In computing, Common Gateway Interface (CGI) is an interface specification that enables web servers to execute an external program, typically to process user requests.

Such programs are often written in a scripting language and are commonly referred to as CGI scripts, but they may include compiled programs.

A typical use case occurs when a Web user submits a Web form on a web page that uses CGI. The form's data is sent to the Web server within an HTTP request with a URL denoting a CGI script. The Web server then launches the CGI script in a new computer process, passing the form data to it. The output of the CGI script, usually in the form of HTML, is returned by the script to the Web server, and the server relays it back to the browser as its response to the browser's request.

Developed in the early 1990s, CGI was the earliest common method available that allowed a Web page to be interactive. Although still in use, CGI is relatively inefficient compared to newer technologies and has largely been replaced by them.

Each Web server runs HTTP server software, which responds to requests from web browsers. Generally, the HTTP server has a directory (folder), which is designated as a document collection – files that can be sent to Web browsers connected to this server.[9] For example, if the Web server has the domain name example.com, and its document collection is stored at /usr/local/apache/htdocs/ in the local file system, then the Web server will respond to a request for http://example.com/index.html by sending to the browser the (pre-written) file /usr/local/apache/htdocs/index.html.

For pages constructed on the fly, the server software may defer requests to separate programs and relay the results to the requesting client (usually, a Web browser that displays the page to the end user). In the early days of the Web, such programs were usually small and written in a scripting language; hence, they were known as scripts.

Such programs usually require some additional information to be specified with the request. For instance, if Wikipedia were implemented as a script, one thing the script would need to know is whether the user is logged in and, if logged in, under which name. The content at the top of a Wikipedia page depends on this information.

HTTP provides ways for browsers to pass such information to the Web server, e.g. as part of the URL. The server software must then pass this information through to the script somehow.

Conversely, upon returning, the script must provide all the information required by HTTP for a response to the request: the HTTP status of the request, the document content (if available), the document type (e.g. HTML, PDF, or plain text), et cetera.

Initially, different server software would use different ways to exchange this information with scripts. As a result, it wasn't possible to write scripts that would work unmodified for different server software, even though the information being exchanged was the same. Therefore, it was decided to specify a way for exchanging this information: CGI (the Common Gateway Interface, as it defines a common way for server software to interface with scripts). Webpage generating programs invoked by server software that operate according to the CGI specification are known as CGI scripts.

This specification was quickly adopted and is still supported by all well-known server software, such as Apache, IIS, and (with an extension) node.js-based servers.

An early use of CGI scripts was to process forms. In the beginning of HTML, HTML forms typically had an "action" attribute and a button designated as the "submit" button. When the submit button is pushed the URI specified in the "action" attribute would be sent to the server with the data from the form sent as a query string. If the "action" specifies a CGI script then the CGI script would be executed and it then produces an HTML page.

# Practice
## Installation of Apache2
A word to avoid confusion: `->  ~` is in the shell logs because I installed ZSH and replaced bash with it. The name or symbol next to arrow indicate the current folder where we are.

### Installing Apache2
We install Apache using the built in package manager.
```Bash
->  ~ sudo apt install apache2
[sudo] password for schueler:
Reading package lists... Done
Building dependency tree
Reading state information... Done
[...]
Enabling module access_compat.
Enabling module authn_file.
Enabling module authz_user.
Enabling module alias.
Enabling module dir.
Enabling module autoindex.
Enabling module env.
Enabling module mime.
Enabling module negotiation.
Enabling module setenvif.
Enabling module filter.
Enabling module deflate.
Enabling module status.
Enabling module reqtimeout.
Enabling conf charset.
Enabling conf localized-error-pages.
Enabling conf other-vhosts-access-log.
Enabling conf security.
Enabling conf serve-cgi-bin.
Enabling site 000-default.
Created symlink /etc/systemd/system/multi-user.target.wants/apache2.service → /lib/systemd/system/apache2.service.
Created symlink /etc/systemd/system/multi-user.target.wants/apache-htcacheclean.service → /lib/systemd/system/apache-htcacheclean.service.
Processing triggers for ufw (0.36-6) ...
Processing triggers for systemd (245.4-4ubuntu3.13) ...
Processing triggers for man-db (2.9.1-1) ...
Processing triggers for libc-bin (2.31-0ubuntu9.2) ...
[...]
```

### Test Installation
![First Test after Install](Pasted image 20211117140516.png)

## Create DNS Records 
To make the server accessible via easily recognizable names, I created DNS Records with the WebGUI from Webmin on a server running the Bind9 Nameserver:
- niklas-public.nvs.lan 
- niklas-private.nvs.lan

The Webmin interface is accessible under the following address:
[Webmin Interface](https://10.128.10.1:10000/bind8/edit_recs.cgi?zone=nvs.lan&view=any&type=A&sort=&xnavigation=1)

I created two A records that point to my Server in the network:

![DNS Records](dns_entry.png)

After that, I put in the URL into my web browser to see if the DNS records were put in correctly:

![Verify DNS Record](Pasted image 20211117142501.png)

## Virtual Hosts
VirtualHost files are the backbone of the Apache Webserver. They contain a variety of options so that Apache knows where to point the user when access a specific Web URL. 

### Structure of a Virtual Host File 
VirtualHost Files contain a variety of different options. They have a structure that is similar to XML or HTML. 
- They first start with a `<VirtualHost *PORT>` so that Apache knows it is a Virtual Host file. Here you need to the define the Port on which they VirtualHost should be accessible on. 

- The `ServerName` Option embedded in the VirtualHost File is crucial. It tells Apache which FQDN (Fully-Qualified-Domain-Name) to look out for. Based on this name, Apache will decide on where to route the request. 

- The `ServerAdmin` Directive can be used to define an E-Mail Address which should appear if the Website is not functioning correctly. Apache will display this address if something is not working right. It is not crucial to add this directive to a VirtualHost file, in certain situations in can be useful tho. 

- `DocumentRoot` is another very crucial directive. It tells Apache where to look for HTML or CGI-related files (e.g. PHP Files). If there is no files present in the folder, Apache will display an empty file tree structure in the browser. If the folder contains HTML or CGI-Files, but it contains no `index.html` or `index.php` (in the example of PHP) file, Apache will list the contents of the folder. If desired, the Default File can be changed with the `Default: index2.html` Directive in the Virtual Host File.

The `ErrorLog` Directive tells Apache where to store error logs for the specified virtualhost. 

### Create public host 
We create VirtualHost for niklas-public, which has the `DocumentRoot` sitting in the `/var/www/public` folder.
```XML
<VirtualHost *:80>
        ServerName niklas-public.nvs.lan
        ServerAdmin webmaster@doesntgoanywhere.com
        DocumentRoot /var/www/public
        <Directory /var/www/public>
                Options Indexes FollowSymLinks MultiViews
                AllowOverride None
                Require all granted
        </Directory>
        ErrorLog /var/log/apache2/error.log
        LogLevel warn
        CustomLog /var/log/apache2/access.log combined
        ServerSignature On
</VirtualHost>
```

### Create private host 
We create VirtualHost for niklas-public, which has the `DocumentRoot` sitting in the `/var/www/private` folder. The options remain the same as for the public file above, where the only parts being changed are the ServerName and the folder where Apache looks for HTML files.
```XML 
<VirtualHost *:80>
        ServerName niklas-private.nvs.lan
        ServerAdmin webmaster@doesntgoanywhere.com
        DocumentRoot /var/www/private
        <Directory /var/www/private>
                Options Indexes FollowSymLinks MultiViews
                AllowOverride None
                Require all granted
        </Directory>
        ErrorLog /var/log/apache2/error.log
        LogLevel warn
        CustomLog /var/log/apache2/access.log combined
        ServerSignature On
</VirtualHost>
```

### Create directories for html files 
With `mkdir` I created the two needed directories in the `/var/www` folder.
```Bash
->  sites-available sudo mkdir -p /var/www/public
->  sites-available sudo mkdir -p /var/www/private
```

### Change permissions
Since the directories were created with sudo in the step above, we need to change the ownership rights from `root` to `www-data`, which is the user that Apache is operating on. This is done with `chown` command with the option `-R` to apply all permissions recursively. 
```Bash 
->  sites-available sudo chown -R www-data:www-data /var/www/public
->  sites-available sudo chown -R www-data:www-data /var/www/private
```

### Enabling the new sites
To enable the sites and make Apache2 recognize them, we have to use the `a2ensite` command with the ServerName we defined earlier afterwards. It will create a symlink to `sites-enabled` which will let Apache2 know, that the sites are active and should be loaded by it.
```Bash
->  sites-available sudo a2ensite niklas-public.nvs.lan
Enabling site niklas-public.nvs.lan.
To activate the new configuration, you need to run:
  systemctl reload apache2
->  sites-available sudo a2ensite niklas-private.nvs.lan
Enabling site niklas-private.nvs.lan.
To activate the new configuration, you need to run:
  systemctl reload apache2
```

After enabling the sites, we reload the services so it loads the VirtualHost Files in memory and enables them.
```Bash 
->  sites-available sudo systemctl reload apache2
```

### Testing new virtual hosts
To test the new sites, I navigated to the sites via a web browser.

#### Testing the public virtual host
I created a index.html file for the public virtual host in the respective folder with the following content:
```HTML
<h1> Hello there</h1>
```

![Testing the public area](Pasted image 20211117142323.png)

Sadly the emoji didn't survive.

#### Testing the private area 
I created a index.html file for the private virtual host in the respective folder with the following content:
```HTML 
<h1>Go away, this is my private area for my stuff!</h1>
```

![Testing the private area](Pasted image 20211117142501.png)

# SSL 
So far we've only accessed the website via the old and insecure way - through the HTTP protocol. This was fine in the early days of the internet, but today, Websites need to secure their users and one way this is done is through SSL certificates and encryption of the connection to a webserver with HTTPS.

## Prerequisites 
To use HTTPS with Apache, we need to prepare some things.

### Enable SSL Module
First, we need to enable the SSL Module of Apache so that it can process HTTPS requests and load the VirtualHost file with respective options added to it. 
We use the `a2enmod` which is the short version of "enable-module". We pass it the parameter of the desired module, in this case `ssl`.
```Bash
->  ~ sudo a2enmod ssl
[sudo] password for schueler:
Considering dependency setenvif for ssl:
Module setenvif already enabled
Considering dependency mime for ssl:
Module mime already enabled
Considering dependency socache_shmcb for ssl:
Enabling module socache_shmcb.
Enabling module ssl.
See /usr/share/doc/apache2/README.Debian.gz on how to configure SSL and create self-signed certificates.
To activate the new configuration, you need to run:
  systemctl restart apache2
```

To complete the process, we have to restart the Apache2 Service so it loads the required modules.
```Bash
->  ~ sudo systemctl restart apache2
```

## Generating SSL Certificates
To use HTTPS, we need to certificates so the web browser can verify the identity and integrity of our connection. We generate one using the easy-rsa utility.

First we generate a CA-Dir, which we use later on to generate certificate. What we do here is essentially creating our own certification authority.

`make-cadir` prepares a folder with some files for us:
```Bash
->  ~ make-cadir ~/niklasca
->  ~ cd niklasca
->  niklasca ls
easyrsa  openssl-easyrsa.cnf  vars  x509-types
```

We edit the `vars` file to indicate our location and how our certificate authority is called:
```
->  niklasca vim vars
```

Contents: 
```

[...]

set_var EASYRSA_REQ_COUNTRY "AT"

set_var EASYRSA_REQ_PROVINCE "Lower Austria"

set_var EASYRSA_REQ_CITY "Die Hölle"

[...]
```

Then we initialize the Private Key Infrastructure:
```
->  niklasca ./easyrsa init-pki

Note: using Easy-RSA configuration from: ./vars

init-pki complete; you may now create a CA or requests.
Your newly created PKI dir is: /home/schueler/niklasca/pki
```

Now we build a CA-Authority which will be imported later in the Firefox Web Browser: 
```
->  niklasca ./easyrsa build-ca

Note: using Easy-RSA configuration from: ./vars

Using SSL: openssl OpenSSL 1.1.1f  31 Mar 2020

Enter New CA Key Passphrase:
Re-Enter New CA Key Passphrase:
Generating RSA private key, 2048 bit long modulus (2 primes)
................+++++
...............................+++++
e is 65537 (0x010001)
Can't load /home/schueler/niklasca/pki/.rnd into RNG
140682725274944:error:2406F079:random number generator:RAND_load_file:Cannot open file:../crypto/rand/randfile.c:98:Filename=/home/schueler/niklasca/pki/.rnd
You are about to be asked to enter information that will be incorporated
into your certificate request.
What you are about to enter is what is called a Distinguished Name or a DN.
There are quite a few fields but you can leave some blank
For some fields there will be a default value,
If you enter '.', the field will be left blank.
-----
Common Name (eg: your user, host, or server name) [Easy-RSA CA]:Der Hoellen

CA creation complete and you may now import and sign cert requests.
Your new CA certificate file for publishing is at:
/home/schueler/niklasca/pki/ca.crt
```


With the authority built, we carry on on building a specific certificate for the public virtualhost:
```
->  niklasca ./easyrsa build-server-full niklas-public.nvs.lan

Note: using Easy-RSA configuration from: ./vars

Using SSL: openssl OpenSSL 1.1.1f  31 Mar 2020
Generating a RSA private key
..+++++
...........................................................................................................+++++
writing new private key to '/home/schueler/niklasca/pki/private/niklas-public.nvs.lan.key.9UhotU8oWX'
Enter PEM pass phrase:
Verifying - Enter PEM pass phrase:
-----
Using configuration from /home/schueler/niklasca/pki/safessl-easyrsa.cnf
Enter pass phrase for /home/schueler/niklasca/pki/private/ca.key:
Check that the request matches the signature
Signature ok
The Subject's Distinguished Name is as follows
commonName            :ASN.1 12:'niklas-public.nvs.lan'
Certificate is to be certified until Nov  1 14:55:16 2024 GMT (1080 days)

Write out database with 1 new entries
Data Base Updated
```

Since we needed a PEM Passphrase earlier, we use the OpenSSL utility to essentially rip the required passphrase out of the Private Key so Apache can read it, without us requiring to enter the PEM Passphrase everytime we want to restart the Apache Server.
```
->  niklasca sudo openssl rsa -in pki/private/niklas-public.nvs.lan.key -out pki/private/niklas-public.nvs.lan.key
Enter pass phrase for pki/private/niklas-public.nvs.lan.key:
unable to load Private Key
140020021810496:error:06065064:digital envelope routines:EVP_DecryptFinal_ex:bad decrypt:../crypto/evp/evp_enc.c:610:
140020021810496:error:23077074:PKCS12 routines:PKCS12_pbe_crypt:pkcs12 cipherfinal error:../crypto/pkcs12/p12_decr.c:62:
140020021810496:error:2306A075:PKCS12 routines:PKCS12_item_decrypt_d2i:pkcs12 pbe crypt error:../crypto/pkcs12/p12_decr.c:93:
140020021810496:error:0907B00D:PEM routines:PEM_read_bio_PrivateKey:ASN1 lib:../crypto/pem/pem_pkey.c:88:
->  niklasca sudo openssl rsa -in pki/private/niklas-public.nvs.lan.key -out pki/private/niklas-public.nvs.lan.key
Enter pass phrase for pki/private/niklas-public.nvs.lan.key:
writing RSA key
->  niklasca ls
easyrsa  openssl-easyrsa.cnf  pki  vars  x509-types
```

### Moving CRT File & Key File to their respective folders
Now we move the certificate and its keyfile to the respective folders. 
`/etc/ssl/certs` is used to store certificates for Websites and `/etc/ssl/private/` is non-readable folder for normal users where the private key, which verifies our signature, is stored.

```Bash
->  niklasca sudo mv pki/issued/niklas-public.nvs.lan.crt /etc/ssl/certs
->  niklasca sudo mv pki/private/niklas-public.nvs.lan.key /etc/ssl/private
```

### Adjusting the config file
To use the newly created ceritifcates, we need to modify our Virtual Host file to include four new options: 

- `<VirtualHost *:443>` We changed the port from the HTTP Port, which is 80, to the HTTPS Port we need to operate on, which is 443.

- `SSLEngine On` tells the Apache Webserver that we want to use a SSL Certificate.

- `SSLCertificateFile` and the appropriate tell the webserver, where the certificate file for the virtual host is located. 

- `SSLCertificateKeyFile` we define the path where Apace can find the respective keyfile that is needed to verify the certificate.

```XML
<VirtualHost *:443>
        ServerName niklas-public.nvs.lan
        ServerAdmin webmaster@doesntgoanywhere.com
        DocumentRoot /var/www/public
        <Directory /var/www/public>
                Options Indexes FollowSymLinks MultiViews
                AllowOverride None
                Require all granted
        </Directory>
        SSLEngine On
        SSLCertificateFile /etc/ssl/certs/niklas-public.nvs.lan.crt
        SSLCertificateKeyFile /etc/ssl/private/niklas-public.nvs.lan.key
        ErrorLog /var/log/apache2/error.log
        LogLevel warn
        CustomLog /var/log/apache2/access.log combined
        ServerSignature On
</VirtualHost>
```

### Importing the certificate authority
Since we are not known certificate authority, we need to import our certification authority into the web browser. Firefox was used for this purpose since it uses its own, from the OS independent certificate store.

![Importing the CA Authority](Pasted image 20211117162249.png)
### Validating the connection
After navigating to the web page, we see by the lock and the accompanying message `Verbindung ist sicher`, that our certificate was verified successfully with our certificate authority that we import earlier.

![Validating the connection](Pasted image 20211117163518.png)

# CGI
So far we've only used static websites where the content is pre-defined. To make websites more dynamic where content is not known before a operation happens, Apache introduced CGI, or Common Gateway Interface. Scripting Languages can hook into this interface to execute scripts when a certain URL is accessed.

## PHP
PHP is an ancronym for `PHP: Hypertext Preprocessor`. It is used on many websites, often in the form of Wordpress. It is the most popular CGI Language in conjunction with Apache and other Web Servers.

### Installing PHP 
Installing PHP is easy. We don't need to any setup or enable modules, a simple `sudo apt install php` installs the PHP language, the Apache Modules and automatically enables them for us.

The message `apache2_invoke: Enable module php7.4` indicates, that the package manager enabled the PHP Module for us.
```bash
->  ~ sudo apt install php
[sudo] password for schueler:
Reading package lists... Done
Building dependency tree
Reading state information... Done
The following additional packages will be installed:
  libapache2-mod-php7.4 libsodium23 php-common php7.4 php7.4-cli
  php7.4-common php7.4-json php7.4-opcache php7.4-readline
Suggested packages:
  php-pear
The following NEW packages will be installed:
  libapache2-mod-php7.4 libsodium23 php php-common php7.4
  php7.4-cli php7.4-common php7.4-json php7.4-opcache
  php7.4-readline
0 upgraded, 10 newly installed, 0 to remove and 38 not upgraded.
Need to get 4169 kB of archives.
After this operation, 18.4 MB of additional disk space will be used.
Do you want to continue? [Y/n] y
Get:1 http://nova.clouds.archive.ubuntu.com/ubuntu focal/main amd64 libsodium23 amd64 1.0.18-1 [150 kB]
Get:2 http://nova.clouds.archive.ubuntu.com/ubuntu focal/main amd64 php-common all 2:75 [11.9 kB]
Get:3 http://nova.clouds.archive.ubuntu.com/ubuntu focal-updates/main amd64 php7.4-common amd64 7.4.3-4ubuntu2.7 [980 kB]
Selecting previously unselected package php7.4-opcache.
Preparing to unpack .../4-php7.4-opcache_7.4.3-4ubuntu2.7_amd64.deb ...
Unpacking php7.4-opcache (7.4.3-4ubuntu2.7) ...
Selecting previously unselected package php7.4-readline.
Preparing to unpack .../5-php7.4-readline_7.4.3-4ubuntu2.7_amd64.deb ...
Unpacking php7.4-readline (7.4.3-4ubuntu2.7) ...
Selecting previously unselected package php7.4-cli.
Preparing to unpack .../6-php7.4-cli_7.4.3-4ubuntu2.7_amd64.deb ...
Unpacking php7.4-cli (7.4.3-4ubuntu2.7) ...
Selecting previously unselected package libapache2-mod-php7.4.
Preparing to unpack .../7-libapache2-mod-php7.4_7.4.3-4ubuntu2.7_amd64.deb ...
Unpacking libapache2-mod-php7.4 (7.4.3-4ubuntu2.7) ...
Selecting previously unselected package php7.4.
Preparing to unpack .../8-php7.4_7.4.3-4ubuntu2.7_all.deb ...
Unpacking php7.4 (7.4.3-4ubuntu2.7) ...
Setting up libapache2-mod-php7.4 (7.4.3-4ubuntu2.7) ...

Creating config file /etc/php/7.4/apache2/php.ini with new version
Module mpm_event disabled.
Enabling module mpm_prefork.
apache2_switch_mpm Switch to prefork
apache2_invoke: Enable module php7.4
Setting up php7.4 (7.4.3-4ubuntu2.7) ...
Setting up php (2:7.4+75) ...
Processing triggers for man-db (2.9.1-1) ...
Processing triggers for libc-bin (2.31-0ubuntu9.2) ...
Processing triggers for php7.4-cli (7.4.3-4ubuntu2.7) ...
Processing triggers for libapache2-mod-php7.4 (7.4.3-4ubuntu2.7) ...
```

### Testing the PHP Script
To test, if the PHP Interpreter and Webserver are working correctly, we can print some version and debug information to a webpage with the `phpinfo()` command. It will print out a slew of debug and version information which can be used to verify if PHP is working correctly.

Creating the file in our public directory: 
```bash
root@u2004-5bhif-6:/var/www/public# echo "<?php phpinfo(); ?>" > info.php
```

Testing the file in a web browser:

![Testing the PHP Script](Pasted image 20211124134929.png)

## Python
To demonstrate that every language can be used to execute scripts on a web-page, we used Python in this second example.

The following tutorial was used as a guidance to set everything up:
[Tutorial - Python CGI auf Apache Schritt für Schritt](https://techexpert.tips/de/apache-de/python-cgi-auf-apache/)

### Installing Python and required dependencies
We use our package manager to install Python and the PIP Python Package manager.
```bash
root@u2004-5bhif-6:/var/www/public# apt install python3 python3-pip
Reading package lists... Done
Building dependency tree
Reading state information... Done
python3 is already the newest version (3.8.2-0ubuntu2).
python3 set to manually installed.
The following additional packages will be installed:
  binutils binutils-common binutils-x86-64-linux-gnu
  build-essential cpp cpp-9 dpkg-dev fakeroot g++ g++-9 gcc gcc-9
  gcc-9-base libalgorithm-diff-perl libalgorithm-diff-xs-perl
  libalgorithm-merge-perl libasan5 libatomic1 libbinutils
  libc-dev-bin libc6-dev libcc1-0 libcrypt-dev libctf-nobfd0
  libctf0 libdpkg-perl libexpat1-dev libfakeroot
  libfile-fcntllock-perl libgcc-9-dev libisl22 libitm1 liblsan0
  libmpc3 libpython3-dev libpython3.8 libpython3.8-dev
  libpython3.8-minimal libpython3.8-stdlib libquadmath0
  libstdc++-9-dev libtsan0 libubsan1 linux-libc-dev make
  manpages-dev python-pip-whl python3-dev python3-wheel python3.8
  python3.8-dev python3.8-minimal zlib1g-dev
Suggested packages:
  binutils-doc cpp-doc gcc-9-locales debian-keyring g++-multilib
  g++-9-multilib gcc-9-doc gcc-multilib autoconf automake libtool
  flex bison gdb gcc-doc gcc-9-multilib glibc-doc bzr
  libstdc++-9-doc make-doc python3.8-venv python3.8-doc
  binfmt-support
The following NEW packages will be installed:
  binutils binutils-common binutils-x86-64-linux-gnu
  build-essential cpp cpp-9 dpkg-dev fakeroot g++ g++-9 gcc gcc-9
  gcc-9-base libalgorithm-diff-perl libalgorithm-diff-xs-perl
  libalgorithm-merge-perl libasan5 libatomic1 libbinutils
  libc-dev-bin libc6-dev libcc1-0 libcrypt-dev libctf-nobfd0
  libctf0 libdpkg-perl libexpat1-dev libfakeroot
  libfile-fcntllock-perl libgcc-9-dev libisl22 libitm1 liblsan0
  libmpc3 libpython3-dev libpython3.8-dev libquadmath0
  libstdc++-9-dev libtsan0 libubsan1 linux-libc-dev make
  manpages-dev python-pip-whl python3-dev python3-pip
  python3-wheel python3.8-dev zlib1g-dev
The following packages will be upgraded:
  libpython3.8 libpython3.8-minimal libpython3.8-stdlib python3.8
  python3.8-minimal
5 upgraded, 49 newly installed, 0 to remove and 33 not upgraded.
Need to get 56.0 MB of archives.
After this operation, 214 MB of additional disk space will be used.Do you want to continue? [Y/n] y
Get:1 http://nova.clouds.archive.ubuntu.com/ubuntu focal-updates/main amd64 python3.8 amd64 3.8.10-0ubuntu1~20.04.1 [387 kB]
Get:2 http://nova.clouds.archive.ubuntu.com/ubuntu focal-updates/main amd64 libpython3.8 amd64 3.8.10-0ubuntu1~20.04.1 [1625 kB]
Get:3 http://nova.clouds.archive.ubuntu.com/ubuntu focal-updates/main amd64 libpython3.8-stdlib amd64 3.8.10-0ubuntu1~20.04.1 [1674 kB]
Get:4 http://nova.clouds.archive.ubuntu.com/ubuntu focal-updates/main amd64 python3.8-minimal amd64 3.8.10-0ubuntu1~20.04.1 [1900 kB]
Get:5 http://nova.clouds.archive.ubuntu.com/ubuntu focal-updates/main amd64 libpython3.8-minimal amd64 3.8.10-0ubuntu1~20.04.1 [717 kB]
Get:6 http://nova.clouds.archive.ubuntu.com/ubuntu focal-updates/main amd64 binutils-common amd64 2.34-6ubuntu1.3 [207 kB]
Get:7 http://nova.clouds.archive.ubuntu.com/ubuntu focal-updates/main amd64 libbinutils amd64 2.34-6ubuntu1.3 [474 kB]
Get:8 http://nova.clouds.archive.ubuntu.com/ubuntu focal-updates/main amd64 libctf-nobfd0 amd64 2.34-6ubuntu1.3 [47.4 kB]
Get:9 http://nova.clouds.archive.ubuntu.com/ubuntu focal-updates/main amd64 libctf0 amd64 2.34-6ubuntu1.3 [46.6 kB]
Get:10 http://nova.clouds.archive.ubuntu.com/ubuntu focal-updates/main amd64 binutils-x86-64-linux-gnu amd64 2.34-6ubuntu1.3 [1613 kB]Get:11 http://nova.clouds.archive.ubuntu.com/ubuntu focal-updates/main amd64 binutils amd64 2.34-6ubuntu1.3 [3380 B]
Get:12 http://nova.clouds.archive.ubuntu.com/ubuntu focal-updates/main amd64 libc-dev-bin amd64 2.31-0ubuntu9.2 [71.8 kB]
Get:13 http://nova.clouds.archive.ubuntu.com/ubuntu focal-updates/main amd64 linux-libc-dev amd64 5.4.0-90.101 [1123 kB]
Get:14 http://nova.clouds.archive.ubuntu.com/ubuntu focal/main amd64 libcrypt-dev amd64 1:4.4.10-10ubuntu4 [104 kB]
Get:15 http://nova.clouds.archive.ubuntu.com/ubuntu focal-updates/main amd64 libc6-dev amd64 2.31-0ubuntu9.2 [2520 kB]
Get:16 http://nova.clouds.archive.ubuntu.com/ubuntu focal-updates/main amd64 gcc-9-base amd64 9.3.0-17ubuntu1~20.04 [19.1 kB]
Get:17 http://nova.clouds.archive.ubuntu.com/ubuntu focal/main amd64 libisl22 amd64 0.22.1-1 [592 kB]
Get:18 http://nova.clouds.archive.ubuntu.com/ubuntu focal/main amd64 libmpc3 amd64 1.1.0-1 [40.8 kB]
[...]
```

### Enabling the required modules
To use CGI Scripts, we first need to enable the module with `a2enmod` and afterwards restart the webserver:
```bash
root@u2004-5bhif-6:/var/www/public# a2enmod cgid
Enabling module cgid.
To activate the new configuration, you need to run:
  systemctl restart apache2
root@u2004-5bhif-6:/var/www/public# systemctl restart apache2
```

### Creating the script
Our script uses `art`, which is package that can print out strings in various forms of ASCII Art. We install it with the help op PIP:
```Bash
root@u2004-5bhif-6:/var/www/public# pip3 install art
Collecting art
  Downloading art-5.3-py2.py3-none-any.whl (574 kB)
     574 kB 2.0 MB/s
Installing collected packages: art
Successfully installed art-5.3

```

CGI Scripts are located in the `/usr/lib/cgi-bin/` folder, so we navigate there:
```
root@u2004-5bhif-6:/var/www/public# cd /usr/lib/cgi-bin/
```

We create the following script: 

- Firstly, we create an Object with the Help of text2art, which is included in `art`, a package which we installed earlier.

- We set the content type to be outputted by apache to the Plain format since we don't output any HTML or JSON. 

- Then we print out, firstly a test message with regular styling and then our ASCII-Art Message. 

```Python
#!/usr/bin/python3
from art import *
Art=text2art("HAIDEN",font='block',chr_ignore=True)
print('Content-Type: text/plain')
print('')
print('This is my test!')
print(Art)
```

Adjusting the permissions so that apache can access the script correctly:
```Bash
chmod 755 /usr/lib/cgi-bin/serveArt.py
```

### Testing our script
After navigating to the web page and calling the script, we get the desired output:

![CGI](Pasted image 20211124141757.png)
