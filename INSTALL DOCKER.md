Setelah ubuntu server diupdate dan diupgrade, langkah selanjutnya install docker

Langkah - langkah install docker
1. Hapus semua versi docker lama atau paket lainnya yang mungkin sudah terpasang di sistem ubuntu. Ketik perintah:

    📝for pkg in docker.io docker-doc docker-compose docker-compose-v2 podman-docker containerd runc;
        do sudo apt-get remove $pkg; done > enter
2. Unduh skrip instalasi resmi Docker dari internet dan menyimpannya ke dalam file di komputer. Ketik perintah:

   📝curl -fsSL https://get.docker.com -o get-docker.sh > enter
3. Memastikan status file skrip installer Docker yang baru saja diunduh telah tersedia di server ubuntu. Ketik perintah:

   📝ls -l > enter

   jika installasi berhasil maka akan muncul seperti ini

   📄 -rw-r--r-- 1 root root 22446 Jun 19 06:22 get-docker.sh
4. 

   


   
