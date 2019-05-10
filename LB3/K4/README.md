***M300-Sicherheitsaspekte sind implementiert***
***

Um die Überwachung gewährleisten zu können, haben wir uns das Tool PRTG
heruntergeladen. Mit diesem ist es möglich die ganze Umgebung von Docker zu
überwachen und allenfalls auch per Benachrichtigung steuern zu lassen. Wir haben
logischerweise nur eine Testversion, das Produkt würde nach ein paar Monaten
etwas kosten.

Weitere drei Absicherungen für den Container zur zusätzlichen Sicherheit konnten
wir wie folgt integrieren:

Speicher begrenzen:

    docker run -m 128m --memory-swap 128m amouat/stress stress --vm 1 --vm-bytes
    127m -t 5s

CPU Einsatz:

    docker run -d --name load1 -c 2048 amouat/stress

    docker run -d --name load2 amouat/stress

    docker run -d --name load3 -c 512 amouat/stress

    docker run -d --name load4 -c 512 amouat/stress

    docker stats \$(docker inspect -f {{.Name}} \$(docker ps -q))

Neustarts begrenzen:

    docker run -d --restart=on-failure:10 my-flaky-image
