## Anggota Kelompok

- Mohammad Fadhil Rasyidin Parinduri // 5025201131
- Marcelino Salim // 5025201026
- Aisyah Nurhalimah // 5025201081 

### Soal Shift

- [link](https://docs.google.com/document/d/11Mz2Fd3DKtGkCknHee9VZRdJYvZ3YAMIaifObHEpBFo/edit?usp=sharing)

Kendala:

1. banyak tugas sedikit waktu (butuh introspeksi diri untuk memperbaiki manajemen waktu)
2. hehe semangat ^-^

# Laporan Resmi
## Daftar Isi
* [Soal 1](#soal-1)
* [Soal 2](#soal-2)
* [Soal 3](#soal-3)
* [Soal 4](#soal-4)
* [Soal 5](#soal-5)
* [Soal 6](#soal-6)
* [Soal 7](#soal-7)
* [Soal 8](#soal-8)
* [Soal 9](#soal-9)
* [Soal 10](#soal-10)
* [Soal 11](#soal-11)
* [Soal 12](#soal-12)
* [Soal 13](#soal-13)
* [Soal 14](#soal-14)
* [Soal 15](#soal-15)
* [Soal 16](#soal-16)
* [Soal 17](#soal-17)


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
    	address 192.178.3.2
    	netmask 255.255.255.0
    	gateway 192.178.3.1
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

Setelah berhasil melakukan konfigurasi dan selesai menjalankan start command, akan dilakukan pengecekan internet untuk semua node dengan melakukan `ping google.com`

![p2_2](https://user-images.githubusercontent.com/81240334/198823214-53bc659c-d7c6-4f4d-a3b7-2d9d75237149.jpeg)
![p2_1](https://user-images.githubusercontent.com/81240334/198823215-e2694b34-e29c-4d02-b970-e7653562fe8d.jpeg)
![Wise ping](https://user-images.githubusercontent.com/81240334/198823210-45e41db3-19d2-41ef-a44b-5a632b809a14.jpg)

# Soal 2
> Untuk mempermudah mendapatkan informasi mengenai misi dari Handler, buat website utama dengan akses **wise.yyy.com** dengan alias **www.wise.yyy.com** pada folder wise 

# Soal 3
> Setelah itu ia juga ingin membuat subdomain **eden.wise.yyy.com** dengan alias **www.eden.wise.yyy.com** yang diatur DNS-nya di WISE dan mengarah ke Eden 

# Soal 4
> Buat juga reverse domain untuk domain utama 

# Soal 5
> Agar dapat tetap dihubungi jika server WISE bermasalah, buatlah juga Berlint sebagai DNS Slave untuk domain utama

# Soal 6
> Karena banyak informasi dari Handler, buat subdomain yang khusus untuk operation yaitu **operation.wise.yyy.com** dengan alias **www.operation.wise.yyy.com** yang didelegasikan dari WISE ke Berlint dengan IP menuju ke Eden dalam folder operation 

# Soal 7
> Untuk informasi yang lebih spesifik mengenai Operation Strix, buatlah subdomain melalui Berlint dengan akses **strix.operation.wise.yyy.com** dengan alias **www.strix.operation.wise.yyy.com** yang mengarah ke Eden
