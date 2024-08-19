<img align="right" src="https://github.com/n00b69/woa-perseus/blob/main/perseus.png" width="350" alt="Windows 11 running on perseus">

# Запуск Windows на Xiaomi Mix 3

## Установка Windows

### Требования
- [Образ ARM Windows](https://worproject.com/esd)
  
- [Драйвера](https://github.com/n00b69/woa-perseus/releases/tag/Drivers)

- [Devcfg исправления touch](https://github.com/n00b69/woa-perseus/releases/download/Files/devcfg-perseus.img)
  
- [Образ UEFI](https://github.com/n00b69/woa-perseus/releases/tag/UEFI)

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
> [!WARNING]
> НЕ УДАЛЯЙТЕ, НЕ СОЗДАВАЙТЕ И НЕ ИЗМЕНЯЙТЕ КАКИМ-ЛИБО ИНЫМ ОБРАЗОМ РАЗДЕЛЫ, НАХОДЯСЬ В DISKPART!!! ЭТО МОЖЕТ ПРИВЕСТИ К УДАЛЕНИЮ UFS ИЛИ НЕВОЗМОЖНОСТИ ЗАГРУЗКИ В FASTBOOT!!! ЭТО ОЗНАЧАЕТ, ЧТО ВАШЕ УСТРОЙСТВО БУДЕТ ОКИРПИЧЕНО БЕЗ КАКОГО-ЛИБО РЕШЕНИЯ! (за исключением доставки устройства в Xiaomi или его перепрошивки с помощью EDL, и то, и другое, скорее всего, будет стоить денег)
```cmd
diskpart
```

#### Выбрать раздел Windows 
> Используйте `list volume` чтобы найти его, замените `$` номером раздела **WINPERSEUS**
```cmd
select volume $
``` 

#### Добавить букву к разделу Windows
```cmd
assign letter x
``` 

#### Выбрать раздел ESP
> Используйте `list volume` чтобы найти его, замените `$` номером раздела **ESPPERSEUS**
```cmd
select volume $
``` 

#### Добавьте букву к ESP
```cmd
assign letter y
```

#### Выйти из diskpart
```cmd
exit
```

### Установка Windows
> [!Warning]
> НЕ ИСПОЛЬЗУЙТЕ 24H2!!!

> Замените `путь\к\install.esd` актуальным путём к install.esd (файл также может называться install.wim или 22631.2861.XXXXXXX.esd)
```cmd
dism /apply-image /ImageFile:путь\к\install.esd /index:6 /ApplyDir:X:\
```

> Если вы получите `Error 87`, проверьте индекс вышего образа используя `dism /get-imageinfo /ImageFile:путь\к\install.esd`, затем замените `index:6` действтельным индексом Windows 11 Pro в вашем образе

### Копирование вашего boot.img в Windows
- Перетащите **rooted_boot.img** на диск **WINPERSEUS** в проводнике Windows, затем переименуйте его в **boot.img**.

### Установка драйверов
- Распакуйте пакет драйверов, затем откройте файл `OfflineUpdater.cmd` (Если появляется ошибка, запустите `OfflineUpdaterFix.cmd`)

> Введите букву диска **WINPERSEUS** (должна быть **X**) затем нажмите Enter
  
#### Создать файлы загрузчика Windows
```cmd
bcdboot X:\Windows /s Y: /f UEFI
```

#### Включение тестовой подпись
```cmd
bcdedit /store Y:\EFI\Microsoft\BOOT\BCD /set "{default}" testsigning on
```

#### Отключите восстановление
```cmd
bcdedit /store Y:\EFI\Microsoft\BOOT\BCD /set "{default}" recoveryenabled no
```

#### Отключите проверку целостности
```cmd
bcdedit /store Y:\EFI\Microsoft\BOOT\BCD /set "{default}" nointegritychecks on
```

#### Удалите букву диска для ESP
> Если это не сработает, проигнорируйте это и перейдите к следующей команде. Этот фантомный диск исчезнет при следующей перезагрузке ПК.
```cmd
mountvol y: /d
```

### Перезагрузитесь в fastboot
> Удерживайте кнопку **уменьшение громкости** + **питание**, чтобы перезагрузить телефон в режим fastboot

#### Исправить touch
> Замените `путь\к\devcfg-perseus.img` актуальным путём к образу
```cmd
fastboot flash devcfg_ab путь\к\devcfg-perseus.img
```

#### Загрузитесь в UEFI
> Замените `путь\к\perseus-uefi.img` актуальным путём к образу UEFI
```cmd
fastboot boot путь\к\perseus-uefi.img
```

### Перезагрузка в Android
Ваше устройство должно перезагрузиться само после +- 10 минут ожидания, после чего вы загрузитесь в Android для последнего шага.

## [Последний шаг: Настройка двойной загрузки](4-dualboot-ru.md)
