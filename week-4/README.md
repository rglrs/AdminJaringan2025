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

## Ekosistem Internet dan DNS Concept

![nsswitch.png](assets/nsswitch.png)

nsswitch

Pada Linux Debian dan sistem Linux lainnya, file `/etc/nsswitch.conf` digunakan untuk mengatur Name Service Switch (NSS). File ini menentukan metode yang digunakan sistem untuk mencari informasi terkait layanan nama, termasuk pencarian pengguna, grup, host, dan berbagai entitas lainnya.

![Screenshot 2025-03-17 094644.png](assets/Screenshot%202025-03-17%20094644.png)

### Penjelasan Beberapa Layanan

- **passwd, group, dan shadow**: Berfungsi untuk mendapatkan informasi mengenai pengguna dan grup dalam sistem. Jika menggunakan **files**, maka sistem akan mencari data di `/etc/passwd`, `/etc/group`, dan `/etc/shadow`.
- **hosts**: Berfungsi untuk mencari alamat IP berdasarkan nama host. Jika menggunakan **files**, sistem akan memeriksa `/etc/hosts` terlebih dahulu. Jika menggunakan **dns**, maka sistem akan mengandalkan layanan DNS jika tidak menemukan hasil di `/etc/hosts`.
- **networks, protocols, services, ethers, dan rpc**: Digunakan untuk mendapatkan informasi terkait jaringan, protokol, layanan, dan berbagai konfigurasi lainnya dalam sistem.

File `/etc/hosts` berfungsi untuk memetakan nama host ke alamat IP secara lokal, sehingga sistem dapat menemukan alamat IP tanpa bergantung pada layanan DNS (Domain Name System). Dengan demikian, sistem akan memeriksa entri di `/etc/hosts` terlebih dahulu sebelum mencoba mencari melalui layanan eksternal seperti DNS.

![nano-etc-hosts-ale.png](assets/nano-etc-hosts-ale.png)

Untuk mengonfigurasi alamat IP dalam file `/etc/hosts` agar komputer dapat mengenali nama host `ale`, ikuti langkah-langkah berikut:

### 1. Buka File `/etc/hosts`

Gunakan editor teks seperti `nano`  dengan hak akses root:

![less-nano-etc-host.png](assets/less-nano-etc-host.png)

### 2. Tambahkan Entri untuk `ale`

Tambahkan baris berikut, ganti `192.168.1.100` dengan alamat IP komputer yang ingin dikaitkan dengan nama `ale`:

```bash
192.168.1.100    ale
```

### 3. Uji Koneksi dengan `ping`

Setelah konfigurasi selesai, coba ping komputer dengan nama `ale` untuk memastikan konfigurasi berfungsi:

![ping-ale.png](assets/ping-ale.png)

### Cek IP

Gunakan command `ip a` 

![cek-ip.png](assets/cek-ip.png)

### **resolv**

[]()

Sedangkan isi dari file resolv.conf sendiri bisa dicek menggunakan command

```bash
sudo less /etc/resolv.conf
```

![nano-etc-resolv-conf.png](assets/nano-etc-resolv-conf.png)

**nameserver** menentukan alamat IP server DNS yang digunakan untuk pencarian domain, dapat berisi lebih dari satu alamat yang dicoba berurutan jika gagal. **search** menetapkan domain yang akan dicari saat hanya sebagian nama host diberikan.

**Test ping www**

![ping-www.png](assets/ping-www.png)

Konfigurasi di `/etc/resolv.conf` memengaruhi resolusi domain melalui dua direktif utama. **search pens.ac.id** memungkinkan sistem menambahkan domain `pens.ac.id` ke nama host yang tidak lengkap, sehingga perintah `ping www` akan otomatis mencoba `ping www.pens.ac.id`. Sementara itu, **nameserver 202.9.85.4** dan **nameserver 202.9.85.3** digunakan jika domain tidak ditemukan secara lokal, di mana sistem akan meminta server DNS tersebut untuk menerjemahkan nama domain ke alamat IP.

### **root.hints**

File `/usr/share/dns/root.hints` berisi daftar server DNS root yang membantu resolver DNS rekursif menemukan server authoritative untuk domain tertentu. File ini biasanya digunakan oleh server DNS lokal seperti BIND, Unbound, atau PowerDNS untuk memulai pencarian domain yang tidak tersedia dalam cache atau zona lokal.

![file-cek-root-serve.png](assets/file-cek-root-serve.png)

![isi-file-root-server.png](assets/isi-file-root-server.png)

## **Instalasi & Konfigurasi bind9**

### **Konfigurasi Jaringan Internal**

Install bind9

Command untuk install bind9, sebelum itu masuk ke root

```bash
root@dlp:~# apt -y install bind9 bind9utils
```

### **Konfigurasi dan Penyesuaian BIND**

Menambahkan `named.conf.internal-zones`, file konfigurasi baru, ke file utama konfigurasi BIND `/etc/bind/named.conf.`

![etc-bind-named.png](assets/etc-bind-named.png)

