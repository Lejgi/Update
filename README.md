# Creality Ender-3 V3 SE — firmware V1.1.0

Nejnovější firmware tiskárny **Creality Ender-3 V3 SE** je **V1.1.0** (soubory z 22. 4. 2025, na webu Creality od 11. 5. 2025). K 26. 9. 2026 Creality žádnou novější verzi pro tuto tiskárnu neuvádí.

Balíček obsahuje firmware originálního knoflíkového displeje a základní desky **C13** i **C14**. Každá deska si při startu vezme jen svůj soubor.

Tento postup je pro tiskárnu s **původním barevným knoflíkovým displejem**. Když je na tiskárně nasazený Creality Nebula Pad, tento balíček na displej nepatří — Nebula má vlastní firmware a špatný soubor displej od tiskárny odpojí.

## Co stáhnout

Oficiální stránka:

https://www.creality.com/download/creality-ender-3-v3-se

Přímý soubor (jediný firmware v sekci Firmware):

https://file2-cdn.creality.com/file/751a1570d23607bd9503f690f7eefcbd/Ender-3%20V3%20SE_HWCR4NS200320C13C14_SWV1.1.0_GD303STM32F401.rar

| Soubor | SHA-256 |
| --- | --- |
| celý `.rar` | `3ea39bbc78b8adb7429a9e0f5c65b60b0e867583692dab6bc6854207dcc38530` |
| `Ender3 V3 SE GD303SWV1.1.0_HWCR4NS200320C13_20250422.bin` | `b6b3276f6217a7f02f2139d849d7ca518408d8edc75457a524afa83c38608a05` |
| `STM32F4_UPDATE/Ender-3V3 SE_HW_CR4NS200141C14_SW_V1.1.0_F401_202504222.bin` | `265440681f1c54b2d82eb39f879f4587767fe5266565f336296e68504d7710da` |
| `TJC_SET/tjc.tft` | `b1285d519ddf26fef386ea8dbf7a91e56b21a8b052caabeae384243f8693ccd0` |

Rozbalení: WinRAR nebo aktuální 7-Zip. Starší 7-Zip soubory z tohoto RAR5 archivu ořeže na nulovou velikost. Po rozbalení zkontroluj, že binární soubory mají stovky kilobajtů a `tjc.tft` asi 7,1 MB.

V archivu jsou tyto věci:

- `屏幕固件/TJC_SET/tjc.tft` — firmware displeje
- `Ender3 V3 SE GD303SWV1.1.0_HWCR4NS200320C13_20250422.bin` — deska **C13** (GD32)
- `STM32F4_UPDATE/Ender-3V3 SE_HW_CR4NS200141C14_SW_V1.1.0_F401_202504222.bin` — deska **C14** (STM32F401)

Názvy nech tak, jak jsou v archivu. V čínském textu uvnitř balíčku je u C13 souboru starší pracovní název; na kartě musí být soubor, který v archivu opravdu leží.

Krátký text od Creality k verzi 1.1.0 říká: rozbalit soubory, dát je na kartu, kartu vložit a tiskárnu restartovat. Přesný postup z návodu uvnitř archivu je níže. Displej se aktualizuje jako první, potom deska. Když se pořadí otočí, displej často zůstane na modré obrazovce, dokud se nenahraje i firmware obrazovky.

## Než začneš

1. Na displeji otevři **Control** a sjeď knoflíkem až na **Info**.
2. Zapiš si **H/W** (končí na `C13` nebo `C14`) a aktuální verzi firmwaru.
3. Když Info už ukazuje **V1.1.0**, další flash není potřeba. Stačí vyrovnání podložky a zkušební tisk.
4. Po aktualizaci zmizí síť vyrovnání a Z-offset. Po flashi se dělá znovu.
5. Během nahrávání tiskárnu nevypínej a nevytahuj kartu.
6. Karta: microSD 8–32 GB. Větší karty a formát exFAT bootloader často ignoruje.
7. Formát **FAT32**, alokační jednotka **4096 bajtů**. Ve Windows: pravé tlačítko na kartu → Formátovat → FAT32 → velikost alokační jednotky 4096. Zámek na boku karty musí být v poloze pro zápis.
8. Na displej patří microSD. Do boku tiskárny patří plná SD, nebo microSD v adaptéru.

## 1. Firmware displeje

1. Naformátuj microSD na FAT32 / 4096.
2. Z rozbaleného archivu zkopíruj na kartu **složku `TJC_SET`**. Uvnitř je jen `tjc.tft`.
3. Na kartě musí být přesně tato cesta:

