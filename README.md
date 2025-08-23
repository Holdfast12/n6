# n6
настройки для прошивки роутера netis n6  
<a href="https://firmware-selector.openwrt.org/?version=24.10.2&target=ramips%2Fmt7621&id=netis_n6" target="_blank">ПЕРЕЙТИ К СБОРКЕ</a>  
Самые необходимые базовые пакеты:  
```
base-files fstools kmod-crypto-hw-eip93 kmod-nft-offload mtd libc libgcc urandom-seed urngd uci netifd dropbear firewall4 nftables dnsmasq wpad-basic-mbedtls kmod-mt7915-firmware kmod-usb3 opkg
```
пакет xmm-modem ставим отдельно от всего
Дополнительные пакеты:
```
xray-core kmod-nft-tproxy python3-light
```
```
uci set system.@system[0].hostname="router"
uci set system.@system[0].timezone='MSK-3'
uci set dropbear.@dropbear[0].Port=2000
uci set network.lan.ipaddr='192.168.3.1'
uci commit dropbear
uci commit system
sed -i 's|^root:[^:]*|root:$1$1PVun.qU$S2zn1FroxL.IW4z8SVTLs0|' /etc/shadow
cat <<EOF > /etc/dropbear/authorized_keys
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAACAQCw2z1pPtthnNbZQPZiz+g4Z+yC0oqygdJ9HLoMWbjMELSe+CVRTGp9l0fcfU4Tfg/bsOIRzCsq7VO4sf3736Bm9y91Ex0HlKjOSpkGkKvu1dEML2n5oN7n6iX0hf2+qzeTLEVfSeJNXNerV+FiQIxzSgstxDPfSGcA1xUBb1HZc+Yzny+IxZ6dXvDiErDEX3E+fco0igz5jooekz+VYgsC8Fy+BehjAjnLZsXeBsZ2nHAu3zZVRcQBRuuV+SXFHrPD2B/YnhYeRj3SaRhhIPxquRMXR3ldpydrDtHIEorStwX7rUduRbYW4qWEkiBPgWn3CBzfzrNlzz2c2Gyh/jU713ILpfIE6ov9STmCG9F7xlHMSnK17sJxIPehMlMhDygyz7BP7l9dQRz299wB5+1u/iIUT7LaoesP5DF0vbfaykJAylGkb7wZvIiwN4gcib8Oo7N1051GItJbOqVZw3IxOHHW63iabVMBP3AKWNuTq5sf1sQ5ar66Nf8UBJbsNw+7tY+0yc4/Y4c2DOsR+/fVm84eh8bNwMzfcnxYp27jYGPJTLApOWIimjFHlEJFqNdKfvuoJk2BWEelUQneNq/BG/Lwkbo+iP00AIdixWiexziRIgydrAIcshYdRDzyXCsjyCfvDgrcmAmLo0WlaoWubgEHyZxSsiksSdqX5fzFjQ== admin@internet0000004
EOF
chmod 600 /etc/dropbear/authorized_keys
/etc/init.d/dropbear restart
/etc/init.d/system restart
```
