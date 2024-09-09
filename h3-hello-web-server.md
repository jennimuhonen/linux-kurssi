# h3 Hello Web Server

Tehtäviä Tero Karvisen kurssille Linux Palvelimet 2024. https://terokarvinen.com/linux-palvelimet/

---

## x) Lue ja tiivistä

**Apache: Name-based Virtual Host Support**
- IP-based virtual hosts: jokaisella täytyy olla oma ip-osoite
- Name-based virtual hosts: voivat jakaa saman ip-osoitteen
- Jälkimmäiseen tarvitaan vähemmän ip-osoitteita, joita on rajatusti
- Tätä kannattaa käyttää, jos ei ole erityistä tarvetta ip-pohjaiseen ja harvemmin on


**Karvinen: Name Based Virtual Hosts on Apache – Multiple Websites to Single IP Address**
- Apachen avulla voi saada monta verkkotunnusta (domain name) yhdelle IP-osoitteelle
- Komennot verkkopalvelimen asentamiseksi ja konfiguroimiseksi
- Komennot uuden nimeen pohjautuvan virtual hostin lisäämiseksi
- Komennot siihen, kuinka voi luoda verkkosivun normaalina käyttäjänä sekä  komennot testaamiseen 


**Lähteet:**
- The Apache Software Foundation 2023: Apache HTTP Server Version 2.4 Documentation: Name-based Virtual Host Support. https://httpd.apache.org/docs/2.4/vhosts/name-based.html
- Karvinen 2018: Name Based Virtual Hosts on Apache – Multiple Websites to Single IP Address. https://terokarvinen.com/2018/04/10/name-based-virtual-hosts-on-apache-multiple-websites-to-single-ip-address/


## Rauta ja OS

**Virtualisoidun Linuxin tiedot**

- Käyttöjärjestelmä: Debian 12.6.0 AMD64
- Virtualisointi: VirtualBox 7.0.20
- Muisti: 4096 MB
- Prosessorit: 4 CPU
- Virtuaalilevyn maksimikoko: 60 GB, josta käytetty 13,92 GB

**Taustajärjestelmän tiedot**

- Pöytäkone
- Käyttöjärjestelmä: Windows 11 Education, 64 bittinen käyttöjärjestelmä, x64-suoritin
- CPU: AMD Ryzen 5 7600 3.8 GHz 6-Core Processor
- Emolevy: MSI PRO B650-P WIFI
- Muisti: 32 GB DDR5-6000 CL30
- SSD: 2 TB, jossa vapaata tilaa 967 GB
- Näytönohjain: AMD RX 6800 XT 16 GB


## a) Testaa

*Tehtävä: Testaa, että weppipalvelimesi vastaa localhost-osoitteesta. Asenna Apache-weppipalvelin, jos se ei ole jo asennettuna.*

*9.9.2024 10.45*

Asensin Apachen luennon aikana, joten aloitan testaamalla.

Kuten luennolla neuvottiin, kirjoitin selaimen osoitekenttään localhost ja sain Apachen oletussivun näkyviin:

