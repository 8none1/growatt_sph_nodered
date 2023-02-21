# Summary of interesting registers

For the full list, see the PDF manual which is included in this repo.  These are some of the interesting ones I spotted while I was reading the list.

SPH type inverter supports:
 - 03 Registers range: 0-124, 1000-1124 (Holding registers?)
 - 04 Registers range: 0-124, 1000-1124 (Reading registers?)


## Useful Registers:
### Holding Regs 03
 - 15 - Read/Set LCD panel language (1 = English)
 - 22 - BAUD rate. 0 = 9600, 1 = 38400
 - 23 -> 27 - Serial number
 - 45 - Year
 - 46 - Month
 - 47 - Day
 - 48 - Hour
 - 49 - Min
 - 50 - Sec
 - 123 - Export Power Limit

 - 1017 - Batt Start #4 high 8 bits = hour, low 8 bits = mins
 - 1018 - Batt Stop #4 high 8 bits = hour, low 8 bits = mins
 - 1019 - Batt #4 on/off
 - 1020 - Batt Start #5
 - 1021 - Batt Stop #5
 - 1022 - Batt #5 on/off
 - 1023, 1024, 1025 - Batt #6 start, stop, on/off
 - 
 - 1037 CT Mode. 0 = wired CT, 1 = wirless CT, 2 = meter
 - 1038 CT Adjust.  0/1.  How does this work?
 - 
 - 1044 Priority Mode. 0 = Load, 1 = Batt, 2 = Grid.  Might be able to use this to switch battery charging instead of the time slots thing.
 - 
 - 1060 - UPS on / off
 - 1061 - UPS voltage output (0: 230, 1: 208, 2:240)
 - 1070 - Discharge to grid power rate %
 - 1071 - Stop discharge when this SOC in grid first
 - 1080, 1081, 1082, 1083, 1084, 1085, 1086, 1087, 1088 = Grid first slots 1,2,3. Start / end / onoff as batt start above
 - 1091 - Stop battery charge at this % SOC - bat first?
 - 1092 - Allow AC battery charging from grid

### Input Regs 04

 - 0 - Inverter status.  6 at night on batt.
 - 37 - grid freq
 - 38 - grid voltage
 - 39 - grid output current.  What does this mean?
 - 40 & 41 - watts used on load?
 - 93 - inverter temperature
 - 94 - IPM temp, whatever that is
 - 95 - Boost temp
 - 116 & 117 - charge power?
 - 118 - priority. 0 = load, 1 = batt, 2 = grid?
 - 119 - battery type.  1 = lion, 0 = lead acid

 - 1000 - system work mode.  0 waiting, 1 self test, 3 fault module, 4 flash module, 5 pvbat online, 6 batt online, 7 pvbatt offline, 8 batt offline
 - 1001,1002,1003,1004,1005,1006, 1007,1008 - system fault words (to investigate)
 - 1009 & 1010 - Battery discharge power
 - 1013 - Battery voltage
 - 1014 - Battery SOC %
 - 1015 & 1016 - AC power to user.  
 - 1032 & 1033 - Current inverter power to load
 - 1037 & 1038 - Total power to load
 - 1040 - Battery temperature
 - 1041 - Battery state charge or discharge 
 - 1086 - Battery SOC from BMS
 - 1087 - Battery volts from BMS
 - 1089 - Battery temp from BMS
 - 1090 - Max capacity of battery from BMS
 - 1091 - BMS Remaining Capacity (Doesn't look right to me)
 - 1092 - BMS Full-charge capacity (also doesn't look right)
 - 1095 - cycle count from BMS
 - 1096 - battery health from BMS
 - 1108 > 1123 - Cell N voltage


# Useful registers to Set
## Holding Registers

 - 1044 - Priority. 0 = load, 1 = batt, 2 = grid (i.e. export)
 - 1091 - Stop charge percent for batt first
 - 1092 - AC Charge enable. 0 = disable, 1 = enable








