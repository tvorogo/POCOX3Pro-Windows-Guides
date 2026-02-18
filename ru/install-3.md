# Запуск Windows на Xiaomi Poco X3 Pro

## Установка

### Предварительные условия
- ```Мозг```
  
- [```Windows ARM ESD```](https://arkt-7.github.io/woawin/)

- [```twrp-3.7.1_vap.img```](https://github.com/WaLoVayu/POCOX3Pro-Windows-Guides/releases/download/twrp/twrp-3.7.1_vap.img)
    
- [```Драйвера```](https://github.com/WaLoVayu/POCOX3Pro-Windows-Releases/releases/latest)

- [```Образ UEFI```](https://github.com/WaLoVayu/POCOX3Pro-Windows-Releases/releases/latest)

### Опять загрузитесь в модифицированный recovery
- Замените `путь\к\recovery.img` на актуальный путь к **recovery.img**
```cmd
fastboot boot путь\к\recovery.img
```

### Выполните msc
> Скрипт может попросить вас запустить его еще раз. В таком случае, выполните эту же команду заново.
```cmd
adb shell msc
```

### Diskpart
>
> [!WARNING]
> НЕ СОЗДАВАЙТЕ, НЕ МОДИФИЦИРУЙТЕ, НЕ УДАЛЯЙТЕ РАЗДЕЛЫ В DISKPART!!!! ЭТО МОЖЕТ ПОЛНОСТЬЮ СТЕРЕТЬ ВАШ ТЕЛЕФОН, ОН ПЕРЕСТАНЕТ ГРУЗИТСЯ ДАЖЕ В FASTBOOT!!!! ЭТО ЗНАЧИТ ЧТО ВЫ ПОЛНОСТЬЮ УБЬЕТЕ СВОЙ ТЕЛЕФОН БЕЗ ВОЗМОЖНОСТИ ВОССТАНОВЛЕНИЯ! (исключениями является прошивка в EDL, но это будет стоить вам лишних денег)

```cmd
diskpart
```

#### Выберите Windows разделы на телефоне
>
> Используйте `list volume` что бы найти, замените `$` с актуальным номером раздела с именем **WINVAYU**

```diskpart
select volume $
```

#### Дайте буквенное обозначение X

```diskpart
assign letter x
```

#### Выберите раздел ESP
>

```diskpart
select volume $
```

#### Дайте ему букву Y

```diskpart
assign letter y
```

#### Выйдите из diskpart

```diskpart
exit
```


### Установка Windows
> [!Important]
> Убедитесь, что вы используете командную строку от имени администратора

> [!Important]
> По соображениям производительности рекомендуется использовать Windows 11 24H2 (сборки, начинающиеся с 261XX, например 26100.2454)
> Не устанавливайте или не обновляйтесь на Windows 11 **24H2 26100.7XXX** / **25H2 26200.7XXX** или выше! Вы не сможете загрузится в Windows из за BSoD'а!
>
- Замените `путь\к\install.esd` на фактический путь к **install.esd** (он также может называться install.wim или 22631.2861.XXXXXXX.esd)
```cmd
dism /apply-image /ImageFile:путь\к\install.esd /index:6 /ApplyDir:X:\
```
> Если вы получаете `Error 87`, проверьте индекс вашего образа с помощью `dism / get -imageinfo /ImageFile:путь\к\install.esd`, затем замените `index: 6` фактическим номером индекса **Windows 11 Pro** в вашем образе.

### Копирование вашего boot.img в Windows
- Перетащите файл **rooted_boot.img** из папки **platform-tools** на диск **WINNABU** в проводнике Windows, затем переименуйте его в **boot.img**.

### Установка драйверов
- Распакуйте архив с драйверами, затем откройте файл `OfflineUpdater.cmd` (если появляется ошибка, запустите вместо него `OfflineUpdaterFix.cmd `)
> Если он попросит вас ввести букву, введите букву диска **WINNABU** (которая должна быть **X**), затем нажмите enter

#### Создание файлов загрузчика Windows
> Если при копировании загрузочных файлов возникает ошибка, запустите **DriveLetterAssigner** еще раз, затем снова запустите следующую команду, заменив **Y** на **U**
```cmd
bcdboot X:\Windows /s Y: /f UEFI
```

#### Удалите букву диска для ESPNABU
> Если это не сработает, проигнорируйте это и перейдите к следующей команде. Этот фантомный диск исчезнет при следующей перезагрузке компьютера.
```cmd
mountvol y: /d
```

### Перезагрузка в fastboot
```cmd
adb reboot bootloader
```

#### Загрузка в UEFI
- Замените `путь\к\uefi.img` на актуальный путь к образу UEFI
```cmd
fastboot boot путь\к\uefi.img
```

### Перезагрузка в Android
- Ваше устройство должно перезагрузиться само по себе после +- 10 минут, после чего вы загрузитесь в Android для последнего шага.

## [Последний шаг: Настройка двойной загрузки](dualboot-4.md)



















