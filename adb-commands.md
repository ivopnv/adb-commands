#  ADB COMMANDS 
----
### GET
Get Serial number
```
adb shell getprop ro.serialno
```
Get Android version
```
adb shell getprop ro.build.version.release
``````
Get OS version
```
adb shell getprop ro.build.display.id
``````
Get IMEI
```
adb shell dumpsys iphonesubinfo
```
Get IMEI2 (dual SIM devices)
```
adb shell dumpsys iphonesubinfo2
```
Get Model
```
adb shell getprop ro.product.model
```
Get Screen density
```
adb shell getprop ro.sf.lcd_density
```
Get full prop
```
adb shell getprop
```
Get Screen size
```
adb shell dumpsys window | grep DisplayWidth
```
Get IP Address (1)
```
adb shell ifconfig tiwlan0
```
Get IP Addres (2)
```
adb shell netcfg | grep wlan0 | awk '{print $3}' | cut -f1 -d"/"
```
Get WIFI MAC
```
adb shell cat /sys/class/net/wlan0/address
```
Get BT MAC
```
adb shell settings get secure bluetooth_address
```
Get APN list
```
adb shell cat /etc/apns-conf.xml
```
Get Foreground activity
```
adb shell dumpsys window windows | grep -E 'mCurrentFocus|mFocusedApp'
```
Get Aalarms
```
adb shell dumpsys alarm
```
Get Bootanimation (1)
```
adb pull data/local/bootanimation.zip
```
Get Bootanimation (2)
```
adb pull system/media/bootanimation.zip
```
Get framework-res.apk (contains all pemissions and resources)
```
adb pull /system/framework/framework-res.apk
```
### LOGS
Log Error only
```
adb logcat :E
```
Log Given tags only
```
adb logcat TAG1:D TAG2:D TAG3:D *:S
```
NFC Logs
```
logcat -c; logcat NFC-HCI:D NfcDispatcher:D NfcService:D *:S
```
Battery Logs (1)
```
dumpsys battery
```
Battery Logs (2)
```
dumpsys batterystats
```
Full log dump
```
adb bugreport 
```
### PACKAGE
Force install application
```
adb install -r -f -d APK_NAME
```
List Packages (icluding apk path)
```
adb shell pm list packages -f
```
Clear Package data
```
adb shell pm clear PACKAGE_NAME
```
Get Pacakge Version Code (1)
```
adb shell dumpsys package com.systemonenoc.avatarapp | grep versionCode
```
Get Package Version Code (2)
```
adb shell pm dump com.systemonenoc.avatarapp | grep -i code
```
### PERMISSIONS
List Permissions (including protection level)
```
adb shell pm list permissions -f
```
Granted Permissions
```
adb shell dumpsys package PACKAGE_NAME
```
### SETTINGS

Open Settings
```
adb shell am start -n com.android.settings/com.android.settings.Settings
```
Add APN
```
adb shell am start -a android.intent.action.INSERT  content://telephony/carriers  --ei simId -1
```
Set settings
[secure](https://developer.android.com/reference/android/provider/Settings.Secure.html) [global](https://developer.android.com/reference/android/provider/Settings.Global.html) [system](https://developer.android.com/reference/android/provider/Settings.System.html)
```
adb shell settings put secure|global|system <value>
adb shell settings put system screen_brightness 0 
```
Get settings
```
adb shell settings get secure|global|system <value>
adb shell settings get system screen_brightness
```
### USEFUL
Take screen-shot
```
adb shell screencap -p | perl -pe 's/\x0D\x0A/\x0A/g' > screen.png
```
Record a video
```
adb shell screenrecord /sdcard
```
Run as app user
```
adb shell run-as PACKAGE_NAME
```
