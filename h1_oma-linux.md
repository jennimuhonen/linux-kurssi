# h1 Oma Linux

Tehtäviä Tero Karvisen kurssille Linux Palvelimet 2024. https://terokarvinen.com/linux-palvelimet/

Markdownissa apuna: Markdown Guide: Markdown Cheat Sheet. https://www.markdownguide.org/cheat-sheet/.


## x) Lue ja tiivistä

Lähdeteksti tiivistelmän alla.

### Tietokoneiden teknisten testien raportointi
- kerro täsmällisesti mitä teit ja mitä sitten tapahtui
- kirjoita raporttia samalla kun teet
- toistettavuus: joku toinen voi toistaa kaiken mokien kera -> raportoi siis myös toimintaympäristö
- täsmällisyys: komennot, klikkaukset, kellonajat, onnistuiko ja mitä sen jälkeen (kuinka totesit onnistumisen?), kirjaa odottamaton, imperfektissä
- helppolukuisuus: väliotsikot, huolellinen kieli, kanavaan sopivuus, halutessa tiivistelmä
- muista lähdeviitteet
- vakiotekstit
- älä tee tätä: sepitä, plagioi, kuvien luvaton käyttö

**Lähteet**

- Karvinen, Tero 2006: Raportin kirjoittaminen. https://terokarvinen.com/2006/raportin-kirjoittaminen-4/


### Free Software ja siihen liittyvät neljä vapautta

**Mitä Free Softwarella tarkoitetaan?**

- käyttäjällä on vapaus suorittaa, kopioida, jakaa, tutkia, muuttaa ja parantaa ohjelmistoa
- kyse on vapaudesta ei hinnasta eli sana "free" tulisi kääntää vapaaksi ei ilmaiseksi -> joskus "libre software"
- free softwaren on voinut saada ilmaiseksi tai siitä on voinut maksaa, mutta käyttäjällä on aina oikeus kopioida ja muuttaa ohjelmistoa ja jopa myydä siitä kopioita
- termejä ohjelmalle, jota käyttäjät eivät kontrolloi: "nonfree", "proprietary"
- kirjoittaja toteaa: "The nonfree program controls the users, and the developer controls the program; this makes the program an instrument of unjust power."
- "open source" ei ole sama kuin "free software", vaikka lähes kaikki ovatkin käytännössä "free"

**Neljä vapautta**

- ohjelma on vapaa, jos käyttäjällä on seuraavat neljä vapautta
- vapaus suorittaa ohjelmaa kuten haluaa, mihin vain käyttötarkoitukseen
- vapaus tutkia kuinka ohjelma toimii ja muuttaa sitä käyttäjän maun mukaiseksi (edellytyksenä pääsy lähdekoodiin)
- vapaus jakaa edelleen kopioita, jotta voi auttaa muita
- vapaus jakaa kopioita käyttäjän itse muokkaamasta versiosta muille (koko yhteisö pääsee hyötymään käyttäjän muutoksista, edellytyksenä pääsy lähdekoodiin)

**Muuta**

- voi olla kaupallinen ja itseasiassa tulee olla oikeus käyttää kaupallisesti
- tietyt säännöt free softwaren levittämiseen ovat sallittuja, kun ne eivät ole konfliktissa keskeisten vapauksien kanssa, esim. copyleft
- artikkelissa kerrotaan erilaisia seikkoja, jotka ovat lisenssissä sallittuja ja ongelmallisia
- jos lisenssissä on kohtuuttomia rajoituksia, ohjelma voidaan määritellä ei-vapaaksi, vaikka free softwaren määritelmissä rajoituksia ei olisikaan huomattu huomioida
- on olemassa erilaisia lisenssejä free softwarelle
- virallinen suomennos on vapaa ohjelmisto
- ohjelmistojen manuaalien yms. tulisi myös olla vapaita, hyvä esimerkki on Wikipedia

**Lähteet**

- Free Software Foundation: What is Free Software? https://www.gnu.org/philosophy/free-sw.html.
- Free Software Foundation: Translations of the term “free software”. https://www.gnu.org/philosophy/fs-translations.html
- Suomenkielisten termien etsinnässä apuna Google Translate, https://translate.google.com/

