# Blocky

##### 10.10.10.37
### Writeup by ![](https://www.hackthebox.eu/badge/image/2426)
## NMAP SCAN [intensive scan]

![nmap scan](images/nmap.png "NMAP Scan")

Lets visit the website.
![index.php](images/index.png "index.php")
After doing some basic enumeration (dirbuster, nikto, WPscan), we see that it is a Wordpress Website and a directory called /plugins. We also see that there is /phpmyadmin.
![/phpmyadmin](images/phpmyadmin.png "10.10.10.37/phpmyadmin")

![/plugins](images/plugins.png "10.10.10.37/plugins")


Let's download the BlockyCore.jar and extract it.
We see, theres a blockycore.class, which could get interesting.
And yes, it is indeed interesting. After running **strings** on it, we see something really juicy:

![strings](images/strings.png "strings blockycore.class")
This looks like the credentials for some database login stuff.

We should test if these are the credentials for **phpmyadmin**.
And yes, they are.

![awesome](http://i.memeful.com/media/post/ewYyqmw_700wa_0.gif)

Okay. Keep calm and pwn. Let's see what the wpusers database is about.

![notch](images/notch.png)
Who that could be.. Maybe the ssh user?!

![batman](http://i.memeful.com/media/post/4wbB3ow_700wa_0.gif)

After testing the password for SSH: we got in and successfully got the **user.txt**.

![ssh](images/ssh.png)

But don't stop. Glad i had a checklist for privilege escalation. (https://blog.g0tmi1k.com/2011/08/basic-linux-privilege-escalation/) After checking some stuff, **sudo -l**, we see that i can run every command as notch. So Why don't we just run **sudo -i** to get root?
And yes, we got it. 

![root](images/root.png)

Boom. got it. Awesome machine, great experience. 
