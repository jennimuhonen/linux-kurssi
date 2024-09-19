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


---

**Lähteet**

- Alex Coventry 6.12.2021 & Archathean_Official 10.11.2022. Reddit-kommentit. https://www.reddit.com/r/virtualbox/comments/ra8cvc/is_there_a_way_to_set_guest_resolution_to/?rdt=44017
- Muhonen, Jenni 2024: h3 Hello Web Server. https://github.com/jennimuhonen/linux-kurssi/blob/main/h3-hello-web-server.md
- Muhonen, Jenni 2024: h4 Maailma kuulee. https://github.com/jennimuhonen/linux-kurssi/blob/main/h4_maailma_kuulee.md
- Karvinen, Tero, 2018: Name Based Virtual Hosts on Apache – Multiple Websites to Single IP Address. https://terokarvinen.com/2018/04/10/name-based-virtual-hosts-on-apache-multiple-websites-to-single-ip-address/
- Webmasters: Why does typing in my site's IP address bring up a different site? https://webmasters.stackexchange.com/questions/113237/why-does-typing-in-my-sites-ip-address-bring-up-a-different-site


---
  
*Tätä dokumenttia saa kopioida ja muokata GNU General Public License (versio 2 tai uudempi) mukaisesti. http://www.gnu.org/licenses/gpl.html*

*Pohjana Tero Karvinen 2012: Linux kurssi, http://terokarvinen.com*

*Raportin tekijä: Jenni Muhonen*
