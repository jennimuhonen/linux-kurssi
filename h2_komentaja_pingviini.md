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

Ei siis sittenkään niin helppoa. Aina saa toivoa. Arvasin, että näin tapahtuu, koska hain yhtä ohjelmista komennolla apt-cache search ja kyseinen ohjelma ei osunut silmiini. Siksi myös varakta googletin useamman ohjelman asentamisen.

Googleria ei ole mainittu epäonnistuneiden listalla, mutta mitään asennustekstiäkään ei näytöllä näkynyt. Kokeilin pelkän googlerin asentamista: 

![image](https://github.com/user-attachments/assets/557979e8-6435-463a-9583-e01c59bbc272)

Tämä näyttäisi onnistuvan. Siispä kokeilin avata ohjelman:

![image](https://github.com/user-attachments/assets/bc71a621-50b5-424f-8bb6-4bdb1cc8b578)

Vertailuna kävin katsomassa selainversiota Googlesta ja haku debian antaa tulokseksi samat linkit. Toimii siis!

Kokeilin asentaa Wikitin ja Browshin yksitellen, mutta lopputulos oli sama. Tulkitsen niin, että näitä ei enää löydy paketinhallinnan kautta.

Siirryin siis kokeilemaan muita listalla suositeltuja ohjelmia.

![image](https://github.com/user-attachments/assets/5a5941e5-19bc-4c84-817a-fdfaf4082705)

Asennus näyttäisi onnistuneen, joten testasin ohjelmia.

![image](https://github.com/user-attachments/assets/3f18b8c9-1180-4dce-9516-95315914d9e6)

Google antoi vastauksen kuvassa näkyvään ongelmaan, vastaus on Ctrl+D. Vastauksen taustalla on sivu https://phoenixnap.com/kb/linux-cat-command.

Lolcatin idean ymmärtäminen vaati lisäohjeita, joten päädyin Youtubeen katsomaan Hex DSL:n videon aiheesta, https://www.youtube.com/watch?v=Ivggw8qBbHM. Opin, että Lolcatin avulla voin saada väriä elämään, jälkimmäinen komento hidastettu ja dramaattismepi vaihtoehto:

![image](https://github.com/user-attachments/assets/db992105-6727-4f88-8856-61935f74a2dc)

Testataan vielä viimeinen ohjelma:

![image](https://github.com/user-attachments/assets/c7a80e4d-93f5-4a91-96a4-555c6f768fee)

![image](https://github.com/user-attachments/assets/c8d55d63-3ec6-4b4d-bf46-fd4c52ade081)

Tästä oli vähemmän iloa kuin Lolcatista.

**Lähteet**

- Ask Ubuntu 2012: https://askubuntu.com/questions/160897/how-do-i-search-for-available-packages-from-the-command-line
- Ask Ubuntu 2017: https://askubuntu.com/questions/874611/installing-multiple-packages-at-the-same-time
- Hex DSL 2016: The BEST Linux Application. - lolcat. https://www.youtube.com/watch?v=Ivggw8qBbHM
- Kili, Aaron 2023: 10 Best Linux Command-Line Tools. https://www.tecmint.com/command-line-tools/
- PhoenixNap 2024: Linux cat Command (With Examples). https://phoenixnap.com/kb/linux-cat-command
- ThioJoe 2024: 11 Cool Command Line Programs You Need to See. https://www.youtube.com/watch?v=K0v9hnn24y8


## FHS

Tehtävä: Esittele tärkeitä kansioita ja näytä kuvaava esimerkki kustakin.

/ on juurikansio, joka on Linuxissa ylin kansio. Juureen pääsin seuraavasti ja tarkastin sen sisällön:

![image](https://github.com/user-attachments/assets/19d34a87-8e77-4ea3-a481-532c51582b5c)

Juurikansion alta löytyy home, jonka alka löytyy käyttäjien kansiot. Näin pääsin juuresta home-kansioon ja totesin, että käyttäjäkansioni löytyy sen alta:

![image](https://github.com/user-attachments/assets/fa7fe3d9-5dba-4c90-b876-7c12148ce169)

Home-kansion olla on käyttäjäprofiilini kansio jenni. Sinne pääsin home-kansiosta vastaavaan tapaan kuin edelläkin. Kyseisen kansion alta löytyi esimerkiksi aiemmin tekemäni testitiedosto eli testi.md, jonka olisi ehkä voinut ennemmin tallentaa vaikkapa Documents-kansioon.

![image](https://github.com/user-attachments/assets/514d4d4d-5c8e-4487-a695-f0d65c74fad6)

testi.md-tiedoston avasin Microlla seuraavalla komennolla:

![image](https://github.com/user-attachments/assets/c571a502-f28e-4e5f-b09c-a15cc21be73a)

![image](https://github.com/user-attachments/assets/5abeeb70-80a0-42a2-ac5f-1bc1a5386c56)

Etc-kansio on juuressa. Sinne pääsin seuraavasti ja tarkastelin sen sisältöä:

![image](https://github.com/user-attachments/assets/c75c326d-898b-433c-9a62-db737304a4e0)

Anne Surendran mukaan tämä kansio sisältää kaikki järjestelmän asetuksiin liittyvät tiedostot ja kurssisivun mukaan tiedostot ovat tekstimuodossa eli voinemme käydä kurkistamassa jotain tiedostoa.

![image](https://github.com/user-attachments/assets/2b5c73dc-70ae-4cc2-a976-590d0e35cedc)

Tai ilmeisesti ainakaan kaikkea ei voi avata. Kokeilin sen sijaan avata jotain kansiota.

![image](https://github.com/user-attachments/assets/6d81e8c6-6105-4809-82df-276c7aec8e8f)

Pääsin gimp-kansioon ja löysin sen alikansiosta tiedoston toolrc, joka avautui Microon.

![image](https://github.com/user-attachments/assets/6beaa8cd-44d0-478f-a0d3-0fdd64a1404e)

Seuraavaksi listalla on media-kansio, jonka avulla kurssisivuston mukaan pääsee käsiksi usb-tikkuihin ja cd-asemaan. Tutkin asiaa:

![image](https://github.com/user-attachments/assets/62269511-f8d7-4d2b-9dc5-f1517cfde227)

Ray Fernandezin mukaan USB täytyy erikseen sallia virtuaalikoneella. Koska minulla ei ole tarvetta saada USB:tä toimimaan, en perehtynyt aiheeseen tarkemmin. Nyt löysin media-kansion alta vain käyttäjäprofiilini kansion, jonka alta ei löytynyt mitään.

Viimeisenä tutustuttavana on var/log. Palasin jälleen juureen, sillä olin nähnyt var-kansion siellä.

![image](https://github.com/user-attachments/assets/93e7c1b3-939e-498c-8248-9ef66e88cdb7)

Kurssisivuston mukaan kyseessä kansio sisältää koko systeemin laajuisia logeja. Kokeilin kurkata lastlog-tiedostoon Microlla, mutta se avasi vain tyhjän tiedoston. Netsurion-sivustolta (https://www.netsurion.com/articles/top-5-linux-log-file-groups-in-var-log) löysin neuvon avata tiedosto suoraan ilman Microa ja näin se aukesikin:

![image](https://github.com/user-attachments/assets/52a79ab6-fbc2-4eb4-a79d-f179fcf32383)

Netsurionin mukaan kyseisestä tiedostosta löytyy viimeaikainen kirjautumistieto kaikista käyttäjistä. 


**Lähteet**

- Fernandez, Ray: How to Enable USB in VirtualBox. https://www.techrepublic.com/article/how-to-enable-usb-in-virtualbox/
- Karvinen, Tero 2020: Command line basics revisited. https://terokarvinen.com/2020/command-line-basics-revisited/?fromSearch=command%20line%20basics%20revisited
- Netsurion: Top 5 Linux log file groups in/var/log. https://www.netsurion.com/articles/top-5-linux-log-file-groups-in-var-log
-  Surendra, Anne: Linux directory structure explained:/etc folder . https://www.linux.com/training-tutorials/linux-directory-structure-explainedetc-folder/


## d) The Friendly M

Tehtävä: 2-3 esimerkkiä grep-komennosta
*29.8.2024 15.48 (Ajan kirjaaminen on päässyt hieman unohtumaan.)

Katsoin Learn Linux TV:n videota grep-komennosta (https://www.youtube.com/watch?v=Tc_jntovCM0) hahmottaakseni mistä on kyse. Kyseessä on komento, jonka avulla voidaan hakea halutun sanan avulla tietty rivi pitkästä tiedostosta. Samalla opin, että cat-komennolla saan tekstitiedoston näkyviin suoraan komentorivillä avaamatta erikseen tekstinkäsittelyä.

Testasin molempia komentoja aiemmin tekemääni testitiedostoon. Vertailuna kokeilin myös, mitä tapahtuu ilman cat-komentoa. Lisäksi totesin, että hymiön hakemin ei toiminut. Jälkimmäisenä toinen tapa kirjoittaa sama komento.

![image](https://github.com/user-attachments/assets/4fd753e7-c037-458e-a880-edc454a96095)

![image](https://github.com/user-attachments/assets/c704fd72-e8c5-44e9-8ce1-daf973a48978)


Grep toimi myös tiedostoa etsiessä eli jos ls tuottaisi tiedostotulvan, grepin avulla voi tsekata, onko tietty tiedosto kansiossa:

![image](https://github.com/user-attachments/assets/f49c7ded-84c0-44dd-8984-0fa157d9b4f1)

Jatkoin Learn Linux TV:n videon parissa ja opin, että lisäämällä komentoon -v, voin hakea kaiken muun paitsi mainitun termin.

![image](https://github.com/user-attachments/assets/94b4c6ca-01ba-4747-afa7-3f3cbb092332)


Vaikuttaa kätevältä työkalulta!

**Lähteet**

- Learn Linux TV 2022: Linux Crash Course - The grep Command. https://www.youtube.com/watch?v=Tc_jntovCM0

---
  
*Tätä dokumenttia saa kopioida ja muokata GNU General Public License (versio 2 tai uudempi) mukaisesti. http://www.gnu.org/licenses/gpl.html*

*Pohjana Tero Karvinen 2012: Linux kurssi, http://terokarvinen.com*

*Raportin tekijä: Jenni Muhonen*
