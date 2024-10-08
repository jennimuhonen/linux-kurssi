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

Kävin tässä vaiheessa tutkimassa, miltä sivusto näyttää verkkoselaimessa.

Domain:

![image](https://github.com/user-attachments/assets/a7dcd13a-d137-4d94-a102-dac862e8af5d)

IP-osoite:

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

Ei ainakaan suorilta auttanut. Tosin tutkin mitä tarkoittaa domainin TTL-kohdassa oleva aika ja Cloudflare Docs:n (https://developers.cloudflare.com/dns/manage-dns-records/reference/ttl/) mukaan tämä tarkoittaa Time to Live eli kuinka kauan kestää, että tietueiden päivitykset saavuttavat loppukäyttäjän. Eli varmaan aivan heti mitään muutosta ei kuulukaan nähdä.

Luin vielä tarkemmin Linux Mint Forumsin keskusteluketjua ja siellä annettiin ohje, että oikeudet kannattaa antaa myös kansioille /home ja /home/user. Tein näin ja lopulta sivu alkoi toimia:

![image](https://github.com/user-attachments/assets/dd162a94-fe20-4288-b10f-d43663ac753e)

Sensijaan portfolio-sivulla on jokin muu ongelma:

![image](https://github.com/user-attachments/assets/f9014ef4-6c20-4a22-9f8e-dd66358d2478)

Johtuisikohan tämä virhe siitä, etten ole vielä tehnyt seuraavassa tehtävissä eteen tulevia toimenpiteitä.

Katsoin Youtubesta Nerd on the Street:n videota (https://www.youtube.com/watch?v=x5fWSWdM4F8) ja sen perusteella arvelen, että en vielä tässä kohtaa oleta, että mitään on pielessä portfolio-sivulla ja vasta jos se ei toimi alidomainin tekemisen jälkeen, huolestun.

Nyt on aika siis viilata sivujen html tehtävänannon mukaiseksi ja tehdä tutkimusmatka-sivustolle samat toimet kuin muillekin.

Seuraavaksi aloin askartelemaan html:n kanssa. Ohessa päätin muuttaa portfolio-sivuston nimeksi linux.

![image](https://github.com/user-attachments/assets/691b67e7-474c-4acf-a3fd-bbeb9e6dcfa4)

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

Molemmat alidomainit teoriassa toimivat, mutta molemmissa on myös korjattavaa. Linux-sivussa on jotain pielessä, sillä se näyttää Testi-sivun. Tarkistan aiemmin tekemäni muutoksen etsiäkseni tekemääni virhettä. Tutkimusmatka-sivun html:ää taas voisi vähän viilata, mutta viilaamisen sijaan kokeilen ohjata kyseisen alidomainin osoittamaan suoraan varsinaiselle github-sivulle.

![image](https://github.com/user-attachments/assets/e60e97c5-8a32-473f-96a8-750fac05300c)

Jouduin hetken hakemaan sitä, missä muodossa github-sivun osoite kuului antaa CNAME Recordiin. Lopussa oleva / ja alun https:// täytyi ottaa pois, jotta osoite hyväksyttiin:

![image](https://github.com/user-attachments/assets/5578227b-775b-4677-9ea8-d47f6230fb45)

Osoite osoittautui virheelliseksi:

![image](https://github.com/user-attachments/assets/e4c5cb51-40ac-4c33-ae2d-e7de6a09037b)

Eli seuraavaksi pitää 1. selvittää kuinka ohjaus github-sivuille kuuluu tehdä ja 2. selvittää linux-sivun ongelmaa. 

Katsoin jälleen Tony Teaches Techin videon (https://www.youtube.com/watch?v=EX4w9hsduNA) ja kävi ilmi, että tein asian aivan väärin. En voinut vain iskeä satunnaista github-sivua osoittamaan omalle sivulleni, vaan githubin päähän pitää antaa käyttämäni domain ja Namecheapin puolelle taas pitää laittaa muutama ip-osoite. Videota katsoessa muistin myös, että minun olisi pitänyt antaa myös www:t aiemmin tekemiini A-tietueisiin.

Korjasin puuttuvat www-tiedot:

![image](https://github.com/user-attachments/assets/2dadc0d1-5bfe-4cbd-ac23-abd383c68b5a)

**Github-seikkailu (tai sekoilu) jatkuu**

*20.9.2024 13.11 (tauon jälkeen)*

Katsomani video-ohje on vuodelta 2021 ja Githubin sivut ovat luultavasti muuttuneet sen jälkeen, sillä en löytänyt videolla nähtyä kohtaa. Vaihdoin sen sijaan lukemaan Githubin ohjeita (https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/managing-a-custom-domain-for-your-github-pages-site). Vilkaisin ohjeita jo aiemminkin, mutta nyt kun olen videomuodossa saanut yleiskäsityksen siitä mitä olen tekemässä, on pelkkiin tekstiohjeisiin helpompi tarttua.

Ohjeet ohjasivat ensiksi vahvistamaan domainin Github-sivuille (https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/verifying-your-custom-domain-for-github-pages), jotta joku muu ei pysty ottamaan sivustoani haltuun. Kun vahvistaa päädomainin, vahvistuvat samalla myös kaikki mahdolliset alidomainit.

Menin Githubin sivuilla asetuksiin ja sivupalkin kohdasta Code, Planning, and Automation alta löytyi Pages. Klikkasin sitä ja syötin domainin:

![image](https://github.com/user-attachments/assets/80622309-2274-43e6-aa25-6dfa7f09648f)

Sen jälkeen minun täytyi vahvistaa domain Githubille suorittamalla vaaditut toimet:

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

**CNAME record**

Koska Githubin kanssa oli liikaa haasteita, jatkoin CNAME-tietueen tekemisen kokeilua kahden alidomainin kesken. Lisäsin CNAME Recordin Namecheapiin tekemättä uutta alidomainia vielä Apachen puolella:

![image](https://github.com/user-attachments/assets/dd282e29-bd83-4cdf-8f35-17e640d6ef32)

Tämä näyttää riittävän ja matka.jennimuhonen.com:n sisältö on sama Github-ongelma kuin tutkimusmatka.jennimuhonen.com.

![image](https://github.com/user-attachments/assets/d17294a2-110b-4bf6-935f-aa5210b402a6)

Eli näyttää siltä, että CNAME recordia tehdessä minun ei tarvitse tehdä mitään Apachen puolella.

**A record, CNAME record jne**

Yritin lukea uudestaan Apachen dokumentaatiota name-based virtual hosteista (https://httpd.apache.org/docs/2.4/vhosts/name-based.html) ja vaikka sivun sisältö on nyt ymmärrettävämpää kuin silloin, kun sitä ensimmäisen kerran piti lukea, ei se edelleenkään avaa aihetta minulle tarpeeksi. Luin myös serveraliaksista (https://httpd.apache.org/docs/current/mod/core.html#serveralias) eli voisin conf-tiedostoon listata myös erilaisia aliaksia sivulle. Kuinka tämä eroaa CNAME:sta? Lisäksi Namecheapin puolella voisin lisätä ALIAS recordin. Miten tämä eroaa edellisistä?

DNSimplen sivuilla vertaillaan erilaisia tietuevaihtoehtoja (https://support.dnsimple.com/articles/differences-between-a-cname-alias-url/). Sivun mukaan A, CNAME, ALIAS ja URL ovat kaikki vaihtoehtoja, joilla osoittaa sivun host nimi, mutta näissä on pieniä eroavaisuuksia.

- A record: ohjaa ip-osoitteeseen
- CNAME record: nimestä nimeen - tätä tulisi käyttää vain, jos nimelle ei ole muita tietueita
- ALIAS record: nimestä nimeen - voi olla rinnakkaisia tietueita nimeen
- URL record: ohjaa nimen kohdenimeen käyttäyn HTTP 301 statuskoodia

Mysteeriksi jäi vielä, onko ALIAS record sama, jonka voisi määrittää myös conf-tiedostoon.

**Github-mysteeri**

*20.9.2024 joskus illalla*

Päätin vielä kokeilla Githubin kanssa. Githubin sivuilla kehotettiin verifioimaan pääsivu, joten verifioin jennimuhonen.com domainin. Tämän jälkeen tein alidomainille sivu A recordit neljään Githubin antamaan ip-osoitteeseen. Githubin sivuja tankkaamalla tajusin, että sivun verifiointia ei ollut näytetty ohjevideolla vaan halutun sivun osoite piti antaa aivan eri paikkaan. Olin mennyt sekaisin siinä, että olin mennyt Github-tilini asetuksissa Page-välilehdelle, mutta lisäksi täytyi mennä halutun repositorion asetusten Pages-välilehdelle ja lisätä Custom domain kohtaan haluttu domain. 

![image](https://github.com/user-attachments/assets/7f6b66b6-a1dc-40a7-88f3-9a16dfdd0a8a)

Tämän lisäksi Githubista saamani virheviestin perusteella tein cielä CNAME Recordin Namecheapin puolelle.

![image](https://github.com/user-attachments/assets/671a2caa-a1b0-42ab-a64f-78e1d3a20cc7)

Tämän jälkeen sivu alkoi toimimaan.

![image](https://github.com/user-attachments/assets/b2611ed3-5f9b-426d-9def-1bce35e16b27)

Apachen puolelle en ole syöttänyt mitään tietoja alidomainista sivu enkä tiedä olisiko tämä tarpeellista vai sekoaisiko sivu tästä.

**CNAME uudestaan**

*21.9.2024 n. 14*

Palasin CNAME-teeman pariin vielä uudestaan, sillä säädettyäni Github-sivun toimimaan ja siirrettyäni sen käyttämään osoitetta sivu.jennimuhonen.com ja vaihdettuani tutkimusmatka.jennimuhonen.com näyttämään alkuperäistä html-tiedostoa, CNAME record matka-sivulle hajosi.

Tutkin asiaa tekemällä CNAME recordin sivulle, josta ei ollut conf-tiedosta ja sivulle, josta oli. Kumpikaan ei toiminut, mutta virheet olivat erilaisia.

Sivu, josta ei ollut conf-tiedostoa ohjasi var-kansiossa olevaan tiedostoon. (Päivitin kyseisen tiedoston sisällön, kun törmäsin siihen jatkuvasti ja "Testi" ei tuntunut sopivalta.)

![image](https://github.com/user-attachments/assets/e4d09584-a614-456d-8818-52761d6be3bc)

Sivu, josta oli conf-tiedosto antoi virheilmoituksen:

![image](https://github.com/user-attachments/assets/e4f7cfbf-6ef0-4914-959b-b1cae92bebc8)

Testailu ei ollut riittävää ja pelkän Apachen name based -sivun tankkaaminen ei ollut riittävää, joten etsiydyin Youtubessa katsomaan Nerd on the Street:n videon Apache Virtual Hosts (https://www.youtube.com/watch?v=x5fWSWdM4F8&t=861s). Videon avulla lopulta hahmotin selkeästi, mitä conf-tiedostot tekivät ja miksi sivut välillä ohjautuivat var-kansiossa olevaan tiedostoon.

Videolla kerrottiin, että kun Apacheen otetaan yhteyttä, etsitään conf-tiedostoista yhteensopivaa ServerName:ia. Jos tätä ei löydy, valitaan järjestyksessä ensimmäinen conf-tiedosto joka on 000.default ja koska tämä tiedosto ohjaa var-kansion tiedostoon, päädytään tänne. Jos taas yhteensopivuus löytyy, ohjataan käyttäjä kyseisessä tiedostossa määriteltyyn tiedostosijaintiin. Jälkimmäisessä testissä tiedostosijainnissa ei ollut oikeasti mitään kansiota eli virheilmoitus johtuu tästä.

Oppimani perusteella sain matka-sivun onnistuneesti osoittamaan sivulle tutkimusmatka.jennimuhonen.com.

Ensiksi muokkasin CNAME recordin kuntoon:

![image](https://github.com/user-attachments/assets/c7c2f626-4618-4f0d-938c-2e16e4a6cc2c)

Tämän jälkeen muokkasin tutkimusmatka.jennimuhonen.com.conf-tiedostoa siten, että tästä tiedostosta löytyi haluttu vastaavuus syötetyn osoitteen kanssa. Apachen ohjeesta (https://httpd.apache.org/docs/2.4/vhosts/name-based.html) tarkistin, kuinka useampi alias merkitään tiedostoon.

![image](https://github.com/user-attachments/assets/b8c1275b-025f-4303-bac6-8e8cd7353fdb)

Tämän jälkeen homma alkoi toimia:

![image](https://github.com/user-attachments/assets/553d54e2-106b-4861-a9eb-8c10f40a9eef)

## c) Pubkey

*Tehtävä: Automatisoi kirjautuminen julkisella SSH-avaimella.*

*21.9.2024 n. 15.30*

Jos haluat lukea kamppailuistani SSH-avaimien kanssa, voit kurkistaa edellisen viikon raporttini: https://github.com/jennimuhonen/linux-kurssi/blob/main/h4_maailma_kuulee.md. UpCloudilla avaimia oli pakko käyttää ja tämän takia päädyin asian opettelemaan.

Tämän viikon tehtävässä noudatin edellisellä viikolla oppimaani kaavaa ja otin mallia edellisestä raportistani.

Koska varsinaisella käyttäjälläni on jo ssh-avaimet käytössä, tein uuden käyttäjän:

![image](https://github.com/user-attachments/assets/227a3776-ccf8-4534-acc6-abeee0b42796)

Kopioin julkisen avaimen käyttäjältä jemjem:

![image](https://github.com/user-attachments/assets/1360389d-b3b3-43bc-a0cd-9001b795ad4b)

Vaihdoin käyttäjään varjo palvelimen sisällä, koska edellisellä viikolla totesin, että vaikka salasanakirjautuminen palvelimelle oli alkuun sallittuna, tämä ei jostain syystä toiminut:

![image](https://github.com/user-attachments/assets/918e3014-68d3-412c-af67-12826b805caf)

![image](https://github.com/user-attachments/assets/f5be3dc1-581d-4699-85ff-bd9e1f1d5b5e)

Tein varjolla kansion samanlaiseen sijaintiin kuin jemjem:llä on ja määritin kansion oikeudet ja tein tiedoston julkisille avaimille ja liitin kopioimani tiedon sinne:

![image](https://github.com/user-attachments/assets/6d9ea59d-227d-4bad-9c56-d9954fc90244)

Ja pääsin sisälle ilman salasanaa:

![image](https://github.com/user-attachments/assets/61d8eab2-7121-4cde-a0e0-b56ae121e015)


## d) Tutki jonkin nimen DNS-tietoja 'host' ja 'dig' -komennoilla.

*Tehtävä: Käytä kumpaakin komentoa kaikkiin nimiin ja vertaa tuloksia. Katso man-sivulta, miten komennot toimivat - esimerkiksi miten 'dig' näyttää kaikki kentät. Analysoi tulokset. Etsi tarvittaessa uusia lähteitä haastaviin kohtiin. Sähköpostin todentamiseen liittyvät SPF ja DMARC -tietojen yksityiskohdat on jätetty vapaaehtoiseksi lisätehtäväksi. Tutkittavat nimet:*

 - *Oma domain-nimesi. Vertaa tuloksia nimen vuokraajan (namecheap.com, name.com...) weppiliittymässä näkyviin asetuksiin.*
- *Jonkin pikkuyrityksen, kerhon tai yksittäisen henkilön weppisivut. (Ei kuitenkaan kurssikaverin tällä viikolla vuokrattua nimeä).*
- *Jonkin suuren ja kaikkien tunteman palvelun tiedot.*

Voidakseni käyttää dig-komentoa minun piti asentaa dnsutils. Olin törmännyt dig-komentoon jo aiemmin Github-sivujen ohjeissa ja asentanut sen silloin virtuaalipalvelimen puolelle, nyt asensin sen myös VirtualBoxilla olevalle Debianille. Oikean asennuspaketin löysin GeeksforGeeks-sivujen ohjeista (https://www.geeksforgeeks.org/dig-command-in-linux-with-examples/).

![image](https://github.com/user-attachments/assets/143a412a-77c9-4afd-b6fa-869426b7364f)

man host -sivun mukaan host-komentoa käytetään normaalisti muuntamaan domain nimiä ip-osoitteiksi ja päinvastoin. Kun kirjoittaa pelkästään host, saa listan käytettävissä olevista komennoista. Pelkän man sivun perusteella en osannut sanoa, mitä lisäkomentoja kannattaisi käyttää mielenkiintoisia tuloksia saadakseni.

man dig -sivun mukaan dig-komento on monipuolinen työkalu, jonka avulla voi tutkia DNS nimiservereitä. Komennon avulla voi selvittää DNS:ään liittyviä ongelmia. dig -h listaa lyhyen tiivistelmän erilaisista komennoista ja vaihtoehdoista.

Man sivun mukaan, yksinkertainen tapa käyttää komentoa on: dig @server name type, jossa serveri: DNS serveri, josta tietoa haetaan ja jos ei ole määritelty, defaulttina ovat serverit, jotka on määritelty tiedostossa /etc/resolv/conf , nimi: sivu josta halutaan tietoa, tyyppi (ANY, A (eli A Recordiin) MC (liittyy sähköpostiin) SIG tms ja jos tyyppiä ei ole määritetty, etsitään A recordia). (Lisätietoa aiheeseen löydetty man dig:n täydennykseksi Tony Teaches Techin videolta (https://www.youtube.com/watch?v=iESSCDnC74k)).

Edelliseen hakuun kuuluu ilmeisesti nimen kohdalle laittaa domainnimi, sillä Tony Teaches Tech näyttää erikseen reverse DNS-haun: `dig -x ip-osoite`.

Man-sivujen perusteella saattoi huomata, että dig-komennossa on huomattavasti enemmän erilaisia lisäkomentoja verrattuna hostiin.

host jennimuhonen.com:

![image](https://github.com/user-attachments/assets/e724f4d4-9b56-4d3e-aca0-e6c9225e950f)

Ylläoleva näyttää selkeältä. Host listaa ip-osoitteen ja lisäksi löytää tietoa sähköpostiin liittyen. Namecheapin sivuilla on TXT record, jossa mainitaan efwd.registrar-servers.com.

dig jennimuhonen.com:

![image](https://github.com/user-attachments/assets/2208ec68-126e-49af-810c-18198f563c4d)

*23.9.2024 n. klo 23*

Dig-komennon tulkitsemiseksi etsin lisätietoa. JSDeliverin artikkelissa (https://www.jsdelivr.com/blog/how-to-read-a-dig-result-a-guide-for-network-novices/) käydään läpi komennolla saatua sisältöä.

- Header: kertoo tehdystä dig-kyselystä, kuten kyselyaika, käytetty serveri ja flags (?)
- Question section: kertoo domainin ja kysellyn recordin tyypin
- Answer section: DNS serveriltä saatu tieto, kuten ip-osoite ja tai muut DNS recordit
- Authority section: listaa authoritatiiviset DNS-palvelimet, jotka liittyvät domainiin, josta kysely tehtiin
- Additional: sisältää muun tiedon, joka DNS-palvelimelta saatiin, esim. authoritatiivisten palvelinten IP-osoitteet

Yllä olevan kyselyn tulkinnassa on käytetty JSDeliverin artikkelin lisäksi Phoenixnapin artikkelia (https://phoenixnap.com/kb/linux-dig-command-examples).

Ensimmäinen rivi kertoo dig-komennon version. Header-osiossa NOERROR-status kertoo, että vastaus saatiin onnistuneesti. OPT Pseudosectionista näkisi jos flageja olisi määritelty. Udp tarkoittaa udp-paketin kokoa.

Question osiosta nähdään, että kysely tehtiin jennimuhonen.com:sta ja että kyseessä oli kysely A recordeista (default-valinta). IN tarkoittaa internettiä . Answer-osiossa nähdään kysytyn sivun ip-osoite. Vastauksen alla Query time kertoo miten pitkään vastauksen saamiseen meni, palvelin josta vastaus saatiin, aika jolloin kysely tehtiin ja DNS-palmelimelta saadun vastauksen koko.

Vertailukohtana tein haun sivu-sivusta, joka linkittyy Github-sivuuni.

![image](https://github.com/user-attachments/assets/5a3f3209-3f9e-4bcc-a2a8-082a1a2ed358)

Vaikka A-record on defaul-vastaus, niin näyttää silti siltä, että haku sisällyttää myös CNAME:n vastaukseen. Vastauksessa listataan myös githubin ip-osoitteet, joihin tämä sivu osoittaa. Sen sijaan kuten näkyy, tämä sivu ei osoita minun virtuaalipalvelimelleni lainkaan.

Seuraavaksi kokeilin hakea Espoon scifiseuran tietoja:

![image](https://github.com/user-attachments/assets/d88a02a6-0970-41d6-abb4-275d35b478c4)

Molemmista vastauksista nähdään, että sivu sijaitsee ip-osoitteessa 5.44.245.27.

Viimeiseksi tutkin Amazonin tietoja:

![image](https://github.com/user-attachments/assets/9272965b-a0c6-4836-85d0-a43ebd0ddd74)

Amazon.com:n sivuun on linkitetty yhden sijaan kolme ip-osoitetta.

Selvitin vielä lisää, mitä Authority sectionilla tarkoitetaan. Uptimian artikkelin (https://www.uptimia.com/questions/what-does-the-authority-section-in-dig-results-mean) mukaan kyseinen osio on olennainen osa vastausta ja kertoo virallisen (authoritative) name serverin, joka liittyy domainiin, josta kysely tehtiin. Eli mitkä DNS serverit ovat vastuussa vastaamaan kyselyihin, jotka liittyvät kyseiseen domainiin. "DNS resolution":ssa tämä osio on keskeinen, sillä tämä ohjaa DNS resolverit oikean nimipalvelimen luokse, kun ne hakevat tietoa domainista. Tämä osio on hyödyllinen esimerkiksi silloin, kun tehdään muutoksia DNS-asetuksiin tai selvitellään siihen liittyviä ongelmia. (Minulla on tällä hetkellä Tietoverkkojen perusteet -kurssi kesken. Uskon, että hahmotan edellä kirjoittamani paremmin, kun olen käynyt kurssin. Tällä hetkellä kurssilla ei olla vielä päästy ylempien OSI-kerrosten tarkempaan tarkasteluun.)

---

**ToDo-lista**

- Opettele siirtämään sivun sisältö omalle palvelimelle sen sijaan, että ohjaan sivun githubiin

**Selvittämättömät ongelmat**

- Miksi en pääse palvelimelle ilman julkista SSH-avainta, vaikka salasanakirjautuminen olisi sallittuna?

---

**Lähteet**

- Alex Coventry 6.12.2021 & Archathean_Official 10.11.2022. Reddit-kommentit. https://www.reddit.com/r/virtualbox/comments/ra8cvc/is_there_a_way_to_set_guest_resolution_to/?rdt=44017
- Apache. Apache Core Features. https://httpd.apache.org/docs/current/mod/core.html#serveralias
- Apache. Name-based Virtual Host Support. https://httpd.apache.org/docs/2.4/vhosts/name-based.html
- Ask Ubuntu: Apache2 Permission denied - access to / denied because search permissions are missing on a component of the path. https://askubuntu.com/questions/1353377/apache2-permission-denied-access-to-denied-because-search-permissions-are-mi
- Ask Ubuntu: What does "chmod +x <filename>" do and how do I use it? https://askubuntu.com/questions/443789/what-does-chmod-x-filename-do-and-how-do-i-use-it
- CloudFlare: What is a DNS TXT record? https://www.cloudflare.com/learning/dns/dns-records/dns-txt-record/
- Debian Wiki: Permissions. https://wiki.debian.org/Permissions
- DNSimple Support: Differences Between A and CNAME Records. https://support.dnsimple.com/articles/differences-a-cname-records/
- DNSimple Support: Differences Among A, CNAME, ALIAS, and URL records. https://support.dnsimple.com/articles/differences-between-a-cname-alias-url/
- Geeksforgeeks 22.6.2024: dig Command in Linux with Examples. https://www.geeksforgeeks.org/dig-command-in-linux-with-examples/
- Github Docs: Managing a custom domain for your GitHub Pages site. https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/managing-a-custom-domain-for-your-github-pages-site
- Github Docs: Verifying your custom domain for GitHub Pages. https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/verifying-your-custom-domain-for-github-pages
- JSDelivr: How to Read a Dig Result: A Guide for Network Novices. https://www.jsdelivr.com/blog/how-to-read-a-dig-result-a-guide-for-network-novices/
- Karvinen, Tero 2018: Name Based Virtual Hosts on Apache – Multiple Websites to Single IP Address. https://terokarvinen.com/2018/04/10/name-based-virtual-hosts-on-apache-multiple-websites-to-single-ip-address/
- Karvinen, Tero: Oppitunti 18.9.2024. Linux-palvelimet. https://terokarvinen.com/linux-palvelimet/
- Linux Mint Forums: [SOLVED][Apache2] AH00035: access to / denied. https://forums.linuxmint.com/viewtopic.php?t=176598
- man dig
- man host
- Muhonen, Jenni 2024: h3 Hello Web Server. https://github.com/jennimuhonen/linux-kurssi/blob/main/h3-hello-web-server.md
- Muhonen, Jenni 2024: h4 Maailma kuulee. https://github.com/jennimuhonen/linux-kurssi/blob/main/h4_maailma_kuulee.md
- Nerd on the Street 17.5.2020: Apache Virtual Hosts. https://www.youtube.com/watch?v=x5fWSWdM4F8&t=861s
- PhoenicNAP 23.5.2024: dig Command in Linux with Examples. https://phoenixnap.com/kb/linux-dig-command-examples
- StackOverflow: Apache giving 403 forbidden error. https://stackoverflow.com/questions/18447454/apache-giving-403-forbidden-errors
- Tony Teaches Tech 27.4.2021: How to Use a Custom Domain with GitHub Pages. https://www.youtube.com/watch?v=EX4w9hsduNA
- Tony Teaches Tech 19.8.2021: What are CNAME records? (and how they compare to DNS A records). https://www.youtube.com/watch?v=ZXCQwdVgDno
- Tony Teaches Tech 7.5.2021. How To Lookup DNS Records With The dig Command https://www.youtube.com/watch?v=iESSCDnC74k
- Uptimia 16.4.2024. What Does The Authority Section In Dig Results Mean? https://www.uptimia.com/questions/what-does-the-authority-section-in-dig-results-mean
- Webmasters: Why does typing in my site's IP address bring up a different site? https://webmasters.stackexchange.com/questions/113237/why-does-typing-in-my-sites-ip-address-bring-up-a-different-site


---
  
*Tätä dokumenttia saa kopioida ja muokata GNU General Public License (versio 2 tai uudempi) mukaisesti. http://www.gnu.org/licenses/gpl.html*

*Pohjana Tero Karvinen 2012: Linux kurssi, http://terokarvinen.com*

*Raportin tekijä: Jenni Muhonen*
