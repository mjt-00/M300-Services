M300 - K3
============

**Bestehende VM aus Vagrant-Cloud einrichten**
***

**Allgemeines**

*Was sind überhaupt diese Vagrant-Cloud Boxen?*

Boxen sind bei Vagrant vorkonfigurierte VMs (Vorlagen). Diese sollen den Prozess
der Softwareverteilung und der Entwicklung beschleunigen. Jede Box, die von dem
Nutzer benutzt wurde, wird auf dem Computer gespeichert und muss so nicht wieder
aus dem Internet geladen werden.

*Wie werden die Boxen hinzugefügt?*

Boxen können explizit durch den Befehl vagrant box add [box-name] oder vagrant
box add [box-url] heruntergeladen und durch vagrant box remove [box-name]
entfernt werden. Ein "box-name" ist dabei durch Konvention wie folgt aufgebaut:
Entwickler/Box (z.B. ubuntu/xenial64).

*Wie werden die Boxen installiert?*

Boxen können explizit durch den Befehl vagrant box add [box-name] oder vagrant
box add [box-url] heruntergeladen und durch vagrant box remove [box-name]
entfernt werden. Ein "box-name" ist dabei durch Konvention wie folgt aufgebaut:
Entwickler/Box (z.B. ubuntu/xenial64).

***

**Box hinzufügen**

Die Vagrant-Boxen können unter folgendem Link heruntergeladen werden: 
https://app.vagrantup.com/boxes/search (dies sind bereits fertige Boxen die mit Vagrant eingepflegt werden können. 

Hinzufügen einer Box zur lokalen Registry:

    $ vagrant box add [box-name]

In der lokalen Registry vorhandene Boxen anzeigen:

    $ vagrant box list

**VM erstellen**

Vagrantfile Erzeugen und Provisionierung starten:

    $ mkdir myserver   

    $ cd myserver

    $ vagrant init ubuntu/xenial64

    $ vagrant up

Aktueller Status der VM anzeigen:

    $ vagrant status
    
**VM updaten** 
Nach Änderungen im Vagrantfile kann ein Server wie folgt aktualisiert werden:

    $ vagrant provision
 
**VM löschen** 
Die VM kann wie folgt gelöscht werden:

    $ vagrant destroy -f

***

**Eigene vorgefertigte VM**

Terminal (Bash) öffnen

In gewünschtem Verzeichnis einen neuen Ordner für die VM anlegen:

    $ cd Wohin\\auch\\immer

    $ mkdir MeineVagrantVM

    $ cd MeineVagrantVM

Vagrantfile erzeugen, VM erstellen und entsprechend starten: (die VM 's sind VM Boxen)

    $ vagrant box add http://10.1.66.11/vagrant/ubuntu/xenial64.box --name
      ubuntu/xenial64 \#Vagrant-Box vom Netzwerkshare hinzufügen

    $ vagrant init ubuntu/xenial64 \#Vagrantfile erzeugen

    $ vagrant up --provider virtualbox \#Virtuelle Maschine erstellen & starten
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

