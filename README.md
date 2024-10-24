# Jarkom-Modul-3-IT25-2024

# Anggota Kelompok
| Nama  | NRP  |
|----------|----------|
| Fikri Aulia As Sa'adi  | 5027231026 |
| Nayla Raissa Azzahra  | 5027231054 |

## Pembuatan Topologi
![image](https://github.com/user-attachments/assets/46562e8e-3f48-4175-bf2a-ef6b1991c4f5)

## Konfigurasi
### Paradis
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

### Annie
```
auto eth0
iface eth0 inet static
	address 10.76.1.2
	netmask 255.255.255.0
	gateway 10.76.1.1
```
### Berthold
```
auto eth0
iface eth0 inet static
	address 10.76.1.3
	netmask 255.255.255.0
	gateway 10.76.1.1
```
### Reiner
```
auto eth0
iface eth0 inet static
	address 10.76.1.4
	netmask 255.255.255.0
	gateway 10.76.1.1
```
### Armin
```
auto eth0
iface eth0 inet static
	address 10.76.2.2
	netmask 255.255.255.0
	gateway 10.76.2.1
```
### Eren
```
auto eth0
iface eth0 inet static
	address 10.76.2.3
	netmask 255.255.255.0
	gateway 10.76.2.1
```
### Mikasa
```
auto eth0
iface eth0 inet static
	address 10.76.2.4
	netmask 255.255.255.0
	gateway 10.76.2.1
```
### Beast
```
auto eth0
iface eth0 inet static
	address 10.76.3.2
	netmask 255.255.255.0
	gateway 10.76.3.1
```
### Colossal
```
auto eth0
iface eth0 inet static
	address 10.76.3.3
	netmask 255.255.255.0
	gateway 10.76.3.1
```
### Warhammer
```
auto eth0
iface eth0 inet static
	address 10.76.3.4
	netmask 255.255.255.0
	gateway 10.76.3.1
```
### Fritz
```
auto eth0
iface eth0 inet static
	address 10.76.4.2
	netmask 255.255.255.0
	gateway 10.76.4.1
```
### Tybur
```
auto eth0
iface eth0 inet static
	address 10.76.4.3
	netmask 255.255.255.0
	gateway 10.76.4.1
```
### Zeke dan Erwin
```
auto eth0
iface eth0 inet dhcp
```

## Instalasi Dependensi
### Paradis (DHCP Relay)
```
apt-get update
apt-get install isc-dhcp-relay -y
```
### Tybur (DHCP Server)
```
apt-get update
apt-get install isc-dhcp-server -y
```
### Fritz (DNS Server)
```
apt-get update
apt-get install bind9 -y
```
### Beast dan Colossal (Load Balancer)
```
apt-get update
apt-get install apache2-utils -y
apt-get install nginx -y
apt-get install lynx -y
```
### Warhammer (Database Server)
```
apt-get update
apt-get install mariadb-server -y
```
### Annie, Bertholdt, Reiner (Laravel Worker)
### Armin, Eren, Mikasa (PHP Worker)
### Zeke dan Erwin (Client)
```
apt-get update
apt-get install lynx -y
apt-get install htop -y
apt-get install apache2-utils -y
apt-get install jq -y
```

## No.0
Pulau Paradis telah menjadi tempat yang damai selama 1000 tahun, namun kedamaian tersebut tidak bertahan selamanya. Perang antara kaum Marley dan Eldia telah mencapai puncak. Kaum Marley yang dipimpin oleh Zeke, me-register domain name marley.yyy.com untuk worker Laravel mengarah pada Annie. Namun ternyata tidak hanya kaum Marley saja yang berinisiasi, kaum Eldia ternyata sudah mendaftarkan domain name eldia.yyy.com untuk worker PHP (0) mengarah pada Armin.

### Membuat script di Fritz untuk memberikan domain marley.it25.com yang menyambung ke IP Annie, dan domain eldia.it25.com yang menyambung ke IP Armin
>Fritz/Script0.sh
```
apt-get update
apt-get install bind9 -y

forward="options {
directory \"/var/cache/bind\";
forwarders {
  	   192.168.122.1;
};

allow-query{any;};
listen-on-v6 { any; };
};
"
echo "$forward" > /etc/bind/named.conf.options

echo "zone \"marley.it25.com\" {
	type master;
	file \"/etc/bind/jarkom/marley.it25.com\";
};

zone \"eldia.it25.com\" {
	type master;
	file \"/etc/bind/jarkom/eldia.it25.com\";
};
" > /etc/bind/named.conf.local

mkdir /etc/bind/jarkom

riegel="
;
;BIND data file for local loopback interface
;
\$TTL    604800
@    IN    SOA    marley.it25.com. root.marley.it25.com. (
        2        ; Serial
                604800        ; Refresh
                86400        ; Retry
                2419200        ; Expire
                604800 )    ; Negative Cache TTL
;                   
@    IN    NS    marley.it25.com.
@       IN    A    10.76.1.2
"
echo "$riegel" > /etc/bind/jarkom/marley.it25.com

granz="
;
;BIND data file for local loopback interface
;
\$TTL    604800
@    IN    SOA    eldia.it25.com. root.eldia.it25.com. (
        2        ; Serial
                604800        ; Refresh
                86400        ; Retry
                2419200        ; Expire
                604800 )    ; Negative Cache TTL
;                   
@    IN    NS    eldia.it25.com.
@       IN    A    10.76.2.2
"
echo "$granz" > /etc/bind/jarkom/eldia.it25.com

service bind9 restart
```
### Test di client menggunakan IP Static Zeke (10.76.1.5) dan Erwin (10.76.2.5)
![image](https://github.com/user-attachments/assets/b856f626-e063-414e-ad47-e25b21ffb104)
![image](https://github.com/user-attachments/assets/253ca319-7736-4c1b-9690-28b8260e11a3)

## No.1-5
Lakukan konfigurasi sesuai dengan peta yang sudah diberikan.

Jauh sebelum perang dimulai, ternyata para keluarga bangsawan, Tybur dan Fritz, telah membuat kesepakatan sebagai berikut:
1. Semua Client harus menggunakan konfigurasi ip address dari keluarga Tybur (dhcp).
2. Client yang melalui bangsa marley mendapatkan range IP dari [prefix IP].1.05 - [prefix IP].1.25 dan [prefix IP].1.50 - [prefix IP].1.100 (2)
3. Client yang melalui bangsa eldia mendapatkan range IP dari [prefix IP].2.09 - [prefix IP].2.27 dan [prefix IP].2 .81 - [prefix IP].2.243 (3)
4. Client mendapatkan DNS dari keluarga Fritz dan dapat terhubung dengan internet melalui DNS tersebut (4)
5. Dikarenakan keluarga Tybur tidak menyukai kaum eldia, maka mereka hanya meminjamkan ip address ke kaum eldia selama 6 menit. Namun untuk kaum marley, keluarga Tybur meminjamkan ip address selama 30 menit. Waktu maksimal dialokasikan untuk peminjaman alamat IP selama 87 menit. (5)

### Membuat script untuk menghubungkan DHCP Relay (Paradis) dengan DHCP Server (Tybur)
>Paradis/Script1.sh
```
apt-get update
apt install isc-dhcp-relay -y

service isc-dhcp-relay start 

echo '# Defaults for isc-dhcp-relay initscript

# sourced by /etc/init.d/isc-dhcp-relay
# installed at /etc/default/isc-dhcp-relay by the maintainer scripts

#
# This is a POSIX shell fragment
#

# What servers should the DHCP relay forward requests to?
SERVERS="10.76.4.3" 

# On what interfaces should the DHCP relay (dhrelay) serve DHCP requests?
INTERFACES="eth1 eth2 eth3 eth4"

# Additional options that are passed to the DHCP relay daemon?
OPTIONS=""' > /etc/default/isc-dhcp-relay


echo net.ipv4.ip_forward=1 > /etc/sysctl.conf

service isc-dhcp-relay restart
```

>Tybur/Script1.sh
```
apt-get update
apt-get install isc-dhcp-server -y

echo 'INTERFACESv4="eth0"
INTERFACESv6=""
' > /etc/default/isc-dhcp-server

subnet="option domain-name \"example.org\";
option domain-name-servers ns1.example.org, ns2.example.org;

default-lease-time 600;
max-lease-time 7200;

ddns-update-style-none;

subnet 10.76.1.0 netmask 255.255.255.0 {
    range 10.76.1.5 10.76.1.25;
    range 10.76.1.50 10.76.1.100;
    option routers 10.76.1.1;
    option broadcast-address 10.76.1.255;
    option domain-name-servers 10.76.4.2;
    default-lease-time 360;
    max-lease-time 5220;
}

subnet 10.76.2.0 netmask 255.255.255.0 {
    range 10.76.2.9 10.76.2.27;
    range 10.76.2.81 10.76.2.243;
    option routers 10.76.2.1;
    option broadcast-address 10.76.2.255;
    option domain-name-servers 10.76.4.2;
    default-lease-time 1800;
    max-lease-time 5220;
}

subnet 10.76.3.0 netmask 255.255.255.0 {
}

subnet 10.76.4.0 netmask 255.255.255.0 {
}

"
echo "$subnet" > /etc/dhcp/dhcpd.conf

service isc-dhcp-server restart
```

### Test setelah client mendapat IP Dynamic dengan konfigurasi lease time yang sudah ditentukan
![image](https://github.com/user-attachments/assets/cb94d6a1-d918-4004-82c0-a6f4950f2231)
![image](https://github.com/user-attachments/assets/770a27fa-170d-4ce8-8219-77bd2a564276)

### Test ping marley.it25.com dan eldia.it25.com setelah mendapat ip dynamic
![image](https://github.com/user-attachments/assets/3dbf6b7c-1fc4-4aed-9f7b-154b44766ca4)
![image](https://github.com/user-attachments/assets/bb1a0ba2-00e5-44bb-9ac5-d74d257316d7)

## No.6
Armin berinisiasi untuk memerintahkan setiap worker PHP untuk melakukan konfigurasi virtual host untuk website berikut https://intip.in/BangsaEldia dengan menggunakan php 7.3 (6)

### Membuat script untuk menambahkan nameserver IP DHCP Server, menginstall PHP, mendownload kebutuhan untuk PHP di link yang disediakan, mengekstrak, memindah dan melakukan symlink pada file yang sudah di download, lalu mengatur konfigurasi Nginx
>Armin, Eren, Mikasa/Script6.sh
```
#!/bin/bash

# Tambahkan nameserver
echo nameserver 10.76.4.3 >> /etc/resolv.conf

# Update dan install paket
apt-get update

# Instal Nginx dan PHP 7.3 bersama dengan PHP-FPM
apt-get install nginx -y
apt-get install lynx -y
apt-get install php7.3 php7.3-fpm php7.3-mysql -y   # Install PHP 7.3 dan modul yang diperlukan
apt-get install wget -y
apt-get install unzip -y
apt-get install rsync -y    # Install rsync untuk transfer file
service nginx start
service php7.3-fpm start    # Jalankan PHP-FPM versi 7.3

# Download file modul-3.zip dari Google Drive
wget --no-check-certificate 'https://drive.google.com/uc?export=download&id=1ufulgiWyTbOXQcow11JkXG7safgLq1y-' -O '/var/www/modul-3.zip'

# Ekstrak file zip
unzip -o /var/www/modul-3.zip -d /var/www/
rm /var/www/modul-3.zip

# Pindahkan isi dari folder modul-3 ke marley.it25.com menggunakan rsync
rsync -av /var/www/modul-3/ /var/www/marley.it25.com/

# Hapus folder modul-3 yang kosong
rm -r /var/www/modul-3

# Konfigurasi Nginx
cp /etc/nginx/sites-available/default /etc/nginx/sites-available/marley.it25.com

# Periksa apakah symbolic link sudah ada, jika iya, hapus dulu
if [ -L /etc/nginx/sites-enabled/marley.it25.com ]; then
    rm /etc/nginx/sites-enabled/marley.it25.com
fi

# Buat symbolic link baru
ln -s /etc/nginx/sites-available/marley.it25.com /etc/nginx/sites-enabled/

# Periksa apakah default sudah ada, jika iya, hapus
if [ -L /etc/nginx/sites-enabled/default ]; then
    rm /etc/nginx/sites-enabled/default
fi

# Membuat konfigurasi Nginx untuk marley.it25.com
echo 'server {
     listen 80;
     server_name _;

     root /var/www/marley.it25.com/;
     index index.php index.html index.htm;

     location / {
         try_files $uri $uri/ /index.php?$query_string;
     }

     location ~ \.php$ {
         include snippets/fastcgi-php.conf;
         fastcgi_pass unix:/run/php/php7.3-fpm.sock;
         fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
         include fastcgi_params;
     }
 }' > /etc/nginx/sites-available/marley.it25.com

# Restart Nginx dan PHP-FPM 7.3
service php7.3-fpm restart
service nginx restart
```

### Test di client Zeke dan Erwin
```
lynx 10.76.2.2
```
![Screenshot 2024-10-22 123416](https://github.com/user-attachments/assets/00684227-522e-4379-a120-6e08219b7a92)

```
lynx 10.76.2.3
```
![image](https://github.com/user-attachments/assets/c4cd9899-5e11-437e-af68-138e5d10d8a8)

```
lynx 10.76.2.4
```
![image](https://github.com/user-attachments/assets/31370c8a-20dc-4235-99c1-288a6caaabb8)

## No.7
Dikarenakan Armin sudah mendapatkan kekuatan titan colossal, maka bantulah kaum eldia menggunakan colossal agar dapat bekerja sama dengan baik. Kemudian lakukan testing dengan 6000 request dan 200 request/second. (7)

### Membuat script untuk konfigurasi 
>Colossal/Script7.sh
```
#!/bin/bash

# Konfigurasi nameserver
echo nameserver 10.76.4.3 > /etc/resolv.conf

# Update dan install paket yang diperlukan
apt-get update
apt-get install apache2-utils -y   # Untuk testing menggunakan ApacheBench (ab)
apt-get install nginx -y           # Install Nginx sebagai load balancer
apt-get install lynx -y            # Install lynx untuk akses web via command line

# Konfigurasi Nginx untuk load balancing menggunakan PHP load balancer
cp /etc/nginx/sites-available/default /etc/nginx/sites-available/colossal_lb

# Tambahkan konfigurasi load balancing
echo '
    upstream php_backend {
        server 10.76.2.2;  # Armin
        server 10.76.2.3;  # Eren
        server 10.76.2.4;  # Mikasa
    }

    server {
        listen 80;
        root /var/www/html;
        index index.html index.htm index.nginx-debian.html;
        server_name _;

        location / {
            proxy_pass http://php_backend;
            proxy_set_header Host $host;
            proxy_set_header X-Real-IP $remote_addr;
            proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
            proxy_set_header X-Forwarded-Proto $scheme;
        }
    }
' > /etc/nginx/sites-available/colossal_lb

# Aktifkan konfigurasi load balancer
ln -sf /etc/nginx/sites-available/colossal_lb /etc/nginx/sites-enabled/

# Hapus default jika masih ada
if [ -f /etc/nginx/sites-enabled/default ]; then
    rm /etc/nginx/sites-enabled/default
fi

# Restart layanan Nginx agar konfigurasi baru berlaku
service nginx restart
```

### Melakukan test di client
```
ab -n 6000 -c 200 http://10.76.3.3/
```
![image](https://github.com/user-attachments/assets/d4551962-045a-4cf3-9b6a-ec8a5e0995a0)
![image](https://github.com/user-attachments/assets/ed5e4f04-571c-4665-bbda-eeedb183500f)

## No.8
Karena Erwin meminta “laporan kerja Armin”, maka dari itu buatlah analisis hasil testing dengan 1000 request dan 75 request/second untuk masing-masing algoritma Load Balancer dengan ketentuan sebagai berikut:
1. Nama Algoritma Load Balancer
2. Report hasil testing pada Apache Benchmark
3. Grafik request per second untuk masing masing algoritma. 
4. Analisis (8)

### Membuat script untuk konfigurasi setiap algoritma load balancer
>Colossal/Script8.sh
```
#!/bin/bash

# Konfigurasi Round Robin
cp /etc/nginx/sites-available/default /etc/nginx/sites-available/round_robin

echo '
    upstream round-robin {
        server 10.76.2.2;
        server 10.76.2.3;
        server 10.76.2.4;
    }

    server {
        listen 81;
        root /var/www/html;

        index index.html index.htm index.nginx-debian.html;

        server_name _;

        location / {
            proxy_pass http://round-robin;
        }
    }
' > /etc/nginx/sites-available/round_robin

# Konfigurasi Weighted Round Robin
cp /etc/nginx/sites-available/default /etc/nginx/sites-available/weight_round_robin

echo '
    upstream weight_round-robin {
        server 10.76.2.2 weight=3;
        server 10.76.2.3 weight=2;
        server 10.76.2.4 weight=1;
    }

    server {
        listen 82;
        root /var/www/html;

        index index.html index.htm index.nginx-debian.html;

        server_name _;

        location / {
            proxy_pass http://weight_round-robin;
        }
    }
' > /etc/nginx/sites-available/weight_round_robin

# Konfigurasi Generic Hash
cp /etc/nginx/sites-available/default /etc/nginx/sites-available/generic_hash

echo '
    upstream generic_hash {
        hash $request_uri consistent;
        server 10.76.2.2 weight=3;
        server 10.76.2.3 weight=2;
        server 10.76.2.4 weight=1;
    }

    server {
        listen 83;
        root /var/www/html;

        index index.html index.htm index.nginx-debian.html;

        server_name _;

        location / {
            proxy_pass http://generic_hash;
        }
    }
' > /etc/nginx/sites-available/generic_hash

# Konfigurasi IP Hash
cp /etc/nginx/sites-available/default /etc/nginx/sites-available/ip_hash

echo '
    upstream ip_hash {
        ip_hash;
        server 10.76.2.2;
        server 10.76.2.3;
        server 10.76.2.4;
    }

    server {
        listen 84;
        root /var/www/html;

        index index.html index.htm index.nginx-debian.html;

        server_name _;

        location / {
            proxy_pass http://ip_hash;
        }
    }
' > /etc/nginx/sites-available/ip_hash

# Konfigurasi Least Connections
cp /etc/nginx/sites-available/default /etc/nginx/sites-available/least_connection

echo '
    upstream least_connection {
        least_conn;
        server 10.76.2.2;
        server 10.76.2.3;
        server 10.76.2.4;
    }

    server {
        listen 85;
        root /var/www/html;

        index index.html index.htm index.nginx-debian.html;

        server_name _;

        location / {
            proxy_pass http://least_connection;
        }
    }
' > /etc/nginx/sites-available/least_connection

# Aktifkan semua konfigurasi load balancer
ln -sf /etc/nginx/sites-available/round_robin /etc/nginx/sites-enabled/
ln -sf /etc/nginx/sites-available/weight_round_robin /etc/nginx/sites-enabled/
ln -sf /etc/nginx/sites-available/generic_hash /etc/nginx/sites-enabled/
ln -sf /etc/nginx/sites-available/ip_hash /etc/nginx/sites-enabled/
ln -sf /etc/nginx/sites-available/least_connection /etc/nginx/sites-enabled/

# Restart Nginx
service nginx restart
```

### Melakukan Pengetesan untuk semua algoritma
#### Round-Robin
```
ab -n 1000 -c 75 http://10.76.3.3:81/
```
![image](https://github.com/user-attachments/assets/91fa8f4e-7630-4628-a580-5e6ab2b3a9f4)

#### Weight Round-Robin
```
ab -n 1000 -c 75 http://10.76.3.3:82/
```
![image](https://github.com/user-attachments/assets/49693449-278d-42b9-9973-e50280b76cde)

#### Generic Hash
```
ab -n 1000 -c 75 http://10.76.3.3:83/
```
![image](https://github.com/user-attachments/assets/f9dcef06-fa42-4d03-b7c2-344ec9a19cf1)

#### IP Hash
```
ab -n 1000 -c 75 http://10.76.3.3:84/
```
![image](https://github.com/user-attachments/assets/e99e9f20-db1e-434f-85d6-bd1072139b43)

#### Least Connection
```
ab -n 1000 -c 75 http://10.76.3.3:85/
```
![image](https://github.com/user-attachments/assets/1c5b04e0-8b92-42f1-9d18-ae8d4dd5487f)

### Grafik dan Analisis
![Screenshot 2024-10-22 174357](https://github.com/user-attachments/assets/24c99074-a29e-4057-a1fb-9dddd07de211)

Generic Hash dan IP Hash adalah algoritma load balancer yang paling efisien dalam hal RPS pada pengujian ini, dengan Generic Hash sedikit lebih unggul.
Least Connection juga menunjukkan performa yang baik, tetapi kurang optimal dibandingkan dua algoritma tersebut.
Round Robin dan Weighted Round Robin berada di posisi terendah dalam hal RPS, mungkin karena distribusi beban yang tidak memperhatikan kondisi atau kemampuan server backend.

## No.9
Dengan menggunakan algoritma Least-Connection, lakukan testing dengan menggunakan 3 worker, 2 worker, dan 1 worker sebanyak 1000 request dengan 10 request/second, kemudian tambahkan grafiknya pada “laporan kerja Armin”. (9)
### Mengubah konfigurasi untuk Algoritma Least Connection dengan mengubah jumlah worker
![image](https://github.com/user-attachments/assets/6879cdd6-6688-4c45-87f6-c2a43b37f5f5)

### Melakukan pengetesan
#### 1 Worker
![image](https://github.com/user-attachments/assets/119b525b-4eff-4e6c-afe9-37a07f67d36e)

#### 2 Worker
![image](https://github.com/user-attachments/assets/54d2afe4-54c8-4e85-a732-35ef8e553cdb)

#### 3 Worker
![image](https://github.com/user-attachments/assets/97464c01-4515-40d0-9286-e83086337f56)

#### Grafik
![image](https://github.com/user-attachments/assets/ca8eb252-fd64-46eb-a10c-82769624732d)

## No.10
Selanjutnya coba tambahkan keamanan dengan konfigurasi autentikasi di Colossal dengan dengan kombinasi username: “arminannie” dan password: “jrkmyyy”, dengan yyy merupakan kode kelompok. Terakhir simpan file “htpasswd” nya di /etc/nginx/supersecret/ (10)
### Menambah konfigurasi untuk membuat file htpasswd dengan username arminannie dan password jrkmit25
>Colossal/Script10.sh
```
#!/bin/bash

# Membuat direktori untuk menyimpan file htpasswd
mkdir -p /etc/nginx/supersecret

# Membuat file htpasswd dengan username arminannie dan password jrkmit25
htpasswd -cb /etc/nginx/supersecret/htpasswd arminannie jrkmit25

# Konfigurasi Round Robin
echo '
    upstream round-robin {
        server 10.76.2.2;
        server 10.76.2.3;
        server 10.76.2.4;
    }

    server {
        listen 81;
        root /var/www/html;
        index index.php index.html index.htm;
        server_name _;

        location / {
            proxy_pass http://round-robin;
            auth_basic "Restricted Content";
            auth_basic_user_file /etc/nginx/supersecret/htpasswd;
        }
    }
' > /etc/nginx/sites-available/round_robin

# Konfigurasi Weighted Round Robin
echo '
    upstream weight_round-robin {
        server 10.76.2.2 weight=3;
        server 10.76.2.3 weight=2;
        server 10.76.2.4 weight=1;
    }

    server {
        listen 82;
        root /var/www/html;
        index index.php index.html index.htm;
        server_name _;

        location / {
            proxy_pass http://weight_round-robin;
            auth_basic "Restricted Content";
            auth_basic_user_file /etc/nginx/supersecret/htpasswd;
        }
    }
' > /etc/nginx/sites-available/weight_round_robin

# Konfigurasi Generic Hash
echo '
    upstream generic_hash {
        hash $request_uri consistent;
        server 10.76.2.2;
        server 10.76.2.3;
        server 10.76.2.4;
    }

    server {
        listen 83;
        root /var/www/html;
        index index.php index.html index.htm;
        server_name _;

        location / {
            proxy_pass http://generic_hash;
            auth_basic "Restricted Content";
            auth_basic_user_file /etc/nginx/supersecret/htpasswd;
        }
    }
' > /etc/nginx/sites-available/generic_hash

# Konfigurasi IP Hash
echo '
    upstream ip_hash {
        ip_hash;
        server 10.76.2.2;
        server 10.76.2.3;
        server 10.76.2.4;
    }

    server {
        listen 84;
        root /var/www/html;
        index index.php index.html index.htm;
        server_name _;

        location / {
            proxy_pass http://ip_hash;
            auth_basic "Restricted Content";
            auth_basic_user_file /etc/nginx/supersecret/htpasswd;
        }
    }
' > /etc/nginx/sites-available/ip_hash

# Konfigurasi Least Connections
echo '
    upstream least_connection {
        least_conn;
        server 10.76.2.2;
        server 10.76.2.3;
        server 10.76.2.4;
    }

    server {
        listen 85;
        root /var/www/html;
        index index.php index.html index.htm;
        server_name _;

        location / {
            proxy_pass http://least_connection;
            auth_basic "Restricted Content";
            auth_basic_user_file /etc/nginx/supersecret/htpasswd;
        }
    }
' > /etc/nginx/sites-available/least_connection

# Aktivasi semua konfigurasi load balancer
ln -sf /etc/nginx/sites-available/round_robin /etc/nginx/sites-enabled/
ln -sf /etc/nginx/sites-available/weight_round_robin /etc/nginx/sites-enabled/
ln -sf /etc/nginx/sites-available/generic_hash /etc/nginx/sites-enabled/
ln -sf /etc/nginx/sites-available/ip_hash /etc/nginx/sites-enabled/
ln -sf /etc/nginx/sites-available/least_connection /etc/nginx/sites-enabled/

# Restart Nginx untuk menerapkan perubahan
service nginx restart
```

### Test di client
```
lynx http://10.76.3.3:81
```
![image](https://github.com/user-attachments/assets/b1a554ed-c750-4f6f-87c3-adb1fb598d1c)
![image](https://github.com/user-attachments/assets/54aa5005-0937-42f0-a30c-7668c54d5798)
![image](https://github.com/user-attachments/assets/57853a05-baf4-473f-847a-6b1929e2e644)
![image](https://github.com/user-attachments/assets/f64c2ff5-9280-4407-bda0-5887763551a5)

## No.11
Lalu buat untuk setiap request yang mengandung /titan akan di proxy passing menuju halaman https://attackontitan.fandom.com/wiki/Attack_on_Titan_Wiki (11) 
hint: (proxy_pass)
### Menambah konfigurasi untuk proxy pass /titan ke https://attackontitan.fandom.com/wiki/Attack_on_Titan_Wiki
>Colossal/Script11.sh
```
#!/bin/bash

# Membuat direktori untuk menyimpan file htpasswd
mkdir -p /etc/nginx/supersecret

# Membuat file htpasswd dengan username arminannie dan password jrkmit25
htpasswd -cb /etc/nginx/supersecret/htpasswd arminannie jrkmit25

# Konfigurasi Round Robin
echo '
    upstream round-robin {
        server 10.76.2.2;
        server 10.76.2.3;
        server 10.76.2.4;
    }

    server {
        listen 81;
        root /var/www/html;
        index index.php index.html index.htm;
        server_name _;

        location / {
            proxy_pass http://round-robin;
            auth_basic "Restricted Content";
            auth_basic_user_file /etc/nginx/supersecret/htpasswd;
        }

        location /titan {
            proxy_pass https://attackontitan.fandom.com/wiki/Attack_on_Titan_Wiki;
        }
    }
' > /etc/nginx/sites-available/round_robin

# Konfigurasi Weighted Round Robin
echo '
    upstream weight_round-robin {
        server 10.76.2.2 weight=3;
        server 10.76.2.3 weight=2;
        server 10.76.2.4 weight=1;
    }

    server {
        listen 82;
        root /var/www/html;
        index index.php index.html index.htm;
        server_name _;

        location / {
            proxy_pass http://weight_round-robin;
            auth_basic "Restricted Content";
            auth_basic_user_file /etc/nginx/supersecret/htpasswd;
        }

        location /titan {
            proxy_pass https://attackontitan.fandom.com/wiki/Attack_on_Titan_Wiki;
        }
    }
' > /etc/nginx/sites-available/weight_round_robin

# Konfigurasi Generic Hash
echo '
    upstream generic_hash {
        hash $request_uri consistent;
        server 10.76.2.2;
        server 10.76.2.3;
        server 10.76.2.4;
    }

    server {
        listen 83;
        root /var/www/html;
        index index.php index.html index.htm;
        server_name _;

        location / {
            proxy_pass http://generic_hash;
            auth_basic "Restricted Content";
            auth_basic_user_file /etc/nginx/supersecret/htpasswd;
        }

        location /titan {
            proxy_pass https://attackontitan.fandom.com/wiki/Attack_on_Titan_Wiki;
        }
    }
' > /etc/nginx/sites-available/generic_hash

# Konfigurasi IP Hash
echo '
    upstream ip_hash {
        ip_hash;
        server 10.76.2.2;
        server 10.76.2.3;
        server 10.76.2.4;
    }

    server {
        listen 84;
        root /var/www/html;
        index index.php index.html index.htm;
        server_name _;

        location / {
            proxy_pass http://ip_hash;
            auth_basic "Restricted Content";
            auth_basic_user_file /etc/nginx/supersecret/htpasswd;
        }

        location /titan {
            proxy_pass https://attackontitan.fandom.com/wiki/Attack_on_Titan_Wiki;
        }
    }
' > /etc/nginx/sites-available/ip_hash

# Konfigurasi Least Connections
echo '
    upstream least_connection {
        least_conn;
        server 10.76.2.2;
        server 10.76.2.3;
        server 10.76.2.4;
    }

    server {
        listen 85;
        root /var/www/html;
        index index.php index.html index.htm;
        server_name _;

        location / {
            proxy_pass http://least_connection;
            auth_basic "Restricted Content";
            auth_basic_user_file /etc/nginx/supersecret/htpasswd;
        }

        location /titan {
            proxy_pass https://attackontitan.fandom.com/wiki/Attack_on_Titan_Wiki;
        }
    }
' > /etc/nginx/sites-available/least_connection

# Aktivasi semua konfigurasi load balancer
ln -sf /etc/nginx/sites-available/round_robin /etc/nginx/sites-enabled/
ln -sf /etc/nginx/sites-available/weight_round_robin /etc/nginx/sites-enabled/
ln -sf /etc/nginx/sites-available/generic_hash /etc/nginx/sites-enabled/
ln -sf /etc/nginx/sites-available/ip_hash /etc/nginx/sites-enabled/
ln -sf /etc/nginx/sites-available/least_connection /etc/nginx/sites-enabled/

# Restart Nginx untuk menerapkan perubahan
service nginx restart
```

### Test di client
```
lynx http://10.76.3.3:81/titan
```
![Screenshot 2024-10-22 195338](https://github.com/user-attachments/assets/3cf4941a-e6b1-4d17-b243-5bd8aa44c7a5)

## No.12
### Mengecek MAC Address Erwin
![image](https://github.com/user-attachments/assets/0fb97c5f-8943-4d28-b55e-a50836ac1d62)

### Menambah konfigurasi untuk fixed address client Erwin
>Tybur/Script12.sh
```
#!/bin/bash

# Update and install isc-dhcp-server
apt-get update
apt-get install isc-dhcp-server -y

# Configure the DHCP server interface
echo 'INTERFACESv4="eth0"
INTERFACESv6=""
' > /etc/default/isc-dhcp-server

# DHCP configuration
subnet="option domain-name \"example.org\";
option domain-name-servers ns1.example.org, ns2.example.org;

default-lease-time 600;
max-lease-time 7200;

ddns-update-style none;

subnet 10.76.1.0 netmask 255.255.255.0 {
    range 10.76.1.5 10.76.1.25;
    range 10.76.1.50 10.76.1.100;
    option routers 10.76.1.1;
    option broadcast-address 10.76.1.255;
    option domain-name-servers 10.76.4.2;
    default-lease-time 360;
    max-lease-time 5220;
}

subnet 10.76.2.0 netmask 255.255.255.0 {
    range 10.76.2.9 10.76.2.27;
    range 10.76.2.81 10.76.2.243;
    option routers 10.76.2.1;
    option broadcast-address 10.76.2.255;
    option domain-name-servers 10.76.4.2;
    default-lease-time 1800;
    max-lease-time 5220;
}

subnet 10.76.3.0 netmask 255.255.255.0 {
}

subnet 10.76.4.0 netmask 255.255.255.0 {
}

host Erwin {
    hardware ethernet ca:66:fa:14:a3:08;
    fixed-address 10.76.2.156;
}"

# Write the configuration to dhcpd.conf
echo "$subnet" > /etc/dhcp/dhcpd.conf

# Restart the DHCP server
service isc-dhcp-server restart
```

### Menambah konfiguras listen ke IP yang diberikan dan menolak dari selain IP tersebut
>Colossal/Script12.sh
```
#!/bin/bash

# Membuat direktori untuk menyimpan file htpasswd
mkdir -p /etc/nginx/supersecret

# Membuat file htpasswd dengan username arminannie dan password jrkmit25
htpasswd -cb /etc/nginx/supersecret/htpasswd arminannie jrkmit25

# Konfigurasi Round Robin
echo '
    upstream round-robin {
        server 10.76.2.2;
        server 10.76.2.3;
        server 10.76.2.4;
    }

    server {
        listen 81;
        root /var/www/html;
        index index.php index.html index.htm;
        server_name _;

        location / {
            allow 10.76.1.77;
            allow 10.76.1.88;
            allow 10.76.2.144;
            allow 10.76.2.156;
            deny all;

            proxy_pass http://round-robin;
            auth_basic "Restricted Content";
            auth_basic_user_file /etc/nginx/supersecret/htpasswd;
        }

        location /titan {
            proxy_pass https://attackontitan.fandom.com/wiki/Attack_on_Titan_Wiki;
        }
    }
' > /etc/nginx/sites-available/round_robin

# Konfigurasi Weighted Round Robin
echo '
    upstream weight_round-robin {
        server 10.76.2.2 weight=3;
        server 10.76.2.3 weight=2;
        server 10.76.2.4 weight=1;
    }

    server {
        listen 82;
        root /var/www/html;
        index index.php index.html index.htm;
        server_name _;

        location / {
            allow 10.76.1.77;
            allow 10.76.1.88;
            allow 10.76.2.144;
            allow 10.76.2.156;
            deny all;

            proxy_pass http://weight_round-robin;
            auth_basic "Restricted Content";
            auth_basic_user_file /etc/nginx/supersecret/htpasswd;
        }

        location /titan {
            proxy_pass https://attackontitan.fandom.com/wiki/Attack_on_Titan_Wiki;
        }
    }
' > /etc/nginx/sites-available/weight_round_robin

# Konfigurasi Generic Hash
echo '
    upstream generic_hash {
        hash $request_uri consistent;
        server 10.76.2.2;
        server 10.76.2.3;
        server 10.76.2.4;
    }

    server {
        listen 83;
        root /var/www/html;
        index index.php index.html index.htm;
        server_name _;

        location / {
            allow 10.76.1.77;
            allow 10.76.1.88;
            allow 10.76.2.144;
            allow 10.76.2.156;
            deny all;

            proxy_pass http://generic_hash;
            auth_basic "Restricted Content";
            auth_basic_user_file /etc/nginx/supersecret/htpasswd;
        }

        location /titan {
            proxy_pass https://attackontitan.fandom.com/wiki/Attack_on_Titan_Wiki;
        }
    }
' > /etc/nginx/sites-available/generic_hash

# Konfigurasi IP Hash
echo '
    upstream ip_hash {
        ip_hash;
        server 10.76.2.2;
        server 10.76.2.3;
        server 10.76.2.4;
    }

    server {
        listen 84;
        root /var/www/html;
        index index.php index.html index.htm;
        server_name _;

        location / {
            allow 10.76.1.77;
            allow 10.76.1.88;
            allow 10.76.2.144;
            allow 10.76.2.156;
            deny all;

            proxy_pass http://ip_hash;
            auth_basic "Restricted Content";
            auth_basic_user_file /etc/nginx/supersecret/htpasswd;
        }

        location /titan {
            proxy_pass https://attackontitan.fandom.com/wiki/Attack_on_Titan_Wiki;
        }
    }
' > /etc/nginx/sites-available/ip_hash

# Konfigurasi Least Connections
echo '
    upstream least_connection {
        least_conn;
        server 10.76.2.2;
        server 10.76.2.3;
        server 10.76.2.4;
    }

    server {
        listen 85;
        root /var/www/html;
        index index.php index.html index.htm;
        server_name _;

        location / {
            allow 10.76.1.77;
            allow 10.76.1.88;
            allow 10.76.2.144;
            allow 10.76.2.156;
            deny all;

            proxy_pass http://least_connection;
            auth_basic "Restricted Content";
            auth_basic_user_file /etc/nginx/supersecret/htpasswd;
        }

        location /titan {
            proxy_pass https://attackontitan.fandom.com/wiki/Attack_on_Titan_Wiki;
        }
    }
' > /etc/nginx/sites-available/least_connection

# Aktivasi semua konfigurasi load balancer
ln -sf /etc/nginx/sites-available/round_robin /etc/nginx/sites-enabled/
ln -sf /etc/nginx/sites-available/weight_round_robin /etc/nginx/sites-enabled/
ln -sf /etc/nginx/sites-available/generic_hash /etc/nginx/sites-enabled/
ln -sf /etc/nginx/sites-available/ip_hash /etc/nginx/sites-enabled/
ln -sf /etc/nginx/sites-available/least_connection /etc/nginx/sites-enabled/

# Restart Nginx untuk menerapkan perubahan
service nginx restart

```

### Menambah konfigurasi untuk client Erwin
>Erwin/Script12.sh
```
#!/bin/bash

echo "auto eth0
iface eth0 inet dhcp
hwaddress ether ca:66:fa:14:a3:08
" > /etc/network/interfaces

# Restart interface eth0 menggunakan ip link
ip link set eth0 down
ip link set eth0 up

```

### Cek apakah IP Erwin sudah berubah
![Screenshot 2024-10-24 114902](https://github.com/user-attachments/assets/040b885f-2107-4d30-acac-1c344f3919e7)

### Tes di client Erwin
```
lynx 10.76.3.3:81
```
![Screenshot 2024-10-22 185935](https://github.com/user-attachments/assets/aba1c8c9-6c23-4b5f-862e-7a06348474a6)

### Tes di client Zeke yang memiliki IP tidak sesuai permintaan
![Screenshot 2024-10-24 115331](https://github.com/user-attachments/assets/b8c821a7-cc68-4f98-b011-393c40895b32)
![image](https://github.com/user-attachments/assets/4a6f81eb-7a44-4992-bafe-39db5f8e4660)




