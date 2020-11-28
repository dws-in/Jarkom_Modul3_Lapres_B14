# **Jarkom_Modul3_Lapres_B14**
### Anggota Kelompok:
- IQBAAL PRATAMA PUTRA  (05111840000021)
- DWI WAHYU SANTOSO     (05111840000121)

<img src="images/topologi.PNG" width="500">

## Topologi:
- SURABAYA    : Router
- Subnet1     : 
  - Switch1
  - GRESIK    : Client
  - SIDOARJO  : Client
- Subnet2     :
  - Switch2
  - TUBAN     : DHCP Server
  - MALANG    : DNS Server
  - MOJOKERTO : Proxy Server
- Subnet3     :
  - Switch3
  - BANYUWANGI: Client
  - MADIUN    : Client

## Soal:
1. Seluruh client TIDAK DIPERBOLEHKAN menggunakan konfigurasi IP Statis. <br>
2. SURABAYA ditunjuk sebagai perantara (DHCP Relay) antara DHCP Server dan client. <br>
3. Client pada subnet 1 mendapatkan range IP dari 192.168.0.10 sampai 192.168.0.100 dan 192.168.0.110 sampai 192.168.0.200. <br>
4. Client pada subnet 3 mendapatkan range IP dari 192.168.1.50 sampai 192.168.1.70. <br>
5. Client mendapatkan DNS Malang dan DNS 202.46.129.2 dari DHCP. <br>
6. Client di subnet 1 mendapatkan peminjaman alamat IP selama 5 menit, sedangkan client pada subnet 3 mendapatkan peminjaman IP selama 10 menit. <br>
7. User autentikasi memiliki format: <br>
   - User : userta_b14 <br>
   - Password : inipassw0rdta_b14 <br>
8. Penggunaan internet setiap hari Selasa-Rabu pukul 13.00-18.00. <br>
9. Jadwal bimbingan setiap hari Selasa-Kamis pukul 21.00 - 09.00 keesokan harinya (sampai Jumat jam 09.00). <br>
10. Setiap dia mengakses google.com, maka akan di redirect menuju monta.if.its.ac.id. <br>
11. Mengubah error page default squid menjadi seperti berikut: <br>
<img src="images/error-page.PNG" width="500"> <br>
12. Menggunakan proxy cukup dengan mengetikkan domain janganlupa-ta.b14.pw dan memasukkan port 8080. <br>

## Langkah-langkah pengerjaan:

**1. Konfigurasi IP client.** <br>
- Edit file `topologi.sh` sebagai berikut: <br>
![alt text](/images/1.1.png) <br>
- Edit file `/etc/network/interfaces` pada SURABAYA sebagai DHCP Relay dengan konfigurasi seperti berikut: <br>
![alt text](/images/1.2.png) <br>
- Edit file `/etc/network/interfaces` pada BANYUWANGI sebagai Client dengan konfigurasi seperti berikut: <br>
![alt text](/images/1.3.png) <br>
- Edit file `/etc/network/interfaces` pada MADIUN sebagai Client dengan konfigurasi sebagai berikut: <br>
![alt text](/images/1.4.png) <br>
- Edit file `/etc/network/interfaces` pada GRESIK sebagai Client dengan konfigurasi sebagai berikut: <br>
![alt text](/images/1.5.png) <br>
- Edit file `/etc/network/interfaces` pada SIDOARJO sebagai Client dengan konfigurasi sebagai berikut: <br>
![alt text](/images/1.6.png) <br>
- Edit file `/etc/network/interfaces` pada MALANG sebagai DNS Server dengan konfigurasi sebagai berikut: <br>
![alt text](/images/1.7.png) <br>
- Edit file `/etc/network/interfaces` pada MOJOKERTO sebagai Proxy Server dengan konfigurasi sebagai berikut: <br>
![alt text](/images/1.8.png) <br>
- Edit file `/etc/network/interfaces` pada TUBAN sebagai DHCP Server dengan konfigurasi sebagai berikut: <br>
![alt text](/images/1.9.PNG) <br>

**2. Surabaya sebagai DHCP Relay.** <br>
- Edit file `/etc/sysctl.conf` pada SURABAYA dengan merubah `ip_forward` menjadi 1. <br>
![alt text](/images/2.1.PNG) <br>
- Install DHCP Relay dengan menjalankan perintah `apt-get install isc-dhcp-relay`. <br>
![alt text](/images/2.2.png) <br>
- Edit file `/etc/default/isc-dhcp-relay` dengan memasukkan IP TUBAN dan interfaces yang digunakan. <br>
![alt text](/images/2.3.PNG) <br>
- Restart DHCP Relay dengan menjalankan perintah `service isc-dhcp-relay restart`. <br>
![alt text](/images/2.4.png) <br>
- Install DHCP Server pada TUBAN dengan menjalankan perintah `apt-get install isc-dhcp-server`. <br>
![alt text](/images/2.5.png) <br>
- Edit file `/etc/default/isc-dhcp-server` dengan memasukkan `eth0`. <br>
![alt text](/images/2.6.png) <br>
- Restart DHCP Server dengan menjalankan perintah `service isc-dhcp-server restart`. <br>
![alt text](/images/2.7.png) <br>

**3. Subnet1 range IP 192.168.0.10 sampai 192.168.0.100 dan 192.168.0.110 sampai 192.168.0.200.** <br>
- Edit file `/etc/dhcp/dhcpd.conf` pada TUBAN dengan memasukkan subnet 1 range yang sudah ditentukan. <br>
![alt text](/images/3.1.png) <br>
- Test pada GRESIK apakah telah mendapatkan IP. <br>
![alt text](/images/3.2.png) <br>
- Test pada SIDOARJO apakah telah mendapatkan IP. <br>
![alt text](/images/3.3.png) <br>

**4. Subnet3 range IP 192.168.1.50 sampai 192.168.1.70.** <br>
- Edit file `/etc/dhcp/dhcpd.conf` pada TUBAN dengan memasukkan subnet 3 range yang sudah ditentukan. <br>
![alt text](/images/4.1.png) <br>
- Test pada BANYUWANGI apakah telah mendapatkan IP. <br>
![alt text](/images/4.2.png) <br>
- Test pada MADIUN apakah telah mendapatkan IP. <br>
![alt text](/images/4.3.png) <br>

**5. Cek setiap Client apakah telah mendapatkan DNS Malang dan DNS 202.46.129.2 dari DHCP.** <br>
- Buka `/etc/resolv.conf` pada GRESIK. <br>
![alt text](/images/5.1.png) <br>
- Buka `/etc/resolv.conf` pada SIDOARJO. <br>
![alt text](/images/5.2.png) <br>
- Buka `/etc/resolv.conf` pada BANYUWANGI. <br>
![alt text](/images/5.3.png) <br>
- Buka `/etc/resolv.conf` pada MADIUN. <br>
![alt text](/images/5.4.png) <br>

**6. Subnet 1 diberi waktu 5x60 sec sedangkan subnet 3diberi waktu 10x60 sec.** <br>
- Edit file `/etc/dhcp/dhcpd.conf` pada TUBAN dengan memasukkan default dan max lease time. <br>
![alt text](/images/6.1.png) <br>

**7. Membuat user autentikasi.** <br>
- Jalankan `htpasswd /etc/squid3/passwd userta_b14` dan masukkan password `inipassw0rdta_b14`. <br>
![alt text](/images/7.1.png) <br>
- Hasilnya bisa diakses melalui browser Mozilla sebagai berikut. <br>
![alt text](/images/7.2.png) <br>



