# Einstieg in AWS – Was du als Anfänger wissen musst

Wenn du **komplett neu in AWS** bist, ist das hier dein Einstieg. Du bekommst einen **soliden Überblick**, um AWS zu verstehen und erste praktische Erfahrungen zu sammeln – auch als Vorbereitung auf die Arbeit mit Terraform.

---

## 🟢 1. Was ist AWS?

**AWS (Amazon Web Services)** ist die Cloud-Plattform von Amazon mit **über 200 Diensten** für:

- Server, Datenbanken, Netzwerke, Speicher
- DevOps, Monitoring, Sicherheit
- KI, Big Data, IoT, u.v.m.

---

## 🧱 2. Grundbegriffe & Konzepte

### 📍 Regionen & Verfügbarkeitszonen
- **Region** = geografischer Ort (z. B. `eu-central-1` = Frankfurt)
- **Verfügbarkeitszonen (AZs)** = isolierte Rechenzentren innerhalb einer Region
- **Edge Locations** sind geographisch verteilte Punkte, die vor allem für Content Delivery Networks (CDNs) wie Amazon CloudFront verwendet werden. Sie befinden sich näher an den Endnutzern und helfen dabei, Inhalte schneller bereitzustellen, indem sie Daten zwischenspeichern (Caching).

Du wählst bei jedem Dienst eine Region aus.

---

## 🔧 3. Wichtige AWS-Dienste für Einsteiger

| Dienst       | Beschreibung                                                        | Terraform-Name              |
|--------------|---------------------------------------------------------------------|-----------------------------|
| **EC2**      | Virtuelle Server (Linux/Windows)                                    | `aws_instance`              |
| **S3**       | Objektspeicher (Dateien, Backups, Webseiten)                        | `aws_s3_bucket`             |
| **RDS**      | Verwaltete relationale Datenbanken (MySQL, PostgreSQL, etc.)        | `aws_db_instance`           |
| **VPC**      | Virtuelles Netzwerk (Subnetze, Firewalls, Gateways)                 | `aws_vpc`                   |
| **IAM**      | Benutzer, Rollen, Rechte & Policies verwalten                       | `aws_iam_user`, `role`, etc.|
| **Lambda**   | Serverless Funktionen (Code ausführen ohne Server)                  | `aws_lambda_function`       |
| **CloudWatch** | Monitoring & Logs                                                  | `aws_cloudwatch_log_group`  |
| **Route 53** | DNS-Verwaltung, Domains, Routing                                    | `aws_route53_record`        |
| **ELB**      | Load Balancer für verteilte Server                                  | `aws_lb`, `aws_lb_target_group` |

---

## 📐 4. Die Struktur deiner Arbeit in AWS

- **Management Console**: Web-Oberfläche
- **AWS CLI**: Kommandozeilentool
- **SDKs & APIs**: Für Entwickler (z. B. Python, Node.js)

**Achtung:** Arbeite **nicht** mit dem Root-Benutzer. Nutze stattdessen einen **IAM-User mit Rechten**.

---

## 📌 5. Was du am Anfang lernen solltest

| Thema                   | Was du verstehen solltest                                |
|-------------------------|----------------------------------------------------------|
| AWS-Konto & IAM         | Wie du sicher arbeitest, Benutzer & Rollen verwaltest   |
| EC2                     | Server starten, verbinden, stoppen                       |
| S3                      | Datei hochladen, öffentliche Zugriffe                    |
| VPC & Security Groups   | Netzwerke & Firewalls                                    |
| RDS                     | Datenbank einrichten & verbinden                         |
| Budgets & Alarme        | Kostenkontrolle & Abrechnung verstehen                   |

---

## 💰 6. Kosten & Free Tier

### AWS Free Tier (12 Monate kostenlos):

| Dienst   | Free-Tier-Kontingent                        |
|----------|---------------------------------------------|
| EC2      | 750 Stunden/Monat (t2.micro)                |
| S3       | 5 GB Speicher                               |
| RDS      | 750 Stunden/Monat (t2.micro, db.t2)         |
| Lambda   | 1 Mio. Funktionsaufrufe/Monat               |

> 🛎 **Tipp:** Aktiviere Budgets & Benachrichtigungen in der AWS Console!

---

## 🧪 7. Erste Schritte (To-do-Liste)

