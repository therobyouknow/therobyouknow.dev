sudo apt install python-is-python3

on remote server.


https://askubuntu.com/questions/1296790/python-is-python3-package-in-ubuntu-20-04-what-is-it-and-what-does-it-actually


setup venv

https://stackoverflow.com/a/77815354/227926

cd <base/top level/root>

python -m venv .

<pre>
robdavisprojects@DesktopMedionUbuntu:~/02-work/10-myprojects/therobyouknow.dev$ python -m venv .
The virtual environment was not created successfully because ensurepip is not
available.  On Debian/Ubuntu systems, you need to install the python3-venv
package using the following command.

    apt install python3.12-venv

You may need to use sudo with that command.  After installing the python3-venv
package, recreate your virtual environment.

Failing command: /home/robdavisprojects/02-work/10-myprojects/therobyouknow.dev/bin/python
</pre>

Not doing that, dont use a specific version, get the latest available (for the platform)

sudo apt-get install python3-venv 


python -m venv .venv


(now it worked)

(you need to give it a folder e.g. .venv for it to put all its stuff in there. doing `.` was a mistake as it will put all its stuff bin etc... in the top level)
(as per https://stackoverflow.com/a/77815354/227926)

(hereafter I will not need to do the above now that this is in source code)
(just do the following)

(don't do this)
cd bin 
source activate

do this:
source .venv/bin/activate

(as per https://stackoverflow.com/a/77815354/227926)


going to edit /etc/hosts to add a local domain to point at locally running django site
going to edit /etc/apache2 vhosts to map local domain to location of django site

local domain


(I've disabled my .gitignore from github because I want all the stuff in .venv so I can replay it elsewhere)


next get pip (if not pip already)

https://pip.pypa.io/en/latest/installation/#ensurepip


https://stackoverflow.com/a/49946281/227926

python -m pip --version

python -m ensurepip --upgrade




https://askubuntu.com/questions/25374/how-do-you-install-mod-wsgi


pip vs apt install fr mod_wsgi?

https://stackoverflow.com/questions/30674644/installing-mod-wsgi-for-python3-on-ubuntu

seems like pip is better. will it work - does it need to be "closer" to apache? can it be installed inside .venv ?

or not?

https://stackoverflow.com/a/74499485/227926

sudo apt install apache2-dev

for wsgi i did this way:

robdavisprojects@DesktopMedionUbuntu:~$ sudo apt-get install libapache2-mod-wsgi-py3
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
The following package was automatically installed and is no longer required:
  mailcap
Use 'sudo apt autoremove' to remove it.
The following NEW packages will be installed
  libapache2-mod-wsgi-py3
0 to upgrade, 1 to newly install, 0 to remove and 56 not to upgrade.
Need to get 103 kB of archives.
After this operation, 300 kB of additional disk space will be used.
Get:1 http://gb.archive.ubuntu.com/ubuntu noble/main amd64 libapache2-mod-wsgi-py3 amd64 5.0.0-1build2 [103 kB]
Fetched 103 kB in 0s (3,004 kB/s)                 
Selecting previously unselected package libapache2-mod-wsgi-py3.
(Reading database ... 244454 files and directories currently installed.)
Preparing to unpack .../libapache2-mod-wsgi-py3_5.0.0-1build2_amd64.deb ...
Unpacking libapache2-mod-wsgi-py3 (5.0.0-1build2) ...
Setting up libapache2-mod-wsgi-py3 (5.0.0-1build2) ...
apache2_invoke: Enable module wsgi

https://stackoverflow.com/a/68151482/227926



(.venv) robdavisprojects@DesktopMedionUbuntu:~/02-work/10-myprojects/therobyouknow.dev$ python -m pip install Django
Collecting Django
  Downloading django-5.2.5-py3-none-any.whl.metadata (4.1 kB)
Collecting asgiref>=3.8.1 (from Django)
  Downloading asgiref-3.9.1-py3-none-any.whl.metadata (9.3 kB)
Collecting sqlparse>=0.3.1 (from Django)
  Downloading sqlparse-0.5.3-py3-none-any.whl.metadata (3.9 kB)
Downloading django-5.2.5-py3-none-any.whl (8.3 MB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 8.3/8.3 MB 18.6 MB/s eta 0:00:00
Downloading asgiref-3.9.1-py3-none-any.whl (23 kB)
Downloading sqlparse-0.5.3-py3-none-any.whl (44 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 44.4/44.4 kB 4.3 MB/s eta 0:00:00
Installing collected packages: sqlparse, asgiref, Django
Successfully installed Django-5.2.5 asgiref-3.9.1 sqlparse-0.5.3
(.venv) robdavisprojects@DesktopMedionUbuntu:~/02-work/10-myprojects/therobyouknow.dev$ 



database:
sudo apt install mariadb-client-core  

mysql
ERROR 2002 (HY000): Can't connect to local server through socket '/run/mysqld/mysqld.sock' (2)
(did I need this, then? if I'm installing mariadb-server below)

https://www.digitalocean.com/community/tutorials/how-to-install-mariadb-on-ubuntu-20-04
sudo apt update
sudo apt install mariadb-server
sudo mysql_secure_installation



(.venv) robdavisprojects@DesktopMedionUbuntu:~/02-work/10-myprojects/therobyouknow.dev$ sudo mysql_secure_installation

NOTE: RUNNING ALL PARTS OF THIS SCRIPT IS RECOMMENDED FOR ALL MariaDB
      SERVERS IN PRODUCTION USE!  PLEASE READ EACH STEP CAREFULLY!

In order to log into MariaDB to secure it, we'll need the current
password for the root user. If you've just installed MariaDB, and
haven't set the root password yet, you should just press enter here.

Enter current password for root (enter for none): 
OK, successfully used password, moving on...

Setting the root password or using the unix_socket ensures that nobody
can log into the MariaDB root user without the proper authorisation.

You already have your root account protected, so you can safely answer 'n'.

Switch to unix_socket authentication [Y/n] n
 ... skipping.

You already have your root account protected, so you can safely answer 'n'.

Change the root password? [Y/n] n
 ... skipping.

By default, a MariaDB installation has an anonymous user, allowing anyone
to log into MariaDB without having to have a user account created for
them.  This is intended only for testing, and to make the installation
go a bit smoother.  You should remove them before moving into a
production environment.

Remove anonymous users? [Y/n] Y
 ... Success!

Normally, root should only be allowed to connect from 'localhost'.  This
ensures that someone cannot guess at the root password from the network.

Disallow root login remotely? [Y/n] Y
 ... Success!

By default, MariaDB comes with a database named 'test' that anyone can
access.  This is also intended only for testing, and should be removed
before moving into a production environment.

Remove test database and access to it? [Y/n] Y
 - Dropping test database...
 ... Success!
 - Removing privileges on test database...
 ... Success!

Reloading the privilege tables will ensure that all changes made so far
will take effect immediately.

Reload privilege tables now? [Y/n] Y
 ... Success!

Cleaning up...

All done!  If you've completed all of the above steps, your MariaDB
installation should now be secure.

Thanks for using MariaDB!


(.venv) robdavisprojects@DesktopMedionUbuntu:~/02-work/10-myprojects/therobyouknow.dev$ sudo su
root@DesktopMedionUbuntu:/home/robdavisprojects/02-work/10-myprojects/therobyouknow.dev# mysql -uroot -p
Enter password: 
Welcome to the MariaDB monitor.  Commands end with ; or \g.
Your MariaDB connection id is 47
Server version: 10.11.13-MariaDB-0ubuntu0.24.04.1 Ubuntu 24.04

Copyright (c) 2000, 2018, Oracle, MariaDB Corporation Ab and others.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

MariaDB [(none)]> 



things to consider

Setting up https locally
https://medium.com/dajngo/how-to-run-a-local-django-development-server-over-https-with-a-trusted-self-signed-ssl-certificate-1cca45800d58

(trying to find the ddev equivalents for python)


ServerName - real live domain name
https://stackoverflow.com/questions/64429412/apache-mod-wsgi-any-url-is-served-by-project-servername-is-ignored


How to persist a .venv environment on a production server
https://stackoverflow.com/questions/14063692/how-to-keep-virtualenv-always-on-in-production

also:
https://stackoverflow.com/questions/23257123/where-should-virtualenvs-go-in-production
https://serverfault.com/questions/733725/how-should-virtualenv-be-set-up-in-a-production-web-server-user-location-etc

