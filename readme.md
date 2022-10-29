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
    - [Script](#script-3)
    - [Test](#test-4)
- [Soal 7](#soal-7)
    - [Script](#script-4)
    - [Test](#test-5)
- [Soal 8](#soal-8)
    - [Script](#script-5)
    - [Test](#test-6)
- [Soal 9](#soal-9)
    - [Script](#script-6)
    - [Test](#test-7)
- [Soal 10](#soal-10)
    - [Script](#script-7)
    - [Test](#test-8)
- [Soal 11](#soal-11)
    - [Script](#script-8)
    - [Test](#test-9)
- [Soal 12](#soal-12)
    - [Script](#script-9)
    - [Test](#test-10)
- [Soal 13](#soal-13)
    - [Script](#script-10)
    - [Test](#test-11)
- [Soal 14](#soal-14)
    - [Script](#script-11)
    - [Test](#test-12)
- [Soal 15](#soal-15)
    - [Script](#script-12)
    - [Test](#test-13)
- [Soal 16](#soal-16)
    - [Script](#script-13)
    - [Test](#test-14)
- [Soal 17](#soal-17)
    - [Script](#script-14)
    - [Test](#test-15)


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

- **Master & Slave**
    
    ```
    # ~/.bashrc: executed by bash(1) for non-login shells.
    # see /usr/share/doc/bash/examples/startup-files (in the package bash-doc)
    # for examples
    ...
    echo 'nameserver 192.168.122.1' > /etc/resolv.conf
    apt-get update
    apt-get install bind9 -y
    ```

- **Client**

    ```
    # ~/.bashrc: executed by bash(1) for non-login shells.
    # see /usr/share/doc/bash/examples/startup-files (in the package bash-doc)
    # for examples
    ...
    echo -e '
    nameserver 10.19.1.2
    nameserver 10.19.3.2
    nameserver 192.168.122.1
    ' > /etc/resolv.conf
    apt-get update
    apt-get install dnsutils
    apt-get install lynx
    ```

- **Web Server**
    
    ```
    echo 'nameserver 192.168.122.1' > /etc/resolv.conf
    apt-get update
    apt-get install apache2
    apt-get install libapache2-mod-php7.0
    service apache2 start
    apt-get install wget -y
    apt-get install unzip -y
    apt-get install php
    echo -e "\n\nPHP Version:"
    php -v
    cd /var/www
    wget 'https://github.com/FadhilRasyidin/Jarkom-Modul-2-D08-2022/raw/main/resources/wise.zip'
    wget 'https://github.com/FadhilRasyidin/Jarkom-Modul-2-D08-2022/raw/main/resources/eden.wise.zip'
    wget 'https://github.com/FadhilRasyidin/Jarkom-Modul-2-D08-2022/raw/main/resources/strix.operation.wise.zip'
    unzip wise.zip
    unzip eden.wise.zip
    unzip strix.operation.wise.zip
    rm wise.zip
    rm eden.wise.zip
    rm strix.operation.wise.zip
    ```

# Soal 1
> WISE akan dijadikan sebagai DNS Master, Berlint akan dijadikan DNS Slave, dan Eden akan digunakan sebagai Web Server. Terdapat 2 Client yaitu SSS, dan Garden. Semua node terhubung pada router Ostania, sehingga dapat mengakses internet 

- **Semua Node** 
    ```
    echo "ping bang"
    ping google.com -c 3
    ```

Setelah berhasil melakukan konfigurasi, akan dilakukan pengecekan internet untuk semua node dengan melakukan `ping google.com`

<img width="622" alt="image" src="https://user-images.githubusercontent.com/73109893/198839687-3d8750dd-2620-422a-88a4-c8c8f5cf1db2.png">
<img width="646" alt="image" src="https://user-images.githubusercontent.com/73109893/198839699-472b4345-d9c9-4529-bb23-936926c9555c.png">
<img width="621" alt="image" src="https://user-images.githubusercontent.com/73109893/198839709-a9345570-e99a-4531-9e67-ad8a09fdb4a0.png">
<img width="636" alt="image" src="https://user-images.githubusercontent.com/73109893/198839728-4aa04563-fd4c-4e55-b2f4-883f1f447a6a.png">
<img width="613" alt="image" src="https://user-images.githubusercontent.com/73109893/198839742-a8699dc7-e891-4513-bccf-84701d244aef.png">

# Soal 2
> Untuk mempermudah mendapatkan informasi mengenai misi dari Handler, buat website utama dengan akses **wise.yyy.com** dengan alias **www.wise.yyy.com** pada folder wise 

Pertama-tama pada node WISE (Master), kita harus konfigurasikan `/etc/bind/named.conf.local` dengan domain wise.B11.com. Setelah itu buatlah direktori `/etc/bind/wise`. Kemudian buatlah file `wise.B11.com` pada direktori yang baru saja dibuat dan isilah file sesuai dengan contoh dibawah ini (setelah command `mkdir /etc/bind/wise`). Setelah selesai maka kita harus merestart bind9 dengan command `service bind9 restart`.

> Script dibawah ini terdapat pada **root node WISE**, untuk menjalankannya bisa langsung dengan melakukan command `bash no2.sh`
- **WISE**
    ```
    echo -e '
    zone "wise.d08.com" {
            type master;
            file "/etc/bind/wise/wise.d08.com";
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
    echo "tes alias (CNAME) (alias dari wise.d08.com)"
    host -t CNAME www.wise.d08.com
    echo "tes arah ping www.wise.d08.com (mengarah ke host IP WISE)"
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
    echo "TEST ALIAS (CNAME) (alias dari  eden.wise.d08.com)"
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
    echo "TES REVERSE DOMAIN (point to wise.d08.com.)"
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
        file "/var/lib/bind/wise.d08.com";
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

### Script

Setelah selesai maka kita harus merestart bind9 dengan command `service bind9 restart`.

> Script dibawah ini terdapat pada **root node WISE**, untuk menjalankannya bisa langsung dengan melakukan command `bash no6.sh`
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
    @               	IN      NS      wise.d08.com.
    @               	IN      A       10.19.1.2             ; IP WISE
    www             	IN      CNAME   wise.d08.com.
    eden            	IN      A       10.19.3.3             ; IP Eden
    www.eden	        IN      CNAME   eden.wise.d08.com.      ; IP Eden
    ns1			IN	A	10.19.3.2		; IP Berlint
    operation		IN	NS	ns1
    ' > /etc/bind/wise/wise.d08.com
    echo -e '
    zone "wise.d08.com" {
            type master;
    	notify yes;
            also-notify { 10.19.3.2; }; // Masukan IP Berlint tanpa tanda petik
            allow-transfer { 10.19.3.2; }; // Masukan IP Berlint tanpa tanda petik
    	file "/etc/bind/wise/wise.d08.com";
    };
    zone "2.19.10.in-addr.arpa" {
        type master;
        file "/etc/bind/wise/2.19.10.in-addr.arpa";
    };
    ' > /etc/bind/named.conf.local
    echo -e '
    options {
            directory "/var/cache/bind";
            // If there is a firewall between you and nameservers you want
            // to talk to, you may need to fix the firewall to allow multiple
            // ports to talk.  See http://www.kb.cert.org/vuls/id/800113
               forwarders {
                    192.168.122.1;
               };
            //========================================================================
            // If BIND logs error messages about the root key being expired,
            // you will need to update your keys.  See https://www.isc.org/bind-keys
            //========================================================================
            //dnssec-validation auto;
            allow-query{any;};
            auth-nxdomain no;    # conform to RFC1035
            listen-on-v6 { any; };
    };
    ' > /etc/bind/named.conf.options
    service bind9 restart
    ```

Setelah selesai maka kita harus merestart bind9 dengan command `service bind9 restart`.

> Script dibawah ini terdapat pada **root node Berlint**, untuk menjalankannya bisa langsung dengan melakukan command `bash no6.sh`
- **Berlint**
    
    ```
    echo -e '
    options {
            directory "/var/cache/bind";
            // If there is a firewall between you and nameservers you want
            // to talk to, you may need to fix the firewall to allow multiple
            // ports to talk.  See http://www.kb.cert.org/vuls/id/800113
            // forwarders {
            //      0.0.0.0;
            // };
            //========================================================================
            // If BIND logs error messages about the root key being expired,
            // you will need to update your keys.  See https://www.isc.org/bind-keys
            //========================================================================
            //dnssec-validation auto;
            allow-query{any;};
            auth-nxdomain no;    # conform to RFC1035
            listen-on-v6 { any; };
    };
    ' > /etc/bind/named.conf.options
    echo -e '
    zone "wise.d08.com" {
        type slave;
        masters { 10.19.1.2; }; // Masukan IP WISE tanpa tanda petik
        file "/var/lib/bind/wise.d08.com";
    };
    zone "operation.wise.d08.com" {
            type master;
            file "/etc/bind/operation/operation.wise.d08.com";
    };
    ' > /etc/bind/named.conf.local
    // Buat folder operation
    mkdir /etc/bind/operation
    echo -e '
    $TTL    604800
    @       IN      SOA     operation.wise.d08.com. root.operation.wise.d08.com. (
                                  2         ; Serial
                             604800         ; Refresh
                              86400         ; Retry
                            2419200         ; Expire
                             604800 )       ; Negative Cache TTL
    ;
    @       	IN      NS          operation.wise.d08.com.
    @       	IN      A           10.19.3.3			; IP Eden
    www       	IN      CNAME       operation.wise.d08.com.
    ' > /etc/bind/operation/operation.wise.d08.com
    service bind9 restart
    ```

Kemudian kita akan mengecek dengan melakukan test ping `ping operation.wise.d08.com -c 3` dan test cname `host -t CNAME www.operation.wise.d08.com`.

Pada Berlint masukkan apa yang ada di file /etc/bind/named.conf.options yang sudah meng-comment bagian `dnssec-validation auto` dan tambahkan `allow-query{any;};` dan edit file /etc/bind/named.conf.local ke file `no.6.sh`.

> Script dibawah ini terdapat pada **root node SSS & Garden**, untuk menjalankannya bisa langsung dengan melakukan command `bash no6.sh`
- **SSS & Garden**
    
    ```
    echo "TEST PING DELEGASI SUBDOMAIN (mengarah ke host IP Eden)"
    ping operation.wise.d08.com -c 3
    echo "TEST ALIAS (CNAME) (alias dari operation.wise.d08.com)"
    host -t CNAME www.operation.wise.d08.com
    ``` 

### Test

# Soal 7
> Untuk informasi yang lebih spesifik mengenai Operation Strix, buatlah subdomain melalui Berlint dengan akses **strix.operation.wise.yyy.com** dengan alias **www.strix.operation.wise.yyy.com** yang mengarah ke Eden

### Script

Setelah selesai maka kita harus merestart bind9 dengan command `service bind9 restart`.

> Script dibawah ini terdapat pada **root node Berlint**, untuk menjalankannya bisa langsung dengan melakukan command `bash no7.sh`
- **Berlint**
    
    ```
    echo -e '
    $TTL    604800
    @       IN      SOA     operation.wise.d08.com. root.operation.wise.d08.com. (
                                  2         ; Serial
                             604800         ; Refresh
                              86400         ; Retry
                            2419200         ; Expire
                             604800 )       ; Negative Cache TTL
    ;
    @               IN      NS		operation.wise.d08.com.
    @               IN      A		10.19.3.3			; IP Eden
    www             IN      CNAME		operation.wise.d08.com.
    strix		IN	A		10.19.3.3			; IP Eden
    www.strix	IN	CNAME		strix.operation.wise.d08.com.
    ' > /etc/bind/operation/operation.wise.d08.com
    service bind9 restart
    ```

Kemudian kita akan mengecek dengan melakukan test ping `ping strix.operation.wise.d08.com. -c 3` dan test cname `ping www.strix.operation.wise.d08.com. -c 1`.

> Script dibawah ini terdapat pada **root node SSS & Garden**, untuk menjalankannya bisa langsung dengan melakukan command `bash no7.sh`
- **SSS & Garden**
    
    ```
    echo "TEST PING SUBDOMAIN (mengarah ke host IP Eden)"
    ping strix.operation.wise.d08.com. -c 3
    echo "TEST ALIAS (CNAME) (alias dari  strix.operation.d08.com)"
    ping www.strix.operation.wise.d08.com. -c 1
    ``` 

### Test

# Soal 8
> Setelah melakukan konfigurasi server, maka dilakukan konfigurasi Webserver. 
Pertama dengan webserver **www.wise.yyy.com**. Pertama, Loid membutuhkan webserver dengan DocumentRoot pada /var/www/wise.yyy.com 

### Script

Setelah selesai maka kita harus merestart bind9 dengan command `service bind9 restart`.

> Script dibawah ini terdapat pada **root node WISE**, untuk menjalankannya bisa langsung dengan melakukan command `bash no8.sh`
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
    @                       IN      NS      wise.d08.com.
    @                       IN      A       10.19.3.3             ; IP Eden
    www                     IN      CNAME   wise.d08.com.
    eden                    IN      A       10.19.3.3             ; IP Eden
    www.eden                IN      CNAME   eden.wise.d08.com.      ; IP Eden
    ns1                     IN      A       10.19.3.2             ; IP Berlint
    operation               IN      NS      ns1
    ' > /etc/bind/wise/wise.d08.com
    service bind9 restart
    ```

Kemudian, edit file `wise.d08.com.conf` lalu tambahkan ServerName dan ServerAlias.

> Script dibawah ini terdapat pada **root node Eden**, untuk menjalankannya bisa langsung dengan melakukan command `bash no8.sh`
- **Eden**
    
    ```
    echo "<VirtualHost *:80>
            ServerAdmin webmaster@localhost
            DocumentRoot /var/www/wise.d08.com
            ServerName wise.d08.com
            ServerAlias www.wise.d08.com
            ErrorLog \${APACHE_LOG_DIR}/error.log
            CustomLog \${APACHE_LOG_DIR}/access.log combined
    </VirtualHost>" > /etc/apache2/sites-available/wise.d08.com.conf
    a2ensite wise.d08.com
    mkdir /var/www/wise.d08.com
    cp -RT /var/www/wise /var/www/wise.d08.com
    service apache2 restart
    ```

Setelah itu, jalankan perintah `lynx wise.d08.com`.

> Script dibawah ini terdapat pada **root node SSS & Garden**, untuk menjalankannya bisa langsung dengan melakukan command `bash no8.sh`
- **SSS & Garden**
    
    ```
    lynx wise.d08.com
    ``` 

### Test

# Soal 9
> Setelah itu, Loid juga membutuhkan agar url **www.wise.yyy.com/index.php/home** dapat menjadi menjadi **www.wise.yyy.com/home**

### Script
Tambahkan `Alias "/home" "/var/www/wise.d08.com/index.php/home"` pada conf agar bisa melakukan direct ke `/index.php/home`.

> Script dibawah ini terdapat pada **root node Eden**, untuk menjalankannya bisa langsung dengan melakukan command `bash no9.sh`
- **Eden**
    
    ```
    echo "<VirtualHost *:80>
            ServerAdmin webmaster@localhost
            DocumentRoot /var/www/wise.d08.com
            ServerName wise.d08.com
            ServerAlias www.wise.d08.com
    	<Directory /var/www/wise.d08.com/index.php/home>
                    Options +Indexes
            </Directory>
            Alias "/home" "/var/www/wise.d08.com/index.php/home"
            ErrorLog \${APACHE_LOG_DIR}/error.log
            CustomLog \${APACHE_LOG_DIR}/access.log combined
    </VirtualHost>" > /etc/apache2/sites-available/wise.d08.com.conf
    a2ensite wise.d08.com
    service apache2 restart
    ```

> Script dibawah ini terdapat pada **root node SSS & Garden**, untuk menjalankannya bisa langsung dengan melakukan command `bash no9.sh`
- **SSS & Garden**
    
    ```
    lynx wise.d08.com/home
    ``` 

### Test

# Soal 10
> Setelah itu, pada subdomain **www.eden.wise.yyy.com**, Loid membutuhkan penyimpanan aset yang memiliki DocumentRoot pada /var/www/eden.wise.yyy.com 

### Script

Lakukan konfigurasi pada `/eden.wise.d08.com`. Lalu, lakukan `a2ensite eden.wise.d08.com` dan `service apache2 restart`.

> Script dibawah ini terdapat pada **root node Eden**, untuk menjalankannya bisa langsung dengan melakukan command `bash no10.sh`
- **Eden**
    
    ```
    a2enmod rewrite
    service apache2 restart
    echo "RewriteEngine On
    RewriteCond %{REQUEST_FILENAME} !-f
    RewriteCond %{REQUEST_FILENAME} !-d
    RewriteRule (.*) /index.php/\$1 [L]" > /var/www/wise.d08.com/.htaccess
    echo "<VirtualHost *:80>
            ServerAdmin webmaster@localhost
            DocumentRoot /var/www/wise.d08.com
            ServerName wise.d08.com
            ServerAlias www.wise.d08.com
            ErrorLog \${APACHE_LOG_DIR}/error.log
            CustomLog \${APACHE_LOG_DIR}/access.log combined
            <Directory /var/www/wise.d08.com>
                    Options +FollowSymLinks -Multiviews
                    AllowOverride All
            </Directory>
    </VirtualHost>" > /etc/apache2/sites-available/wise.d08.com.conf
    service apache2 restart
    echo "<VirtualHost *:80>
            ServerAdmin webmaster@localhost
            DocumentRoot /var/www/eden.wise.d08.com
            ServerName eden.wise.d08.com
            ServerAlias www.eden.wise.d08.com
            ErrorLog \${APACHE_LOG_DIR}/error.log
            CustomLog \${APACHE_LOG_DIR}/access.log combined
            <Directory /var/www/wise.d08.com>
                    Options +FollowSymLinks -Multiviews
                    AllowOverride All
            </Directory>
    </VirtualHost>" > /etc/apache2/sites-available/eden.wise.d08.com.conf
    a2ensite eden.wise.d08.com
    mkdir /var/www/eden.wise.d08.com
    cp -RT /var/www/eden.wise/ /var/www/eden.wise.d08.com
    service apache2 restart
    ```

Setelah itu, jalankan perintah `lynx http://www.eden.wise.d08.com`.

> Script dibawah ini terdapat pada **root node SSS & Garden**, untuk menjalankannya bisa langsung dengan melakukan command `bash no10.sh`
- **SSS & Garden**
    
    ```
    lynx http://www.eden.wise.d08.com
    ``` 

### Test

# Soal 11
> Pada folder /public, Loid ingin hanya dapat melakukan directory listing saja 

### Script

Lakukan konfigurasi pada `/eden.wise.d08.com`. Lalu, tambahkan Options +Indexes pada direktori yang ingin di directory list.

> Script dibawah ini terdapat pada **root node Eden**, untuk menjalankannya bisa langsung dengan melakukan command `bash no11.sh`
- **Eden**
    
    ```
    echo "<VirtualHost *:80>
            ServerAdmin webmaster@localhost
            DocumentRoot /var/www/eden.wise.d08.com
            ServerName eden.wise.d08.com
            ServerAlias www.eden.wise.d08.com
            <Directory /var/www/eden.wise.d08.com/public>
                    Options +Indexes
            </Directory>
            ErrorLog \${APACHE_LOG_DIR}/error.log
            CustomLog \${APACHE_LOG_DIR}/access.log combined
            <Directory /var/www/wise.d08.com>
                    Options +FollowSymLinks -Multiviews
                    AllowOverride All
            </Directory>
    </VirtualHost>" > /etc/apache2/sites-available/eden.wise.d08.com.conf
    service apache2 restart
    ```

Setelah itu, jalankan perintah `lynx http://www.eden.wise.d08.com/public`.

> Script dibawah ini terdapat pada **root node SSS & Garden**, untuk menjalankannya bisa langsung dengan melakukan command `bash no11.sh`
- **SSS & Garden**
    
    ```
    lynx http://www.eden.wise.d08.com/public
    ``` 

### Test

# Soal 12
> Tidak hanya itu, Loid juga ingin menyiapkan error file 404.html pada folder /error untuk mengganti error kode pada apache

### Script

Lakukan konfigurasi pada `/eden.wise.d08.com`. Lalu, tambahkan konfigurasi ErrorDocument agar ketika ada yang error akan diarahkan ke file `/error/404.html`.

> Script dibawah ini terdapat pada **root node Eden**, untuk menjalankannya bisa langsung dengan melakukan command `bash no12.sh`
- **Eden**
    
    ```
    echo "<VirtualHost *:80>
            ServerAdmin webmaster@localhost
            DocumentRoot /var/www/eden.wise.d08.com
            ServerName eden.wise.d08.com
            ServerAlias www.eden.wise.d08.com
            ErrorDocument 404 /error/404.html
            ErrorDocument 500 /error/404.html
            ErrorDocument 502 /error/404.html
            ErrorDocument 503 /error/404.html
            ErrorDocument 504 /error/404.html
            <Directory /var/www/eden.wise.d08.com/public>
                    Options +Indexes
            </Directory>
            ErrorLog \${APACHE_LOG_DIR}/error.log
            CustomLog \${APACHE_LOG_DIR}/access.log combined
            <Directory /var/www/wise.d08.com>
                    Options +FollowSymLinks -Multiviews
                    AllowOverride All
            </Directory>
    </VirtualHost>" > /etc/apache2/sites-available/eden.wise.d08.com.conf
    service apache2 restart
    ```

Setelah itu, jalankan perintah `lynx http://www.eden.wise.d08.com/lahkmn`.

> Script dibawah ini terdapat pada **root node SSS & Garden**, untuk menjalankannya bisa langsung dengan melakukan command `bash no12.sh`
- **SSS & Garden**
    
    ```
    lynx http://www.eden.wise.d08.com/lahkmn
    ``` 

### Test

# Soal 13
> Loid juga meminta Franky untuk dibuatkan konfigurasi virtual host. Virtual host ini bertujuan untuk dapat mengakses file asset **www.eden.wise.yyy.com/public/js** menjadi **www.eden.wise.yyy.com/js**

### Script

Lakukan konfigurasi pada `/eden.wise.d08.com`. Lalu, tambahkan konfigurasi Alias, `Alias \"/js\" \"/var/www/eden.wise.d08.com/public/js\"`.

> Script dibawah ini terdapat pada **root node Eden**, untuk menjalankannya bisa langsung dengan melakukan command `bash no13.sh`
- **Eden**
    
    ```
    echo "<VirtualHost *:80>
            ServerAdmin webmaster@localhost
            DocumentRoot /var/www/eden.wise.d08.com
            ServerName eden.wise.d08.com
            ServerAlias www.eden.wise.d08.com
            ErrorDocument 404 /error/404.html
            ErrorDocument 500 /error/404.html
            ErrorDocument 502 /error/404.html
            ErrorDocument 503 /error/404.html
            ErrorDocument 504 /error/404.html
            <Directory /var/www/eden.wise.d08.com/public>
                    Options +Indexes
            </Directory>
            Alias \"/js\" \"/var/www/eden.wise.d08.com/public/js\"
            ErrorLog \${APACHE_LOG_DIR}/error.log
            CustomLog \${APACHE_LOG_DIR}/access.log combined
            <Directory /var/www/wise.d08.com>
                    Options +FollowSymLinks -Multiviews
                    AllowOverride All
            </Directory>
    </VirtualHost>
    " > /etc/apache2/sites-available/eden.wise.d08.com.conf
    service apache2 restart
    ```

Restart kemudian jalankan perintah `lynx http://www.eden.wise.d08.com/js` di Client.

> Script dibawah ini terdapat pada **root node SSS & Garden**, untuk menjalankannya bisa langsung dengan melakukan command `bash no13.sh`
- **SSS & Garden**
    
    ```
    lynx http://www.eden.wise.d08.com/js
    ```

### Test

# Soal 14
> Loid meminta agar **www.strix.operation.wise.yyy.com** hanya bisa diakses dengan port 15000 dan port 15500 

### Script

Lakukan konfigurasi pada `/strix.operation.wise.d08.com`. Lalu, buat config baru general.mecha.e10.com-15000.conf, virtualHost baru yang berada di port 15000 dan 15500.

> Script dibawah ini terdapat pada **root node Eden**, untuk menjalankannya bisa langsung dengan melakukan command `bash no14.sh`
- **Eden**
    
    ```
    echo "<VirtualHost *:15000>
            ServerAdmin webmaster@localhost
            DocumentRoot /var/www/strix.operation.wise.d08.com
            ServerName strix.operation.wise.d08.com
            ServerAlias www.strix.operation.wise.d08.com
            ErrorLog \${APACHE_LOG_DIR}/error.log
            CustomLog \${APACHE_LOG_DIR}/access.log combined
    </VirtualHost>
    <VirtualHost *:15500>
            ServerAdmin webmaster@localhost
            DocumentRoot /var/www/strix.operation.wise.d08.com
            ServerName strix.operation.wise.d08.com
            ServerAlias www.strix.operation.wise.d08.com
            ErrorLog \${APACHE_LOG_DIR}/error.log
            CustomLog \${APACHE_LOG_DIR}/access.log combined
    </VirtualHost>" > /etc/apache2/sites-available/strix.operation.wise.d08.com.conf
    a2ensite strix.operation.wise.d08.com
    service apache2 restart
    mkdir /var/www/strix.operation.wise.d08.com
    cp -RT /var/www/strix.operation.wise/ /var/www/strix.operation.wise.d08.com/
    echo "# If you just change the port or add more ports here, you will likely also
    # have to change the VirtualHost statement in
    # /etc/apache2/sites-enabled/000-default.conf
    Listen 80
    Listen 15000
    Listen 15500
    <IfModule ssl_module>
            Listen 443
    </IfModule>
    <IfModule mod_gnutls.c>
            Listen 443
    </IfModule>" > /etc/apache2/ports.conf
    service apache2 restart
    ```

Setelah itu, jalankan perintah `lynx www.strix.operation.wise.d08.com:15000`.

> Script dibawah ini terdapat pada **root node SSS**, untuk menjalankannya bisa langsung dengan melakukan command `bash no14.sh`
- **SSS**
    
    ```
    lynx www.strix.operation.wise.d08.com:15000
    ``` 

Setelah itu, jalankan perintah `lynx www.strix.operation.wise.d08.com:15500`.

> Script dibawah ini terdapat pada **root node Garden**, untuk menjalankannya bisa langsung dengan melakukan command `bash no14.sh`
- **Garden**
    
    ```
    lynx www.strix.operation.wise.d08.com:15500
    ``` 

### Test

# Soal 15
> dengan autentikasi username Twilight dan password opStrix dan file di /var/www/strix.operation.wise.yyy 

### Script

Jalankan command `htpasswd -c -b /etc/apache2/.htpasswd Twilight opStrix`. Lalu, konfigurasi file `/strix.operation.wise.d08.com`.

> Script dibawah ini terdapat pada **root node Eden**, untuk menjalankannya bisa langsung dengan melakukan command `bash no15.sh`
- **Eden**
    
    ```
    htpasswd -c -b /etc/apache2/.htpasswd Twilight opStrix
    echo "<VirtualHost *:15000>
            ServerAdmin webmaster@localhost
            DocumentRoot /var/www/strix.operation.wise.d08.com
            ServerName strix.operation.wise.d08.com
            ServerAlias www.strix.operation.wise.d08.com
            <Directory \"/var/www/strix.operation.wise.d08.com\">
                    AuthType Basic
                    AuthName \"Restricted Content\"
                    AuthUserFile /etc/apache2/.htpasswd
                    Require valid-user
            </Directory>
            ErrorLog \${APACHE_LOG_DIR}/error.log
            CustomLog \${APACHE_LOG_DIR}/access.log combined
    </VirtualHost>
    <VirtualHost *:15500>
            ServerAdmin webmaster@localhost
            DocumentRoot /var/www/strix.operation.wise.d08.com
            ServerName strix.operation.wise.d08.com
            ServerAlias www.strix.operation.wise.d08.com
            <Directory \"/var/www/strix.operation.wise.d08.com\">
                    AuthType Basic
                    AuthName \"Restricted Content\"
                    AuthUserFile /etc/apache2/.htpasswd
                    Require valid-user
            </Directory>
            ErrorLog \${APACHE_LOG_DIR}/error.log
            CustomLog \${APACHE_LOG_DIR}/access.log combined
    </VirtualHost>" > /etc/apache2/sites-available/strix.operation.wise.d08.com.conf
    service apache2 restart
    ```

Setelah itu, jalankan perintah `lynx www.strix.operation.wise.d08.com:15500`.

> Script dibawah ini terdapat pada **root node SSS & Garden**, untuk menjalankannya bisa langsung dengan melakukan command `bash no15.sh`
- **SSS & Garden**
    
    ```
    lynx www.strix.operation.wise.d08.com:15500
    ``` 

### Test

# Soal 16
> dan setiap kali mengakses IP Eden akan dialihkan secara otomatis ke **www.wise.yyy.com**

### Script

Lalukan konfigurasi file `/000-default.conf`. Lalu, lakukan `service apache2 restart`.

> Script dibawah ini terdapat pada **root node Eden**, untuk menjalankannya bisa langsung dengan melakukan command `bash no16.sh`
- **Eden**
    
    ```
    echo "<VirtualHost *:80>
            ServerAdmin webmaster@localhost
            DocumentRoot /var/www/html
            RewriteEngine On
            RewriteCond %{HTTP_HOST} !^wise.d08.com$
            RewriteRule /.* http://wise.d08.com/ [R]
            ErrorLog \${APACHE_LOG_DIR}/error.log
            CustomLog \${APACHE_LOG_DIR}/access.log combined
    </VirtualHost>" > /etc/apache2/sites-available/000-default.conf
    service apache2 restart
    ```

Setelah itu, jalankan perintah `lynx 10.19.3.3`.

> Script dibawah ini terdapat pada **root node SSS & Garden**, untuk menjalankannya bisa langsung dengan melakukan command `bash no16.sh`
- **SSS & Garden**
    
    ```
    lynx 10.19.3.3
    ``` 

### Test

# Soal 17
> Karena website **www.eden.wise.yyy.com** semakin banyak pengunjung dan banyak modifikasi sehingga banyak gambar-gambar yang random, maka Loid ingin mengubah request gambar yang memiliki substring “eden” akan diarahkan menuju eden.png. Bantulah Agent Twilight dan Organisasi WISE menjaga perdamaian! 

### Script

Lakukan konfigurasi file `/eden.wise.d08.com/.htaccess`. Lalu, konfigurasi file `/eden.wise.d08.com` dan lakukan restart service apache2 dengan `service apache2 restart`.

> Script dibawah ini terdapat pada **root node Eden**, untuk menjalankannya bisa langsung dengan melakukan command `bash no17.sh`
- **Eden**
    
    ```
    echo "RewriteEngine On
    RewriteCond %{REQUEST_URI} ^/public/images/(.*)eden(.*)
    RewriteCond %{REQUEST_URI} !/public/images/eden.png
    RewriteRule eden http://eden.wise.d08.com/public/images/eden.png$1 [L,R=301]" > /var/www/eden.wise.d08.com/.htaccess
    echo "<VirtualHost *:80>
            ServerAdmin webmaster@localhost
            DocumentRoot /var/www/eden.wise.d08.com
            ServerName eden.wise.d08.com
            ServerAlias www.eden.wise.d08.com
            ErrorDocument 404 /error/404.html
            ErrorDocument 500 /error/404.html
            ErrorDocument 502 /error/404.html
            ErrorDocument 503 /error/404.html
            ErrorDocument 504 /error/404.html
            <Directory /var/www/eden.wise.d08.com/public>
                    Options +Indexes
            </Directory>
            Alias \"/js\" \"/var/www/eden.wise.d08.com/public/js\"
            <Directory /var/www/eden.wise.d08.com>
                    Options +FollowSymLinks -Multiviews
                    AllowOverride All
            </Directory>
            ErrorLog \${APACHE_LOG_DIR}/error.log
            CustomLog \${APACHE_LOG_DIR}/access.log combined
            <Directory /var/www/wise.d08.com>
                    Options +FollowSymLinks -Multiviews
                    AllowOverride All
            </Directory>
    </VirtualHost>" > /etc/apache2/sites-available/eden.wise.d08.com.conf
    a2enmod rewrite
    service apache2 restart
    ```

Setelah itu, jalankan perintah `lynx http://www.eden.wise.d08.com/public/images/not-eden.png`.

> Script dibawah ini terdapat pada **root node SSS & Garden**, untuk menjalankannya bisa langsung dengan melakukan command `bash no17.sh`
- **SSS & Garden**
    
    ```
    lynx http://www.eden.wise.d08.com/public/images/not-eden.png
    ``` 

### Test

![image](https://user-images.githubusercontent.com/73109893/198837905-1ee039d2-96b6-4f4c-ae8b-a23926dbb642.png)