### Konfigurasi pada `/etc/bind/named.conf.options`

![etc-bind-named-conf-options.png](assets/etc-bind-named-conf-options.png)

Konfigurasi ACL **internal-network** untuk jaringan `192.168.80.0/24` menentukan siapa yang dapat mengakses layanan DNS, di mana hanya **localhost** dan jaringan internal yang diizinkan melakukan query (`allow-query`), sementara transfer zona hanya diperbolehkan untuk **localhost** (`allow-transfer`). Pencarian rekursif diaktifkan (`recursion yes`) untuk resolusi domain eksternal, validasi DNSSEC diatur otomatis (`dnssec-validation auto`), dan BIND dikonfigurasi agar menerima koneksi IPv6 (`listen-on-v6 { any; }`).

### **Konfigurasi Zona DNS di BIND**

![etc-bind-named-conf-internal-zones.png](assets/etc-bind-named-conf-internal-zones.png)

**1. Zona Forward (kelompok4.home)**

Zona ini digunakan untuk menerjemahkan nama domain ke alamat IP dan disimpan dalam file `/etc/bind/kelompok4.home.lan`. Bertindak sebagai **master (utama)**, sehingga server ini menjadi sumber resmi data DNS untuk domain tersebut. Selain itu, update dinamis tidak diizinkan dengan konfigurasi `allow-update { none; };`.

**2. Zona Reverse (80.168.192.in-addr.arpa)**

Zona ini berfungsi untuk menerjemahkan alamat IP ke nama domain (**reverse lookup**) dan disimpan dalam file `/etc/bind/80.168.192.db`. Seperti zona forward, zona ini juga bertindak sebagai **master**, dengan update dinamis yang dinonaktifkan.

### **Konfigurasi opsi BIND untuk menggunakan hanya IPv4 dan menonaktifkan IPv6.**

![etc-default-named.png](assets/etc-default-named.png)

Untuk mengonfigurasi BIND agar hanya menggunakan IPv4, edit file `/etc/default/named` dan tambahkan opsi `OPTIONS="-u bind -4"`. Opsi ini memastikan BIND berjalan sebagai pengguna `bind` dan hanya menggunakan IPv4, mengabaikan IPv6 untuk menghindari kemungkinan error pada jaringan yang tidak mendukung IPv6.

### **Konfigurasi Zone Files**

Konfigurasi **forward lookup** pada BIND DNS Server untuk jaringan **192.168.80.0/24** dengan domain **kelompok4.home** memungkinkan server menerjemahkan nama domain ke alamat IP dengan menetapkan file zona sebagai **master** dan mendefinisikan pemetaan nama host.

![etc-bind-kelompok4-home-lan.png](assets/etc-bind-kelompok4-home-lan.png)

Konfigurasi **reverse lookup** pada BIND DNS Server untuk jaringan **192.168.80.0/24** dengan domain **kelompok4.home** dilakukan dengan membuat file zona `/etc/bind/80.168.192.db`, mendaftarkannya sebagai **master** di `/etc/bind/named.conf.local`, lalu memverifikasi dan merestart BIND agar perubahan diterapkan.

![etc-bind-80-168-192-db.png](assets/etc-bind-80-168-192-db.png)

### **BIND: Verify Resolution**

Restart BIND untuk menerapkan perubahan dengan command 

```bash
root@dlp:~# systemctl restart named
```

### **Konfigurasi DNS Client untuk menggunakan DNS Server sendiri**

![etc-resolve-conf.png](assets/etc-resolve-conf.png)

Sistem Linux menggunakan file /etc/resolv.conf untuk memilih DNS server mana yang akan digunakan untuk melakukan query DNS, misalnya menyelesaikan domain ke IP atau sebaliknya.

Dengan mengedit **`/etc/resolv.conf`** dan mengubah **nameserver** menjadi **192.168.80.193**, berarti:

- Mengatur sistem supaya pakai **DNS Server sendiri** (BIND di **192.168.80.193**)
- Prioritaskan pencarian DNS ke **server lokal dulu**, sebelum ke DNS eksternal
- Bikin sistem bisa resolve **domain lokal** yang cuma dikenali oleh DNS internal

### **DNS Query menggunakan DiG (Domain Information Groper) untuk Forward Lookup**

![dig-kelompok4-home.png](assets/dig-kelompok4-home.png)

Perintah di atas digunakan untuk menggunakan DNS Server yang telah dikonfigurasi untuk melihat resolusi nama domain ke alamat IP.

### **Reverse DNS Lookup**

![dig-ip-server.png](assets/dig-ip-server.png)

Nama domain yang terkait dengan alamat IP tertentu dapat ditemukan dengan menggunakan perintah di atas untuk melakukan pencarian balik.

### Referensi
[Configure for Internal Network](https://www.server-world.info/en/note?os=Debian_12&p=dns&f=1)

[Configure Zone Files](https://www.server-world.info/en/note?os=Debian_12&p=dns&f=3)

[Verify Resolution](https://www.server-world.info/en/note?os=Debian_12&p=dns&f=4)
