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

Tässä kohtaa aloin muistelemaan, kuuluuko minun tehdä samanlainen tiedosto myös pääsivustani jennimuhonen.com. Tutkin mitä tein kahdessa edellisessä raportissani






---

**Lähteet**

- Alex Coventry 6.12.2021 & Archathean_Official 10.11.2022. Reddit-kommentit. https://www.reddit.com/r/virtualbox/comments/ra8cvc/is_there_a_way_to_set_guest_resolution_to/?rdt=44017
- Muhonen, Jenni 2024: h3 Hello Web Server. https://github.com/jennimuhonen/linux-kurssi/blob/main/h3-hello-web-server.md
- Muhonen, Jenni 2024: h4 Maailma kuulee. https://github.com/jennimuhonen/linux-kurssi/blob/main/h4_maailma_kuulee.md
- Karvinen, Tero, 2018: Name Based Virtual Hosts on Apache – Multiple Websites to Single IP Address. https://terokarvinen.com/2018/04/10/name-based-virtual-hosts-on-apache-multiple-websites-to-single-ip-address/


---
  
*Tätä dokumenttia saa kopioida ja muokata GNU General Public License (versio 2 tai uudempi) mukaisesti. http://www.gnu.org/licenses/gpl.html*

*Pohjana Tero Karvinen 2012: Linux kurssi, http://terokarvinen.com*

*Raportin tekijä: Jenni Muhonen*
