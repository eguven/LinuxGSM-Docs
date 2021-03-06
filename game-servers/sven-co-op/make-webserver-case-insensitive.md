---
description: Make LAMP webserver case insensitive with apache2 mod_speling
---

# Make Webserver Case Insensitive

Most community created files for Sven Co-op do not work with case sensitivity. LAMP servers are case sensitive. Enabling apache2 mod\_speling ignores case sensitivity on a LAMP stack. **This workaround will not work on shared webhosting** **where editing apache files is not available.** This guide applies to debian and ubuntu. Linked at bottom of page are external guides for Debian/Ubuntu/CentOS/Fedora.

 Enable mod\_speling

```text
a2enmod speling
```

 Restart apache

```text
service apache2 restart
```

Now apache needs to be told which directories mod\_speling is applied to, open the webserver's .conf file located inside /etc/apache2/sites-available/ and set AllowOverride to All.

 Example:

```text
<Directory /var/www/html/>
	Options Indexes FollowSymLinks
	AllowOverride All
	Require all granted
</Directory>
```

Now enter the command

```text
a2ensite name_of_.conf_file
```

 Move to /var/www/html/ or your chosen webserver directory and in a .htaccess file enter

```text
<IfModule mod_speling.c>
CheckSpelling On
CheckCaseOnly On
</IfModule>
```

 Test the configuration by creating a case sensitive file, i.e. TesT.txt, and see if it can be read in browser by typing test.txt, text.TXT, etc. If it works, you are finished.



[mod\_speling Documentation](%20https://httpd.apache.org/docs/2.4/mod/mod_speling.html)

Guides from other sources:

[Wikitechy mod\_speling Guide](https://www.wikitechy.com/tutorials/apache/how-to-use-the-mod-speling-apache-module)

[a2Hosting mod\_speling Guide](https://www.a2hosting.com/kb/developer-corner/apache-web-server/using-the-mod-speling-apache-module)

 

 

