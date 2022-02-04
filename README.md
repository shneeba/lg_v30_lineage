This has only been done on the US998 version of the LG V30.

# Prerequisits

Make sure you have the following available:

1. H93310h_00_OPEN_CA_OP_1124.kdz https://lg-firmwares.com/downloads-file/12260/H93310h_00_OPEN_CA_OP_1124
2. US99820h_00_0318.kdz https://lg-firmwares.com/downloads-file/19157/US99820h_00_0318
3. US99830b_00_0902.kdz https://lg-firmwares.com/downloads-file/20723/US99830b_00_0902
4. LGUP patched https://forum.xda-developers.com/attachment.php?attachmentid=4828349&d=1569503757
5. Wifi Fix
6. Tools
7. Pie Root
8. Lineage Install
9. LGUP
10. APKs


#### UNLOCK BOOTLOADER SO WE CAN INSTALL LINEAGE ####

1. Download mode
2. 318
3. boot to welcome
4. bootloader
5. flash new.bin with `.\fastboot.exe flash unlock .\new_unlock.bin`

Using LGUPD do the following. Make sure you do the button presses as specified, we don't want it to do the initial boot and start doing setups:

1. H93310h_00_OPEN_CA_OP_1124.kdz - Partition DL mode (check all partitions) - On reboot immediately do hardreset using the sequence (Hold vol-down and power, when you see LG splash release and press power again) - Keep holding vol-up to get download mode again.
2. US99820h_00_0318.kdz - REFURBISH mode - After reboot wait for "Erasing" screen and immediately hold vol-up button to get download mode again
3. Flash US99830b_00_0902.kdz - UPGRADE mode - Allow phone to fully boot to welcome screen

# Installing Lineage - the fun part

Now we're done with LGUP for a while until we use it at the very end to fix the modem.
You will want to do this from where you have the adb.exe file. Everything should be in Tools.

Some commands / button combos you will need:
```
# Button tricks - Use reset (vol-down and power) or just before boot before these combos
Boot to bootloader - vol-down + cable in
Boot to download mode - vol-up + cable in
Hard reset - hold vol-down + power - at LG splash let go of power and press again quickly

# From the bootloader screen boot to TWRP via the image on your PC
.\fastboot.exe boot TWRP.img

# From bootloader we can flash TWRP to recovery with
.\fastboot.exe flash recovery .\TWRP.img

# Reboot to recovery (make sure TWRP is installed first otherwise you'll get a sad screen)
.\adb.exe reboot recovery

# With ADB debug enabled on the phone you can go straight to the bootloader with
.\adb.exe reboot bootloader
```

1. Copy `Magisk-v18.0.zip`, `Disable_Dm-Verity_ForceEncrypt_08.18.2019_(Zackptg5).zip` and `AK3_RCTD_Remover_(JohnFawkes).zip` to the SD card or 'Internal Storage' ready and stay plugged in
2. From the welcome screen after the US99830b_00_0902.kdz LGUP flash, reboot to bootloader by restarting and holding vol-up
3. Boot to TWRP with `.\fastboot.exe boot TWRP.img`
4. It will error and ask for password, skip and go to 'WIPE' -> 'Format Data' -> 'yes' -> 'Swipe to Factory Reset'
5. Back to menu and click 'Reboot' -> 'Bootloader'
6. Boot to TWRP with `.\fastboot.exe boot TWRP.img`
7. ! Note - Don't wipe cache/davlic till instructed ! - Install `Magisk-v18.0.zip`, `Disable_Dm-Verity_ForceEncrypt_08.18.2019_(Zackptg5).zip` and `AK3_RCTD_Remover_(JohnFawkes).zip`
8. Wipe cache/davlik and reboot to welcome screen
9. Reboot to bootloader
10. Boot to TWRP with `.\fastboot.exe boot TWRP.img`
11. Go to 'Wipe' -> 'Advanced Wipe' -> Select 'Dalvik / ART Cache', 'System', 'Data', 'Internal Storage' and 'Cache' - ! DO NOT REBOOT !
12. !!!!!!!!!! DO THIS TO SAVE YOURSELF A HEADACHE !!!!!!!!!! - Wipe SD Card (it may be named slightly different) via 'Wipe' -> 'Advanced Wipe' -> Select 'SD Card'
13. Copy over `lineage-17.1-20200205-UNOFFICIAL-h930.zip`, `open_gapps-arm64-10.0-stock-20211217.zip`, `Magisk-v21.4.zip` and `Disable_Dm-Verity_ForceEncrypt_08.18.2019.zip` to either 'Internal Storage' or the 'SD Card' - ! Note - If you can't see your SD Card here don't worry, we'll get it back)
14. Go to 'Install' and install `lineage-17.1-20200205-UNOFFICIAL-h930.zip`, `open_gapps-arm64-10.0-stock-20211217.zip`, `Magisk-v21.4.zip` and `Disable_Dm-Verity_ForceEncrypt_08.18.2019.zip`. - ! Note - If you have issues with boot it's best to boot up first before installing `Magisk-v21.4.zip` and `Disable_Dm-Verity_ForceEncrypt_08.18.2019.zip`
15. Reboot the phone and wait for welcome screen
16. Reboot back to bootloader
17. Flash TWRP `.\fastboot.exe flash recovery .\TWRP.img`
18. Once booted you may see a 'Google speech' process error go through the setup process but do not login with an email address. - ! Your WiFi may or may not work at this point but we will fix it !
19. Your phone is now ready to configure, if you have any issues (other than WiFi) or boot loops check near the bottom of the guide for notes and possible fixes

