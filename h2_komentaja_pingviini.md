# h2 Komentaja Pingviini

Tehtäviä Tero Karvisen kurssille Linux Palvelimet 2024. https://terokarvinen.com/linux-palvelimet/

---

## x) Lue ja tiivistä

- Komentoja hakemistossa liikkumisen avuksi: esim. pwd, ls, cd kansio_xyz/, cd ..
- Komentoja tiedostojen manipuloimiseen esim. nano testi.md (luo tiedoston, jos sitä ei vielä ole olemassa), mkdir uusikansio, rmdir uusikansio
- Helppoja tekstieditoreja pico ja nano
- SSH Remote Control -komentoja: esim. ssh testi@testi.com, exit
- Erilaisia help-komentoja: esim. man ls, ls --help
- Tabin painaminen kahteen kertaan näyttää, mitä voi kirjoittaa seuraavaksi, kertaalleen täydentää komentoa (Mahtavaa!)
- Historiaa voi kaivella: ctrl+R (eli ^R)
- Käyttäjäkansioni yllä on home/ ja sen yllä /, joka on juurikansio eli ylin kansio
- Toimintoja, joihin tarvitaan enemmän oikeuksia, käytetään komennolla sudo (kuten ohjelmien asentaminen ja poistaminen, käyttäjien luominen, oikeuksien hallinnointi) 


**Kommentit**
- Eri komentoja hahmottaakseni, kokeilin luoda tekstitiedoston, nimetä sen uudestaan ja poistaa sen. Hämmentävää oli täysi palautteen puuttuminen, jos jokin onnistui. Joka välissä oli pakko kirjoittaa ls, jotta sai olla varma, että asia todella onnistui.
  
  
**Lähteet**

- Karvinen, Tero 2020: Command line basics revisited. https://terokarvinen.com/2020/command-line-basics-revisited/?fromSearch=command%20line%20basics%20revisited


## Rauta ja OS

**Virtualisoidun Linuxin tiedot**

- Käyttöjärjestelmä: Debian 12.6.0 AMD64
- Virtualisointi: VirtualBox 7.0.20
- Muisti: 4096 MB
- Prosessorit: 4 CPU
- Virtuaalilevyn maksimikoko: 60 GB, josta käytetty 13,37 GB

**Taustajärjestelmän tiedot**

- Pöytäkone
- Käyttöjärjestelmä: Windows 11 Education, 64 bittinen käyttöjärjestelmä, x64-suoritin
- CPU: AMD Ryzen 5 7600 3.8 GHz 6-Core Processor
- Emolevy: MSI PRO B650-P WIFI
- Muisti: 32 GB DDR5-6000 CL30
- SSD: 2 TB, jossa vapaata tilaa 976 Gt
- Näytönohjain: AMD RX 6800 XT 16 GB

## a) Micro

Tehtävä: Asenna Micro
*29.8.2024 n. 12.00*

Suuntasin opettajan komentokehotteet listaavalle sivulle (https://terokarvinen.com/2020/command-line-basics-revisited/?fromSearch=command%20line%20basics%20revisited) ja etsin asennukseen liittyvät komennot. Ensiksi kehotetaan päivittämään tarjolla olevat paketit. Eli näin tein seuraavalla komennolla:

*(Kaikki käyttämäni kuvat ovat ruutukaappauksia siitä, mitä olen tekemässä.)*

![image](https://github.com/user-attachments/assets/522d7df7-ec76-4ba9-8332-7a5203016402)

Jatkoin ohjeiden seuraamista ja tarkistin, löytyykö Micro listalta seuraavalla komennolla:

![image](https://github.com/user-attachments/assets/f6958a0d-39fa-40d6-bece-7f49881f65f5)

(Luonnollisesti ennätin painaa enter ennen kuin otin kuvakaappauksen, mutta nuolinäppäin ylöspäin toi komennon uudelleen käytettäväksi ja näin saatoin lavastaa kuvakaappauksen.)

Selasin listaa etsiäkseni Micron. Tähän varmaan oli parempiakin keinoja kuin vain scrollata ylöspäin, kunnes oikea kohta tulee vastaan, mutta en lähtenyt tässä kohtaa etsimään vinkkejä selailuun:

![image](https://github.com/user-attachments/assets/cf1b18bc-8d04-406b-987e-2a42b4c1ea2e)

Näyttäisi siis siltä, että Micro on asennettavissa paketinhallinnan kautta. Seuraavaksi ohjesivusto ohjeistaa asentamaan ohjelmon seuraavalla komennolla:



**Lähteet**

- Karvinen, Tero 2020: Command line basics revisited. https://terokarvinen.com/2020/command-line-basics-revisited/?fromSearch=command%20line%20basics%20revisited

---
  
*Tätä dokumenttia saa kopioida ja muokata GNU General Public License (versio 2 tai uudempi) mukaisesti. http://www.gnu.org/licenses/gpl.html*

*Pohjana Tero Karvinen 2012: Linux kurssi, http://terokarvinen.com*

*Raportin tekijä: Jenni Muhonen*
