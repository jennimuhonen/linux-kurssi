# h4 Maailma kuulee

Tehtäviä Tero Karvisen kurssille Linux Palvelimet 2024. https://terokarvinen.com/linux-palvelimet/

---

## x) Lue ja tiivistä

Susanna Lehto 2022: Teoriasta käytäntöön pilvipalvelimen avulla (h4). https://susannalehto.fi/2022/teoriasta-kaytantoon-pilvipalvelimen-avulla-h4/

- a: Kuinka hankitaan DigitalOceanilta palvelin ja Namecheapilta domainnimi hyödyntäen GitHub Educationin krediittejä. Lisäksi kuinka domainnimi saadaan osoittamaan virtuaalipalvelimelle.
- d: Kirjautuminen virtuaalipalvelimelle ensimmäistä kertaa, päivitykset ja palomuurin asentaminen.
- e: Uusi pääkäyttäjä virtuaalipalvelimelle, juuren lukitseminen, virtuaalipalvelimen päivittäminen, Apachen asentaminen, testisivu.
- f: Palvelimen päivitykset

Karvinen 2012: First Steps on a New Virtual Private Server – an Example on DigitalOcean and Ubuntu 16.04 LTS. https://terokarvinen.com/2017/first-steps-on-a-new-virtual-private-server-an-example-on-digitalocean/

- paikkoja vuokrata virtuaalipalvelin
- muista hyvä salasana alusta alkaen
- ensimmäinen kirjautuminen uudelle virtuaalipalvelimelle, palomuuri, sudo käyttäjä, sulje root, päivitä
- muista tehdä reikä palomuuriin
- ip-osoitteen lisäksi nimi on kiva eli vuokraa sellainen


## Rauta ja OS

**Virtuaalikoneella pyörivän Linuxin tiedot**

- Käyttöjärjestelmä: Debian 12.6.0 AMD64
- Virtualisointi: VirtualBox 7.0.20
- Muisti: 4096 MB
- Prosessorit: 4 CPU
- Virtuaalilevyn maksimikoko: 60 GB, josta käytetty 14,02 GB

**Taustajärjestelmän tiedot**

- Pöytäkone
- Käyttöjärjestelmä: Windows 11 Education, 64 bittinen käyttöjärjestelmä, x64-suoritin
- CPU: AMD Ryzen 5 7600 3.8 GHz 6-Core Processor
- Emolevy: MSI PRO B650-P WIFI
- Muisti: 32 GB DDR5-6000 CL30
- SSD: 2 TB, jossa vapaata tilaa 974 GB
- Näytönohjain: AMD RX 6800 XT 16 GB


## a) Oma virtuaalipalvelin

*Tehtävä: Vuokraa oma virtuaalipalvelin haluamaltasi palveluntarjoajalta. (Vaihtoehtona voit käyttää ilmaista kokeilujaksoa, GitHub Education krediittejä; tai jos mikään muu ei onnistu, voit kokeilla ilmaiseksi vagrant:ia paikallisesti. Suosittelen kuitenkin harjoittelemaan oikeilla, tuotantoon kelpaavilla julkisilla palveluilla).*

*To 12.9.2024 klo 14.35*

Hain maanantaina GitHub Educationin etuja. Hakemukseni hyväksyttiin, mutta etujen luvataan olevan käytettävissä "kohta". Eli en pysty hyödyntämään tätä etua tässä kohtaa.

Opettaja suositteli tunnilla vaihtoehtoina DigitalOceania, Linodea ja UpCloudia. DigitalOceanista näimme tunnilla käytännön esimerkin ja samoin x-kohdan tiivistystehtävässä oli käytetty DigitalOceania. Jotta saan vähän laajempaa kuvaa aiheesta, perehdyn ensisijaisesti jompaan kumpaan muista vaihtoehdoista.

