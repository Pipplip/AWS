## AWS Deployment Workflow mit Terraform, CI/CD und ECS

| Abkürzung | Bedeutung                                                                                                           |
| --- |---------------------------------------------------------------------------------------------------------------------|
| ECR | Amazon Elastic Container Registry (verwaltet unsere Docker Images)                                                  |
| ECS | Amazon Elastic Container Service (Container Orchestrierungsdienst, startet, skaliert und verwaltet unsere Container) |
| Cluster | Umgebung, in der mehrere Anwendungen oder Container gemeinsam verwaltet werden                                   |
 | VPC | Virtual Private Cloud (isolierte Netzwerkumgebung für unsere Infrastruktur)                                         |

**Vorgehensweise:**
1) Wir machen ein Merge Request im CE `tf-container-repositories` für ECR Repository, damit wir ein neues Repository für unseren Service bekommen.   
   Das Repository ist quasi die zentrale Anlaufstelle für die Docker Images unseres Services.   
   In diesem Merge Request definieren wir auch den Namen des Moduls    
   z.B. `module "test_management_tool_service"`

2) CE Team erstellt daraufhin ein leeres Backend, also ein S3 Bucket, IAM Permissions etc.   
   Als Antwort bekommen wir ein `state.tf`, also eine Backend Konfiguration.    
   Die sagt, wo Terraform den State speichern und lesen soll.   

3) Bei `terraform init` verbindet sich terraform mit diesem Backend

4) Wenn `terraform apply` ausgeführt wird, also Infrastruktur deployed, dann wird der `.tfstate` in dieses Bucket geschrieben.   
   Der Bucket hält quasi immer den letzten bekannten Zustand der Infrastruktur.

5) Im Projekt eines Services/Anwendung hat man zwei Ordner `/infrastructure` und `/deployment`   
   **infrastructure apply**       
   → erstellt Cluster / VPC / DB   
   → schreibt State in S3   

   **deployment apply**     
   → liest Outputs aus infra state   
   → deployed Apps in diese Infrastruktur    

6) Anwendung bauen/build:   
   Anwendung wird als Docker Image gebaut   

   Anwendung wird über die CI/CD Pipeline gepublished (also zu ECR hochgeladen) (AC-ADFS-Developers xxxx168910)   
   D.h. das Image ist jetzt zentral verfügbar    

   Deployment: in der Pipeline wird das neue Image in ECS ausgetauscht    

   **Kurz:**   
   Erst wird die Infrastruktur mit Terraform aufgebaut. (einmalig, oder bei Infrastruktur-Änderung)      
   Danach baut die CI/CD-Pipeline Docker Images, published sie in ECR und deployed sie auf ECS. (regelmäßig bei neuen Releases)    
   ECS tauscht daraufhin die laufenden Container gegen neue Container mit dem neuen Image aus.    

7) Verbindung zwischen `/infrastructure` und `/deployment` im Projekt:   
   Nachdem die Infrastruktur applied wurde, hat man die Outputs der Services.    
   Das Deployment lädt die Infrastruktur-Outputs per `terraform_remote_state` in `data.tf`    

   In `locals.tf` werden die remote-outputs in `local.service_infra` gepackt und aufbereitet.   

   Die Anwendung, also der Service wird in `Service.tf` definiert. Hier setzt man die Werte, die die Anwendung braucht.   

8) Fallbeispiel: Man hat einen neuen Service, der in die bestehende Infrastruktur eingebunden werden soll.   
   a - Im Workspace wo Infrastruktur definiert wird, muss ein neuer Zugriff definiert werden z.B: `resource "aws_security_group_rule" "allow_service_db"`   
   b - Im Workspace des neuen Services stellt man die Verbindung zur bestehenden Infra auf: `data "terraform_remote_state" "core_infra"`   
   c - Wenn man bestimmte Rechte und Rollen für die Services braucht, muss man diese in `/infrastructure` im neuen Service repo definieren. Meist in `iam.tf` und `security_groups.tf`   

   IAM definiert service-spezifische Rollen, z.B. Zugriff auf S3, Secret Manager etc.   

   Wenn man nicht genau weiß: Frag dich immer: „Gehört das NUR meinem Service?“   
