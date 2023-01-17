# Growatt SPH 3-6k TL BL UP 

I've got two 6kW Growatt SPH inverters, one of which has two Growatt 6.5kW batteries connected.  I want to get access to the data to use in my own automations and for logging and graphing.
This is a work in progress.

## Existing solutions

First off there is Solar Assistant.  It sounds very good but I haven't tried it.  It is a commercial application and seems to offer a decent feature set.

Alternatively, you can reflash the Shine Wifi X dongles. 
You can read more about re-flashing the dongle here:  https://diysolarforum.com/threads/hacking-the-new-growatt-wifi-f-modules.43231/

## The hard way

Another way to talk to your inverters is to use Modbus RS-485.  There is an RS-485 port on the bottom of the inverter labeled "485-2" - this is where I have plugged in a custom cat5 cable.  You can read more about the pin outs for this port on the Solar Assistant page here:  https://solar-assistant.io/help/growatt/sph-range

At the other end of the cat5 cable you need to plug in to something which talks Modbus.  I have found the Elfin EW11A to be easy to use and so far very reliable.  They look like this:

![image](https://user-images.githubusercontent.com/6552931/212492135-d448d79f-f914-47ad-84ce-a15d6241f465.png)



You can buy them on Ali Express for about £10 inc tax & delivery.  https://www.aliexpress.com/item/1005001273331424.html

Alternatively you could use an ESP8266 or ESP32 and an RS-485 converter.

You will also need a suitable power supply.

I've got +/- volts from the PSU going to pins 7 & 8 on a cat 5 plug.  I used the brown pair.
Pins 5 & 6 from the same cat5 plug going to a length of cat5 on a different pair to the power.  I used the orange pair.
That pair goes to another cat5 plug on pins 1 & 5 which plugs in to the inverter.

I'll post a proper diagram later.

Once you've got it connected up and configured the Elfin EW11 (instructions to follow) you can easily query them from Node Red and do whatever you like with the data.


# The SPH inverter

## Modbus RTU Registers

The SPH line of inverters provide Modbus RTU registers that you can read (and in some cases write) to gather information about the performance and settings of the inverter.  There is a rich function set and you can read what each register does in the RTU protocol PDF document in this repo.

### 03 Register Range
The 03 registers are called "holding" registers.  These typically hold values for configuration like options and system settings.  You can write to a lot of these registers to change settings.  For example, you can switch the inverter on and off, set the time, change the LCD language.  There are also a lot of factory configured low level configuration options available.  I'm staying well away from these until I understand what they do. 

The SPH inverter supports registers:
 - 0 to 124
 - 1000 to 1124

### 04 Register Range
The 04 registers are called "input" registers.  These typically hold values referring to the performance of the inverter, how much PV power is being produce, what the voltages are, etc.  These are read only.

The SPH inverter supports registers:
 - 0 to 124
 - 1000 to 1124
 - 1125 to 1249



# Automation

## Node Red
An example flow which uses the node-red-contrib-modbus module https://github.com/biancoroyal/node-red-contrib-modbus is available in this repo.

There are a few different functions which process the Modbus registers and turn them in to something useful.  This are then stuck in a JSON object and sent to MQTT for you to do what you like with.
I will include some examples for Home Assistant and Telegraf so that you can process and graph this data in, for example, InfluxDB.

## Home Assistant
To follow

## Telegraf
To follow

# Registers of interest
I will fill this out later.  In the meantime, look at the functions in the Node Red flow for the registers I've found useful.

# Resources

A list of the registers available for the inverter is included in this repo in a PDF. There doesn't seem to be an official source of this information from Growatt, so caveat emptor.


