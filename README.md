# Установка и настройка ПО на станции ЕГЭ под Linux

Скрипты предназначены для установки КриптоПРО CSP и драйверов для оборудования, применяемого на ЕГЭ в Свердловской области:
- Pantum BP5100DN
- Avision AV332U
- Fujitsu SP-1120

# Alt Linux 10.4

Запускаем эмулятор терминала и вводим команды:

```
# переходим под root
su -
# обновляем пакеты
apt-get update
# установка КриптоПРО CSP
wget -O /tmp/linux-amd64.tgz "https://ou4.ru/f/linux-amd64.tgz" && cd /tmp && tar -xzf linux-amd64.tgz && cd /tmp/linux-amd64 && apt-get install -y cryptopro-preinstall && apt-get install cprocsp-curl* lsb-cprocsp-base* lsb-cprocsp-capilite* lsb-cprocsp-kc1-64* lsb-cprocsp-rdr-64* && apt-get install -y cprocsp-rdr-gui-gtk* cprocsp-rdr-rutoken* cprocsp-rdr-pcsc* lsb-cprocsp-pkcs11* pcsc-lite-rutokens pcsc-lite-ccid && apt-get install -y cprocsp-rdr-cryptoki* && apt-get install -y cprocsp-cptools*
# установка драйверов для Pantum BP5100DN
wget -O /tmp/pantum.zip "https://www.pantum.ru/wp-content/uploads/2024/06/pantum-1_1_99-alt3_x86_64-8.zip" && unzip -o /tmp/pantum.zip -d /tmp/  && apt-get install -y /tmp/pantum-1.1.99-alt3.x86_64.rpm
# установка драйверов для Fujitsu SP-1120
epm play -y pfusp && cp /usr/lib/sane/libsane-pfusp* /usr/lib64/sane/
# установка прав доступа к Fujitsu SP-1120
wget -O /etc/udev/rules.d/60-pfusp.rules "https://raw.githubusercontent.com/olegpecherkin/ege_alt_2026/refs/heads/main/60-pfusp.rules"
# установка драйверов для Avision AV332U
wget -O /tmp/avision.tar.gz "https://docscan.ru/media/drivers/AD345GN_LINUX_DRIVER/scanner-driver-avision_rpm64_0.1.0.24165_20240613.tar.gz" && cd /tmp && tar -xzf /tmp/avision.tar.gz && rpm -Uvh /tmp/scanner-driver-avision-0.1.0-24165.x86_64.rpm
```

# Astra Linux 1.8.4

Запускаем терминала и вводим команды:

```
# переходим под root
sudo su -
# отключаем cdrom репозиторий
sudo sed -i 's/^deb cdrom:/#deb cdrom:/' /etc/apt/sources.list
# включаем интернет репозиторий
sudo sed -i 's/^#deb https:\/\/download.astralinux/deb https:\/\/download.astralinux/' /etc/apt/sources.list
# обновляем пакеты
apt update
# установка КриптоПРО CSP
wget -O /tmp/linux-amd64_deb.tgz "https://ou4.ru/f/linux-amd64_deb.tgz" && cd /tmp && tar -xzf linux-amd64_deb.tgz && cd /tmp/linux-amd64_deb && apt install -y ./cprocsp-curl* ./lsb-cprocsp-base* ./lsb-cprocsp-capilite* ./lsb-cprocsp-kc1-64* ./lsb-cprocsp-rdr-64* && apt install -y ./cprocsp-rdr-gui-gtk* ./cprocsp-rdr-rutoken* ./cprocsp-rdr-pcsc* ./lsb-cprocsp-pkcs11* && apt install -y ./cprocsp-rdr-cryptoki* && apt install -y ./cprocsp-cptools* && apt install -y ./cprocsp-pki* ./cprocsp-rdr-* ./lsb-cprocsp-ca-certs* ./lsb-cprocsp-import-ca-certs*
# установка librtpkcs11ecp
wget -O /tmp/librtpkcs11ecp_2.18.4.0-1_amd64.deb "https://ou4.ru/f/librtpkcs11ecp_2.18.4.0-1_amd64.deb" && dpkg -i /tmp/librtpkcs11ecp_2.18.4.0-1_amd64.deb
# установка драйверов для Pantum BP5100DN
wget -O /tmp/pantum.zip "https://www.pantum.ru/wp-content/uploads/2025/06/pantum-r_1.0.17-1astra1_amd64.deb_.zip" && unzip -o /tmp/pantum.zip -d /tmp/ && dpkg -i /tmp/pantum-r_1.0.17-1astra1_amd64.deb
# установка драйверов для Fujitsu SP-1120
wget -O /tmp/pfusp.deb "https://origin.pfultd.com/downloads/IMAGE/driver/ubuntu/221/pfusp-ubuntu_2.2.1_amd64.deb" && dpkg -i /tmp/pfusp.deb
# установка прав доступа к Fujitsu SP-1120
wget -O /etc/udev/rules.d/60-pfusp.rules "https://raw.githubusercontent.com/olegpecherkin/ege_alt_2026/refs/heads/main/60-pfusp.rules"
# установка драйверов для Avision AV332U
wget -O /tmp/avision.tar.gz "https://disk.astralinux.ru/s/67a2Sx8LokJksoK/download/scanner-driver-avision_deb64_0.1.0.24165_20240613.tar.gz" && cd /tmp && tar -xzf /tmp/avision.tar.gz && dpkg -i scanner-driver-avision_0.1.0-24165_amd64.deb

```
