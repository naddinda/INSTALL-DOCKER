Jika setting modem telah berhasil, selanjutnya koneksikan genieACS ke modem untuk melakukan manajemen perangkat jarak jauh secara terpusat.

1. Buka web genieACS di browser. Ketik IP server (contoh: http://192.168.115.2:3000) > enter

2. Agar modem dan genieACS dapat terhubung, masukkan connection request password dan username yang akan digunakan saat menyeting modem.
   
4. Buka tab admin > config > new config > isi key: cwmp.connectionRequestAuth > isi value: AUTH("isi request username", "isi request password") > klik save.

5. Selanjutnya, koneksikan modem ke GenieACS

6. Pastikan perangkat yang digunakan terhubung ke modem yanng telah disetting.
   
7. Buka aplikasi Winbox, pada halaman login winbox masukkan IP yang terhubung ke port ONT (contoh: 103.134.220.123:12500) > connect

8. Pilih menu PPP > Active Connections > ketik "acs-pkl" pada kolom pencarian > klik 2 kali pada "acs-pkl"> copy paste IP Addnya di browser > enter

9. Setelah masuk ke halaman login setting modem masukkan username dan passwordnya > login

10. Pilih menu administration > pilih TR069 > pada kolom ACS URL copy paste IP Address di browser GenieACS (contoh: 192.168.115.2:3000) port 3000 diganti dengan 7547 jadi (contoh: 192.168.115.2:7547) pastikan enable

11. Pada kolom username menjadi acs dan password menjadi acs5758

12. Pada kolom connection request username menjadi admin, connection request password menjadi admin (sesuaikan pada settingan di genieACS)

13. Buka kembali GenieACS, pastikan GenieACS sudah terhubung dengan modem yang telah disetting.

14. Ketika sudah muncul modem yang terkoneksi dengan GenieACS klik summon untuk memaksa modem langsung menarik pembaruan konfigurasi terbaru dan memperbarui data parameter perangkat tanpa harus menunggu jadwal periodik

15. Pastikan setelah diklik summon hasilnya "summoned", itu tandanya modem dan GenieACS sudah berhasil terhubung tanpa error.
