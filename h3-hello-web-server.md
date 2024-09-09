# h3 Hello Web Server

Tehtäviä Tero Karvisen kurssille Linux Palvelimet 2024. https://terokarvinen.com/linux-palvelimet/

---

## x) Lue ja tiivistä

**Apache: Name-based Virtual Host Support**
- IP-based virtual hosts: jokaisella täytyy olla oma ip-osoite
- Name-based virtual hosts: voivat jakaa saman ip-osoitteen
- Jälkimmäiseen tarvitaan vähemmän ip-osoitteita, joita on rajatusti
- Tätä kannattaa käyttää, jos ei ole erityistä tarvetta ip-pohjaiseen ja harvemmin on


**Karvinen: Name Based Virtual Hosts on Apache – Multiple Websites to Single IP Address**
- Apachen avulla voi saada monta verkkotunnusta (domain name) yhdelle IP-osoitteelle
- Komennot verkkopalvelimen asentamiseksi ja konfiguroimiseksi
- Komennot uuden nimeen pohjautuvan virtual hostin lisäämiseksi
- Komennot siihen, kuinka voi luoda verkkosivun normaalina käyttäjänä sekä  komennot testaamiseen 


**Lähteet:**
- The Apache Software Foundation 2023: Apache HTTP Server Version 2.4 Documentation: Name-based Virtual Host Support. https://httpd.apache.org/docs/2.4/vhosts/name-based.html
- Karvinen 2018: Name Based Virtual Hosts on Apache – Multiple Websites to Single IP Address. https://terokarvinen.com/2018/04/10/name-based-virtual-hosts-on-apache-multiple-websites-to-single-ip-address/


## Rauta ja OS

**Virtualisoidun Linuxin tiedot**

- Käyttöjärjestelmä: Debian 12.6.0 AMD64
- Virtualisointi: VirtualBox 7.0.20
- Muisti: 4096 MB
- Prosessorit: 4 CPU
- Virtuaalilevyn maksimikoko: 60 GB, josta käytetty 13,92 GB

**Taustajärjestelmän tiedot**

- Pöytäkone
- Käyttöjärjestelmä: Windows 11 Education, 64 bittinen käyttöjärjestelmä, x64-suoritin
- CPU: AMD Ryzen 5 7600 3.8 GHz 6-Core Processor
- Emolevy: MSI PRO B650-P WIFI
- Muisti: 32 GB DDR5-6000 CL30
- SSD: 2 TB, jossa vapaata tilaa 967 GB
- Näytönohjain: AMD RX 6800 XT 16 GB


## a) Testaa

*Tehtävä: Testaa, että weppipalvelimesi vastaa localhost-osoitteesta. Asenna Apache-weppipalvelin, jos se ei ole jo asennettuna.*

*9.9.2024 10.45*

Asensin Apachen luennon aikana, joten aloitan testaamalla.

Kuten luennolla neuvottiin, kirjoitin selaimen osoitekenttään localhost ja sain Apachen oletussivun näkyviin:

![image](https://github.com/user-attachments/assets/6a95bea9-c723-402b-b6f7-5fe906ff15fc)

Näyttäisi siis hyvältä. Testataan vielä myös komentorivin puolella kehoitteella `curl localhost`, johon myös tutustuttiin tunnilla.

![image](https://github.com/user-attachments/assets/8d427ff2-62b4-44cd-9b4a-66c134da2e96)

Tälläkin puolella näyttää hyvältä, ja <title>-kohdassa nähdään sivun nimi It works, joka nähtiin myös selaimen puolella.


## b) Etsi lokista

*Tehtävä: Etsi lokista rivit, jotka syntyvät, kun lataat omalta palvelimeltasi yhden sivun. Analysoi rivit (eli selitä yksityiskohtaisesti jokainen kohta ja numero, etsi tarvittaessa lähteitä).*




**Lähteet:**
- Karvinen, Tero: Oppitunti 4.9.2024. Linux-palvelimet. https://terokarvinen.com/linux-palvelimet/
- 

---
  
*Tätä dokumenttia saa kopioida ja muokata GNU General Public License (versio 2 tai uudempi) mukaisesti. http://www.gnu.org/licenses/gpl.html*

*Pohjana Tero Karvinen 2012: Linux kurssi, http://terokarvinen.com*

*Raportin tekijä: Jenni Muhonen*
