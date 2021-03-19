# Kuinka asentaa Android 10 Samsung S4 Mini:in

* Ohjeessa käytettiin Windows 10 Pro Build 19041 tietokonetta.

* Malli GT-i9195i
  * https://www.gsmarena.com/samsung_galaxy_s4_mini_i9195i-7468.php
* Alkuperäiset asetukset:
  * Android 4.4.4
  * Baseband i9195iXXU1A0B1
  * Kernel 3.10.28.4126898
  * Build number KTU84P.i9195iXXS1AQA4

# Lataa asennustiedostot valmiiksi tietokoneelle
1. TWRP
   * TWRP on palautusohjelma, jolla pystyy asentamaan eri Android-versioita puhelimeen.
   * https://twrp.me/samsung/samsunggalaxys4minilte.html
   * Tässä ohjeessa käytettiin versiota:
     * https://androidfilehost.com/?fid=8889791610682915398
     * https://eu.dl.twrp.me/serranoltexx/twrp-3.4.0-0-serranoltexx.img.tar.html
1. Android 10
   * Tässä ohjeessa käytetään LineageOS 17.1 ROMia
     * https://www.androidfilehost.com/?fid=8889791610682944583
   * Lähde https://forum.xda-developers.com/galaxy-s4-mini/development/rom-lineageos-17-0-t4017179
1. Open GApps
   * https://opengapps.org/
   * Asennetaan, jotta Google Play Store toimii.
   * Tässä ohjeessa käytettin versiota:
     * Platform: ARM (ARM64 antaa virheen, jos sitä yritää asentaa)
     * Android: 10
     * Variant: Pico (bare minimum functionality)
1. Magisk
   * https://github.com/topjohnwu/Magisk
   * Tässä ohjeessa käytettiin versiota 20.4.
1. Odin
   * https://odindownload.com/download/
   * Tässä ohjeessa käytettiin versiota 3.14.
1. ~Siirrä Magisk, Open_Gapps ja LineageOS puhelimelle **Documents** kansioon.~ Puhelin formatoidaan ennen asennusta, ei tarvitse siirtää vielä.

## TWRP:n asennus
1. Käynnistä Odin tietokoneella
1. Klikkaa AP ja valitse TWRP tar-paketti
1. Options-välilehdellä ota valinnat **Auto Reboot** ja **F.Reset Time** pois.
1. Sammuta puhelin ja käynnistä puhelin lataustilassa
    * Paina yhtäaikaa "Koti + Virta + Äänenvoimakkuusalas" -näppäimiä, (Home + Power + Volume Down)
1. Kytke puhelin tietokoneeseen USB:lla.
    * Odin-sovelluksen Log-ikkunaan pitäisi ilmestyä **<ID:0/00x> Added!!**
1. Fläshää puhelin painamalla Start. Log-ikkunassa pitäisi näkyä jotain tämäntapaista:

       <ID:0/006> Odin engine v(ID:3.1401)..
       <ID:0/006> File analysis..
       <ID:0/006> Total Binary size: 13 M
       <ID:0/006> SetupConnection..
       <ID:0/006> Initialzation..
       <ID:0/006> Get PIT for mapping..
       <ID:0/006> Firmware update start..
       <ID:0/006> NAND Write Start!! 
       <ID:0/006> SingleDownload.
       <ID:0/006> recovery.img
       <ID:0/006> RQT_CLOSE !!
       <ID:0/006> RES OK !!
       <ID:0/006> Removed!!
       <ID:0/006> Remain Port ....  0 
       <OSM> All threads completed. (succeed 1 / failed 0
1. Irroita USB-johto ja käynnistä kännykkä TWRP:hen painamalla yhtäaikaa:
   * "Koti + Äänenvoimakkuusylös + Virta", (Home + Volume Up + Power)

## Android 10:n asennus
1. Team Win Recovery Project -palautustilassa valitse **Wipe**
  * Valitse: Advanced Wipe -> Dalvik / ART Cache, Data, Internal Storage, Cache, System
  * Valitse: Format Data
1. Yhdistä puhelin USB:lla ja kopioi GApps, Magisk ja LineageOS puhelimeen
1. Mene TWRP:n aloitus valikkoon ja valitse **Install**
  1. sdcard -> LineageOS zip -> täppää *Zip signature verification*
  1. Lisää myös OpenGapps zip asennettavaksi.
  1. Confirm Flash
1. Fläshää myös Magisk samalla tavalla.
1. Pyyhi välimuisti pariin kertaan.
    * Wipe Cache/Dalvik
1. Käynnistä puhelin uudelleen. Android 10:n pitäisi olla asennettuna.