![image](https://github.com/user-attachments/assets/6a95bea9-c723-402b-b6f7-5fe906ff15fc)

Näyttäisi siis hyvältä. Testatasin vielä myös komentorivin puolella kehoitteella `curl localhost`, johon myös tutustuttiin tunnilla.

![image](https://github.com/user-attachments/assets/8d427ff2-62b4-44cd-9b4a-66c134da2e96)

Tälläkin puolella näyttää hyvältä, ja <title>-kohdassa nähdään sivun nimi It works, joka nähtiin myös selaimen puolella.


## b) Etsi lokista

*9.9.2024 n. klo 11*

*Tehtävä: Etsi lokista rivit, jotka syntyvät, kun lataat omalta palvelimeltasi yhden sivun. Analysoi rivit (eli selitä yksityiskohtaisesti jokainen kohta ja numero, etsi tarvittaessa lähteitä).*

Kurssisivulla vinkataan komennot `sudo tail /var/log/apache2/access.log`, `sudo tail /var/log/apache2/error.log`, joten näillä varmaankin pääsen haluttuihin lokeihin käsiksi. Tutkin asiaa.

Ensimmäisellä komennolla saadaan seuraavanlaista tietoa:

![image](https://github.com/user-attachments/assets/0e7fdc70-f85e-413f-a44c-6562c59055ad)

Ja jälkimmäisellä seuraava:

![image](https://github.com/user-attachments/assets/460cb920-ff23-40d1-b7fb-e9b83ae296fb)

Seuraavaksi perehdyin aiheeseen lisää, jotta osasin tulkita näkemääni.

Apachen sivujen (https://httpd.apache.org/docs/current/logs.html) mukaan pääsyloki (access log) tallentaa kaikki pyynnöt, jotka serveri on prosessoinut. Virheloki (error log) puolestaan on sivuston mukaan tärkein lokitiedosto. Apache lähettää tänne diagnostiikkatietoja ja kirjaa kohtaamansa virheet. Jos kohtaa ongelman serverin käynnistämisessä tai operoinnissa, niin täältä kannattaa tarkistaa ensimmäisenä.

Komennoilla hain siis pääsylokin ja virhelokin.

**Pääsyloki**

Tässä uudestaan pääsylokin kuvakaappaus:

![image](https://github.com/user-attachments/assets/1719de4b-283a-44bb-9a8c-b5e9b8775254)

Pääsylokien aivan alussa on IP-osoite eli 127.0.0.1. Arvelin, että luennolla oli ehkä puhetta localhostin IP-osoitteesta ja ainakin muutamassa tunnilta ottamassani ruutukaappauksessa näkyy sama IP-osoite. Selvitin asian (https://whatismyipaddress.com/localhost) ja kyseessä on tosiaan localhostin IP-osoite.

Ayooluwa Isaiahin (https://betterstack.com/community/guides/logging/how-to-view-and-configure-apache-access-and-error-logs/) mukaan IP-osoitteen perässä olevat kaksi viivaa ovat placeholdereita, ensimmäinen on "remote log name (name used to log in a user)" ja jälkimmäinen "remote username (username of logger-in user)" ja jos näitä ei ole asetettu, tilalla on -. 

Seuraavana on päiväys ja kellonaika. Päiväys on sekä pääsylokissa että virhelokissa tälle päivälle, mutta kellonajat ovat pääsylokin ja virhelokin puolella noin 15 minuutin erotuksella toisistaan. Pääsylokia tarkemmin tarkastelemalla totesin, että siinä on kuvattu edellisen tehtävän toiminnot. Tehtävässä kirjoitin komentoriville `curl localhost` ja hain Firefox-selaimella saman sivun.

*Huomio: Hämmensin itseäni sillä, että olin kirjannut tekemäni toimet edelliseen tehtävään eri järjestykseen kuin lokissa näkyy. Tästä opin, että on tärkeää kirjoittaa raporttiin asiat oikeaan järjestykseen, jotta jos jälkikäteen asioihin joutuu palaamaan, on tulkinta helpompaa. Samoin unohdukseni kirjata kellonaika tämän tehtävän alkuun lisäsi haasteita arvioida lokien kellonaikoja.*

Eli päiväys ja kellonaika ovat se aika, jolloin olen tehnyt komennot. Lokiin on kirjautunut se hetki, kun olen hakenut sivuston tiedot komentorivillä ja verkkoselaimessa ja määritetään vielä se, millä aikavyöhykkeellä käytetty kellonaika on.

"GET / HTTP/1.1" tarkoittaa Ayooluwa Isaiahin mukaan pyynnön metodia, reittiä ja protokollaa. 200 on vastauksen koodi ja 10956 / 3380 on vastauksen koko bitteinä. "-" on viittaajan URL-osoite, jos tarjolla tai muuten placeholderina on jälleen -. Viimeisenä on yksityiskohtaista tietoa pyynnön tehneestä "user agent of the client".


**Virheloki**

Tässä uudestaan virhelokin kuvakaappaus:

![image](https://github.com/user-attachments/assets/bffabe54-b497-41d0-bb3c-509328d816de)

Apachen sivuston (https://httpd.apache.org/docs/current/logs.html) kuvaa virhelokin sisältöä seuraavasti:

- ensimmäisenä lokitiedossa on viestin päiväys ja aika
- seuraavana on moduuli, joka tuottaa viestin
- kolmantena prosessin ID ja mahdollisesti "thread ID"
- neljäntenä "client address", joka teki pyynnön
- viimeisenä tarkka virheviesti

Tarkasteltavassa virhelokissa ensimmäisenä on siis viestin päiväys ja aika. Päiväys on tälle päivälle ja kellonaika on kymmenen minuuttia ennen kuin aloitin tekemään testausta tehtävässä a. Oletan, että kyseessä on suunnilleen kellonaika, jolloin olen tänään käynnistänyt Debianin. Sekunnin murto-osissa on kahdessa lokissa eroa.

Seuraavaksi ovat viestin tuottaneet moduulit, jotka on molemmat merkktty ilmoituksiksi (notice). Apachen toisella sivulla (https://httpd.apache.org/docs/current/mod/directive-dict.html) kerrotaan, että:

- MPM: tulee sanoista Multi-Processing Module 
- Core: keskeisimpiä Apachen osia ja aina käytettävissä.

Eric Stackifyn sivulla (https://stackify.com/apache-error-log-explained/) toteaa, että notice tarkoittaa normaalia, mutta merkittävää tilaa.

[pid 749:tid 749], joka on molemmissa lokeissa, on prosessin id ja myös mahdollisesti "thread ID". Eli molemmissa on sama prosessi id sekä thread id 749.

Client address on Apachen (https://httpd.apache.org/docs/current/logs.html) sivujen esimerkissä hakasuluissa. Tällaista tietoa ei lokeissa ollut näkyvillä. Ericin mukaan virhelokissa puuttuvat parametrit jätetään pois eli vaikuttaisi toimivan eri tavalla kuin pääsyloki, jossa puuttuvien tietojen tilalla oli -.

Viimeisenä on tarkka virheviesti. AH00489 vaikuttaisi olevan kyseisen viestin tunnus, koska keskustelupalstalla Nicola Urbinatin (https://talk.plesk.com/threads/apache-restarts-randomly.358945/) kuvakaappauksissa on sama koodi, kun virhelokin viesti on ilmoittanut "resuming normal operations". Kyseinen viesti vaikuttaisi kertovan, että Apache versionumerolla 2.4.62 ja joka pyörii Debianilla on konfiguroitu ja palaa normaaliin toimintaan. Eli käynnistettyäni Debianin, myös Apache on käynnistynyt.

Toinen viesti puolestaan kertoo, että komentoa /usr/bin/apache2 käytettiin. (Lähde: https://serverfault.com/questions/607873/apache-is-ok-but-what-is-this-in-error-log-mpm-preforknotice)

*(Lopetus klo 13.23.)*

*Kommentti 14.56: Tehtävässä näköjään ei olisikaan tarvinnut analysoida virhelokia, mutta tuskin työ hukkaan meni.*

## c) Etusivu uusiksi

*9.9.2024 14.50*

*Tehtävä: Etusivu uusiksi. Tee uusi name based virtual host. Sivun tulee näkyä suoraan palvelimen etusivulla http://localhost/. Sivua pitää pystyä muokkaamaan normaalina käyttäjänä, ilman sudoa. Tee uusi, laita vanhat pois päältä. Uusi sivu on hattu.example.com, ja tämän pitää näkyä: asetustiedoston nimessä, asetustiedoston ServerName-muuttujassa sekä etusivun sisällössä (esim title, h1 tai p).*

Etsin opettajan ohjesivulta (https://terokarvinen.com/2018/04/10/name-based-virtual-hosts-on-apache-multiple-websites-to-single-ip-address/) neuvoja tehtävän tekemiseen. Sieltä löytyy tällainen komento `$ echo "Default"|sudo tee /var/www/html/index.html`

Kokeilin:

![image](https://github.com/user-attachments/assets/3811de12-e7ba-49f8-bae9-b8545607e931)

Tarvitsin lisätietoa komennosta. Koska googlaamalla ei heti löytynyt suoraa selkeää vastausta, kysyin ChatGPT:ltä seuraavan kysymyksen: "Mitä tämä komento tekee: $ echo "Default"|sudo tee /var/www/html/index.html" ChatGPT kertoi, että `echo "Default"` tulostaa sanan Default ja että `echo`-komento tulostaa tekstin komentoriville. Putki lähettää komennon tulosteen seuraavan komennon syötteeksi. tee-komento lukee syotteen eli tässä tapauksessa "Default"-tekstin ja kirjoittaa sen tiedostoon eli `/var/www/html/index.html`.

Eli jos oikein ymmärsin, komennon olisi pitänyt korvata aiempi etusivun sisältö, mutta sivu näyttää edelleen samalta:

![image](https://github.com/user-attachments/assets/13012819-0642-4b41-94e5-b07b4382ce67)

Hetken ihmeteltyäni ymmärsin tarkistaa kirjoittamani komennon ja sieltä löytyi kirjoitusvirhe. Uusi yritys:

![image](https://github.com/user-attachments/assets/5a4aab15-54ac-4fa0-b8a8-2407ca7a498a)

Kokeillaan myös selaimessa:

![image](https://github.com/user-attachments/assets/0ea9286d-4ffe-472d-a515-a6e4fc419e8d)

Molempiin on nyt vaihtunut alkuperäisen tekstin sijalle pelkkä Default eli etusivun sisältö on muutettu.

Seuraavaksi opettajan ohjeessa lisätään uusi name based virtual host. Tehtävässä uuden sivun nimi on hattu.example.com.

ChatGPT avasi yllä komennon selkeästi, joten palasin ChatGPT:n äärelle ja kysyin "Mitä tämä komento tekee sudoedit /etc/apache2/sites-available/pyora.example.com.conf". ChatGPT:n mukaan komento avaa pyora.example.com konfiguraatiotiedoston muokattavaksi.

Muutin ohjeissa olevan pyora.example.com tilalle hattu.example.com ja katsoi, mitä tapahtuu.

Komento avasi tyhjän tiedoston muokattavaksi.

![image](https://github.com/user-attachments/assets/0c82f00b-6913-4be6-b7ba-b08db69ec344)

Suljin tiedoston tallentamatta, koska olin säätänyt jotain. Kokeilin pari kertaa uudestaan, kunnes löysin oikeat näppäimet, jolla tiedosto tallentui. Alkuun cat-komento ilmoitti, että tiedostoa ei ole ja kun lopulta tallensin tiedoston, komento ei näyttänyt mitään, koska tiedost oli tyhjä.

![image](https://github.com/user-attachments/assets/f45e8b97-1c5f-4db7-aaf4-20289e03930c)

Opettajan ohjesivulla cat-komento näytti tiedoston sisältä tietoja. Aiheuttiko säätäminen jotain ongelmia? Vai kuuluiko minun kirjoittaa cat-komennolla näkyvät tiedot itse tiedostoon?

Kokeilin molempia vaihtoehtoja, mutta ohjesivun seuraava vaihe, jossa pitäisi tehdä verkkosivu normaalina käyttäjänä, ei toimi kummallakaan tavalla. Jokin on ongelmana, mutta en tiedä mikä.

Ihmetellessä raportoinnista jäi jokunen ihmettely ja testikerta nyt välistä, tässä viimeisin. Kuten voi huomata, hattu.example.com oli jo aiemmin otettu käyttöön:

![image](https://github.com/user-attachments/assets/d1fb469e-e730-4be9-8ff2-8472024dc5c0)

Etsin lisätietoa. TechRepublic-kanavan ohjeiden (https://www.youtube.com/watch?v=_uZjqSyLWQM) perusteella tiedot tosiaan tuli itse laittaa tiedostoon. Näin olinkin jo tehnyt, kuten yllä olevasta kuvasta näkyy.

Jotain kuitenkin on vielä väärin, sillä ohjesivun se

Yksi ongelma ainakin oli, että seurasin liian kirjaimellisesti ohjetta. Vaihdoin xubuntun omaan käyttäjänimeeni.

![image](https://github.com/user-attachments/assets/0f26669a-3cc3-4cdc-80e7-c253c6d5fed1)

Käynnistin varalta apache2:n uudelleen. Ja kokeilin mkdir-komentoa uudestaan.

![image](https://github.com/user-attachments/assets/f4922fe1-1934-40bf-9ca0-1a88a79eae06)

Ja nyt ei enää tule virheilmoituksia, kun komennossa on oikeasti olemassa oleva käyttäjänimi.

Jatkoin opettajan ohjeiden mukaisesti:

![image](https://github.com/user-attachments/assets/2fb2662a-36be-4727-bda7-256097d850f3)

Ja kuten näkyy, päivitys onnistui ilman sudoa ja sivulla lukee nyt testi.


---

**Lähteet:**
- Apache: Log Files. https://httpd.apache.org/docs/current/logs.html
- Apache: Terms Used to Describe Directives. https://httpd.apache.org/docs/current/mod/directive-dict.html
- ChatGPT
- Eric, 17.3.2023: Apache Error Log Explained. https://stackify.com/apache-error-log-explained/
- Isaiah, Ayooluwa, 23.11.2023: How to View and Configure Apache Access & Error Logs. https://betterstack.com/community/guides/logging/how-to-view-and-configure-apache-access-and-error-logs/
- Karvinen, Tero: Linux Palvelimet 2024 alkuksyksy. https://terokarvinen.com/linux-palvelimet/
- Karvinen, Tero: Oppitunti 4.9.2024. Linux-palvelimet. https://terokarvinen.com/linux-palvelimet/
- Karvinen, Tero, 2018: Name Based Virtual Hosts on Apache – Multiple Websites to Single IP Address. https://terokarvinen.com/2018/04/10/name-based-virtual-hosts-on-apache-multiple-websites-to-single-ip-address/
- Nicola Urbinati: Apache restarts randomly. https://talk.plesk.com/threads/apache-restarts-randomly.358945/
- Serverfault: Apache is OK, but what is this in error.log - [mpm_prefork:notice]?. https://serverfault.com/questions/607873/apache-is-ok-but-what-is-this-in-error-log-mpm-preforknotice
- TechRepublic, 31.12.2020: Apache web server: How to install and configure a website. https://www.youtube.com/watch?v=_uZjqSyLWQM
- WhatIsMyIPAddress. https://whatismyipaddress.com/localhost

---
  
*Tätä dokumenttia saa kopioida ja muokata GNU General Public License (versio 2 tai uudempi) mukaisesti. http://www.gnu.org/licenses/gpl.html*

*Pohjana Tero Karvinen 2012: Linux kurssi, http://terokarvinen.com*

*Raportin tekijä: Jenni Muhonen*
