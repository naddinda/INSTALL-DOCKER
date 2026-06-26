Jiks install portainer telah berhasil, langkah berikutnya adalah install genieacs

Langkah - langkah install genieacs:
1. Pastikan Docker & Docker Compose sudah terinstal. Jalankan perintah:

   📝docker --version > enter (akan muncul versi docker yang sudah terinstall)

   📝docker compose version (akan muncul versi docker compose)
2. Buat folder project GenieACS. Jalankan perintah:

   📝mkdir genieacs-docker > enter
   
   📝cd genieacs-docker > enter
3. Buat File docker-compose.yml. Jalankan perintah:

   📝nano docker-compose.yml > enter (muncul terminal GNU)
4. Ketik teks di bawah ini di terminal GNU

   services:
   
  mongo:
  
    image: mongo:4.4
    
    container_name: genieacs-mongodb
    
    restart: always
    
    volumes:
    
      - mongo_data:/data/db

  redis:
  
    image: redis:7.0-alpine
    
    container_name: genieacs-redis
    
    restart: always
    
    volumes:
    
      - redis_data:/data

  genieacs-cwmp:
  
    build: .
    
    container_name: genieacs-cwmp
    
    restart: always
    
    environment:
    
      - GENIEACS_MONGODB_CONNECTION_URL=mongodb://mongo:27017/genieacs
      
      - GENIEACS_REDIS_CONNECTION_URL=redis://redis:6379/0
      
    ports:
    
      - "7547:7547"
      
    depends_on:
    
      - mongo
      
      - redis
      
    command: genieacs-cwmp

  genieacs-nbi:
  
    build: .
    
    container_name: genieacs-nbi
    
    restart: always
    
    environment:
    
      - GENIEACS_MONGODB_CONNECTION_URL=mongodb://mongo:27017/genieacs
      
      - GENIEACS_REDIS_CONNECTION_URL=redis://redis:6379/0
      
    ports:
    
      - "7557:7557"
      
    depends_on:
    
      - mongo
      
      - redis
      
    command: genieacs-nbi

  genieacs-fs:
  
    build: .
    
    container_name: genieacs-fs
    
    restart: always
    
    environment:
    
      - GENIEACS_MONGODB_CONNECTION_URL=mongodb://mongo:27017/genieacs
      
      - GENIEACS_REDIS_CONNECTION_URL=redis://redis:6379/0
      
    ports:
    
      - "7567:7567"
      
    depends_on:
    
      - mongo
      
      - redis
      
    command: genieacs-fs

  genieacs-ui:
  
    build: .
    
    container_name: genieacs-ui
    
    restart: always
    
    environment:
    
      - GENIEACS_MONGODB_CONNECTION_URL=mongodb://mongo:27017/genieacs
      
      - GENIEACS_REDIS_CONNECTION_URL=redis://redis:6379/0
      
      - GENIEACS_UI_JWT_SECRET=rahasiasangat-aman-123
      
      - GENIEACS_UI_USERS=${GENIEACS_UI_USERS}
      
    ports:
    
      - "3000:3000"
      
    depends_on:
    
      - mongo
      
      - redis
      
    command: genieacs-ui

volumes:

  mongo_data:
  
  redis_data:
  
5. Jalankan seluruh layanan (service) GenieACS di latar belakang (background) menggunakan Docker. Jalankan perintah:

   📝sudo docker compose up -d > enter (jika tidak ada error lanjut ke langkah berikutnya)
6. Cek status kontainer yang sedang berjalan.

   📝sudo docker ps > enter
7. Buka browser > ketik http://IP_Server_Ubuntu:3000 (contoh http://192.168.115.2:3000) > enter
8. Jika berhasil masuk ke halaman GenieACS, klik ABRACADABRA
9. Masukkan username dan password yang otomatis diberi oleh GenieACS

   📝Username: admin
   📝Password: admin
10. Setelah memasukkan username dan password muncul dashbord GenieACS. Maka sudah berhasil install GenieACS on Docker
