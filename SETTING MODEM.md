Setelah semua berhasil terinstall, kemudian setting modem.

Lagkah - langkah mengoneksikan modem ke server:

1. Siapkan alat dan bahan:

    a. Modem

    b. Kabel fiber optic single mode

    c. Adaptor modem

    d. Splitter

    e. Stop kontak

    f. Kabel Fiber Optic yang terhubung ke koneksi internet

    g. Handphone atau Laptop

    h. Kabel LAN (opsional)
2. Hidupkan modem:
   
   a. Pastikan stop kontak sudah menyala

   b. Hubungkan adaptor ke stop kontak lalu hubungkan ke port modem, tekan tombol on pada modem untuk menyalakannya

   c. Hubungkan splitter dan kabel fiber optic yang terkoneksi ke internet

   d. Hubungkan ujung 1 kabel fiber optic single mode ke port splitter, kemudian ujung ke 2 kabel fiber optic single mode ke port belakang modem

   e. Modem sudah bisa disetting
      
3. Setting modem melalui Handphone atau Laptop (saya tidak menggunakan kabel LAN dan saya menggunakan Handphone)
   
   a. Karena saya tidak menggunakan kabel LAN maka Handphone harus terkoneksi dengan wifi pada modem yang sudah dinyalakan

   b. Buka browser > ketik ip yang tertera di belakang modem (contoh 192.168.1.1) > enter

   c. Masukkan username dan password > klik login

   d. Pada halaman dashbord klik menu Network > WAN > pada halaman WAN setting:

       Enable VLAN ✅
   
       VLAN ID     514

       Service List: TR069_VOIP_INTERNET

       Username: acs-pkl
   
       Password: acs-pkl

       Port Binding ✅LAN1  ✅LAN2  ✅LAN3  ✅LAN4
   
                     ✅SSID1

       Jika sudah selesai disetting klik create
   e. Masih di menu Network > WLAN > setting pada Authentication Type: Open System > submit
   
   f. Kembali ke dashbord, pilih menu status > interface network

       📄pastikan Ip address dan DNS sudah ada IP dan Connected.
   g. Buka aplikasi speedtest > mulai > akan muncul Mbps nya. Setting modem telah berhasil


