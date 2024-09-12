# h4 Maailma kuulee

Tehtäviä Tero Karvisen kurssille Linux Palvelimet 2024. https://terokarvinen.com/linux-palvelimet/

---

## x) Lue ja tiivistä

Susanna Lehto 2022: Teoriasta käytäntöön pilvipalvelimen avulla (h4). https://susannalehto.fi/2022/teoriasta-kaytantoon-pilvipalvelimen-avulla-h4/

- a: Kuinka hankitaan DigitalOceanilta palvelin ja Namecheapilta domainnimi hyödyntäen GitHub Educationin krediittejä. Lisäksi kuinka domainnimi saadaan osoittamaan virtuaalipalvelimelle.
- d: Kirjautuminen virtuaalipalvelimelle ensimmäistä kertaa, päivitykset ja palomuurin asentaminen.
- e: Uusi pääkäyttäjä virtuaalipalvelimelle, juuren lukitseminen, virtuaalipalvelimen päivittäminen, Apachen asentaminen, testisivu.
- f: Palvelimen päivitykset

Karvinen 2012: First Steps on a New Virtual Private Server – an Example on DigitalOcean and Ubuntu 16.04 LTS. https://terokarvinen.com/2017/first-steps-on-a-new-virtual-private-server-an-example-on-digitalocean/

- paikkoja vuokrata virtuaalipalvelin
- muista hyvä salasana alusta alkaen
- ensimmäinen kirjautuminen uudelle virtuaalipalvelimelle, palomuuri, sudo käyttäjä, sulje root, päivitä
- muista tehdä reikä palomuuriin
- ip-osoitteen lisäksi nimi on kiva eli vuokraa sellainen

## a) Oma virtuaalipalvelin

*Tehtävä: Vuokraa oma virtuaalipalvelin haluamaltasi palveluntarjoajalta. (Vaihtoehtona voit käyttää ilmaista kokeilujaksoa, GitHub Education krediittejä; tai jos mikään muu ei onnistu, voit kokeilla ilmaiseksi vagrant:ia paikallisesti. Suosittelen kuitenkin harjoittelemaan oikeilla, tuotantoon kelpaavilla julkisilla palveluilla).*

*To 12.9.2024 klo 14.35*

Hain maanantaina GitHub Educationin etuja. Hakemukseni hyväksyttiin, mutta etujen luvataan olevan käytettävissä "kohta". Eli en pysty hyödyntämään tätä etua tässä kohtaa.

Opettaja suositteli tunnilla vaihtoehtoina DigitalOceania, Linodea ja UpCloudia. DigitalOceanista näimme tunnilla käytännön esimerkin ja samoin x-kohdan tiivistystehtävässä oli käytetty DigitalOceania. Jotta saan vähän laajempaa kuvaa aiheesta, perehdyn ensisijaisesti jompaan kumpaan muista vaihtoehdoista.

