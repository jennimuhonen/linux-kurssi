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

![image](https://github.com/user-attachments/assets/cc5a36f9-a78c-4cd9-b1d5-0ea8d93902ec)


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

Eli tässä palaamme Bashin pariin.

Ensin tarvitsin jonkin komennon. Apuna toimi Milica Dancukin artikkeli (https://phoenixnap.com/kb/bash-read) read-komennosta ja whoami:n käytöstä puolestaan opin esimerkiksi StackExchangen sivuilta (https://unix.stackexchange.com/questions/473947/using-whoami-to-search-for-files-that-mention-user).

Lopputuloksena seuraava:

![image](https://github.com/user-attachments/assets/83c4aa4e-bc2a-446d-b3c2-12af29b7e811)

*(luvattoman pitkään Bashin parissa vietetyn ajan jälkeen eli 17.51)*




---

**Lähteet**

- Datacamp: What is Shell? https://www.datacamp.com/blog/what-is-shell
- Debian: Chapter 12. Programming. https://www.debian.org/doc/manuals/debian-reference/ch12.en.html#_coding_in_compiled_languages
- GNU: Bash Reference Manual. https://www.gnu.org/software/bash/manual/bash.html#What-is-Bash_003f
- Karvinen, Tero 2018: Hello World Python3, Bash, C, C++, Go, Lua, Ruby, Java – Programming Languages on Ubuntu 18.04. https://terokarvinen.com/2018/hello-python3-bash-c-c-go-lua-ruby-java-programming-languages-on-ubuntu-18-04/
- man javac
- Milica Dancuk: How To Use The Bash read Command. https://phoenixnap.com/kb/bash-read
- StackExchange: Using whoami to search for files that mention user. https://unix.stackexchange.com/questions/473947/using-whoami-to-search-for-files-that-mention-user
- WebHi: How to install Java with “apt-get” on Ubuntu / Debian. https://www.webhi.com/how-to/how-to-install-java-with-apt-get-on-ubuntu-debian/

---
  
*Tätä dokumenttia saa kopioida ja muokata GNU General Public License (versio 2 tai uudempi) mukaisesti. http://www.gnu.org/licenses/gpl.html*

*Pohjana Tero Karvinen 2024: Linux kurssi, http://terokarvinen.com*

*Raportin tekijä: Jenni Muhonen*
