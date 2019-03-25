***Sicherheitsaspekte sind implementiert***
***
**Firewall eingerichtet inkl. Rules**

Bei der Firewall haben wir folgende Sachen eingerichtet:

>   sudo apt-get install ufw

>   sudo ufw allow 1234/tcp

>   sudo ufw allow 22/tcp

>   sudo ufw allow out 22/tcp

>   sudo ufw enable

Diese Konfigs heissen nichts Anderes, als die uncomplicated Firewall zu
installieren. Die oben genannten Ports zu öffnen und die Firewall auch noch zu
enablen bzw. zu aktivieren.

**Reverse Proxy ist eingerichtet**

>   sudo apt-get -y install libapache2-mod-proxy-html

>   sudo apt-get -y install libxml2-dev

>   sudo a2enmod proxy

>   sudo a2enmod proxy_html

>   sudo a2enmod proxy_http

Zuerst werden also die Module installiert und im Anschluss die Module an sich
noch aktiviert. (Die Installation alleine würde nämlich noch nicht viel bringen.

**Benutzer- und Rechtevergabe ist eingerichtet**

>   sudo groupadd admin

>   sudo useradd user01 -g admin -m -s /bin/bash

>   sudo useradd user02 -g admin -m -s /bin/bash

>   sudo chpasswd \<\<\<user01:1234

>   sudo chpasswd \<\<\<user02:1234

Hier sieht man die Konfigs für die Erstellung von Usern und Gruppen.

Die Befehle sind relativ selbsterklärend. Unten werden die Passwörter der beiden
User (User01 und User02) auf «1234» gesetzt. Zuvor müssen logischerweise die
User erstellt werden.

Mit groupadd wird die angegebene Gruppe an allen nötigen Stellen in den
System-Dateien eingefügt.

**Zugang mit SSH-Tunnel abgesichert**

udo apt-get -y install unzip

>   wget https://bin.equinox.io/c/4VmDzA7iaHb/ngrok-stable-linux-amd64.zip

>   unzip ngrok-stable-linux-amd64.zip

>   ./ngrok authtoken znJsMkTvBtmru1d1zvRf_4indT3cjMiW4nj7Vda32G

>   ./ngrok http 1234

Hier wird zuerst das Unzip Modul installiert, sowie auch Ngrok. Ngrok ist dafür
da um sichere SSH-Tunnels zu erstellen.

Hier wird noch die Einstellung mitgegeben HTTP auf Port 1234
umzustellen/weiterzuleiten.
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

