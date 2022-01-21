# lg_v30_lineage - For LG US998

1. H93310h_00_OPEN_CA_OP_1124.kdz https://lg-firmwares.com/downloads-file/12260/H93310h_00_OPEN_CA_OP_1124
2. US99820h_00_0318.kdz https://lg-firmwares.com/downloads-file/19157/US99820h_00_0318
3. US99830b_00_0902.kdz https://lg-firmwares.com/downloads-file/20723/US99830b_00_0902
4. LGUP patched https://forum.xda-developers.com/attachment.php?attachmentid=4828349&d=1569503757

Steps:

1. Flash H93310h_00_OPEN_CA_OP_1124.kdz via LGUP using Partition DL mode ( check all partitions), when phone automatically restarts - immediately do hardreset using the buttons, keep hold Vol. up button, we get download mode again

2. Flash US99820h_00_0318.kdz using REFURBISH mode, when phone automatically restarts - just wait "Erasing" screen and now immediately keep hold Vol. up button, we get download mode again

3. Flash US99830b_00_0902.kdz using UPGRADE mode ,
at this stage the phone will boot normaly and you finally get 9.0 Pie.
Next step is optional, but strongly recommended

4. Flash US99830b_00_0902.kdz again using REFURBISH mode, and now you have clearly fully stock.

5. Boot to recovery TWRP
6. flash recovery
7. root
8. decrypt
9. lg root unblocker
10. Reboot phone to welcome screen
11. Back to recovery
12. lineage install
13. gapps install
14. Boot phone to lineage
15. Will fail and require factory reset (could do this in TWRP before maybe?)
16. WiFi still fucked, back to recovery
17. root
18. decrypt

-------
WIFI

Wifi seems to fail when reg domain set to GB (look in dmesg)

** So I think the fix is the reg domain for wifi, this command fixes it but not perm **
`iw reg set "KR"`
I need to work out how to configure this perm either via wpa_supplicant or some other way


### Post install fixes
In magisk install:
1. MagiskHide Props Config
2. Debloater

To fix safetynet 
