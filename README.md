# Jarkom-Modul-3-IT25-2024

# Anggota Kelompok
| Nama  | NRP  |
|----------|----------|
| Fikri Aulia As Sa'adi  | 5027231026 |
| Nayla Raissa Azzahra  | 5027231054 |

## Pembuatan Topologi
![image](https://github.com/user-attachments/assets/46562e8e-3f48-4175-bf2a-ef6b1991c4f5)

## Konfigurasi
#### Paradis
```
auto eth0
iface eth0 inet dhcp

auto eth1
iface eth1 inet static
	address 10.76.1.1
	netmask 255.255.255.0

auto eth2
iface eth2 inet static
	address 10.76.2.1
	netmask 255.255.255.0

auto eth3
iface eth3 inet static
	address 10.76.3.1
	netmask 255.255.255.0

auto eth4
iface eth4 inet static
	address 10.76.4.1
	netmask 255.255.255.0
```

#### Annie
```
auto eth0
iface eth0 inet static
	address 10.76.1.2
	netmask 255.255.255.0
	gateway 10.76.1.1
```
#### Berthold
```
auto eth0
iface eth0 inet static
	address 10.76.1.3
	netmask 255.255.255.0
	gateway 10.76.1.1
```
#### Reiner
```
auto eth0
iface eth0 inet static
	address 10.76.1.4
	netmask 255.255.255.0
	gateway 10.76.1.1
```
#### Armin
```
auto eth0
iface eth0 inet static
	address 10.76.2.2
	netmask 255.255.255.0
	gateway 10.76.2.1
```
#### Eren
```
auto eth0
iface eth0 inet static
	address 10.76.2.3
	netmask 255.255.255.0
	gateway 10.76.2.1
```
#### Mikasa
```
auto eth0
iface eth0 inet static
	address 10.76.2.4
	netmask 255.255.255.0
	gateway 10.76.2.1
```
#### Beast
```
auto eth0
iface eth0 inet static
	address 10.76.3.2
	netmask 255.255.255.0
	gateway 10.76.3.1
```
#### Colossal
```
auto eth0
iface eth0 inet static
	address 10.76.3.3
	netmask 255.255.255.0
	gateway 10.76.3.1
```
#### Warhammer
```
auto eth0
iface eth0 inet static
	address 10.76.3.4
	netmask 255.255.255.0
	gateway 10.76.3.1
```
#### Fritz
```
auto eth0
iface eth0 inet static
	address 10.76.4.2
	netmask 255.255.255.0
	gateway 10.76.4.1
```
#### Tybur
```
auto eth0
iface eth0 inet static
	address 10.76.4.3
	netmask 255.255.255.0
	gateway 10.76.4.1
```
#### Zeke dan Erwin
```
auto eth0
iface eth0 inet dhcp
```

