# Samsung Galaxy S6 Androidin päivittäminen versioon 9 Pie

### Ota varmuuskopiot kaikista tiedostoistasi, joita et halua menettää ennen kuin jatkat Androidin päivitystä!

Näillä oheilla on päivitetty S6 onnistuneesti Android 7-versiosta versioon 9. Ohjeet on koottu eri englanninkielisistä lähteistä.
  * Päälähde: https://forum.xda-developers.com/galaxy-s6/orig-development/g920x-5x-nexusos-9-0-samsung-galaxy-s6-t3843199

**Huomio! Päivitä CP/baseband/modeemi ennen kuin päivität Androidin**. Modeemi on helpoin päivittää asentamalla uusin virallinen Android 7. Android-käyttöjärjestelmän päivitys versioon 9  ei päivitä modeemia. Jos puhelin on päivitetty uuteen Android-versioon kauan sitten (esim. vuosi sitten versioon 8), puhelimen modeemi on saattanut jäädä vaille saada päivityksiä.

~~**Toinen huomio!** Tällä hetkellä, 15.11.2018, paikannus ei toimi GPS:n kanssa. Kävellessä tämä ei haittaa, mutta autolla ei pysty ajamaan kaupungissa ja seuraamaan GPS:ää.~~ Uusimmalla 11.12.2018 julkaistulla buildilla GPS:n pitäisi toimia normaalisti.

## Asennustiedostojen lataaminen valmiiksi
1. Lataa uusin versio TWRP:stä
    * https://twrp.me/samsung/samsunggalaxys6.html
    * Tässä ohjeessa käytettiin versiota twrp-3.2.3.-0-zeroflte.img.tar
    * TWRP on palautusohjelma, jolla pystyy asentamaan eri Android-versioita puhelimeen.
2. Lataa uusin Android 9 Pie
    * https://stor.lukasberger.at/TeamNexus/Samsung/zero/9/
    * Tässä ohjeessa käytettiin versiota NexusOS-9-zero-multitarget-2018-10-08_1245.zip
    * Lataa myös md5sum-tiedosto, jolla voi tarkistaa, että lataus ei ole korruptoitunut NexusOS-9-zero-multitarget-2018-10-08_1245.zip.md5sum
3. Lataa Open GApps
    * http://opengapps.org/
    * S6 on ARM64
      * Lähde: http://itechify.com/2016/07/13/identify-correct-architecture-for-android-apk-arm-arm64/
    * Tässä ohjeessa käytettiin versiota open_gapps-arm64-9.0-micro-20181113.zip
    * Lataa myös md5-tiedosto, jolla voi tarkistaa, että lataus ei ole korruptoitunut
4. Lataa Magisk
    * https://forum.xda-developers.com/apps/magisk/
    * Ilman Magisk-ohjelmaa esimerkiksi Snapchatia ei välttämättä pysty asentamaan; toisaalta tämä taisi olla ainoa jokapäiväisessä käytössä eteen tullut ongelma.
    * Käytetty versio 17.1. Stable
5. Siirrä tiedostot puhelimelle
    * Android asennustiedostot, zip sekä md5sum
    * Open GApps, zip sekä md5
    * Magisk
6. Lataa Odin-ohjelma
    * https://odindownload.com/download/
    * Tässä ohjeessa käytettiin versiota v3.12.3

## Modeemin / Basebandin / CP:n (Communication Processor) päivittäminen
  * Modeemia ei tarvitse välttämättä päivittää, jotta Android 9:n saa asennettua. Kuitenkin xda-developers-sivulla on maininta mahdollisista yhteysongelmista, jos modeemia ei päivitä. 
> Problem: Problems with modem like dropping/slow/slowly connecting data connections, missed calls/SMS

> Solution: Try to update your device's baseband/modem to the latest available version. If there are still problems, report this bug to the developers
  
 Lähde: https://forum.xda-developers.com/galaxy-s6/orig-development/g920x-5x-nexusos-9-0-samsung-galaxy-s6-t3843199

0. **Lataa yllä olevassa ohjeessa mainitut asennustiedostot valmiiksi puhelimeesi!**
    * Tätä ohjetta tehdessä Android 7:n asennuksen jälkeen puhelin ei käynnistynyt kunnolla, vaan käynnisti itsensä aina uudelleen heti, kun taustakuva oli ladattu. Kun asennustiedostot ovat valmiiksi puhelimessa, päivitys-/asennusprosessia voi jatkaa Android 9:n asennukseen ilman, että uudelleen käynnistymisestä tarvitsee välittää.
1. Tarkista basebandin/modeemin versio, onko Settings -> System -> About Phone -> Android Version -> Baseband version: G920FXXU5DQB8 (arvo ei välttämättä ole sama).
2. Lataa uusin Android 7 -paketti. Tällä paketilla voi päivittää puhelimen modeemin.
    * https://updato.com/firmware-archive-select-model?q=sm-g920f&rpp=15&order=date&dir=desc&exact=1
      * Käytetty versio G920FXXU6ERI1_SM-G920F_1_20180927120940_x3fwqy78m2.zip
    * Toinen lähde firmwarelle https://www.sammobile.com/firmwares/galaxy-s6/SM-G920F/
3. Käynnistä Odin.
4. Käynnistä puhelin lataustilassa (Download Mode)
    * Paina yhtäaikaa "Koti + Virta + Äänenvoimakkuusalas" -näppäimiä, (Home + Power + Volume Down)
5. Kytke puhelin tietokoneeseen USB:lla.
    * ID: COM ruutuun pitäisi ilmestyä **0:[COM5]** tai jotakin saman tapaista.
6. Lisää purettu zip-paketti kohtaan AP (Android Processor) ja ruksi valinta ruutu.
    * Esim. G920FXXU6ERI1_G920FOJV6ERI1_G920FXXU6ERI1_HOME.tar.md5
7. Varmista, että **Re-Partition** ei ole valittuna **Options**-valikossa.
    * Katso, että **Auto Reboot** ja **F. Reset Time** ovat valittuna.
8. Käynnistä fläshäys painamalla **Start**
9. Puhelimen pitäis käynnistyä uudelleen automaattiseti, kun fläshäys on valmis. Anna puhelimen käynnistyä uudelleen muutaman kerran, koska tämä on normaalia asennuksen aikana. Jos puhelin kuitenkin käynnistyy uudelleen kymmeniä kertoja, kun taustakuva on ladattu, jatka Android 9:n asennukseen.

## Android 9:n asennus

1. TWRP:n asennus
   1. Käynnistä Odin
   1. Klikkaa AP ja valitse TWRP tar-paketti, esim. twrp-3.2.3.-0-zeroflte.img.tar
   1. Sammuta puhelin ja käynnistä puhelin lataustilassa
      * Paina yhtäaikaa "Koti + Virta + Äänenvoimakkuusalas" -näppäimiä, (Home + Power + Volume Down)
   1. Kytke puhelin tietokoneeseen USB:lla.
      * ID: COM ruutuun pitäisi ilmestyä **0:[COM5]** tai jotakin saman tapaista.
   1. Aloita fläshäys painamalla **Start**
1. Käynnistä puhelin TWRP:hen
    * Paina yhtäaikaa "Koti + Virta + Äänenvoimakkuusylös" -näppäimiä, (Home + Power + Volume Up)
1. Asenna Android, Gapps ja Magisk
1. Pyyhi välimuisti pariin kertaan.
    * Wipe Cache/Dalvik
1. Käynnistä puhelin uudelleen. Nyt uusin Android 9 pitäisi olla asennettuna.
