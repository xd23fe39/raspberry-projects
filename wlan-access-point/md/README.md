[0]: README.md "Startseite"
[1]: FIRSTSTEPS.md
[2]: INSTALL.md
[3]: CONFIG.md
[4]: SUPPORT.md

WLAN Access Point using Raspberry PI
====================================

Von [Frank](mailto:xd23fe39@yahoo.de)

Dieses Dokument ist Teil von [WLAN Access Point using Raspberry PI][0]

***

Aufgabenstellung
----------------

Im konkreten Anwendungsfall soll ein Raspberry Pi Modell 2 1GB RAM als **Coderbox** so eingerichtet werden, dass man sich unabhängig von der Verfügbarkeit eines Festnetzes oder Heimnetzes direkt über WLAN mit der **Coderbox** verbinden kann. Die Coderbox soll dabei in der Anzeige der verfügbaren Funknetzwerke angezeigt werden, so dass jederzeit eine einfache Verbindung zur **Coderbox** aufgebaut werden kann. Dafür muss die **Coderbox** als sog. WLAN Access Point eingerichtet werden. Verbindet sich ein PC über WLAN mit der **Codebox**, wird die WLAN-Verbindung über DHCP automatisch konfiguriert. Dies erfordert die Installation eines einfachen DHCP-Servers auf der **Coderbox**.

Grundsätzlich sollte diese Anleitung mit unterschiedlichen Modellen des Raspberry PI funktionieren. Im Rahmen der Entwicklung dieser Anleitung wurde folgendes Modell verwendet: `Raspberry Pi 2, Modell B, 1GB RAM`

Im Rahmen dieser Anleitung kann natürlich keine Gewähr irgendwelcher Art geleistet werden.

Nächste Schritte
-----------------

* [Erste Schritte][1]
* [Installation durchführen][2]
