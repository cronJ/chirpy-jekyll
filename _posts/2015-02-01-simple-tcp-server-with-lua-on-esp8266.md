---
title: Simple TCP server with LUA on ESP8266
date: 2015-02-01 15:19:00 +0200
categories: [Electronics, ESP8266]
tags: [electronics, esp8266, lua]
---

Here is a new LUA script example for your ESP8266 running NodeMCU.
The script creates a TCP server listening on port 80.
Each time you receive data on the server, it toggles the LED connected to the ESP8266 and sends a message back to the client.

If you need help with installing NodeMCU on your ESP8266, here I have a post for the process.

## First TCP server example

Let us got through the code in detail and in the end, you will find the full code.

We need to map our GPIO to the correct pins.
This was already discussed in the last article.

```lua
gpio0 = 3
gpio2 = 4
```

Enter your Wi-Fi SSID which you want to use for the connection and also the password for this network.

```lua
ssid = "AP-Name"
password = "password"
```

Then we define our GPIO0 as the LED output and create a helper variable to save the pin status.

```lua
pinLed = gpio0
pinStatus = 0
gpio.mode(pinLed, gpio.OUTPUT)
```

This code block sets your module into STATION mode, which can connect to other access points.
Then it will configure the Wi-Fi SSID and password.
After the configuration, it will enter a loop that runs every 1000 ms.
Here we check if the module has an IP which means we are connected to our network and start the main function.
If not we will run in this loop as long as we have no IP.

```lua
wifi.setmode(wifi.STATION)
wifi.sta.config(ssid, password)
tmr.alarm(0, 1000, 1, function()
     if wifi.sta.getip() == nil then
          print("connecting...")
     else
          print("IP: ", wifi.sta.getip())
          tmr.stop(0) -- Stop loop
          main() -- Start the main function
     end
```

Now we can create the TCP server.
The net.createServer() lets you create a UDP or TCP server.
With `net.TCP` we tell the function that we want a TCP server.

We tell the server module to implement a function when we receive a connection on port 80.
If this connection receives a payload we start a new function.

```lua
server = net.createServer(net.TCP)
server:listen(80, function(connection)
    connection:on("receive", function(connection, payload)
        [...]
    end)
end)
```

This is the content of our receiving function.
We print our payload, so we can see what happens.
Then we send back a string to the connected client.
On our board, we toggle the LED to show that the receiving function was called.
After all of this, we close the connection.

```lua
print(payload)
connection:send("<p>Hello Browser, I am an ESP-01 Modul</p>")
pinStatus = 1 - pinStatus
gpio.write(pinLed, pinStatus)
connection:close() -- Verbindung trennen
```

And here the full structured code with comments:

```lua
-- Pin mapping
gpio0 = 3
gpio2 = 4

-- Wifi credentials
ssid = "AP-Name"
password = "password"

-- Helper variables
pinLed = gpio0
pinStatus = 0

-- GPIO setup
gpio.mode(pinLed, gpio.OUTPUT)

-- Wifi setup
wifi.setmode(wifi.STATION)
wifi.sta.config(ssid, password)

-- Connection loop
tmr.alarm(0, 1000, 1, function()
     if wifi.sta.getip() == nil then
          print("connecting...")
     else
          print("IP: ", wifi.sta.getip())
          tmr.stop(0) -- Stop loop
          main() -- Start main function
     end
end)

-- Main function
function main()
    server = net.createServer(net.TCP)
    server:listen(80, function(connection)
        connection:on("receive", function(connection, payload)
            print(payload)
            connection:send("<p>Hello Browser, I am an ESP-01 Modul</p>")
            pinStatus = 1 - pinStatus
            gpio.write(pinLed, pinStatus)
            connection:close() -- Close connection
        end)
    end)
end
```

## Second TCP server example (URL request)

Because all the initial code is already in the code above, we only look at the main function.

The creation of the TCP server is the same as in the first example.

```lua
function main()
    server = net.createServer(net.TCP)
    server:listen(80, function(connection)
        connection:on("receive", function(connection, payload)
            [...]
        end)
    end)
end
```

We search for the two strings `led_on` and `led_off` in the payload.
If the string is not found, the variable will contain `nil`.

When both strings are found, the usage information is sent to the client.

If one of the strings was found, we toggle the LED into the requested state and send a confirmation to the client.

```lua
if string.find(payload, "led_on") and string.find(payload, "led_off") then
    connection:send("<p>Usage:</br>[IP]/led_on - turn LED on</br>[IP]/led_off - turn LED off</p>")
elseif string.find(payload, "led_on") ~= nil then
    connection:send("<p>LED is now on</p>")
    pinStatus = 1
    gpio.write(pinLed, pinStatus)
elseif string.find(payload, "led_off") ~= nil then
    connection:send("<p>LED is now off</p>")
    pinStatus = 0
    gpio.write(pinLed, pinStatus)
else
    connection:send("<p>Command not recognized</p>")
end
```

Here is the full code:

```lua
-- Pin mapping
gpio0 = 3
gpio2 = 4

-- Wifi credentials
ssid = "AP-Name"
password = "password"

-- Helper variables
pinLed = gpio0
pinStatus = 0

-- GPIO setup
gpio.mode(pinLed, gpio.OUTPUT)

-- Wifi setup
wifi.setmode(wifi.STATION)
wifi.sta.config(ssid, password)

-- Connection loop
tmr.alarm(0, 1000, 1, function()
     if wifi.sta.getip() == nil then
          print("connecting...")
     else
          print("IP: ", wifi.sta.getip())
          tmr.stop(0) -- Stop loop
          main() -- Start main function
     end
end)

-- Main function
function main()
    server = net.createServer(net.TCP)
    server:listen(80, function(connection)
        connection:on("receive", function(connection, payload)
            if string.find(payload, "led_on") and string.find(payload, "led_off") then
                connection:send("<p>Usage:</br>[IP]/led_on - turn LED on</br>[IP]/led_off - turn LED off</p>")
            elseif string.find(payload, "led_on") ~= nil then
                connection:send("<p>LED is now on</p>")
                pinStatus = 1
                gpio.write(pinLed, pinStatus)
            elseif string.find(payload, "led_off") ~= nil then
                connection:send("<p>LED is now off</p>")
                pinStatus = 0
                gpio.write(pinLed, pinStatus)
            else
                connection:send("<p>Command not recognized</p>")
            end

            connection:close() -- Close connection
        end)
    end)
end
```
