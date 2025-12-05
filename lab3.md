## Lab Debriefing: Networking

## I. AWS Lab

### What was specifically done in the lab?

Harjoituksessa luotiin Virtual Private Cloud (VPC) ympäristöineen.

- Ympäristöön luotiin sekä yksityisiä että julkisia aliverkkoja, jotka sijaitsivat kahdessa eri Availability Zonessa.
- Määritettiin reititystaulut, NAT Gateway, Internet Gateway.
- User data skriptillä konfiguroitiin EC2 -instanssista weppi palvelin.

### Virtual Private Cloud -konfiguraatio:

<img width="490" height="608" alt="image" src="https://github.com/user-attachments/assets/2b8d49f5-be10-45b3-8f4b-69ee02498c95" />

<img width="491" height="561" alt="image" src="https://github.com/user-attachments/assets/a17c463f-5222-4402-96ba-ac706dc0e3b3" />

<img width="494" height="653" alt="image" src="https://github.com/user-attachments/assets/e162e527-c950-4d45-97e8-458a9e3b1f39" />

### VPC resurssit ja konfiguraatio alussa:

<img width="790" height="363" alt="image" src="https://github.com/user-attachments/assets/2b823437-bfca-4a41-a335-c45de0df36d5" />

### Julkiset ja yksityiset aliverkot kahdessa eri Availability Zonessa:

<img width="797" height="368" alt="image" src="https://github.com/user-attachments/assets/ee3b24ce-74c7-4335-85e9-aef3e324e54b" />

### Lopullinen arkkitehtuuri, jossa toimii virtuaalinen palomuuri (Security Group)

<img width="825" height="373" alt="image" src="https://github.com/user-attachments/assets/7c4b9a3e-cc40-4473-94fd-a56360a38c2c" />

### Identify what cloud services you used during the lab?

- Amazon AWS Management Console - Hallintanäkymä
- Amazon VPC - Virtual Private Cloud ympäristön luominen
- Amazon EC2 - Virtuaalipalvelimen luominen ja ajaminen
- Amazon EC2 Security Groups - Virtuaalipalomuurin asettaminen


### What technical details did you learn from the lab about each cloud services used?

- Aliverkkojen ip-osoiteavaruus määritettiin CIDR lohkoilla
- Security Group toimii virtuaalisena palomuurina (firewall)
- Aliverkko sijaitsee aina tietyssä Availability Zonessa
- Private Subnet saadaan pidettyä yksityisenä, kun liikenne reititetään NAT Gatewayn kautta eikä Internet Gatewayn kautta

### Labra harjoituksen tulokset:

<img width="580" height="401" alt="image" src="https://github.com/user-attachments/assets/ae0eaae8-d121-4f16-a539-233f21ddcc47" />


## II. Azure Lab

### What was specifically done in the lab?

- Tehtiin määritykset Azure Cloud Shelliä varten
- Luotiin virtuaalikone
- Haettiin virtuaalikoneen julkinen IP-osoite ja testattiin yhteyttä weppi palvelimeen
- Määritettiin uusi palomuuri sääntö joka sallii sisääntulevan HTTP-liikenteen porttiin 80
- Testattiin että weppipalvelimen weppi sivu aukeaa

### Lopulliset palomuuri-säännöt:

<img width="753" height="172" alt="image" src="https://github.com/user-attachments/assets/df4fb7a9-9311-4386-8b13-587cfbe42fc9" />

### Sivustoon saadaan yhteys portin 80 avaamisen jälkeen:

<img width="618" height="154" alt="image" src="https://github.com/user-attachments/assets/a45da315-31a3-4479-a539-33247ce7c417" />

### Identify what cloud services you used during the lab?

- Azure Portal - hallinta
- Azure VM - virtuaalikoneet
- Azure Cloud Shell - komentorivityökalu
- Azure Storage Account - tallennus
- Network Security Group - palomuurisäännöt

### What technical details did you learn from the lab about each cloud services used?

- Network Security Group vastaa AWS:n Security Groupia käytännössä.
- Network Security Groupissa käytetään prioriteetteja (lukuja), pienin luku saa suurimman prioriteetin ja suoritetaan ensin.
- Oletuksena virtuaalikoneelle on sallittu vain SSH (portti 22).

### Comparison between AWS and Azure laboratories

- Sama kuin aiemmissa labra harjoituksissa; Azuren puolella käytetään pääosin komentorivityökaluja (haastavampi) kun taas AWS puolella graafista hallintakonsolia (aloittelijaystävällisempi).
- HTTP-liikenne (portti 80) on oletuksena (default) suljettuna ja täytyy erikseen avata kummassakin ympäristössä.
- Palomuuri säännöissä Azurella on prioriteetti -järjestelmä, jota AWS:stä ei löydy.

| Aihe | Amazon AWS | Microsoft Azure |
| ---------- | ---------- | ---------- |
| Virtuaalipalvelin | EC2 | Azure Virtual Machine |
| Käytetetty weppi palvelin | Apache | Nginx |
| Hallinta | GUI Management Console | Azure Portal, Azure CLI |
| Palomuuri säännöt | Inbound Rule | NSG Rule |
