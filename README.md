# x1c7_2020_hacintosh
Lenovo Thinkpad X1 Carbon 7th 20R1 (2020, comet lake) Hackintosh</br>
**TL;DR : You cannot hackintosh on intel 10th generation based thinkpad at the moment without modding your BIOS**</br>
**AFAIK, There is no way modding and flashing BIOS for this generation Thinkpads.**</br>
**I'll keep this repo just to let people know why I failed (and you will too)**

## Brief info
X1 Carbon 7th Gen - (Type 20R1, 20R2) Laptop (ThinkPad) - Type 20R1 </br>
i7-10510u Comet Lake / LPDDR3 16GB onboard / UHD620 </br>
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
Unable to set XHCI Handoff, CFG Lock, Legacy RTC on BIOS - **THIS IS WHY YOU CANNOT BOOT**</br>
Based on dumped memory map, this machine has plenty of space @ 0x0001000 - no slide values needed

## Status
Cannot boot from both opencore (0.5.5 - 0.6.0) and clover (r5101 - r5111)</br>

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


#### Why I can't run macOS on modern Thinkpad?

- CFG Lock (MSR 0xE2) cannot be disabled <br>
with UEFI firmware N2QET22W, offset 0x3E on CpuSetup should be change to 0x00
```One Of: CFG Lock, VarStoreInfo (VarOffset/VarName): 0x3E```
- since this option is hidden on BIOS, you may change 0x3E offset to 0x00 but this area is protected by BIOS.<br>
Both GRUB shell and RU method failes while other laptops are normally okay with this.
- You may dump, fix and reflash your bios but I've found no success story. It is reported that BIOS is protected so you may no longer boot after modding.

## No hope?

- if !enovora1n comes out and supports modern Thinkpad to fix BIOS, We may.

## For people whom are willing to dump BIOS

- You can use intel flash programmer
- Classic way : SPI programmer. But I failed since this thinkpad has winbond w25q256fv which is WSON package type - I only had DIP8 clip.

