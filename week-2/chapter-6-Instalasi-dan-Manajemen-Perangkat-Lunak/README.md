<div align="center">
  <h1 class="text-align: center;font-weight: bold">Praktikum <br>Workshop Administrasi Jaringan</h1>
  <h3 class="text-align: center;">Dosen Pengampu : Dr. Ferry Astika Saputra, S.T., M.Sc.</h3>
</div>
<br />
<div align="center">
  <img src="https://upload.wikimedia.org/wikipedia/id/4/44/Logo_PENS.png" alt="Logo PENS">
  <h3 style="text-align: center;">Disusun Oleh : </h3>
  <p style="text-align: center;">
    <strong>Ragil Ridho Saputra (3123500016)</strong><br>
  </p>

<h3 style="text-align: center;line-height: 1.5">Politeknik Elektronika Negeri Surabaya<br>Departemen Teknik Informatika Dan Komputer<br>Program Studi Teknik Informatika<br>2025/2026</h3>
  <hr><hr>
</div>

# **Chapter 6 Instalasi dan Manajemen Perangkat Lunak**

### Instalasi Sistem Operasi

Distribusi Linux dan FreeBSD memiliki prosedur instalasi dasar yang cukup sederhana.

- **Instalasi Fisik vs. Virtual:**
    
    Pada perangkat fisik, proses boot dapat dilakukan melalui CD, DVD, atau USB drive. Sementara itu, pada mesin virtual, proses booting dilakukan menggunakan file ISO. Instalasi sistem operasi dari media lokal cukup mudah berkat antarmuka GUI yang membimbing pengguna selama proses berlangsung.
    
- **Instalasi Melalui Jaringan:**
    
    Jika perlu menginstal sistem operasi pada banyak komputer, penggunaan media lokal seperti CD/DVD/USB kurang efisien karena memakan waktu, rentan kesalahan, dan repetitif. Solusi yang lebih praktis adalah melakukan instalasi melalui jaringan.
    
    Metode umum yang digunakan adalah kombinasi protokol seperti DHCP dan TFTP tanpa memerlukan media fisik, di mana sistem akan mengunduh file instalasi OS dari server jaringan melalui HTTP, FTP, atau NFS. File instalasi tersebut dapat berada di server yang sama atau terpisah.
    
    PXE (Preboot eXecution Environment) merupakan metode yang memungkinkan instalasi OS berlangsung secara otomatis. Standar yang dikembangkan oleh Intel ini memungkinkan sistem untuk boot melalui jaringan tanpa memerlukan driver khusus untuk setiap kartu jaringan.
    

### Sistem Manajemen Paket Linux

- **Format Paket:**
    
    Linux menggunakan berbagai format paket, dengan dua yang paling umum adalah:
    
    - **RPM:** Digunakan oleh distribusi seperti Red Hat, CentOS, SUSE, dan Amazon Linux.
    - **.deb:** Digunakan oleh sistem berbasis Debian seperti Ubuntu.
    
    Kedua format ini memiliki fungsi yang hampir serupa.
    
- **Alat Manajemen Paket Dasar:**
    
    Setiap sistem memiliki alat bawaan untuk mengelola paket:
    
    - **rpm** untuk paket RPM.
    - **dpkg** untuk paket .deb.

### Manajemen Paket Tingkat Tinggi

Alat manajemen paket tingkat tinggi memungkinkan instalasi, penghapusan, dan pembaruan paket dengan lebih mudah. Selain itu, alat ini juga memungkinkan pencarian paket serta melihat daftar paket yang sudah terinstal.

- **Repositori Paket:**
    
    Konfigurasi default sistem manajemen paket umumnya terhubung ke satu atau beberapa server yang dikelola oleh distributor.
    
    - *Release* merupakan snapshot konsisten dari semua paket.
    - *Component* adalah subset perangkat lunak dalam sebuah release.
    - *Architecture* mengacu pada jenis perangkat keras yang kompatibel dengan binary paket, seperti i386 untuk Fedora 20.
- **yum (Yellowdog Updater, Modified):**
    
    Manajer paket berbasis RPM ini menangani resolusi dependensi saat menginstal, memperbarui, dan menghapus paket. yum dapat mengelola paket dari repositori yang sudah terdaftar serta menjalankan operasi baris perintah untuk paket tertentu.
    
- **APT (Advanced Package Tool):**
    
    APT adalah kumpulan alat yang menyediakan sistem manajemen paket lengkap untuk sistem berbasis Debian (.deb). Beberapa alat dalam APT meliputi:
    
    - **apt-get:** Mengelola instalasi, penghapusan, dan pembaruan paket.
    - **apt-cache:** Mencari dan menampilkan informasi dari cache paket APT.
    - **apt-file:** Mencari file di dalam paket.
    - **apt-show-versions:** Menampilkan versi paket yang terinstal.
    - **aptitude:** Antarmuka tingkat tinggi untuk manajemen paket, dengan fungsionalitas tambahan dibandingkan apt-get.
    - **apt-mirror:** Menyediakan fitur pencerminan repositori paket.
    
    APT merupakan sistem yang paling banyak digunakan pada distribusi berbasis Debian dan dapat menangani paket .deb maupun RPM.
    

### Lokalisasi dan Konfigurasi Perangkat Lunak

Menyesuaikan sistem agar sesuai dengan lingkungan kerja lokal atau berbasis cloud adalah bagian penting dari administrasi sistem. Pendekatan yang terstruktur dan dapat direproduksi sangat penting untuk menghindari sistem unik yang sulit dipulihkan jika terjadi masalah besar.

Keseluruhan pembahasan ini bertujuan untuk memberikan pemahaman praktis tentang cara menginstal sistem operasi serta mengelola paket perangkat lunak secara efisien, terutama dalam lingkungan yang membutuhkan otomatisasi dan skalabilitas.