1. ✅ AWS-Konto erstellen: [https://aws.amazon.com](https://aws.amazon.com)
2. ✅ IAM-User erstellen (nicht mit Root-Account arbeiten!)
3. ✅ AWS CLI installieren & konfigurieren
4. ✅ Praktische Tests:
   - EC2: Starte einen Server
   - S3: Bucket anlegen & Datei hochladen
   - IAM: Nutzer & Rechte ausprobieren
5. ✅ Region `eu-central-1` (Frankfurt) verwenden

---

## 📚 8. Lernressourcen

### Offiziell:
- [Skill Builder](https://skillbuilder.aws/learn/94T2BEN85A/aws-cloud-practitioner-essentials/)
- 🔗 [AWS Free Tier Übersicht](https://aws.amazon.com/free/)
- 📘 [AWS Getting Started Guide](https://aws.amazon.com/getting-started/)

### Tutorials & Kurse:
- [learn.awscloud.com](https://learn.awscloud.com)
- YouTube: „AWS für Einsteiger“
- Plattformen: Udemy, A Cloud Guru, freeCodeCamp

---

## 🚫 9. Was du vermeiden solltest

- ❌ Dauerhaft mit dem Root-User arbeiten
- ❌ EC2-Instanzen vergessen zu stoppen
- ❌ S3-Buckets öffentlich setzen ohne Absicherung
- ❌ `0.0.0.0/0` Zugriff in Security Groups ohne Not

---

## 🔁 10. Verbindung zu Terraform

Du kannst AWS-Ressourcen mit **Terraform als Code verwalten**:

```hcl
provider "aws" {
  region = "eu-central-1"
}

resource "aws_s3_bucket" "mein_bucket" {
  bucket = "mein-erster-bucket"
  acl    = "private"
}
```

## Weitere Notizen

#### EC2

Es gibt minimum capacity, desired capacity und maximum capacity.

D.h. minimum capacity hat eine minimale Anzahl an EC2 Instanzen, damit das System überhaupt läuft. Desired capacity ist die optimale Anzahl an EC2 Instanzen um den aktuellen workload abzuarbeiten. Der Workload schwankt je nach Anzahl der Requests. Mithilfe des Auto scalings von AWS werden Instanzen aktiviert oder wieder deaktiviert um Anfragen effizient abzuarbeiten. Die maximum capacity definiert die maximale Anzahl an Instanzen um Kosten kontrollieren zu können.

Scaling: Instanzen können vertikal (scaling up) oder horizontal (scaling out) skaliert werden.

Scaling out:
Mehr Ressourcen, also mehr Instanzen um Arbeit parallel abzuarbeiten.

Scaling Up:
Rechenleistung der einzelnen Maschine erhöhen, aber nicht mehr Instanzen. (Also mehr Power per instance)

#### ELB (elastic load balancing)

Beispiel: Wenn mehr Anfragen reinkommen, wird die Anzahl an Instanzen erhöht, um alle Anfragen parallel abarbeiten zu können. Nun kann es aber sein, dass alle Anfragen nur in eine Instanz eingehen. Um die Anfragen gleichmäßig verteilen zu können und somit die maximale Auslastung zu erreichen, gibt es den sogennanten load balancer, der die Anfragen an die einzelnen Instanzen verteilt.

Der Load balancer regelt auch die Verteilung zwischen tiers.
D.h. man hat z.B. ordering tiers, also EC2 Instanzen, die Anfragen annehmen (Frontend) und man hat production tiers EC2 Instanzen, die die Anfrage verarbeiten (Backend). Beide tiers können unterschiedliche Anzahl an Instanzen haben. Der load balancer regelt nicht nur die Verteilung der User Anfragen, sondern auch die Verteilung der Weiterleitung an das production tier.

#### Messaging und Queuing

Monolithen Anwendungen sind tightly coupled. D.h. Komponenten innerhalb des Monolithen sind eng miteinander verbunden. Wenn eine Komponente ausfällt, ist das ganze System in Gefahr.

Bsp: Wenn alle production tiers ausgelastet sind und es mehr Anfragen vom Frontend kommen, könnte es sein, dass Anfragen fallengelassen werden, um weitere Anfragen anzunehmnen. Oder das production tier fällt komplett aus und die Anfragen gehen verloren.
Um das zu verhindern, gibt es eine Art Queue (Buffer), auf die die Request geschrieben werden und eine Backend Instanz eine annimmt, sobald sein Service wieder frei ist. Das frontend ist direkt wieder frei für Anfragen, sobald der Request auf der Queue steht.

Auch wenn z.B. das Backend komplett ausfällt, dann bekommt das Frontend keine Fehler, da die Queue den Fehler nicht weitergibt und wartet bis das Backend wieder antwortet (loosely couple) -> Microservices.

-> SQS (Amazon simple queue service) oder SNS (Amazon simple notification service)

#### Managed services

Unmanaged Services: wie E2, ist man eigenverantwortlich für das Setup, Sicherheit, Wartung des OS, Netzwerkkonfiguration und den Anwendungen selbst. AWS liefert nur die phyiskalische 
Infrastruktur.

Managed Services:
Weniger verantwortlich für einen selbst.

Fully managed Services (Lambda-Service, AWS Fargate(für Container only)):
AWS kümmert sich komplett um die Verwaltung des Servies, auch serverless gennannt, da die unterliegende Infrastruktur nicht sichtbar ist.

Lambda-Service:
Lambda ist ein serverloser Rechenservice, der Code als Reaktion auf Ereignisse ausführt, ohne dass Server bereitgestellt oder verwaltet werden müssen. Er verwaltet automatisch die zugrunde liegende Infrastruktur und skaliert die Ressourcen basierend auf dem Anfragevolumen. Es werden nur die tatsächlich genutzten Rechenzeiten in Millisekunden in Rechnung gestellt. Lambda übernimmt die Ausführung, Skalierung und Ressourcenzuweisung. Man können die Leistung optimieren, indem man die geeignete Speichergröße für eine Funktion konfiguriert.
Stichwort: Trigger
Die eigene Anwendung muss auf einen Trigger konfiguriert werden z.B. HTTP requests.

#### Container

Container ein einziges portables Formate, welches alles enthält, damit eine Anwendung unabhängig vom Setup und Host läuft.
Container laufen auf einem Hostsystem, nicht wie eine VM, welche über ein Hypervisor läuft.

ECR - Amazon Elastic Container Registry:
Speichert Docker images. In ECR kann man die Container managen und deployen.

ECS - Amazon Elastic Container Service
Orchistration Service

EKS - Amazon Elastic Kubernetes Service
Orchistration Service mithilfe von Kubernetes

Vorgehen:
1) Man lädt ein container image zu ECR hoch.
2) Orchistration Service wählen, ECS oder EKS
3) Wähle Platform: EC2 oder Fargate (managed von AWS)

#### Networking - Virtual Private Cloud (VPC)

Die VPC ist der oberste Container der Netzwerkisolation innerhalb eines AWS-Accounts.
Alles, was IP-Netzwerke nutzt (EC2, RDS, ElastiCache, ENIs, NAT/IGW usw.), läuft innerhalb einer VPC.
Ein VPC ist ein logisch isoliertes Netzwerk innerhalb der AWS Cloud.
Ein VPC ist die Grundlage für z.B. EC2 Instanzen.

Andere Services wie z.B. S3 brauchen kein VPC.

Vorteil:
- Man kann das Netzwerk nicht von außen (clients) zugänglich machen.
- Eigenen IP Adressraum festlegen
- Subnetze erstellen (private (z.B. Datenbanken) und öffentliche z.B. EC2 Instanzen), um Resourcen zu organisieren
- Routing steuern
- Sicherheitskontrolle (Steuerun von eingehenden und ausgehenden Traffic)

__Gateways__

Um einen öffentlichen Zugang zum VPC zu ermöglichen, braucht man ein Internt Gateway. (Eine Art Tür zum VPC)

Für einen privaten Zugang zu ermöglichen, braucht man einen Virtual Private Gateway. Dieser ist nur über VPN zugänglich.

Beispiel Szenario öffentlicher Zugang:

Client (Anfrage via Internet) ---> AWS Cloud ---> Internet Gateway (Türe zum VPC) ---> VPC ----> Subnet ---> EC2 Instanzen

__Zugangsarten zur Cloud__

- Client VPN (OpenVPN based) - Überall erreichbar
- Site-to-Site VPN
- PrivateLink
- Direct Connect
