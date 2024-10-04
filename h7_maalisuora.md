# h7 Maalisuora

Tehtäviä Tero Karvisen kurssille Linux Palvelimet 2024. https://terokarvinen.com/linux-palvelimet/

---

## Rauta ja OS

**Virtuaalikoneella pyörivän Linuxin tiedot**

- Käyttöjärjestelmä: Debian 12.6.0 AMD64
- Virtualisointi: VirtualBox 7.0.20
- Muisti: 4096 MB
- Prosessorit: 4 CPU
- Virtuaalilevyn maksimikoko: 60 GB, josta käytetty 15,29 GB

**Taustajärjestelmän tiedot**

- Pöytäkone
- Käyttöjärjestelmä: Windows 11 Education, 64 bittinen käyttöjärjestelmä, x64-suoritin
- CPU: AMD Ryzen 5 7600 3.8 GHz 6-Core Processor
- Emolevy: MSI PRO B650-P WIFI
- Muisti: 32 GB DDR5-6000 CL30
- SSD: 2 TB, jossa vapaata tilaa 959 GB
- Näytönohjain: AMD RX 6800 XT 16 GB

---

## a) "Hei maailma" kolmella kielellä

Tunnilla kokeiltiin Pythonia, joten kokeilin nyt jotain muuta.

**Java**

