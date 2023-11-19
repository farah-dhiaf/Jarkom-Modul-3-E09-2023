# Jarkom-Modul-3-E09-2023

|Nama Anggota |NRP |
|---|---|
|Thoriq Fatihassalam | 5025201254 |
|Farah Dhia Fadhila | 5025211030 |

## Setup Config
### Aura (DHCP Relay)
```
auto eth0
iface eth0 inet dhcp

#SWITCH 1
auto eth1
iface eth1 inet static
	address 10.41.1.0
	netmask 255.255.255.0

#SWITCH 2
auto eth2
iface eth2 inet static
	address 10.41.2.0
	netmask 255.255.255.0

#SWITCH 3
auto eth3
iface eth3 inet static
	address 10.41.3.0
	netmask 255.255.255.0

#SWITCH 4
auto eth4
iface eth4 inet static
	address 10.41.4.0
	netmask 255.255.255.0
```
### Himmel (DHCP Server)
```
auto eth0
iface eth0 inet static
	address 10.41.1.1
	netmask 255.255.255.0
	gateway 10.41.1.0
```
### Heiter (DNS Server)
```
auto eth0
iface eth0 inet static
	address 10.41.1.2
	netmask 255.255.255.0
	gateway 10.41.1.0
```
### Denken (Database Server)
```
auto eth0
iface eth0 inet static
	address 10.41.2.1
	netmask 255.255.255.0
	gateway 10.41.2.0
```
### Eisen (Load Balancer)
```
auto eth0
iface eth0 inet static
	address 10.41.2.2
	netmask 255.255.255.0
	gateway 10.41.2.0
```
### Lugner (PHP Worker)
```
auto eth0
iface eth0 inet static
	address 10.41.3.1
	netmask 255.255.255.0
	gateway 10.41.3.0

hwaddress ether 0e:4b:5a:31:8a:2a
```
### Linie (PHP Worker)
```
auto eth0
iface eth0 inet static
	address 10.41.3.2
	netmask 255.255.255.0
	gateway 10.41.3.0

hwaddress ether ca:a4:b5:39:a9:b5
```
### Lawine (PHP Worker)
```
auto eth0
iface eth0 inet static
	address 10.41.3.3
	netmask 255.255.255.0
	gateway 10.41.3.0

hwaddress ether c2:83:2d:bb:00:d2
```
### Richter (Client)
```
auto eth0
iface eth0 inet static
	address 10.41.3.4
	netmask 255.255.255.0
	gateway 10.41.3.0
```
### Revolte (Client)
```
auto eth0
iface eth0 inet static
	address 10.41.3.5
	netmask 255.255.255.0
	gateway 10.41.3.0

```
### Fern (Laravel Worker)
```
auto eth0
iface eth0 inet static
	address 10.41.4.1
	netmask 255.255.255.0
	gateway 10.41.4.0

hwaddress ether 6e:33:92:a9:84:4e
```
### Flamme (Laravel Worker)
```
auto eth0
iface eth0 inet static
	address 10.41.4.2
	netmask 255.255.255.0
	gateway 10.41.4.0

hwaddress ether 86:21:b1:5c:54:e4
```
### Frieren (Laravel Worker)
```
auto eth0
iface eth0 inet static
	address 10.41.4.3
	netmask 255.255.255.0
	gateway 10.41.4.0

hwaddress ether 3e:94:be:ca:0c:2c
```
### Stark (Client)
```
auto eth0
iface eth0 inet static
	address 10.41.4.4
	netmask 255.255.255.0
	gateway 10.41.4.0
```
### Sein (Client)
```
auto eth0
iface eth0 inet static
	address 10.41.4.5
	netmask 255.255.255.0
	gateway 10.41.4.0

```
## Inisialisasi
Sebelum memulai, perlu dilakukan inisialisasi pada setiap node di /root/.bashrc berupa nameserver dan installment yang dibutuhkan.

### Aura (DHCP Relay)
```
iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE -s 10.41.0.0/16
echo 'nameserver 192.168.122.1' > /etc/resolv.conf
```
### Himmel (DHCP Server)
```
echo 'nameserver 10.41.1.2' > /etc/resolv.conf
```
### Heiter (DNS Server)
```
echo "nameserver 192.168.122.1" > /etc/resolv.conf
```
### Denken (Database Server)
```
echo 'nameserver 10.41.1.2' > /etc/resolv.conf

apt-get update
apt-get install mariadb-server -y

```
### Eisen (Load Balancer)
```
echo 'nameserver 10.41.1.2' > /etc/resolv.conf

apt-get update
apt-get install apache2-utils -y
apt-get install nginx -y
apt-get install lynx -y

```
### PHP Worker (Lugner, Linie, Lawine)
```
echo 'nameserver 10.41.1.2' > /etc/resolv.conf

apt-get update
apt-get install nginx -y
apt-get install lynx -y
apt-get install htop -y
apt-get install apache2-utils -y
apt-get install wget -y
apt-get install unzip -y
apt-get install php7.3-fpm php7.3-common php7.3-mysql php7.3-gmp php7.3-curl php7.3-intl php7.3-mbstring php7.3-xmlrpc php7.3-gd php7.3-xml php7.3-cli php7.3-zip -y

```
### Laravel Worker (Fern, Flamme, Frieren)
```
echo 'nameserver 10.41.1.2' > /etc/resolv.conf

apt-get update
apt-get install lynx -y
apt-get install mariadb-client -y
apt-get install -y lsb-release ca-certificates apt-transport-https software-properties-common gnupg2
curl -sSLo /usr/share/keyrings/deb.sury.org-php.gpg https://packages.sury.org/php/apt.gpg
sh -c 'echo "deb [signed-by=/usr/share/keyrings/deb.sury.org-php.gpg] https://packages.sury.org/php/ $(lsb_release -sc) main" > /etc/apt/sources.list.d/php.list'
apt-get update
apt-get install php8.0-mbstring php8.0-xml php8.0-cli php8.0-common php8.0-intl php8.0-opcache php8.0-readline php8.0-mysql php8.0-fpm php8.0-curl unzip wget -y
apt-get install nginx -y
```
<img width="564" alt="image" src="https://github.com/farah-dhiaf/Jarkom-Modul-3-E09-2023/assets/91003215/4906bc55-34d6-4935-b24f-8036c4163ea4">