Linode mainostaa uusien asiakkaiden saavan sadan dollarin edestä ilmaisia krediittejä ja samoin UpCloudilla on ilmainen testijakso. Kävi ilmi, että UpCloud on suomalainen firma (https://www.finder.fi/IT-palvelut/UpCloud+Oy/Helsinki/yhteystiedot/2617969), joten päätin kannattaa kotimaista (upcloud.com).

Hyvin nopeasti kävi ilmi, että UpCloudin ilmainen kokeilujakso tarkoittaa kolmea ilmaista päivää. Sattumalta päädyin kuitenkin Redditin kautta artikkeliin (https://techblog.nexxwave.eu/benchmark-between-cloud-servers-january-2024/), jossa arvosteltiin eri pilvipalvelimia ja heidän linkkinsä kautta voisi saada 25 ilmaista euroa UpCloudin käyttöön.

Klikkasin yllä mainitun sivuston linkin kautta ja rekisteröidyin UpCloudin sivulle. Minulle tarjottiin edelleen kolmen päivän ilmaista kokeilujaksoa ja tämän lisäksi minulla näytti olevan tililläni luvatut 25 euroa. Sivulla ei näkynyt tietoa siitä, onko näillä euroilla jotain erääntymispäivää.

![image](https://github.com/user-attachments/assets/40567c24-4261-4f0b-b9d8-a117d3f9b23a)

Olin saanut sähköpostiin ohjeet palvelun käytön aloittamiseksi:

![image](https://github.com/user-attachments/assets/74236e7b-17a9-4b0b-97c5-a501ff7c21f9)

Ensinnä siis pitää aloittaa ilmaisjakso. Tässä kohtaa pyydettiin luottokorttitietoja, jotka annoin.

![image](https://github.com/user-attachments/assets/feb646b5-1722-4b16-b878-59686d4c1b93)

Vahvistettuani korttitietoni ilmainen kokeilujakso alkoi:

![image](https://github.com/user-attachments/assets/e78b9fff-60b2-4231-9553-b8e98ee3c7d8)

Jotain rahaa tosin ilmeisesti täytyy antaa jossain vaiheessa, sillä sivusto ilmoittaa, että kokeilujaksolla on rajoitteita ja tietoni häviävät kolmen päivän päästä, jos en ole käyttänyt rahaa:

![image](https://github.com/user-attachments/assets/67a1105f-3500-435d-af02-7119677753da)

Sivusto kehotti ottamaan käyttöön kaksivaiheisen tunnistautumisen, joten lisäsin sivuston Google Authenticatoriini.

Ilmaisjakson rajoitteet ovat nämä, en osaa sanoa, onko näillä vaikutusta tehtävien tekoon:

![image](https://github.com/user-attachments/assets/ccc4b342-c9e9-4d6f-b4b0-4850c99e789e)

Lue ja tiivistä -kohdan materiaaleissa mainittiin portit 22 ja 80. En tiedä tuottaako se ongelmia, että kokeilujaksolla portin 22 liikenne on vain yksisuuntaista. Pidän tämän mielessä ja katson, kuinka käy.

*(Jälkikäteiskommentti: Tein lopulta kaikki tehtävät ennen kuin maksoin 10 euroa, jotta tekemäni palvelin ei katoaisi testijakson päätyttyä. Testijakson rajoitteet eivät haitanneet tehtävien tekemistä.)*

Seuraavaksi ohjesähköpostissa oli kohta Deploy your first cloud server, joka vei aiheeseen liittyvälle ohjesivulle: https://upcloud.com/resources/tutorials/deploy-server. Sivun perusteella klikkailin itseni Servers-sivustolle, josta löytyi kohta Deploy New Server.

![image](https://github.com/user-attachments/assets/75a3756e-67bb-4ed9-9297-4de36d1c05c4)

Tunnilla kerrottiin, että sijainti kannattaa ottaa niin läheltä asiakasta kuin mahdollista ja että EU-maat ovat hyviä valintoja EU:n sääntelyn takia. Koska UPCloud on suomalainen palvelu, sain valita jopa kahden kotimaisen vaihtoehdon väliltä:

![image](https://github.com/user-attachments/assets/af36e6e4-c691-4891-8397-3314a9f1caa8)

Oppitunnilla sanottiin, että kannattaa valita halvin vaihtoehto, jossa on gigatavu ram-muistia. Eli tämän perusteella kolmen euron vaihtoehto kuulosti hyvältä.

![image](https://github.com/user-attachments/assets/5b36c132-bb9c-4b72-b7fa-aa5873eff558)

Seuraaville kohdille en tehnyt mitää, sillä tunnilla kerrottiin, ettei ekstrasta kannata maksaa ja varmuuskopiot täytyy joka tapauksessa ottaa itse.

![image](https://github.com/user-attachments/assets/c2b83bd3-a3e0-46a6-b076-ace34db4fbcc)

Käyttöjärjestelmäksi valitsin uusimman Debian-version.

![image](https://github.com/user-attachments/assets/672d5a50-9e23-420c-8f89-59304eeb9f5d)

Seuraaville valinnoille en tehnyt mitään. Klikkasin Utility networkin linkkiä ja sivulla kerrottiin, että kaikki käyttäjän palvelimet on yhdistettu "utility networkiin", joka yhdistää kaikkia yrityksen palvelinkeskuksia. Tämä takaa nopean yhteyden palvelinten välillä.

![image](https://github.com/user-attachments/assets/47cdbf60-7a66-4c37-8738-b0cf383b4167)

Myöskään seuraaviin en tehnyt muutoksia ja sivusto kertoi, että Metadata Servicen pitää olla päällä valitsemassani kokonaisuudessa.

![image](https://github.com/user-attachments/assets/150161e2-470e-48c5-8cf2-1a8716077a0a)

Tunnilla kerrottiin, että SSH olisi parempi vaihtoehto, mutta koska emme vielä osaa tätä, voimme valita salasanan. Tässä kohtaa ongelmaksi tuli se, että sivusto ilmoitti, etten voi valita salasanaa kyseisen käyttöjärjestelmän version kanssa.

![image](https://github.com/user-attachments/assets/149dd5d9-e3bf-45a9-8a59-32b04c40e851)

Joudun siis omatoimisesti perehtymään SSH-salaukseen, jos en halua luovuttaa ja vaihtaa palvelua. Pidin tauon miettiäkseni asiaa.

*12.9.2024 16.40*

UpCloudin sivuilla on SSH-ohjeet (https://upcloud.com/resources/tutorials/use-ssh-keys-authentication), mutta aloitin aiheeseen perehtymisen mieluummin katsomalla ensin videon Youtubesta: https://www.youtube.com/watch?v=ZhMw53Ud2tY.

Videolta sain yleisen kuvan siitä, mistä on kyse. Tämän jälkeen palasin UpCloudin sivulle tutkimaan, mitä rekisteröitymisvaiheessa tarvitaan. En vielä ymmärrä, mitä tietoa sivulle pitäisi antaa:

![image](https://github.com/user-attachments/assets/027ff9b5-448f-407a-b3b5-e82f6e225379)

Aiemmin mainitulla SSH-ohjeiden sivulla kerrotaan kuinka SSH-salaus tehdään komentorivillä, mutta se ei vastaa siihen, mitä yllä olevaan pitäisi antaa. Siirryin etsimään vastausta sähköpostin ohjeviestiin linkatun sivun takaa (https://upcloud.com/resources/tutorials/deploy-server), mutta siellä aihetta käsiteltiin hyvin yleisesti. Päätin avata terminaalin ja kokeilla luoda SSH-avaimet Debianillani ja katsoa mitä tapahtuu. Tein rekisteröitymistä Windowsin puolella, mutta avaimet kokeilen lisätä Debianin puolella. Avaimet voi lisätä tilin tietoihin omalla välilehdellä eli voin palata rekisteröitymisen pariin Windowsin puolelle, jos saan salausasiat kuntoon.

**SSH**

Ryhdyin toimeen apunani UpCloudin ohjesivu https://upcloud.com/resources/tutorials/use-ssh-keys-authentication ja ChatGPT.

UpCloudin ohjeiden mukaan luon SSH-avainparin seuraavasti:

![image](https://github.com/user-attachments/assets/e94baf55-c7d7-4046-8bab-bcba1cc5c0d4)

Ennen kuin syötin komentoja tarkistin vielä ChatGPT:ltä, mitä kukin komento tekee ja mitä olen tehnyt laitettuani nämä kolme komentoa.

Kysyin seuraavat kysymykset ChatGPT:ltä:

- mitä komento mkdir -p ~/.ssh tekee?
- mitä tämä komento tekee: chmod 700 ~/.ssh
- mitä tämä komento tekee: ssh-keygen -t rsa
- Eli näiden komentojen jälkeen olen 1. luonu kansion 2. määrittänyt sen oikeudet vain itselleni ja 3. luonut kansioon ssh-avainparin? Tämä ei vielä ota SSH:ta käyttöön?
- viimeisimmässä vaiheessa saan vastauksen bash: ssh-keygen: command not found. Johtuuko tämä siitä, että minun tarvitsee asentaa ensin jotain vai käyttää sudoa?

Viimeisimmän kysymyksen kysyin saatuani virheviestin. ChatGPT kertoi minulle, että en tarvitse tässä sudoa (joka olisikin ollut yllättävää, koska ohjeissakaan sitä ei ollut) vaan että luultavasti minun täytyy asentaa ssh-keygen.

Aion ensin suoraan noudattaa ChatGPT:n neuvoja, mutta päädyin kuitenkin tarkistamaan, mitkä kurssilla neuvotut komennot asennuksiin olivat (https://terokarvinen.com/2020/command-line-basics-revisited/?fromSearch=command%20line%20basics%20revisited). ChatGPT halusi käyttää sudo apt -komentoa ja kurssille on ohjeistettu käyttämään sudo apt-get. Muistan, että opettaja on kertonut näiden eron, mutta en enää muista vastausta. ChatGPT:n mukaan ("mitä eroa on komennoilla sudo apt ja sudo apt-get?") ero on tiivistetysti se, että apt on uudempi ja helpompi komento, kun taas apt-get tarjoaa ominaisuuksia, joita apt:lla ei ole.

Vaihdoin siis apt-getiin ja jatkoin ChatGPT:n ohjeiden mukaan. Googlasin nopsaan ChatGPT:n ehdottaman asennuspaketin (https://packages.debian.org/unstable/openssh-client) ja koska se näytti hyvältä, jatkoin asentamaan sen. Tunnilla opettaja puhui asentamisen turvallisuudesta apt-getin avulla, joten en olisi ollut kovin huolestunut asentamisesta ilmankaan googlausta.

History-komennon avulla etsin, mitä olin tehnyt tähän mennessä tänään:

![image](https://github.com/user-attachments/assets/c91d36c7-93f8-4924-8ec0-eaee25e5f756)

Eli nyt minulla pitäisi olla ssh-avainpari kansiossa odottamassa.

Halusin vielä nähdä, onko näin todella. Pelkkä ls-komento ei tuottanut vastausta, joten keskustelin hetken aiheesta ChatGPT:n kanssa. Ymmärsin lopulta, että kyseinen kansio on piilotettu ja sen takia sitä ei näkynyt. Kun annoin kotihakemistossani komennon `ls -la` kyseinen ja varsin moni muukin tiedosto tuli näkyviin.

![image](https://github.com/user-attachments/assets/70e0db64-1e9c-4e52-afcd-e9d9b301f799)
![image](https://github.com/user-attachments/assets/26f7674c-09f3-4dac-866e-6fff1d87f6a1)

Sitten takaisin UpCloudin sivulle, mutta tällä kertaa Debianin kautta. Jotta tämä onnistui, jouduin vaihtamaan salasanan palveluun, sillä olin laiskana antanut Googlen luoda ja tallentaa salasanan, josta minulla ei ollut enää mitään aavistusta.

Seuraava haaste: kuinka kopioin salausavaimen verkkosivulle.

Tämä kohta osoittautui kinkkiseksi. ChatGPT ehdotti, että tulostan tiedoston cat-komennon avulla ja saan sen jälkeen kopioitua sen. 

![image](https://github.com/user-attachments/assets/c7e68f88-e8d9-4b1e-8bf1-e9c5c9239d07)

Tarkastin yllä tiedoston sisällön, mutta en näe siellä tiedostoa, jonka nimi olisi id_rsa.pub.

Kokeilin varalta luoda avaimen uudelleen, mutta tässä kohtaa käy ilmi, että avain kyllä on olemassa:

![image](https://github.com/user-attachments/assets/c1cefdee-d280-4ffc-9069-2fec0bc4acbf)

Lähdin etsimään neuvoja jostain muualta.

Raivokkaasta googlettamisesta huolimatta kaikkialla vain tarjottiin samat komennot eikä mitään ratkaisuja eli mistään en löytänyt vastausta ongelmaani. Päätin kokeilla vielä kerran avaimen luomista ja lopulta ymmärsin, missä olin mennyt vikaan. En ollut lukenut kunnolla, mitä avainta luodessa oikeastaan sanotaan. Olin painanut y ja ajatellut, että haluttiin vain hyväksyntää, mutta itseasiassa tässä kohtaa kysyttiin, haluanko antaa tiedostolle uuden nimen vai käyttää default nimeä. Olin siis nimennyt tiedoston nimellä y. Olin siis tehnyt saman virheen kahteen kertaan ja vasta kolmannella yrityksellä luin tarpeeksi hitaasti ja ymmärsin, mitä olin tehnyt. Päädyin tekemään uuden avaimen oletusnimellä.

![image](https://github.com/user-attachments/assets/a9ef3677-63e1-464e-b08c-a19dbbffcc33)

Jostain syystä ensimmäisen tiedoston nimi näyttäytyy y:n sijaan pisteenä ja luulin, että pisteet piilottavat jotain tietoa. Jotain vikaa y:ksi nimetyssä tiedostossa varmaankin on, koska sen tiedot näyttävät oudoilta. Defaul-nimellä nimetyt tiedostot näyttävät sen sijaan oikealta. (Vertailuna käytin: https://docs.oracle.com/en/operating-systems/oracle-linux/openssh/openssh-WorkingwithSSHKeyPairs.html#remote-access-without-password)

Kokeilin cat-komentoa ja nyt se toimii. Kopioin avaimen ja liitin sen UpCloud-tililleni. Kopioin kaiken cat-komennon antaman tiedon, toivottavasti tämä on oikein. Ainakin Up-Cloudilla kaikki näyttää hyvältä. (En ota kuvakaappauksia, koska en tiedä mitä tietoa avaimeen liittyen voin tietoturvallisesti näyttää.)

**Takaisin alkuperäisen tehtävän pariin**

*12.9.2024 19.16*

Tähänhän nyt meni hieman ennalta odotettua pitempään... Olisin päässyt niin paljon helpommalla, jos en olisi päättänyt tutustua uuteen palveluun. Seuraavaksi jatkoin virtuaalipalvelimen luomista.

![image](https://github.com/user-attachments/assets/69369935-464e-4015-8074-4989d4a7dbde)

En tiedä olisiko avaimen default-nimeä voinut ongelmitta vaihtaa sitä UpCloudiin tallentaessa, mutta en halunnut kokeilla.

Tämä valinta kuulostaa edistyneemmille käyttäjille suunnatulta, joten hyppäsin sen yli:

![image](https://github.com/user-attachments/assets/c563bf3f-41b7-48ec-aba5-8f0a11202017)

Ja viimeiseksi piti valita Hostname ja Servername. Tässä on yksi nimi enemmän kuin esimerkeissä näkemälläni DigitalOceanilla. Tarkistin ohjesivulta (https://upcloud.com/resources/tutorials/deploy-server), mitä eri nimillä tarkoitetaan. Sivun mukaan Hostname-kohtaan laittaisin domainini, jos minulla sellainen olisi ja Server name -kohtaan taas nimi, jolla tunnistan nopeasti serverini. Tämä nimi näkyy servereiden listauksessa ilmeisestikin UpCloudin sivuilla. Opettajan ohje nimeämiseen oli laittaa jotain harmitonta, jonka näkyminen ulospäin ei haittaa. Laitoin kahteen kohtaan hieman erilaiset nimet, niin näen mitä näkyy missäkin.

![image](https://github.com/user-attachments/assets/b50f234c-3dd5-4fb9-bd42-d351d58818f8)

Sitten klikkasin Deploy.

![image](https://github.com/user-attachments/assets/2e3d1980-f2e1-4a41-885a-39d9459bd2a3)
![image](https://github.com/user-attachments/assets/837f00b5-9b03-41f5-ab31-5bbe404827ec)

Näytti lupaavalta.

## b) Alkutoimet

*Tehtävä: Tee alkutoimet omalla virtuaalipalvelimellasi: tulimuuri päälle, root-tunnus kiinni, ohjelmien päivitys.*

*12.9.2024 klo 19.48*

Seuraavaksi aloin seuraamaan opettajan ohjeita (https://terokarvinen.com/2017/first-steps-on-a-new-virtual-private-server-an-example-on-digitalocean/) virtuaalipalvelimen alkutoimien kanssa.

Ensiksi kopioin virtuaalipalvelimeni ip-osoitteen ja sen jälkeen otin siihen yhteyttä root-käyttäjänä.

![image](https://github.com/user-attachments/assets/82499348-aa48-4d18-aa4d-af99d86e9df4)

Jostain syystä, kun annoin tuon komennon, yhteys lopuksi suljettiin ja en päässyt kirjautumaan sisään. Kävin ChatGPT:n kanssa keskustelun siitä, mihin vaikuttaa se, että kokeilujaksolla portin 22 lähtevä liikenne on suljettu. ChatGPT kuitenkin vakuutti minut siitä, että tämä ei ole ongelmaan syyllinen. Kokeilin siis varalta komentoa uudestaan ja tällä kertaa pääsinkin sisään:

![image](https://github.com/user-attachments/assets/18ac676b-21e6-407c-871b-5e8ee070d01b)

Tässä kohtaa kävin ChatGPT:n kanssa keskustelun myös SSH-salauksesta ja hahmotin, miksi riittää, että olen antanut virtuaalipalvelimelle vain avaimen julkisen puoliskon. ChatGPT selitti, että kun otan yhteyttä palvelimelle, palvelin heittää haasteena julkisen avaimen ja koska koneeni osaa yksityisen avaimen avulla ratkaista haasteen, pääsen sisälle.

SSH-avaimien käyttämisen takia minun ei tarvinnut antaa salasanaa, kuten ohjeessa neuvottiin.

Seuraavaksi minun tuli tehdä reikä palomuuriin komennolla `sudo ufw allow 22/tcp`. ChatGPT selitti (kysymys: mitä tämä komento tekee: sudo ufw allow 22/tcp), että ufw on palomuurin hallintatyökalu ja allow sallii yhteydet määritettyyn porttiin.

![image](https://github.com/user-attachments/assets/404f466f-748a-4a11-83c3-d731a88c50ed)

Komentoa antaessani oli käynyt niin, että yhteys virtuaalipalvelimelle oli katkennut ja annoin komennon vahingossa väärällä puolella. Lyhyt keskustelu ChatGPT:n kanssa antoi minulle keinot korjata asian ja vahvistuksen arviolle, että tietosuojasyistä aukkoa ei ole syytä huvikseen sinne jättää.

Otin yhteyttä uudestaan virtuaalipalvelimelle, mutta siellä komento ei onnistunut. Kävin tarkistamassa palomuurin asennusohjeet (https://terokarvinen.com/2021/install-debian-on-virtualbox/) ja tosiaan, ufw piti ensin asentaa.

Tällä välin yhteys virtuaalipalvelimeen oli taas katkennut:

![image](https://github.com/user-attachments/assets/3a19e7e9-24dd-40d2-bade-fe51545cfc16)

Tätäkin pitäisi varmaan selvittää. Googlaus tuottikin yllättävän helposti vastauksen. Ravi Saiven (https://www.tecmint.com/client_loop-send-disconnect-broken-pipe/) mukaan yhteys katkeaa, kun se on liian pitkään käyttämättä. Liian pitkään on tässä hyvin suhteellinen käsite, sillä hetki tiedonhakua muualla katkaisi yhteyden.

Ravi Saive kehotetti antamaan komento sudo vi /etc/ssh/sshd_config ja etsimään tiedostosta alla olevassa kuvassa näkyvät tiedot.

![image](https://github.com/user-attachments/assets/b47d1f3a-cc20-4769-9435-468ae96d0f65)

Saiven mukaan ClientAliveInterval (https://www.cs.colostate.edu/helpdocs/vi.html) tarkoittaa sitä, kuinka pitkän inaktiivisuuden jälkeen SSH serveri lähettää alive-viestin clientille ja ClientAliveCountMax tarkoittaa, kuinka monta kertaa tämä tapahtuu. Eli toisin sanoen heti epäaktiivisuuden jälkeen serveri alkoi tarkistella tilannetta, totesi kuolleeksi ja sulki yhteyden. Eipä ihme, että oli haasteita.

Saive kehottaa päivittämään ylemmäksi luvun arvoksi 300, jolloin alive-viesti lähtee 300 sekunnin eli viiden minuutin päästä. Koska tämä toistetaan kolmesti, on armonaikaa tämän jälkeen 15 minuuttia. Tämä kuulosti huomattavasti paremmalta, mutta vi-editorin käyttö vaati erikseen käyttöohjeiden etsimisen. Kokeilin myös välissä, voiko tiedoston avata microlla, mutta ei voinut. Tiedoston sisältö näytti sellaiselta, että varmaan ihan hyvä, ettei sitä aivan helposti saanut käpälöityä.

![image](https://github.com/user-attachments/assets/f8cdf267-2fcc-4772-8798-cdbd40a5c49a)

Lopulta ohjeiden (https://www.cs.colostate.edu/helpdocs/vi.html) avulla sain päivitettyä ClientAliveInterval:n 300 sekuntiin:

![image](https://github.com/user-attachments/assets/c1d768a6-b3d0-4de1-93e3-a6b2d518c043)

Tosin tätä kirjoittaessa serveri heitti minut taas pihalle ja oletan, etten tuhlannut varttia.

Luin ohjetta vielä uudelleen ja ohjeessa käskettiin käynnistämään SSH daemon uudestaan. Oletan, että tätä ei nyt enää erikseen tarvitse tehdä, kun minut ehdittiin jo heittää pihalle. Palaan ohjeiden pariin, jos ongelma jatkuu.

Eli olin asentamassa usw:tä. Ensiksi ajoin päivityksiä ja sen jälkeen asensin ufw:n ja samalla tajusin, että micro piti myös erikseen asentaa, jos sitä haluaa käyttää.

![image](https://github.com/user-attachments/assets/e359c52b-f008-4e7a-b71e-ccadb909a21a)

Tämän jälkeen tein palomuuriin reiän ja aktivoin sen. Hetkeksi pysähdyin ja tarkistin, että palomuurin reikä näyttäisi olevan ok, ennen kuin hyväksyin palomuurin käynnistämisen.

![image](https://github.com/user-attachments/assets/114f1725-4e14-47c3-ac41-eabdca44ace7)

Palomuuri on käytössä vasta systeemin uudelleenkäynnistämisen jälkeen. Muistelin, että aiemmin katsomallani Youtube-videolla asioita tarkisteltiin toisen terminaaliyhteyden kautta ennen kuin aiempaa yhteyttä suljettiin, jotta voitiin olla varmoja siitä, että mitään ei ollut mennyt pieleen ja yhteyden ottaminen edelleen onnistui. Kokeilin tätä ja pääsin edelleen sisälle. Niinpä siirryin ohjeen seuraavaan kohtaan.

Testailun keskellä alkuperäinen yhteys oli taas katkennut. Kävin tarkistamassa mikä komento ohjeessa vielä annettiin lopuksi ja kokeilin antaa sen, josko erillinen uudelleenkäynnistäminen sittenkin tarvittiin.

![image](https://github.com/user-attachments/assets/24e63722-0a2d-4229-b0bd-d2dd2f560b27)

Lisäsin käyttäjän ja annoin käyttäjälle sudo-oikeudet:

![image](https://github.com/user-attachments/assets/8e962a6a-032c-46f2-a1c5-4024b82d59fb)

Annoin käyttäjän tietoihin koko nimen, kuten Susanna Lehto (https://susannalehto.fi/2022/teoriasta-kaytantoon-pilvipalvelimen-avulla-h4/) oli tehnyt omassa tehtävässään ja jätin muut kohdat tyhjiksi. Annoin käyttäjälle salasanan.

Tämän jälkeen ohje kehotti testaamaan uutta käyttäjää ja hyvä niin:

![image](https://github.com/user-attachments/assets/d1f98c3d-f90d-409a-9bd0-197c9a9db4e0)

Ongelma oletettavasti liittyy siihen, että jouduin ottamaan SSH-avaimet käyttöön ja en ollut antanut uudelle käyttäjälle julkista avainta.

Paitsi että tässähän on myös kirjoitusvirhe.

![image](https://github.com/user-attachments/assets/ffdfff04-6aaa-4b62-8de2-23a593fffb7a)

Virhe toistuu myös oikealla käyttäjänimellä.

UpCloudin ohjeiden (https://upcloud.com/resources/tutorials/use-ssh-keys-authentication) mukaan tällä komennolla voidaan antaa julkinen avain käyttäjälle: ssh-copy-id -i ~/.ssh/id_rsa.pub user@server

![image](https://github.com/user-attachments/assets/d1a3d58d-e3fc-43c1-a8ed-c60c1f124826)

Jostain syystä ei onnistunut. Tässä kohtaa etsin varalta vahingossa tekemäni ylimääräiset avaimet, jos ne vaikuttavat asiaan. Avaimet löytyivät kotihakemistostani, josta poistin ne.

![image](https://github.com/user-attachments/assets/48e8f0e9-b3b4-46ce-9c60-b172898948a1)

Pääsy palvelimelle oli kuitenkin edelleen estetty käyttäjältä jemjem, mutta root pääsi edelleen kirjautumaan ongelmitta.

Kello oli tässä kohtaa sen verran paljon, että jätin ongelman selvittelyn toiseen päivään.

*13.9.2024 10.26*

Pohdittuani asiaa ja tarkistettuani asian ChatGPT:ltä tajusin, että käyttäjänhän pitäisi päästä kirjautumaan salasanalla niin pitkään, kun sellaisen käyttöä ei ole kielletty. Lisäksi kuvakaappauksessa, jossa yritän lähettää SSH-koodin käyttäjälle jemjem tulee virhe jo koodin lähettämisvaiheessa eli se ei onnistu ja tulee sama virheilmoitus kuin kirjautumista yrittäessä.

Lähdin etsimään tietoa virheilmoituksesta. Pranita (https://www.redswitches.com/blog/ssh-permission-denied/) on pureutunut ongelmaan blogipostauksessaan ja näyttää siltä, että alkuperäinen ajatukseni oli kuitenkin oikea ja ongelma johtuu ssh-salauksesta. Onko salasanan käyttö valmiiksi estetty kaikilta käyttäjiltä?

Tutkin asian heti, sillä olisi ollut kovin helppoa, jos olisin voinut kiertää ssh-ongelmat. NetworkChuck näyttää videollaan (https://www.youtube.com/watch?v=ZhMw53Ud2tY), kuinka salasanakirjautuminen estetään, joten tarkistin hänen neuvojensa avulla, onko tämä jo kielletty, mutta ei valitettavasti ollut:

![image](https://github.com/user-attachments/assets/d21bb93b-a9d8-4089-934e-54dd4ff75965)

![image](https://github.com/user-attachments/assets/19afa4a3-dffc-47c9-a788-d2e28b673d72)

Pranitan mukaan virheviesti tarkoittaa juuri sitä, mitä alunperin itsekin ajattelin eli pääsy on kielletty julkiseen avaimeen liittyvän ongelman takia. 

Pranitan ohjeet tuntuivat lähtevän siitä, että tarkistellaan ssh-tiedostoja. Niinpä kysyin ChatGPT:ltä, kuinka vaihdan käyttäjää rootista jemjem:ksi ollessani kirjautuneena, jotta pääsen helpommin tarkastelemaan käyttäjän tietoja. Komento oli `su`.

![image](https://github.com/user-attachments/assets/980f1a9f-4bca-4f0f-b7b8-f174073c30a0)

Kuten aiemman virheviestin perusteella saattoi päätellä, .ssh-kansion luominen ei ole onnistunut. Loin sen siis ja asetin käyttöoikeudet. Seuraavaksi palaan aiempien ohjeiden pariin sen suhteen, kuinka kopioin käsin julkisen avaimen käyttäjätunnukselleni. Josko tämä auttaisi ongelmaan.

Tarkistin, löytyisikö Oraclen sivulta (https://docs.oracle.com/en/operating-systems/oracle-linux/openssh/openssh-WorkingwithSSHKeyPairs.html#copy-public-key), tarkat ohjeet kopiointiin. Silmiin ei suoraan osunut sopivaa ohjetta siihen, mitä kopioinnin jälkeen teen, joten päädyin kopioimaan koodin ja tekemään microlla uuden vastaavan nimisen tiedoston jemjem:lle ja liittämään kopioimani tiedot tiedostoon.

![image](https://github.com/user-attachments/assets/7b077c1e-1a18-4704-9f1d-6d24fc871603)

![image](https://github.com/user-attachments/assets/363d89c4-7366-4de7-959c-4a9e8f87c15d)

![image](https://github.com/user-attachments/assets/6b88cbc3-1c59-4ec2-ad62-852a1e98a204)

Valitettavasti ongelma ei ratkennut tällä:

![image](https://github.com/user-attachments/assets/cbeb0cdd-7502-4719-8376-5f7a81a16ced)

Eli joko tein jonkin virheen kopioinnissa tai ongelma on jossain muualla.

*13.9.2024 n. 14.30*

(Eli pitemmän tauon jälkeen.)

Ongelma ei ratkea säätämällä ympäriinsä, joten ryhdyin järjestelmällisesti käymään läpi Pranitan (https://www.redswitches.com/blog/ssh-permission-denied/) vianselvityslistaa.

Ensimmäisenä kehotetaan tarkistamaan, että yksityisten avainten oikeudet ovat oikein. Aiemman ottamani kuvakaappauksen tiedot täsmäävät Pranitan esimerkkikuvaan.

Toisena kehotetaan tarkistamaan, että "auhorized keys" ovat oikein ~/.ssh/authorized_keys-tiedostossa. Tarkastin ChatGPT:ltä, kuinka katson kyseistä tiedostoa ja sen jälkeen tutkin tilannetta jemjem:llä ja root:lla.

![image](https://github.com/user-attachments/assets/ff696fcd-42c0-47b1-8009-bc7523ab117b)

jemjem:llä tätä tiedostoa ei ole, kun taas root:lla se oli. Eli olin ilmeisesti kopioinut tiedot väärään paikkaan, kun en ollut perehtynyt ohjeisiin aiemmin tarpeeksi tarkkaan. Kokeilin ohjeiden mukaisesti lähettää taas tiedoston koneelta virtuaalipalvelimelle, mutta tämä ei edelleenkään toimi. Sen sijaan, kun loin samaan tapaan kuin aiemmin tiedoston oikealla nimellä, sain homman lopulta toimimaan!

Eli kopioin avaintiedoston sisällön ja loin jemjem:lle uuden tiedoston ja sen jälkeen cat-komento näytti tiedoston sisällön (jota en tässä näytä).

![image](https://github.com/user-attachments/assets/0425d30a-8c6e-4d75-bbdb-698e41a515d2)

![image](https://github.com/user-attachments/assets/24ee2585-d844-4963-abbb-10fd8c72b78a)

Mitä tästä opin. 1. lue ohjeita huolellisesti ja säädä vähemmän. 2. ssh-avaimet ovat kotikoneella ja virtuaalipalvelimella eri nimisissä tiedostoissa (ylläri). 3. tehdyt virheet tuntuvat usein liittyvän enemmän huolimattomuuteen kuin siihen, että olisi ollut tekemässä jotain totaalisen väärää asiaa.

**Takaisin varsinaisen tehtävän pariin**

Ohjeissa käyttäjä lisätään ryhmiin sudo, adm ja admin. Olin lisännyt jemjem:n jo ryhmään sudo, mutta opettaja taisi tunnilla mainita, että kaikkia ryhmiä ei välttämättä ole käytössä. Kysyin ChatGPT:ltä miten asia tarkistetaan ja sen jälkeen tutkin asiaa:

![image](https://github.com/user-attachments/assets/309fe942-2da5-4e3a-b16a-2b59e995b00a)

Adminia ei ilmeisestikään ole, mutta adm antoi jotain tulosta. Niinpä päätin lisätä käyttäjäni myös adm-ryhmään.

Jatkoin opettajan ohjeiden seurantaa ja seuraavaksi tulee sulkea root-tunnus. Noudatin ohjeita, mutta ohjeissahan itseasiassa sanotaa, että tässä lukitaan salasana. Ja root-käyttäjällähän ei ole salasanaa vaan ssh:n julkisen avaimen tiedosto.

![image](https://github.com/user-attachments/assets/5a575587-3f6f-46cc-8e5a-cc2042df6c25)

![image](https://github.com/user-attachments/assets/f7b5e6c3-c645-4fb3-83c7-4c7a0873dca1)

Kuten epäilinkin, root-käyttäjä pääsee edelleen kirjautumaan koneelle. Eli poistetaanpa samainen tiedosto, jota jemjem:lle äsken työllä ja tuskalla luotiin.

![image](https://github.com/user-attachments/assets/426774a7-a83d-4d7b-92a7-d75893c786d0)

![image](https://github.com/user-attachments/assets/7d3b3500-712d-4ed6-a675-b79b21a620d1)

Avasin toisen terminaaliyhteyden ja tarkistin kaiken varalta, että jemjem pääsee edelleen sisään (pääsee) ja sen jälkeen kokeilin, pääseekö root:

![image](https://github.com/user-attachments/assets/71452086-7c19-4907-933b-470d9b3793ce)

Näköjään äskeinen ei ollutkaan vielä kaikki mitä piti tehdä eli ehkä tiedoston poistaminen oli turhaa? Eli seuraavaksi kävin komennolla sudoedit `/etc/ssh/sshd_config` muokkaamassa root:n kirjautumisoikeuksia:

![image](https://github.com/user-attachments/assets/19b8e0e2-e2b7-480f-b25f-82ffa79ea39e)

Ja lopuksi ohje kehotti vielä:

![image](https://github.com/user-attachments/assets/3e3b46bb-d70d-4909-8a17-dae51dad3ada)

Päivitykset tein jo palomuurin asentamisen yhteydessä. Palomuuripäivitysten ohjesivulla oli dist-upgrade ja nyt käytetyssä ohjessa pelkkä upgrade. Googlasin asiaa ja päädyin Debianin wikiin (https://wiki.debian.org/AptCLI). upgrade päivittää kaikki paketit ilman, että poistaa mitään, kun taas dist-upgrade myös poistaa asioita. Debianin ohjeessa kehotetaan kirjaamana, mitä on poistetu, jotta näitä voi tarvittaessa asentaa uudestaan.

*13.9.2024 16.16.*

Päädyin takaisin NetworkChuckin videolle (https://www.youtube.com/watch?v=ZhMw53Ud2tY) ja muistin, että hän esti salasanakirjautumisen kokonaan. Noudatin hänen ohjeitaan:

![image](https://github.com/user-attachments/assets/f53f5f5e-0b5d-4cd0-bec4-39add25d2ff1)

![image](https://github.com/user-attachments/assets/49999be7-638f-4933-9a58-65f3b39a85f9)

![image](https://github.com/user-attachments/assets/0735ddc4-969c-445d-9000-24a456f9f418)



## c) Apache

*Tehtävä: c) Asenna weppipalvelin omalle virtuaalipalvelimellesi. Korvaa testisivu. Kokeile, että se näkyy julkisesti. Kokeile myös eri koneelta, esim kännykältä.*

*13.9.2024 n. 15.45*

Opettajan ohjesivu (https://terokarvinen.com/2017/first-steps-on-a-new-virtual-private-server-an-example-on-digitalocean/) muistuttaa tekemään reiän palomuuriin, jotta Apache toimii. Aloitin siis siitä:

![image](https://github.com/user-attachments/assets/b263d1e3-8faa-4f11-9d38-ce1a8bac141a)

Sen jälkeen palasin viime viikolta tutulle opettajan Apache-ohjesivulle (Karvinen, Tero, 2018: Name Based Virtual Hosts on Apache – Multiple Websites to Single IP Address. https://terokarvinen.com/2018/04/10/name-based-virtual-hosts-on-apache-multiple-websites-to-single-ip-address/) asentaakseni Apachen ja tehdäkseni uuden testisivun.

Hain ensin päivitykset, koska en ollut niitä tänään vielä hakenut ja sen jälkeen asensin apachen. Sitten tarkistin, että localhost näyttää oletussivun ja sen jälkeen muutin oletussivun tekstiksi "Testi". Sen jälkeen tarkistin, että näin tosiaan kävi.

![image](https://github.com/user-attachments/assets/f7e38625-610b-4bd7-8386-b3adde68b09c)

Tämä ei kuitenkaan vielä julkaissut sivua verkkoon, vaan Apache täytyi vielä käynnistää ja localhostin sijaan tarkastin, että sivu löytyy ip-osoitteen takaa:

![image](https://github.com/user-attachments/assets/e3e13c66-d19e-444d-b626-aaabbade1a14)

Tämän jälkeen vielä testasin, että pääsen sivulleni kännykällä:

![Screenshot_20240913_162813_Chrome2](https://github.com/user-attachments/assets/97c9136c-7f6e-4338-bd8c-5c4f769d1d9c)

Onnistui!

Lopuksi kävin laittamassa UpCloudin tilille 10 euroa, ettei koko virtuaalipalvelinta poisteta kokeilukauden päätteeksi eli huomenna.

---

**Lähteet**

- ChatGPT
- Colorado State University. Computer Science Department : Basic vi Commands. https://www.cs.colostate.edu/helpdocs/vi.html
- Debian: AptCli. https://wiki.debian.org/AptCLI.
- Finder: UpCloud Oy. https://www.finder.fi/IT-palvelut/UpCloud+Oy/Helsinki/yhteystiedot/2617969
- Karvinen, Tero 2012: First Steps on a New Virtual Private Server – an Example on DigitalOcean and Ubuntu 16.04 LTS. https://terokarvinen.com/2017/first-steps-on-a-new-virtual-private-server-an-example-on-digitalocean/
- Karvinen, Tero 2018: Name Based Virtual Hosts on Apache – Multiple Websites to Single IP Address. https://terokarvinen.com/2018/04/10/name-based-virtual-hosts-on-apache-multiple-websites-to-single-ip-address/
- Karvinen, Tero 2020: Command Line Basics Revisited. https://terokarvinen.com/2020/command-line-basics-revisited/?fromSearch=command%20line%20basics%20revisited
- Karvinen, Tero 2024: Oppitunti 11.9.2024. Linux-palvelimet. https://terokarvinen.com/linux-palvelimet/
- Karvinen, Tero: Install Debian on Virtualbox - Updated 2023. https://terokarvinen.com/2021/install-debian-on-virtualbox/
- Lovet, Kris. Benchmark between cloud servers (January 2024). (https://techblog.nexxwave.eu/benchmark-between-cloud-servers-january-2024/)
- NetworkChuck 18.3.2021: 5 Steps to Secure Linux (protect from hackers). https://www.youtube.com/watch?v=ZhMw53Ud2tY
- Oracle. 4 Working with SSH Key Pairs. https://docs.oracle.com/en/operating-systems/oracle-linux/openssh/openssh-WorkingwithSSHKeyPairs.html#remote-access-without-password
- Pranita 2.11.2023: How to Fix SSH Permission Denied (Publickey) Error. https://www.redswitches.com/blog/ssh-permission-denied/
- Saive, Ravi 31.5.2023: How to Fix SSH Client_loop: send disconnect: Broken pipe Error. https://www.tecmint.com/client_loop-send-disconnect-broken-pipe/
- Susanna Lehto 2022: Teoriasta käytäntöön pilvipalvelimen avulla (h4). https://susannalehto.fi/2022/teoriasta-kaytantoon-pilvipalvelimen-avulla-h4/
- UpCloud 24.5.2023: How to use SSH keys for authentication https://upcloud.com/resources/tutorials/use-ssh-keys-authentication
- UpCloud 23.4.2024: How to deploy a new Cloud Server. https://upcloud.com/resources/tutorials/deploy-server
- UpCloud: Documentation. https://upcloud.com/docs/products/networking/features/utility-network/

---
  
*Tätä dokumenttia saa kopioida ja muokata GNU General Public License (versio 2 tai uudempi) mukaisesti. http://www.gnu.org/licenses/gpl.html*

*Pohjana Tero Karvinen 2012: Linux kurssi, http://terokarvinen.com*

*Raportin tekijä: Jenni Muhonen*
