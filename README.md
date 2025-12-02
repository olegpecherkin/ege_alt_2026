# Установка и настройка ПО на станции ЕГЭ под Alt Linux

Запускаем эмулятор терминал и вводим команды:

```
# переходим под root
su -
# обновляем пакеты
apt-get update
# установка КриптоПРО CSP
wget -O /tmp/linux-amd64.tgz "https://ou4.ru/f/linux-amd64.tgz" && cd /tmp && tar -xzf linux-amd64.tgz && cd /tmp/linux-amd64 && apt-get install -y cryptopro-preinstall && apt-get install cprocsp-curl* lsb-cprocsp-base* lsb-cprocsp-capilite* lsb-cprocsp-kc1-64* lsb-cprocsp-rdr-64* && apt-get install -y cprocsp-rdr-gui-gtk* cprocsp-rdr-rutoken* cprocsp-rdr-pcsc* lsb-cprocsp-pkcs11* pcsc-lite-rutokens pcsc-lite-ccid && apt-get install -y cprocsp-rdr-cryptoki* && apt-get install -y cprocsp-cptools*
# установка драйверов для Pantum BP5100DN
wget -O /tmp/pantum.zip "https://www.pantum.ru/wp-content/uploads/2024/06/pantum-1_1_99-alt3_x86_64-8.zip" && unzip -o /tmp/pantum.zip -d /tmp/  && apt-get install -y /tmp/pantum-1.1.99-alt3.x86_64.rpm
# установка драйверов для Avision AV332U
wget -O /tmp/avision.tar.gz "https://docscan.ru/media/drivers/AD345GN_LINUX_DRIVER/scanner-driver-avision_rpm64_0.1.0.24165_20240613.tar.gz" && cd /tmp && tar -xzf /tmp/avision.tar.gz && rpm -Uvh /tmp/scanner-driver-avision-0.1.0-24165.x86_64.rpm
# установка драйверов для Fujitsu SP-1120
epm play -y pfusp && copy /usr/lib/sane/libsane-pfusp* /usr/lib64/sane/
# установка прав доступа к Fujitsu SP-1120
   echo -ne "ACTION!=\"add\", GOTO=\"pfusp_scanner_rules_end\"\n" > /etc/udev/rules.d/60-pfusp.rules 
   echo -ne "ENV{DEVTYPE}!=\"usb_device\", GOTO=\"pfusp_scanner_rules_end\"\n" >> /etc/udev/rules.d/60-pfusp.rules 
   echo -ne "ATTR{idVendor}!=\"04c5\", GOTO=\"pfusp_scanner_rules_end\"\n\n" >> /etc/udev/rules.d/60-pfusp.rules 
   echo -ne "LABEL=\"pfusp_scanner_rules_begin\"\n" >> /etc/udev/rules.d/60-pfusp.rules 
   echo -ne "#SP-1120\nATTRS{idProduct}==\"1473\", ENV{pfusp_driver}=\"yes\"\n" >> /etc/udev/rules.d/60-pfusp.rules 
   echo -ne "#SP-1125\nATTRS{idProduct}==\"1475\", ENV{pfusp_driver}=\"yes\"\n" >> /etc/udev/rules.d/60-pfusp.rules 
   echo -ne "#SP-1130\nATTRS{idProduct}==\"1476\", ENV{pfusp_driver}=\"yes\"\n" >> /etc/udev/rules.d/60-pfusp.rules 
   echo -ne "#SP-1425\nATTRS{idProduct}==\"1524\", ENV{pfusp_driver}=\"yes\"\n" >> /etc/udev/rules.d/60-pfusp.rules 
   echo -ne "#SP-1120N\nATTRS{idProduct}==\"1625\", ENV{pfusp_driver}=\"yes\"\n" >> /etc/udev/rules.d/60-pfusp.rules 
   echo -ne "#SP-1125N\nATTRS{idProduct}==\"1626\", ENV{pfusp_driver}=\"yes\"\n" >> /etc/udev/rules.d/60-pfusp.rules 
   echo -ne "#SP-1130N\nATTRS{idProduct}==\"1627\", ENV{pfusp_driver}=\"yes\"\n" >> /etc/udev/rules.d/60-pfusp.rules 
   echo -ne "# Give scanner users read/write permissions on the device.\n" >> /etc/udev/rules.d/60-pfusp.rules 
   echo -ne "ENV{pfusp_driver}==\"yes\", MODE=\"0666\", OWNER=\"root\", GROUP=\"root\"\n\n" >> /etc/udev/rules.d/60-pfusp.rules 
   echo -ne "# Device detection by pfusp depends on libsane_matched being set.\n" >> /etc/udev/rules.d/60-pfusp.rules 
   echo -ne "ENV{pfusp_driver}==\"yes\", ENV{libsane_matched}=\"yes\"\n\n" >> /etc/udev/rules.d/60-pfusp.rules 
   echo -ne "LABEL=\"pfusp_scanner_rules_end\"\n" >> /etc/udev/rules.d/60-pfusp.rules 
```
