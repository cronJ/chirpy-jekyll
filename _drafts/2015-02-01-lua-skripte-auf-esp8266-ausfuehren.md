---
layout: post
title: "LUA Skripte auf ESP8266 ausführen"
date: 2015-02-01 11:53:26 +0200
categories: electronics
---
Nach der Installation von NodeMcu besteht nun die Möglichkeit, ganze LUA Skript-Dateien auf dem ESP-01 Modul abzulegen. Das Ganze soll hier kurz anhand eines kleinen Testskriptes gezeigt werden. 

# Benötigte Software

Im Grunde reicht jedes Terminalprogramm, in dem man die Geschwindigkeit der Übertragung von Zeilen einstellen kann. Der Interpreter im ESP8266 ist nicht immer schnell genug, um mit der Übertragung des Terminals mithalten zu können. Deshalb sollte man eine Verzögerung zwischen den einzelnen Programmzeilen einfügen. Ich selbst verwende den ESPlorer von [4refr0nt](http://esp8266.ru/esplorer/). Damit konnte ich die vorherige AT-Firmware komfortabel testen und er hat auch NodeMcu Unterstützung. 

# Hello LED

Wie bei jeder neuen Mikrocontrollerarchitektur lassen wir nun erst einmal unsere LED blinken. 
    
{% highlight lua linenos %}
ledPin = 3	-- GPIO0
ledStatus = 0

gpio.mode(ledPin, gpio.OUTPUT) -- GPIO0 als Ausgang

tmr.alarm(0, 1000, 1, function() -- Alarm an Timer 0 auf 1000ms setzen
    ledStatus = 1 - ledStatus -- Wenn ledStatus = 1 -> 0; Wenn ledStatus = 0 -> 1

    gpio.write(ledPin, ledStatus) -- LED umschalten
end)
{% endhighlight %}

Dieses einfache Skript startet eine Alarmfunktion bei Timer 0. Der eigentliche Alarm ist eine Funktion, die unsere LED umschaltet. Der Alarm wird alle 1000ms -> 1s ausgeführt.

{% include image.html path="/images/2015/02/" img="ESPlorer_HelloLed" type="jpg" desc="" %}

Im ESPlorer verbindet man sich erst mit dem passenden COM-Port. Dann erstellt man seinen Code im Script-Tab und speichert die erstellte Datei auf seinem System. Mit dem Button "Save to ESP" wird die Datei auf dem Modul abgelegt und ausgeführt. Möchte man bei jedem Start sein Skript starten lassen, zum Beispiel nach einem Versorgungsspannungsverlust, sollte es als init.lua gespeichert werden. Und das Ergebnis als Bewegtbild:

[[Youtube] Hallo LED auf ESP8266 mit NodeMcu](https://www.youtube.com/watch?v=daclmhlzUhs)