# aqualin rev 0.1

All rights of the device are owned by Aqualin

This is a reverse engeneered Bluetooth Low Energy control of the aqualin BLE solenoid valve device without custumizations on the device itself.

The purpose of this script is to prove that it's possible to control a off the shelve BLE selenoid valve with open software (scripts). No garantees or liability can be given on usage of these scripts, usage of these scripts are at your own risk. 

Requirements are: 
- Linux distro (eg debian etc)
- hcitool
- gatttool 
- A compatible version of a BLE stack

I wrote two scripts containing the gatt commands to the correct uuid to control the device. Its neseccary to change the mac address to your aquilin device within this command in the script.

To identify the mac address of your device use hcitool (sudo hcitool lescan). This will list all the devices for example:

01:02:03:04:05:06 Spray-Mist

The mac address should be entered in the command below replacing the brackets with the correct mac, for example: 
```bash gatttool -b 01:02:03:04:05:06 --char-write-req -a 0x0073 -n 7b0301003c) ```

The command in the open valve for 30min is: 
```bash gatttool -b [01:02:03:04:05:06 put a valid mac address of the aqualin device here without the brackets] --char-write-req -a 0x0073 -n 7b0301003c ```

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
