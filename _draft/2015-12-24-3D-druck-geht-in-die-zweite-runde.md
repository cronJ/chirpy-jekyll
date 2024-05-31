---
layout: post
title: "3D-Druck geht in die zweite Runde"
date: 2015-12-24 11:46:00 +0200
categories: 3d-printing
---
Nach dem ich mit dem GRR Neo nun einige Kilogramm Filament verdruckt habe, kann ich für mich sagen, dass sich die Anschaffung eines solchen Werkzeuges gelohnt hat. Ab und zu drucke ich auch mal ein interessantes Teil von Thingiverse, aber hauptsächlich erstelle ich die Teile selbst, das ist schneller als etwas zu suchen (und nicht zu finden) und ich kann die Teile an die Eigenarten meines Druckers anpassen um schöne Endprodukte zu erhalten. Meine benötigten Teile erstelle ich mittlerweile mit Hilfe von OpenSCAD oder Autodesk Fusion 360.

So schön der GRR Neo auch ist, einige Sachen waren für mich nervig. Die Druckbettkalibrierung ist das A und O für einen funktionierenden Druck. Wie die Kalibierung funktioniert, habe ich im letzten Artikel beschrieben. Meistens habe ich aber während dem Druck vom Skirt den Abstand noch feinjustiert damit es passt. Mein Drucker steht mit der Rückseite zur Wand. Dadurch war ein Filamentwechsel immer ein Akt. Das Filament in den Bowdenzug des Extruders zu schieben, welcher sich ebenfalls hinten befindet, liess mich so manches Mal fluchen.

Das waren aber die einzigen beiden Sachen, die mich störten und die letzte war nur Standort bedingt. Ansonsten war ich sehr zufrieden mit dem Drucker. Die ein oder andere Verstopfung des Hotends war jedes Mal relativ leicht zu beseitigen.

# Neue Anforderungen
Mit steigendem Interesse an dem Thema 3D-Druck, steigen auch die Anforderungen an das Werkzeug. Testdrucke von Smartphonehüllen für Familienmitglieder zerlegte es beim Überziehen, auf Grund des festen PLA. Flexibles Material steht zum Kauf bereit aber kann von meinem Drucker nicht gedruckt werden. Auche andere Materialien wie ABS, HIPS, Nylon oder Filamente mit Holz-, Kupfer-, Bronzefüllung sind mittlerweile erwerbbar. Ein neuer Drucker sollte die Möglichkeit haben, dies alles drucken zu können.

Ein Drucker der mir direkt einfiel, ist der Lulzbot Mini von Aleph Objects. Dieser verfügt über eine automatische Druckbettkalibrierung. Dafür befinden sich an jeder Ecke des Druckbettes Metallscheiben. Die Düse des Hotends wird automatisch mit Hilfe eines Abstreifers gereinigt. Dann fährt der Drucker die Düse auf die Metallscheiben, wodurch ein Stromkreis durch die metallische Düse geschlossen wird. Die Software berechnet dann die Lage des Druckbetts und korrigiert während dem Druck die Z-Achse entsprechend. Die ganze Prozedur erfolgt vor jedem Druck und läuft komplett autark ab.

Mit diesem Drucker wäre die Kalibrierung kein Thema mehr, aber wie sehen die weiteren Eigenschaften des Druckers aus? Der Druckraum beträgt 152 x 152 x 158 (L x B x H), welcher ungefähr meinem GRR Neo entspricht. Dieser Druckraum war mit immer ausreichend, ich hatte erst zwei Teile die auf einer Seite 150mm lang waren. Der Spulenhalter befindet sich über dem Druckraum und ist somit einfach zu erreichen. Der Lulzbot Mini wird mit einem Vollmetall-Hotend ausgeliefert was bis 300°C aufgeheizt werden kann. Dadurch kann es für viele der neuen Materialien verwendet werden, wie zum Beispiel Nylon (225°C - 270°C Drucktemperatur). Allerdings erfordern diese Materialien auch ein beheiztes Druckbett, welches der Mini ebenfalls besitzt (bis zu 120°C heizbar). Der Extruder sitzt direkt über dem Hotend, was den Filamentwechsel vereinfacht. Der Drucker besitzt nur einen USB-Anschluss, mit Hilfe von OctoPi kann er aber unabhängig von einem PC betrieben werden. Der Lulzbot Mini benötigt 3mm Filamentdurchmesser, wodurch mein 1,75mm PLA Vorrat nicht mit dem Drucker verwendbar ist.

Alles in allem, habe ich mich für den Drucker entschieden und es bis jetzt noch nicht bereut.

# Der Neue
Das gute Stück hat die Position seines Vorgängers erhalten.

{% include image.html path="/images/2015/12/" img="DSC5166" type="jpg" desc="Der Stellplatz" %}

Hier wird gerade eine Halterung für den Kofferraum gedruckt. Als Material verwende ich schwarzes HIPS, was eine mattere Oberfläche als PLA hat.

{% include image.html path="/images/2015/12/" img="DSC5169" type="jpg" desc="Am drucken" %}

Nach dem Druck fährt das Druckbett zur Rückseite, wenn es dann die 60°C unterschreitet kommt es nach vorne. Dann kann man das gedruckte Teil leicht vom Druckbett lösen.

{% include image.html path="/images/2015/12/" img="DSC5172" type="jpg" desc="Oktopus" %}

Dieser Oktopus liegt dem Drucker bei. Er wurde zu Kalibrierungszwecken auf diesem Drucker im Werk gedruckt.

{% include image.html path="/images/2015/12/" img="DSC5178" type="jpg" desc="Rocktopus" %}

Der Rocktopus liegt als Objekt auf dem mitgelieferten USB-Stick und wird als erster Druck nach Anleitung erzeugt. Dafür liegt dem Drucker ein Meter gelbes HIPS bei. Die Druckeinstellungen sind auf mittlerer Geschwindigkeit.