
# Запуск Windows на Xiaomi Poco X3 Pro

## Рутируем ваш планшет
> [!NOTE]
> **Если вы уже рутированы, просто пропустите этот шаг и перейдите на следующую страницу**

### Предварительные условия
- ```Мозг```
  
- [```magisk.apk```](https://github.com/topjohnwu/Magisk/releases/latest)

### Прошивка magisk 
- Скачайте [`magisk.apk`](https://github.com/topjohnwu/Magisk/releases/latest) на ваш ПК/Ноутбук
> Замените `путь\к\magisk.apk` на актуальный путь к magisk.apk
```cmd
adb push путь\к\magisk.apk /tmp/magisk.zip && adb shell twrp install /tmp/magisk.zip
```

#### Перезагрузка в Android
> Если он не загружается, войдите в режим **recovery** и выполните **сброс к заводским настройкам**
```cmd
adb reboot
```

### Завершение настройки
- Пройдите первоначальную настройку устройства, затем скачайте и установите [Magisk](https://github.com/topjohnwu/Magisk/releases/latest), если он ещё не установлен.
- Откройте приложение **Magisk** и следуйте инструкциям на экране. Через несколько секунд ваше устройство перезагрузится.

### Создайте резервную копию загрузочного образа с правами суперпользователя
> Перезагрузитесь в [модифицированный образ recovery](https://github.com/WaLoVayu/POCOX3Pro-Common-Files/releases/download/twrp/twrp-3.7.1_vap.img), затем выполните приведенную ниже команду
```cmd
adb shell "dd if=/dev/block/platform/soc/1d84000.ufshc/by-name/boot$(getprop ro.boot.slot_suffix) of=/tmp/rooted_boot.img" && adb pull /tmp/rooted_boot.img
```

### [Следующий шаг: Установка Windows](install-3.md)