---


## a) Asenna Linux virtuaalikoneeseen

*Tehtävän aloitus 22.8.2024 klo 12.25*

Toimintasuunnitelma:

1. varmuuskopioi
2. kuvaa käytössä oleva rauta & OS
3. virtuaalikone
4. linux

Muista koko ajan raportoida + lähteet.


### Varmuuskopioi

Luennolla muistutettiin huolehtimaan varmuuskopioista, koska koskaan ei tiedä mitä tapahtuu. Pääosin oleelliset asiat ovat jo valmiiksi pilvessä eli elän luottaen pilvipalveluihin.

Jossain vaiheessa voisi hankkia uuden ulkoisen kovalevyn, kuten opettaja tunnilla suositteli. Lähes 20 vuotta vanhaan ulkoiseen kovalevyyn en taida enää uskaltaa luottaa.

Työn alla olevan Ohjelmointi 1 -kurssin tehtävät olivat vain kovalevyllä, joten varmuuskopioin ne OneDriveen talteen. Kuvatiedostoja varmuuskopioin Dropboxiin.


### Käytössä oleva rauta & OS

Etsin sähköpostistani sinne tallettamani tiedot koneeni osista. Lisäksi tarkistin Windowsin asetukset kohdasta Järjestelmä > Tietoja.

En ollut aivan varma, mitä kaikkea tietoja omasta koneesta tulisi kertoa, joten tutkin satunnaisotannalla, kuinka kevään kurssilaiset olivat tehneet. Tarkastelemistani tehtävistä tarkin kuvaus oli Juuso Vainikalla, josta otin osin mallia.


**Koneen tiedot** 

- Pöytäkone
- Käyttöjärjestelmä: Windows 11 Education
- CPU: AMD Ryzen 5 7600 3.8 GHz 6-Core Processor
- Emolevy: MSI PRO B650-P WIFI
- Muisti: 32 GB DDR5-6000 CL30
- SSD: 2 TB, jossa vapaata tilaa 982 Gt
- Näytönohjain: RX 6800 XT 16 GB


### VirtualBox

*22.8.2024 14:13*

Luennolla suositeltiin asentamaan Virtual box, joten tällä mennään. Google-haku ei anna suoraan yksiselitteistä vastausta, mitä linkkiä klikata ja sitä kautta hypätä suoraan asennukseen eli tein taustatutkimusta aiheesta.

Tutustuin aiheeseen Kevin Stratvertin Youtube-videon avulla. Hän kehottaa tarkistamaan onko, virtualisointi tietokoneella sallittuna. Tarkastin hänen ohjeidensa mukaan Tehtävienhallinnasta, että asia on kunnossa.

Seuraavaksi Stratvert vastasi alkuperäiseen kysymykseeni siitä, miltä sivulta lataan VirtualBoxin ja suuntasin sivustolle https://www.virtualbox.org/. Latasin sivulta VirtualBox 7.0.20 platform packages/Windows hosts.

Aloin asentamaan VirtualBoxia ja seurasin samalla Stratvertin ohjeita. Custom Setup -ikkuna ei kuitenkaan vastannut Stratvertin videolla näyttämää versiota, joten googlasin hieman ennen kuin klikkasin kohdan "Register file associations". Geekflaren sivuilta löytyneessä asennusohjeessa Hitesh Sant ei avaa kyseista valintaa suuremmin, mutta esimerkkikuvassa kohta on valittuna, joten hyväksyin valinnan ja jatkoin eteenpäin.

