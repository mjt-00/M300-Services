M300 - K3
============

**Bestehenden Docker-Dontainer kombinieren & Bestehende Container als Backend, Desktop-App als Frontend  einsetzen**

Hier geht es darum Docker Container zu kombinieren beziehungsweise einen
Bakcend, und Frontend einzusetzen. Die Desktop-App die bei uns als Frontend
eingesetzt wurde, war OSTicket. Im Hintergrund dazu haben wir eine SQL, die die
ganzen Daten dazu speichert und aufnimmt.

Wie wir dies genau gemacht haben hier im Anschluss:

Als erstes musste MySQL installiert werden, dazu gehört auch Passwort etc.
mitzugeben:

    docker run --name osticket_mysql -d -e MYSQL_ROOT_PASSWORD=secret -e
    MYSQL_USER=osticket -e MYSQL_PASSWORD=secret -e MYSQL_DATABASE=osticket mysql:5

Anschliessend logischerweise noch OSTicket, welches an die Datenbank angehängt
und verknüpft wird:

    docker run --name osticket -d --link osticket_mysql:mysql -p 8080:80
    campbellsoftwaresolutions/osticket
    
**Volumes zur persistenten Datenablage eingerichte**

Kommen wir zum sogenannten Volume. Hier geht es darum, die Volumes also die
Pfade abzuändern, daher wollen wir beispielsweise das ganze bei uns Lokal
abspeichern. Leider hatten wir Probleme (wir haben dies auch mit Herrn Bernet
angeschaut). Es ist weder bei Git Bash weder noch bei Powreshell gegangen. Hier
aber dennoch den Befehl dafür:

    docker run --name osticket_mysql -d -e MYSQL_ROOT_PASSWORD=secret -e
    MYSQL_USER=osticket -e MYSQL_PASSWORD=secret -e MYSQL_DATABASE=osticket mysql:5
    -v C:\\DOCKER\\container\\mysql:/var/lib/mysql

Was damit gewollt ist, die ganzen SQL Dateien im C:\\Docker\\container\\mysql
abzuspeichern.

**Docker spezifischen Befehle**

| Befehl         | Beschreibung                                    |
| -------------- | ----------------------------------------------- |
| `docker run`   | Führt einen Befehl in einem neuen Container aus |
| `docker start` | Startet einen oder mehrere Container            |
| `docker stop`  | Stoppt einen oder mehrere Container             |
| `docker build` | Baut eine Image aus dem Dockerfile              |
| `docker pull`  | Lädt Image aus einer Repository herunter        |
| `docker push`  | Lädt Image in eine Repository hoch              |

