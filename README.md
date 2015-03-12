====================================================================================
mini-dinstall - Apache with basic auth
====================================================================================

* Install mini-dinstall

```
apt-get install mini-dinstall
```


* Add special user

```
adduser --quiet --system --group --disabled-password --shell /bin/bash --gecos "APT Repository" apt-repo
```

* Create directory for the reository

```
mkdir -p ~apt-repo/public_html/apt/mini-dinstall/incoming
```

* Set the correct apache Vhost ServerName for the site

* Copy all the files to thier destinations

```
cp mini-dinstall.conf ~apt-repo/.mini-dinstall.conf
cp htgroup ~apt-repo/.htgroup
cp sign_release.sh ~apt-repo/
cp apt.conf /etc/apache2/sites-available/
```

* Create the password file using htpasswd utility

```
htpasswd -c ~apt-repo/.htpasswd admin
```

* Make sure file ownership are correct

```
chown -R apt-repo:apt-repo ~apt-repo/
```

* enable the site and restart apache

```
a2ensite apt.conf
service apache2 restart
```

* Create a pgp key pair to sign the Release files, or comment out the `release_signscript` in `.mini-dinstall.conf`

```

```

* Add a line in your sources.list

```
deb http://user:password@apt.example.com stable/
```

* add your ssh key to `~apt-repo/.ssh/authorized_keys`
* modify and save dput.cf on your local machine as ~/.dput.cf