## Soal 0
Setelah mengalahkan Demon King, perjalanan berlanjut. Kali ini, kalian diminta untuk melakukan register domain berupa riegel.canyon.yyy.com untuk worker Laravel dan granz.channel.yyy.com untuk worker PHP (0) mengarah pada worker yang memiliki IP [prefix IP].x.1.

### Jawaban
Pada DNS server (Heiter), nstall dahulu package bind9.
```
apt-get update
apt-get install bind9 -y
```
Atur konfigurasi bind9 seperti pada modul 2 kemarin, masuk ke file /etc/bind/named.conf.local dan isi dengan kode berikut.
```
zone "riegel.canyon.e09.com" {
        type master;
        file "/etc/bind/jarkom/riegel.canyon.e09.com";
};

zone "granz.channel.e09.com" {
        type master;
        file "/etc/bind/jarkom/granz.channel.e09.com";
};
```

lalu buat direktori bernama jarkom dengan `mkdir -p /etc/bind/jarkom` dan copy file `db.local` untuk dilakukan kustomisasi file bind9.
```
cp -p /etc/bind/db.local /etc/bind/jarkom/riegel.canyon.e09.com
cp -p /etc/bind/db.local /etc/bind/jarkom/granz.channel.e09.com

echo '
;
; BIND data file for local loopback interface
;
$TTL    604800
@       IN      SOA     riegel.canyon.e09.com. root.riegel.canyon.e09.com. (
                              2         ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
@       IN      NS      riegel.canyon.e09.com.
@       IN      A       10.41.4.1 ; IP Fern Laravel Worker
www     IN      CNAME   riegel.canyon.e09.com.
' > /etc/bind/jarkom/riegel.canyon.e09.com

echo '
;
; BIND data file for local loopback interface
;
$TTL    604800
@       IN      SOA     granz.channel.e09.com. root.granz.channel.e09.com. (
                              2         ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
@       IN      NS      granz.channel.e09.com.
@       IN      A       10.41.3.1 ; IP Lugner PHP Worker
www     IN      CNAME   granz.channel.e09.com.
' > /etc/bind/jarkom/granz.channel.e09.com
```
Jangan lupa untuk melakukan restart bind9 dengan `service bind9 restart`