** NOTE on boot loops **
1. Google FRP - go through login process using a stock LG image (318 or 902) and do not configure with an email
2. Remove your SD card - Trust me, this might be it being corrupt or something else just a bit dodgy
3. Make sure 'System' is fully wiped before install
4. Try and do a fresh boot to the OS first before installing Magisk
5. One of the LGUP processes messed up or you didn't catch it right, go back to the start from LGUP, trust me, it won't take as long as you think and will save you so much headache
6. If you have Google FRP (tied to phone) you'll need to either go through the login process using a stock LG image (318 or 902) - !!!!Not been tested!!!! but you could try using EFS (in Tools) to take NV backup and then do CHIP ERASE in LGUP (!!!!THIS WILL REMOVE YOUR IMEI!!!!) - !!!!! DO NOT DO THIS, LAST RESORT ONLY !!!!


# Final configuration for Lineage

There is a final bit of configuration we need to do just to get it as up to date and also fix safetynet. Some of this is preference but highly recommended.

## WiFi fix

Copy the following to the SD card:
`Wifi Fix\etc_vendor_wifi`
`Wifi Fix\mnt_vendor_persist-lg_wifi`

Fix WiFi directories in two mounts
1. Boot phone into the OS, make sure Debugging is enabled
2. Load into the shell `.\adb.exe shell`
3. Switch to root `su`
4. You should get a prompt from Magisk to allow - allow permenantly
5. Run the two commands to make a backup of your WiFi directories

`mkdir /sdcard/wifi_backups`
`cp -r /vendor/etc/wifi /sdcard/wifi_backups/wifi_etc_backup`
`cp -r /mnt/vendor/persist-lg/wifi /sdcard/wifi_backups/wifi_mnt_backup`

Copy over 'fixed' WiFi directories
1. `cp -r /mnt_vendor_persist-lg_wifi/* /mnt/vendor/persist-lg/wifi`
2. `cp -r /vendor/etc/wifi /sdcard/wifi_backups/wifi_etc_backup`

Fix permission structure !!!!!!!!!!!!!!!!!! WRITE OUT COMMANDS !!!!!!!!!!!!!!!!!!!!!!!!!
```
!!!MNT!!!

drwxrwx--- 5 wifi         wifi   4096 2017-03-01 01:02 wifi

/mnt/vendor/persist-lg/wifi
-rw-rw---- 1 wifi   system 15822 2017-03-01 16:06 WCNSS_qcom_cfg.ini
-rw-rw---- 1 wifi   system 15822 2022-01-22 00:06 WCNSS_qcom_cfg.ini.bak
-rw-rw---- 1 wifi   system    33 2017-03-01 16:06 wlan_mac.bin
-rwxrwxr-x 1 wifi   system   154 2017-03-01 16:05 wpa_supplicant_runtime.conf
-rwxrwxr-x 1 wifi   system   138 2022-01-14 19:56 wpa_supplicant_runtime.conf.bak
-rwxrwxr-x 1 wifi   system   154 2020-02-05 10:02 wpa_supplicant_runtime.conf.us


!!!ETC!!!
drwxr-xr-x 2 root shell   4096 2009-01-01 00:00 wifi

/vendor/etc/wifi
-rw-r--r-- 1 root root 15822 2009-01-01 00:00 WCNSS_qcom_cfg.ini
-rw-r--r-- 1 root root 19152 2009-01-01 00:00 bdwlan.bin
-rw-r--r-- 1 root root 19152 2009-01-01 00:00 bdwlan_ch0.bin
-rw-r--r-- 1 root root 19152 2009-01-01 00:00 bdwlan_ch1.bin
-rw-r--r-- 1 root root    67 2009-01-01 00:00 p2p_supplicant_overlay.conf
-rw-r--r-- 1 root root    71 2009-01-01 00:00 wifi_concurrency_cfg.txt
-rw-r--r-- 1 root root    81 2009-01-01 00:00 wpa_supplicant.conf
-rw-r--r-- 1 root root   149 2009-01-01 00:00 wpa_supplicant_overlay.conf
```

