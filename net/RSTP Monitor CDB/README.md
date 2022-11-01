
# RSTP Rapid Spanning Tree template for Zabbix

## Overview

For Zabbix version: 6.2 and higher  
A **draft** template for monitoring RSTP status and operation on SNMP enabled Ethernet switches.

## Setup

> See [Zabbix template operation](https://www.zabbix.com/documentation/6.2/manual/config/templates_out_of_the_box/network_devices) for basic instructions.

Refer to the vendor documentation.

## Zabbix configuration

No specific Zabbix configuration is required.

### Macros used

|Name|Description|Default|
|----|-----------|-------|
|{$INTERFACE_DISCOVERY_INTERVAL}|<p>Update interval for interface names (description) discovery</p> |`30m` |
|{$ITEMS_INTERVAL}|<p>Update interval for all items</p> |`1m` |
|{$RSTP_PORT_DISCOVERY_INTERVAL}|<p>Update interval for "RSTP" (bridge) ports discovery</p> |`30m` |

## Template links

There are no template links in this template.

## Discovery rules

|Name|Description|Type|Key and additional info|
|----|-----------|----|----|
|RSTP Port Discovery|<p>Discovers all RTSP (bridge) ports</p> |SNMP |rstp.port.discovery|
|SNMP Interface Discovery|<p>Discovers all interface names</p> |SNMP |snmp.if.discovery|

## Triggers

|Name|Description|Additional info|
|----|-----------|--------------------------------|
|RSTP Designated Root Change (now is {ITEM.LASTVALUE}) on {HOST.NAME}|Warning on Designated Root Change|A new Root Bridge has been elected|
|RSTP Root Port Change (now is {ITEM.LASTVALUE}) on {HOST.NAME}|Warning on Root Port Change|Root Bridge is now reachable via a different port (topology change)|
|RSTP Topology Change on {HOST.NAME}|A recent Topology Change as been detected|Time since last Topology Change <10m|

## Issues and limitations

This template has been tested on Zabbix 6.2 on an Ubuntu 22.04 LTS virtual machine with the following switches:
- HP Procurve 4204 and 4202vl
- Mikrotik RB4011iGS+ (some OIDs are not available)
- Mikrotik CCR1009-7G-1C-1S+ (some OIDs are not available)
- Planet GS-4210-24PL4C
- Cisco 2960 (running MSTP) with incomplete results (only 1 instance reponds to SNMP queries)

**PLEASE NOTE**: I didn't find a way to get interface names directly on RSTP Port Discovery rule so on discovered RSTP Ports you'll find interface index ({#PORTIFINDEX}) between parentheses (hence SNMP Interface Discovery rule just to have a way to get interface names associated with their indexes). Any suggestion to reach this goal would be welcome! ;-)

**IMPORTANT NOTICE**: this template generates a lot of items. On a Mikrotik RB4011iGS+ with 10 gigabit copper interfaces + 1 sfp+ module it generates 110 items. Adjust update intervals and add discovery filters to adjust this template to your Zabbix server performance and to your networking environment.

## Licence and Credits

I used a template by Enderson Maia as a starting point, correcting some import problems, adding some more discovery rules and improving some triggers to reduce false positives (ifAdminStatus and ifOperStatus must be taken into consideration when a bridge port is blocking).
[Thanks to Enderson Maia!] (https://github.com/endersonmaia/zabbix-templates/blob/master/rstp/Template_SNMP_RSTP.zbx.xml)

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

- https://en.wikipedia.org/wiki/RSTP
- https://oidref.com/
- https://oidref.com/1.3.6.1.2.1.1
- https://oidref.com/1.3.6.1.2.1.2
- https://oidref.com/1.3.6.1.2.1.17

## Final Notice

> This template has not been published on the official [Zabbix Community Template Repository](https://github.com/zabbix/community-templates) because is far from being perfect.
> Use it as a starting point and adjust it to your monitoring needs! ;-) 
