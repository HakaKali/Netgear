# Vulnerability Description
Netgear R6250 router is vulnerable to malicious input after authentication.
potential - SQL injection, buffer overflow

## Basic Information
* CVE-ID:
* Vendor: Netgear
* Product: R6250
* Firmware version: R6250-V1.0.4.48_10.1.30.zip

## Firmware Analysis
Firmware download: `https://www.netgear.com/support/download/?model=R6250`
![download](download.png)

Extract it directly using binwalk with the option -Me.

## Code Analysis

To extract data directly using Binwalk with the option `-Me`, use the `-Me` flag in Binwalk. This option allows you to quickly extract embedded files from a binary file without additional steps or tools.

Analyzing the binary file `/usr/sbin/httpd`, in the function FUN_00081a80, the values of `vlan_id` and `vlan_prio` is obtained from FUN_00016b04 (URLdecode) without proper input sanitization.
FUN_00017bd0 (Navigate to page).

![Decompiler](Decompile.png) <!-- Add this line to insert the decompiler image -->

Set up the router environment through FirmAE.

![Environment](environment.png) <!-- Add this line to insert the environment image -->


![VLAN_IPTV](VLAN_IPTV.png) <!-- Add this line to insert the VLAN_IPTV image -->


![WrongPriority](WrongPriority.png) <!-- Add this line to insert the WrongPriority image -->


![WrongVLAN_ID](WrongVLAN_ID.png) <!-- Add this line to insert the WrongVLAN_ID image -->


![Result](result.png) <!-- Add this line to insert the result image -->


A potential PoC is shown below:

![Burp](Burp.png)


## Vulnerability Fix

Treated and sanitized the input