Linode mainostaa uusien asiakkaiden saadan sadan dollarin edestä ilmaisia krediittejä ja samoin UpCloudilla on ilmainen testijakso. Kävi ilmi, että UpCloud on suomalainen firma (https://www.finder.fi/IT-palvelut/UpCloud+Oy/Helsinki/yhteystiedot/2617969), joten päätin kannattaa kotimaista.

Hyvin nopeasti kävi ilmi, että UpCloudin ilmainen kokeilujakso tarkoittaa kolmea ilmaista päivää. Sattumalta päädyin kuitenkin Redditin kautta artikkeliin (https://techblog.nexxwave.eu/benchmark-between-cloud-servers-january-2024/), jossa arvosteltiin ei palveluita ja heidän linkkinsä kautta voisi saada 25 ilmaista euroa palvelun käyttöön.

Klikkasin yllä mainitun sivuston linkin kautta ja rekisteröidyin UpCloudin sivulle. Minulle tarjotaan edelleen kolmen päivän ilmaista kokeilujaksoa ja tämän lisäksi minulla näyttää olevan tililläni luvatut 25 euroa. Sivulla ei ainakaan vielä näy, onko näillä euroilla jotain erääntymispäivää.

![image](https://github.com/user-attachments/assets/40567c24-4261-4f0b-b9d8-a117d3f9b23a)

Olin saanut sähköpostiin ohjeet palvelun käytön aloittamiseksi:

![image](https://github.com/user-attachments/assets/74236e7b-17a9-4b0b-97c5-a501ff7c21f9)

Ensinnä siis pitää aloittaa ilmaisjakso. Tässä kohtaa pyydettiin luottokorttitietoja, jotka annoin.

![image](https://github.com/user-attachments/assets/feb646b5-1722-4b16-b878-59686d4c1b93)

Vahvistettuani korttitietoni ilmainen kokeilujakso alkoi:

![image](https://github.com/user-attachments/assets/e78b9fff-60b2-4231-9553-b8e98ee3c7d8)

Jotain rahaa tosin ilmeisesti täytyy antaa, sillä sivusto ilmoittaa, että kokeilujaksolla on rajoitteita ja tietoni häviävät kolmen päivän päästä, jos en ole käyttänyt rahaa:

![image](https://github.com/user-attachments/assets/67a1105f-3500-435d-af02-7119677753da)

Sivusto kehotti ottamaan käyttöön kaksivaiheisen tunnistautumisen, joten lisäsin sivuston Google Authenticatoriini.

Ilmaisjakson rajoitteet ovat nämä, en

![image](https://github.com/user-attachments/assets/ccc4b342-c9e9-4d6f-b4b0-4850c99e789e)

Lue ja tiivistä -kohdan materiaaleissa mainittiin portit 22 ja 80. En tiedä tuottaako se ongelmia, että kokeilujaksolla portin 22 liikenne on vain yksisuuntaista. Pidän tämän mielessä ja katson, kuinka käy.

Seuraavaksi ohjesähköpostissa oli kohta Deploy your first cloud server, joka vei aiheeseen liittyvälle ohjesivulle: https://upcloud.com/resources/tutorials/deploy-server. Sivun perusteella klikkailin itseni Servers-sivustolle, josta löytyi kohta Deploy New Server.

![image](https://github.com/user-attachments/assets/75a3756e-67bb-4ed9-9297-4de36d1c05c4)

Tunnilla kerrottiin, että sijainti kannattaa ottaa niin läheltä asiakasta kuin mahdollista ja että EU-maat ovat hyviä valintoja EU:n sääntelyn takia. Koska UPCloud on suomalainen palvelu, saan valita jopa kahden kotimaisen vaihtoehdon väliltä:

![image](https://github.com/user-attachments/assets/af36e6e4-c691-4891-8397-3314a9f1caa8)

Oppitunnilla sanottiin, että kannattaa valita halvin vaihtoehto, jossa on gigatavu ram-muistia. Eli tämän perusteella kolmen euron vaihtoehto kuulostaa hyvältä.

![image](https://github.com/user-attachments/assets/5b36c132-bb9c-4b72-b7fa-aa5873eff558)

Seuraaville kohdille en tehnyt mitää, sillä tunnilla kerrottiin, ettei ekstrasta kannata maksaa, sillä varmuuskopiot täytyy joka tapauksessa ottaa itse.

![image](https://github.com/user-attachments/assets/c2b83bd3-a3e0-46a6-b076-ace34db4fbcc)

Käyttöjärjestelmäksi valitsin Debianin.

![image](https://github.com/user-attachments/assets/672d5a50-9e23-420c-8f89-59304eeb9f5d)

Seuraaville valinnoille en tehnyt mitään. Klikkasin Utility networkin linkkiä ja sivulla kerrottiin, että kaikki käyttäjän palvelimet on yhdistettu "utility networkiin", joka yhdistää kaikkia yrityksen palvelinkeskuksia. Tämä takaa nopean yhteyden palvelinten välillä.

![image](https://github.com/user-attachments/assets/47cdbf60-7a66-4c37-8738-b0cf383b4167)

Myöskään seuraaviin en tehnyt muutoksia ja sivusto kertoi, että Metadata Servicen pitää olla päällä valitsemassani kokonaisuudessa.

![image](https://github.com/user-attachments/assets/150161e2-470e-48c5-8cf2-1a8716077a0a)

Tunnilla kerrottiin, että SSH olisi parempi vaihtoehto, mutta koska emme vielä osaa tätä, voimme valita salasanan. Tässä kohtaa ongelmaksi tuli se, että sivusto ilmoitti, etten voi valita salasanaa kyseisen käyttöjärjestelmän version kanssa.

![image](https://github.com/user-attachments/assets/149dd5d9-e3bf-45a9-8a59-32b04c40e851)

Joudun siis omatoimisesti perehtymään SSH-salaukseen. Tämä lienee hyvä hetki pitää ruokatauko.


**Lähteet**

-Finder: UpCloud Oy. https://www.finder.fi/IT-palvelut/UpCloud+Oy/Helsinki/yhteystiedot/2617969
- Karvinen 2012: First Steps on a New Virtual Private Server – an Example on DigitalOcean and Ubuntu 16.04 LTS. https://terokarvinen.com/2017/first-steps-on-a-new-virtual-private-server-an-example-on-digitalocean/
- Karvinen, Tero: Oppitunti 11.9.2024. Linux-palvelimet. https://terokarvinen.com/linux-palvelimet/
- Lovet, Kris. Benchmark between cloud servers (January 2024). (https://techblog.nexxwave.eu/benchmark-between-cloud-servers-january-2024/)
- Susanna Lehto 2022: Teoriasta käytäntöön pilvipalvelimen avulla (h4). https://susannalehto.fi/2022/teoriasta-kaytantoon-pilvipalvelimen-avulla-h4/
- UpCloud 23.4.2024: How to deploy a new Cloud Server. https://upcloud.com/resources/tutorials/deploy-server
- UpCloud: Documentation. https://upcloud.com/docs/products/networking/features/utility-network/


---
  
*Tätä dokumenttia saa kopioida ja muokata GNU General Public License (versio 2 tai uudempi) mukaisesti. http://www.gnu.org/licenses/gpl.html*

*Pohjana Tero Karvinen 2012: Linux kurssi, http://terokarvinen.com*

*Raportin tekijä: Jenni Muhonen*
