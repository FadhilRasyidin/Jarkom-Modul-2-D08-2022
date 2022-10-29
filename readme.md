## Anggota Kelompok

- Mohammad Fadhil Rasyidin Parinduri // 5025201131
- Marcelino Salim // 5025201026
- Aisyah Nurhalimah // 5025201081 (juara harapan 1 basket dies natalis)

### Soal Shift

- [link](https://docs.google.com/document/d/11Mz2Fd3DKtGkCknHee9VZRdJYvZ3YAMIaifObHEpBFo/edit?usp=sharing)

Kendala:

1. banyak tugas sedikit waktu (butuh introspeksi diri untuk memperbaiki manajemen waktu)
2. hehe

# Laporan Resmi
## Daftar Isi
- [Laporan Resmi](#laporan-resmi)
  - [Daftar Isi](#daftar-isi)
  - [Topologi](#topologi)
  - [Config](#config)
  - [Sebelum Memulai](#sebelum-memulai)
- [Soal 1](#soal-1)
- [Soal 2](#soal-2)
    - [Test](#test)
- [Soal 3](#soal-3)
    - [Script](#script)
    - [Test](#test-1)
- [Soal 4](#soal-4)
    - [Script](#script-1)
    - [Test](#test-2)
- [Soal 5](#soal-5)
    - [Script](#script-2)
    - [Test](#test-3)
- [Soal 6](#soal-6)
- [Soal 7](#soal-7)
- [Soal 8](#soal-8)
- [Soal 9](#soal-9)
- [Soal 10](#soal-10)
- [Soal 11](#soal-11)
- [Soal 12](#soal-12)
- [Soal 13](#soal-13)
- [Soal 14](#soal-14)
- [Soal 15](#soal-15)
- [Soal 16](#soal-16)
- [Soal 17](#soal-17)


## Topologi
<img width="620" alt="image" src="https://user-images.githubusercontent.com/73109893/198057634-f58d1a5f-1718-40af-95d1-28e4d13a164e.png">

## Config

- **Ostania**
    
    ```
    auto eth0
    iface eth0 inet dhcp

    auto eth1
    iface eth1 inet static
	    address 10.19.1.1
	    netmask 255.255.255.0

    auto eth2
    iface eth2 inet static
	    address 10.19.2.1
	    netmask 255.255.255.0

    auto eth3
    iface eth3 inet static
	    address 10.19.3.1
	    netmask 255.255.255.0
    ```

- **WISE**
    
    ```
    auto eth0
    iface eth0 inet static
	    address 10.19.1.2
	    netmask 255.255.255.0
	    gateway 10.19.1.1
    ```

- **SSS**
    
    ```
    auto eth0
    iface eth0 inet static
        address 10.19.2.2
        netmask 255.255.255.0
        gateway 10.19.2.1
    ```

- **Garden**
    
    ```
    auto eth0
    iface eth0 inet static
        address 10.19.2.3
        netmask 255.255.255.0
        gateway 10.19.2.1
    ```

- **Berlint**
    
    ```
    auto eth0
    iface eth0 inet static
        address 10.19.3.2
        netmask 255.255.255.0
        gateway 10.19.3.1
    ```

- **Eden**
    
    ```
    auto eth0
    iface eth0 inet static
        address 10.19.3.3
        netmask 255.255.255.0
        gateway 10.19.3.1
    ```

## Sebelum Memulai

setiap node, kita inisiasi pada `.bashrc` menggunakan `nano`

- **Ostania**
    
    ```
    apt-get update
    apt-get install nano -y
    iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE -s 192.178.0.0/16
    ```

- **Eden**
    
    ```
    echo 'nameserver 192.168.122.1' > /etc/resolv.conf
    apt-get update
    apt-get install nano -y
    apt-get install dnsutils -y
    apt-get install lynx -y
    apt-get install apache2 -y
    apt-get install bind9 -y
    apt-get install libapache2-mod-php7.0 -y
    service apache2 start
    apt-get install wget -y
    apt-get install unzip -y
    apt-get install php -y
    echo -e "\n\nPHP Ver:"
    php -v
    cd /var/www
    wget 'https://github.com/FadhilRasyidin/Jarkom-Modul-2-D08-2022/raw/main/resources/wise.zip'
    wget 'https://github.com/FadhilRasyidin/Jarkom-Modul-2-D08-2022/raw/main/resources/eden.wise.zip'
    wget 'https://github.com/FadhilRasyidin/Jarkom-Modul-2-D08-2022/raw/main/resources/strix.operation.wise.zip'
    unzip wise.zip
    unzip eden.wise.zip
    unzip strix.operation.wise.zip
    cd ~
    ```

- **Sisanya (SSS, Garden, Berlint, WISE)**
    
    ```
    echo 'nameserver 192.168.122.1' > /etc/resolv.conf
    apt-get update
    apt-get install nano -y
    apt-get install dnsutils -y
    apt-get install lynx -y
    apt-get install apache2 -y
    apt-get install bind9 -y
    service apache2 start
    apt-get install php -y
    echo -e "\n\nPHP Ver:"
    php -v
    ```

# Soal 1
> WISE akan dijadikan sebagai DNS Master, Berlint akan dijadikan DNS Slave, dan Eden akan digunakan sebagai Web Server. Terdapat 2 Client yaitu SSS, dan Garden. Semua node terhubung pada router Ostania, sehingga dapat mengakses internet 

Setelah berhasil melakukan konfigurasi, akan dilakukan pengecekan internet untuk semua node dengan melakukan `ping google.com`

![p2_2](https://user-images.githubusercontent.com/81240334/198823214-53bc659c-d7c6-4f4d-a3b7-2d9d75237149.jpeg)
![p2_1](https://user-images.githubusercontent.com/81240334/198823215-e2694b34-e29c-4d02-b970-e7653562fe8d.jpeg)
![Wise ping](https://user-images.githubusercontent.com/81240334/198823210-45e41db3-19d2-41ef-a44b-5a632b809a14.jpg)

# Soal 2
> Untuk mempermudah mendapatkan informasi mengenai misi dari Handler, buat website utama dengan akses **wise.yyy.com** dengan alias **www.wise.yyy.com** pada folder wise 

> Script dibawah ini terdapat pada **root node WISE**, untuk menjalankannya bisa langsung dengan melakukan command `bash no2.sh`
- **WISE**
    ```
    echo -e '
    zone "wise.d08.com" {
            type master;
            file "/etc/bind/wise/wise.b11.com";
    };
     ' > /etc/bind/named.conf.local
    mkdir /etc/bind/wise
    echo -e '
    ;
    ; BIND data file for local loopback interface
    ;
    $TTL    604800
    @       IN      SOA     wise.d08.com. root.wise.d08.com. (
                                  2         ; Serial
                             604800         ; Refresh
                              86400         ; Retry
                            2419200         ; Expire
                             604800 )       ; Negative Cache TTL
    ;
    @       IN      NS      wise.d08.com.
    @       IN      A       10.19.1.2	; IP WISE
    www	IN	CNAME	wise.d08.com.
    ' > /etc/bind/wise/wise.d08.com
    service bind9 restart
    ```

Kemudian pada node client (SSS & Garden), kita harus lakukan setting nameserver yang ada. Kemudian kita akan mengecek dengan melakukan `host -t CNAME www.wise.d08.com` dan `www.wise.d08.com -c 3`.

> Script dibawah ini terdapat pada **root node SSS & Garden**, untuk menjalankannya bisa langsung dengan melakukan command `bash no2.sh`
- **SSS & Garden**
    
    ```
    echo "TEST ALIAS (CNAME) (alias dari wise.B11.com)"
    host -t CNAME www.wise.d08.com
    echo "TEST ARAH PING www.wise.d08.com (mengarah ke host IP WISE)"
    ping www.wise.d08.com -c 3
    ```

### Test

# Soal 3
> Setelah itu ia juga ingin membuat subdomain **eden.wise.yyy.com** dengan alias **www.eden.wise.yyy.com** yang diatur DNS-nya di WISE dan mengarah ke Eden 

### Script

Untuk membuat subdomain kita harus menambahkan `eden            IN      A       10.19.2.3             ; IP Eden` pada file `/etc/bind/wise/wise.d08.com`. Kemudian tambahkan juga `www.eden        IN      CNAME   eden.wise.d08.com.` pada file yang sama. Setelah selesai maka kita harus merestart bind9 dengan command `service bind9 restart`.

> Script dibawah ini terdapat pada **root node WISE**, untuk menjalankannya bisa langsung dengan melakukan command `bash no3.sh`
- **WISE**
    
    ```
    echo -e '
    ;
    ; BIND data file for local loopback interface
    ;
    $TTL    604800
    @       IN      SOA     wise.d08.com. root.wise.d08.com. (
                                  2         ; Serial
                             604800         ; Refresh
                              86400         ; Retry
                            2419200         ; Expire
                             604800 )       ; Negative Cache TTL
    ;
    @       	IN      NS      wise.d08.com.
    @       	IN      A       10.19.1.2     	; IP WISE
    www     	IN      CNAME   wise.d08.com.
    eden		IN	A	10.19.3.3		; IP Eden
    www.eden	IN	CNAME	eden.wise.d08.com.
    ' > /etc/bind/wise/wise.d08.com
    service bind9 restart
    ```

Kemudian kita akan mengecek dengan melakukan test ping `ping eden.wise.d08.com -c 3` dan test cname `host -t CNAME www.eden.wise.d08.com`.

> Script dibawah ini terdapat pada **root node SSS & Garden**, untuk menjalankannya bisa langsung dengan melakukan command `bash no3.sh`
- **SSS & Garden**
    
    ```
    echo "TEST PING SUBDOMAIN (mengarah ke host IP Eden)"
    ping eden.wise.d08.com -c 3
    echo "TEST ALIAS (CNAME) (alias dari  eden.wise.B11.com)"
    host -t CNAME www.eden.wise.d08.com
    ``` 

### Test

# Soal 4
> Buat juga reverse domain untuk domain utama 

### Script

Untuk membuat reverse domain kita memerlukan tambahan Zone Baru, tambahkan zone tersebut pada file `/etc/bind/named.conf.local` sesuai dengan ip kita.  Kemudian buatlah sebuah file pada direktori `/etc/bind/wise/` dengan nama file `"3 byte reverse ip kita".in-addr.arpa`. Setelah selesai maka kita harus merestart bind9 dengan command `service bind9 restart`.

> Script dibawah ini terdapat pada **root node WISE**, untuk menjalankannya bisa langsung dengan melakukan command `bash no4.sh`
- **WISE**
    
    ```
    echo -e '
    zone "wise.d08.com" {
            type master;
            file "/etc/bind/wise/wise.d08.com";
    };
    zone "1.19.10.in-addr.arpa" {
        type master;
        file "/etc/bind/wise/1.19.10.in-addr.arpa";
    };
     ' > /etc/bind/named.conf.local
    echo -e '
    $TTL    604800
    @       IN      SOA     wise.d08.com. root.wise.d08.com. (
                                  2         ; Serial
                             604800         ; Refresh
                              86400         ; Retry
                            2419200         ; Expire
                             604800 )       ; Negative Cache TTL
    ;
    1.19.10.in-addr.arpa.    IN     NS      wise.d08.com.
    2                      	   IN     PTR     wise.d08.com.
    ' > /etc/bind/wise/1.19.10.in-addr.arpa
    service bind9 restart
    ```

Kemudian kita akan mengecek reverse domain dengan melakukan `host -t PTR 10.19.1.2`.

> Script dibawah ini terdapat pada **root node SSS & Garden**, untuk menjalankannya bisa langsung dengan melakukan command `bash no4.sh`
- **SSS & Garden**
    
    ```
    echo "TES REVERSE DOMAIN (point to wise.b11.com.)"
    host -t PTR 10.19.1.2
    ``` 

### Test

# Soal 5
> Agar dapat tetap dihubungi jika server WISE bermasalah, buatlah juga Berlint sebagai DNS Slave untuk domain utama

### Script

Setelah selesai maka kita harus merestart bind9 dengan command `service bind9 restart`.

> Script dibawah ini terdapat pada **root node WISE**, untuk menjalankannya bisa langsung dengan melakukan command `bash no5.sh`
Konfigurasi server WISE dengan menuliskan syntax seperti di bawah ini di file /etc/bin/named.conf.local
- **WISE**
    
    ```
    echo -e '
    zone "wise.d08.com" {
            type master;
    	notify yes;
    	also-notify { 10.19.3.2; }; // Masukan IP Berlint tanpa tanda petik
    	allow-transfer { 10.19.3.2; }; // Masukan IP Berlint tanpa tanda petik
    	file "/etc/bind/wise/wise.d08.com";
    };
    zone "1.19.10.in-addr.arpa" {
        type master;
        file "/etc/bind/wise/1.19.10.in-addr.arpa";
    };
     ' > /etc/bind/named.conf.local
    service bind9 restart
    ```

Setelah selesai maka kita harus merestart bind9 dengan command `service bind9 restart`.

> Script dibawah ini terdapat pada **root node Berlint**, untuk menjalankannya bisa langsung dengan melakukan command `bash no5.sh`
- **Berlint**
    
    ```
    echo -e '
    zone "wise.d08.com" {
        type slave;
        masters { 10.19.1.2; }; // Masukan IP WISE tanpa tanda petik
        file "/var/lib/bind/wise.b11.com";
    };
     ' > /etc/bind/named.conf.local
    service bind9 restart
    ```

Pada server WISE kita akan mematikan service bind9 dengan command `service bind9 stop`

> Script dibawah ini terdapat pada **root node SSS & Garden**, untuk menjalankannya bisa langsung dengan melakukan command `bash no5test.sh`
- **WISE**
    
    ```
    echo "DNS MASTER STOP"
    service bind9 stop
    ```

Kemudian pada node client (SSS & Garden), kita harus menambahkan nameserver Berlint. Kemudian setelah mematikan server WISE, kita akan mengecek dengan melakukan `ping wise.d08.com -c 3`. Jika ping berhasil maka konfigurasi DNS Slave telah berhasil.

> Script dibawah ini terdapat pada **root node SSS & Garden**, untuk menjalankannya bisa langsung dengan melakukan command `bash no5.sh`
- **SSS & Garden**
    
    ```
    echo "TES SLAVE DNS, DNS MASTER DI STOP"
    ping wise.d08.com -c 3
    ``` 

### Test

# Soal 6
> Karena banyak informasi dari Handler, buat subdomain yang khusus untuk operation yaitu **operation.wise.yyy.com** dengan alias **www.operation.wise.yyy.com** yang didelegasikan dari WISE ke Berlint dengan IP menuju ke Eden dalam folder operation 

# Soal 7
> Untuk informasi yang lebih spesifik mengenai Operation Strix, buatlah subdomain melalui Berlint dengan akses **strix.operation.wise.yyy.com** dengan alias **www.strix.operation.wise.yyy.com** yang mengarah ke Eden

# Soal 8
> Setelah melakukan konfigurasi server, maka dilakukan konfigurasi Webserver. 
Pertama dengan webserver **www.wise.yyy.com**. Pertama, Loid membutuhkan webserver dengan DocumentRoot pada /var/www/wise.yyy.com 

# Soal 9
> Setelah itu, Loid juga membutuhkan agar url **www.wise.yyy.com/index.php/home** dapat menjadi menjadi **www.wise.yyy.com/home**

# Soal 10
> Setelah itu, pada subdomain **www.eden.wise.yyy.com**, Loid membutuhkan penyimpanan aset yang memiliki DocumentRoot pada /var/www/eden.wise.yyy.com 

# Soal 11
> Pada folder /public, Loid ingin hanya dapat melakukan directory listing saja 

# Soal 12
> Tidak hanya itu, Loid juga ingin menyiapkan error file 404.html pada folder /error untuk mengganti error kode pada apache

# Soal 13
> Loid juga meminta Franky untuk dibuatkan konfigurasi virtual host. Virtual host ini bertujuan untuk dapat mengakses file asset **www.eden.wise.yyy.com/public/js** menjadi **www.eden.wise.yyy.com/js**

# Soal 14
> Loid meminta agar **www.strix.operation.wise.yyy.com** hanya bisa diakses dengan port 15000 dan port 15500 

# Soal 15
> dengan autentikasi username Twilight dan password opStrix dan file di /var/www/strix.operation.wise.yyy 

# Soal 16
> dan setiap kali mengakses IP Eden akan dialihkan secara otomatis ke **www.wise.yyy.com**

# Soal 17
> Karena website **www.eden.wise.yyy.com** semakin banyak pengunjung dan banyak modifikasi sehingga banyak gambar-gambar yang random, maka Loid ingin mengubah request gambar yang memiliki substring “eden” akan diarahkan menuju eden.png. Bantulah Agent Twilight dan Organisasi WISE menjaga perdamaian! 

yeayy
