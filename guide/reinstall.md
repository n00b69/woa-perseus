<img align="right" src="https://github.com/n00b69/woa-perseus/blob/main/perseus.png" width="350" alt="Windows 11 running on perseus">

# Running Windows on the Xiaomi Mix 3

## Reinstalling Windows

### Prerequisites
- [ADB & Fastboot](https://developer.android.com/studio/releases/platform-tools)

- [Modded OFOX recovery](https://github.com/n00b69/woa-perseus/releases/download/Files/modded-ofox-perseus.img)

### Boot into OFOX
> If MIUI has replaced your recovery, boot to fastboot and run
```cmd
fastboot flash recovery path\to\modded-ofox-perseus.img reboot recovery
```

#### Formatting the Windows partition
```cmd
adb shell format
```

## [Next step: Reinstalling Windows](3-install.md)









