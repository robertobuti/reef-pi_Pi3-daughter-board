PRELIMINARY, work in progress
=============================

Reef-Pi daugther board
---------------------
This board has been designed in order to add some features on reef-pi project and help user to have all typical interface / requirements in a single board. Project is based on Pi3 CPU board, this chapter is long and reach of pictures & table , read it carefully before operate on board.

Main characteristics are :
- same size of Pi3, same fixing holes
- UPS function with lithium battery & battery charger
- GSM data connection for connectivity when power supply is down
- 8 outputs channel configurable for pwm or analog output, 0/5V or 0/10V (dimming light, variable speed pumps & c. )
- 4 digital inputs with pull-up and led for sensor level
- input 1 wire, optional HW protocol converter (temperature probes)
- 1 output RS485 for relay on multiple board expander (plugs)
- 1 port I2C for pH probe adapter

## Functions description ##

**Assembly daughter board to Pi3**
Mechanically the daughter board will be fixed on same 4 holes available on Pi3, 4 spacers M3 are required, lenghts suggest is XX mm. Main connection to and from Pi3 are with 40 pins connector, be carefull to insert it correctly.
Only other connection need to Pi3 is USB J28 that need to be connected on USB port of Pi3, unfortunatly no USB are available from Pi3 expansion connector, so an extra cable is required, i don't like it too much this solution but it's the only way.
On bottom side of daugther board is provided J2 connector for Lithium battery , before connect the battery be sure J29 is open / removed. (battery not inserted)
Be careful on battery polarity when you make connection.
Main power supply 5V doesn't any more be provided on Pi3 on MiniUSB but on equivalent J3 MiniUSB on daugher board, then the board itself provide to manage Pi3 from expansion connector pins.
Close J29 only when the system is fully installed , daughter board on Pi3 and battery connected, to switch off the system you will need open J29.

**UPS function & GSM**
It's the most relevant part of the project, goal of this task is to be advised by the system when the power (tank energy supply ) drop down, with a SMS, email, or by phone call, software will manage this functions at the moment i write this document is to be implemented. Equivalent system on my tank save it more then one time, obviousy any problem occur when you are in vacancy or long from tank, be advised is vital for tank, so a Lithium battery is required , one cell 500mA to 1A is more than need, circuit to charge and monitor is added, 3 leds permit also check the status on board it self. D1,D2,D3
D3 will On when power supply is OFF
D2 will On when battery is 50% charge
D1 will On when battery is 100% charge
A boost switching circuit provide Pi3 5V power supply with and without energy on  power line.  Is not relevant how many time battery provide backup, with 500mAh probalby are hours, but all we need is time to send alarm .
Data connections is provided by GSM module, miniPCIe style like Quectel EC20 LTE or similar. Be careful to connect it only when system is off and J29 open, remember also do not power the system without connect the antenna on LTE module, irreversible damange can occur. About antenna in most case simple and cheaper small dipole with UFL connector (flexible self adhesive or thin pcb style ) can be used. If you locally have bad signal you can opt for external antenna with cable , in this case tipically antenna are available with SMA connector and you will need a cable SMA to UFL connector available on module. LTE module need to be fixed on board with two hole and spacers, also only one can be used , just to be sure the module still in socket. On the board below the LTE module on right border (see the picture) is available the SIM socket J5, you will need to inser here a micro SIM enabled for service. No PIN protected. Please inset it always with system OFF.

**PWM & analog output**
8 individual channel from PCA9685 are provided on J24 connector, each one if buffered so can drive safely any signal interface, each channel can be configured with two jumpers, one two pins (open or close) and one 3 pins (two position jumper).
This option permit to hava on signal output a Square wave PWM or analog filtered signal, then you can choose if the span is 0/5V or 0/10V. A boot power supply circuit inside provide to generate 10V power supply, so no external aux power supply is required for 10V span. With this options any type of dimmerable equipment can be interfaced, like variable speed pumps or dimmerable lights. Most of dimming light system use 0/10V analog signal, but today you will find devices in all style, so with time and your suggestion we will complete a reference table for most diffused lights & pumps.

**Digital inputs**
This is really a simple connector where are provided leds for inputs immediate stays check and pull-up in order to operate them.
The table show the pins, inputs on Pi3 and matching leds

**1 wire interface **
One wire interface protocol is manage by kernel on Pi3, so is just a connector with pull-up to enable the connection of temperature probes, however one wire protocol is eavy to manage from kernel, if a day we see this become a problem a hw protocol converter can be enabled, the converter provide one wire bridge to I2C, some resistors 0 ohm are used to choose the configuration, for the moment is used the SW kernel management, but hw is ready if need ......

**RS485**
Reef-pi use some GPIO of Pi3 to drive relay for general purpose socket, that's fine but limited by number  of availabe GPIO and require a lot of wires. There are available from market simple and cheaper relay boards with RS485 interface (two wires only) , titpically any board drive 8 plugs and on some interface you can place many raly board with different address, so the system doens't have limit, more then no problem of distance from Pi3 and relay board will be with RS485 interface.
Actually reef-pi3 doesn't provide this feature, but i'm sure shortly does it.

**I2C**
pH adapter probe require I2C interface with pullup, so deicated connector is provided J25. This are low voltage high speed signal, my be better use shielded cable as showed on picture.

> Written with [StackEdit](https://stackedit.io/).