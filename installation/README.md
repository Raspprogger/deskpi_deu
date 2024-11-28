# HINWEIS:
## Zur Auswahl des Betriebssystems
Bitte wählen Sie das richtige Betriebssystem und die Plattformarchitektur für die Installation aus.

> **Hinweis:** Die Unterstützung für 32-Bit-Systeme wurde eingestellt; Verwenden Sie ein 64-Bit-System, um die Leistung des Raspberry Pi voll auszuschöpfen.

> Außerdem wird aufgrund der hardwarebasierten Optimierungen des offiziellen Betriebssystems für den Raspberry Pi dringend empfohlen, das Raspberry Pi OS zu verwenden.

---

## Die aktuelle Verzeichnisstruktur ist wie folgt:

```plaintext
.
├── deskpi-config
├── DietPi
│   ├── install-dietPi-64bit.sh
│   └── uninstall-dietPi-64bit.sh
├── drivers
│   ├── c
│   │   ├── Makefile
│   │   ├── pwmFanControl64
│   │   ├── pwmFanControl.c
│   │   ├── safeCutOffPower64
│   │   └── safeCutOffPower.c
│   ├── deskpi-config
│   ├── Deskpi-uninstall
│   ├── python
│   │   ├── pwmControlFan.py
│   │   └── safecutoffpower.py
│   └── README.md
├── Fedora
│   ├── install-fedora.sh
│   ├── README.md
│   └── uninstall-fedora.sh
├── Kali
│   ├── install-kali.sh
│   └── uninstall-kali.sh
├── Manjaro
│   ├── install-manjaro.sh
│   └── uninstall-manjaro.sh
├── RaspberryPiOS
│   └── 64bit
│       ├── install-raspios-64bit.sh
│       └── uninstall-raspios-64bit.sh
├── README.md
├── Ubuntu
│   ├── install-ubuntu-64.sh
│   └── uninstall-ubuntu-mate.sh
└── uninstall.sh
```

---

## Skripte ausführen

### So führen Sie die Installations- und Deinstallationsskripte aus:

1. Öffnen Sie ein Terminal.
2. Navigieren Sie in das Verzeichnis, in dem sich das gewünschte Skript befindet.
3. Machen Sie das Skript ausführbar (falls dies nicht bereits der Fall ist):

    ```bash
    chmod +x install-<OS>-64bit.sh
    ```

4. Führen Sie das Skript aus:

    ```bash
    ./install-<OS>-64bit.sh
    ```

Ersetzen Sie `<OS>` durch den Namen des Betriebssystems, das Sie installieren möchten (z. B. `dietPi`, `fedora`, `ubuntu`, etc.).

---

## Unterstützung erhalten
Falls Sie Probleme bei der Nutzung unseres Produkts haben, senden Sie bitte eine E-Mail an: [support@deskpi.com](mailto:support@deskpi.com)



