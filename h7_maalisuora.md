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

Olin kopioinut huolimattomasti ja jättänyt luokka-osion pois. Ihmettelin vielä, eikö tähän tule mainintaa puclic classista ja silti en ollut tarkistanut kopioinko oikein. Samalla kun korjasin asian, nimesin myös tiedostot alkamaan isoilla kirjaimilla.

![image](https://github.com/user-attachments/assets/9d90e25e-c825-425a-a9ed-84599e06ca00)

Lopuksi ajoin ohjelman:

![image](https://github.com/user-attachments/assets/3d83f631-f7a9-40a1-943d-cf46114e9e06)

Toimii.







---

**Lähteet**

- Karvinen, Tero 2018: Hello World Python3, Bash, C, C++, Go, Lua, Ruby, Java – Programming Languages on Ubuntu 18.04. https://terokarvinen.com/2018/hello-python3-bash-c-c-go-lua-ruby-java-programming-languages-on-ubuntu-18-04/
- man javac
- WebHi: How to install Java with “apt-get” on Ubuntu / Debian. https://www.webhi.com/how-to/how-to-install-java-with-apt-get-on-ubuntu-debian/

---
  
*Tätä dokumenttia saa kopioida ja muokata GNU General Public License (versio 2 tai uudempi) mukaisesti. http://www.gnu.org/licenses/gpl.html*

*Pohjana Tero Karvinen 2024: Linux kurssi, http://terokarvinen.com*

*Raportin tekijä: Jenni Muhonen*
