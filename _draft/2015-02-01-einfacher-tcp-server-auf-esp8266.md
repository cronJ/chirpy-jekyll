---
layout: post
title: "Einfacher TCP-Server auf ESP8266"
date: 2015-02-01 15:19:00 +0200
categories: electronics
---
Folgender Code erzeugt einen TCP-Server der auf Port 80 hört. Wenn Daten auf dieser Verbindung gesendet werden, schickt er eine Meldung an den verbundenen Client und schaltet die angeschlossene LED.

{% highlight lua linenos %}
-- Variablendeklaration
gpio0 = 3
gpio2 = 4

ssid = "AP-Name"
password = "DeinPasswort"

pinLed = gpio0
pinStatus = 0

-- Konfiguriere Ports
gpio.mode(pinLed, gpio.OUTPUT)

-- Starte Verbindung zu Netzwerk
wifi.setmode(wifi.STATION)
wifi.sta.config(ssid, password)

-- Wiederhole Schleife bis zur Verbindung
tmr.alarm(0, 1000, 1, function()
        if wifi.sta.getip() == nil then
            print("verbinde...")
        else
            print("IP: ", wifi.sta.getip())
            tmr.stop(0) -- Stoppe Schleife
            main() -- Starte Hauptprogramm
        end
end)

-- Hauptprogramm
function main()
        server = net.createServer(net.TCP) -- Erstelle TCP Server
        server:listen(80, function(connection) -- Server reagiert auf Port 80
            connection:on("receive", function(connection, payload) -- Verbindung reagiert auf empfangene Daten
                print(payload) -- Empfangene daten ausgeben
                connection:send("&lt;p>Hallo Browser, ich bin ein ESP-01 Modul&lt;/p>") -- Client eine Meldung schicken
                pinStatus = 1 - pinStatus
                gpio.write(pinLed, pinStatus)
                connection:close() -- Verbindung trennen
            end)
        end)
end
{% endhighlight %}

Beim Aufruf der IP-Adresse über einen Browser versucht dieser per HTTP an eine Webseite zu kommen. Dafür sendet er ein GET-Request was im Modul eine Funktion ausführt, da ja nun Daten empfangen wurden. Und noch eine Version, um die LED per URL zu schalten: 
    
{% highlight lua linenos %}
-- Variablendeklaration
gpio0 = 3
gpio2 = 4

ssid = "Dein-AP"
password = "DeinPasswort"

pinLed = gpio0
pinStatus = 0

-- Konfiguriere Ports
gpio.mode(pinLed, gpio.OUTPUT)

-- Starte Verbindung zu Netzwerk
wifi.setmode(wifi.STATION)
wifi.sta.config(ssid, password)

-- Wiederhole Schleife bis zur Verbindung
tmr.alarm(0, 1000, 1, function()
        if wifi.sta.getip() == nil then
            print("verbinde...")
        else
            print("IP: ", wifi.sta.getip())
            tmr.stop(0) -- Stoppe Schleife
            main() -- Starte Hauptprogramm
        end
end)

-- Hauptprogramm
function main()
        server = net.createServer(net.TCP) -- Erstelle TCP Server
        server:listen(80, function(connection) -- Server reagiert auf Port 80
            connection:on("receive", function(connection, payload) -- Verbindung reagiert auf empfangene Daten

                findLedAn = string.find(payload, "led_an") -- Finde String in Payload und speichere Position
                findLedAus = string.find(payload, "led_aus") -- Finde String in Payload und speichere Position

                print(payload) -- Empfangene Daten ausgeben

                if findLedAn == nil and findLedAus == nil then
                    connection:send("<p>Usage:</br>[IP]/led_an - schaltet LED an</br>[IP]/led_aus - schaltet LED aus</p>")
                elseif findLedAn ~= nil then
                    connection:send("<p>Die LED ist nun an</p>")
                    pinStatus = 1
                    gpio.write(pinLed, pinStatus)
                elseif findLedAus ~= nil then
                    connection:send("<p>Die LED ist nun aus</p>")
                    pinStatus = 0
                    gpio.write(pinLed, pinStatus)
                else
                    connection:send("<p>Befehl nicht eindeutig</p>")
                end

                connection:close() -- Verbindung trennen
            end)
        end)
end
{% endhighlight %}