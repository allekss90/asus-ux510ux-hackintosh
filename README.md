## КОРОТКИЙ ГАЙД ПО ВСТАНОВЛЕННЮ macOS 11 (debug mode) ЗА ДОПОМОГОЮ OPENCORE 0.7.4 (ONLINE INSTALLER) на окремий диск.
*(для особистого використання та тільки в цілях тестування)**


#### Технічні Характеристики: 
Asus zenbook ux510ux:
- Intel Core i7-6500U (Skylake)
- Intel HD Graphics 520 / NVIDIA GeForce GTX 950M
- Intel Dual Band Wireless-AC 7265
- Realtek High Definition Audio
- BIOS Type - UEFI

#### Що не працює / працює погано:
- гарячі клавіші з Fn
- підсвітка клавіатури
- сон
- Bluetooth не стабільний
- NVIDIA GeForce GTX 950M - disabled
- можливо щось інше

## Увага:
Данні налаштування підійдуть тільки в тому випадку - якщо Ваш пристрій відповідає характеристикам - описаним вище і потребує додаткових знань та розуміння процесу встановлення!

Повна версія гайду:
https://dortania.github.io/OpenCore-Install-Guide/prerequisites.html#prerequisites

## Не забудьте зберегти свої данні, оскільки вони можуть бути втрачені !

------------


#### Для роботи необхідно:

**0) Python**

**1)** Згенерувати унікальний серійний номер вашого фейкового макбук за допомогою программи GenSMBIOS https://github.com/corpnewt/GenSMBIOS
При генеруванні обрати тип: **MacBook9,1**
Детальніше: https://dortania.github.io/OpenCore-Install-Guide/config-laptop.plist/skylake.html#platforminfo

В результаті Ви отримаєте:
-Type
-Serial
-Board Serial
-SmUUID
-Apple ROM

Збережіть цю інформацію в текстовий файл, вона вам згодом знадобиться.

**2)** Далі ці данні необхідно внести в файл config.plist за допомогою программи ProperTree https://github.com/corpnewt/ProperTree у розділі **PlatformInfo**

**-Деякі Пояснення:**
- The Type part gets copied to Generic -> SystemProductName
- The Serial part gets copied to Generic -> SystemSerialNumber.
- The Board Serial part gets copied to Generic -> MLB.
- The SmUUID part gets copied to Generic -> SystemUUID.

Більше інформації: https://dortania.github.io/OpenCore-Install-Guide/config-laptop.plist/skylake.html#platforminfo

Повна інструкція з використання https://dortania.github.io/OpenCore-Install-Guide/config.plist/#creating-your-config-plist

**3)** Створіть завантажувальну  флешку.
-Помістіть папку EFI та папку com.apple.recovery.boot з цього репозиторія в корінь свого відформатованого накопичувача (fat32 / 8Gb+).
-Завантажте OpenCore 0.7.4 (на інших версія не тестовано) https://github.com/acidanthera/OpenCorePkg/releases та розархівуйте
-Завантажте графічний інсталятор MacOS за допомогою інструмента macrecovery, який знаходиться в папці OpenCore, далі /Utilities/macrecovery/
-виконайте команду:
`python macrecovery.py -b Mac-42FD25EABCABB274 -m 00000000000000000 download`
-перемістіть завантажені файли, які з'являться в поточній папці в папку  com.apple.recovery.boot в корені usb (BaseSystem або RecoveryImage files)

**4)** BIOS settings https://dortania.github.io/OpenCore-Install-Guide/config-laptop.plist/skylake.html#intel-bios-settings

**5)** Завантажтесь з usb та перейдіть до встановлення:
-спершу підготуйте розділи диску за допомогою дискової утиліти:

**-Деякі Пояснення:**
GPT formatted disk
розділ EFI partition (ESP) of 210MB minumum (тільки один розділ EFI на диску)
основний розділ для самої macOS - format MAC OS Extended - GUID
-Далі оберіть встановлення.

**6)** PostInstall - переміщення папки EFI на EFI partition
Після успішного встановлення - флешки можна позбутися, якщо перемістити наш завантажувач до розділу EFI
Детальніше: https://dortania.github.io/OpenCore-Post-Install/

Будь ласка, пишіть у issue, якщо у Вас є пропозиції щодо покращення.:smile:
