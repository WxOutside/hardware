Performance information
=======================

The Raspberry Pi A+ consumes very little power when not busy - especially compared to the RPi 2, which idles at 230mA amps and easily exceeds 300mA. I expect the Raspberry Pi Zero to match the A+ but not be much more efficient. The number one trick for lowering power consumption is to reduce the number of USB devices that are attached since there is no way of switching these on and off.
Also, it's worth noting that these numbers were taken in Wellington, New Zealand, on the 41st parallel south, so other locations will experience different solar activity.

Summary of power consumption when not busy (idling):
----------------------------------------------------

* Raspberry Pi A+: 70mA
* 3G dongle: 60mA
* weatherPiArduino: 10mA
* AM2315: 10mA
* USB hub: 5mA
* Aquaflex soil sensor: 3mA
* Total power in idle: 158mA

Various measurements are taken across the hour, and all telemetry is sent out in one batch. Not all sensors are triggered at once, and the telemetry is sent during a time when no final measurements are taking place, so the 'in use' power consumption isn't a sum of every component.

Additional power consumption when triggered:
--------------------------------------------

* 3G dongle: 180mA
* weatherPiAuduino: 20mA
* AM2315: 40mA
* USB hub 5mA
* Aquaflex soil sensor: 3mA

For the soil probe and the AM2315, these numbers also include the background process of storing the data, so it's more than the stated power consumption that each device claims to use.
During the summer months, two 9w solar panels will easily provide enough power for continuous 24 hour operation - in fact, just one will suffice for most of summer. Occasional days of thick cloud cover or rain will not be severe enough to completely drain the battery because the daylight hours are long enough to provide a trickle of solar energy - enough to get us through to the next sunny day.

It is a bit different during winter when the days get shorter. Depending on the cloud cover, the battery will last about 2.5-3 days of rain and heavy cloud before it gives up. Even during the winter solstice when there is about 9 hours between sunrise and sunset (and even less that the solar panels can use), a nice clear day will fully charge the battery.

Further improvements can be made by using a power management device such as a WittyPi where the RPi is shutdown for most of the hour if no rain is expected and wind is consistent. This will allow for faster charging and better uptime during cloudy days.

