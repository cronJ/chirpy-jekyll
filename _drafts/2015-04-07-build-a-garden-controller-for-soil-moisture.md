---
title: Build a garden controller for soil moisture
date: 2015-04-07 07:18:08 +0200
categories: [Electronics, Software, Hydroponics]
tags: [electronics, soil, moisture, controller, c, php, hydroponics]
---

To improve the efficiency of automatic garden watering systems, I tested some methods to measure the soil moisture.
Mainly I tried resistive and capacitive methods.

For connecting the sensors to a home automation system I need an adapter circuit.
It should read the sensor periodically and send the data to the home automation system.
All this should be possible while running on battery to be flexible where I place the system.

## Build

So, last weekend I build a little circuit with parts I already had lying around.
I use an Atmel ATMega48 to read a 10 bit DAC which I connected to the battery voltage.
From a DHT11 connected to the microcontroller, we read the temperature and humidity.
All three values are then sent to a MySQL database every 30 minutes.
I connected an ESP8266 via UART to the microcontroller.
The ESP8266 communicates via GET methods with an PHP script.
The script saves the data then to an MySQL database.

I created a quick prototype on a bread board.

![Garden Controller - Prototype](/assets/img/2015-04-07/2015-04-07-garden-controller-breadboard.jpg)

And then I started to build the circuit.
It was then placed into a 3D-printed case.

![Garden Controller - Top](/assets/img/2015-04-07/2015-05-10-garden-controller-top.jpg)

![Garden Controller - Side](/assets/img/2015-04-07/2015-05-10-garden-controller-side.jpg)

## Data plot

Here is an overview of the data:

![Garden Controller - Plot soil moisture](/assets/img/2015-04-07/2015-09-26-garden-controller-plot-soil-moisture.png)

![Garden Controller - Plot humidity](/assets/img/2015-04-07/2015-09-26-garden-controller-plot-humidity.png)

![Garden Controller - Plot temperature](/assets/img/2015-04-07/2015-09-26-garden-controller-plot-temperature.png)

![Garden Controller - Plot battery](/assets/img/2015-04-07/2015-09-26-garden-controller-plot-battery.png)

## Firmware

The firmware repository can be found here: [Firmware](https://github.com/cronJ/GardenController)

In the firmware the data is sent via HTTP GET requests.
We give the data as a GET parameter to the PHP script.
The `id` parameter tells the PHP script which data is given.

```c
void send_sensor_data(uint16_t analog_data, uint8_t temperature_data, uint8_t humidity_data)
{
	char value_buffer[10];
	char length_buffer[10];
	int string_length;

	/* give module time to power up */
	_delay_ms(2000);

	/* connect to wlan */
	serial_puts("AT+RST\r\n");
	_delay_ms(2000);
	serial_puts("AT+CWMODE=3\r\n");
	_delay_ms(2000);
	serial_puts("AT+CWJAP=\"SSID\",\"yourpassword\"\r\n");
	_delay_ms(10000);

	/* send analog value over tcp */
	serial_puts("AT+CIPSTART=\"TCP\",\"www.cronj.de\",80\r\n");
	_delay_ms(500);
	utoa(analog_data, value_buffer, 10);
	string_length = strlen(value_buffer) + 66;
	itoa(string_length, length_buffer, 10);
	serial_puts("AT+CIPSEND=");
	serial_puts(length_buffer);
	serial_puts("\r\n");
	_delay_ms(100);
	serial_puts("GET /your_page.php?id=1&value=");
	serial_puts(value_buffer);
	serial_puts(" HTTP/1.1\r\nHost: www.cronj.de\r\n\r\n");
	_delay_ms(500);
	serial_puts("AT+CIPCLOSE\r\n");
	_delay_ms(500);

[...]
}
```

## PHP script example

The receiving PHP script can look like this:

```php
<?php

$mysql_host = "localhost";
$mysql_db = "database";
$mysql_user = "username";
$mysql_pw = "password";
$mysql_table = "sensor_data";

/* check if both variables  are set */
if(isset($_GET["id"]) && isset($_GET["value"]))
{
	/* expect wrong usage */
	try
	{
		$id = (int) $_GET["id"];
		$value = (int) $_GET["value"];
	}
	catch(Exception $ex)
	{
		echo $ex;
		exit();
	}

	/* id should be an 8bit value and sensor value should be 16bit */
	if($id >= 0 && $id <= 1024 && $value >= 0 && $value <= 65536)
	{
		/* open mysql connection */
		$link = mysql_connect($mysql_host, $mysql_user, $mysql_pw)
			or die("can't connect to database: " . mysql_error());

		mysql_select_db($mysql_db)
			or die("can't select database: " . mysql_error());

		$query = "INSERT INTO " . $mysql_table . " (sensor_id, sensor_value) VALUES ('" . $id . "', '" . $value . "')";

		if(mysql_query($query) === TRUE)
		{
			echo "storage complete";
		}
		else
		{
			echo "storage failed";
		}

		mysql_close($link);
		exit();
	}

	echo "values doesn't match";
	exit();
}

echo "usage: 'file'?id='id'&value='value'";

?>
```
