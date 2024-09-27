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

## a) Tee yksinkertainen esimerkkiohjelma Djangolla

Aloitin lukemalla opettajan ohjesivua: https://terokarvinen.com/2022/django-instant-crm-tutorial/.

Tunnilla opettaja kertoi, että asennamme Djangon virtuaaliympäristöön, jotta voimme tarvittaessa asentaa Djangon toistamiseen. En vielä tunnin perusteella täysin ymmärtänyt mistä virtuaaliympäristöissä oli kyse, joten katsoin täydennykseksi Youtubesta tecladon videon alkupuoliskon (https://www.youtube.com/watch?v=KxvKCSwlUv8), jossa hän selitti virtuaaliympäristöä. Tiivistetysti tulkitsin, että seuraavan ohjelman kohdalla Python-version saatetaan haluta olevan eri, mutta Pythonin päivittäminen voisi sotkea aiemman ohjelman toiminnan ja tämän takia Pythonit halutaan ajaa eri ympäristöissä. Lisäksi eri ohjelmat saattavat kaivata erilaisia lisäpalikoita. Erillisten virtuaaliympäristöjen avulla nämä palikat ja versiot voidaan eristää toisistaan.

Opettaja myös varoitti, että koska tällä kerralla joudumme käyttämään apt-get:n sijaan pip:iä Djangon asentamiseen, kirjoitusvirheitä on parempi olla tekemättä. Jos asennustiedoston nimen kirjoittaa väärin, on erittäin suuri mahdollisuus asentaa Djangon sijaan jokin haittaohjelma!

**Kehitysympäristön asentaminen**

*26.9.2024 15.16 (tauon jälkeen)*

Opettajan ohjeita noudattaen ryhdyin asentamaan kehitysympäristöä.

Ensiksi asensin virtuaaliympäristön apt-getillä:

![image](https://github.com/user-attachments/assets/8882bc36-b47f-4be8-86d3-a6bac7b845d3)

(Tajusin unohtaneeni päivittää apt-getin, joten päivitin sen `sudo apt-get update` ja annoin komennon `sudo apt-get -y install virtualenv` uudelleen.)

Seuraavaksi ohjeissa annetaan komento `virtualenv --system-site-packages -p python3 env/`. Ohjeissa selitetään, että komento luo uuden kansion env/, jossa on uusimmat paketit ilmeisestikin kansiossa `lib/site-packages/`. Ja haluamme käyttää Python 3:ea.

Ohjeen selitystä kohdasta `--system-site-packages` en aivan ymmärtänyt, joten tarkistin mitä sanotaan `man virtualenv`. Siellä sanottiin, että kyseinen komento antaa virtuaaliympäristölle pääsyn systeemin "site-packages dir", joka oletuksena on "False". Eli ilmeisesti kyseinen hakemisto ei automaattisesti ole käytössä ja näin se otetaan käyttöön ja sitä kautta saadaan paketteja käytettäväksi. Man-sivulta myös luin, että -p liittyy python3:een eli komennolla `-p python3` määritellään, että asennamme Python 3:n. (Käytin Man-tekstin tulkinnan tukena myös ChatGPT:tä kysymällä, mitä komento tekee.)

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

Seuraavaksi ohjeissa tehdään tiedosto, jossa lukee django ja tämän tiedoston avulla asennamme Djangon komennolla `pip install -r requirements.txt`. Pyysin ChatGPT:tä selittämään tämän komennon ja ChatGPT:n mukaan yhteisen tiedoston käyttäminen on yleinen tapa jakaa Python projekteja, jotta kaikilla tiimissa on täsmälleen samat paketit ja versiot käytössään.

Noudatin ohjeita. Tein tiedoston ja tarkistin sisällön cat:lla ja asensin sen. Kopioin komennot ohjeista ja tarkistin ne vielä ennen enterin painallusta, jotten tekisi virheitä ja asentaisi mitä sattuu:

![image](https://github.com/user-attachments/assets/a314d8a4-d042-4a01-8c71-6b0151a157fb)

Seuraavaksi kuului tarkistaa, onko uusin versio asennettuna:

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

Seuraavaksi ohjeissa lisätään ylläpitäjä sivustolle, sillä tällä hetkellä sivulle http://127.0.0.1:8000/admin/ ei vielä ole kirjautumistunnuksia olemassa:

![image](https://github.com/user-attachments/assets/b09ac21b-d679-4043-92f5-5c11f2277d3a)

Ensiksi kuului päivittää tietokanta:

![image](https://github.com/user-attachments/assets/d0f787e5-a0c4-4aa4-a59e-18b0afbba6cf)

Jatkoin ohjeiden mukaan eli asensin salasanageneraattorin, loin sillä salasanan ja loin superkäyttäjän. Lisäksi laitoin palvelimen pyörimään, jotta pääsen sivulle:

![image](https://github.com/user-attachments/assets/8ab9e804-c79b-405c-889f-6476ccc5340d)

Kirjauduin käyttäjätunnuksella ja salasanalla admin-sivulle:

![image](https://github.com/user-attachments/assets/7e36796a-e808-4467-87c9-44a2add8ab9a)

Seuraavaksi ohjeissa kehotettiin tekemään toinen käyttäjä ja antamaan myös hänelle superkäyttäjän oikeudet. Tein saman kuin edellä eli generoin salasanan ja loin uuden superkäyttäjän komennolla `./manage.py createsuperuser`. Uuden käyttäjän käyttäjänimi on joku ja myös tämä käyttäjä pääsi onnistuneesti kirjautumaan:

![image](https://github.com/user-attachments/assets/176ebd8f-b373-4dce-8d15-4a6fc58ac034)

Tein kolmannen käyttäjän ja tämä tein käyttöliittymän puolelta ja generoin hänelle toisessa avaamassani terminaalissa salasanan. Näköjään käyttöliittymän kautta tehdessä löytyivät valinnat superuser ja staff eli varmaan tämä oli tehtävän alkuperäinen tarkoitus. Valitsin käyttäjälle testi nämä molemmat, tallensin ja kirjauduin ulos.

![image](https://github.com/user-attachments/assets/fec05c78-39e2-4208-bb7b-09d872abf430)

Myös käyttäjä testi pystyi vastaavaan tapaan hallinnoimaan käyttäjiä kuin edellisetkin.

**Asiakaspalvelin (customer database)**

Jatkoin ohjeiden seuraamista, ensimmäisenä luotiin uusi kansio crm:

![image](https://github.com/user-attachments/assets/39386945-fe0a-4905-9e2b-853469fecea1)

Päivitin asetustiedostoa ohjeiden mukaisesti eli lisäsin riville 40 `'crm',`:

![image](https://github.com/user-attachments/assets/eb37fba4-9fb5-49c3-b3a1-07854e9465bb)

![image](https://github.com/user-attachments/assets/fd42d82b-57ea-4aa5-9f49-3c43b9491204)

Seuraavaksi ohjeissa lisätään malleja (models). Ohjeiden mukaan Customer-luokka luo customer-taulukon tietokantaan nimi-sarakkeen kera.

![image](https://github.com/user-attachments/assets/c86752bf-1410-45a6-8ce2-365b87895fd6)

Ja päivitettiin muutokset tietokantaan:

![image](https://github.com/user-attachments/assets/12147d99-519d-4cfb-aa96-b5e521e09095)

![image](https://github.com/user-attachments/assets/d0c4c656-4267-4169-9119-9e24812a3a62)

Seuraavaksi ohjeissa todetaan, että nähdäksemme uuden tietokantamme admin-sivulla, meidän täytyy rekisteröidä se:

![image](https://github.com/user-attachments/assets/714a9b0e-5fa6-4dfc-8826-ca3832c7f46c)

![image](https://github.com/user-attachments/assets/81018cfe-1022-4b23-9ccb-cd6911804b58)

Ja tämän jälkeen mennään jälleen admin-sivulle katsomaan, mitä varsinaisesti tulikaan tehtyä.

![image](https://github.com/user-attachments/assets/9490c138-a9dd-4dd4-ad5c-1aab87313a34)

![image](https://github.com/user-attachments/assets/f7e4cc15-22d8-4a1a-9df0-ca94e17b3317)

Ja siellähän tämä uusi taulu näkyy olevan!

Lisäsin kolme uutta asiakasta ja näköjään heille annetut nimet eivät näy tässä näkymässä:

![image](https://github.com/user-attachments/assets/ceae559f-40c5-418f-b787-bc07d3d362e8)

Poistin, lisäsin ja poistin vielä yhden käyttäjän ja totesin, että kukin saa yksilöllisen numeron sulkuihin:

![image](https://github.com/user-attachments/assets/ae11644f-a058-46cd-9121-051251e0b49d)

**Asiakkaiden nimet**

Viimeisenä ohjeissa päivitetään vielä nimet kuntoon, joten kävin päivittämässä tiedoston tämän mukaisesti:

![image](https://github.com/user-attachments/assets/12ab128a-0949-4f5f-8e8f-530770615ead)

![image](https://github.com/user-attachments/assets/69d35c39-84d7-466e-9d9b-052fa910689d)

Unohdin ajaa muutokset ja käynnistin palvelimen suoraan, joka sai palvelimen sekaisin:

![image](https://github.com/user-attachments/assets/3c594931-9ddf-4fba-abbf-245ec63dd5bf)

Kokeilin ajaa muutoksia, mutta sain samaa virheviestiä:

![image](https://github.com/user-attachments/assets/b99da804-f8c0-4cfa-8afb-55caeaadb810)

Otin muutokset pois ja tämän jälkeen palvelin käynnistyi taas:

![image](https://github.com/user-attachments/assets/1aa18cbc-2fdd-4415-ae4a-79d7842eceaf)

Lisäsin muutokset uudestaan ja muistin ajaa muutokset. Tässä kohtaa kävi ilmi, että muutoksessa itsessään oli jotain vikaa, koska sain jälleen virheilmoituksia.

![image](https://github.com/user-attachments/assets/2323d140-2281-4d08-8f2e-408a1c29753c)

Etsin yllä olevasta mainintaa viimeisimmästä muokkaamastani tiedostosta, koska ongelma hyvin ilmeisesti liittyi siihen. Aivan lopussa on maininta kyseisestä tiedostosta ja viittaus riville 8. Tutkin asiaa ja virhe korjautui muuttamalla nimikentän maksimipituudeksi 160 (kuten ohjeessakin oli). Olin huomannut, että ohjeessa pituus oli aiemmin 300 ja uudessa se oli 160, mutta jätin sen muuttamatta, koska ohjeessa ei tätä kehotettu muuttamaan. (Tämä oli mukavan helposti tutkittava ja korjattava virhetilanne eli onneksi en ollut muuttanut tätä heti. Nyt pääsin hieman näkemään minkälaisia ongelmia voi tulla vastaan.) Veikkaan, että etusivun nimikenttä on jossain määritelty lyhyemmäksi kuin 300, jonka takia uusi muutos oli virheellinen.

Korjausten jälkeen palvelin käynnistyi ja antamani nimet näkyivät:

![image](https://github.com/user-attachments/assets/6c4807a0-dd0a-476e-afbc-105082adaa8e)

Tehtävä oli oikein opettavainen ja hieman kun opiskelisi Pythonia, voisi kokeilla jotain omaakin.

## b) Tee Djangon tuotantotyyppinen asennus

*26.9.2024 20.21 (eli tauon jälkeen)*

Asiaa harkittuani päätin olla asentamatta Djangoa virtuaalipalvelimen puolelle ja pysyä VirtualBoxin Debianilla, sillä Python-osaamiseni pitäisi olla parempaa (tai edes olemassa) ennen kuin haluan jakaa mitään kenenkään nähtäville.

Luin opettajan ohjeita (https://terokarvinen.com/2022/deploy-django/) jo ennen taukoa perehtyäkseni aiheeseen. Ohjeiden alkupuolella on paljon asioita, jotka on tehty jo aiemmin kurssilla, joten poimin vain uusia asioita ohjeen alkupuoliskolta.

Päivitin apt-getin jo aiemmin tänään, joten hyppäsin suoraan asentamaan bash-completionia, jota minulla ei vielä ollut.

![image](https://github.com/user-attachments/assets/c5221763-afb9-43c9-a832-fa50e9344eb9)

Tämän avulla Tab:ia painamalla voi täydentää tiedostonimiä. (Näppärää!)

Tein uuden kansion ja alikansion projektia varten:

![image](https://github.com/user-attachments/assets/cde33ce9-ee8f-4443-aa65-ea37fb088f8d)

Tarkistin, miten Apachella menee. Ohjeiden mukaan kaikki on hyvin, jos ainoa valitus on AH00558 ja sanotaan Syntax OK. Näin oli eli kaikki vaikutti olevan ok:

![image](https://github.com/user-attachments/assets/0ce5d94f-acb1-4120-be05-4acfedc88f64)

Tein uuden virtuaaliympäristön uudelle projektille ja aktivoin sen. Arvelin, että ympäristön nimenä mikalie olisi ärsyttävän pitkä, joten ympäristöstä tuli lie:

*(Lisäys 27.9. 21.26: Koska käytin samaa projektia samalla koneella, minun olisi kannattanut käyttää jo olemassaolevaa virtuaaliympäristöä. Toisaalta lienee käytännöllistä, että ympäristö on kansiorakenteessa lähempänä kuin alkuperäinen ympäristö, sillä muuten saattaisin helpommin rikkoa linkityksen, jos päätyisin tekemään jotain pieniä kansiomuutoksia. Jostain myös luin/näin videolta, että yleensä käytetään ympäristön nimenä env tai venv eikä aleta nimeämään niitä miksi sattuu. Myös mikalie-kansio aiheutti ylimääräistä säätämistä myöhemmin. Sen sijaan ohjeessa oli olennaisia kohtia, joista hyppäsin yli, kuten myöhemmin raportista voi lukea.)*

![image](https://github.com/user-attachments/assets/7618aae8-9d47-4136-bc9a-cb23e8262243)

Tarkistin, että käytä pip:iä oikeassa paikassa. Olin aiemmin tehnyt vaatimustiedoston kotihakemistossa, joten voin käyttää samaa tiedostoa uudestaan. Sen jälkeen asensin Djangon ja tarkistin asennuksen.

![image](https://github.com/user-attachments/assets/e980900d-45e3-49d1-8bb0-ff964e2c616e)

Ohjeissa sanotaan, että voin kopioida aiemmin tekemäni projektin. Tein siis näin ja eli kopioin projektin kansioon publicprojekti. Tunnilla oli puhetta kopioimisesta ja tarkistin komennon vielä Shittu Olumiden artikkelista (https://www.freecodecamp.org/news/how-to-copy-a-directory-in-linux-use-the-cp-command-to-copy-a-folder/).

![image](https://github.com/user-attachments/assets/63cb0f80-86d0-4e1c-bec4-9806c49b7ade)

**Python & Apache**

Seuraavaksi ohjeissa todetaan, että tarvitsen tietooni kolme tiedostopolkua.

1. Django-protektin pääkansio: /home/jenni/publicprojekti/jotakin (TDIR)
2. wsgi.py: /home/jenni/publicprojekti/jotakin/jotakin/wsgi.py (TWSGI)
3. Virtualenv site-packages directory: /home/jenni/publicprojekti/lie/lib/python3.11/site-packages (TVENV)

Bash-completionista on ollut paljon iloa tätä tehtävää tehdessä ja esimerkiksi yllä olevat osoiteet kopioin tähän komentoriviltä, johon etsin ne bash-completionin avulla. (Kuten ohjeessakin kehotettiin tekemään.) Lisäsin tiedostojen perään ohjeen mukaiset lyhenteet, joita käytetään pian. Lisäksi otin ylimääräiset / lopusta pois, sillä tiedostopolut tullaan kopioimaan ilman niitä.

Ohjeessa kehotetaan tekemään django-käyttäjä, jolla ei ole sudo-oikeuksia. Koska en ole verkkopalvelimen puolella ja en ole julkaisemassa verkkoon, en tee erillistä käyttäjää. Virtuaalipalvelimen puolella olen tehnyt parikin eri testikäyttäjää testattuani SSH-avaimiin liittyviä ongelmia, toinen pääsee kirjautumaan SSH-avaimilla ja toinen ei eivätkä kumpikaan ole sudo-ryhmässä, joten jätän VirtualBoxin puolella käyttäjien kanssa säätämisen tekemättä.

Tein tiedoston ohjeiden mukaisesti:

![image](https://github.com/user-attachments/assets/7bc22c84-e738-4c39-a2f2-cde1f955b443)

![image](https://github.com/user-attachments/assets/11244c28-035d-4362-99a2-92cd9220f3a3)

Ja tarkistin, että tiedosto on oikeassa paikassa:

![image](https://github.com/user-attachments/assets/214cc349-c5e5-46fe-b177-92cd159698a1)

Asensin Apache WSGI moduulin:

![image](https://github.com/user-attachments/assets/1b3d40dc-a72c-45b3-8ae9-302c5db8095d)

Tarkistin, että Apachella on kaikki kunnossa. Viesti on edelleen sama kuin aiemmin. 

![image](https://github.com/user-attachments/assets/1315dfcb-f457-408d-af69-79f01ec4ad18)

Testaamisen myötä huomasin, että jotain oli pielessä. Tiesin aiempien viikkojen ongelmanselvittelyjen pohjalta, että näkyvissä oli var-kansion default-sivu, jonne päädytään helposti esimerkiksi silloin, kun conf-tiedostossa on jotain häikkää:

![image](https://github.com/user-attachments/assets/b64925d0-fd67-406c-979e-b9e57df2f7eb)

![image](https://github.com/user-attachments/assets/0737fd71-8cb4-49d6-aa70-ee617154b89c)

Kurkistin tekemääni conf-tiedostoon, jossa viitataan static-kansioon, jota minulla ei tietenkään ole:

![image](https://github.com/user-attachments/assets/3b46d594-c37d-4e1e-aba4-0e7ec324d26a)

Palasin tarkistamaan ja seuraamaan alkupään ohjeita.

Korjasin static:n tilalle mikalie ja tarkistin, ettei mitään unohtunut:

*(Lisäys 27.9. 21.39: kansion nimenä olisi kannattanut pitää static, muutin tämän myöhemmin takaisin.)*

![image](https://github.com/user-attachments/assets/a4d169e8-21cb-44c7-8f6e-328603ff06d1)

Static-kansio on ohjeissa kansion terocon alla eli minun tapauksessani mikalie:n pitäisi olla jotakin:n alla. Katsoin Vivek Giten sivuilta (https://www.cyberciti.biz/faq/mv-command-howto-move-folder-in-linux-terminal/) kuinka tiedostoja siirretään ja siirsin kansion:

![image](https://github.com/user-attachments/assets/2468653b-e305-4217-95e4-4686e83b3344)

Tein index-sivun:

![image](https://github.com/user-attachments/assets/4fef5614-2aee-43df-b82e-ac7cb8b41b55)

Tein conf-tiedoston:

![image](https://github.com/user-attachments/assets/4b1fd43e-49d0-4df1-9946-2caa7c513a3f)

Ja poistin sen tajuttuani, että sitä ei tarvittu. Tässä kohtaa ohjetta tehtiin jotakin-tiedostoa vastaava conf-tiedosto, joka myöhemmin päivitettiin tuohon hieman ylempänä raportissa näkyvään muotoon.

![image](https://github.com/user-attachments/assets/17a6ffa9-58fa-45e7-a6e9-2a6c08f02e1d)

Jossain vaiheessa aiemmin olin miettinyt, että jokin vaihe oli mahdollisesti jäänyt tekemättä ja tässä kohtaa totesin, että tämä puuttuva komento oli a2ensite. Koska jotakin.conf olisi oikeutettu jo aiemmin, mutta en siinä kohtaa seurannut ohjeita, jäi tämä vaihe epähuomiossa välistä. Tein siis nyt ohjeiden mukaisesti, default-tiedosto otettiin myös pois käytöstä:

![image](https://github.com/user-attachments/assets/78c8c137-c004-4daf-be8e-74550027e7c1)

Nyt localhost näytti conf-kansiossa aakkosjärjestyksessä seuraavana olevaan tiedostoon liittyvän sivun (aakkosjärjestysasian opin edellisiä tehtäviä tehdessä): 

![image](https://github.com/user-attachments/assets/b2bf1c9e-3b2f-46cf-9e5f-f4faebd10b13)

Tiedostoissa on siis luultavasti keskenään hieman ristiriitaisia tietoja, joten otin hattu.example.comin pois häiritsemästä:

![image](https://github.com/user-attachments/assets/3507674b-eedc-4ced-94c2-7923e2e55eca)

Ja lopultakin toimii:

![image](https://github.com/user-attachments/assets/620278a7-5aa7-4a15-9286-575d1f50166c)

Tämän jälkeen tarkistettiin, että kyseessä on varmasti Apache eikä kehityspalvelin. Ja kyllä Apachehan se!

![image](https://github.com/user-attachments/assets/34123947-caf6-46fd-bb42-a3af1301acff)

Ja vielä selaimessa:

![image](https://github.com/user-attachments/assets/221e19b7-98ab-48f4-b8cc-77952a2cbfc3)

**DEBUG:n estäminen**
*27.9.2024 10:16*

Jatkoin opettajan ohjeiden mukaisesti muokkaamaan asetustiedostoa:

![image](https://github.com/user-attachments/assets/42d542c4-d6df-492b-937c-e2b4dd3b6e6b)

Ohjeiden mukaan localhost on testaamista varten ja domain-nimeksi se, mitä suunnittelee käyttävänsä tälle sivulle. Tässä tapauksessa en tietenkään ole suunnitellut mitään eli käytin helloa placeholderina:

![image](https://github.com/user-attachments/assets/a3f38e63-8ff6-4b8b-a29d-bb0b05dc3caf)

Seuraavaksi ohjeissa on komento `touch teroco/wsgi.py`. Touch:n man-sivun mukaan tällä komennolla muutetaan tiedoston
aikaleimoja. Annoin komennon, tarkistin Apachen tilan ja käynnistin sen uudestaan.

![image](https://github.com/user-attachments/assets/f23befd0-6dd3-48b1-88b4-6dfa6d83122c)

Ohjeiden mukaan nyt localhostin ei pitäisi toimia ja näin oli:

![image](https://github.com/user-attachments/assets/e6a7a388-49b0-4a9b-a311-e8a570fe682d)

Ohjeissa kehotettiin myös tarkistamaan jollain satunnaisella lisäyksellä osoitteen lopussa, ettei vastaan tule debug-näkymää. Ei tullut:

![image](https://github.com/user-attachments/assets/6fc10b0a-ebdc-470c-b418-d59eda38f695)

Admin-sivu sen sijaan toimi, mutta näytti kauhealta:

![image](https://github.com/user-attachments/assets/4b5930cb-d0bc-41ff-ae1d-c427e05ca78c)

Kokeilin myös kirjautua käyttäjänä "joku" ja samat tunnukset, jotka tein a-tehtävässä, toimivat edelleen:

![image](https://github.com/user-attachments/assets/d9ba70b8-b254-483a-94fd-5e4d89924fe5)

**Ulkonäön fiksaaminen**

Nyt opin miksi sen yhden kansion nimi ohjeissa oli static. Se viittaa staattisiin tiedostoihin, kuten CSS:ään. Kävin korjaamassa mikalien staticiksi selkeyden nimissä:

![image](https://github.com/user-attachments/assets/0ad831e9-789b-46e0-865b-012cd8fdf1d5)

![image](https://github.com/user-attachments/assets/f4149619-3487-45e9-9fe5-71a6e12593fd)

Tämän jälkeen jatkoin ohjeiden seuraamista eli siirryin muokkaamaan asetustiedostoa:

![image](https://github.com/user-attachments/assets/543a7f94-8874-4840-8805-abd509a71844)

Ohjeiden mukaan lisäyksen voisi tehdä mihin vain tiedostossa, mutta oikea paikka on alussa muiden importien kanssa:

*(Lisäys 27.9. 22.07: Kuvassa näkyvä paikka on liian ylhäällä. Komento tulee laittaa muutamaa riviä alemmas, kuten hieman myöhemmin voi lukea.)*

![image](https://github.com/user-attachments/assets/47e24648-6098-4acd-aa48-7b2c73f82ab4)

**Välipohdinta**

Tässä kohtaa aloin enemmän miettiä seikkaa, jota ajoittain pohdin jo aiemminkin b-tehtävää tehdessä. Olisiko jotain kohdan b-toimista kuulunut tehdä virtuaaliympäristössä Pythonin asentamisen lisäksi? Huomaan, etten aivan vielä hahmota virtuaaliympäristön ideaa. Which-pip komennon perusteella on selkeää, että sitä en voi käyttää virtuaaliympäristön ulkopuolella. Ja sillä asensin Pythonin eli sitä en varmasti voi käyttää virtuaaliympäristön ulkopuolella. Mutta eli rajautuuko virtuaaliympäristö env/lie-kansioiden sisään? Miten varsinainen projekti suhtautuu siihen? Onko virtuaaliympäristöllä väliä vain koodatessa? Entä koodaamisen ulkopuolella?

Asiaa mietittyäni minun ei ainakaan olisi kuulunut tehdä uutta virtuaaliympäristöä kopioidulle projektille, koska jos jotain olisi tässä vaiheessa muuttunut, vanhalla versiolla tehty projektini olisi solmussa. (Lisäys myöhemmin samana päivänä: Koska tein virtuaaliympäristön samoilla määrityksillä, niin ei siitä haittaakaan ollut, mutta olisin voinut käyttää myös alkuperäistä ympäristöä, kun se oli jo olemassa.)

Ryhdyin katsomaan Tech With Tim:n videota aiheesta (https://www.youtube.com/watch?v=Y21OR1OPC9A) ja hän toteaa, että virtuaaliympäristö on yksinkertaisesti vain kansio ja tämä kansio on loogista sijoittaa Python-projektin läheisyyteen, joka tätä ympäristöä tarvitsee.

**Takaisin aiheeseen**

Pohdintä liittyi seuraavaan komentoon eli tuleeko virtuaaliympäristöä käyttää komennon ´./manage.py collectstatic` yhteydessä. Laitoin alkuperäisen ympäristön päälle ja annoin sen jälkeen komennon:

![image](https://github.com/user-attachments/assets/4b39eec5-ea2b-4bbe-99a1-f57f10829c56)

![image](https://github.com/user-attachments/assets/73fd1881-c875-4a86-a2b6-d7fa0b14f825)

Jotain on kuitenkin pielessä joko edellä tekemieni muutosten kanssa tai virtuaaliympäristön käytössä:

![image](https://github.com/user-attachments/assets/687eb3fe-9dbc-488d-a34e-ca3a2cc0ecc5)

Testimielessä kokeilin komentoa virtuaaliympäristön ulkopuolella:

![image](https://github.com/user-attachments/assets/bc8e5de6-5fcb-435b-926e-3dc50c94a2f1)

Eli kyllä, tämä komento piti antaa virtuaaliympäristössä. Onko nyt kyse vain jostain kirjoitusvirheestä vai siitä, että jotain tekemistäni asioista olisi kuulunut tehdä virtuaaliympäristössä?

Luin raporttiani ja ongelmallista on varmasti ainakin se, että vaihdoin virtuaaliympäristön lennosta, mutta olen määrittänyt eri virtuaaliympäristön conf-tiedostoon.

(Lisäys samana päivänä, omaa pohdintaa oppimaani liittyen: näyttää siltä, ettei ole väliä muokkaanko ei-kooditiedostoja virtuaaliympäristön sisällä vai ulkona. Koska kaksi eri virtuaaliympäristöäni ovat identtiset, voin myös käyttää niitä rinnakkain ja vuorotellen. Conf-tiedostossa viittaan lie-ympäristöön. Tämän viittauksen avulla ohjelmalle määritetään oikea virtuaaliympäristö selaimessa pyöriessään. Voisin myös viitata env-ympäristöön.)

Seuraavaksi katsoin error.logia:

![image](https://github.com/user-attachments/assets/d9ef6feb-d551-4c35-bde7-084067803c3c)

Hetken tuijotettuani virhelokia keksin ongelman. Kuten virheilmoitukset ovat yrittäneet kertoa "NameError: name 'BASE_DIR' is not defined". Eli BASE_DIR:iä ei ole määritelty siinä kohtaa, kun yritän ohjata STATIC_ROOT:iin. Eli lisäämäni pätkä oli hivenen liian ylhäällä ja tiedossa ei oltu vielä määritelty BASE_DIR:iä.

Korjasin siirtämällä lisäämäni tekstin muutaman rivin alaspäin:

![image](https://github.com/user-attachments/assets/7ed543b0-9898-481a-8310-771209a29498)

Tämän jälkeen pystyin antamaan komennon `./manage.py collectstatic`:

![image](https://github.com/user-attachments/assets/612316ba-2548-40a8-9282-0c4b43874f20)

Admin-sivu näyttää siltä kuin a-tehtävässä:

![image](https://github.com/user-attachments/assets/9242aa69-0c96-4789-bfd6-5510dee6cb8e)


---

**Lähteet**

- ChatGPT.
- Django: How to get Django. https://www.djangoproject.com/download/
- Geeksforgeeks 19.6.2024: Source Command in Linux with Examples. https://www.geeksforgeeks.org/source-command-in-linux-with-examples/
- Karvinen, Tero 2017: First Steps on a New Virtual Private Server – an Example on DigitalOcean and Ubuntu 16.04 LTS. https://terokarvinen.com/2017/first-steps-on-a-new-virtual-private-server-an-example-on-digitalocean/
- Karvinen, Tero 2022: Deploy Django 4 - Production Install. https://terokarvinen.com/2022/deploy-django/
- Karvinen, Tero 2022: Django 4 Instant Customer Database Tutorial. https://terokarvinen.com/2022/django-instant-crm-tutorial/
- Karvinen, Tero: Oppitunti 25.9.2024. Linux-palvelimet. https://terokarvinen.com/linux-palvelimet/
- man touch
- man virtualenv
- man which
- Shittu Olumide 3.5.2024: How to Copy a Directory in Linux – Use the cp Command to Copy a Folder. https://www.freecodecamp.org/news/how-to-copy-a-directory-in-linux-use-the-cp-command-to-copy-a-folder/
- Tech With Tim 16.2.2024: Python Virtual Environments - Full Tutorial for Beginners. https://www.youtube.com/watch?v=Y21OR1OPC9A
- teclado 13.4.2021: The Complete Guide to Python Virtual Environments! https://www.youtube.com/watch?v=KxvKCSwlUv8
- Vivek Gite 26.8.2024: How to move a folder in Linux using mv command. https://www.cyberciti.biz/faq/mv-command-howto-move-folder-in-linux-terminal/

---
  
*Tätä dokumenttia saa kopioida ja muokata GNU General Public License (versio 2 tai uudempi) mukaisesti. http://www.gnu.org/licenses/gpl.html*

*Pohjana Tero Karvinen 2012: Linux kurssi, http://terokarvinen.com*

*Raportin tekijä: Jenni Muhonen*
