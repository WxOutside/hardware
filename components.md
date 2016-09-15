Components
==========

This file describes the exact hardware components you need to build a fully functioning weather station. You'll still need to get the software set up, but that is described in a subsequent file.
The components included here are specifically picked for a low power consumption weather station. You can swap any of these for something else, but the power usage may change, and there may be software incompatibilities that you'll have to navigate.

Voltaic Systems V44 battery
---------------------------
This is a really tidy battery and comes with built-in power management. It will shut down when voltage drops too low, and won't turn back on until there is roughly 20 minutes of power stored. The always-on mode is a killer feature which makes this whole project possible.

Two 9w Voltaic Systems solar panels
-----------------------------------
Two panels give roughly 99% uptime through the course of the year, against 150mA-230mA device consumption. It's easily possible to add more - 3 panels would probably get 99.9% uptime depending on your climate.

Raspberry Pi A+
---------------
The Raspberry Pi A+ runs all the sensors, stores the telemetry and sends messages back to the dashboard. The A+ is a low-power model, and pulls 150mA when idle (with all the software installed and devices attached), peaking at 230mA depending on what it's doing.
If an A+ is no longer available, a Pi Zero will also be a good option - it should have roughly the same power consumption.
The Pi 3 will work, but consumes much more power and will drain your battery faster.

The A+ is not a particularly powerful unit though, and resource intensive processes should be avoided to ensure stability. The most lightweight solution was to use Python for communicating with the sensors, and to send all messages via the Linux email SMTP protocol.
A custom-built email message bus sends telemetry back to the main site, which responds with a receipt. When the receipt is received, the telemetry records are deleted. In cases where there is an outage (cellular network unavailable, or the RPi shut down before messages were sent), then messages are queued for resending. Although it might be delayed in some circumstances, no recorded data is ever lost.

WeatherPiArduino
----------------
The weatherPiArduino is made by SwitchDoc Labs and is a very convenient unit for connecting the anemometer and rain bucket. It's also the most complicated component to connect due to some ambiguous documentation.

AM2315
------
The AM2315 temperature and humidity sensor is a very reliable device and easy to set up. It needs a solar radiation shield, which you can 3D print using plans found on the web.
The plans found here work perfectly: http://www.thingiverse.com/thing:1067700

Wind Anemometer
---------------
Wellington gets some ferocious wind at times - it's not unusual to have average winds of 100Kph for extended lengths of time. If it's properly secured, the wind anemometer is a reliable device. The rain bucket absolutely must be secured to something solid and flat otherwise it won't trigger properly. Because this is an analog device, the weatherPiArduino is required to convert readings to digital signals.
This anemometer seems to be the standard device: https://www.sparkfun.com/products/8942

Some comments on this though:

* The metal pole doesn't have good galvanising. It will start to rust over time (just a cosmetic issue really)
* If you're in a high wind zone, the pole will need to be very firmly attached to something solid, such as a fence or a bigger pole. The provided attachment options are flimsy and the pole will wobble causing bad readings.

Soil moisture probe
-------------------
Originally I used an I2C soil moisture sensor from Catnip Electronics. It is not a reliable device for outdoor usage, and will eventually fail even with protective coatings on the sensor. **I do not recomment this device.**
SDI-12 devices such as AquaFlex or Decagon are much more expensive, but will provide industry-grade information, such as volumetric moisture readings, and battery voltages.

SDI-12 USB adaptor
------------------
If you're going to use a professional moisture probe, such as an Aquaflex sensor, you'll need to use an adaptor to convert the SDI-12 interface to something the RPi can use.
I recommend the SDI-12 USB adaptor, found here: https://liudr.wordpress.com/gadget/sdi-12-usb-adapter/
This adds a tiny amount of overhead to the power consumption (3mA), but will work out of the box, with no configuration required.

USB Splitter/Hub
----------------
Again, if you're using a professional moisture probe, then you'll also need a USB hub or splitter because the only USB port is now being shared between the 3G dongle and the USB adaptor.
Any unpowered USB hub should work - just get something with as few ports as possible, and preferably with no LED lighting.
The overhead for this is about 5mA.

3G dongle (Huawei e3131)
------------------------
This is a cellular device, which sends data via an email-based message bus. When it's not in use, it reverts to a low-power mode. This is really important since it's a high-consumption component and there is no way of switching off USB devices on the Raspberry Pi, so something with built-in power management is really useful. It's also very reliable - WiFi and radio connectivity is tricky to manage and it is an architectural principal to not maintain infrastructure.

Nanuk 905 case
--------------
This is a really solid case, and is perfect for holding all of the components together. All the cables run out a hole which is drilled in the side and sealed with a waterproof gland. Some careful tucking of cables gives it a nice clean look.

Silica gel packet
-----------------
If you open the case and the air is moist or humid, then the heat from the components will cause humidity to reach 100% and the Raspberry Pi will shut down. Throw in a silica gel sachet and problem solved - or don't open the case when it’s been raining!