Fix symlinks just in case
1. Boot into TWRP
2. Copy over `[RECOVERY] WiFi_Fix_LG-v30_v2.zip`
3. Install `[RECOVERY] WiFi_Fix_LG-v30_v2.zip`
4. Reboot

! Note - The command `iw reg set "KR"` would fix my wifi issue, use this if having issues !

## Other updates and fixes

### Install Fdroid and Termux
1. Copy over the Fdroid APK and install Fdroid
2. Search and install termux

### Update Magisk to latest versions
1. Load Magisk Manager
2. Update Manager first, then Magisk
3. You will have to do this two or three times and reboot each time

### Install Magisk tools
1. Navigate to 'Modules'
2. Search for and install 'Debloater'
3. Search for and install 'MagiskHide Props Config'

### Fix SafetyNet
1. Load Termux
2. Swtch to root `su`
3. Run 'Props config' with `props` and select the following:

`1` - Edit device fingerprint 
`f` - Pick a certified fingerprint
`11` - LG
`19` - LG V30 LS998 (8.0.0)

4. Reboot the phone
5. Once booted load Magisk and use the 'Test SafetyNet' feature to confirm worked

### Remove YouTube and install Vanced
1. Load Termux
2. Swtch to root `su`
3. Run 'Debloater' with `debloat` and select the following:

`1` - System Apps
`60` - Youtube
`y` - Yes

4. Reboot phone
5. Download Vanced APK from https://github.com/YTVanced/VancedManager/releases/tag/v2.6.2-262
6. Install and grant root permissions for 10 minutes
7. Install YouTube


# Other stuff

** IMEI stuff **
To set IMEI you can use SRV menu:
1. Go to dialer and type \*#546368#*930#
2. Set 'Port Check Test' to 1
3. Use 'Mid Info' to set IMEI to dev one

!Not tested!
1. Take NV backup using EFS
2. Try and write IMEI using EFS Qualcomm tools

** SD Card not visible in OS or TWRP **
I think this is because it was formatted for a specific device, either way you need to:
1. Remove from device
2. Insert into PC or laptop
3. Open 'Disk manager' and find the drive
4. Delete the partitions
5. Leave unformatted

When you boot into the OS you should be able to format as a portable drive, NOT a data drive as part of the phone storage
You may need to format in TWRP first


** Other Commands **
```
# cat a file to PC directory as SU
adb.exe shell su -c cat /mnt/vendor/persist-lg/wifi/WCNSS_qcom_cfg.ini > WCNSS_qcom_cfg.ini

# Pull a file to PC directory
adb.exe pull /mnt/vendor/persist-lg/wifi/WCNSS_qcom_cfg.ini

# Push a file from PC to Phone
adb.exe push .\WCNSS_qcom_cfg.ini /sdcard/
# View dmesg logs to file (good for debugging)
adb.exe shell su -c dmesg > dmesg.txt

# View general android logs
adb.exe logcat
```

PIE stock key - magiskprop - `lge/joan_global_com/joan:9/PKQ1.190414.001/193091504cde8:user/release-keys`

-------
WIFI

Wifi seems to fail when reg domain set to GB (look in dmesg)

** So I think the fix is the reg domain for wifi, this command fixes it but not perm **
`iw reg set "KR"`
The main fix is to set the following to 0 in 'WCNSS_qcom_cfg.ini':
gRegulatoryChangeCountry=0
gCountryCodePriority=0

It seemed when looking at reg country with 'iw reg get' it would drop when going to GB
Setting to KR with 'iw reg set 'KR'' would fix but the above stops it breaking when set to GB
