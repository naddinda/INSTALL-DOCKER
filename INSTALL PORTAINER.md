Install docker telah berhasil dan selesai. Langkah selanjutnya adalah install portainer.

Langkah - langkah install portainer:
1. Untuk membuat tempat penyimpanan data permanen (hard disk virtual) khusus untuk Portainer. Jalankan perintah:
   
   📝docker volume create portainer_data > enter

    Tujuannya agar semua data penting di Portainer seperti username, password, dan pengaturan kontainer tidak hilang atau terhapus secara otomatis saat Portainer dimatikan, diperbarui, atau direstart.
2. Untuk mengunduh sekaligus menjalankan Portainer (aplikasi web untuk mengelola Docker). jalankan perintah:

   📝docker rund -p 8000:8000 p 9443:9443-name portainer - restart=a lways -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer-ce:latest > enter
3. cek dan pastikan apakah kontainer Portainer sudah benar-benar aktif dengan statusnya Up. Jalankan perintah:

   📝docker ps > enter

4. Jika statusnya dauh Up, kemudian buka chrome lalu ketik ip address ubuntu server (contoh https://192.168.115.2:9443) > enter. Akan muncul halaman buat username dan password lalu klik creat user.
5. Setelah itu muncul dashbord portainer yang siap digunakan.