![image](https://github.com/user-attachments/assets/21a0070f-0bd3-4895-8923-0124addd6039)

Muuten asennus oli ruudusta toiseen klikkailua ja lopulta asennus oli valmis.

![image](https://github.com/user-attachments/assets/696b0484-c928-4d95-9d21-dd6cd048c7c3)

VirtualBox näyttäisi avautuvan ongelmitta.

![image](https://github.com/user-attachments/assets/8bffe799-4bff-4b5a-96a1-53cbecd83eaa)


### Debian

*22.8.2024 14:51*

Kevin Stratvert ohjeistaa seuraavaksi Youtube-videollaan, kuinka VirtualBoxiin asennetaan Linux. Hän kuitenkin asentaa Ubuntun ja kurssilla tarkoituksena on asentaa Debian, joten hyppäsin hetkeksi videon matkasta etsimään oikeaa asennustiedostoa.

Kurssin pääsivulta seurasin opettajan asennusohjeisiin sivulle https://terokarvinen.com/2021/install-debian-on-virtualbox/. Täältä löytyivät linkki ja neuvot oikean asennustiedoston etsintään.

Oikean tiedoston lataaminen ei kuitenkaan ollut aivan niin selkää. Sivustolla https://cdimage.debian.org/debian-cd/current-live/amd64/iso-hybrid/ on pitkä lista tiedostoja, mutta mikä näistä on oikea? Kopioin opettajan sivulta halutun tiedostonimen debian-live-12.6.0-amd64-xfce.iso, painoin Ctrl+F ja Ctrl+V ja Enter ja vaihtoehdot rajautuivat. Latasin .iso-päätteisen tiedoston eli vaihtoehdoista suurimman (kuten opettajakin taisi tunnilla ohjeistaa).

![image](https://github.com/user-attachments/assets/184cbc7b-95ec-457e-ab67-9ac6bf11ffd7)


### Takaisin virtuaaliboksiin

*22.8.2024 15.19.*

Pienen tauon jälkeen palasin Stratvertin video-ohjeiden pariin.

Videolla ohjeistetaan, että seuraavaksi pitää luoda uusi virtuaalikone. Klikkasin siis New.

![image](https://github.com/user-attachments/assets/cd7d4d89-02ac-409b-a4de-a3d6089a6c40)

Videolla annetaan seuraavat neuvot asennusikkunan valintoihin:

- nimeksi yksinkertaisesti Ubuntu (eli Debian meidän tapauksessamme), sijainniksi sellainen, jossa on tarpeeksi tilaa ja etsitään juuri äsken ladatun iso-tiedoston sijainti.
- seuraavassa ikkunassa suositellaan vaihtamaan käyttäjänimi ja salasana ja suositellaan klikkaamaan kohta Guest Additions
- Hardware-ikkunassa Stratwert antaa virtuaalikoneelle neljä gigaa muistia ja neljä prosessoria. (Tarkistin myös opettajan ohjesivulta, siellä esimerkissä on myös 4 gigaa muistia, mutta prosessorien määrästä en löytänyt mainintaa.)
- Virtual Hard disk -sivusta Stratvert toteaa, että Pre-allocate Full Size parantaa hieman suorituskykyä, mutta ei kuitenkaan suosittele tätä valintaa

Noudatin Stratvertin suosituksia:

![image](https://github.com/user-attachments/assets/6da3a4d6-dabf-4c6b-a3db-e76361158349)

![image](https://github.com/user-attachments/assets/f50c7ab2-f765-4ccf-bcf6-9b2ef8b2b613)

Ennen seuraavia valintoja googlasin hieman prosessorien määrää virtuaalikoneessa. Päädyin lukemaan paria eri Reddit-keskustelua, joiden perusteella voisin aloittaa myös kahdesta ja tätä voisi sitten myöhemmin tarvittaessa nostaa. Kuinka eri valinnat vaikuttavat toisaalta Debianin toimintaan ja toisaalta Windowsin toimintaan? Totesin, että tarvitsen jonkin paremman lähteen ja googlasin lukemaan Asyush Panden artikkelia aiheesta. Hänen mukaansa paras tasapaino suorityskyvyn ja vakauden välillä saadaan, jos virtuaalikoneelle annetaan 50-75% "physical core":sta, mutta ei koskaan enempää, kuin systeemissä on saatavilla.

Päädyin pysymään Stratvertin ohjeissa, vaikka hänen koneellaan onkin hieman enemmän prosessoreita.

![image](https://github.com/user-attachments/assets/4d442b0e-8032-4108-9b58-7106259018e8)

![image](https://github.com/user-attachments/assets/70200246-059c-4f39-87a2-210466bc7444)

Opettajan ohjeissa virtuaalikoneelle on annettu mahdollisuus käyttää 60 GB tilaa, joten menin sillä.

![image](https://github.com/user-attachments/assets/1dfb5268-cc58-412c-9944-8a17e7c0e62e)

![image](https://github.com/user-attachments/assets/d068868b-f298-4f1b-a586-de7b0a2fbf66)

Tarkoittaako tuo viesti oikealla sitä, että asennuksessa on joku ongelma?

![image](https://github.com/user-attachments/assets/679e7374-91bc-4256-8d04-9812ee8d894c)

Koska näkymä ei vastaa Stratvertin videota, oli aika etsiä seuraava video, jolla asennetaan juuri Debiania. Videon tekijänä on ProgramminKnowledge. Katsoin videolta uudestaan edellä tekemäni ja videolla iso-tiedoston sijaan valitaan 64-bittinen Debian. Tämä valinta oli minulle harmaana. Myös opettajan ohjeissa on 64-bittinen versio. Kokeilin muuttaa tämän asetuksista. Aiemmin valittuna oli 32-bittinen.

![image](https://github.com/user-attachments/assets/a2e4186d-fdf9-474b-91e2-cc24caa8fe75)

Ilmeisesti Ubuntun asennus toimi eri tavalla, saamani näkymä oli ProgramminKnowledgen videon perusteella odotettu. Videolla neuvotaan muuttamaan General-asetuksien alta Advanced-asetuksista kahteen kohtaan Bidirectional. Tämä ilmeisestikin mahdollistaa tiedostojen helpon siirtämisen Windowsin ja Debianin välillä. Muutin asetukset.

![image](https://github.com/user-attachments/assets/13879d78-c3b3-44c7-a5df-59cd5b7ed1fc)

Seuraavaksi ProgramminKnowledge ohjeistaa menemään asetuksissa kohtaan Storage ja laittamaan sinne tiedon iso-tiedostosta. Ilmeisesti tämä tieto ei ollutkään jäänyt muistiin. Tein ohjeen mukaisesti.

![image](https://github.com/user-attachments/assets/d8fd6fc0-21bb-4044-b405-11d88fbaf805)

Tämän jälkeen neuvotaan klikkaamaan Start, tein näin.

![image](https://github.com/user-attachments/assets/ed04290e-0377-42da-a0e0-b2d0d1dfa0b7)

Tämän jälkeen edessä oli lopulta tunnilta tutun näköinen asennusnäkymä.


### Debianin asentaminen

*22.8.2024 16:39*

![image](https://github.com/user-attachments/assets/ebe8edcb-add8-4c60-9e3e-70e3bd4edc35)

Painoin Enter.

![image](https://github.com/user-attachments/assets/51ea048d-3675-44ce-aa59-cac7d8db0b83)

Yllä oleva näkymä oli hyvin hämmentävä, sillä mihin menivät kaikki asennukseen liittyvät valinnat? Ohjevideollani tehtiin asennus eri lailla, mutta opettajan ohjeissa neuvotaan valitsemaan default-vaihtoehto, joten hylkäsin videon ja aloin lukemaan tarkemmin ohjeita. Hämmennykseni hälventyi, sillä opettajan mukaan kyseessä on testiversio Linuxista. Mitään ei siis vielä olekaan asennettu!

Seuraavaksi opettajan ohjeissa kehotetaan testaamaan Linuxia avaamalla selain, googlaamaan jotain ja käyttämään hiirtä ja testaamaan linkkejä. Etsiydyin toisella kurssilla tekemälleni sivustolle ja klikkailin ympäriinsä. Kyllä toimii. (Sen sijaan Linuxin ollessa valittuna ruudunkaappaustyökalu ei toimi. Valitsin eri ikkunan ja kaappaustyökalu oli taas toiminnassa.)

![image](https://github.com/user-attachments/assets/c8ed7a0e-fd88-479c-9498-ee21651de3ad)

Selainta sulkiessa jouduin olemaan tarkkana, etten sulkenut koko Debiania. Hieman vielä opettelua käyttöliittymän kanssa. Vältin kuitenkin mokan ja seuraavaksi siirryin varsinaiseen Debianin asennukseen. Kieleksi valitsin opettajan ohjeiden mukaisesti englannin ja seurasin muutenkin opettajan ohjeita. Alla kuvina valitut asetukset.

![image](https://github.com/user-attachments/assets/c49d339f-de2a-4225-9ef5-63921bf8c4e2)

![image](https://github.com/user-attachments/assets/a522cafd-1634-43f3-8da3-d087fc98b4a7)

![image](https://github.com/user-attachments/assets/3ae4dfc0-da98-4781-a0d0-47679aa7abd6)

![image](https://github.com/user-attachments/assets/00738f97-1694-47ed-a240-17ddde93b51d)

![image](https://github.com/user-attachments/assets/18fc1270-a5e1-4a8c-813b-bb65bc8ee741)

Pienen hetken jouduin miettimään, kuinka saan Install-nappulan näkyviin. Ratkaisu oli klikata koko ruudun näkymää asennusikkunassa.

![image](https://github.com/user-attachments/assets/3d46c109-dd0d-4569-87a2-1967386c2600)

![image](https://github.com/user-attachments/assets/eadef9d1-d539-4da6-a418-6a8681aedd9a)

![image](https://github.com/user-attachments/assets/82dcb3d7-059a-405e-b01e-4923ab56c815)

Debian näyttäisi asentuneen.

*22.8.2024 17:18*

![image](https://github.com/user-attachments/assets/3b3522cd-60a8-4ac9-8713-8e99cfd91a26)

Miksi Debianin näkymä on niin pieni? Onko tämä tarkoitus, voiko tätä muuttaa jostain asetuksista? Vastauksen selvittämisen sijaan siirryin tekemään ekstratehtävää.

---

Myöhemmin illalla ruudun koon ongelmaan löytyi ratkaisu asetuksia tutkimalla. Aiemmin pikagooglatessa Super userin googletulosnäkymässä tämä ehdotus oli ollut, mutta silloin luultavasti yritin liian suurta resoluutiota. Baeldung nimittäin kirjoittaa artikkelissaan, että Debian 12:ssa maksimiresoluuion on 1366 x 768. Debianin ikkunan kokoa saa muutettua, kun klikkaa hiiren oikealla näppäimellä, valitsee Applications -> Settings -> Display ja vaihtaa resoluution suuremmaksi.

Resoluutio kuitenkin palautuu alkuperäiseksi, jos Debianin päästää menemään kirjautumisnäkymään. Tämä tapahtuu liian nopeasti, seuraavaksi pitäisi siis löytää asetus tämän viivyttämiseksi.

Ruudussa vilahteli välillä ärsyttäviä virheilmoituksia, kun klikkaili pikkuruisen ruudun rajalla huonosti skaalautunutta verkkosivua oikealle ja vasemmalle.

![image](https://github.com/user-attachments/assets/e6977dec-bf1f-42ba-a796-b21f7cd070f6)

Virheilmoituksessa sanotaan drag and drop, joten arvelin, että tämä voisi johtua ohjevideolla ehdotetusta asetuksesta Bidirectional. Kokeilin palauttaa asetukseksi Disabled ja virheilmoitukset katosivat. (Eli VirtualBox:n puolella Settings -> General -> Advanced ja valinnoiksi Disabled.)


**Lähteet**

- Baeldung: Increasing Screen Size/Resolution on a VirtualBox Instance. https://www.baeldung.com/linux/virtual-box-larger-screen 
- Debianin lataussivu. https://cdimage.debian.org/debian-cd/current-live/amd64/iso-hybrid/
- Karvinen, Tero: Install Debian on Virtualbox - Updated 2023. https://terokarvinen.com/2021/install-debian-on-virtualbox/
- Karvinen, Tero: Linux Palvelimet 2024 alkukevät. https://terokarvinen.com/2024/linux-palvelimet-2024-alkukevat/
- Karvinen, Tero: Linux Palvelimet 2024 alkuksyksy. https://terokarvinen.com/linux-palvelimet/
- Karvinen, Tero: Oppitunti 21.8.2024. Linux-palvelimet. https://terokarvinen.com/linux-palvelimet/
- Pande, Ayush: How many CPUs should I assign to a VM? https://www.xda-developers.com/how-many-cpus-vm/
- ProgramminKnowledge. How to Install Debian Linux on VirtualBox on Windows 11. https://www.youtube.com/watch?v=Rusk2FofQPo
- Reddit. How many processors and cores per processor should I assign to my VM? https://www.reddit.com/r/vmware/comments/suqdtj/how_many_processors_and_cores_per_processor/
- Reddit. Recommended number of CPU cores to allocate to VMs? https://www.reddit.com/r/Proxmox/comments/ri1u49/recommended_number_of_cpu_cores_to_allocate_to_vms/
- Sant, Hitesh: How to Install VirtualBox on Windows? https://geekflare.com/install-virtualbox-on-windows/
- Stratvert, Kevin: How to use VirtualBox - Tutorial for Beginners. https://www.youtube.com/watch?v=nvdnQX9UkMY
- Superusers: Increase resolution for debian guest in virtualbox. https://superuser.com/questions/923313/increase-resolution-for-debian-guest-in-virtualbox
- Vainikka, Juuso. Introduction. https://github.com/GitJuski/Linux-servers/blob/main/h1-GJ.md
- VirtualBox. Welcome to VirtualBox.org! https://www.virtualbox.org/

**Henkilökohtaiset lähteet: oma tietokone ja sähköposti**

- Muhonen, Jenni: My PC build. 2.7.2023. Sähköposti
- Tehtävienhallinta: Suorituskyky, Suoritin
- Tämä tietokone: Laitteet ja asemat
- Windowsin Asetukset: Järjestelmä > Tietoja

---


## k) Suosikkiohjelmani Linuxilla

Yksi suosikki-ohjelmistani on Steam, joka pikaisen googlauksen perusteella (Jack Wallenin artikkeli Googlen esikatselunäkymässä) näyttäisi toimivan myös Debianissa. Tätä siis päätin kokeilla.

Windowsissa Steam tarjoaa sivun yläkulmassa asennus-vaihtoehdon, mutta Debianin puolella tätä en näe. Mikä on ongelmana? Googletin. Googlettaminen ei ratkaissut asiaa, vaan satunnainen klikkailu Steamissä. En ollut työpöytäsivustolla ja siksi asennusvaihtoehtoa ei ollut näkyvissä.

![image](https://github.com/user-attachments/assets/ce8efb7f-1dcd-4f76-9b29-14d30cdc5e90)

![image](https://github.com/user-attachments/assets/630d5eca-49cd-4628-aaa0-71298afaa2a1)

Klikkasin Asenna. Sen jälkeen pääsin jälleen hämmentymään.

![image](https://github.com/user-attachments/assets/dc338c2c-f183-4da9-b2c7-50c1413ca168)

Yllä oleva näkymä muistutti mieleeni, että olemme nyt jossain muualla kuin Windowsissa ja että en ymmärrä Debianista tai Linuxista mitään. Googlasin lisää asennusohjeita. Päädyin jälleen Youtubeen. Linux made simple -kanavan videolla juoksevat komentorivit vakuuttivat minut siitä, että jään sittenkin odottelemaan seuraavia tunteja ja sitä, että opin käyttämään Debiania ennen kuin alan itse satunnaisesti testailemaan.

Sanottakoon siis, että selain olikin suosikkiohjelmani ja latasin sillä onnistuneesti Steamin lataustiedoston. Alkuperäinen suunnitelmani oli selvästi liian korkealentoinen asennusprojektin päätteeksi. ;)


**Lähteet**

- Linux made simple: How to install Steam on Debian 12. https://www.youtube.com/watch?v=tX9RswgmLWI
- Steam. https://store.steampowered.com/
- Wallen, Jack. How to install Steam and start gaming on almost any Linux distro - now it's a Snap. https://www.zdnet.com/article/how-to-install-steam-and-start-gaming-on-almost-any-linux-distro-now-its-a-snap/![image](https://github.com/user-attachments/assets/a97fb0ad-3698-4f96-b579-44058a59e53f)



---

*Tätä dokumenttia saa kopioida ja muokata GNU General Public License (versio 2 tai uudempi) mukaisesti. http://www.gnu.org/licenses/gpl.html*

*Pohjana Tero Karvinen 2012: Linux kurssi, http://terokarvinen.com*
