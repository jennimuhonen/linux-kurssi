# h6 Hello Django

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

---

## Extra, kirjautumismysteerin salaisuus

*26.9.2024 12.56*

Olin aiemmin ihmetellyt, miksi en pääse kirjautumaan UpCloudin virtuaali-Debianiini salasanalla, vaikka se oli alunperin asetustiedostossa sallittuna. Ratkaisu ongelmaan löytyi viime oppitunnilla, kun kanssaopiskelijalla oli toisenlainen kirjautumishaaste eri palvelun virtuaalipalvelimella. Aivan tunnin lopuksi hän kertoi löytäneensä ongelmaan ratkaisun eli asetustiedossa oli linkki toiseen asetustiedostoon, jossa oli tämä ongelmia aiheuttanut asetus. Koska linkki on tiedoston alussa, tämä yliajaa myöhemmin tulevat asetukset. (Tämän opin edellisen kerran tehtäviä tehdessä.) Opettaja kehotti ratkaisemaan ongelman poistamalla kyseisen linkin.

Tutkin tämän perusteella omaa asetustiedostoani ja löysin sieltä kuvatunlaisen linkin:

![image](https://github.com/user-attachments/assets/1580d6cd-6f6e-4921-b7db-71364a1cda7c)

![image](https://github.com/user-attachments/assets/6090a7e7-8fef-4490-820e-a75ae3e3da3c)

Kävin tutkimassa, mitä tiedostosta löytyy ja kuten arvata saattoi, siellä estettiin kirjautuminen salasanalla:

![image](https://github.com/user-attachments/assets/0bbd4f9d-f1cd-4fc4-9e48-22d47b8b5811)

![image](https://github.com/user-attachments/assets/c9ed0025-e69c-4d71-b2ad-a5a8f0ef2c9d)

Noudatin opettajan ohjeita ja poistin alkuperäisestä tiedostosta linkin ylimääräisiin asetuksiin.

Testasin muutokset:

![image](https://github.com/user-attachments/assets/2ceac9c0-d29e-4977-81bc-5b34c1b42914)

![image](https://github.com/user-attachments/assets/09b414ac-8f70-47f6-b8ab-5176cf641ed8)

Tein uuden testihenkilön, jolla ei ole ssh-avaimia ja kokeilin, pääseekö tällä tunnuksella sisään:

![image](https://github.com/user-attachments/assets/7d4dd441-f4e8-4e6e-ae20-3f94f8fb9ee7)

Muutaman salasanan typotuskerran jälkeen kirjautuminen onnistui!

Tämän jälkeen yritin kieltää salasana-kirjautumisen uudestaan. Tässä kohtaa tuli ongelmia vastaan ja jostain syystä testi-käyttäjäni pääsi edelleen salasanalla sisään, vaikka olin laittanut PasswordAuthentication no. Lopulta päädyin lisäämään alkuperäisen rivin asetustiedostoon takaisin ja tämän jälkeen testi-käyttäjä ei päässyt enää salasanalla sisään.

(Viimeistä haastetta selvitellessäni huomasin, että opettaja on antanut aiemmin ohjeen (https://terokarvinen.com/2017/first-steps-on-a-new-virtual-private-server-an-example-on-digitalocean/), että uudelleenkäynnistys hoidetaan tällä komennolla: `sudo service ssh restart`. Käytin tätä palauttaessani asetuksia. (Kysyin ChatGPT:ltä mitä eroa komennoilla `sudo systemctl restart sshd` ja `sudo service ssh restart` on ja sen mukaan molemmat komennot suorittavat saman perustoiminnon eli käynnistävät uudelleen SSH-palvelun. En jäänyt selvittämään asiaa enempää.)

## Tee yksinkertainen esimerkkiohjelma Djangolla

Aloitin lukemalla opettajan ohjesivun: https://terokarvinen.com/2022/django-instant-crm-tutorial/.

Tunnilla opettaja kertoi, että asennamme Djangon virtuaaliympäristöön, jotta voimme tarvittaessa asentaa Djangon toistamiseen. En vielä tunnin perusteella täysin ymmärtänyt mistä virtuaaliympäristöissä oli kyse, joten katsoin täydennykseksi Youtubesta tecladon videon alkupuoliskon (https://www.youtube.com/watch?v=KxvKCSwlUv8), jossa hän selitti virtuaaliympäristöä. Tiivistetysti tulkitsin, että seuraavan ohjelman kohdalla Python-versio voi olla eri, mutta sen päivittäminen voisi sotkea aiemman ohjelman toiminnan ja tämän takia Pythonit halutaan ajaa eri ympäristöissä. Lisäksi eri ohjelmat saattavat kaivata erilaisia lisäpalikoita. Erillisten virtuaaliympäristöjen avulla nämä palikat ja versiot voidaan eristää toisistaan.

Opettaja myös varoitti, että koska tällä kerralla joudumme käyttämään apt-get:n sijaan pip:iä Djangon asentamiseen, kirjoitusvirheitä on parempi olla tekemättä. Jos asennustiedoston nimen kirjoittaa väärin, on erittäin suuri mahdollisuus asentaa Djangon sijaan jokin haittaohjelma!



---

**Lähteet**

- ChatGPT.
- Karvinen, Tero 2017: First Steps on a New Virtual Private Server – an Example on DigitalOcean and Ubuntu 16.04 LTS. https://terokarvinen.com/2017/first-steps-on-a-new-virtual-private-server-an-example-on-digitalocean/
- Karvinen, Tero 2022: Django 4 Instant Customer Database Tutorial. https://terokarvinen.com/2022/django-instant-crm-tutorial/
- Karvinen, Tero: Oppitunti 25.9.2024. Linux-palvelimet. https://terokarvinen.com/linux-palvelimet/
- teclado 13.4.2021: The Complete Guide to Python Virtual Environments! https://www.youtube.com/watch?v=KxvKCSwlUv8

---
  
*Tätä dokumenttia saa kopioida ja muokata GNU General Public License (versio 2 tai uudempi) mukaisesti. http://www.gnu.org/licenses/gpl.html*

*Pohjana Tero Karvinen 2012: Linux kurssi, http://terokarvinen.com*

*Raportin tekijä: Jenni Muhonen*
