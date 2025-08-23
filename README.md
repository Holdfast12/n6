# n6
настройки для прошивки роутера netis n6  
<a href="https://firmware-selector.openwrt.org/?version=24.10.2&target=ramips%2Fmt7621&id=netis_n6" target="_blank">ПЕРЕЙТИ К СБОРКЕ</a>  
Самые необходимые базовые пакеты:  
```
base-files fstools mtd libc libgcc urandom-seed urngd uci netifd dropbear firewall4 nftables dnsmasq wpad-basic-mbedtls kmod-mt7915-firmware kmod-usb3
```
пакет xmm-modem ставим отдельно от всего
Дополнительные пакеты:
```
sudo xray-core kmod-nft-tproxy
```
