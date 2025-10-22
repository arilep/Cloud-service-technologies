## Lab Debriefing: IAM and Security

## I. AWS Lab

- Labrassa keskityttiin Identity and Access Management (IAM) palveluun ja sen kautta tapahtuvaan käyttöoikeuksien hallintaan.
- Labrassa oli valmiiksi luotuja käyttäjiä ja ryhmiä. Käyttäjille määritettiin käyttöoikeuksia ryhmien kautta.
- Lopuksi testattiin eri käyttäjien käyttö- ja pääsyoikeuksia AWS-konsolissa.

Console Home -aloitusnäkymä

<img width="1918" height="607" alt="image" src="https://github.com/user-attachments/assets/7c472469-55ff-43b1-ace4-85d85b2e3f61" />

### Task 1: Explore the Users and Groups

IAM Dashboardissa oli valmiiksi luodut käyttäjät user-1, user-2 ja user-3.

<img width="1625" height="417" alt="image" src="https://github.com/user-attachments/assets/e6b4e50d-f494-4e08-8e51-36d1d5422fd1" />

Käyttäjien Summary -ikkunasta nähdään oleellisia tietoja:

- ARN-tunniste
- Onko monivaiheinen tunnistautuminen käytössä
- Avaimet (Access Key)
- Käyttäjän luonti pvm
- Viimeisin sisäänkirjautuminen

Access management > User groups löytyi valmiiksi luodut ryhmät:

<img width="1625" height="275" alt="image" src="https://github.com/user-attachments/assets/609eb89c-6ca6-487e-9be3-483743e3db16" />

Jokaiselle ryhmälle oli ennalta määritetyt käyttöoikeuspolitiikat. Nämä tiedot olivat nähtävissä jokaisen ryhmän 'Permissions' -välilehden alta.

EC2-Admin ryhmällä oli kahdesta muusta ryhmästä poiketen määriteltynä inline policy -politiikka, ryhmällä oli hallintaoikeudet EC2-palveluun.

### Task 2: Add Users to Groups

Seuraavaksi tehtävänä oli liittää jokainen käyttäjä omaan ryhmäänsä seuraavasti:

    user-1 --> S3-Support
    user-2 --> EC2-Support
    user-3 --> EC2-Admin

Käyttäjän liittäminen ryhmään tapahtui navigoimalla:

    Access management > User groups > Group > Users > Add users

Esimerkiksi käyttäjän User-1 liittäminen S3-Support -ryhmään:

<img width="1899" height="492" alt="image" src="https://github.com/user-attachments/assets/c3dad839-55c2-4aa0-b549-995f6ed7de6c" />

Lisäyksen jälkeen käyttäjät perivät kyseisen ryhmän oikeudet. Aiemman esimerkin user-1 lisättynä S3-Support ryhmään:

<img width="1614" height="478" alt="image" src="https://github.com/user-attachments/assets/97ec5872-6305-40a5-ae50-929983ab52e6" />

Users -näkymästä voidaan nähdä mihin ryhmään käyttäjä kuuluu ja mitkä politiikat käyttäjää koskevat:

<img width="1610" height="503" alt="image" src="https://github.com/user-attachments/assets/b744c6cb-4144-46ee-8869-ad94295faab2" />

### Task 3: Sign-In and Test Users

Lopuksi testattiin kaikkien käyttäjien oikeudet.

    user-1 - S3-Support

    - Käyttäjällä päästiin siirtymään S3-consoleen
    - EC2-consoleen käyttäjällä ei ollut oikeuksia ("You are not authorized to perform this operation")

    user-2 - EC2-Support

    - Käyttäjällä oli näkyvissä EC2-instanssit LabHost ja Bastion Host
    - Käyttäjällä oli vain lukuoikeudet (Read Only), joten sillä ei pystynyt pysäyttämään instansseja
    - Käyttäjällä ei ollut pääsyä S3-consoleen

    user-3 - EC2-Admin

    - Käyttäjällä aiemmin mainitut EC2 palvelun hallintaoikeudet
    - Käyttäjällä pystyttiin pysäyttämään LabHost instanssi (Instance state --> Stop instance)

### Omia huomioita

- Käyttöoikeuksien määrittely oli hyvin samankaltaista kuin Microsoft Active Directory:ssä
- Viimeisessä testausvaiheessa ilmeni hyvin vähimpien oikeuksien periaate (principle of least privilege)
- Käyttäjien lisääminen ryhmiin helppoa ja nopeaa
- Navigointi AWS-lab ympäristössä oli myös helppoa ja selkeää

