# React native
## Edit host of android sdk

```
Library/Android/sdk/tools/emulator -avd Pixel_3 -writable-system &
Library/Android/sdk/platform-tools/adb devices
Library/Android/sdk/platform-tools/adb root
Library/Android/sdk/platform-tools/adb remount
Library/Android/sdk/platform-tools/adb -s emulator-5554 push ~/Desktop/hosts /system/etc/hosts
Library/Android/sdk/platform-tools/adb reboot
```
