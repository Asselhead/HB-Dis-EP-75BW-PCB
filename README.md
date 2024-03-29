# HB-Dis-EP-75BW-PCB
Homematic Homebrew Leiterplatte für 7,5" (und andere) ePaper Displays

Es handelt sich hierbei um eine Leiterplatte, die den direkten Anschluss eines 7,5" ePaper Display (und ähnliche) ermöglicht.
Die sonst üblichen HAT oder Driver Leiterplatten können entfallen.
Die Schaltung orientiert sich an der Schaltung für das 4,2" Display: https://github.com/jp112sdl/HB-Dis-EP-42BW

![TOP_ISO.png](https://github.com/Asselhead/HB-Dis-EP-75BW-PCB/blob/master/TOP_ISO.png)

12 GPIOs wurden an den Rand der Leiterplatte gelegt, damit man hier z.B. bis zu 12 Taster (auch Touch-Taster) anschließen kann.
Softwareseitig sind jedoch aktuell nur 10 Taster vorgesehen (Siehe Link zum 4.2" Projekt).

![BOT.png](https://github.com/Asselhead/HB-Dis-EP-75BW-PCB/blob/master/BOT.png)

Aus Platzgründen wurden die Beschriftungen auf die BOT Seite der Leiterplatte gelegt.

Die Leiterplatte hat die Maße 50x50mm, der Durchmesser der Befestigungslöcher beträgt 3,2mm.

Zum Schutz vor einem "Babbling Idiot" wurde auch hier (u.a.) ein Reset Baustein vorgesehen, dessen Pinbelegung stimmt jedoch nicht mit dem in der 4.2" Schaltung überein.
Eine mögliche Type wäre von ON Semiconductor der NCP803SN232T1G mit einer Reset Schwelle von 2,32V.

Wer z.B. einen LiPo Akku als Spannungsquelle einsetzen möchte, sollte eher einen Reset Bausteine mit einer Schwelle von 2,63V oder 2,93V einsetzen.

Alle weiteren benötigten Bauteile sind (auch mit Link) im Schaltplan hinterlegt. Auch der Link zum Reichelt Warenkorb kann im PDF angeklickt werden.

Die Bauteilbezeichnungen in der Schaltung stimmen nicht immer mit den Angaben in der Stückliste überein, da ich auf eine bestehende Bauteilbibliothek zurückgreife.
Maßgeblich sind aber die Angaben in der Stückliste.

### Lötbrücke

~~Die Lötbrücke sollte in der Regel nach 4-Wire geschlossen werden!~~
Die Lötbrücke ist in Version 1.0 der Leiterplatte bereits mit einer kleinen Leiterbahn nach 4-Wire geschlossen.
Wer hier 3-Wire verwenden möchte, muss die Leiterbahn aufkratzen und die Lötbrücke entsprechend schließen.

## Thread im Homematic Forum

[Vorstellung Leiterplatte für ePaper Displays (z.B. 7,5") inkl. Driver](https://homematic-forum.de/forum/viewtopic.php?f=76&t=60213#p596751)

## Sketch

Als Sketch sollte zunächst der [4.2" Sketch](https://github.com/jp112sdl/HB-Dis-EP-42BW/blob/master/HB-Dis-EP-42BW.ino) verwendet werden.
Alle Signale zum Display, zum CC1101 Modul und den LEDs sind von der 4.2" Schaltung übernommen worden. Bei den Tastern stimmt das auch weitgehend überein, die Unterschiede (12 statt 10 Button) sollten noch einmal in der Schaltung geprüft und im Sketch nach eigenen Wünschen angepasst werden.

Auch die Bootloader Einstellungen sollten vom 4.2" Projekt übernommen werden.

## Gerber Daten
Wer die Leiterplatte z.B. bei JLCPCB in Auftrag geben möchte, kann sich hier die Gerberdaten herunterladen:
[Gerber](https://github.com/Asselhead/HB-Dis-EP-75BW-PCB/blob/master/Gerber/ePaperV1.zip)

Es handelt sich um eine 4-Lagen Leiterplatte. 

## Pick&Place + BOM Daten für die Bestellung einer (Teil-) Bestückten Leiterplatte
JLCPCB bietet auch die Möglichkeit Leiterplatten bestücken zu lassen.
Nicht immer sind alle Bauteile verfügbar und für "Extended" Parts wird eine extra Gebühr fällig.
Wie so eine Bestellung abläuft kann man sich hier anschauen:
[Anleitung](https://github.com/Asselhead/Bestellanleitung-JLCPCB-SMT-Service)

Wer möglichst wenig selber löten möchte, sollte bei der Bestellung folgende BOM (Bill of Material) verwenden:

[BOM inkl. MCU, Taster, Drossel, Resonator](https://github.com/Asselhead/HB-Dis-EP-75BW-PCB/blob/master/Gerber/JLCSMT_BOM_HB-Dis-EP-75-PCB_FULL.xlsx)

Wer Drossel, MCU, Resonator und Taster selber löten kann, spart einiges an Geld, denn folgende BOM beinhaltet nur Basic Parts (ausser der Display Buchse):

[Basic BOM](https://github.com/Asselhead/HB-Dis-EP-75BW-PCB/blob/master/Gerber/JLCSMT_BOM_HB-Dis-EP-75-PCB_Basic_Disp_Conn.xlsx)

Wichtig! Die Basic BOM enthält für R5 anstelle eines 0,47 Ohm Widerstand einen 1 Ohm Widerstand.
Falls es damit nicht funktioniert muss ein weiterer 1 Ohm Widerstand auf R5 Huckepack gelötet werden (ergibt 0,5 Ohm).
Wichtig! Der Spannungsregler IC5 darf am Eingang mit maximal 6V versorgt werden - er weicht von dem in der Schaltung bzw. Reichelt BOM ab.

So sieht das bestückt aus:

![PartsPlacementBasic.png](https://github.com/Asselhead/HB-Dis-EP-75BW-PCB/blob/master/Gerber/PartsPlacementBasic.png)

Damit die Bauteile an der korrekten Stelle platziert werden, benötigt man noch folgende Pick&Place (CPL) Datei:

[Pick&Place](https://github.com/Asselhead/HB-Dis-EP-75BW-PCB/blob/master/Gerber/Pick_Place_HB-Dis_EP-75BW-PCB.xlsx)

Bei der Bestellung bei JLCPCB folge Reihenfolge einhalten:

1. ZIP Datei mit Gerberdaten hochladen
2. Leiterplattendicke wählen (habe selbst 1mm genommen - ist Minimum)
3. Layer Stackup im Dropdown Menü auswählen (L1=GTL, L2=G1, L3=G2, L4=GBL)
4. STM Assembly anwählen -> Top Side 5 Stück (kostet fast das selbe wie 2 Stück) -> Confirm
5. Add BOM File -> z.B. JLCSMT_BOM_HB-Dis-EP-75-PCB_Basic_Disp_Conn.xlsx hochladen
6. Add CPL File -> Pick_Place_HB-Dis_EP-75BW-PCB.xlsx hochladen -> Next
7. Bauteile noch einmal checken und ggf. Bauteile abwählen, die man nicht bestückten lassen möchte -> Next
8. Sichtkontrolle der Bauteile auf der Leiterplatte und ab in den Warenkorb
9. Als Versandmethode empfehle ich EuroPacket - im Bezahlvorgang daran denken einen der Coupons zu nutzen (7,87€ Discount)
10. Auf diese Weise bezahlt man aktuell (Stand 10.02.2022) rund 23€ für 5 bestückte Leiterplatten (ohne MCU usw. - siehe oben)

Zur Info: Ich selbst habe mit der BOM und Pick&Place Datei noch keine bestückten Display-Leiterplatten bestellt. Ich stelle die Daten hier nach bestem Wissen und Gewissen zur Verfügung, kann aber keine Haftung übernehmen, falls JLCPCB etwas falsches bestückt.

Danke auch an Marc (Rundll32) der mir etwas Arbeit bei der BOM abgenommen hat!


## Gefällt Dir die Leiterplatte? Dann freue ich mich über einen Kaffee:

[![ko-fi](https://www.ko-fi.com/img/githubbutton_sm.svg)](https://ko-fi.com/L3L52JYN0)

## Schaltung und Stückliste
[Schaltung](https://github.com/Asselhead/HB-Dis-EP-75BW-PCB/blob/master/Schematic_HB-Dis-EP-75BW-PCB.pdf)

**Achtung!** In den Unterlagen wird R14 noch als 0603 Widerstand mit 22 Ohm angegeben. Dieser wurde ab Leiterplatte Version 1.0 auf die Bauform 0805 geändert. Die Reichelt Stückliste wurde angepasst, die Bestückungsunterlagen und die Schaltung aber noch nicht. Bitte beachten!

## Bestückungsunterlagen und Stückliste 

[Bestückungsunterlagen](https://github.com/Asselhead/HB-Dis-EP-75BW-PCB/blob/master/Assembly_HB-Dis-EP-75BW-PCB.pdf)

## Reichelt Warenkorb

[Warenkorb](https://www.reichelt.de/my/1742358)

## Lizenz

![by-nc-sa.eu.png](https://github.com/Asselhead/HB-Dis-EP-75BW-PCB/blob/master/by-nc-sa.eu.png)

## Mögliche Bezugsquellen für das 7,5" Display (Lieferfähigkeit variiert):

***Auflösung 800x480 Pixel:***

Deutschland:

[Amazon](https://www.amazon.de/Waveshare-Resolution-Electronic-Controller-Communicating/dp/B075R69T93?ref_=ast_sto_dp)
 
Version mit HAT: [Amazon](https://www.amazon.de/HAT-Resolution-Electronic-Controller-Communicating/dp/B075R4QY3L?ref_=ast_sto_dp)

Ebenfalls mit HAT: [Reichelt](https://www.reichelt.de/entwicklerboards-display-epaper-7-5-schwarz-weiss-debo-epa-7-5-p253956.html?&nbc=1)

[Eckstein](https://eckstein-shop.de/Waveshare-800480-75inch-E-Ink-Raw-Display-SPI-interface-Arduino)

**China:**

[Aliexpress](https://de.aliexpress.com/item/32832484087.html?spm=a2g0x.12057483.0.0.48a129e5z26zGS)

[Banggood](https://de.banggood.com/Waveshare-7_5-Inch-Ink-Screen-Bare-Screen-E-paper-Display-SPI-Interface-BlackandWhite-800x480-Resolution-p-1707059.html?rmmds=search&cur_warehouse=CN)

***Auflösung 640x384:***

Deutschland:

[Exp-Tech](https://www.exp-tech.de/displays/e-paper-e-ink/8697/640x384-7.5inch-e-ink-raw-display?c=1424)
