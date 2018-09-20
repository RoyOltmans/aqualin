# Aqualin BLE bash control rev 0.2
-- Changes: Appending and extending the readme

All rights of the device are owned by Aqualin

This is a reverse engeneered Bluetooth Low Energy control of the aqualin BLE solenoid valve device without custumizations on the device itself.

# Motivation

The purpose of this script is to prove that it's possible to control a off the shelve BLE selenoid valve with open software (scripts). No garantees or liability can be given on usage of these scripts, usage of these scripts are at your own risk. 

I wrote two scripts containing the gatt commands to the correct uuid to control the device. Its neseccary to change the mac address to your aquilin device within this command in the script.

Next step will be a port to Python combining it with MQTT as an IoT controller/provider endpoint.

# Installation

Requirements are: 
- Linux distro (eg debian or raspbian etc)
- hcitool
- gatttool 
- A compatible version of a BLE stack and hardware (a rpi zero w in total works great and is quite cheap)

To install hcitool and gatttool for debian:

    $  sudo apt install git bluetooth bluez


Create a folder for example aqualin and clone the repository


    $  git clone https://github.com/RoyOltmans/aqualin.git /opt/aqualin

# Configuration

To identify the mac address of your device use hcitool (sudo hcitool lescan). This will list all the BLE devices, for example a identified Aqualin device is (it identifies as Spray-Mist, like the app):


    $  sudo hcitool lescan

*01:02:03:04:05:06* Spray-Mist

Now edit the two files ""timeronoff_off.sh"" and ""timeronoff_on.sh"". The mac address (in this ecxample *01:02:03:04:05:06*) in the file should be entered in the command below replacing the brackets with the correct mac, for example: 
::

    $  gatttool -b 01:02:03:04:05:06 --char-write-req -a 0x0073 -n 7b0301003c)

# Details

Service identified for manual programming:
uuid: 0000fceb-0000-1000-8000-00805f9b34fb
handle: 0x0073

Write bytes/char string see the breakup

Value (payload) [7b03][00|01]00[hex:MM]

Examples are:

- 7b03010005 on for 5min
- 7b0301001e on for 30min
- 7b0301003c on for 60min

Last two characters are hex written minute timer (how long the valve will be opened, untested but assumed in a quick test)

- 7b03010000 off
