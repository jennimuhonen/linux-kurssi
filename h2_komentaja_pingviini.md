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

Näyttäisi siltä, että Micro on asennettavissa paketinhallinnan kautta. Seuraavaksi ohjesivusto ohjeistaa asentamaan ohjelmon seuraavalla komennolla:

![image](https://github.com/user-attachments/assets/e95d4dac-2a42-4366-ad44-6af0ffb6da69)

Oletin asennuksen onnistuneen ja testasin asiaa tekemällä uuden tiedoston microlla.

![image](https://github.com/user-attachments/assets/e7510446-3598-4a8c-a6e3-23a9d4c2b057)

Hyvältä näytti:

![image](https://github.com/user-attachments/assets/a1810cf3-5f27-4244-9e21-bbc80e58618e)

Suurin haaste tuli lopuksi, kun ohjelma piti sulkea. Pikainen googlaus ohjasi sivulle https://crazcalm.github.io/blog/post/learning_micro/, josta löytyi vastaus. Ohjelma suljetaan komennolla Ctrl+q. Tämän olisi varmasti voinut arvata, jos ei olisi näin aloittelija Linuxin kanssa. Sama vastaus olisi löytynyt, jos olisi avannut ohjelman alalaidassa mainitun helpin.


**Lähteet**

- Crazcalm. https://crazcalm.github.io/blog/post/learning_micro/
- Karvinen, Tero 2020: Command line basics revisited. https://terokarvinen.com/2020/command-line-basics-revisited/?fromSearch=command%20line%20basics%20revisited


## Apt

Tehtävä: asenna kolme itsellesi uutta komentoriviohjelmaa ja kokeile niitä.

Kaikki komentoriviohjelmat ovat minulle uusia eli ensimmäiseksi minun pitää selvittää, mitä voisin edes haluta asentaa, kun en tiedä aiheesta mitään. Google ohjasi minut Youtubeen katsomaan ThioJoe:n videota aiheesta https://www.youtube.com/watch?v=K0v9hnn24y8. Hetken videota katsottuani tarkistin, löytyykö ensimmäistä suositeltua ohjelmaa paketinhallinnan kautta. Ei löytynyt. Kokeilin aiemmin asentaa Steamiä Debianiini ja sain huomata, ettei se olekaan niin yksinkertaista. Nyt en siis lähtenyt repimään hiuksiani satunnaisten ohjelmien takia vaan päätin etsiä vinkkini muualta.

Miten löydän ohjelmia paketinhallinnasta ilman että tiedän, mitä etsin? Ask Ubuntu -sivustolla joku oli miettinyt samaa ja hänelle annettiin vinkkinä "apt-cache searc keyword". Kokeilin ensin avainsanaa game, mutta mistä tiedän mikä on komentoriviohjelma? Seuraavaksi kokeilin avainsanaa commandline ja edessäni oli pitkä lista ohjelmia, joiden käyttötarkoitus näytti varsin mystiseltä.

Palasin googlen ääreen etsimään parempia vinkkejä ja päädyin lukemaan Aaron Kilin listausta kymmenestä parhaasta Linuxin komentorivityökalusta https://www.tecmint.com/command-line-tools/. Kilin mukaan kaikki hänen listaamansa ohjelmat löytyvät paketinhallinnan kautta. Hänen vinkeillään siis mentiin.

Tehtävässä oli ekstrana asentaa kaikki ohjelmat kerralla yhdellä komennolla. Minulla oli veikkaus asiaan, mutta kokeilemisen sijaan tarkistin vastauksen Ask Ubuntu sivustolta ja kuten epäilin, riittää kun listaan haluamani paketit komentoon peräkkäin.

![image](https://github.com/user-attachments/assets/ef0862b5-eb42-413e-8f49-58ceb6a395b9)

Ei siis sittenkään niin helppoa. Aina saa toivoa. Arvasin, että näin tapahtuu ja siksi googletin useamman ohjelman asentamisen. Kokeillaanpa seuraavaksi yksitellen.


**Lähteet**

- Ask Ubuntu 2012: https://askubuntu.com/questions/160897/how-do-i-search-for-available-packages-from-the-command-line
- Ask Ubuntu 2017: https://askubuntu.com/questions/874611/installing-multiple-packages-at-the-same-time
- Kili, Aaron 2023: 10 Best Linux Command-Line Tools. https://www.tecmint.com/command-line-tools/
- ThioJoe 2024: 11 Cool Command Line Programs You Need to See. https://www.youtube.com/watch?v=K0v9hnn24y8

---
  
*Tätä dokumenttia saa kopioida ja muokata GNU General Public License (versio 2 tai uudempi) mukaisesti. http://www.gnu.org/licenses/gpl.html*

*Pohjana Tero Karvinen 2012: Linux kurssi, http://terokarvinen.com*

*Raportin tekijä: Jenni Muhonen*
