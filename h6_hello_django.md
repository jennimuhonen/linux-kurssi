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

Aloitin lukemalla opettajan ohjesivua: https://terokarvinen.com/2022/django-instant-crm-tutorial/.

Tunnilla opettaja kertoi, että asennamme Djangon virtuaaliympäristöön, jotta voimme tarvittaessa asentaa Djangon toistamiseen. En vielä tunnin perusteella täysin ymmärtänyt mistä virtuaaliympäristöissä oli kyse, joten katsoin täydennykseksi Youtubesta tecladon videon alkupuoliskon (https://www.youtube.com/watch?v=KxvKCSwlUv8), jossa hän selitti virtuaaliympäristöä. Tiivistetysti tulkitsin, että seuraavan ohjelman kohdalla Python-versio voi olla eri, mutta sen päivittäminen voisi sotkea aiemman ohjelman toiminnan ja tämän takia Pythonit halutaan ajaa eri ympäristöissä. Lisäksi eri ohjelmat saattavat kaivata erilaisia lisäpalikoita. Erillisten virtuaaliympäristöjen avulla nämä palikat ja versiot voidaan eristää toisistaan.

Opettaja myös varoitti, että koska tällä kerralla joudumme käyttämään apt-get:n sijaan pip:iä Djangon asentamiseen, kirjoitusvirheitä on parempi olla tekemättä. Jos asennustiedoston nimen kirjoittaa väärin, on erittäin suuri mahdollisuus asentaa Djangon sijaan jokin haittaohjelma!

**Kehitysympäristön asentaminen**

*26.9.2024 15.16 (tauon jälkeen)*

Opettajan ohjeita noudattaen ryhdyin asentamaan kehitysympäristöä.

Ensiksi asensin virtuaaliympäristön apt-getillä:

![image](https://github.com/user-attachments/assets/8882bc36-b47f-4be8-86d3-a6bac7b845d3)

(Tajusin unohtaneeni päivittää apt-getin, joten päivitin sen `sudo apt-get update` ja annoin komennon `sudo apt-get -y install virtualenv` uudelleen.)

Seuraavaksi ohjeissa annetaan komento `virtualenv --system-site-packages -p python3 env/`. Ohjeissa selitetään, että komento luo uuden kansion env/, jossa on uusimmat paketit ilmeisestikin kansiossa `lib/site-packages/`. Ja haluamme käyttää Python 3:ea.

Ohjeen selitystä kohdasta `--system-site-packages` en aivan ymmärtänyt, joten tarkistin mitä sanotaan `man virtualenv`. Siellä sanottiin, että kyseinen komento antaa virtuaaliympäristölle pääsyn systeemin "site-packages dir", joka oletuksena on "False". Eli ilmeisesti kyseinen hakemisto ei automaattisesti ole käytössä ja näin se otetaan käyttöön ja sitä kautta saadaan paketteja käytettäväksi. Man-sivulta myös totesin, että -p liittyy python3:een eli komennolla `-p python3` määritellään, että asennamme Python 3:n. (Käytin tulkinnan tukena myös ChatGPT:tä kysymällä, mitä komento tekee.)

Saatuani kuvan siitä, mitä olin tekemässä, annoin komennon:

![image](https://github.com/user-attachments/assets/9575d0e7-b63b-4582-958b-142a6c7b092b)

Tutkin, että kotihakemistossani oli tosiaan uusi env-kansio ja sen syvyyksistä löytyi site-packages-kansio:

![image](https://github.com/user-attachments/assets/1231370d-a266-4c0a-848f-6d89b81fd147)

Seuraava komento ohjeissa on `source env/bin/activate` ja että tämä aktivoi virtuaaliympäristö. Komento vaatii jälleen hieman selvitystä ennen kuin annan sen. Kurkistin kansioon env/bin ja siellä näkyy olevan tiedosto activate:

![image](https://github.com/user-attachments/assets/a63b5bc8-50e1-4c31-8d73-ad37f690d417)

Geeksforgeeks-sivustoa (https://www.geeksforgeeks.org/source-command-in-linux-with-examples/) lukemalla ymmärsin, että source-komennolla suoritetaan mainittu tiedosto.

Annoin komennon:

![image](https://github.com/user-attachments/assets/2bd2d6a4-ebab-456a-ac26-6fe0fc95d75e)

Ohjeissa sanottiin, että komento luultavasti näyttää env:n alussa eli tällä ilmeisestikin viitataan yllä näkyvään.

Seuraava komento ohjeessa on `which pip` eli tällä tarkistetaan, että olemme varmasti asentamassa pip:llä virtuaaliympäristöön. Ohjeessa sanotaan, että pip:iä ei tule käyttää ilman virtuaaliympäristöä eikä sudo:n kanssa.

Tarkistin which:n man-sivulta, että kyseinen komento kertoo annetun tiedoston hakemistopolun.

Seuraavaksi annoin komennon ja pip näkyy olevan env-kansion alla, samoin kuin opettajan ohjeessa:

![image](https://github.com/user-attachments/assets/5a964df2-6ea6-42d4-a5ad-ca4123d822a9)

Seuraavaksi ohjeissa tehdään tiedosto, jossa lukee django ja tämän tiedoston avulla asennamme djangon komennolla `pip install -r requirements.txt`. Pyysin ChatGPT:tä selittämään tämän komennon ja ChatGPT:n mukaan yhteisen tiedoston käyttäminen on yleinen tapa jakaa Python projekteja, jotta kaikilla tiimissa on täsmälleen samat paketit ja versiot käytössään.

Noudatin ohjeita. Tein tiedoston ja tarkistin sisällön cat:lla ja asensin sen. Kopioin komennot ohjeista ja tarkistin, ennen kuin asensin, jotten tekisi virheitä ja asentaisi mitä sattuu:

![image](https://github.com/user-attachments/assets/a314d8a4-d042-4a01-8c71-6b0151a157fb)

Seuraavaksi tarkistetaan, onko uusin versio asennettuna:

![image](https://github.com/user-attachments/assets/18cab386-c010-456e-aaed-cfc464563478)

Tarkistin Djangon sivuilta (https://www.djangoproject.com/download/), että uusin virallinen versio on 5.1.1 eli näyttää oikealta.

**Django**

*26.9.2024 16.39*

Luin seuraavan pätkän ohjeita ja kokeilin käytännössä niiden mukaisesti:

![image](https://github.com/user-attachments/assets/16cea040-cfb1-442d-ac9c-0965db5b1b2c)

Ohjeissa, kuten tunnillakin sanottiin, että tämä on kehityspalvelin eli tätä ei saa viedä internetiin. Tästä ei pitäisi olla huolta, koska asensin kaiken virtuaaliboksin Debianille, en UpCloudin palvelimella olevalle.

Testasin selaimessa, kuten ohjeessa kehotettiin:

![image](https://github.com/user-attachments/assets/1573e213-c252-4682-8875-04491b85ad68)

Ja sivu näyttää siltä kuin ohjeen mukaan pitääkin.

Lopetin komennon ohjeen mukaan Ctrl + c ja katsoin sivua uudelleen. Nyt sivulla näkyi Unable to connect eli sivu on nähtävissä vain kun tuo komento on käynnissä.

Katsoin jotakin-kansioon ja sieltä löytyi manage.py:

![image](https://github.com/user-attachments/assets/eb3935c4-4fe2-40eb-997b-62422cea1e27)

**Admin-liittymä**

Seuraavaksi ohjeissa lisätään admin sivustolle, sillä tällä hetkellä sivustolle http://127.0.0.1:8000/admin/ ei vielä pääse kirjautumaan:

![image](https://github.com/user-attachments/assets/b09ac21b-d679-4043-92f5-5c11f2277d3a)

Ensiksi kuului päivittää tietokanta:

![image](https://github.com/user-attachments/assets/d0f787e5-a0c4-4aa4-a59e-18b0afbba6cf)



---

**Lähteet**

- ChatGPT.
- Django: How to get Django. https://www.djangoproject.com/download/
- Geeksforgeeks 19.6.2024: Source Command in Linux with Examples. https://www.geeksforgeeks.org/source-command-in-linux-with-examples/
- Karvinen, Tero 2017: First Steps on a New Virtual Private Server – an Example on DigitalOcean and Ubuntu 16.04 LTS. https://terokarvinen.com/2017/first-steps-on-a-new-virtual-private-server-an-example-on-digitalocean/
- Karvinen, Tero 2022: Django 4 Instant Customer Database Tutorial. https://terokarvinen.com/2022/django-instant-crm-tutorial/
- Karvinen, Tero: Oppitunti 25.9.2024. Linux-palvelimet. https://terokarvinen.com/linux-palvelimet/
- man virtualenv
- man which
- teclado 13.4.2021: The Complete Guide to Python Virtual Environments! https://www.youtube.com/watch?v=KxvKCSwlUv8

---
  
*Tätä dokumenttia saa kopioida ja muokata GNU General Public License (versio 2 tai uudempi) mukaisesti. http://www.gnu.org/licenses/gpl.html*

*Pohjana Tero Karvinen 2012: Linux kurssi, http://terokarvinen.com*

*Raportin tekijä: Jenni Muhonen*
