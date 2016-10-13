[0]: README.md

[Q01]: https://wiki.archlinux.org/index.php/Dhcpcd
[Q02]: https://wiki.archlinux.org/index.php?title=Core_utilities

Installation
====================================

Von [Frank](mailto:xd23fe39@yahoo.de)

Dieses Dokument ist Teil von [WLAN Access Point using Raspberry PI][0].

***

Zusammenfassung der Installationsschritte
------------------------------------------

Der Installationsablauf besteht aus folgenden Schritten:

* Kontrolle der verfügbaren Netzwerkschnittstellen
* Funktion des DHCP-Client-Deamon `dhcpcd` prüfen
* Installieren und Einrichten des Host-Access-Point-Deamon `hostapd`
* Installieren und Einrichten eines eigenen DHCP-Servers `dnsmasq`

***

Netzwerkschnittstellen einrichten
---------------------------------

Der RaspberryPI sollte zu diesem Zeitpunkt über ein Netzwerkkabel am Heimnetz angebunden sein. Ggf. wurde auch bereits der WLAN-Adapter mit dem System über USB verbunden.

Die Kontrolle der verfügbaren Netzwerkschnittstellen erledigt man wie folgt:

```shell
# Anzeige aller Interfaces
sudo ip link
```

* lo: Loopback Device mit IP 127.0.0.1
* eth0: Kabelgebundener Adapter
* wlan0: Wireless Adapter


Ob bereits Datenpakete erfolgreich über die Schnittstellen übertragen wurden, lässt sich folgendermaßen feststellen:

```shell
# Anzeige von Statistikdaten zu den Schnittstellen
sudo ifconfig -s
```

In der Regel werden alle Netzwerkadapter erkannt und angezeigt. Weitere Problembehandlungsmaßnahmen sollen hier nicht erörtert werden.

***

DHCP-Client Service einrichten
-------------------------------

Zuerst einmal muss geprüft werden, ob auf dem RaspberryPI-System überhaupt ein `dhcpcd`-Client Service läuft:

```shell
# Status von dhcpcd prüfen
service dhcpcd status
```

In der Regel sollte dieser installiert und gestartet sein.

Installieren und Einrichten von `hostapd`
-----------------------------------------

hostapd  ist ein Deamon (Service) für Access Point und Authentication Server. Dieser Implementiert z.B. WPA und WPA2/PSK für die sichere Anmeldung an ein Wireless LAN. Der Installationsablauf ist dabei wie folgt:

```shell
# Teste den Wireless Adapter auf Access Point Eignung
iw list | grep AP

# Installiere den hostapd
sudo apt-get install hostapd

# Konfiguriere
sudo vi /etc/hostapd/hostapd.conf

# Schütze die Konfigurationsdatei
sudo chmod 600 /etc/hostapd/hostapd.conf

# Ausführen im Kommandozeilen-Debug-Modus
sudo hostapd -dd /etc/hostapd/hostapd.conf
```

```shell
# File: /etc/hostapd/hostapd.conf
# WLAN-Router-Betrieb
# Schnittstelle und Treiber für Pi 2 Modell B
interface=wlan0
driver=nl80211
# WLAN-Konfiguration
ssid=MYCLOUD
channel=1
hw_mode=g
wmm_enabled=1
country_code=DE
ieee80211d=1
ignore_broadcast_ssid=0
auth_algs=1
# WLAN-Verschlüsselung
wpa=2
rsn_preauth=1
rsn_preauth_interfaces=wlan0
wpa_key_mgmt=WPA-PSK
rsn_pairwise=CCMP
wpa_passphrase=00000008
```

***

DNS-Server `dnsmasq` einrichten
---------------------------------

Schnittstelle `wlan0` einrichten:

```shell
# File: /etc/network/interfaces
allow-hotplug wlan0
iface wlan0 inet static
address 10.1.1.254
netmask 255.255.255.0
gateway 10.1.1.254
```

DNS-Server `dnsmasq` einrichten:

```shell
# File: /etc/dnsmasq.d/wlan0
# DHCP-Server aktiv für WLAN-Interface
interface=wlan0
# DHCP-Server nicht aktiv für bestehendes Netzwerk
no-dhcp-interface=eth0
# IPv4-Adressbereich und Lease-Time
dhcp-range=10.1.1.10,10.1.1.225,24h
# DNS
dhcp-option=option:dns-server,10.1.1.254

local=/localhost/
local=/coder/
address=/sandbox.coderbox/10.1.1.254
address=/owncloud.coderbox/10.1.1.254
address=/pastebin.coderbox/10.1.1.254
address=/www.coderbox/10.1.1.254
address=/test.coderbox/10.1.1.254
```

***

Quellen
--------

* [DHCPCD auf archlinux][Q01]
