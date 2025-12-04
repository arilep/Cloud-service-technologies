## Lab Debriefing: Compute

## I. AWS Lab

### What was specifically done in the lab?

Harjoituksessa luotiin vaiheittain virtuaalipalvelinympäristö Amazonin EC2 -palveluun. 

- Tarkasteltiin EC2-instanssin monitorointi työkaluja.
- EC2-instanssi käynnistettiin ja suojattiin siten, että sitä ei vahingossa poisteta tai pysäytetä (Termination protection, Stop protection).
- Määriteltiin user data -skripti instanssille, joka asentaa, käynnistää ja ajaa Apache weppi palvelimen ja luo yksinkertaisen weppi sivun.
- Vaihdettiin instanssityyppi ja kasvatettiin EBS -volyymin kokoa.
- Perehdyttiin EC2:n rajoituksiin ja testattiin Stop Protection -asetuksen toimivuutta.

### Identify what cloud services you used during the lab?

- EC2 - virtuaalipalvelimen luomisessa ja hallinnassa
- EBS - root -tallennustila
- CloudWatch - instanssin monitoroinnissa
- Service Quotas - sisälsi aluekohtaiset resurssirajoitukset
- Security Groups - palomuuri määritykset
- Virtual Private Cloud - templatesta luotu VPC labraa varten

### What technical details did you learn from the lab about each cloud services used?

- Termination protection ja Stop protection -määritysten avulla voidaan suojata instanssia tahattomalta poistamiselta/pysäyttämiseltä.
- HTTP liikenne (portti 80) erikseen sallittava, jotta käyttäjät voivat päästä sivustolle.
- Instanssityypin ja EBS-volyymin koko on helposti säädettävissä (pl. volyymin koon laskeminen).
- User Data -skripteillä voidaan automatisoida esimerkiksi palvelimen asennus jo instanssin käynnistysvaiheessa.

### AMI Quickstart -imaget:

<img width="1058" height="458" alt="image" src="https://github.com/user-attachments/assets/f4f5ae0e-e38a-47ad-b495-793abbf5255c" />

### Instanssin summary -osio:

<img width="536" height="736" alt="image" src="https://github.com/user-attachments/assets/120a14df-1ce0-47d6-87f4-aab54b08a807" />

### Monitorointi:

<img width="1869" height="379" alt="image" src="https://github.com/user-attachments/assets/54945eec-8d6c-460b-8256-a6cf560da2c8" />

### HTTP-liikenteen salliminen:

<img width="1645" height="374" alt="image" src="https://github.com/user-attachments/assets/c2610c61-6bd6-4e69-acf8-a0ed91bf5eb3" />

### Verkkosivustolla vierailu HTTP-liikenteen sallimisen jälkeen:

<img width="550" height="190" alt="image" src="https://github.com/user-attachments/assets/05f2fb8f-c9ea-46dc-9298-4981d0340e5f" />

### Labra harjoituksen tulokset:

<img width="590" height="413" alt="image" src="https://github.com/user-attachments/assets/3febede9-c110-431e-8b10-9c7ff253d625" />

## II. Azure Lab

### What was specifically done in the lab?

Tässä harjoituksessa tehtiin määritykset Azure Cloud Shelliä varten, luotiin Azure virtuaalikone (Azure VM) Azure Command Line Interfacella (Azure CLI) ja asennettiin Nginx -weppi palvelin.

Virtuaalikoneen luominen ja konfiguraatiot:

    az vm create \
    --resource-group myRGKV-lod57393285 \
    --name my-VM-57393285 \
    --image Ubuntu2204 \
    --admin-username azureuser \
    --generate-ssh-keys

Nginx palvelimen konfiguraatiot virtuaalikoneelle:

    az vm extension set \
    --resource-group myRGKV-lod57393285 \
    --vm-name my-VM-57393285 \
    --name customScript \
    --publisher Microsoft.Azure.Extensions \
    --version 2.1 \
    --settings '{"fileUris":
    ["https://raw.githubusercontent.com/MicrosoftDocs/mslearn-welcome-to-azure/master/configure-nginx.sh"]}' \
    --protected-settings '{"commandToExecute": "./configure-nginx.sh"}'

### Identify what cloud services you used during the lab?

- Azure Virtual Machine
- Azure CLI
- Azure CloudShell
- Custom Script Extension

### What technical details did you learn from the lab about each cloud services used?

- Vaadittavat konfiguraatiot voidaan ajaa joko Azure portalissa, Azure CLI:ssä, Azure PowerShell:ssä tai Azure Resource Managerissa.
- Custom Script Extensionin avulla voidaan ajaa Bash skriptiä virtuaalikoneelle

### Comparison between AWS and Azure laboratories

Azuren puolella vaadittiin enemmän teknistä osaamista, sillä labran vaiheet suoritettiin suurelta osin komentorivityökalujen avulla. AWS puolella hyödynnetään taas käyttäjäystävällisempää graafista hallintakonsolia.

Suurimmat erot labrojen välillä:

| Aihe | Amazon AWS | Microsoft Azure |
| ---------- | ---------- | ---------- |
| Virtuaalipalvelin | EC2 | Azure Virtual Machine |
| Automatisointi | User Data | Custom Script Extension |
| Käytetetty weppi palvelin | Apache | Nginx |
| Hallinta | GUI Management Console | Azure Portal, Azure CLI |