```text
TJC_SET/tjc.tft
```

Čínskou složku `屏幕固件` na kartu nedávej. Displej hledá `TJC_SET` v kořeni.

4. Tiskárnu vypni.
5. Displej vysuň nahoru z držáku. Na boku displeje je slot microSD. Kartu zasuň **kontakty nahoru**, až zaklapne.
6. Displej nasaď zpět a tiskárnu zapni.
7. Na obrazovce naběhne průběh aktualizace a na konci **Update Successful**. Trvá to obvykle do dvou minut.
8. Tiskárnu vypni, kartu vyndej a složku `TJC_SET` z ní smaž.

## 2. Firmware základní desky

1. Kartu znovu naformátuj na FAT32 / 4096, ať na ní nezůstane firmware displeje.
2. Do **kořene** karty zkopíruj obojí. Oficiální návod v balíčku to tak předepisuje a každá deska si přečte jen svůj soubor:

```text
Ender3 V3 SE GD303SWV1.1.0_HWCR4NS200320C13_20250422.bin
STM32F4_UPDATE/Ender-3V3 SE_HW_CR4NS200141C14_SW_V1.1.0_F401_202504222.bin
```

- Deska **C13** bere `.bin` v kořeni.
- Deska **C14** bere `.bin` uvnitř složky `STM32F4_UPDATE`. Soubor C14 nech v této složce. V názvu je `CR4NS200141` — tak ho Creality pojmenovala, nic v názvu neměň.

3. Tiskárnu nech vypnutou. Kartu vlož do **SD slotu na boku základny**, ne do displeje.
4. Zapni tiskárnu. Modrá obrazovka může svítit déle než při běžném startu, klidně několik desítek sekund. Úspěch je logo Creality a normální menu.
5. Tiskárnu vypni, kartu vyndej a oba firmware soubory z ní smaž. Když `.bin` na kartě zůstane, tiskárna ho při dalším startu načte znovu.

V **Control → Info** má být verze **V1.1.0**.

## 3. Aby tiskárna zase tiskla

Firmware po nahrání nemá uloženou síť podložky ani Z-offset.

1. Nasaď čistou podložku a zkontroluj, že pojezdy nikde nedrhnou.
2. Spusť **Auto Level**. Sonda CR Touch objede podložku. Nech ji dojet až do konce.
3. Nastav **Z-offset**: mezi trysku a podložku dej list kancelářského papíru. Offset snižuj, dokud papír nejde táhnout s lehkým odporem a zároveň se nelepí. Ulož nastavení, když to obrazovka nabídne.
4. Nahřej trysku na 200 °C a podložku na 60 °C. Teploty mají dojít na cíl a držet ho. U PLA je to běžná zkušební teplota.
5. Z SD karty vytiskni malý test, třeba krychli 20 mm. První vrstva má být slitá, bez rytí do podložky a bez mezer mezi linkami.
6. Ve sliceru vyber profil **Ender-3 V3 SE**. Aktuální Creality Print na stejné stránce ke stažení je **V7.2.2.5483** (6. 9. 2026). To je program v počítači, ne firmware tiskárny.

## Když se aktualizace nespustí nebo zůstane modrá obrazovka

1. Vypni tiskárnu a kartu vyndej.
2. Kartu znovu naformátuj na FAT32 s alokační jednotkou 4096. Zkus jinou kartu, ideálně 8 nebo 16 GB.
3. Displej zopakuj jako první: v kořeni jen `TJC_SET/tjc.tft`, karta v displeji, zapnout, počkat na Update Successful, vypnout, kartu vyndat.
4. U desky soubor přejmenuj na krátké jméno, které bootloader spolehlivě přečte:
   - C13: `123.bin` v kořeni karty
   - C14: `123.bin` uvnitř `STM32F4_UPDATE`
5. Kartu dej do slotu na boku tiskárny, zapni a počkej i minutu na logo.
6. Po úspěchu kartu vyndej a `123.bin` smaž.
7. Pořád modrá obrazovka znamená, že displej a deska nemají sadu ze stejného balíčku. Zopakuj nejdřív displej, potom desku, obojí z tohoto V1.1.0.

Oficiální popis modré obrazovky: https://wiki.creality.com/en/ender-series/ender-3-v3-se/troubleshooting/blue-screen-after-firmware-update-or-how-to-determine-if-the-firmware-update-was-successful-or-firmware-upgrade-failure
