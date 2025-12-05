## Lab Debriefing: Networking

## I. AWS Lab

### Note

Labra harjoituksessa ilmeni ongelma (alla) jota en saanut korjattua, eikä siitä ollut ohjeissa mainintaa. Raportissa käsitelty vaiheet siten kuin ne olivat harjoituksen ohjeissa ja itse harjoitus niiltä osin kuin se oli mahdollista.

Ongelma jota en saanut korjattua: `Error: Failed to create 1 Scaling policy` > Diagnose with Amazon Q:

<img width="808" height="355" alt="image" src="https://github.com/user-attachments/assets/c0d27626-3ba7-43d7-a0b6-4cf75c1e3dac" />

### What was specifically done in the lab?

- Luotiin Amazon Machine Image valmiista instanssista
- Luotiin ja määritettiin Target group sekä Application Load Balancer
- Määritettiin Launch template auto scaling
- Kuormitettiin tarkoituksella Load Balanceria ja Auto Scalingia ja seurattiin kuinka ne toimivat
- Poistettiin lopuksi Web Server 1 -instanssi, jota oli käytetty AMI:n luomiseen

### Auto Scaling Group -määritykset:

### 1/5 Launch template:

<img width="1339" height="342" alt="image" src="https://github.com/user-attachments/assets/c74eadd4-b9c1-4725-87e4-e089ac467819" />

### 2/5 Instance launch options:

<img width="1319" height="505" alt="image" src="https://github.com/user-attachments/assets/b16eb462-11b1-400d-9a8d-adcd1f171e60" />

### 3/5 Integrate with other services:

<img width="1316" height="617" alt="image" src="https://github.com/user-attachments/assets/00f323ad-8c3a-4ead-a532-5afdd13ecdef" />

### 4/5 Configure group size and scaling policies:

<img width="1184" height="761" alt="image" src="https://github.com/user-attachments/assets/123b49d2-0865-4d04-bdeb-ac128968f244" />

### 5/5 Notifications and tags:

<img width="1347" height="337" alt="image" src="https://github.com/user-attachments/assets/a5f53c8c-8088-412b-9c2f-44c64d8e31cc" />

### Identify what cloud services you used during the lab?

- Amazon EC2
- Amazon Machine Image (AMI)
- Elastic Load Balancing (ELB)
- Auto Scaling
- CloudWatch

### What technical details did you learn from the lab about each cloud services used?

- Instansseja voidaan kopioida ja luoda AMI -imageista
- Load Balancerin ansiosta liikenne jaetaan instanssien kesken > vähentää kuormitusta
- CloudWatchin avulla voidaan seurata hälytyksiä

### Labra harjoituksen tulokset:

<img width="564" height="454" alt="image" src="https://github.com/user-attachments/assets/613cf617-ddec-4425-b013-90a32567f1d3" />
