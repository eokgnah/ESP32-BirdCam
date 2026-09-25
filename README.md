# BirdCam Web Flasher

Statische GitHub-Pages-Seite für BirdCam v0.4.6.5 mit ESP Web Tools.

## Dateien ins Repository kopieren

```text
/
  index.html
  manifest-update.json
  manifest-initial.json
  firmware/
    BirdCam_ESP32_v0.4.6.5.ino.bin
    BirdCam_ESP32_v0.4.6.5.ino.merged.bin
```

Die beiden BIN-Dateien stammen aus dem Arduino-Build-Verzeichnis.

## GitHub Pages

Repository auf GitHub anlegen/hochladen und unter **Settings → Pages** die Veröffentlichung aus dem gewünschten Branch (typisch `main`, `/root`) aktivieren. Danach die von GitHub angezeigte HTTPS-Adresse öffnen.

## Flash-Modi

### Update

`manifest-update.json` schreibt die normale `ino.bin` in beide App-Partitionen des BirdCam-Dual-OTA-Layouts:

- app0: `0x10000` (65536)
- app1: `0x1F0000` (2031616)

Das ist absichtlich BirdCam-spezifisch und setzt die bisher verwendete `partitions.csv` voraus. Es ersetzt weder Bootloader noch Partitionstabelle.

ESP Web Tools kann bei einer nicht erkannten Firmware einen Installationsdialog anzeigen. Beim Update **keinen Full-Erase wählen**, wenn Einstellungen erhalten bleiben sollen.

### Initialinstallation

`manifest-initial.json` schreibt `BirdCam_ESP32_v0.4.6.5.ino.merged.bin` ab Offset `0x0`. Dieses Arduino-Build-Artefakt enthält Bootloader, Partitionstabelle, boot_app0 und die Anwendung in einem zusammengeführten Image.

Eine Initialinstallation ist für einen neuen/neu aufzubauenden ESP gedacht und kann vorhandene Flash-Daten löschen.

## Voraussetzungen

- HTTPS (GitHub Pages erfüllt das)
- Desktop-Browser mit Web Serial
- ESP32-CAM über USB-Seriell-Adapter im Download-/Bootloader-Modus, falls das Board keinen eigenen USB-UART besitzt

## Neue BirdCam-Version veröffentlichen

Bei einer neuen Version die beiden BIN-Dateien im Ordner `firmware/` ersetzen und Dateinamen sowie `version` in beiden Manifesten und `index.html` anpassen.