### Output
Lakukan ping ke `riegel.canyon.e09.com` dan `granz.channel.e09.com` di client.
![image](https://github.com/farah-dhiaf/Jarkom-Modul-3-E09-2023/assets/91003215/8b2471cb-ddc8-4281-a436-6def4ba85a0e) </br>
![image](https://github.com/farah-dhiaf/Jarkom-Modul-3-E09-2023/assets/91003215/ee0aa64b-dfbc-4e5b-bd90-420519ace3f2)

## Soal 1-5
(1) Lakukan konfigurasi sesuai dengan peta yang sudah diberikan.
Kemudian, karena masih banyak spell yang harus dikumpulkan, bantulah para petualang untuk memenuhi kriteria berikut.: </br>
2. Semua CLIENT harus menggunakan konfigurasi dari DHCP Server.
Client yang melalui Switch3 mendapatkan range IP dari [prefix IP].3.16 - [prefix IP].3.32 dan [prefix IP].3.64 - [prefix IP].3.80 (2) </br>
3. Client yang melalui Switch4 mendapatkan range IP dari [prefix IP].4.12 - [prefix IP].4.20 dan [prefix IP].4.160 - [prefix IP].4.168 (3) </br>
4. Client mendapatkan DNS dari Heiter dan dapat terhubung dengan internet melalui DNS tersebut (4) </br>
5. Lama waktu DHCP server meminjamkan alamat IP kepada Client yang melalui Switch3 selama 3 menit sedangkan pada client yang melalui Switch4 selama 12 menit. Dengan waktu maksimal dialokasikan untuk peminjaman alamat IP selama 96 menit (5)

### Jawaban
Pada DHCP server (Himmel), install package untuk DHCP server terlebih dahulu.
```
apt-get update && apt-get install isc-dhcp-server -y
```
Lalu lakukan konfigurasi untuk interface yang akan diberi DHCP.
```
echo '
INTERFACESv4="eth0"
INTERFACESv6=""
' > /etc/default/isc-dhcp-server
```
Lalu lakukan konfigurasi DHCP. Untuk switch 3 akan diberi ip dengan rentang `x.x.3.16 - x.x3.32` dan `x.x.3.64 - x.x.3.80`(2). Sedangkan untuk switch 4 akan diberi ip dengan rentang `x.x.4.12 - x.x.4.20` dan `x.x.4.160 - x.x.4.168` (3). Jangan lupa mengatur leasing times untuk switch 3 selama 3 menit (180 s) dan untuk switch 4 selama 12 menit (720 s) dengan alokasi waktu maksimal peminjaman IP selama 96 menit (5760 s) (5).
```
echo '
option domain-name "example.org";
option domain-name-servers ns1.example.org, ns2.example.org;

default-lease-time 600;
max-lease-time 7200;

ddns-update-style none;

subnet 10.41.1.0 netmask 255.255.255.0 {
}

subnet 10.41.2.0 netmask 255.255.255.0 {
}

#nomor 2
subnet 10.41.3.0 netmask 255.255.255.0 {
    range 10.41.3.16 10.41.3.32;
    range 10.41.3.64 10.41.3.80;
    option routers 10.41.3.0;
    option broadcast-address 10.41.3.255;
    option domain-name-servers 10.41.1.2;
    default-lease-time 180;
    max-lease-time 5760;
}

#nomor 3
subnet 10.41.4.0 netmask 255.255.255.0 {
    range 10.41.4.12 10.41.4.20;
    range 10.41.4.160 10.41.4.168;
    option routers 10.41.4.0;
    option broadcast-address 10.41.4.255;
    option domain-name-servers 10.41.1.2;
    default-lease-time 720;
    max-lease-time 5760;
}
' > /etc/dhcp/dhcpd.conf
```
Jangan lupa untuk restart bind9 dengan `service bind9 restart`. </br>

Setelah itu kita perlu atur untuk DHCP relay, pada DHCP relay (Aura), install package untuk DHCP relay terlebih dahulu.
```
apt-get update && apt-get install isc-dhcp-relay -y
```
Lalu lakukan konfigurasi pada `isc-dhcp-relay`
```
echo '
SERVERS="10.41.1.1" #IP DHCP Server

# On what interfaces should the DHCP relay (dhrelay) serve DHCP requests?
INTERFACES="eth1 eth2 eth3 eth4"

# Additional options that are passed to the DHCP relay daemon?
OPTIONS=""
' > /etc/default/isc-dhcp-relay
```
Lalu lakukan konfigurasi IP forwarding
```
echo 'net.ipv4.ip_forward=1' > /etc/sysctl.conf
```
Jangan lupa untuk start isc-dhcp-relay dengan `service isc-dhcp-relay restart`

Karena client harus terhubung dengan internet melalui DNS server, maka kita harus mengatur konfigurasi file `named.conf.options` pada DNS server.
```
echo '
options {
        directory "/var/cache/bind";

         forwarders {
                192.168.122.1;
         };

        //dnssec-validation auto;
        allow-query{any;};
        listen-on-v6 { any; };
};
' > /etc/bind/named.conf.options
```

### Output
Pada client Stark</br>
![image](https://github.com/farah-dhiaf/Jarkom-Modul-3-E09-2023/assets/91003215/5239dd99-a163-42e1-a531-26b981f7b08e)
![image](https://github.com/farah-dhiaf/Jarkom-Modul-3-E09-2023/assets/91003215/15b0d336-36c6-4dad-872e-261fb17024ae)

Pada client Sein</br>
![image](https://github.com/farah-dhiaf/Jarkom-Modul-3-E09-2023/assets/91003215/42f0d425-6ea2-4a20-bf4e-31a0e7b328e6)
![image](https://github.com/farah-dhiaf/Jarkom-Modul-3-E09-2023/assets/91003215/d13ac8c5-a3a5-4723-9be9-3f8ed88478cf)

Pada client Revolte</br>
![image](https://github.com/farah-dhiaf/Jarkom-Modul-3-E09-2023/assets/91003215/bf59358d-14d8-4f08-b712-903fe364449a)
![image](https://github.com/farah-dhiaf/Jarkom-Modul-3-E09-2023/assets/91003215/7801878d-b029-462b-b39e-398c4012c7af)

Pada client Richter</br>
![image](https://github.com/farah-dhiaf/Jarkom-Modul-3-E09-2023/assets/91003215/356908d8-6c06-40d6-9f40-3acfdf5a30b8)
![image](https://github.com/farah-dhiaf/Jarkom-Modul-3-E09-2023/assets/91003215/c02aae17-aec8-457d-beba-b4c85685c2b4)

## Soal 6
Pada masing-masing worker PHP, lakukan konfigurasi virtual host untuk website berikut dengan menggunakan php 7.3. 

### Jawaban
Sebelum itu kita perlu mendownload file zip yang telah disediakan dari soal.
```
wget --no-check-certificate 'https://drive.google.com/uc?export=download&id=1ViSkRq7SmwZgdK64eRbr5Fm1EGCTPrU1' -O granz.channel.yyy.com.zip
unzip granz.channel.yyy.com.zip -d /var/www
mv /var/www/modul-3 /var/www/granz.channel.e09.com
rm granz.channel.yyy.com.zip
```
Setelah itu melakukan konfigurasi nginx pada worker PHP. Copy dahulu file defaultnya lalu lakukan kostumisasi yang diperlukan.
```
cp /etc/nginx/sites-available/default /etc/nginx/sites-available/granz.channel.e09.com
rm /etc/nginx/sites-enabled/default

echo '
server {
    listen 80;
    server_name _;

    root /var/www/granz.channel.e09.com;
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
}
' > /etc/nginx/sites-available/granz.channel.e09.com
```
Jangan lupa untuk symlink agar setiap perubahan akan tersimpan dan lakukan restart nginx.
```
ln -s /etc/nginx/sites-available/granz.channel.e09.com /etc/nginx/sites-enabled/
service nginx restart
```
### Output
Lakukan `lynx localhost` pada worker yang bersangkutan.
![image](https://github.com/farah-dhiaf/Jarkom-Modul-3-E09-2023/assets/91003215/90c06281-0668-4f90-9869-302ecab7dae2)

## Soal 7
Kepala suku dari Bredt Region memberikan resource server sebagai berikut:
Lawine, 4GB, 2vCPU, dan 80 GB SSD.
Linie, 2GB, 2vCPU, dan 50 GB SSD.
Lugner 1GB, 1vCPU, dan 25 GB SSD.
aturlah agar Eisen dapat bekerja dengan maksimal, lalu lakukan testing dengan 1000 request dan 100 request/second.

### Jawaban
Pada DNS server, lakukan edit konfigurasi pada domain yang sebelumnya mengarah ke worker PHP dan Laravel dengan IP x.x.x.1 menjadi IP load balancer (Eisen).

```
echo '
;
; BIND data file for local loopback interface
;
$TTL    604800
@       IN      SOA     riegel.canyon.e09.com. root.riegel.canyon.e09.com. (
                        2               ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
@       IN      NS      riegel.canyon.e09.com.
@       IN      A       10.41.2.2     ; IP Eisen
www     IN      CNAME   riegel.canyon.e09.com.
' > /etc/bind/jarkom/riegel.canyon.e09.com

echo '
; BIND data file for local loopback interface
;
$TTL    604800
@       IN      SOA     granz.channel.e09.com. root.granz.channel.e09.com. (
                        2               ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
@       IN      NS      granz.channel.e09.com.
@       IN      A       10.41.2.2     ; IP Eisen
www     IN      CNAME   granz.channel.e09.com.
' > /etc/bind/jarkom/granz.channel.e09.com
```
Jangan lupa untuk restart bind9 dengan `service bind9 restart`. Setelah itu atur konfigurasi load balancer pada Eisen (load balancer).
```
cp /etc/nginx/sites-available/default /etc/nginx/sites-available/lb-jarkom

echo ' 
upstream php-worker {
    server 10.41.3.1;
    server 10.41.3.2;
    server 10.41.3.3;
}

server {
    listen 80;
    server_name granz.channel.e09.com www.granz.channel.e09.com;

    root /var/www/html;

    index index.html index.htm index.nginx-debian.html;

    server_name _;

        proxy_pass http://php-worker;
    }
} 
' > /etc/nginx/sites-available/lb-jarkom
```
Jangan lupa untuk melakukan symlink dan restart nginx.
```
ln -s /etc/nginx/sites-available/lb-jarkom /etc/nginx/sites-enabled/
rm /etc/nginx/sites-enabled/default
service nginx restart
```
Pada client, kita perlu install package yang diperlukan terlebih dahulu, saya menyimpannya di file dependancy.sh
```
apt update
apt install lynx -y
apt install apache2-utils -y
```

### Output
Lakukan `ab -n 1000 -c 100 http://www.granz.channel.e09.com/` pada client.
![image](https://github.com/farah-dhiaf/Jarkom-Modul-3-E09-2023/assets/91003215/5d0f7209-b4ea-4911-9470-e56a81ff49e0)

## Soal 8
Karena diminta untuk menuliskan grimoire, buatlah analisis hasil testing dengan 200 request dan 10 request/second masing-masing algoritma Load Balancer dengan ketentuan sebagai berikut: </br>
a. Nama Algoritma Load Balancer </br>
b. Report hasil testing pada Apache Benchmark </br>
c. Grafik request per second untuk masing masing algoritma. 
Analisis

### Jawaban
Perlu menerapkan algoritma load balancer pada konfigurasi nginx. 
1. Algoritma round robin mengurutkan berdasarkan nomor dari server</br>
```
    server 10.41.3.1;
    server 10.41.3.2;
    server 10.41.3.3;

```
2. Algoritma least-connection melakukan prioritas pembagian dari beban kinerja paling rendah</br>
```
    ip_hash;
    server 10.41.3.1;
    server 10.41.3.2;
    server 10.41.3.3;
```
3. Algoritma ip hash akan melakukan hash berdasarkan request user, sehingga server akan menerima request dari ip yang berbeda</br>
```
    least_conn;
    server 10.41.3.1;
    server 10.41.3.2;
    server 10.41.3.3;
```
4. Algoritma generic hash akan memetakkan beban ke masing-masing node dengan membuat hashing berdasarkan text dan atau `Nginx Variables` yang ditentukan dalam hash config</br>
```
    hash $request_uri consistent;
    server 10.41.3.1;
    server 10.41.3.2;
    server 10.41.3.3;
```

### Output
Run command `ab -n 200 -c 10 http://www.granz.channel.e09.com/` di client dan melakukan analisis grimoire di file pdf.

#### Round Robin
<img width="407" alt="image" src="https://github.com/farah-dhiaf/Jarkom-Modul-3-E09-2023/assets/91003215/d62dbb27-9c5b-4d04-95fc-761ef92c88e9">
<img width="407" alt="image" src="https://github.com/farah-dhiaf/Jarkom-Modul-3-E09-2023/assets/91003215/05b99371-100d-424e-9942-c36e9be11f01">
<img width="406" alt="image" src="https://github.com/farah-dhiaf/Jarkom-Modul-3-E09-2023/assets/91003215/742f00bf-981e-45a1-bdad-410357c20ec9">

#### Least connection
<img width="406" alt="image" src="https://github.com/farah-dhiaf/Jarkom-Modul-3-E09-2023/assets/91003215/27381af0-39a5-4acc-801c-05e67a8830ae">
<img width="407" alt="image" src="https://github.com/farah-dhiaf/Jarkom-Modul-3-E09-2023/assets/91003215/f0631018-814f-4a5c-a955-24c116f75083">
<img width="406" alt="image" src="https://github.com/farah-dhiaf/Jarkom-Modul-3-E09-2023/assets/91003215/88e5ffa8-1d62-4bb4-9722-e1813e3f89c6">

#### IP Hash
<img width="406" alt="image" src="https://github.com/farah-dhiaf/Jarkom-Modul-3-E09-2023/assets/91003215/8500e37a-b9ee-4a11-b2ad-0d340870d158">
<img width="391" alt="image" src="https://github.com/farah-dhiaf/Jarkom-Modul-3-E09-2023/assets/91003215/f9c468b8-b42d-47b5-bc61-936c415d468a">
<img width="405" alt="image" src="https://github.com/farah-dhiaf/Jarkom-Modul-3-E09-2023/assets/91003215/67142896-773f-4b56-ade4-8a8750ab7f0a">

#### Generic Hash
<img width="405" alt="image" src="https://github.com/farah-dhiaf/Jarkom-Modul-3-E09-2023/assets/91003215/3a37d248-70f4-4f53-9409-cf4d3e4fd4e8">
<img width="407" alt="image" src="https://github.com/farah-dhiaf/Jarkom-Modul-3-E09-2023/assets/91003215/dcb4e455-00fe-4393-9f6b-a6b4f094de92">
<img width="406" alt="image" src="https://github.com/farah-dhiaf/Jarkom-Modul-3-E09-2023/assets/91003215/f368c3a4-5fae-4a53-aad7-823851a9df86">

## Soal 9
Dengan menggunakan algoritma Round Robin, lakukan testing dengan menggunakan 3 worker, 2 worker, dan 1 worker sebanyak 100 request dengan 10 request/second, kemudian tambahkan grafiknya pada grimoire.

### Output
#### 3 Worker
<img width="406" alt="image" src="https://github.com/farah-dhiaf/Jarkom-Modul-3-E09-2023/assets/91003215/26bad3bd-0aee-474c-a30e-2ce315fcc192">
<img width="406" alt="image" src="https://github.com/farah-dhiaf/Jarkom-Modul-3-E09-2023/assets/91003215/78df7f44-b09b-4223-8b04-cfc9af3f50ee">

#### 2 Worker
<img width="408" alt="image" src="https://github.com/farah-dhiaf/Jarkom-Modul-3-E09-2023/assets/91003215/d15379de-8dbe-4063-82b0-6ba396caa5b4">
<img width="407" alt="image" src="https://github.com/farah-dhiaf/Jarkom-Modul-3-E09-2023/assets/91003215/22b71cb7-8725-49dd-9e2c-0edea734237f">

#### 1 Worker
<img width="407" alt="image" src="https://github.com/farah-dhiaf/Jarkom-Modul-3-E09-2023/assets/91003215/50011b57-c38b-402a-a546-a9861a76f940">
<img width="406" alt="image" src="https://github.com/farah-dhiaf/Jarkom-Modul-3-E09-2023/assets/91003215/32b23857-57e6-4794-946a-06fc71f44355">

## Soal 10
Selanjutnya coba tambahkan konfigurasi autentikasi di LB dengan dengan kombinasi username: “netics” dan password: “ajkyyy”, dengan yyy merupakan kode kelompok. Terakhir simpan file “htpasswd” nya di /etc/nginx/rahasisakita/ 

### Jawaban
Pertama membuat direktori **/etc/nginx/rahasisakita** dengan `mkdir /etc/nginx/rahasisakita`, lalu membuat user auth dengan username `netics` dan password `ajke09`.
```
htpasswd -c /etc/nginx/rahasisakita/htpasswd netics
```
lalu masukkan password ajke09. Setelah itu menambahkan 
```
auth_basic "Administrators Area";
auth_basic_user_file /etc/nginx/rahasisakita/htpasswd;
```
dan juga untuk block file .htaccess dan .htpasswd
```
location ~ /\.ht {
  deny all;
}
```
Jangan lupa untuk restart nginx `service nginx restart`.

### Output
Menjalankan command `ab -A netics:ajke09 -n 100 -c 100 http://granz.channel.e09.com/` di client.
<img width="501" alt="image" src="https://github.com/farah-dhiaf/Jarkom-Modul-3-E09-2023/assets/91003215/db1bf862-404e-4c7d-8e8e-52ba189bc178">
<img width="481" alt="image" src="https://github.com/farah-dhiaf/Jarkom-Modul-3-E09-2023/assets/91003215/cf993a5d-f385-40e7-bc50-7ff25647a41e">

## Soal 11
Lalu buat untuk setiap request yang mengandung /its akan di proxy passing menuju halaman https://www.its.ac.id. (11) hint: (proxy_pass)

### Jawaban
Menambahkan proxy pass menuju page https://www.its.ac.id di konfigurasi nginx.
```
location ~ /its {
    proxy_pass https://www.its.ac.id;
    proxy_set_header Host www.its.ac.id;
    proxy_set_header X-Real-IP $remote_addr;
    proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    proxy_set_header X-Forwarded-Proto $scheme;
}
```

### Output
Menjalankan `lynx https://granz.channel.e09.com/its` pada client. Namun pada soal ini kode saya masih tidak berhasil alias belum mengarah ke website its.

## Soal 12
Selanjutnya LB ini hanya boleh diakses oleh client dengan IP [Prefix IP].3.69, [Prefix IP].3.70, [Prefix IP].4.167, dan [Prefix IP].4.168. (12) hint: (fixed in dulu clinetnya)
### Jawaban 
### Output

## Soal 13
Semua data yang diperlukan, diatur pada Denken dan harus dapat diakses oleh Frieren, Flamme, dan Fern.
### Jawaban
Pada database server (Denken), kita perlu mengatur konfigurasi mysql dahulu seperti kode berikut.
```
echo '# This group is read both by the client and the server
# use it for options that affect everything
[client-server]

# Import all .cnf files from configuration directory
!includedir /etc/mysql/conf.d/
!includedir /etc/mysql/mariadb.conf.d/

# Options affecting the MySQL server (mysqld)
[mysqld]
skip-networking=0
skip-bind-address
' > /etc/mysql/my.cnf
```
Lalu mengatur mengubah `bind-address` menjadi `0.0.0.0` pada file `/etc/mysql/mariadb.conf.d/50-server.cnf`. Jangan lupa untuk merestart mysql. </br>
Setelah itu membuat user `kelompoke09` dengan password `passworde09`, membuat database `dbkelompoke09`, dan jangan lupa untuk grant all privileges untuk user tersebut.

```
CREATE USER 'kelompoke09'@'%' IDENTIFIED BY 'passworde09';
CREATE USER 'kelompoke09'@'localhost' IDENTIFIED BY 'passworde09';
CREATE DATABASE dbkelompoke09;
GRANT ALL PRIVILEGES ON *.* TO 'kelompoke09'@'%';
GRANT ALL PRIVILEGES ON *.* TO 'kelompoke09'@'localhost';
FLUSH PRIVILEGES;
```
![image](https://github.com/farah-dhiaf/Jarkom-Modul-3-E09-2023/assets/91003215/f08a5292-f642-48b3-950a-d02c17e12c9f)

### Output
Run perintah `mariadb --host=10.41.2.1 --port=3306 --user=kelompoke09 --password=passworde09` di client.
![image](https://github.com/farah-dhiaf/Jarkom-Modul-3-E09-2023/assets/91003215/2bfb2df0-71e9-4c46-92ea-04bdb70b184e)

## Soal 14
Frieren, Flamme, dan Fern memiliki Riegel Channel sesuai dengan quest guide berikut. Jangan lupa melakukan instalasi PHP8.0 dan Composer
### Jawaban
Pada worker Laravel, perlu menginstall PHP8.0 dan composer terlebih dahulu.
```
wget https://getcomposer.org/download/2.0.13/composer.phar
chmod +x composer.phar
mv composer.phar /usr/local/bin/composer
```
Lalu melakukan clone resource yang telah disediakan di soal.
```
apt-get install git -y
cd /var/www && git clone https://github.com/martuafernando/laravel-praktikum-jarkom
cd /var/www/laravel-praktikum-jarkom && composer update
```
Setelah itu perlu melakukan konfigurasi untuk setiap worker Laravel.
```
cd /var/www/laravel-praktikum-jarkom && cp .env.example .env
echo 'APP_NAME=Laravel
APP_ENV=local
APP_KEY=
APP_DEBUG=true
APP_URL=http://localhost

LOG_CHANNEL=stack
LOG_DEPRECATIONS_CHANNEL=null
LOG_LEVEL=debug

DB_CONNECTION=mysql
DB_HOST=10.41.2.1
DB_PORT=3306
DB_DATABASE=dbkelompoke09
DB_USERNAME=kelompoke09
DB_PASSWORD=passworde09

BROADCAST_DRIVER=log
CACHE_DRIVER=file
FILESYSTEM_DISK=local
QUEUE_CONNECTION=sync
SESSION_DRIVER=file
SESSION_LIFETIME=120

MEMCACHED_HOST=127.0.0.1

REDIS_HOST=127.0.0.1
REDIS_PASSWORD=null
REDIS_PORT=6379

MAIL_MAILER=smtp
MAIL_HOST=mailpit
MAIL_PORT=1025
MAIL_USERNAME=null
MAIL_PASSWORD=null
MAIL_ENCRYPTION=null
MAIL_FROM_ADDRESS="hello@example.com"
MAIL_FROM_NAME="${APP_NAME}"

AWS_ACCESS_KEY_ID=
AWS_SECRET_ACCESS_KEY=
AWS_DEFAULT_REGION=us-east-1
AWS_BUCKET=
AWS_USE_PATH_STYLE_ENDPOINT=false

PUSHER_APP_ID=
PUSHER_APP_KEY=
PUSHER_APP_SECRET=
PUSHER_HOST=
PUSHER_PORT=443
PUSHER_SCHEME=https
PUSHER_APP_CLUSTER=mt1

VITE_PUSHER_APP_KEY="${PUSHER_APP_KEY}"
VITE_PUSHER_HOST="${PUSHER_HOST}"
VITE_PUSHER_PORT="${PUSHER_PORT}"
VITE_PUSHER_SCHEME="${PUSHER_SCHEME}"
VITE_PUSHER_APP_CLUSTER="${PUSHER_APP_CLUSTER}"' > /var/www/laravel-praktikum-jarkom/.env
cd /var/www/laravel-praktikum-jarkom && php artisan key:generate
cd /var/www/laravel-praktikum-jarkom && php artisan config:cache
cd /var/www/laravel-praktikum-jarkom && php artisan migrate
cd /var/www/laravel-praktikum-jarkom && php artisan db:seed
cd /var/www/laravel-praktikum-jarkom && php artisan storage:link
cd /var/www/laravel-praktikum-jarkom && php artisan jwt:secret
cd /var/www/laravel-praktikum-jarkom && php artisan config:clear
chown -R www-data.www-data /var/www/laravel-praktikum-jarkom/storage
```
Lalu mengatur konfigurasi nginx pada worker tersebut, sesuaikan dengan port yaitu untuk worker Fern yaitu port 8001, worker Flamme yaitu port 8002, dan worker Frieren yaitu port 8003.
```
cp /etc/nginx/sites-available/default /etc/nginx/sites-available/laravel-worker

echo 'server {
    listen <ip>:<port>

    root /var/www/laravel-praktikum-jarkom/public;

    index index.php index.html index.htm;
    server_name _;

    location / {
            try_files $uri $uri/ /index.php?$query_string;
    }

    # pass PHP scripts to FastCGI server
    location ~ \.php$ {
      include snippets/fastcgi-php.conf;
      fastcgi_pass unix:/var/run/php/php8.0-fpm.sock;
    }

    location ~ /\.ht {
            deny all;
    }

    error_log /var/log/nginx/implementasi_error.log;
    access_log /var/log/nginx/implementasi_access.log;
}
' > /etc/nginx/sites-available/laravel-worker
```
Jangan lupa menyimpan symlink dan merestart nginx.
```
ln -s /etc/nginx/sites-available/laravel-worker /etc/nginx/sites-enabled/
service nginx restart
```
### Output
Melakukan perintah `lynx localhost:<port>` pada worker.
![image](https://github.com/farah-dhiaf/Jarkom-Modul-3-E09-2023/assets/91003215/f9dbfa5a-6aae-4d72-9c60-f69680ec0afc)

## Soal 15
Riegel Channel memiliki beberapa endpoint yang harus ditesting sebanyak 100 request dengan 10 request/second. Tambahkan response dan hasil testing pada grimoire.</br>
a. POST /auth/register
### Jawaban
Dalam melakukan testing ini, kami menggunakan file register.json untuk membantu mengirim data username dan password untuk melakukan register.
```
echo '
{
  "username": "kelompoke09",
  "password": "passworde09"
}
' > register.json
```
### Output
Run command berikut di client.
`ab -n 100 -c 10 -p register.json -T application/json http://10.41.4.2:8002/api/auth/register`
![image](https://github.com/farah-dhiaf/Jarkom-Modul-3-E09-2023/assets/91003215/eb59d6ba-4058-43f5-b7ac-02430e028206)
![image](https://github.com/farah-dhiaf/Jarkom-Modul-3-E09-2023/assets/91003215/30c933c0-6f73-4aa1-92b2-2f38d24a7258)

## Soal 16
b. POST /auth/login

### Jawaban
Dalam melakukan testing ini, kami menggunakan file login.json untuk membantu mengirim data username dan password untuk melakukan login.
```
echo '
{
  "username": "kelompoke09",
  "password": "passworde09"
}
' > login.json
```
### Output
Run command berikut di client.
`ab -n 100 -c 10 -p login.json -T application/json http://10.41.4.2:8002/api/auth/login`
![image](https://github.com/farah-dhiaf/Jarkom-Modul-3-E09-2023/assets/91003215/3f353aab-d683-450d-a01f-9bd3f40ab93f)
![image](https://github.com/farah-dhiaf/Jarkom-Modul-3-E09-2023/assets/91003215/5c7972f2-66b0-4d3a-9548-ec100260adfd)

## Soal 17
c. GET /me
### Jawaban
Untuk mengakses endpoint `/api/me` perlu didapatkan tokennya terlebih dahulu dengan command berikut.
`curl -X POST -H "Content-Type: application/json" -d @login.json http://10.41.4.2:8002/api/auth/login > login_output.txt`
![image](https://github.com/farah-dhiaf/Jarkom-Modul-3-E09-2023/assets/91003215/731decad-847b-4b9a-878f-7d8264c922b4)
Lalu set token secara global.
`token=$(cat login_output.txt | jq -r '.token')`

### Output
Melakukan testing dengan command berikut di client.
`ab -n 100 -c 10 -H "Authorization: Bearer $token" http://10.41.4.2:8002/api/me`
![image](https://github.com/farah-dhiaf/Jarkom-Modul-3-E09-2023/assets/91003215/8aa55e8e-d1ac-4a1d-aa9f-ebca0a1b3201)
![image](https://github.com/farah-dhiaf/Jarkom-Modul-3-E09-2023/assets/91003215/f7f52a9f-0a49-479e-b445-f82310e19d8e)

## Soal 18
Untuk memastikan ketiganya bekerja sama secara adil untuk mengatur Riegel Channel maka implementasikan Proxy Bind pada Eisen untuk mengaitkan IP dari Frieren, Flamme, dan Fern.
### Jawaban
Pada load balancer (Eisen) kita melakukan setup nginx untuk riegel.canyon.e09.com dengan setup seperti berikut.
```
echo 'upstream laravel-worker {
    server 10.41.4.1:8001;
    server 10.41.4.2:8002;
    server 10.41.4.3:8003;
}

server {
    listen 80;
    server_name riegel.canyon.e09.com www.riegel.canyon.e09.com;

    location / {
        proxy_pass http://laravel-worker;
    }
} 
' > /etc/nginx/sites-available/laravel-worker
```
Jangan lupa untuk menyimpan symlink dan melakukan restart nginx.
```
ln -s /etc/nginx/sites-available/laravel-worker /etc/nginx/sites-enabled/laravel-worker

service nginx restart
```
### Output
Melakukan testing dengan command berikut.
```
ab -n 100 -c 10 -p login.json -T application/json http://www.riegel.canyon.e09.com/api/auth/login
```
![image](https://github.com/farah-dhiaf/Jarkom-Modul-3-E09-2023/assets/91003215/03d47239-672f-4c18-9f05-c726572cc3df)
![image](https://github.com/farah-dhiaf/Jarkom-Modul-3-E09-2023/assets/91003215/502b16c2-2f9f-4683-bad0-ee2b3cc26df9)

Melihat access.log pada salah satu worker Laravel.
![image](https://github.com/farah-dhiaf/Jarkom-Modul-3-E09-2023/assets/91003215/6a170669-2747-4062-bcca-708732378099)

## Soal 19
Untuk meningkatkan performa dari Worker, coba implementasikan PHP-FPM pada Frieren, Flamme, dan Fern. Untuk testing kinerja naikkan 
- pm.max_children
- pm.start_servers
- pm.min_spare_servers
- pm.max_spare_servers
sebanyak tiga percobaan dan lakukan testing sebanyak 100 request dengan 10 request/second kemudian berikan hasil analisisnya pada Grimoire.
### Jawaban 
Untuk soal ini kita hanya perlu mengatur pm.max_children, pm.start_servers, pm.min_spare_servers, dan pm.max_spare_servers untuk dibandingkan hasilnya. Konfigurasi akan diatur dalam file PHP-FPM `/etc/php/8.0/fpm/pool.d/www.conf`.

Kombinasi pertama
```
pm = dynamic
pm.max_children = 10
pm.start_servers = 5
pm.min_spare_servers = 1
pm.max_spare_servers = 10
```
Kedua
```
pm = dynamic
pm.max_children = 25
pm.start_servers = 10
pm.min_spare_servers = 5
pm.max_spare_servers = 15
```
Ketiga
```
pm = dynamic
pm.max_children = 75
pm.start_servers = 15
pm.min_spare_servers = 8
pm.max_spare_servers = 20
```
Jangan lupa untuk melakukan restart PHP-FPM setelah mengatur konfigurasinya dengan `service php8.0-fpm restart`

### Output
Melakukan testing dengan `ab -n 100 -c 10 -p login.json -T application/json http://www.riegel.canyon.e09.com/api/auth/login` pada client.
#### Kombinasi 1
![image](https://github.com/farah-dhiaf/Jarkom-Modul-3-E09-2023/assets/91003215/76ee0a1f-7661-42e0-91c9-769b4fd4109d)
![image](https://github.com/farah-dhiaf/Jarkom-Modul-3-E09-2023/assets/91003215/3c210318-aa43-49cf-a6e1-c421616b41f3)
#### Kombinasi 2
![image](https://github.com/farah-dhiaf/Jarkom-Modul-3-E09-2023/assets/91003215/a31f735a-ff3d-4e4d-9b66-084f1aa857a2)
![image](https://github.com/farah-dhiaf/Jarkom-Modul-3-E09-2023/assets/91003215/954b91cc-c8e4-4564-a21e-8ce45ae858f3)
#### Kombinasi 3
![image](https://github.com/farah-dhiaf/Jarkom-Modul-3-E09-2023/assets/91003215/a22723ed-d797-4c71-b13a-69c7e330345e)
![image](https://github.com/farah-dhiaf/Jarkom-Modul-3-E09-2023/assets/91003215/51467a4b-62f4-49eb-a72f-78f075a77f94)

## Soal 20
Nampaknya hanya menggunakan PHP-FPM tidak cukup untuk meningkatkan performa dari worker maka implementasikan Least-Conn pada Eisen. Untuk testing kinerja dari worker tersebut dilakukan sebanyak 100 request dengan 10 request/second. 
### Jawaban
Menambahkan algoritma least connection pada load balancer, berikut setup nginx-nya.
```
echo 'upstream laravel-worker {
    least_conn;
    server 10.41.4.1:8001;
    server 10.41.4.2:8002;
    server 10.41.4.3:8003;
}

server {
    listen 80;
    server_name riegel.canyon.e09.com www.riegel.canyon.e09.com;

    location / {
        proxy_pass http://laravel-worker;
    }
} 
' > /etc/nginx/sites-available/laravel-worker
```
Jangan lupa untuk restart nginx dengan `service nginx restart`.

### Output
![image](https://github.com/farah-dhiaf/Jarkom-Modul-3-E09-2023/assets/91003215/8b1f863d-6fa5-4974-971c-877072994be7)
![image](https://github.com/farah-dhiaf/Jarkom-Modul-3-E09-2023/assets/91003215/76468e0b-2755-40b2-bb77-c42c73298103)

## Kendala
Soal terlalu banyak dengan waktu pengerjaan yang terlalu singkat, terlebih dengan soal analisis yang cukup menguli. Materi reverse proxy juga masih belum terlalu paham implementasinya sehingga masih banyak error dan struggle dalam pengerjaannya. 
