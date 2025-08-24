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


(I've disabled my .gitignore from github because I want all the stuff in .venv so I can replay it elsewhere)

consider

https://medium.com/dajngo/how-to-run-a-local-django-development-server-over-https-with-a-trusted-self-signed-ssl-certificate-1cca45800d58
