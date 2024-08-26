<img align="right" src="https://github.com/n00b69/woa-perseus/blob/main/perseus.png" width="350" alt="Windows 11 running on perseus">

# Запуск Windows на Xiaomi Mix 3

## Обновление драйверов 

### Требования
- [ADB & Fastboot](https://developer.android.com/studio/releases/platform-tools)

- [Образ UEFI](https://github.com/n00b69/woa-perseus/releases/tag/UEFI)

- [Драйвера](https://github.com/n00b69/woa-perseus/releases/tag/Drivers)

### Загрузитесь в UEFI
> Замените `путь\к\perseus-uefi.img` актуальным путём к образу UEFI
```cmd
fastboot boot путь\к\perseus-uefi.img
```

#### Включите режим mass storage
> После загрузки в UEFI используйте кнопки регулировки громкости для навигации по меню и кнопку питания для подтверждения
- Выберите **UEFI Boot Menu**.
- Выберите **USB Attached SCSI (UAS) Storage**.
- Нажмите кнопку **питания** дважды чтобы подтвердить.

### Diskpart
```cmd
diskpart
```

#### Выбрать раздел Windows 
> Используйте `list volume` чтобы найти его, замените `$` номером раздела **WINPERSEUS**
```diskpart
select volume $
```

#### Добавить букву к разделу Windows
```cmd
assign letter X
```

### Выйти из diskpart
```cmd
exit
```

### Установка драйверов 
> [!Note]
> This process will take +- 20 minutes. Do not worry, this is normal.

- Распакуйте пакет драйверов, затем откройте файл `OfflineUpdater.cmd` (Если появляется ошибка, запустите `OfflineUpdaterFix.cmd`)

> Введите букву диска **WINPERSEUS** (должна быть **X**) затем нажмите Enter

### Reboot your device
> Make sure to also change the UEFI image in Android, otherwise you may face a "blue screen of death" (BSoD) when booting Windows later.
```cmd
adb reboot
```

## Готово!












