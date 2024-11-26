# Über DeskPi Pro

Das DeskPi Pro ist ein Hardware-Kit, das einen Standard-Raspberry Pi 4 von einem einfachen Einplatinencomputer (SBC) mit begrenztem Speicherplatz in einen Mini-PC verwandelt. Es bietet einen Netzschalter, Kühlung, bessere Anschlüsse und Speicheroptionen (2,5"- oder M.2-SSD) über SATA und USB 3.

## YouTube-Tutorial

[Youtube video](https://youtu.be/eaXC5O3amfA)

## Derzeit getestete Betriebssysteme, die DeskPi-Skripte unterstützen:
* Raspberry Pi OS (32-Bit) - Veraltet  
* RaspiOS (64-Bit) - Getestet  
* Ubuntu-mate OS (32-Bit) - Veraltet  
* Ubuntu OS (64-Bit) - In Prüfung (Version 24.04) – Nicht mehr unterstützt. `dtoverlay=dwc2,dr_mode=host` funktioniert nicht richtig.  
* Manjaro OS (32-Bit) - Veraltet  
* Manjaro OS (64-Bit) - Getestet  
* Kali-linux-arm OS (32-Bit) - Veraltet  
* Kali-linux-arm OS (64-Bit) - Veraltet  
* Twister OS v2.0.2 (32-Bit) - Veraltet  
* DietPi OS (64-Bit) - Getestet  
* Volumio OS Version: 2021-04-24-Pi (32-Bit) - Getestet  
* RetroPie OS (32-Bit) - Getestet  
* Windows 10 IoT - Nicht unterstützt  
* Windows 11 - Nicht unterstützt

## Bitte diesen Abschnitt sorgfältig lesen:
* Wenn Sie ein 64-Bit-Betriebssystem verwenden, finden Sie das Skript zur Steuerung des Lüfters im Verzeichnis `installation/drivers/c/`. Dateien mit der Endung `64` sind für 64-Bit-Systeme. Die ausführbaren Dateien für 32-Bit-Systeme wurden entfernt. Wenn Sie 32-Bit verwenden möchten, laden Sie das Repository herunter und kompilieren Sie die Dateien selbst. 

* Stellen Sie sicher, dass Ihr Raspberry Pi eine Internetverbindung hat und Zugriff auf die GitHub-Website besteht, bevor Sie das Skript installieren.

## So installieren Sie das Skript:
* 1. Laden Sie das Repository herunter.  
* 2. Wechseln Sie in das Verzeichnis `installation`.  
* 3. Wählen Sie Ihren Betriebssystemtyp aus.  
* 4. Führen Sie das Shell-Skript im entsprechenden Ordner aus.

**Beispiel:**

### Für Raspbian OS 64bit (bookworm)
```bash 
git clone https://github.com/DeskPi-Team/deskpi.git 
cd ~/deskpi/installation/RaspberryPiOS/64bit/
sudo ./install-raspios-64bit.sh 
```

### Für Volumio OS Version: 2021-04-24-Pi
* Image Download URL: https://updates.volumio.org/pi/volumio/2.882/volumio-2.882-2021-04-24-pi.img.zip
* Schnellstart-Anleitung:　https://volumio.github.io/docs/User_Manual/Quick_Start_Guide.html
* Stellen Sie sicher, dass Volumio eine Internetverbindung hat. 
* Es müssen einige Schritte ausgeführt werden.
```
sudo nano /etc/network/interface
```
Stellen Sie sicher, dass die Datei „/etc/network/interface“ folgende Parameter enthält: 
```
auto wlan0 
allow-hotplug wlan0 
iface wlan0 inet dhcp
wpa-ssid "IHR_WIFI_SSID"
wpa-psk "IHR_WIFI_PASSWORT"
```
Aktivieren Sie den Internetzugriff, indem Sie diesen Befehl im Terminal eingeben:
```
volumio internet on
```
Starten Sie dann das DeskPi neu:
```
sudo reboot
```

###Lüftergeschwindigkeit manuell einstellen
* Öffnen Sie ein Terminal und geben Sie ein: 
```
deskpi-config
```
Wählen Sie `4` und drücken Sie `Enter`, um den Lüfter zu aktivieren und die Front-USB-Anschlüsse verfügbar zu machen.

> HINWEIS: Sobald Sie den Befehl `deskpi-config` ausführen, wird der Dienst `deskpi.service` im Hintergrund gestoppt.

> Sie müssen den folgenden Befehl ausführen, um ihn wieder zu aktivieren:
```bash
sudo systemctl restart deskpi.service
```
 
> Wenn sich der `deskpi.service`-Dienst im gestoppten Zustand befindet, wird die Konfiguration aus der Datei `/etc/deskpi.conf` nicht gelesen, um den Lüfter zu steuern.
 
> Daher sollten Sie sicherstellen, dass der Dienst `deskpi.service` immer im Hintergrund läuft, insbesondere nachdem Sie den Befehl `deskpi-config` ausgeführt haben. Sie müssen den Dienst manuell neu starten, indem Sie den folgenden Befehl in einem Terminal ausführen:
```bash
sudo systemctl restart deskpi.service
```
 

## Wie man die Lüftergeschwindigkeit manuell steuert.
* Öffnen Sie ein Terminal und geben Sie folgenden Befehl ein:
```bash
deskpi-config
```
Sie können den Anweisungen folgen, um die Lüftergeschwindigkeit durch Eingabe von Zahlen wie im 
folgenden Beispiel einzustellen:
### Erklärung der Auswahlmöglichkeiten
* Die Zahlen 1 bis 4 dienen dazu, die Lüftergeschwindigkeit auf einen statischen Wert einzustellen.
* Nummer 5 schaltet den Lüfter einfach aus.
* Nummer 6 führt Sie durch die Erstellung einer Datei unter `/etc/deskpi.conf`, 
in der Sie die Temperaturschwellen und Lüftergeschwindigkeiten nach Ihren Wünschen 
festlegen können. Sobald die Datei erstellt ist, richtet das Programm den Lüfter 
gemäß der Konfigurationsdatei ein.
* Nummer 7 aktiviert die automatische Lüftersteuerung mit den Standardparametern. 

**Standardwerte:**  
```
TEMP   : Fan_SPEED_LEVEL
<40C   : 0%  
40~50C : 25%  
50~65C : 50%  
65~75C : 75%  
>75C   : 100%  
```
![Bespiel](https://raw.githubusercontent.com/DeskPi-Team/deskpi/master/imgs/deskpi-config-snap.jpg)
** Falls Sie die Werte ändern möchten, geben Sie einfach folgendes ein:**
```
deskpi-config
```
Wählen Sie `6`, geben Sie dann `45` ein und drücken Sie Enter, anschließend geben Sie `50` ein. Dies bedeutet, dass die Lüftergeschwindigkeit auf `50%` eingestellt wird, wenn die CPU-Temperatur 45 Grad überschreitet. Es gibt 4 Stufen, die eingerichtet werden können.

> **HINWEIS:** Die Einstellung der Lüftergeschwindigkeit auf 50% bedeutet, dass Sie bereits `PWM50` an den Port `/dev/ttyUSB0` gesendet haben. Dieser Port wird verfügbar, wenn Sie `dtoverlay=dwc2,dr_mode=host` in die Datei `/boot/firmware/config.txt` einfügen und Ihr DeskPi neu starten. 


## Wie bootet man von einer USB-SSD/HDD?
Nach der anfänglichen Konfiguration des Raspberry Pi und sobald eine Internetverbindung hergestellt wurde, installieren Sie die DeskPi Pro Utilities aus `https://github.com/DeskPi-Team/deskpi.git`.
Öffnen Sie ein Terminal / Konsole und führen Sie die folgenden Befehle aus:  
```bash 
sudo apt update
sudo apt full-upgrade
sudo rpi-update
```
Nach Abschluss führen Sie aus:
```bash
sudo reboot
```
Nach dem Neustart öffnen Sie das Terminal erneut:
```bash
sudo raspi-config
```
* Gehen Sie zu „Advanced Options“ (Erweiterte Optionen). 
* Wählen Sie „Boot Order“ und setzen Sie `USB Boot` als #1. Gehen Sie zurück zu „Advanced Options“.
* Wählen Sie „Boot Loader Version“ und setzen Sie diese auf „Latest Version“.
* Speichern und verlassen.

### Erneut neustarten (um die neuen Einstellungen zu übernehmen)
```bash
sudo reboot 
```
Nach dem Neustart öffnen Sie das Terminal erneut
```bash
sudo -E rpi-eeprom-config --edit
```
•	Ändern Sie nichts, das ist nicht notwendig.
•	Drücken Sie `Ctrl-X`, um zu speichern, und bestätigen Sie mit `Y`, um die Datei zu überschreiben.
```bash
sudo reboot    
```
Jetzt können Sie Raspberry-OS auf Ihrem USB-Boot-Gerät installieren.
Sie können den Raspberry Imager von der Webseite `www.raspberrypi.org` verwenden. 
Abhängig vom Gerät kann der neue SD-Karten-Kopierer das SD-Karten-Image auf das USB-Gerät übertragen (stellen Sie sicher, dass Sie „generate a new UUID“ auswählen). 
Sobald Ihr USB-Laufwerk mit dem Image beschrieben und startbereit ist, fahren Sie Ihr DeskPi Pro herunter, entfernen Sie die SD-Karte und starten Sie mit dem USB-Boot-Gerät. Sobald das System läuft und konfiguriert ist, können Sie Ihre zusätzliche Software installieren und wie gewohnt fortfahren. 
<br>
* Tutorial-Video: https://youtu.be/wUHZb9E_WDQ  <br>

## So verwenden Sie die integrierte IR-Funktion.
1. Aktivieren Sie gpio-ir in /boot/config.txt:
```bash
dtoverlay=gpio-ir,gpio_pin=17 
```
2. Installieren Sie das Paket `lirc`:
```bash
sudo apt-get install lirc
```
3. Ändern Sie die Konfigurationsdatei am Speicherort: /etc/lirc/lirc_options.conf und stellen Sie sicher, dass sie die folgenden Parameter enthält:
```bash
driver          = default
device          = /dev/lirc0
```
4. Starten Sie Ihren Raspberry Pi neu und testen Sie ihn mit dem folgenden Befehl:
```bash
mode2 -d /dev/lirc1
```
## LOGO
![LOGO](https://raw.githubusercontent.com/DeskPi-Team/deskpi/master/imgs/deskpilogo1.png)
