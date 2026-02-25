# Wissensdatenbank: Netzwerksicherheit & SSH-Zugriff

## 1. Firewall und Reverse Proxy

Sicherheit in verteilten Systemen wird durch verschiedene Schichten gewährleistet, die den Zugriff kontrollieren und die interne Struktur verbergen.

* **Web Server vs. Reverse Proxy**:
* **Web Server**: Liefert Inhalte wie Webseiten oder Files direkt an den Client aus.
* **Reverse Proxy**: Agiert als Schutzschild vor dem Server. Er übernimmt das **Load Balancing** (Lastverteilung) und verbirgt die interne Infrastruktur vor direkten Zugriffen aus dem Internet.


* **Sicherheitskonzepte**:
* **White List**: Ein restriktives Konzept, bei dem standardmässig jeder Zugriff verboten ist. Nur explizit freigegebene Adressen oder Programme dürfen kommunizieren.
* **Zentrale Filterung**: Als Alternative zur Firewall auf jedem einzelnen Server können zentrale **Gateways** oder **Security Groups** auf Cloud-Ebene genutzt werden, um den Traffic bereits vor dem Server zu filtern.



## 2. SSH (Secure Shell)

SSH ist der Standard für die sichere Fernwartung von Linux-Servern. Die Sicherheit basiert auf der asymmetrischen Verschlüsselung.

### Key-Management

| Datei | Funktion | Aufbewahrungsort |
| --- | --- | --- |
| `id_rsa` | **Privater Schlüssel**: Muss absolut geheim bleiben. | Lokal auf dem Client-PC. |
| `id_rsa.pub` | **Öffentlicher Schlüssel**: Kann bedenkenlos geteilt werden. | Wird auf dem Zielserver hinterlegt. |

### Wichtige Konfigurationsdateien

* **`authorized_keys`**: Diese Datei auf dem Zielserver speichert die öffentlichen Schlüssel (`.pub`). Sie erlaubt berechtigten Usern den Login ohne Passwort.
* **`known_hosts`**: Speichert die Fingerprints (Identitäten) besuchter Server. Dies verhindert **Man-in-the-Middle-Angriffe**, da bei einer Änderung des Schlüssels sofort eine Warnmeldung erscheint.

### Sicherheitshinweis zu SSH-Tunneln

Ein SSH-Tunnel darf **nicht** zur Umgehung von Firmen-Sicherheitsrichtlinien (**Firewall-Bypassing**) verwendet werden. Ebenso ist der Einsatz kritisch in Umgebungen, in denen verschlüsselter Traffic zur Malware-Prüfung kontrolliert werden muss, da der Tunnel diese Kontrollen umgeht.

