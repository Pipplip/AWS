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

## 🔧 3. Wichtige AWS-Dienste

| Dienst                    | Beschreibung                                                 | Terraform-Name                                            |
|---------------------------|--------------------------------------------------------------|-----------------------------------------------------------|
| **EC2**                   | Virtuelle Server (Linux/Windows)                             | `aws_instance`                                            |
| **S3**                    | Objektspeicher (Dateien, Backups, Hosting)                   | `aws_s3_bucket`                                           |
| **RDS**                   | Verwaltete relationale Datenbanken (MySQL, PostgreSQL, etc.) | `aws_db_instance`                                         |
| **VPC**                   | Virtuelles Netzwerk (Subnetze, Firewalls, Gateways)          | `aws_vpc`                                                 |
| **IAM**                   | Benutzer, Rollen, Rechte & Policies verwalten                | `aws_iam_user`, `aws_iam_role`, `aws_iam_policy`          |
| **Lambda**                | Serverless Funktionen (Code ausführen ohne Server)           | `aws_lambda_function`                                     |
| **CloudWatch**            | Monitoring & Logs, Alarm                                     | `aws_cloudwatch_log_group`, `aws_cloudwatch_metric_alarm` |
| **CloudTrail**            | API-Auditing & Aktivitätslogs                                | `aws_cloudtrail`                                          |
| **Route 53**              | DNS-Verwaltung, Domains, Routing                             | `aws_route53_zone`, `aws_route53_record`                  |
| **ELB**                   | Load Balancer für verteilte Server (Traffic Verteiler)       | `aws_lb`, `aws_lb_target_group`                           |
| **Auto Scaling Group**    | Automatische Skalierung von EC2                              | `aws_autoscaling_group`                                   |
| **EBS**                   | Block-Storage für EC2                                        | `aws_ebs_volume`                                          |
| **EFS**                   | Gemeinsames Dateisystem (network file storage)               | `aws_efs_file_system`                                     |
| **Elasticache**           | In-memory cache                                              | `aws_elasticache_cluster`                                 |
| **DynamoDB**              | No-SQL Key-Value Datenbank                                   | `aws_dynamo_table`                                        |
| **API Gateway**           | REST/HTTP API Management für Lambda und Microservices        | `aws_api_gateway_rest_api`                                |
| **SQS**                   | Message Queue                                                | `aws_sqs_queue`                                           |
| **SNS**                   | Notifications                                                | `aws_sns_topic`                                           |
| **ECS**                   | Container Orchestrierung (Docker)                            | `aws_ecs_cluster`, `aws_ecs_service`                      |
| **EKS**                   | Kubernetes auf AWS                                           | `aws_eks_cluster`                                         |
| **ECR**                   | Docker Image registry                                        | `aws_ecr_repository`                                      |
| **CloudFront**            | CDN für schnelle Content-Auslieferung                        | `aws_cloudfront_distribution`                             |
| **Global Accelerator**    | Optimierter globaler Traffic-Routing Layer                   | `aws_globalaccelerator_accelerator`                       |
| **Systems Manager (SSM)** | EC2 Management ohne SSH                                      | `aws_ssm_parameter`, `aws_ssm_document`                   |
| **Secrets Manager**       | Sicheres Speichern von Secrets & Credentials                 | `aws_secretsmanager_secret`                               |
| **KMS**                   | Key Management & Verschlüsselung                             | `aws_kms_key`                                             |
| **WAF**                   | Web Application Firewall                                     | `aws_wafv2_web_acl`                                       |
| **GuardDuty**             | Threat Detection & Security Monitoring                       | `aws_guardduty_detector`                                  |
| **Inspector**             | Sicherheits- & Vulnerability Scans                           | `aws_inspector2_enabler`                                  |
| **Config**                | Compliance & Ressourcen-Drift Monitoring                     | `aws_config_configuration_recorder`                       |
| **Organizations**         | Multi-Account Management                                     | `aws_organizations_organization`                          |
| **Control Tower**         | Enterprise Multi-Account Governance                          | AWS-managed                                               |
| **Glue**                  | ETL & Data Catalog                                           | `aws_glue_catalog_database`, `aws_glue_job`               |
| **Kinesis**               | Echtzeit Data Streaming                                      | `aws_kinesis_stream`                                      |
| **Firehose**              | Managed Data Delivery Streams                                | `aws_kinesis_firehose_delivery_stream`                    |
| **Athena**                | SQL Queries direkt auf S3 Data Lake                          | `aws_athena_database`                                     |
| **EMR**                   | Hadoop/Spark Cluster Processing                              | `aws_emr_cluster`                                         |
| **QuickSight**            | BI Dashboards & Data Visualization                           | `aws_quicksight_*`                                        |
| **SageMaker**             | Machine Learning Plattform                                   | `aws_sagemaker_notebook_instance`                         |
| **Bedrock**               | Generative AI / Foundation Models                            | `aws_bedrock_*`                                           |
---

