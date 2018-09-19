# aqualin rev 0.1

Reverse engeneered aqualin BLE solenoid valve

No garantees or liability can be given usage of these scripts are totaly on your own risk.

The purpose of this script is to prove that it's possible to control a off the shelve BLE selenoid valve with open software (scripts).

The script shows the current breakup of a working command set.

NOTE requirements are: 
- Linux distro (eg debian etc)
- HCITOOL
- GATTTOOl 
- A compatible version of a BLE stack


BLE reverse engeneered findings:

Service identified for maunual programming:
uuid: 0000fceb-0000-1000-8000-00805f9b34fb
handle: 0x0073

write bytes/char string see the breakup

value [7b03][00|01]00[hex:MM]
Examples are:

7b03010005 on for 5min
7b0301001e on for 30min
7b0301003c on for 60min
Last two characters are hex written minute timer (how long the valve will be opened, untest yet)

7b03010000 off
