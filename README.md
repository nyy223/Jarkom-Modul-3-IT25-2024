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

## Instalasi Dependensi
#### Paradis (DHCP Relay)
```
apt-get update
apt-get install isc-dhcp-relay -y
```
#### Tybur (DHCP Server)
```
apt-get update
apt-get install isc-dhcp-server -y
```
#### Fritz (DNS Server)
```
apt-get update
apt-get install bind9 -y
```
#### Beast dan Colossal (Load Balancer)
```
apt-get update
apt-get install apache2-utils -y
apt-get install nginx -y
apt-get install lynx -y
```
#### Warhammer (Database Server)
```
apt-get update
apt-get install mariadb-server -y
```
#### Annie, Bertholdt, Reiner (Laravel Worker)
#### Armin, Eren, Mikasa (PHP Worker)
#### Zeke dan Erwin (Client)
```
apt-get update
apt-get install lynx -y
apt-get install htop -y
apt-get install apache2-utils -y
apt-get install jq -y
```

## No.0
Pulau Paradis telah menjadi tempat yang damai selama 1000 tahun, namun kedamaian tersebut tidak bertahan selamanya. Perang antara kaum Marley dan Eldia telah mencapai puncak. Kaum Marley yang dipimpin oleh Zeke, me-register domain name marley.yyy.com untuk worker Laravel mengarah pada Annie. Namun ternyata tidak hanya kaum Marley saja yang berinisiasi, kaum Eldia ternyata sudah mendaftarkan domain name eldia.yyy.com untuk worker PHP (0) mengarah pada Armin.

#### Membuat Script
