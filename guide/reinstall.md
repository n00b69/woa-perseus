<img align="right" src="https://github.com/n00b69/woa-perseus/blob/main/perseus.png" width="350" alt="Windows 11 running on perseus">

# Running Windows on the Xiaomi Mix 3

## Reinstalling Windows

### Prerequisites
- [Windows on ARM image](https://worproject.com/esd)

- [Drivers](https://github.com/n00b69/woa-perseus/releases/tag/Drivers)
  
- [UEFI image](https://github.com/n00b69/woa-perseus/releases/tag/UEFI)

### Boot to the UEFI
> Replace `path\to\perseus-uefi.img` with the actual path of the UEFI image
```cmd
fastboot boot path\to\perseus-uefi.img
```

#### Enabling mass storage mode
> Once booted into the UEFI, use the volume buttons to navigate the menu and the power button to confirm
- Select **UEFI Boot Menu**.
- Select **USB Attached SCSI (UAS) Storage**.
- Press the **power** button twice to confirm.

### Diskpart
```cmd
diskpart
```

#### Finding your phone
> This will list all connected disks
```cmd
lis dis
```

#### Selecting your phone
> Replace $ with the actual number of your phone (it should be the last one)
```cmd
sel dis $
```

#### Listing your phone's partitions
> This will list your device's partitions
```cmd
lis par
```

#### Selecting the Windows partition
> Replace $ with the partition number of Windows (should be 23)
```cmd
sel par $
```

#### Add letter to Windows
```cmd
assign letter x
```

#### Exit diskpart
```cmd
exit
```

#### Formatting Windows
> Go to Windows Explorer > This PC and select **WINPOLARIS**. Right click and format as NTFS.

### Installing Windows
> Replace `path\to\install.esd` with the actual path of install.esd (it may also be named install.wim)
```cmd
dism /apply-image /ImageFile:path\to\install.esd /index:6 /ApplyDir:X:\
```

> If you get `Error 87`, check the index of your image with `dism /get-imageinfo /ImageFile:path\to\install.esd`, then replace `index:6` with the actual index number of Windows 11 Pro in your image

### Installing Drivers
> Unpack the driver archive, then open the `OfflineUpdater.cmd` file

> If it asks you to enter a letter, enter the drive letter of **WINPERSEUS** (which should be **X**), then press enter

### Boot into Windows
Reboot your phone. If you end up in Android instead of Windows, flash the UEFI again using WOA Helper.

#### Setting up Windows
> Your device will now set up Windows. This will take some time. It will eventually reboot, and after that the initial setup (oobe) should launch.

> [!Tip]
> If you wish to skip the Microsoft Account login, press the **I don't have internet** button in the WiFi page, then when prompted, press the **Continue with limited setup** button.

## Finished!
















