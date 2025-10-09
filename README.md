# n6
настройки для прошивки роутера netis n6  
<a href="https://firmware-selector.openwrt.org/?version=24.10.3&target=ramips%2Fmt7621&id=netis_n6" target="_blank">ПЕРЕЙТИ К СБОРКЕ</a>  
Самые необходимые базовые пакеты:  
```
base-files ca-bundle dnsmasq dropbear firewall4 fstools kmod-nft-offload libc libgcc libustream-mbedtls logd mtd netifd nftables opkg procd uci uclient-fetch urandom-seed urngd wpad-basic-mbedtls kmod-mt7915-firmware kmod-usb3 kmod-crypto-hw-eip93
```
пакет xmm-modem ставим отдельно от всего
Дополнительные пакеты:
```
sudo kmod-nft-tproxy rsync tcpdump prometheus-node-exporter-lua prometheus-node-exporter-lua-nat_traffic prometheus-node-exporter-lua-netstat prometheus-node-exporter-lua-openwrt prometheus-node-exporter-lua-wifi prometheus-node-exporter-lua-wifi_stations
```
```
uci set system.@system[0].hostname="router"
uci set system.@system[0].timezone='MSK-3'
uci commit system
/etc/init.d/system restart
uci set network.lan.ipaddr='192.168.3.1'
uci commit network
/etc/init.d/network restart
uci set dropbear.@dropbear[0].Port=2000
uci commit dropbear
/etc/init.d/dropbear restart
sed -i 's|^root:[^:]*|root:$5$WXMblhlNpFKxhwRo$DcqKlxhGzAMFOIJAIcMDJ.IuPWIYO3H2mt5xFrN6Y5A|' /etc/shadow
cat <<EOF > /etc/dropbear/authorized_keys
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAACAQCw2z1pPtthnNbZQPZiz+g4Z+yC0oqygdJ9HLoMWbjMELSe+CVRTGp9l0fcfU4Tfg/bsOIRzCsq7VO4sf3736Bm9y91Ex0HlKjOSpkGkKvu1dEML2n5oN7n6iX0hf2+qzeTLEVfSeJNXNerV+FiQIxzSgstxDPfSGcA1xUBb1HZc+Yzny+IxZ6dXvDiErDEX3E+fco0igz5jooekz+VYgsC8Fy+BehjAjnLZsXeBsZ2nHAu3zZVRcQBRuuV+SXFHrPD2B/YnhYeRj3SaRhhIPxquRMXR3ldpydrDtHIEorStwX7rUduRbYW4qWEkiBPgWn3CBzfzrNlzz2c2Gyh/jU713ILpfIE6ov9STmCG9F7xlHMSnK17sJxIPehMlMhDygyz7BP7l9dQRz299wB5+1u/iIUT7LaoesP5DF0vbfaykJAylGkb7wZvIiwN4gcib8Oo7N1051GItJbOqVZw3IxOHHW63iabVMBP3AKWNuTq5sf1sQ5ar66Nf8UBJbsNw+7tY+0yc4/Y4c2DOsR+/fVm84eh8bNwMzfcnxYp27jYGPJTLApOWIimjFHlEJFqNdKfvuoJk2BWEelUQneNq/BG/Lwkbo+iP00AIdixWiexziRIgydrAIcshYdRDzyXCsjyCfvDgrcmAmLo0WlaoWubgEHyZxSsiksSdqX5fzFjQ==
EOF
chmod 600 /etc/dropbear/authorized_keys
/etc/init.d/dnsmasq restart
```
