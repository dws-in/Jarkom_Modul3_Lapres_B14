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
7. User autentikasi milik Anri memiliki format:
<br>
     User : userta_b14
     Password : inipassw0rdta_b14
<br>


## Langkah-langkah pengerjaan:
**1. Membuat domain `http://semerub14.pw` dengan DNS MALANG dan mengarah ke IP Server PROBOLINGGO.** <br>
