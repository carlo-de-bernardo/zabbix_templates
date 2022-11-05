
# Teracom TCW220 template for Zabbix

## Overview

For Zabbix version: 6.2 and higher  
A **draft** template for monitoring Teracom TCW220 measurements (1-wire sensors) + analog and digital inputs + relay status.

> [Teracom TCW220](https://www.teracomsystems.com/ethernet/ethernet-data-logger-tcw220/)

## Setup

> See [Zabbix template operation](https://www.zabbix.com/documentation/6.2/manual/config/templates_out_of_the_box/network_devices) for basic instructions.

Teracom TCW220 support up to 8 sensor, with 1 o 2 different readings depending on sensor type (TSH206 is and humidity and temperature sensor returning 2 readings).

This template contains only 1 item for sensor1/value1 (S1V1). The other 15 items must be created following these criteria:
- take a look at the existing item for sensor1/value1 (tcw220.sensor1.value1) and adjust it according to your monitoring needs setting the correct unit depending on the sensor in use
- adjust the trigger and/or create new ones for this item
- pay attention to the "observation time": triggers generate events after average threshold has been reached after 10 minutes to avoid firing too many events in case of a fluctuating signal on analog inputs and fluctuating measurements on sensors
- adjust the threshold macros for this item
- clone and rename the threshold macros to be used on the other 15 readings (if needed)
- clone the sensor1/value1 item for all your sensors, change keys and OIDs paying attention to use the following OIDs for each new item

  - S1V1: 1.3.6.1.4.1.38783.2.3.1.1.1.0
  - S1V2: 1.3.6.1.4.1.38783.2.3.1.1.2.0
  - S2V1: 1.3.6.1.4.1.38783.2.3.1.2.1.0
  - S2V2: 1.3.6.1.4.1.38783.2.3.1.2.2.0
  - S3V1: 1.3.6.1.4.1.38783.2.3.1.3.1.0
  - S3V2: 1.3.6.1.4.1.38783.2.3.1.3.2.0
  - S4V1: 1.3.6.1.4.1.38783.2.3.1.4.1.0
  - S4V2: 1.3.6.1.4.1.38783.2.3.1.4.2.0 
  - S5V1: 1.3.6.1.4.1.38783.2.3.1.5.1.0
  - S5V2: 1.3.6.1.4.1.38783.2.3.1.5.2.0
  - S6V1: 1.3.6.1.4.1.38783.2.3.1.6.1.0
  - S6V2: 1.3.6.1.4.1.38783.2.3.1.6.2.0
  - S7V1: 1.3.6.1.4.1.38783.2.3.1.7.1.0
  - S7V2: 1.3.6.1.4.1.38783.2.3.1.7.2.0
  - S8V1: 1.3.6.1.4.1.38783.2.3.1.8.1.0
  - S8V2: 1.3.6.1.4.1.38783.2.3.1.8.2.0

- clone the triggers changing macros and keys used 
- clone the graph changing graph name and item key

Refer to the vendor documentation.

> [Teracom TCW220](https://www.teracomsystems.com/ethernet/ethernet-data-logger-tcw220/)


## Zabbix configuration

No specific Zabbix configuration is required.

### Macros used

|Name|Description|Default|
|----|-----------|-------|
|{$ANALOG1_MAX_THRESHOLD}|<p>Upper threshold for analog input #1</p> |`10V` |
|{$ANALOG1_MIN_THRESHOLD}|<p>Lower threshold for analog input #1</p> |`0V` |
|{$ANALOG2_MAX_THRESHOLD}|<p>Upper threshold for analog input #2</p> |`10V` |
|{$ANALOG2_MIN_THRESHOLD}|<p>Lower threshold for analog input #2</p> |`0V` |
|{$MEASUREMENT_INTERVAL}|<p>Update interval for measurements</p> |`10s` |
|{$S1V1_MAX_THRESHOLD}|<p>Upper threshold for sensor1/value1</p> |`30` |
|{$S1V1_MIN_THRESHOLD}|<p>Lower threshold for sensor1/value1</p> |`10` |



## Template links

There are no template links in this template.

## Discovery rules

There are no discovery rules in this template.

## Triggers

|Name|Description|Additional info|
|----|-----------|--------------------------------|
|Analog 1 Voltage ({ITEM.VALUE}) on {HOST.NAME} is above {$ANALOG1_MAX_THRESHOLD} V|||
|Analog 1 Voltage ({ITEM.VALUE}) on {HOST.NAME} is below {$ANALOG1_MIN_THRESHOLD} V|||
|Analog 2 Voltage ({ITEM.VALUE}) on {HOST.NAME} is above {$ANALOG2_MAX_THRESHOLD} V|||
|Analog 2 Voltage ({ITEM.VALUE}) on {HOST.NAME} is below {$ANALOG2_MIN_THRESHOLD} V|||
|Digital Input 1 changed state: now {ITEM.LASTVALUE}|||
|Digital Input 2 changed state: now {ITEM.LASTVALUE}|||
|Relay 1 changed state: now {ITEM.LASTVALUE}|||
|Relay 2 changed state: now {ITEM.LASTVALUE}|||
|Sensor 1 Value 1 ({ITEM.VALUE}) on {HOST.NAME} is above {$S1V1_MAX_THRESHOLD}|||
|Sensor 1 Value 1 ({ITEM.VALUE}) on {HOST.NAME} is below {$S1V1_MIN_THRESHOLD}|||
|{HOST.NAME} has been restarted (Uptime: {ITEM.VALUE})|||


## Issues and limitations

This template has been tested on Zabbix 6.2 on an Ubuntu 22.04 LTS virtual machine with a Teracom TCW220 whith 1 TSH206 sensor.

> [Teracom TSH206](https://www.teracomsystems.com/sensors/digital-humidity-temperature-sensor-tsh206/)

## Licence

**MIT License**

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.


## References

>[Teracom TCW220 User Manual](https://www.teracomsystems.com/download/ethernet-data-logger-tcw220-user-manual/)
>
>[Teracom TCW220 MIB file](https://www.teracomsystems.com/download/ethernet-data-logger-tcw220-mib-file/)

## Final Notice

> This template has not been published on the official [Zabbix Community Template Repository](https://github.com/zabbix/community-templates) because it is far from being perfect.
> Use it as a starting point and adjust it to your monitoring needs! ;-) 
