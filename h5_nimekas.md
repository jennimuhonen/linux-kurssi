# h5 Nimekäs

Tehtäviä Tero Karvisen kurssille Linux Palvelimet 2024. https://terokarvinen.com/linux-palvelimet/

---

## Rauta ja OS

**Virtuaalikoneella pyörivän Linuxin tiedot**

- Käyttöjärjestelmä: Debian 12.6.0 AMD64
- Virtualisointi: VirtualBox 7.0.20
- Muisti: 4096 MB
- Prosessorit: 4 CPU
- Virtuaalilevyn maksimikoko: 60 GB, josta käytetty 14,13 GB

**Taustajärjestelmän tiedot**

- Pöytäkone
- Käyttöjärjestelmä: Windows 11 Education, 64 bittinen käyttöjärjestelmä, x64-suoritin
- CPU: AMD Ryzen 5 7600 3.8 GHz 6-Core Processor
- Emolevy: MSI PRO B650-P WIFI
- Muisti: 32 GB DDR5-6000 CL30
- SSD: 2 TB, jossa vapaata tilaa 974 GB
- Näytönohjain: AMD RX 6800 XT 16 GB

## a) Kotisivu

*Tehtävä: Kotisivu. Tee vähintään kolmen erillisen weppisivun kotisivu ja kopioi se näkymään palvelimellesi. Jos sinulla on oikea palvelin Internetissä, kannattaa käyttää sitä. Käytä name based virtual hosting tekniikkaa. Sivujen muokkaamisen pitää onnistua ilman pääkäyttäjän oikeuksia, niiden kopioiminen pääkäyttäjänä testisivun paikalle ei käy. Kotisivujen ei tarvitse olla hienoja, mutta niiden tulee olla validia HTML:ää ja linkittää toisiinsa.*