### Lab tulokset

<img width="608" height="563" alt="image" src="https://github.com/user-attachments/assets/5b15de48-eb07-473a-bc25-d3b0c7b36e79" />

## II. Azure Lab

- Labrassa keskityttiin Role-Based Access Control (RBAC) malliin
- Labrassa määritettiin rooli käyttäjälle, muokattiin roolia PowerShell:ssä ja testattiin käyttäjän oikeuksia

Tehtävänä oli määrittää käyttäjälle Dev1-55768804@cloudslice.onmicrosoft.com Network Contributor -rooli resurssiryhmään AZ900RGlod55768804.

Roolin määrittäminen eteni seuraavasti:

    1. Navigoitiin ensin Resource groups (Resource Manager) ja valittiin resurssiryhmä AZ900RGlod55768804.
    2. Navigointipalkista siirryttiin Access controliin (IAM).
    3. Alasvetovalikosta 'Add' siirryttiin roolin lisäämiseen 'Add role assignment'.
    4. Hakukentästä haettiin kaivattu rooli 'Network Contributor'.
    5. 'Add role assignment' -ikkunasta haettiin käyttäjä jolle rooli lisätään.
    6. Summary -ikkuna ja vahvistus. Ruudulle tuli ilmoitus joka kertoi roolin lisäyksestä.

Tämän jälkeen käyttäjän käyttöoikeuksia (Network Contributor) testattiin luomalla uusi virtuaaliverkko VNET1.

<img width="936" height="451" alt="image" src="https://github.com/user-attachments/assets/7b3f0717-3068-44a7-8999-3ddf692a0a7a" />

Seuraavaksi käynnistettiin Azure Cloud Shell (PowerShell) ja luotiin uusi rooli (custom role)

PowerShelliin syötettiin seuraava komento:

    Get-AzProviderOperation "Microsoft.Compute/virtualmachines/*" | FT Operation, Description -AutoSize

Jonka jälkeen haettiin ja tallennettiin rooli JSON-tiedostoon:

    Get-AzRoleDefinition -Name "Virtual Machine Contributor" | ConvertTo-Json | Out-File $home\clouddrive\VMOperatorRole.json

Tiedostoon tehtiin seuraavat muutokset:

    Name: Virtual Machine Operator
    ID property: Rivi poistettiin kokonaan
    IsCustom property: Arvo muutettiin false --> true
    Kuvaukseen vaihdettiin: "Lets you view, start and stop virtual machines."
    Tiedostoon jätettiin vain seuraavat toiminnot:
    "Microsoft.Compute/*/read"
    "Microsoft.Compute/virtualMachines/start/action"
    "Microsoft.Compute/virtualMachines/deallocate/action".
    
Tämän jälkeen rooli luotiin ajamalla komento:

    New-AzRoleDefinition -InputFile $home\clouddrive\VMOperatorRole.json

### Omia huomioita

- Kyseiset vaiheet vaativat käyttäjältä enemmän osaamista kuin AWS -harjoituksessa (mm. PowerShellin käyttö).
- Navigointi Azure ympäristössä ei ollut yhtä selkeää.
- Harjoitus oli aikarajattu (30min), mikä teki yhtäaikaisesta työskentelystä ja raportoinnista haastavaa.

## Lab tulokset

<img width="529" height="684" alt="image" src="https://github.com/user-attachments/assets/e13affa6-9834-4639-8a20-688801550328" />

### III. Write a comparison between AWS and Azure laboratories for each indicated laboratory pair

- Kummassakin korostuu vähimpien oikeuksien periaate (principle of least privilege), kuten testit osoittivat.
- Politiikat ja roolit JSON-pohjaisia, rakenteet melko samanlaisia
- Kumpikin ympäristö tukee sekä omia että muokattuja (custom) rooleja.
- AWS ympäristössä käyttöoikeuksien määrittely tapahtui politiikkojen (ryhmien) kautta, Azure ympäristössä ne määritettiin roolien kautta.
- AWS ympäristössä navigointi oli huomattavasti helpompaa kuin Azure ympäristössä (ainakin noviisille).

Vastaavuuksia

    AWS              Azure
    ---              -----
    IAM              Azure Active Directory
    IAM roles        Role assignments
    IAM policies     Role definitions
