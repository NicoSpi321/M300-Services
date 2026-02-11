Deployment-Prozess und Systemvalidierung
1. Initialisierung der Umgebung
Zuerst wurde lokal die Verzeichnisstruktur m300-arbeit/erste-vm erstellt. Die Bereitstellung der virtuellen Infrastruktur erfolgte anschliessend über die Kommandozeile mittels folgender Schritte:

![Vagrantfile](M300-10-1.png)

Vorbereitung: Durch vagrant init ubuntu/xenial64 wurde das offizielle Ubuntu-Image als Basis definiert und die Konfigurationsdatei (Vagrantfile) angelegt.

Provisionierung: Der Befehl vagrant up startete den automatisierten Download und die Einrichtung der Instanz in VirtualBox.

Interaktion: Mit vagrant ssh wurde der direkte Zugriff auf die Linux-Shell der VM realisiert.

2. Visuelle und technische Kontrolle
Ein Abgleich mit der VirtualBox-GUI bestatigte, dass die VM korrekt registriert wurde und ohne Fehlermeldungen lauft.

![VirtualBox](M300-10-3.png)

Um sicherzustellen, dass die virtuelle Hardware den Erwartungen entspricht, wurden nach dem Verbindungsaufbau die Systemressourcen intern geprüft:

Dateisystem: Überprüfung der Mount-Points und Kapazitaten mit df -h.

Arbeitsspeicher: Validierung des zugewiesenen RAMs mittels free -m.

3. Automatisierung und Web-Service
Um den Webserver nicht manuell installieren zu müssen, wurde das Vagrantfile angepasst. Ein integriertes Shell-Skript übernimmt nun die automatische Installation und Konfiguration der Dienste beim Systemstart.

4. Abschliessende Verifizierung
Die Erfolgskontrolle belegt die korrekte Funktion der gesamten Kette: Nach dem Start der VM ist der Apache-Webserver über ein Port-Forwarding auf dem Host-Rechner unter http://localhost:8080 erreichbar. Dies bestatigt sowohl die erfolgreiche Provisionierung als auch die Netzwerk-Konfiguration.

![Webserver](M300-10-2.png)