## 📐 4. Die Struktur deiner Arbeit in AWS

- **Management Console**: Web-Oberfläche
- **AWS CLI**: Kommandozeilentool
- **SDKs & APIs**: Für Entwickler (z. B. Python, Node.js)

**Achtung:** Arbeite **nicht** mit dem Root-Benutzer. Nutze stattdessen einen **IAM-User mit Rechten**.

---

## 💰 5. Kosten & Free Tier

### AWS Free Tier (12 Monate kostenlos):

| Dienst   | Free-Tier-Kontingent                        |
|----------|---------------------------------------------|
| EC2      | 750 Stunden/Monat (t2.micro)                |
| S3       | 5 GB Speicher                               |
| RDS      | 750 Stunden/Monat (t2.micro, db.t2)         |
| Lambda   | 1 Mio. Funktionsaufrufe/Monat               |

> 🛎 **Tipp:** Aktiviere Budgets & Benachrichtigungen in der AWS Console!

---

## 🧪 6. Erste Schritte (To-do-Liste)

1. ✅ AWS-Konto erstellen: [https://aws.amazon.com](https://aws.amazon.com)
2. ✅ IAM-User erstellen (nicht mit Root-Account arbeiten!)
3. ✅ AWS CLI installieren & konfigurieren
4. ✅ Praktische Tests:
   - EC2: Starte einen Server
   - S3: Bucket anlegen & Datei hochladen
   - IAM: Nutzer & Rechte ausprobieren
5. ✅ Region `eu-central-1` (Frankfurt) verwenden

---

## 📚 7. Lernressourcen

### Offiziell:
- [Skill Builder](https://skillbuilder.aws/learn/94T2BEN85A/aws-cloud-practitioner-essentials/)
- 🔗 [AWS Free Tier Übersicht](https://aws.amazon.com/free/)
- 📘 [AWS Getting Started Guide](https://aws.amazon.com/getting-started/)

### Tutorials & Kurse:
- [learn.awscloud.com](https://learn.awscloud.com)
- YouTube: „AWS für Einsteiger“
- Plattformen: Udemy, A Cloud Guru, freeCodeCamp

---

## 🚫 8. Was du vermeiden solltest

- ❌ Dauerhaft mit dem Root-User arbeiten
- ❌ EC2-Instanzen vergessen zu stoppen
- ❌ S3-Buckets öffentlich setzen ohne Absicherung
- ❌ `0.0.0.0/0` Zugriff in Security Groups ohne Not

---

## 🔁 9. Verbindung zu Terraform

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

Typische Enterprise Architektur:  
```
Internet
│
▼
Route53
│
CloudFront
│
WAF
│
ALB
│
┌──────────────────────────────┐
│ Private VPC                  │
│                              │
│ ECS/Fargate Cluster          │
│ oder                         │
│ EKS Cluster                  │
│                              │
│ ┌─────────────────────────┐  │
│ │ Microservice A          │  │
│ └─────────────────────────┘  │
│                              │
│ ┌─────────────────────────┐  │
│ │ Microservice B          │  │
│ └─────────────────────────┘  │
│                              │
│ SQS / EventBridge            │
│                              │
│ RDS / DynamoDB               │
│ ElastiCache                  │
└──────────────────────────────┘

Monitoring:
CloudWatch + CloudTrail

Security:
IAM + KMS + Secrets Manager

Deployment:
Terraform + GitHub Actions
oder
Terraform + CodePipeline
```

## Weitere Notizen

## EC2

EC2 (Amazon Elastic Compute Cloud) sind virtuelle Maschinen (Server) in der Cloud. 
Eine EC2 Instanz ist wie ein normaler PC, Server, Laptop, nur dass dieser in der Cloud läuft.
Man kann verschiedene Betriebssysteme (Linux, Windows) auswählen und Software darauf installieren.

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

## Managed services

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

## Container

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

## Networking - Virtual Private Cloud (VPC)

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

__Network Access Control Lists (ACLs) & Security groups__

Zusätzlich gibt es ACLs, die den ein- und ausgehenden Traffic auf Subnet Ebene kontrollieren. Wie eine Art Firewall.
ACLs sind zustandslos (stateless), d.h. es muss für eingehenden und ausgehenden Traffic eine Regel definiert werden, weil sich die ACLs nicht merken, ob eine Paket-Anfrage erlaubt wurde oder nicht.

Nun gibt es innerhalb des Subnets eventuell mehrere EC2 Instanzen, die nur bestimmten Traffic erlauben sollen. Dafür gibt es die Security Groups.
D.h. eine Security Group ist eine virtuelle Firewall auf Instanz (z.B. EC2) Ebene. Security Groups sind zustandsbehaftet (stateful), d.h. wenn eine eingehende Regel definiert wird, wird der ausgehende Traffic automatisch erlaubt

Eine Security Group kann man sich als Türsteher vorstellen, der nur bestimmte Anfragen durchlässt, aber alle Antworten wieder herauslässt.

ACLs und Security Groups müssen selbst konfiguriert werden, da AWS keine Standardregeln vordefiniert.

__Zugangsarten zur Cloud__

- Client VPN (OpenVPN based) - Überall erreichbar (z.B. Home Office)
- Site-to-Site VPN
- PrivateLink
- Direct Connect (Höhree Bandbreite, niedrige Latenz)

![VPC](/images/VPC.png)
  
![VPC subnet](/images/VPC_subnet.png)

![VPC regions](/images/VPC_regions.png)

__Amazon Route 53__

Route 53 ist ein skalierbarer und hochverfügbarer Domain Name System (DNS)-Webdienst. Er übersetzt Domain-Namen (z.B. www.beispiel.de) in 
IP-Adressen (z.B. 192.0.2.1), die Computer verwenden, um sich gegenseitig im Internet zu finden.

__Amazon CloudFront__

CloudFront ist ein Content Delivery Network (CDN)-Dienst, der Inhalte (z.B. Webseiten, Videos, APIs) schnell und sicher an Endbenutzer weltweit liefert. CloudFront nutzt ein Netzwerk von Edge-Standorten, um Inhalte näher an den Benutzern zu speichern und so die Latenz zu reduzieren.

![VPC](/images/cloudfront.png)

__AWS Globals Accelerator__

AWS Global Accelerator ist ein Netzwerkdienst, der den Datenverkehr von Benutzern zu Anwendungen optimiert, die in AWS ausgeführt werden. Er verwendet das globale AWS-Netzwerk, um den Datenverkehr über die optimalen Pfade zu leiten, was die Leistung und Verfügbarkeit von Anwendungen verbessert.

## Storage

__Block Storage__

Block Storage ist eine Speicherart, bei der Daten in Blöcken fester Größe gespeichert werden. Jeder Block hat eine eindeutige Adresse, die es dem Betriebssystem ermöglicht, direkt auf die Daten zuzugreifen. Block Storage wird häufig für Betriebssysteme und Anwendungen verwendet, die schnellen und direkten Zugriff auf Daten benötigen.
Amazon EC2 instance store oder EBS (Elastic Block Store) sind Beispiele für Block Storage in AWS.

Die Instance store ist temporär und geht verloren, wenn die Instanz gestoppt wird. EBS ist persistent und bleibt auch nach dem Stoppen der Instanz erhalten.
Sie hängt direkt an der EC2 Instanz und kann wie eine Festplatte formatiert und gemountet werden. Anwendungsbeispiele temporäre Datenverarbeitung, Cache, Swap Dateien.

EBS Volumes sind persistent und können unabhängig von der Lebensdauer der EC2 Instanz existieren. Snapshots ermöglichen Backups und die Wiederherstellung von Daten.

Für die Automatisierung von Snapshots kann der Amazon Data Lifecycle Manager verwendent werden.

__Object Storage__

Object Storage ist eine Speicherarchitektur, bei der Daten als Objekte gespeichert werden. Jedes Objekt besteht aus den eigentlichen Daten, Metadaten und einer eindeutigen Kennung. Object Storage ist ideal für die Speicherung großer Mengen unstrukturierter Daten wie Bilder, Videos, Dokumente und Backups.

Object = Daten + Metadaten + eindeutige ID

S3 (Simple Storage Service) ist ein Beispiel für Object Storage in AWS.
Die Objekte werden in Buckets organisiert, die als Container für die Objekte dienen. Jedes Objekt in einem Bucket wird durch einen eindeutigen Schlüssel (Key) identifiziert.

__File Storage__

File Storage ist eine Speicherart, bei der Daten in einer hierarchischen Struktur von Dateien und Verzeichnissen organisiert sind. Benutzer und Anwendungen greifen auf Dateien über Dateipfade zu. File Storage wird häufig für gemeinsame Dateifreigaben und Anwendungen verwendet, die eine traditionelle Dateisystemstruktur benötigen. Dateien können
ohne Probleme synchron aufgerufen und bearbeitet werden.

Amazon Elastic File System (EFS) ist ein Beispiel für File Storage in AWS.

## Datenbanken

__Relationale Datenbanken__

Relationale Datenbanken speichern Daten in Tabellen mit Zeilen und Spalten. Sie verwenden SQL (Structured Query Language) für die Datenverwaltung und -abfrage. Relationale Datenbanken sind ideal für strukturierte Daten und unterstützen ACID-Eigenschaften (Atomicity, Consistency, Isolation, Durability).

Amazon Relational Database Service (Amazon RDS) ist ein verwalteter Dienst für relationale Datenbanken in AWS. RDS unterstützt mehrere Datenbank-Engines, darunter Amazon Aurora, PostgreSQL, MySQL, MariaDB, Oracle Database und Microsoft SQL Server.
Aufgaben von RDS:
- Automatisches Backup
- Software-Patching
- Überwachung
- Skalierung der Rechen- und Speicherressourcen
- Hochverfügbarkeit mit Multi-AZ-Bereitstellungen
  
Amazon Aurora ist eine gemanagte relationale Datenbank-Engine, die mit MySQL und PostgreSQL kompatibel ist. Sie bietet eine hohe Leistung und Verfügbarkeit durch verteilte Architektur und automatische Replikation.

__NoSQL-Datenbanken__

NoSQL-Datenbanken sind nicht-relationale Datenbanken, die flexible Datenmodelle unterstützen. Sie sind ideal für unstrukturierte oder semi-strukturierte Daten und bieten hohe Skalierbarkeit und Leistung.

Amazon DynamoDB ist ein verwalteter NoSQL-Datenbankdienst in AWS. DynamoDB bietet schnelle und vorhersehbare Leistung mit nahtloser Skalierung. Es unterstützt sowohl dokumentenbasierte als auch schlüsselwertbasierte Datenmodelle.
Daten einer NoSQL Datenbank heißen Items und werden in Tabellen organisiert. Jedes Item besteht aus Attributen (Schlüssel-Wert-Paare).

__Caching__

Caching ist eine Technik zur temporären Speicherung von Daten, um den schnellen Zugriff auf häufig verwendete Informationen zu ermöglichen. Caches reduzieren die Latenz und verbessern die Leistung von Anwendungen, indem sie Daten näher an den Endbenutzern speichern.

Amazon ElastiCache ist ein verwalteter Caching-Dienst in AWS, der In-Memory-Datenbanken wie Redis und Memcached unterstützt. ElastiCache verbessert die Anwendungsleistung, indem es häufig verwendete Daten im Arbeitsspeicher speichert und so den Zugriff beschleunigt.

## AI ML and Data Analytics

AWS AI/ML besteht aus 3 Schichten:   
1. AI Services - vorgefertigte KI-Services, die bestimmte Aufgaben wie Bilderkennung, Sprachverarbeitung oder Übersetzung erledigen. Z.B: Amazon Rekognition, Amazon Comprehend, Amazon Translate.
2. ML Services - baue, trainiere und deploye eigene ML Modelle, z.B. mit Amazon SageMaker.
3. ML frameworks and infrastructure - komplett freikonfigurierbare ML-Umgebungen, z.B. TensorFlow, PyTorch, MXNet.

## Data Analytics

Data Analytics ist der Prozess der Untersuchung von Datensätzen.   
Daten werden in einem DataLake gespeichert, um sie zu analysieren und daraus Erkenntnisse zu gewinnen.   
Ein ETL Prozess (Extract, Transform, Load) wird verwendet, um Daten aus verschiedenen Quellen zu extrahieren, sie in ein geeignetes Format zu transformieren und sie in den DataLake zu laden.   

AWS hat verschiedene Services für Data Analytics:   
- Kinesis oder AWS Glue: Daten aus verschiedenen Quellen sammeln, transformieren und in den DataLake laden.
- S3 oder Redshift: Speicherung der Daten im DataLake (S3) oder Data-Warehouse (Redshift).
- EMR (Elastic MapReduce): Verarbeitung der Daten im DataLake mit Apache Hadoop, Spark oder Presto.
- Quicksight: Visualisierung der Daten und Erstellung von Dashboards.
- Athena: Abfragen der Daten im DataLake mit SQL.

__Kinesis:__   
Für das Sammeln von Daten aus verschiedenen Quellen, z.B. IoT-Geräten, Webanwendungen, Datenbanken oder externen APIs in Echtzeit.

__Firehose:__   
Firehose ist ein Service von Kinesis, der Datenströme in Echtzeit verarbeitet und sie in andere AWS-Dienste wie S3, Redshift oder Elasticsearch weiterleitet.

Bsp. Szenario: Ein Unternehmen benutzt ein automatisierte Pipeline, um Daten zu sammlen, zu transformieren, speichern und Stakeholdern zur Verfügung zu stellen.
![DataAnalytics](/images/DataAnalytics.png)

1. Die App möchte Produkt-Empfehlungen dem Kunden anzeigen
2. App Daten speichern. Eine DynamoDB Tabelle speichert die Produktinformationen und die Kundeninteraktionen.
3. Kinesis Data Streams nimmt die Daten auf und leitet sie an Kinesis Data Firehose weiter.
4. Kinesis Data Firehose transformiert die Daten mithilfe von AWS Lambda (z.B. von json in csv)...
5. ...und speichert sie in einem S3 Bucket (DataLake)
6. AWS Glue crawlt die Daten im S3 Bucket und erstellt ein Schema, das die Struktur der Daten beschreibt.
7. Datenentwickler (Stakeholder) verwenden Athena, um die Daten im DataLake abzufragen und zu analysieren.
8. SageMaker (Stakeholder) verwendet die Daten im DataLake, um ein Machine Learning Modell zu trainieren, das personalisierte Produkt-Empfehlungen für Kunden erstellt.

## Security

Authentication: Wer ist der Benutzer? (z.B. IAM User, Rolle, Service)   
Authorization: Was darf der Benutzer tun? (z.B. Zugriff auf S3 Bucket, EC2 Instanz starten)   

Vorgehensweise bei Erstellung eines AWS Accounts:  

__AWS account root user__
ist der erste Benutzer, der bei der Erstellung eines AWS-Kontos erstellt wird.   
Er hat uneingeschränkten Zugriff auf alle Ressourcen und Dienste im Konto.   
Der Root-Benutzer sollte nur für die anfängliche Kontoeinrichtung und für bestimmte administrative Aufgaben verwendet werden.    
Es wird dringend empfohlen, den Root-Benutzer nicht für den täglichen Betrieb zu verwenden.    

__MFA__
Multi-Factor Authentication (MFA) ist eine Sicherheitsmaßnahme, die einen zusätzlichen Authentifizierungsfaktor neben dem Passwort erfordert.  

__AWS IAM__
IAM (Identity and Access Management) ist ein Service, der es ermöglicht, den Zugriff auf AWS-Ressourcen zu verwalten.   
IAM ermöglicht die Erstellung von Benutzern, Gruppen, Rollen und Richtlinien, um den Zugriff auf Ressourcen basierend auf den Prinzipien der geringsten Privilegien zu steuern.  
Least Privilege Principle: Ein neu erstellter IAM User hat standardmäßig keine Berechtigigungen. Man muss explizit Berechtigungen zuweisen, um auf Ressourcen zugreifen zu können.

IAM besteht aus:
- **Benutzer (Users)**: Individuelle Identitäten, die Zugriff auf AWS-Ressourcen haben können. Jeder Benutzer hat Anmeldeinformationen (Passwort, Zugriffsschlüssel) und kann spezifische Berechtigungen erhalten.
- **Gruppen (Groups)**: Eine Sammlung von Benutzern, die gemeinsame Berechtigungen erhalten. Benutzer können Mitglied mehrerer Gruppen sein.
- **Rollen (Roles)**: Rollen sind AWS-Identitäten mit bestimmten Berechtigungen, die von Benutzern oder Diensten übernommen werden können. Rollen ermöglichen es, temporären Zugriff auf Ressourcen zu gewähren, ohne dass Anmeldeinformationen benötigt werden.
- **Policies**: Json-Dokumente, die Berechtigungen definieren, um den Zugriff auf AWS-Ressourcen zu steuern. Policies können an Benutzer, Gruppen oder Rollen angehängt werden, um ihnen die entsprechenden Berechtigungen zu erteilen. Wenn man eine Policy einer Group zuweist, erhalten alle Mitglieder dieser Gruppe die Berechtigungen der Policy.   

Wie IAM prüft:
```
Benutzer/Rolle
      ↓
IAM Policy
      ↓
Erlaubt?
      ↓
Ja → Aktion
Nein → AccessDenied
```

![IAM](/images/IAM.png)

__AWS Organizations__
AWS Organizations ist ein Service, der es ermöglicht, mehrere AWS-Konten zentral zu verwalten und zu organisieren.   
Mit AWS Organizations können Unternehmen ihre Konten in einer hierarchischen Struktur (Organizational Units, OUs) organisieren, Richtlinien auf Kontoebene anwenden und die Abrechnung konsolidieren.   
AWS Organizations unterstützt die Verwaltung von Berechtigungen, Sicherheitsrichtlinien und Compliance-Anforderungen über mehrere Konten hinweg.  

__Security groups__
Security Groups sind virtuelle Firewalls, die den ein- und ausgehenden Datenverkehr für AWS-Ressourcen wie EC2-Instanzen steuern.

Weitere AWS Services für Sicherheit:
- AWS Key Management Service (KMS): Verwaltung von Verschlüsselungsschlüsseln
- AWS Secrets Manager: Sicheres Speichern und Verwalten von Anmeldeinformationen, API-Schlüsseln und anderen sensiblen Daten
- AWS CloudTrail: Protokollierung von API-Aufrufen und Aktivitäten in AWS-Konten
- AWS ACM (AWS Certificate Manager): Verwaltung von SSL/TLS-Zertifikaten für sichere Kommunikation
- AWS Shield: Schutz vor DDoS-Angriffen und Sicherheitsbedrohungen
- AWS WAF (Web Application Firewall): Schutz von Webanwendungen vor häufigen Sicherheitsbedrohungen und Angriffen

## Monitoring, Compliance und Governance in AWS Cloud

#### Monitoring
Monitoring ist der Prozess der Überwachung von Systemen, Anwendungen und Infrastruktur, um deren Leistung, Verfügbarkeit und Sicherheit sicherzustellen.   
Monitoring hilft dabei, Probleme frühzeitig zu erkennen, die Ursachen zu identifizieren und die Systemleistung zu optimieren.   
Monitoring sammelt metrics (Messwerte) und logs (Protokolle) von verschiedenen Ressourcen und Diensten, um Einblicke in deren Zustand und Verhalten zu erhalten.
Metrics sind Variablen, die den Zustand oder die Leistung eines Systems messen, z.B. CPU-Auslastung, Speicherverbrauch, Netzwerkverkehr, Anzahl von Anfragen, ...

__CloudWatch__
Amazon CloudWatch ist ein Überwachungs- und Managementdienst, der Monitoring in AWS-Ressourcen, Anwendungen und Dienste bietet.   
CloudWatch sammelt Metriken (metrics) und Protokolle (logs). Sobald eine Metric einen bestimmten Schwellenwert überschreitet, kann CloudWatch Alarm auslösen, um Administratoren zu benachrichtigen oder automatisierte Aktionen auszuführen.
Ein Dashboard in CloudWatch ist eine visuelle Darstellung von Metriken und Logs.   

__CloudTrail__
AWS CloudTrail ist ein Service, der die Aktivitäten und API-Aufrufe in einem AWS-Konto protokolliert.   
CloudTrail ermöglicht die Nachverfolgung von Änderungen, die an Ressourcen vorgenommen wurden, und unterstützt die Sicherheits- und Compliance-Anforderungen.   
CloudTrail speichert Protokolle in S3 Buckets, die für die Analyse und Überprüfung von Aktivitäten verwendet werden können.   

#### Compliance (Einhalten von Vorschriften)
Compliance bezieht sich auf die Einhaltung von gesetzlichen, regulatorischen und organisatorischen Anforderungen in Bezug auf Sicherheit, Datenschutz und Governance.   
AWS bietet eine Vielzahl von Compliance-Zertifizierungen und -Berichten, die Unternehmen dabei unterstützen, ihre eigenen Compliance-Anforderungen zu erfüllen.   
AWS unterstützt Standards wie ISO 27001, SOC 1/2/3, PCI DSS, HIPAA und GDPR (DSGVO).

#### Governance (Führung)
Control Tower ist ein Service, der Unternehmen dabei unterstützt, ihre AWS-Umgebungen zu verwalten und zu steuern.
