<img align="right" src="https://github.com/n00b69/woa-perseus/blob/main/perseus.png" width="350" alt="Windows 11 running on perseus">

# Windows na Xiaomi Mix 3

## Ponowna instalacja Windows

### Wymagania
- [Windows dla ARM](https://worproject.com/esd)

- [Sterowniki](https://github.com/n00b69/woa-perseus/releases/tag/Drivers)
  
- [Obraz UEFI](https://github.com/n00b69/woa-perseus/releases/tag/UEFI)

### Uruchom do UEFI
> Zastąp `path\to\perseus-uefi.img` rzeczywistą ścieżką obrazu UEFI
```cmd
fastboot boot path\to\perseus-uefi.img
```

#### Włączanie trybu pamięci masowej
> Po uruchomieniu systemu UEFI użyj przycisków głośności do poruszania się po menu i przycisku zasilania, aby potwierdzić
- Wybierz **UEFI Boot Menu**.
- Wybierz **USB Attached SCSI (UAS) Storage**.
- Naciśnij przycisk dwa razy aby potwierdzić.

### Diskpart
```cmd
diskpart
```

#### Znajdowanie telefonu
> Spowoduje to wyświetlenie listy wszystkich podłączonych dysków
```cmd
lis dis
```

#### Wybieranie telefonu
> Zastąp $ rzeczywistym numerem partycji telefonu (powinien być ostatnim)
```cmd
sel dis $
```

#### Lista partycji Twojego telefonu
> Spowoduje to wyświetlenie listy partycji urządzenia
```cmd
lis par
```

#### Wybór partycji Windows
> Zastąp $ numerem partycji systemu Windows (powinno być 23)
```cmd
sel par $
```

#### Formatowanie dysku z systemem Windows
```cmd
format quick fs=ntfs label="WINPERSEUS"
```

#### Dodaj literę do systemu Windows
```cmd
assign letter x
```

#### Wyjdź z Diskpart
```cmd
exit
```

### Installing Windows
> Zamień `path\to\install.esd` na rzeczywistą ścieżkę do pliku install.esd (może on również nosić nazwę install.wim)

```cmd
dism /apply-image /ImageFile:path\to\install.esd /index:6 /ApplyDir:X:\
```

> Jeśli pojawi się komunikat `Błąd 87`, sprawdź indeks obrazu za pomocą polecenia `dism /get-imageinfo /ImageFile:<path\to\install.esd>`, a następnie zastąp `index:6` rzeczywistym numerem indeksu systemu Windows 11 Pro na Twoim obrazie

### Instalowanie sterowników
> Wypakuj archiwum ze sterownikami, potem otwórz plik `OfflineUpdater.cmd`
 
> Jeśli poprosi Cię o podanie litery, wpisz literę dysku **WINPERSEUS** (która powinna być X), a następnie naciśnij enter.

### Uruchom do Androida
Uruchom ponownie telefon. Jeśli zamiast systemu Windows wylądujesz w systemie Android, ponownie wykonaj flashowanie UEFI za pomocą WOA Helper.

#### Konfiguracja Windowsa
> Twoje urządzenie skonfiguruje teraz system Windows. To zajmie trochę czasu. W końcu uruchomi się ponownie, a następnie powinna rozpocząć się konfiguracja wstępna (oobe).

> [!Tip]
> If you wish to skip the Microsoft Account login, press the **I don't have internet** button in the WiFi page, then when prompted, press the **Continue with limited setup** button.

## Skończone!
















