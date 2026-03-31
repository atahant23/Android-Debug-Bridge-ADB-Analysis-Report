1. Device Connection & Status
Commands to verify the bridge between Kali Linux and the physical Android device.


#Displays connected devices and their authorization status.sudo adb start-serverEnsures the ADB daemon is running with necessary privileges.
adb devices

#Ensures the ADB daemon is running with necessary privileges.
sudo adb start-server

# List Google packages to find the correct naming
adb shell pm list packages -f | grep "google"

# Find the specific path for the YouTube APK
adb shell pm path com.google.android.youtube

# Pull the APK using your specific filename
adb pull /product/app/YouTube/YouTube.apk ~/Desktop/youtube_analiz.apk

# (Optional) If direct pull fails, use the SDCard bridge
adb shell cp /product/app/YouTube/YouTube.apk /sdcard/Download/yt.apk
adb pull /sdcard/Download/yt.apk ~/Desktop/youtube_analiz.apk

# Analyze permissions and save to your specific file
adb shell dumpsys package com.google.android.youtube | grep permission > youtube_izinleri.txt

# Capture system logs into your specific log file
adb logcat -d *:W > cihaz_log_analizi.txt

# Launch JADX to inspect your extracted APK
jadx-gui ~/Desktop/youtube_analiz.apk

# Capture screenshot on the device
adb shell screencap -p /sdcard/evidence.png

# Pull the evidence to your project assets
adb pull /sdcard/evidence.png ./assets/ui_evidence.png

# Simulate 'Enter' key to demonstrate remote control
adb shell input keyevent 66
