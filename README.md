# x1c7_2020_hacintosh
Lenovo Thinkpad X1 Carbon 7th 20R1 (2020, comet lake) Hackintosh</br>
**WORK IN PROGRESS**</br>
**READ BEFORE USE!!**

## Brief info
X1 Carbon 7th Gen - (Type 20R1, 20R2) Laptop (ThinkPad) - Type 20R1 </br>
i7-10510u 4core Comet Lake / LPDDR3 16GB onboard / UHD620 </br>
BIOS : 1.16 (31 MAR 2020, N2QET22W)

<pre><code>
  Security Chip DISABLED
  Fingerprint 	Predesktop Authentication DISABLED
  Wireless WAN DISABLED (since my model does not came with WWAN and also not supported)
  Fingerprint Reader DISABLED
  Secure Boot DISABLED
  Intel SGX Control DISABLED
  UEFI/Legacy Boot UEFI Only
  CSM Support No
</code></pre>

Based on dumped DSDT, this machine has correct EC name - no EC fix needed</br>
Unable to set XHCI Handoff, CFG Lock, Legacy RTC on BIOS - should be fixed</br>
Based on dumped memory map, this machine has plenty of space @ 0x0001000 - no slide values needed

## Status
Cannot boot from both opencore (0.5.5 - 0.5.8) and clover (r5101 - r5111)</br>

- Clover : **stucks with +++++++++++++++++** (with every memory fix drivers on planet)

- Opencore : **stucks at bootscreen**

```
  26:526 11:424 AAPL: [EB|#LOG:EXITBS:START] 2020-04-13T02:10:07
```
or
```
  OCSMC : OCSMC: SmcReadValue Key 4D534163 Size 2
```
Tried both Clover and Opencore but mainly testing with Opencore

#### Applied fixes

- CFG Lock (MSR 0xE2) fix <br>
with UEFI firmware N2QET22W, 0x3E should be change to 0x00
```One Of: CFG Lock, VarStoreInfo (VarOffset/VarName): 0x3E```
- CPUID, platform-id, device-id fix<br>

