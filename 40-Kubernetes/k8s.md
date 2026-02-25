# Dokumentation: Kubernetes Hands-on (Pod & Service Deployment)

## 1. Einleitung und Zielsetzung

In diesem Projekt wurde die Bereitstellung eines Apache-Webservers innerhalb eines Kubernetes-Clusters (K8s) realisiert.

* **Ziel**: Der Fokus lag auf dem Wechsel von der **imperativen Steuerung** (Einzelbefehle) zur **deklarativen Steuerung** (Infrastruktur via YAML-Dateien).
* **Kernkonzept**: Ein **Pod** beherbergt den Container, während ein **Service (LoadBalancer)** die Erreichbarkeit über das Netzwerk sicherstellt.

## 2. Infrastruktur und Vorbereitung

Die Umgebung wurde auf Basis des Projekts `lernkube` aufgebaut. Aufgrund der hohen Anforderungen der Container-Orchestrierung benötigt das System mindestens 16 GB RAM und 40 GB Speicherplatz.

* **Management**: Der Zugriff erfolgt entweder über die PowerShell (via `kubeps.bat`) oder direkt auf dem Master-Node (`master-01`).
* **Dashboard**: Für die visuelle Kontrolle wurde ein Dashboard-Token generiert, der als "Passwort" für die grafische Oberfläche dient.

## 3. Imperative Erstellung (CLI-Steuerung)

Um die grundlegende Funktionsweise zu verstehen, wurden die Ressourcen zuerst manuell über die Kommandozeile (`kubectl`) erzeugt.

Verwendete Befehle im Terminal:
`kubectl create namespace test`: Erstellung eines isolierten Bereichs (Namespace), um die Umgebung sauber zu halten.
`kubectl run apache --image=httpd --restart=Never -n test`: Startet einen einzelnen Apache-Pod ohne Deployment-Logik.
`kubectl expose pod/apache --type="LoadBalancer" --port 80 -n test`: Erstellt den Service und mappt Port 80 auf einen extern erreichbaren NodePort.

## 4. Deklarative Methode (Infrastructure as Code)

Der professionelle Ansatz in Kubernetes ist die Verwendung von YAML-Konfigurationen. Dies ermöglicht es, ganze Anwendungslandschaften versioniert abzuspeichern.

### Konfigurations-Logik

Die Verbindung zwischen dem Pod und dem Service wird über **Labels** und **Selectors** hergestellt. In den YAML-Dateien (`apache-pod.yaml` und `apache-service.yaml`) wurde definiert, dass der Service genau den Pod anspricht, der das Label `app.kubernetes.io/name: apache` trägt.

`kubectl apply -f ./apache-verzeichnis/ -n yaml`: Dieser Befehl fährt die gesamte Infrastruktur, die im Ordner definiert ist, mit einem Schlag hoch.

## 5. Verifizierung und Zugriff

Der Erfolg der Bereitstellung wurde durch die Abfrage der Service-Details geprüft. Da Kubernetes intern mit Cluster-IPs arbeitet, muss für den externen Zugriff der **NodePort** ermittelt werden.

Automatisierte URL-Ermittlung:
`kubectl get service -n yaml apache -o=jsonpath='{.spec.ports[0].nodePort}'`: Dieser Befehl gibt den dynamisch zugewiesenen Port aus, über den der Apache-Server vom Host-Laptop aus erreichbar ist.

## 6. Fazit und Fehlerbehebung (Troubleshooting)

Während des Hands-on wurden wichtige Erkenntnisse zur Abstraktion in K8s gewonnen:

* **Entkopplung**: Durch das Weglassen von festen Namespaces in den YAML-Dateien sind die Konfigurationen portabel und können in jeder Umgebung (Dev/Prod) wiederverwendet werden.
* **Typisches Problem**: Falls der Webserver nicht erreichbar ist, liegt es oft an einem fehlerhaften `selector` in der Service-YAML. Wenn das Label im Pod nicht exakt mit dem Selector im Service übereinstimmt, leitet Kubernetes den Traffic ins Leere.
* **Automatisierung**: Mit `kubectl apply` wurde demonstriert, wie effizient skalierbare Systeme verwaltet werden können, im Vergleich zum manuellen Starten einzelner Container.

