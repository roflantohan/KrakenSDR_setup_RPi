# KrakenSDR Setup

## Встановлення образу ОС

Посилання 1: https://github.com/krakenrf/heimdall_daq_fw/tree/development?tab=readme-ov-file#usage

1. Завантажити образ системи для Raspberry Pi 4 за посиланнями(https://mega.nz/folder/8T1jiIzR#_1Ujs4Eoy0wdRib9eHCVSg або https://drive.google.com/drive/folders/14NuCOGM1Fh1QypDNMngXEepKYRBsG--B?usp=sharing).

2. За допомогою "Raspberry Pi Imager"(https://www.raspberrypi.com/software) або "BalenaEtcher"(https://etcher.balena.io) встановити образ на SD карту.

## Користування WEB інтерфейсом KrakenSDR

Посилання 2: https://github.com/krakenrf/krakensdr_docs/wiki/02.-Direction-Finding-Quickstart-Guide

1. Для користування WEB інтерфейсом достатньо підключити RPi та ПК до однієї мобільної мережі (KrakenAndroid/KrakenAndroid - необхідні назва та пароль мережі) або підключити ПК до мережі "krakensdr"(пароль: krakensdr).
2. Далі потрібно дізнатись через налаштування мобільної мережі на телефоні ip адресу RPi 5 та доступ то web інтерфейсу знаходиться: IP_ADDR:8080 або 192.168.50.5:8080 (у випадку мережі "krakensdr").

## Налаштування KrakenSDR для роботи з GNURadio:

### (ОПЦІОНАЛЬНО)
1. Для віддаленої роботи з графічною оболонкою завантажуємо на RPi Remote Desktop Protocol:
```
sudo apt-get install xrdp -y
```
2. Через додаток Remote Desktop Connection (Windows) (вбудовано), Reminna (Linux)(https://remmina.org/how-to-install-remmina/#ubuntu), Microsoft Remote Desktop (MacOS) (AppStore) підключаємось за IP адресою, використовуючи логін та пароль:
```
Логін/Пароль: krakenrf/krakensdr
```
### (ОБОВ'ЯЗКОВО)
Посилання 3: https://github.com/krakenrf/gr-krakensdr

3. Відкримаємо термінал та виконуємо команди:
```
cd /boot
sudo mv start_kraken.sh start_kraken.sh_stop
cd ~/krakensdr_doa/
```
4. В головній директорії(krakensdr_doa) знаходимо файл ./heimdall_daq_fw/Firmware/daq_chain_config.ini та змінюємо параметр:
```
[data_interface]
out_data_iface_type = eth
```
5. Копіюємо файли heimdall_only_start.sh та heimdall_only_stop.sh з цього репозиторію до головної директорії(krakensdr_doa)
5. Замінюємо файл kill.sh з тим, що в репозиторії за шляхом ./krakensdr_doa/krakensdr_doa/
6. Запускаємо файл heimdall_only_start.sh:
```
bash ./heimdall_only_start.sh
```

## Встановлення GNURadio та KrakenSDR GR Blocks для Linux

Примітка: даний пункт можна робити на RPi чи на ПК

1. Встановлюємо GNURadio:
```
sudo apt-get install gnuradio
```
2. Виконуємо компіляцію krakenSDR gr blocks:
```
sudo apt-get install gnuradio-dev cmake libspdlog-dev clang-format

git clone https://github.com/krakenrf/gr-krakensdr

cd gr-krakensdr
mkdir build
cd build
cmake ..
make
sudo make install
```

3. Запускаємо GNURadio Companion у терміналі:
```
gnuradio-companion
```

Посилання встановлення для Windows: https://www.redgo.ch/krakensdr/gr-krakensdr_natively_on_Windows.pdf
