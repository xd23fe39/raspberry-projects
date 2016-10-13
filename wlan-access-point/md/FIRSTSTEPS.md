[0]: README.md


Raspberry PI - Erste Schritte
====================================

Von Frank

Dieses Dokument ist Teil von [WLAN Access Point using Raspberry PI][0].

***

Erste Schritte
--------------

Anmelden als Benutzer `pi` am RaspberryPi `raspberry`. Dieser sollte zunächst über ein LAN-Kabel an das Heimnetzwerk angebunden sein.

|Begriff                 |Erklärung oder Verwendung
|------------------------|--------------------------------------------------|
|Benutzername            |pi
|Hostname                |raspberry

> Benutzername und Hostname weichen ggf. von den hier beschriebenen ab und sind durch die in Ihrem Heimnetzwerk geltenden Daten zu ersetzen.

```shell
# SecureShell zu entferntem System öffnen
ssh pi@raspberry
```

Das Standard-Kennwort lautet `raspberry`. Es sollte unmittelbar nach der Installation auf ein persönliches Kennwort geändert werden.

```shell
# System von RaspberryPi aktualisieren
 sudo apt update
 sudo apt upgrade
```

> Das Ausführen einer Systemaktualisierung dauert je nach Internetverbindung eine Weile. Auch, wenn das Warten lästig sein kann, sollte dieser Schritt ausgeführt werden.

Anschließend muss der RaspberryPI neu gestartet werden (reboot):

```shell
# System rebooten
sudo reboot
```

Dabei verliert man die aktuelle Verbindung (SSH-Session) zum RaspberryPI. Nach einer kurzen Wartezeit kann man sich erneut via `ssh` mit `raspberry` verbinden.
