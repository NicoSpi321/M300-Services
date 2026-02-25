# Wissensdatenbank: Kubernetes Grundlagen (K8s)

## 1. Definition und Herkunft

Kubernetes ist das Herzstück moderner Cloud-Infrastrukturen. Ursprünglich von **Google** entwickelt, wird die Open-Source-Plattform heute von der **Cloud Native Computing Foundation (CNCF)** verwaltet.

* **Hauptaufgabe**: Die Automatisierung der Bereitstellung, Skalierung und Verwaltung (Orchestrierung) von containerisierten Anwendungen.
* **Ziel**: Sicherstellung, dass die gewünschte Anzahl an Containern läuft, Lasten verteilt werden und Ressourcen effizient genutzt werden.

## 2. Netzwerk-Architektur

Die Kommunikation innerhalb eines Clusters folgt strikten Regeln, um Skalierbarkeit zu garantieren.

* **Struktur**: Kubernetes nutzt ein flaches, Cluster-weites Netzwerk. Jeder **Pod** erhält eine eigene IP-Adresse und kann ohne NAT mit jedem anderen Pod kommunizieren.
* **Node-Kommunikation**: Der Traffic zwischen den Nodes wird über das **Kube-Proxy-Modul** und virtuelle IP-Adressen (**ClusterIP**) gesteuert, die Daten über ein Overlay-Netzwerk an die Ziel-Pods leiten.

## 3. Verwaltung und Objekte

Kubernetes wird primär über Textdateien gesteuert, was die Infrastruktur reproduzierbar macht.

* **Format & Tool**: Objekte werden im **YAML-Format** beschrieben und über das CLI-Tool `kubectl` verwaltet.
* **Gruppierung**: Mittels **Labels** (Key-Value-Paare) und **Selectors** lassen sich Ressourcen logisch organisieren und gezielt ansprechen.

## 4. Kern-Ressourcen im Überblick

| Objekt | Beschreibung |
| --- | --- |
| **Pod** | Die kleinste Einheit; beherbergt einen oder mehrere Container (teilen sich Netzwerk/Speicher). |
| **Service** | Stabile Abstraktion (IP/DNS), um eine Gruppe von Pods im Netzwerk erreichbar zu machen. |
| **Ingress** | Verwaltet den externen HTTP/HTTPS-Zugriff auf Services (ähnlich einem Reverse Proxy). |
| **Namespace** | Virtuelle Trennung innerhalb des Clusters (z.B. für `prod`, `dev` oder verschiedene Projekte). |
| **ReplicaSet** | Garantiert, dass zu jedem Zeitpunkt die festgelegte Anzahl identischer Pod-Kopien läuft. |
| **Deployment** | Deklarative Steuerung für Updates von Pods und ReplicaSets (Skalierung, Rollbacks). |

