# Samsung Galaxy S6 Androidin päivittäminen versioon 10

### Ota varmuuskopiot kaikista tiedostoistasi, joita et halua menettää ennen kuin jatkat Androidin päivitystä!

**Huomio! Päivitä CP/baseband/modeemi ennen kuin päivität Androidin**. Modeemi on helpoin päivittää asentamalla uusin virallinen Android 7. Android-käyttöjärjestelmän päivitys versioon 9  ei päivitä modeemia. Jos puhelin on päivitetty uuteen Android-versioon kauan sitten (esim. Android versioon 8), puhelimen modeemi on saattanut jäädä vaille saada päivityksiä.

## Asennustiedostojen lataaminen valmiiksi
1. Lataa uusin versio TWRP:stä
    * https://twrp.me/samsung/samsunggalaxys6.html
    * Tässä ohjeessa käytettiin versiota twrp-3.3.1-0-zeroflte.img.tar
    * TWRP on palautusohjelma, jolla pystyy asentamaan eri Android-versioita puhelimeen.
2. Lataa uusin Android 9 Pie
    * https://www.los-legacy.de/zerofltexx
    * Tässä ohjeessa käytettiin versiota  	lineage-17.1-20200606-UNOFFICIAL-zerofltexx.zip
    * Lataa/luo myös md5sum-tiedosto, jolla voi tarkistaa, että lataus ei ole korruptoitunut lineage-17.1-20200606-UNOFFICIAL-zerofltexx.zip.md5
3. Lataa Open GApps
    * http://opengapps.org/
    * S6 on ARM64
      * Lähde: http://itechify.com/2016/07/13/identify-correct-architecture-for-android-apk-arm-arm64/
    * Tässä ohjeessa käytettiin versiota open_gapps-arm64-10.0-pico-2020-1023.zip
    * Lataa myös md5-tiedosto, jolla voi tarkistaa, että lataus ei ole korruptoitunut
4. Valinnainen: lataa Magistk-ohjelma, jolla voit rootata puhelimesi.
5. Siirrä tiedostot puhelimelle
    * Android asennustiedostot, zip sekä md5sum
    * Open GApps, zip sekä md5sum
6. Lataa Odin-ohjelma
    * https://odindownload.com/download/
    * Tässä ohjeessa käytettiin versiota v3.14.1

## Modeemin / Basebandin / CP:n (Communication Processor) päivittäminen
* Katso puhelimen modeemin päivitysohjeet linkistä:
** https://github.com/iisti/mobile-tricks/blob/main/samsung-s6-android-9-asennusohje.md#modeemin--basebandin--cpn-communication-processor-p%C3%A4ivitt%C3%A4minen

## TWRP:n asennus
   1. Käynnistä Odin
   1. Klikkaa AP ja valitse TWRP tar-paketti, esim. twrp-3.3.1-0-zeroflte.img.tar
   1. Sammuta puhelin ja käynnistä puhelin lataustilassa
      * Paina yhtäaikaa "Koti + Virta + Äänenvoimakkuusalas"-näppäimiä, (Home + Power + Volume Down)
   1. Kytke puhelin tietokoneeseen USB:lla.
      * ID: COM ruutuun pitäisi ilmestyä **0:[COM5]** tai jotakin saman tapaista.
   1. Aloita fläshäys painamalla **Start**
   1. Puhelimen pitäisi käynnistyä uudelleen automaattisesti TWRP-ohjelmaan.
      * Jos puhelin ei käynnistö automaattisesti TWRP:hen:
        * Paina yhtäaikaa "Koti + Virta + Äänenvoimakkuusylös" -näppäimiä, (Home + Power + Volume Up)

## Android 10:n asennus
1. Team Win Recovery Project -palautustilassa valitse **Wipe**
  * Valitse: Advanced Wipe -> Dalvik / ART Cache, Data, Internal Storage, Cache, System
  * Valitse: Format Data
1. Yhdistä puhelin USB:lla ja kopioi GApps ja LineageOS puhelimeen
1. Mene TWRP:n aloitus valikkoon ja valitse **Install**
  1. sdcard -> LineageOS zip -> täppää *Zip signature verification*
  1. Lisää myös OpenGapps zip asennettavaksi.
  1. Confirm Flash
1. Fläshää myös Magisk samalla tavalla.
1. Pyyhi välimuisti pariin kertaan.
    * Wipe Cache/Dalvik
1. Käynnistä puhelin uudelleen. Android 10:n pitäisi olla asennettuna.