Aloitin tehtävän teon lukemalla aiempaa raporttiani (https://github.com/jennimuhonen/linux-kurssi/blob/main/h3-hello-web-server.md), jossa opettelin käyttämään name based virtual hostingia ilman pilvipalvelinta. Lisäksi tarkistin kyseisessä tehtävässä käytetyn opettajan ohjeistuksen (https://terokarvinen.com/2018/04/10/name-based-virtual-hosts-on-apache-multiple-websites-to-single-ip-address/)

**Sivuhuomioita**

Toinen taustatyö jonka tein, oli Windows-puolen sijaan siirtää mahdollisimman paljon tarvittavia sivuja Linuxin puolelle, jotta voisin kopioida ohjeista koodeja suoraan terminaaliin sen sijaan, että kirjoittaisin niitä käsin. Työntekoani on jatkuvasti hidastanut erilaiset kirjoitusvirheet, joita on helppo vähentää kirjoittamalla koodeja vähemmän käsin. Koska käsin kirjoittaminen on johtunut kahden eri käyttöjärjestelmän käyttämisestä, pyrin vähentämään tätä.

Pari ongelmaa, joihin törmäsin, mutta joita en kokonaan ratkonut:

- Virtuaalisen käyttöjärjestelmän maksimikoko on  1920x1200, kun taas näyttöni on 2560x1440. Löysin tähän mahdollisen ratkaisun (https://www.reddit.com/r/virtualbox/comments/ra8cvc/is_there_a_way_to_set_guest_resolution_to/?rdt=44017) eli säätää VirtualBoxin puolelta Debianin asetuksia kohdasta Display -> Screen ja nostaa Video Memoryn määrää.
- En pikaisella googletuksella löytänyt yhtä tehokasta ruutukaappausmenetelmää, kuin mitä käytän Windowsin puolella.

**Varsinaiseen asiaan**

*19.9.2024 17.24*

Aivan aluksi syötin varalta komennon `sudo apt-get update`, jos päädyn asentamaan mitään. Ja tämän jälkeen ryhdyin seuraamaan edellä mainittua opettajan ohjeistusta uuden name based virtual hostin tekemiseen.

![image](https://github.com/user-attachments/assets/0f6ad50c-5d99-4fe1-80e4-0df3f7d399fe)

![image](https://github.com/user-attachments/assets/8d93ab77-2fd7-4531-b030-f613764f42b1)

Tässä kohtaa aloin muistelemaan, kuuluuko minun tehdä samanlainen tiedosto myös pääsivustani jennimuhonen.com. Tutkin mitä tein kahdessa edellisessä raportissani ja tulin siihen tulokseen, että tällä hetkellä pääsivua on muokattu vain sudo-käyttäjänä, mutta koska sivua tulee pystyä muokkaamaan myös ilman pääkäyttäjän oikeuksia, edellisellä kerralla tekemäni ei vielä riitä.

![image](https://github.com/user-attachments/assets/e2d9c6b4-ab8b-4325-8bf2-b12057dd283e)

![image](https://github.com/user-attachments/assets/5b259b73-3019-4175-8d95-22e56add6eba)

Kokeilin voiko kaikki kolme sivustoa oikeuttaa kerralla ja kyllä pystyi. Lisäksi käynnistin Apachen uudestaan.

![image](https://github.com/user-attachments/assets/26f91119-856c-4052-b215-81a84f5431d8)

Nyt minun pitäisi pystyä luomaan verkkosivuja ilman sudoa.

**Välitutkimus**

Kävin tässä vaiheessa tutkimassa, miltä sivusto näyttää verkkoselaimessa:

![image](https://github.com/user-attachments/assets/a7dcd13a-d137-4d94-a102-dac862e8af5d)

![image](https://github.com/user-attachments/assets/1eb66a6f-f183-4135-81dd-7fd93182481f)

jennimuhonen.com:sta katosi edellisellä kerralla tekemäni testisivu, mutta sivu näkyi, kun syötin ip-osoitteen. Tämä vaatii hieman lisätutkimusta, jotta hahmotan, mitä edellä tein. (Raporttia kolme tekiessä kaikki oli niin uutta ja kyseisellä viikolla aikaa oli tavallista vähemmän, joten silloin en pysähtynyt ihmettelemään samaan tapaan.)

Tutkin mitä komentoja olen antanut. Kun viime viikolla (raportti 4) loin testi-sivun automaattisen sivun sijalle, käytetyn komennon perusteella sivu tallentui var-kansion alle. Seikkailin kansiossa ja löysin kansiorakenteen syvyyksistä index.html-tiedoston, joka näkyy edelleen, kun sivustolle pyrkii ip-osoitteella. 

![image](https://github.com/user-attachments/assets/a4b44586-0b00-4d99-9e30-75d6f07952bf)

Conf-tiedosto viittaa hakemistoon, joka on kansiossa jemjem/publicsites, mutta sellaista kansiota ei vielä ole, koska en sitä ole luonut:

![image](https://github.com/user-attachments/assets/57f4b60e-3359-47c0-bb66-310b6edb2956)

Eli kysymykseksi jää, miksi ip-osoite ohjaa eri paikkaan kuin domain? Hain esimerkit vielä curlilla varmistaakseni, ettei kyse ollut vain selaimen välimuistista:

![image](https://github.com/user-attachments/assets/926ec309-ea0b-434d-b9ae-327f7542a7da)

Ja hain host-komennolla vielä domainin tiedot, kuten tunnilla opin:

![image](https://github.com/user-attachments/assets/9f80587f-a5e5-4c8d-bfc0-c82325532114)

Googletin asiaa ja Webmasters-sivustolla olleen vastauksen (https://webmasters.stackexchange.com/questions/113237/why-does-typing-in-my-sites-ip-address-bring-up-a-different-site) perusteella tulkitsin, että http://jennimuhonen.com yhdistää sekä ip-osoitteeseen, että Host: jennimuhonen.com. Ip-osoite sen sijaan lähettää Host: 94.237.16.92. Tässä tapauksessa serveri ei välttämättä tiedä, minkä sivuston tarjoaisi, jolloin se voi palauttaa default-sivuston. Eli default-sivu lienee se var-kansion uumenissa oleve index.html, jonka ip-osoite löytää, kun varsinaista sivua ei ole olemassa.

**Takaisin varsinaiseen aiheeseen**

*19.9.2024 19.31 (tauon ja asioiden ihmettelyn jälkeen)*

Jatkoin opettajan ohjeiden seuraamista ja ilmeisestikin olen jotain mokannut jossain vaiheessa, sillä tulos on edelleen sama kuin aiemminkin:

![image](https://github.com/user-attachments/assets/fd6b0aec-e5b0-4b0b-bb57-d4bee2a8b8c1)

Vertailuna kokeilin, mitä portfolio-sivu sanoo curlilla. Tämän sivun virheilmoitus on erilainen:

![image](https://github.com/user-attachments/assets/4d49224c-ba7c-42a0-864d-4db6b44f71fe)

Päätin kokeilla tehdä tälle sivulle loputkin toimet ja katsoa, käykö sen kanssa eri lailla.

![image](https://github.com/user-attachments/assets/e1277e6c-a800-47a1-9619-3d301c2318f1)

Tälläkin sivulla virheilmoitus pysyi samana. Onko tässä jotain viivettä vai olenko tehnyt jonkin virheen?

*19.9.2024 20.25*

Googletin asiaa (https://stackoverflow.com/questions/18447454/apache-giving-403-forbidden-errors)
 ja päädyin sen myötä tutkimaan Apachen virhelokia:

![image](https://github.com/user-attachments/assets/63b3272c-2b56-4d6f-ade7-3a11c9a1558b)

Googletin virheilmoituksen koodilla AH00035 ja esimerkiksi Linux Mint Forumsilla on ongelmasta keskustelua (https://forums.linuxmint.com/viewtopic.php?t=176598). Eli kuten ilmoituksessakin itsessään lukee, ongelmana on puutteelliset oikeudet. Ratkaisuksi tarjotaan komentoa chmod +x. Toisessa keskustelussa (https://askubuntu.com/questions/1353377/apache2-permission-denied-access-to-denied-because-search-permissions-are-mi) komento on sanottu selkeämmin chmod +x /home/username.

DebianWikissä (https://wiki.debian.org/Permissions) kerrotaan, että chmod:lla voidaan manipuloida tiedostojen oikeuksia. AskUbunto-sivustolla (https://askubuntu.com/questions/443789/what-does-chmod-x-filename-do-and-how-do-i-use-it) selitettiin tarkemmin, että +x komennon perässä tekee sen, että siihen annetaan suoritusoikeudet.

Eli kokeilen, auttaisiko komento `chmod +x /home/jemjem/publicsites`.

![image](https://github.com/user-attachments/assets/d665ffe3-d8da-4362-bc05-9cf1302f504d)

Ei ainakaan suorilta auttanut. Tosin tutkin mitä tarkoittaa domainin TTL-kohdassa oleva aika ja Cloudflare Docs:n (https://developers.cloudflare.com/dns/manage-dns-records/reference/ttl/) tämä tarkoittaa Time to Live eli kuinka kauan kestää, että tietueiden päivitykset saavuttavat loppukäyttäjän. Eli varmaan aivan heti mitään muutosta ei kuulukaan nähdä.

Luin vielä tarkemmin Linux Mint Forumsin keskusteluketjua ja siellä annettiin ohje, että oikeudet kannattaa antaa myös kansioille /home ja /home/user. Tein näin ja lopulta sivu alkoi toimia:

![image](https://github.com/user-attachments/assets/dd162a94-fe20-4288-b10f-d43663ac753e)

Sensijaan portfolio-sivulla on jokin muu ongelma:

![image](https://github.com/user-attachments/assets/f9014ef4-6c20-4a22-9f8e-dd66358d2478)

Johtuisikohan tämä virhe siitä, etten ole vielä tehnyt seuraavassa tehtävissä eteen tulevia toimenpiteitä.

Katsoin Youtubesta Nerd on the Street:n videota (https://www.youtube.com/watch?v=x5fWSWdM4F8) ja sen perusteella arvelen, että en vielä tässä kohtaa oleta, että mitään on pielessä portfolio-sivulla ja vasta jos se ei toimi alidomainin tekemisen jälkeen, huolestun.

Nyt on aika siis viilata sivujen html tehtävänannon mukaiseksi ja tehdä tutkimusmatka-sivustolle samat toimet kuin muillekin.

Seuraavaksi aloin askartelemaan html:n kanssa. Ohessa päätin muuttaa portfolio-sivuston nimeksi linux.

![image](https://github.com/user-attachments/assets/3a2aaf53-b314-4497-aebf-d1386fb5d1be)

Muokkasin myös conf-tiedostoa:

![image](https://github.com/user-attachments/assets/ec5e3c3e-5e8a-47f8-b0df-c362f2ad3159)

Tämän jälkeen palasin viilaamaan sivustojen html:ää:

![image](https://github.com/user-attachments/assets/1550f18c-0db2-4633-b436-bf7a716c3493)

![image](https://github.com/user-attachments/assets/91983f8d-2ee1-46f1-a5a2-6830765d92fd)

Lopuksi validoin sivustojen html:n (https://validator.w3.org) opettajan ohjeista löytyneen linkin kautta.

![image](https://github.com/user-attachments/assets/8d0eddda-730d-464c-99c4-c92a174f3033)

Pääsivu ja tutkimusmatka olivat kunnossa, mutta linux-sivulta validaattori löysi typon, jota en ollut huomannut, kun en ollut päässyt näkemään sivustoa selaimessa. Korjasin virheen. 

## b) Alidomain

*Tehtävä: Alidomain. Tee kaksi uutta alidomainia, jotka osoittava omaan koneeseesi. Esimerkiksi palvelu on example.com -> linuxkurssi.example.com. Tee toinen alidomain A-tietueella ja toinen CNAME-tietueella. Alidomainit ovat tyypillisesti ilmaisia, kun sinulla on päädomain (example.com).*

*20.9.2024 n. 10.30*

Aloitin perehtymällä aiheeseen. DNSimplen sivuilla (https://support.dnsimple.com/articles/differences-a-cname-records/) selitetään tiiviisti A recordin ja CNAME recordin ero. A record osoittaa nimen suoraan IP-osoitteeseen eli esimerkiksi jennimuhonen.com osoittaa ip-osoitteeseen 94.237.16.92. CNAME record puolestaan osoittaa nimestä toiseen nimeen. Eli esimerkiksi voisin laittaa tekemäni sivun tutkimusmatka.jennimuhonen.com osoittamaan aiemmin kurssityönä tekemääni githubissa olevaan verkkosivuun.

Halusin nähdä käytännössä miten näitä tietoja muokataan, joten katsoin Tony Teaches Techin videon (https://www.youtube.com/watch?v=ZXCQwdVgDno) aiheesta. Hänen ohjeidensa perusteella suuntasin Namecheepin sivuille kokeilemaan asiaa käytännössä.

Kokeilin ensin tehdä molemmille alidomaineille A-tietueet:

![image](https://github.com/user-attachments/assets/00cda459-378a-4a6d-97d7-2787cd98c95c)

Pidin pienen tauon ennen kuin kokeilin, ovatko sivut lähteneet toimimaan.

Molemmat alidomainit toimivat, mutta molemmissa on korjattavaa:

![image](https://github.com/user-attachments/assets/e60e97c5-8a32-473f-96a8-750fac05300c)

Linux-sivussa on jotain pielessä, sillä se näyttää Testi-sivun. Tarkistan aiemmin tekemäni muutoksen etsiäkseni tekemääni virhettä. Tutkimusmatka-sivun html:ää taas voisi vähän viilata, mutta viilaamisen sijaan kokeilen ohjata kyseisen alidomainin osoittamaan suoraan varsinaiselle github-sivulle.

![image](https://github.com/user-attachments/assets/5578227b-775b-4677-9ea8-d47f6230fb45)

Jouduin hetken hakemaan sitä, missä muodossa github-sivun osoite kuului antaa. lopun / ja alun https:// täytyi ottaa pois, jotta osoite hyväksyttiin.

Osoite osoittautui virheelliseksi:

![image](https://github.com/user-attachments/assets/e4c5cb51-40ac-4c33-ae2d-e7de6a09037b)

Eli seuraavaksi pitää 1. selvittää kuinka ohjaus github-sivuille kuuluu tehdä ja 2. selvittää linux-sivun ongelmaa. 

Katsoin jälleen Tony Teaches Techin videon (https://www.youtube.com/watch?v=EX4w9hsduNA) ja kävi ilmi, että tein asian aivan väärin. En voinut vain iskeä satunnaista github-sivua osoittamaan omalle sivulleni, vaan githubin päähän pitää antaa käyttämäni domain ja Namecheapin puolelle taas pitää laittaa muutama ip-osoite. Videota katsoessa muistin myös, että minun olisi pitänyt antaa myös www:t aiemmin tekemiini A-tietueisiin.

Korjasin puuttuvat www-tiedot:

![image](https://github.com/user-attachments/assets/2dadc0d1-5bfe-4cbd-ac23-abd383c68b5a)

**Github-seikkailu vailla onnellista loppua**

*20.9.2024 13.11 (tauon jälkeen)*

Katsomani video-ohje on vuodelta 2021 ja Githubin sivut ovat luultavasti muuttuneet sen jälkeen, sillä en löytänyt videolla nähtyä kohtaa. Vaihdoin sen sijaan lukemaan Githubin ohjeita (https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/managing-a-custom-domain-for-your-github-pages-site). Vilkaisin ohjeita jo aiemminkin, mutta nyt kun minulla olen videomuodossa saanut yleiskäsityksen siitä mitä olen tekemässä, on pelkkiin tekstiohjeisiin helpompi tarttua.

Ohjeet ohjasivat ensiksi vahvistamaan domainin Github-sivuille (https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/verifying-your-custom-domain-for-github-pages), jotta joku muu ei pysty ottamaan sivustoani haltuun. Kun vahvista päädomainin, vahvistuvat samalla myös kaikki mahdolliset alidomainit.

Menin Githubin sivuilla asetuksiin ja sivupalkin kohdasta Code, Planning, and Automation alta löytyi Pages. Klikkasin sitä ja syötin domainin:

![image](https://github.com/user-attachments/assets/80622309-2274-43e6-aa25-6dfa7f09648f)

Sen jälkeen minun täytyy vahvistaa domain Githubille suorittamalla vaadityt toimet:

![image](https://github.com/user-attachments/assets/f48c9ec8-afd3-4dab-8e09-682b8dae6d73)

Tein ensin uuden A-tietueen Githubin pyytämällä nimellä:

![image](https://github.com/user-attachments/assets/3541d49f-3ba7-49b9-8a67-c1eb2876dc35)

En ole varma mitä kohtia voisin hypätä ohjeessa tarkistussivua tehdessä, joten noudatin ohjeita:

![image](https://github.com/user-attachments/assets/296215d8-a4c7-419a-b0bc-170dc2929c40)

Kuitenkin Apachea uudelleen käynnistäessä sain virheilmoituksen, jossa kehotettiin tarkistamaan systemctl:ää. Kurkistin ensin virhelokia, mutta siellä ei näkynyt mitään ja sen jälkeen laitoin ohjeessa pyydetyn komennon. Näyttää siltä, että tekemässäni conf-tiedostossa on jotain pielessä:

![image](https://github.com/user-attachments/assets/ba6124f0-3826-4534-ade5-104d2491bd1e)

![image](https://github.com/user-attachments/assets/e9789cfa-2068-49e7-8963-5fcc9d6491a0)

(Laitettuani komennon systemctl status apache2.service en löytänyt enää takaisin aiempiin komentoihin muuten kuin history:n kautta, joten en voinut raportoida tarkemmin tekemääni tai saamaani virheilmoitusta enää tässä vaiheessa.)

Tulkitsin, että rivillä kahdeksan viitataan conf-tiedoston riviin kahdeksan:

![image](https://github.com/user-attachments/assets/918784e5-6794-4280-a2bb-6775af6e2518)

Kyseinen rivi on tiedoston viimeinen rivi ja siinä itsessään ei ole mitään vikaa eli oletan, että vika on jossain muualla sisällössä. Kun tarpeeksi pitkään tuijotin, löysin lopulta virheen ensimmäiseltä riviltä, siellä oli ylimääräinen <-merkki.

Korjattuani virheen, uudelleenkäynnistin Apachen onnistuneesti:

![image](https://github.com/user-attachments/assets/b117584c-9f7a-4975-baea-9c83c2e664b5)

Historystä voi myös todeta, että käytin a2ensite-komentoa myös linux-sivuun, sillä arvelin unohtaneeni tehdä tämän. Olin oikeassa, sillä tämän jälkeen sivu alkoi toimimaan:

![image](https://github.com/user-attachments/assets/9d1bf8ac-0cc7-4bb4-8784-ea9e2cf0bd1b)

Tässä kohtaa toivoin, että olisin googlettanut aiemmin, mutta edellisen voinee ottaa harjoituksena ja sain ainakin korjattua linux-sivun. Googletin siis lopulta termin DNS TXT record ja Cloudflaren sivuilta (https://www.cloudflare.com/learning/dns/dns-records/dns-txt-record/) opin, että tämän avulla voin syöttää tekstiä suoraan Domain Name Systemiin eli DNS. TXT record on siis tyyppi, jonka voin valita suoraan namecheapin sivulta, minun ei kuulunut askarrella mitään apacheen:

![image](https://github.com/user-attachments/assets/4e7241eb-a119-4af7-acf0-352f98b568d3)

Lisättyäni yllänäkyvän tiedon ja odotettuani hetken klikkasin Verify Githubin sivuilla ja prosessi oli suoritettu:

![image](https://github.com/user-attachments/assets/1d4c5bb9-87bd-495f-9c76-7e135ed4318d)

Palasin takaisin Githubin verifiointiohjeeseen, jossa sanotaan, että TXT record kannattaa pitää DNS configuraatiossa, jotta domain pysyy verifioituna. Tämän jälkeen palasin alkuperäiseen Github-ohjeeseen.

Tämän jälkeen ohjeen mukaan tuli lisätä A-tietueena Githubin antamat ip-osoitteet. Tässä kohtaa aloin miettimään, kumpi minun oikeastaan tulisi verifioida jennimuhonen.com vai tutkimusmatka.jennimuhonen.com. Kokeilin molempia vaihtoehtoja sekä githubin verifioinnin puolella sekä A recordina. Kumpikaan ei toiminut ja sekä sivu jennimuhonen.com että tutkimusmat.jennimuhonen.com pysyivät entisellään. Videolla ei tarvinnut tehdä muuta ja toki olisi mahdollista, että muutos ei vielä ollut aktiivinen, mutta tässä kohtaa huomasin alkaa miettimään, että luultavasti esimerkiksi conf-tiedostossa olevat tiedot ovat ristiriidassa nyt yrittämäni kanssa ja ongelma on luultavasti jossain siellä päässä. Haluaisin myös oikeastaan ensisijaisesti siirtää verkkosivujen materiaalit palvelimen puolelle pelkän sivun uudelleenohjauksen sijaan, joten päätin, ettei minulla ollut nyt aikaa selvittää tätä ongelmaa enempää, koska olin eksynyt sivupoluilla varsinaisesta tehtävänannosta.



---
**ToDo-lista**

- poista turhaan tehdyt githubin verifiointisivun tiedot
- opettele siirtämään sivun sisältö omalle palvelimelle sen sijaan, että ohjaan sivun githubiin

**Selvittämättömät ongelmat**

- Mikä meni pieleen Github-kokeilun kanssa

---

**Lähteet**

- Alex Coventry 6.12.2021 & Archathean_Official 10.11.2022. Reddit-kommentit. https://www.reddit.com/r/virtualbox/comments/ra8cvc/is_there_a_way_to_set_guest_resolution_to/?rdt=44017
- Ask Ubuntu: Apache2 Permission denied - access to / denied because search permissions are missing on a component of the path. https://askubuntu.com/questions/1353377/apache2-permission-denied-access-to-denied-because-search-permissions-are-mi
- Ask Ubuntu: What does "chmod +x <filename>" do and how do I use it? https://askubuntu.com/questions/443789/what-does-chmod-x-filename-do-and-how-do-i-use-it
- CloudFlare: What is a DNS TXT record? https://www.cloudflare.com/learning/dns/dns-records/dns-txt-record/
- Debian Wiki: Permissions. https://wiki.debian.org/Permissions
- DNSimple Support: Differences Between A and CNAME Records. https://support.dnsimple.com/articles/differences-a-cname-records/
- Github Docs: Managing a custom domain for your GitHub Pages site. https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/managing-a-custom-domain-for-your-github-pages-site
- Github Docs: Verifying your custom domain for GitHub Pages. https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/verifying-your-custom-domain-for-github-pages
- Karvinen, Tero 2018: Name Based Virtual Hosts on Apache – Multiple Websites to Single IP Address. https://terokarvinen.com/2018/04/10/name-based-virtual-hosts-on-apache-multiple-websites-to-single-ip-address/
- Karvinen, Tero: Oppitunti 18.9.2024. Linux-palvelimet. https://terokarvinen.com/linux-palvelimet/
- Linux Mint Forums: [SOLVED][Apache2] AH00035: access to / denied. https://forums.linuxmint.com/viewtopic.php?t=176598
- Muhonen, Jenni 2024: h3 Hello Web Server. https://github.com/jennimuhonen/linux-kurssi/blob/main/h3-hello-web-server.md
- Muhonen, Jenni 2024: h4 Maailma kuulee. https://github.com/jennimuhonen/linux-kurssi/blob/main/h4_maailma_kuulee.md
- StackOverflow: Apache giving 403 forbidden error. https://stackoverflow.com/questions/18447454/apache-giving-403-forbidden-errors
- Tony Teaches Tech 27.4.2021: How to Use a Custom Domain with GitHub Pages. https://www.youtube.com/watch?v=EX4w9hsduNA
- Tony Teaches Tech 19.8.2021: What are CNAME records? (and how they compare to DNS A records). https://www.youtube.com/watch?v=ZXCQwdVgDno
- Webmasters: Why does typing in my site's IP address bring up a different site? https://webmasters.stackexchange.com/questions/113237/why-does-typing-in-my-sites-ip-address-bring-up-a-different-site


---
  
*Tätä dokumenttia saa kopioida ja muokata GNU General Public License (versio 2 tai uudempi) mukaisesti. http://www.gnu.org/licenses/gpl.html*

*Pohjana Tero Karvinen 2012: Linux kurssi, http://terokarvinen.com*

*Raportin tekijä: Jenni Muhonen*
