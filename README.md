# Creality Ender-3 V3 SE C14 — firmware V1.1.0

Tiskárna má desku **C14** (STM32F401, v Info řádek končící na `C14` / `CR4NS200320C14`). Nejnovější oficiální firmware je **V1.1.0** (soubory z 22. 4. 2025, na webu Creality od 11. 5. 2025). K 26. 9. 2026 Creality novější verzi pro Ender-3 V3 SE neuvádí.

Deska C14 čte firmware jen ze složky **`STM32F4_UPDATE`**. Soubor pro desku C13 (`GD303`, leží v kořeni archivu) na kartu nepatří.

Postup je pro původní knoflíkový displej. U Creality Nebula Pad se firmware displeje z tohoto balíčku nenahrává.

## Co stáhnout

Oficiální stránka:

https://www.creality.com/download/creality-ender-3-v3-se

Přímý soubor:

https://file2-cdn.creality.com/file/751a1570d23607bd9503f690f7eefcbd/Ender-3%20V3%20SE_HWCR4NS200320C13C14_SWV1.1.0_GD303STM32F401.rar

Pro desku C14 a displej stačí tyto dva soubory:

| Soubor | SHA-256 |
| --- | --- |
| celý `.rar` | `3ea39bbc78b8adb7429a9e0f5c65b60b0e867583692dab6bc6854207dcc38530` |
| `STM32F4_UPDATE/Ender-3V3 SE_HW_CR4NS200141C14_SW_V1.1.0_F401_202504222.bin` | `265440681f1c54b2d82eb39f879f4587767fe5266565f336296e68504d7710da` |
| `TJC_SET/tjc.tft` | `b1285d519ddf26fef386ea8dbf7a91e56b21a8b052caabeae384243f8693ccd0` |

Rozbalení: WinRAR nebo aktuální 7-Zip. Starší 7-Zip umí tento RAR5 rozbalit jako prázdné soubory. `tjc.tft` má mít asi 7,1 MB a soubor desky asi 198 KB.

Z archivu se použije:

- `屏幕固件/TJC_SET/tjc.tft` — firmware displeje
- `STM32F4_UPDATE/Ender-3V3 SE_HW_CR4NS200141C14_SW_V1.1.0_F401_202504222.bin` — deska **C14**

V názvu souboru desky je `CR4NS200141`. Tak ho Creality pojmenovala, název se nemění. Soubor zůstane uvnitř složky `STM32F4_UPDATE`.

Nejdřív se nahrává displej, potom deska. Opačné pořadí nechá displej na modré obrazovce, dokud se nenahraje i firmware obrazovky.

## Než začneš

1. V **Control → Info** ověř koncovku **C14** a zapiš si současnou verzi firmwaru.
2. Když Info už ukazuje **V1.1.0**, další flash není potřeba. Stačí vyrovnání podložky a zkušební tisk.
3. Po aktualizaci zmizí síť vyrovnání a Z-offset. Po flashi se dělá znovu.
4. Během nahrávání tiskárnu nevypínej a nevytahuj kartu.
5. Karta: microSD 8–32 GB, formát **FAT32**, alokační jednotka **4096 bajtů**. Ve Windows: pravé tlačítko na kartu → Formátovat → FAT32 → 4096. Zámek na boku karty musí být odemčený.
6. Na displej patří microSD. Do boku tiskárny patří plná SD, nebo microSD v adaptéru.

## 1. Firmware displeje

1. Naformátuj microSD na FAT32 / 4096.
2. Na kartu zkopíruj složku `TJC_SET`. Uvnitř je jen `tjc.tft`.
3. Na kartě musí být přesně tato cesta:

```text
TJC_SET/tjc.tft
```

Čínskou složku `屏幕固件` na kartu nedávej. Displej hledá `TJC_SET` v kořeni.

4. Tiskárnu vypni.
5. Displej vysuň nahoru z držáku. Na boku displeje je slot microSD. Kartu zasuň kontakty nahoru, až zaklapne.
6. Displej nasaď zpět a tiskárnu zapni.
7. Na obrazovce naběhne průběh aktualizace a na konci **Update Successful**. Trvá to obvykle do dvou minut.
8. Tiskárnu vypni, kartu vyndej a složku `TJC_SET` smaž.

## 2. Firmware desky C14

1. Kartu znovu naformátuj na FAT32 / 4096.
2. Do kořene karty zkopíruj celou složku `STM32F4_UPDATE` i se souborem uvnitř. V kořeni karty žádný jiný `.bin` není.

```text
STM32F4_UPDATE/Ender-3V3 SE_HW_CR4NS200141C14_SW_V1.1.0_F401_202504222.bin
```

Soubor s `GD303` a `C13` v názvu na kartu nekopíruj. Deska C14 ho nepoužívá a soubor v kořeni u ní aktualizaci nespustí.

3. Tiskárnu nech vypnutou. Kartu vlož do SD slotu na boku základny, ne do displeje.
4. Zapni tiskárnu. Modrá obrazovka může svítit déle než při běžném startu, klidně několik desítek sekund. Úspěch je logo Creality a normální menu.
5. Tiskárnu vypni, kartu vyndej a složku `STM32F4_UPDATE` smaž. Když `.bin` na kartě zůstane, tiskárna ho při dalším startu načte znovu.

V **Control → Info** má být verze **V1.1.0** a hardware pořád **C14**.

## 3. Aby tiskárna zase tiskla

Firmware po nahrání nemá uloženou síť podložky ani Z-offset.

1. Nasaď čistou podložku a zkontroluj, že pojezdy nikde nedrhnou.
2. Spusť **Auto Level**. Sonda CR Touch objede podložku. Nech ji dojet až do konce.
3. Nastav **Z-offset**: mezi trysku a podložku dej list kancelářského papíru. Offset snižuj, dokud papír jde táhnout s lehkým odporem. Ulož nastavení, když to obrazovka nabídne.
4. Nahřej trysku na 200 °C a podložku na 60 °C. U PLA je to běžná zkušební teplota.
5. Z SD karty vytiskni malý test, třeba krychli 20 mm. První vrstva má být slitá, bez rytí do podložky a bez mezer mezi linkami.
6. Ve sliceru vyber profil **Ender-3 V3 SE**. Aktuální Creality Print na stejné stránce ke stažení je **V7.2.2.5483** (6. 9. 2026). To je program v počítači, ne firmware tiskárny.

## Když se aktualizace nespustí nebo zůstane modrá obrazovka

1. Vypni tiskárnu a kartu vyndej.
2. Kartu znovu naformátuj na FAT32 s alokační jednotkou 4096. Zkus jinou kartu, ideálně 8 nebo 16 GB.
3. Displej zopakuj jako první: v kořeni jen `TJC_SET/tjc.tft`, karta v displeji, zapnout, počkat na Update Successful, vypnout, kartu vyndat.
4. Soubor desky přejmenuj na `123.bin` a nech ho **uvnitř** `STM32F4_UPDATE`:

```text
STM32F4_UPDATE/123.bin
```

5. Kartu dej do slotu na boku tiskárny, zapni a počkej i minutu na logo.
6. Po úspěchu kartu vyndej a `123.bin` smaž.
7. Pořád modrá obrazovka znamená, že displej a deska nemají sadu ze stejného balíčku. Zopakuj nejdřív displej, potom desku C14, obojí z tohoto V1.1.0.

Oficiální popis modré obrazovky: https://wiki.creality.com/en/ender-series/ender-3-v3-se/troubleshooting/blue-screen-after-firmware-update-or-how-to-determine-if-the-firmware-update-was-successful-or-firmware-upgrade-failure