Opettajan ohjeissa ei ollut mainintaa, millä nimellä java-paketti löytyy apt-getistä, joten etsin tähän ohjeen (https://www.webhi.com/how-to/how-to-install-java-with-apt-get-on-ubuntu-debian/).

Päivitin apt-getin, tarkistin onko javaa (ei ollut), asensin javan ja tarkistin asentamani javan version:

![image](https://github.com/user-attachments/assets/ad08cdb0-aa3e-4ba9-bd10-2eb1d66e3a33)

![image](https://github.com/user-attachments/assets/e8fba5ce-adb2-4161-ab38-d7f1c1ea2ecd)

Tein kansion nimeltään koodit ja siirsin tunnilla tehdyn Hei maailman Python-version sinne ja tarkistelin ls:llä välissä, että asiat olivat halutuissa paikoissa:

![image](https://github.com/user-attachments/assets/df177229-aa4a-473e-b1e4-0676ed1a8237)

*Melkein unohtui, nyt on 3.10.2024 13.35*

Seuraavaksi siirryin opettajan ohjeisiin (https://terokarvinen.com/2018/hello-python3-bash-c-c-go-lua-ruby-java-programming-languages-on-ubuntu-18-04/).

Annoin komennon `micro hello.java` ja kirjoitin koodin ohjeen mukaisesti.

![image](https://github.com/user-attachments/assets/b5cb1d3d-2f66-4b8b-8615-180102f2c9f5)

Ohjeissa annetaan komento javac ennen kuin koodi ajetaan. `man javac` kertoo, että kyseinen komento lukee annetun lähdetiedoston ja koostaa ne class-tiedostoksi.

Annoin komennon ja sain virheilmoituksen:

![image](https://github.com/user-attachments/assets/7bc3e34b-7e57-4ef5-930d-56470c8d9634)

Olin kopioinut huolimattomasti ja jättänyt luokka-osion pois. Ihmettelin vielä, eikö tähän tule mainintaa public classista ja silti en ollut tarkistanut kopioinko oikein. Samalla kun korjasin asian, nimesin myös tiedostot alkamaan isoilla kirjaimilla.

![image](https://github.com/user-attachments/assets/9d90e25e-c825-425a-a9ed-84599e06ca00)

Lopuksi ajoin ohjelman:

![image](https://github.com/user-attachments/assets/3d83f631-f7a9-40a1-943d-cf46114e9e06)

Toimii.

Kokeilin myös hieman pitempää Java-koodia:

![image](https://github.com/user-attachments/assets/c0cc6d4c-6e58-4599-84ab-0647a6d9cade)

Hyvin toimi! Tässä vielä cat-komennolla koodi:

![koodi](https://github.com/user-attachments/assets/c6ab24b1-44da-40c3-a258-4df3f9ee21af)


**C**

*Tauon jälkeen 3.10.2024 15.46*

Debianin sivujen (https://www.debian.org/doc/manuals/debian-reference/ch12.en.html#_coding_in_compiled_languages) mukaan C:tä käyttääkseen tarvitsee asentaa paketti gcc, mutta näköjään olin asentanut sen jo aiemmin:

![image](https://github.com/user-attachments/assets/ad482693-1c64-4ca8-b7a2-4c0352b868df)

Tein kooditiedoston ohjeidon mukaisesti ja ajoin sen ongelmitta:

![image](https://github.com/user-attachments/assets/1e6bfba1-ee0b-4c33-aca7-3c3748708c33)

**Bash**

GNU:n Bash-manuaalin (https://www.gnu.org/software/bash/manual/bash.html#What-is-Bash_003f) mukaan Bash on "shell" tai komentokieli GNU:n käyttöjärjestelmille ja sen nimi tulee sanaleikistä. Datacampin (https://www.datacamp.com/blog/what-is-shell) mukaan "shell" on puolestaan tietynlainen tietokoneohjelma, jonka avulla Linux ja Unix -käyttäjät voivat ohjata käyttöjärjestelmää komentorivikäyttöliittymästä.

Ilmeisesti olen siis käyttänyt Bashia jatkuvasti Debianin terminaalia käyttäessäni ja Bash-termiin onkin tämän kurssin aikana törmännyt säännöllisesti esimerkiksi silloin, kun antamaani komentoa ei ole tunnistettu:

![image](https://github.com/user-attachments/assets/6ecd7712-d865-4695-83ed-9928d1d6864d)

Tarkistin vielä Bashin version:

![image](https://github.com/user-attachments/assets/ea14ec46-421a-48cf-a762-59dafc282958)

Tämän jälkeen tein opettajan ohjeiden mukaisesti Bash-ohjelman:

![image](https://github.com/user-attachments/assets/42d62696-6f36-4baa-934c-56e70d1d2ff5)


## Linuxiin uusi komento, jota kaikki käyttäjät voivat ajaa

Eli palasin Bashin pariin.

Ensin tarvitsin jonkin komennon, jota tehtävässä käyttäisin. Apuna toimi Milica Dancukin artikkeli (https://phoenixnap.com/kb/bash-read) read-komennosta ja whoami:n käytöstä puolestaan opin esimerkiksi StackExchangen sivuilta (https://unix.stackexchange.com/questions/473947/using-whoami-to-search-for-files-that-mention-user).

Lopputulos:

![image](https://github.com/user-attachments/assets/83c4aa4e-bc2a-446d-b3c2-12af29b7e811)

*(luvattoman pitkään Bashin parissa vietetyn ajan jälkeen eli 17.51)*

Siirryin opettajan ohjesivulle (https://terokarvinen.com/2007/12/04/shell-scripting-4/), tehdäkseni komennosta sellaisen, että kaikki käyttäjät voivat käyttää sitä. Kysyin ChatGPT:ltä, mitä komennon eri kohdat tekevät. `#!/bin/bash` lisätään komentotiedoston alkuun ja tämän avulla järjestelmä tunnistaa, että kyseinen koodi suoritettaan Bashilla. Tämän jälkeen komennolla `chmod a+x lspwd` annetaan kaikille käyttäjäille suoritusoikeudet tiedostoon lspwd. Komennolla `./lspwd` koodi suoritetaan.

Lisäsin ensin vaaditun pätkän tiedoston alkuun:

![image](https://github.com/user-attachments/assets/219a9581-2dcd-4276-b845-92997685e91f)

Oikeuksia antaessa tuli ongelmia vastaan, kun olin toiminut ohjeen mukaisesti. Tämän perusteella arvelin, että tiedostossa ei pitänyt olla päätettä ja poistin päätteen ja muokkasin nimen samalla lyhyemmäksi. Tämän jälkeen sain oikeudet annettua ja testasin komentoa:

![image](https://github.com/user-attachments/assets/cd06ca86-7a24-4f32-b179-1c9b5f5ab62e)

Testatakseni komentoa toisella käyttäjällä tein uuden käyttäjän nyar.

![image](https://github.com/user-attachments/assets/88f9d0c6-9aad-4ed4-a614-e7b98d2be9b5)

Vaihdoin käyttäjää, siirryin nyarin kotihakemistoon ja kokeilin komentoa, mutta jotain oli pielessä:

![image](https://github.com/user-attachments/assets/74dcf140-20c5-4241-8688-c31abc2eb2d8)

Palasin käyttäjänä nyar käyttäjän jenni kansioon koodit ja kokeilin uudestaan. Siellä komentoi toimi:

![image](https://github.com/user-attachments/assets/dbcd2c55-a344-47cc-a3c7-76ab767efbd4)

*4.10.2024 19.55*

Seuraavan tehtävän vaihtoehtoja tarkastellessani tulin siihen tulokseen, että komennon kuuluisi toimia muuallakin kuin kotihakemistossa. Olin lopussa googlettanut asiaa, mutta saanut liian monimutkaiselta vaikuttavan ratkaisun, joten olin jättänyt asian siihen. Nyt palasin kuitenkin tarkastelemaan opettajan ohjetta ja kommenteissa olikin ohje siihen, kuinka komento saadaan toimimaan kaikkialla. Testasin ensiksi asian alusta alkaen tekemällä samanlaisen lspwd-komennon, kuin opettaja oli tehnyt ja kun se toimi ongelmitta, muokkasin myös omaa komentoani.

Annoin komennon `sudo cp moi /usr/local/bin/`, vaihdoin käyttäjäksi nyar ja kokeilin komentoa `moi` nyarin kotihakemistossa. Toimi:

![image](https://github.com/user-attachments/assets/1b019f58-277f-4173-84ef-05328ac470ad)

## c) Ratkaise vanha arvioitava laboratorioharjoitus soveltuvin osin

Edellisen lisäksi tehtäviä tarkastellessani tulin siihen tulokseen, että käyttäoikeuksiin liittyvät tietoni kaipaavat syvennystä. Luin aiheesta Scott McBrienin artikkelia (https://www.redhat.com/sysadmin/linux-file-permissions-explained) ja tarkastelin omia tiedostojani komennolla `ls -l`.

![image](https://github.com/user-attachments/assets/9dda96d1-4f3b-4ba8-98b4-afefb8b6d69d)

Kuvassa näkyviin tiedostoihin käyttäjällä jenni on kaikkiin read (r) ja write (w) -oikeudet ja lisäksi kansioon ja ohjelmiin on myös execute (x) oikeudet. Muut käyttäjät ovat automaattisesti saaneet tekemiini tiedoistoihin read-oikeudet ja kansioon read ja execute -oikeudet. Edellisessä tehtävässä muokkasin komennolla `chmod a+x moi` ohjelmaa moi siten, että kaikilla oli siihen read ja execute oikeudet.

Olennaiset komennot McBrienin artikkelista poimittuna:

- chmod u : omistajan oikeuksien muokkaaminen
- chmod g : muut käyttäjät tiedoston ryhmässä
- chmod o : muut käyttäjät, jotka eivät ole tiedoston ryhmässä
- chmod a : kaikki käyttäjät
- chown-komennolla puolestaan voi muuttaa tiedoston omistajaa ja chgrp:lla ryhmää
- chmod ug+rwg esim.txt : omistajalle ja ryhmälle kaikki oikeudet tiedostoon
- chmod o+r esim.txt : muille lukuoikeus tiedostoon

Tarkistin vielä chmod:n man-sivulta, että muistin oikein, että jos +-merkin sijaan käytetään -, tällöin komento poistaa mainitut oikeudet. Kuten edellisen tehtävän komennosta ja yllä olevasta kuvakaappauksesta voi todeta, +:lla annettu komento on vain lisännyt pyydetyt oikeudet, mutta ei ole tehnyt mitään oikeuksille, joita komennossa ei mainittu.

*4.102024 23.00 palasin tehtävän pariin*

Valitsin tehtäväksi tämän vuoden kevään laboratoriotyön: https://terokarvinen.com/2024/arvioitava-laboratorioharjoitus-2024-linux-palvelimet/?fromSearch=laboratorio

**Pohjatyöt**

Ensiksi tarvitaan tyhjä Linux-virtuaalikone, jossa saa olla virtualisointiympäristön tuki, palomuuri ja asennuksen mukana tulevat oletuspaketit. Ohjelmat saa päivittää.

Debianista oli ilmestynyt uusi versio, latasin sen:

![image](https://github.com/user-attachments/assets/22b127a7-5f00-4882-9a00-76bc795bf531)

Seurasin omaa raporttiani: https://github.com/jennimuhonen/linux-kurssi/blob/main/h1_oma-linux.md

Homma sujui ongelmitta raporttia seuratessa. Kokeilin paria vaihtoehtoista ratkaisua, mutta tulin siihen tulokseen, että raportti etenee järkevästi ja sivupolut aiheuttivat vain ongelmia. Kokeilin esimerkiksi jättää käymättä asetuksissa VirtualBoxin puolella ja hyvin pian jouduin palaamaan sinne. Kehitysehdotuksena itselleni raporttiin voisi vielä lisätä testi-Debianin työpöydällä olevan asennuskuvakkeen ja pari muuta pientä viilausta.

Tässä se pyörii, uuden version myötä yläkulman kuvakkeeseen oli ilmestynyt jokin juuston kaltainen möhkäle:

![image](https://github.com/user-attachments/assets/cb1783b3-d6d9-409b-8dce-31b109e71529)

Edellä mainittua raporttia tehdessä en ollut huomannut tehdä päivityksiä tai asentaa palomuuria. Siksi listaan tähän tiivistetysti askeleet itselleni muistiin. Ohjeena toimi opettajan ohje (https://terokarvinen.com/2021/install-debian-on-virtualbox/).

1. Päivitetään eli `sudo apt-get update` ja sen jälkeen `sudo apt-get -y dist-upgrade`
2. Palomuuri `sudo apt-get -y install ufw` ja sen jälkeen `sudo ufw enable`
3. Käynnistä uudelleen (Applications -> Log out -> Restart)

Ja tämä oli se, mitä sai olla valmiina ennen varsinaista tehtävää.

**Ongelma asennuksessa**

Seuraavaksi muistelin, mitä pieniä mukavuuksia kurssin myötä on asennettu.

Ensimmäisenä ryhdyin luonnollisesti opettajan edellisten ohjeiden loppupätkä, joilla mahdollistetaan virtuaalityöpöydän koon kasvattaminen

Tässä kohtaa eteen tuli ongelmia, kun yritin tehdä asennusta:

![ajureidenAsennus](https://github.com/user-attachments/assets/0591881b-b5c8-4e5a-a485-4edf91466166)

Jouduin käynnistämään jumiutuneen Debianin uudestaan ja sen jälkeen kävin katsomassa lokitiedostoa:

![ajureidenAsennus2](https://github.com/user-attachments/assets/b638f0ef-b65f-4ddf-a6d6-0ba3e5683e89)



![ajureidenAsennus3](https://github.com/user-attachments/assets/8c5887cf-78db-4276-9c3f-8d5d1c6c44c2)

![ajureidenAsennus4](https://github.com/user-attachments/assets/80f100f3-c8f5-4a8d-9308-c6b0bd02631a)


(Homma päätyi virheilmoitukseen, kehotukseen katsoa logia ja siellä tietoon, että ei asennettu. Kokeilin aloittaa alusta ja kokeilin klikata päivitä, mutta kehottaa reboottaamaan Guestin Virtual Boxissa.)

Tässä kohtaa aloin arvella, että ehkä pikkukuvakkeessa näkynyt juustonpalanen olikin hätähuuto. Olin Debianin asennusta tehdessä unohtanut, että asetuksissa oli määritetty Debian 64-bittiseksi 32-bittisen sijaan ja muuttanut tämän vasta yritettyäni aloittaa asennusta ja saatuani virheviestin. Ehkä tässä kohtaa jokin oli mennyt pieleen.

Päätin asentaa Debianin alusta ja nyt kuvake näytti oikealta. (Olisi varmaan selkeyden nimissä pitänyt nimetä tämä joksikin muuksi kuin reppuliksi, mutta kyseessä siis alla olevassa kuvassa DebianTheThird ja juustopalallinen on DebianTheSecond, josta edellinen kuvakaappaus on.)

![image](https://github.com/user-attachments/assets/d5ad5f58-3459-455f-86c2-9b1e08334967)




---

**Lähteet**

- Dancuk, Milica: How To Use The Bash read Command. https://phoenixnap.com/kb/bash-read
- Datacamp: What is Shell? https://www.datacamp.com/blog/what-is-shell
- Debian: Chapter 12. Programming. https://www.debian.org/doc/manuals/debian-reference/ch12.en.html#_coding_in_compiled_languages
- GNU: Bash Reference Manual. https://www.gnu.org/software/bash/manual/bash.html#What-is-Bash_003f
- Karvinen, Tero 2007: Shell Scripting. https://terokarvinen.com/2007/12/04/shell-scripting-4/
- Karvinen, Tero 2018: Hello World Python3, Bash, C, C++, Go, Lua, Ruby, Java – Programming Languages on Ubuntu 18.04. https://terokarvinen.com/2018/hello-python3-bash-c-c-go-lua-ruby-java-programming-languages-on-ubuntu-18-04/
- man chmod
- man javac
- McBrien, Scott: Linux file permissions explained. https://www.redhat.com/sysadmin/linux-file-permissions-explained
- StackExchange: Using whoami to search for files that mention user. https://unix.stackexchange.com/questions/473947/using-whoami-to-search-for-files-that-mention-user
- WebHi: How to install Java with “apt-get” on Ubuntu / Debian. https://www.webhi.com/how-to/how-to-install-java-with-apt-get-on-ubuntu-debian/

---
  
*Tätä dokumenttia saa kopioida ja muokata GNU General Public License (versio 2 tai uudempi) mukaisesti. http://www.gnu.org/licenses/gpl.html*

*Pohjana Tero Karvinen 2024: Linux kurssi, http://terokarvinen.com*

*Raportin tekijä: Jenni Muhonen*
