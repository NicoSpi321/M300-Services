# Wissensdatenbank: Monitoring, Security & Continuous Integration

## 1. Protokollieren & Überwachen

Das Monitoring ist entscheidend, um die Verfügbarkeit von Diensten sicherzustellen und Fehler frühzeitig zu beheben.

* **Warum überwachen?**: Erkennung von Performance-Engpässen, Ressourcenbelastungen und Fehlern zur Garantie der Dienst-Verfügbarkeit.
* **Das Syslog**: Das zentrale Protokollierungssystem eines Linux-Hosts; zu finden unter `/var/log` (z. B. `/var/log/syslog`).
* **Datenkanäle**:
* `stdin`: Standard-Eingabe (Datenfluss in das Programm).
* `stdout`: Standard-Ausgabe (normale Programmausgaben).
* `stderr`: Standard-Fehlerausgabe (spezieller Kanal für Fehlermeldungen).



## 2. Container sichern & beschränken

Container teilen sich den Kernel des Hosts, weshalb Sicherheitsmassnahmen und Ressourcen-Limits zwingend erforderlich sind.

* **Daemon-Schutz**: Um gefährliche Befehle wie `docker run -v /:/homeroot` (Mounten des Root-Verzeichnisses) durch normale User zu verhindern, darf der Zugriff auf den Docker-Daemon nur für `root` oder die Gruppe `docker` erlaubt sein.
* **Mandantentrennung**: Die sicherste Trennung zwischen verschiedenen Kunden (Mandanten) erfolgt über separate **Virtuelle Maschinen (VMs)**, da diese durch einen eigenen Kernel stärker isoliert sind als Container.
* **Ressourcen-Limits**: Der Verbrauch kann in Docker durch Flags wie `--memory` oder `--cpus` (Resource Constraints) eingeschränkt werden, um zu verhindern, dass ein einzelner Container den ganzen Host lahmlegt.

## 3. Kontinuierliche Integration (CI)

Automatisierung ist der Schlüssel zur effizienten Softwareverteilung.

* **Jenkins**: Übernimmt die Automatisierung von Software-Builds, führt Modultests (Unit-Tests) aus und überwacht Logfiles oder Batch-Jobs.
* **Modultests**: Test-Skripte (z. B. in Bash oder Python), die automatisiert prüfen, ob Funktionen das erwartete Ergebnis liefern.
* **Job-Trigger**: Neben manuellen oder zeitgesteuerten Starts können Jenkins-Jobs professionell über **Webhooks** (ausgelöst durch einen `git push`) oder durch Abhängigkeiten von anderen erfolgreichen Jobs gestartet werden.

