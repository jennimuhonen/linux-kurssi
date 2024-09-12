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

## a) Oma virtuaalipalvelin

*Tehtävä: Vuokraa oma virtuaalipalvelin haluamaltasi palveluntarjoajalta. (Vaihtoehtona voit käyttää ilmaista kokeilujaksoa, GitHub Education krediittejä; tai jos mikään muu ei onnistu, voit kokeilla ilmaiseksi vagrant:ia paikallisesti. Suosittelen kuitenkin harjoittelemaan oikeilla, tuotantoon kelpaavilla julkisilla palveluilla).*

*To 12.9.2024 klo 14.35*

Hain maanantaina GitHub Educationin etuja. Hakemukseni hyväksyttiin, mutta etujen luvataan olevan käytettävissä "kohta". Eli en pysty hyödyntämään tätä etua tässä kohtaa.

Opettaja suositteli tunnilla vaihtoehtoina DigitalOceania, Linodea ja UpCloudia. DigitalOceanista näimme tunnilla käytännön esimerkin ja samoin x-kohdan tiivistystehtävässä oli käytetty DigitalOceania. Jotta saan vähän laajempaa kuvaa aiheesta, perehdyn ensisijaisesti jompaan kumpaan muista vaihtoehdoista.

Linode mainostaa uusien asiakkaiden saadan sadan dollarin edestä ilmaisia krediittejä ja samoin UpCloudilla on ilmainen testijakso. Kävi ilmi, että UpCloud on suomalainen firma (https://www.finder.fi/IT-palvelut/UpCloud+Oy/Helsinki/yhteystiedot/2617969), joten päätin kannattaa kotimaista.

Hyvin nopeasti kävi ilmi, että UpCloudin ilmainen kokeilujakso tarkoittaa kolmea ilmaista päivää. Sattumalta päädyin kuitenkin Redditin kautta artikkeliin (https://techblog.nexxwave.eu/benchmark-between-cloud-servers-january-2024/), jossa arvosteltiin ei palveluita ja heidän linkkinsä kautta voisi saada 25 ilmaista euroa palvelun käyttöön.

Klikkasin yllä mainitun sivuston linkin kautta ja rekisteröidyin UpCloudin sivulle. Minulle tarjotaan edelleen kolmen päivän ilmaista kokeilujaksoa ja tämän lisäksi minulla näyttää olevan tililläni luvatut 25 euroa. Sivulla ei ainakaan vielä näy, onko näillä euroilla jotain erääntymispäivää.

![image](https://github.com/user-attachments/assets/40567c24-4261-4f0b-b9d8-a117d3f9b23a)

Olin saanut sähköpostiin ohjeet palvelun käytön aloittamiseksi:

![image](https://github.com/user-attachments/assets/74236e7b-17a9-4b0b-97c5-a501ff7c21f9)

Ensinnä siis pitää aloittaa ilmaisjakso. Tässä kohtaa pyydettiin luottokorttitietoja, jotka annoin.

![image](https://github.com/user-attachments/assets/feb646b5-1722-4b16-b878-59686d4c1b93)

Vahvistettuani korttitietoni ilmainen kokeilujakso alkoi:

![image](https://github.com/user-attachments/assets/e78b9fff-60b2-4231-9553-b8e98ee3c7d8)

Jotain rahaa tosin ilmeisesti täytyy antaa, sillä sivusto ilmoittaa, että kokeilujaksolla on rajoitteita ja tietoni häviävät kolmen päivän päästä, jos en ole käyttänyt rahaa:

![image](https://github.com/user-attachments/assets/67a1105f-3500-435d-af02-7119677753da)

Sivusto kehotti ottamaan käyttöön kaksivaiheisen tunnistautumisen, joten lisäsin sivuston Google Authenticatoriini.

Ilmaisjakson rajoitteet ovat nämä, en

![image](https://github.com/user-attachments/assets/ccc4b342-c9e9-4d6f-b4b0-4850c99e789e)

Lue ja tiivistä -kohdan materiaaleissa mainittiin portit 22 ja 80. En tiedä tuottaako se ongelmia, että kokeilujaksolla portin 22 liikenne on vain yksisuuntaista. Pidän tämän mielessä ja katson, kuinka käy.

Seuraavaksi ohjesähköpostissa oli kohta Deploy your first cloud server, joka vei aiheeseen liittyvälle ohjesivulle: https://upcloud.com/resources/tutorials/deploy-server. Sivun perusteella klikkailin itseni Servers-sivustolle, josta löytyi kohta Deploy New Server.

![image](https://github.com/user-attachments/assets/75a3756e-67bb-4ed9-9297-4de36d1c05c4)

Tunnilla kerrottiin, että sijainti kannattaa ottaa niin läheltä asiakasta kuin mahdollista ja että EU-maat ovat hyviä valintoja EU:n sääntelyn takia. Koska UPCloud on suomalainen palvelu, saan valita jopa kahden kotimaisen vaihtoehdon väliltä:

![image](https://github.com/user-attachments/assets/af36e6e4-c691-4891-8397-3314a9f1caa8)

Oppitunnilla sanottiin, että kannattaa valita halvin vaihtoehto, jossa on gigatavu ram-muistia. Eli tämän perusteella kolmen euron vaihtoehto kuulostaa hyvältä.

![image](https://github.com/user-attachments/assets/5b36c132-bb9c-4b72-b7fa-aa5873eff558)

Seuraaville kohdille en tehnyt mitää, sillä tunnilla kerrottiin, ettei ekstrasta kannata maksaa, sillä varmuuskopiot täytyy joka tapauksessa ottaa itse.

![image](https://github.com/user-attachments/assets/c2b83bd3-a3e0-46a6-b076-ace34db4fbcc)

Käyttöjärjestelmäksi valitsin Debianin.

![image](https://github.com/user-attachments/assets/672d5a50-9e23-420c-8f89-59304eeb9f5d)

Seuraaville valinnoille en tehnyt mitään. Klikkasin Utility networkin linkkiä ja sivulla kerrottiin, että kaikki käyttäjän palvelimet on yhdistettu "utility networkiin", joka yhdistää kaikkia yrityksen palvelinkeskuksia. Tämä takaa nopean yhteyden palvelinten välillä.

![image](https://github.com/user-attachments/assets/47cdbf60-7a66-4c37-8738-b0cf383b4167)

Myöskään seuraaviin en tehnyt muutoksia ja sivusto kertoi, että Metadata Servicen pitää olla päällä valitsemassani kokonaisuudessa.

![image](https://github.com/user-attachments/assets/150161e2-470e-48c5-8cf2-1a8716077a0a)

Tunnilla kerrottiin, että SSH olisi parempi vaihtoehto, mutta koska emme vielä osaa tätä, voimme valita salasanan. Tässä kohtaa ongelmaksi tuli se, että sivusto ilmoitti, etten voi valita salasanaa kyseisen käyttöjärjestelmän version kanssa.

![image](https://github.com/user-attachments/assets/149dd5d9-e3bf-45a9-8a59-32b04c40e851)

Joudun siis omatoimisesti perehtymään SSH-salaukseen, jos en halua luovuttaa. Tämä lienee hyvä hetki pitää tauko.

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

Tätäkin pitäisi varmaan selvittää. Googlaus tuottikin yllättävän helposti vastauksen (https://www.tecmint.com/client_loop-send-disconnect-broken-pipe/) eli yhteys katkeaa, kun se on liian pitkään käyttämättä. Liian pitkään on tässä hyvin suhteellinen käsite, sillä hetki tiedonhakua muualla katkaisi yhteyden.

![image](https://github.com/user-attachments/assets/b47d1f3a-cc20-4769-9435-468ae96d0f65)


**Lähteet**

- ChatGPT
- Finder: UpCloud Oy. https://www.finder.fi/IT-palvelut/UpCloud+Oy/Helsinki/yhteystiedot/2617969
- Karvinen 2012: First Steps on a New Virtual Private Server – an Example on DigitalOcean and Ubuntu 16.04 LTS. https://terokarvinen.com/2017/first-steps-on-a-new-virtual-private-server-an-example-on-digitalocean/
- Karvinen, Tero 2020: Command Line Basics Revisited. https://terokarvinen.com/2020/command-line-basics-revisited/?fromSearch=command%20line%20basics%20revisited
- Karvinen, Tero 2024: Oppitunti 11.9.2024. Linux-palvelimet. https://terokarvinen.com/linux-palvelimet/
- Karvinen, Tero: Install Debian on Virtualbox - Updated 2023. https://terokarvinen.com/2021/install-debian-on-virtualbox/
- Lovet, Kris. Benchmark between cloud servers (January 2024). (https://techblog.nexxwave.eu/benchmark-between-cloud-servers-january-2024/)
- NetworkChuck 18.3.2021: 5 Steps to Secure Linux (protect from hackers). https://www.youtube.com/watch?v=ZhMw53Ud2tY
- Oracle. 4 Working with SSH Key Pairs. https://docs.oracle.com/en/operating-systems/oracle-linux/openssh/openssh-WorkingwithSSHKeyPairs.html#remote-access-without-password
- Saive, Ravi 31.5.2023: How to Fix SSH Client_loop: send disconnect: Broken pipe Error. https://www.tecmint.com/client_loop-send-disconnect-broken-pipe/
- Susanna Lehto 2022: Teoriasta käytäntöön pilvipalvelimen avulla (h4). https://susannalehto.fi/2022/teoriasta-kaytantoon-pilvipalvelimen-avulla-h4/
- UpCloud 24.5.2023: How to use SSH keys for authentication https://upcloud.com/resources/tutorials/use-ssh-keys-authentication
- UpCloud 23.4.2024: How to deploy a new Cloud Server. https://upcloud.com/resources/tutorials/deploy-server
- UpCloud: Documentation. https://upcloud.com/docs/products/networking/features/utility-network/

---
  
*Tätä dokumenttia saa kopioida ja muokata GNU General Public License (versio 2 tai uudempi) mukaisesti. http://www.gnu.org/licenses/gpl.html*

*Pohjana Tero Karvinen 2012: Linux kurssi, http://terokarvinen.com*

*Raportin tekijä: Jenni Muhonen*
