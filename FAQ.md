# FAQ 
## Über USB-Boot, was ist UASP?
* Ohne UASP wird ein Laufwerk als Massenspeichergerät mit Bulk Only Transport (oder BOT) eingebunden, einem Protokoll, das für die Datenübertragung in den Tagen von USB "Full Speed" entwickelt wurde, als die maximale Geschwindigkeit nur 12 Mbps betrug!
* Mit USB 3.0 begrenzt das BOT-Protokoll den Datendurchsatz erheblich. USB 3.0 bietet 5 Gbps Bandbreite, was 400-mal mehr ist als bei USB 1.1. Das alte BOT-Protokoll übertrug Daten in großen Blöcken, wobei jeder Block der Reihe nach übertragen werden musste, ohne Berücksichtigung von Pufferung oder paralleler Datenübertragung.
* Daher wurde ein neues Protokoll entwickelt, das 'USB Attached SCSI Protocol' oder kurz 'UASP' genannt wird.
 
## Wie kann ich überprüfen, ob mein Laufwerk UASP unterstützt?
* Wenn Sie ein USB-Laufwerk haben und es nicht auseinanderbauen möchten, um die Spezifikationen des Controller-Chips nachzuschlagen, können Sie nur durch den folgenden Befehl feststellen, ob es mit UASP-Unterstützung eingebunden wird oder nicht. Schließen Sie das Laufwerk an Ihren Pi an und führen Sie den Befehl `lsusb -t` aus:
```bash
$ lsusb -t
/:  Bus 02.Port 1: Dev 1, Class=root_hub, Driver=xhci_hcd/4p, 5000M
    |__ Port 1: Dev 2, If 0, Class=Mass Storage, Driver=uas, 5000M
```
Dieser Befehl listet alle USB-Geräte in einer Baumstruktur auf, und für jedes Laufwerk wird ein Treiber angegeben. Wenn dort `uas` (wie im obigen Beispiel) steht, unterstützt Ihr Laufwerk UASP und Sie erhalten die beste Geschwindigkeit. Wenn dort `usb-storage` steht, verwendet es das ältere BOT-Protokoll und Sie werden nicht das volle Potenzial sehen.

## Warum dreht sich mein Lüfter nicht, wenn das System im Leerlauf ist? 
* Standardmäßig passt der Lüftertreiber von DeskPi die Geschwindigkeit entsprechend der aktuellen CPU-Temperatur an. Wenn die aktuelle Temperatur unter der Lüfterrotation-Schwelle liegt, stoppt der Lüfter automatisch. Wenn Sie möchten, dass der Lüfter mit einer bestimmten Geschwindigkeit läuft, öffnen Sie ein Terminal und führen Sie den Befehl `deskpi-config` aus. Wählen Sie den entsprechenden Betriebsmodus gemäß den Anweisungen.

## Wie lauten Benutzername und das Passwort des vorinstallierten Raspbian OS?
* Der Benutzername des vorinstallierten Raspbian OS ist `pi` und das Passwort ist `raspberry`. Diese Daten sind die Originalwerte von Raspbian; wir haben sie nicht verändert, als wir das Image verteilt haben.

## Warum sind die Einstellungen dieses vorinstallierten Raspbian-OS-Images auf China voreingestellt?
* Dieses vorinstallierte Raspbian-OS-Image basiert auf Raspbian OS Buster (Version: 2020-08-20). Beim Initialisieren des OS und dem Versuch, eine Verbindung zum Internet herzustellen, um den DeskPi-Treiber von github.com herunterzuladen, müssen wir das Wi-Fi-Land vor dem Aktivieren der Wi-Fi-Adapter einstellen. Da dieses Produkt weltweit verkauft wird, können wir nicht erkennen, in welchem Land oder welcher Region sich unser Kunde befindet. Daher ist die Standardeinstellung Shanghai, China. Sie können das Wi-Fi-Land jedoch ganz einfach ändern, indem Sie den folgenden Befehl im Terminal ausführen: `sudo raspi-config` und dann die Lokalisierungsoptionen auswählen, um Sprache und Region zu konfigurieren.

## Der USB-Anschluss auf der Frontplatte funktioniert nicht.
* Dies liegt daran, dass in der Datei `/boot/config.txt` keine Konfiguration vorhanden ist. Sie müssen die folgende Konfiguration zu dieser Datei hinzufügen: `dtoverlay=dwc2,dr_mode=host` und den Raspberry Pi neu starten. Wenn Sie den DeskPi-Treiber installiert haben, wird diese Konfiguration automatisch hinzugefügt.

## Kann ich den Computernamen im vorinstallierten Raspbian OS ändern?
* Ja, natürlich. Geben Sie `sudo raspi-config` ein, wählen Sie Systemoptionen (Punkt 1) und navigieren Sie zu `S4 Hostname`, um den Hostnamen zu konfigurieren. Alternativ können Sie den Befehl `sudo hostnamectl set-hostname IHRHOSTNAMEHIER` verwenden, um den Hostnamen über die Befehlszeile einzustellen.

## Wie kann ich überprüfen, ob mein Laufwerk UASP unterstützt?
* Öffnen Sie ein Terminal und geben Sie den Befehl ein: `lsusb -t |grep -i "uas"` und drücken Sie Enter.

## Wie installiere ich den DeskPi-Lüftertreiber, nachdem ich meine TF-Karte neu geflasht habe?
* Stellen Sie sicher, dass Ihr Betriebssystem auf der Liste der unterstützten Betriebssysteme steht.
* Stellen Sie sicher, dass Ihr Raspberry Pi Zugriff auf das Internet hat.
* Klonen Sie das Repository mit: `git clone https://github.com/DeskPi-Team/deskpi.git`
* Geben Sie die folgenden Befehle in ein Terminal ein:
```bash
cd ~/deskpi/
chmod +x install.sh
sudo ./install.sh
```

## Wo finde ich die Liste der unterstützten Betriebssysteme ?
* Besuchen Sie einfach: https://github.com/DeskPi-Team/deskpi
