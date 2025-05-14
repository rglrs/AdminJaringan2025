<div align="center">
  <h1 style="text-align: center;font-weight: bold">Laporan Praktikum
  <br>Workshop Administrasi Jaringan</h1>
  <h4 style="text-align: center;">Dosen Pengampu : Dr. Ferry Astika Saputra, S.T., M.Sc.</h4>
</div>
<br />
<div align="center">
  <img src="https://upload.wikimedia.org/wikipedia/id/4/44/Logo_PENS.png" alt="Logo PENS">
  <h3 style="text-align: center;">Disusun Oleh : </h3>
  <p style="text-align: center;">
    <strong>Nama: Ragil Ridho Saputra</strong><br>
    <strong>NRP: 3123500016 </strong><br>
    <strong>Kelas: D3 IT A</strong>
  </p>
<h3 style="text-align: center;line-height: 1.5">Politeknik Elektronika Negeri Surabaya<br>Departemen Teknik Informatika Dan Komputer<br>Program Studi Teknik Informatika<br>2023/2024</h3>
  <hr><hr>
</div>

# Rangkuman Electronic Mail 
https://www.geeksforgeeks.org/introduction-to-electronic-mail/ 
## Rangkuman

Surel, atau surat elektronik, adalah metode utama untuk bertukar pesan melalui internet. Layanan ini memungkinkan pengguna internet mengirim pesan dalam bentuk surat (mail) dengan format tertentu, termasuk teks, gambar, audio, dan video, kepada pengguna lain di seluruh dunia. Sistem surel melibatkan komponen penting seperti Agen Pengguna (UA), Agen Transfer Pesan (MTA), Kotak Surat (Mailbox), dan Spool file, yang semuanya bekerja sama untuk memfasilitasi pengiriman dan penerimaan pesan. Meskipun surel menawarkan keuntungan signifikan seperti kecepatan, efektivitas biaya, dan kemampuan untuk mengirim lampiran, surel juga memiliki kelemahan, termasuk risiko spam, serangan _phishing_, kelebihan informasi, dan potensi miskomunikasi.

## Poin-Poin Utama

- Basics of email:
	- Alamat email: Ini adalah pengidentifikasi unik untuk setiap pengguna, biasanya dalam format name@domain.com.
	- Klien email: Ini adalah program perangkat lunak yang digunakan untuk mengirim, menerima, dan mengelola email, seperti Gmail, Outlook, atau Apple Mail.
	- Server email: Ini adalah sistem komputer yang bertanggung jawab untuk menyimpan dan meneruskan email ke penerima yang dituju.
- Surel (email) adalah metode pertukaran pesan melalui internet yang memungkinkan pengiriman berbagai jenis data.
- Surel (email) memiliki pengirim dan penerima, mirip dengan layanan pos tradisional.
- Komponen dasar sistem surel meliputi Agen Pengguna (UA) untuk mengirim dan menerima, Agen Transfer Pesan (MTA) untuk mentransfer, Mail Box untuk menyimpan pesan, dan Spool file untuk mengelola pesan keluar. Berikut adalah rangkuman poin-poin penting mengenai komponen dalam sistem email:
	- **User Agent (UA):** Aplikasi yang digunakan pengguna untuk membuat, mengirim, menerima, membalas email, serta mengelola kotak surat (mailbox). Sering disebut "mail reader".
	- **Message Transfer Agent (MTA):** Bertanggung jawab mentransfer email antar sistem. Membutuhkan MTA klien dan server. Menggunakan **Simple Mail Transfer Protocol (SMTP)** untuk pengiriman antar MTA.
		![email](images/email.png)
	- **Mailbox:** File di hard drive lokal tempat email yang diterima disimpan. Hanya pemilik mailbox yang dapat mengaksesnya. Pemilik bisa membacanya atau menghapusnya sesuai keinginannya.
	- **Spool file:** File yang berisi email yang akan dikirim. UA menambahkan email keluar ke file ini, dan MTA mengambilnya untuk dikirim.
	- **Mailing list (Alias):** Satu nama yang mewakili beberapa alamat email. Ketika email dikirim ke alias, sistem akan membuat dan mengirim email terpisah untuk setiap alamat dalam daftar. Jika alias tidak terdaftar, email dikirim ke alamat tersebut.
- Proses pengiriman surel melibatkan penulisan pesan, memasukkan alamat penerima, subjek, isi, lampirkan file yang diperlukan jika ada dan mengirimkannya melalui peladen surel.
- Surel (email) dapat menggunakan fitur CC (carbon copy) dan BCC (blind carbon copy) untuk mengirim salinan pesan kepada beberapa penerima, serta opsi reply, reply all, dan forward email untuk mengelola percakapan.
- Surel (email) menyediakan layanan seperti komposisi (menulis pesan dan jawaban), transfer (mengirim), pelaporan (konfirmasi pengiriman), menampilkan (menyajikan pesan), dan disposisi (tindakan penerima terhadap pesan).
	- **Komposisi** : Proses untuk membuat pesan dan jawaban.
	- **Transfer** : prosedur pengiriman mail dari pengirim ke penerima.
	- **Pelaporan (Reporting)** : Konfirmasi untuk pengiriman surat, membantu pengguna memeriksa apakah email mereka sudah terkirim, hilang atau ditolak.
	- **Disposisi (Disposition)** : Hal ini berhubungan dengan apa yang akan dilakukan oleh penerima setelah menerima email, yaitu menyimpan email, menghapus sebelum atau sesudah membaca.
- Daftar surel, atau alias, memungkinkan satu nama mewakili beberapa alamat surel, memfasilitasi pengiriman pesan ke banyak penerima sekaligus.
- Keuntungan surel meliputi komunikasi yang cepat dan nyaman, kemampuan penyimpanan dan pencarian pesan yang mudah, pengiriman lampiran, efektivitas biaya, dan ketersediaan 24/7.
- Kelemahan surel mencakup risiko spam dan serangan _phishing_, kelebihan informasi, kurangnya komunikasi tatap muka, potensi miskomunikasi, dan masalah teknis.

# Laporan Mail Server

## Postfix Configuration

Konfigurasi SMTP-Auth untuk menggunakan Davecot SASL Function

1. Instalasi Postfix:
	Gunakan perintah dibawah ini untuk melakukan instalasi postfix
	```bash
	apt -y install postfix sasl2-bin
	```
2. uncomment mail_owner
	![postfix](images/postfix/1.jpg)
3. uncomment and specify hostname
	Gunakan hostname sesuai dengan kelompok masing-masing yang sudah dikonfigurasi di awal.
	
	![postfix](images/postfix/1.jpg)
4. Uncomment and specify domain name
	Gunakan domain name sesuai dengan kelompok masing-masing yang sudah dikonfigurasikan pada praktikum sebelumnya
	
	![postfix](images/postfix/2.jpg)
5. Uncomment myorigin
	![postfix](images/postfix/3.jpg)
6. Uncomment inet_interfaces
	![postfix](images/postfix/4.jpg)
7. Uncomment mydestination
	![postfix](images/postfix/5.jpg)
8. Uncomment local_recipient_maps
	![postfix](images/postfix/6.jpg)
9. Uncomment mynetworks_style
	![postfix](images/postfix/7.jpg)
10. Tambahkan local network
	Tambahkan local network yang digunakan / terhubung dengan PC
	
	![postfix](images/postfix/8.jpg)
11. Uncomment alias_maps
	![postfix](images/postfix/9.jpg)
12. Uncomment alias_database
	![postfix](images/postfix/10.jpg)
13. Uncomment home_mailbox
	![postfix](images/postfix/11.jpg)
14. Comment smtpd debian dan tambahkan smtpd baru
	Comment baris smtpd_banner Debian dan tambahkan smtpd_banner yang baru tanpa $email_name
	
	![postfix](images/postfix/12.jpg)
15. Tambahkan beberapa path baru dan satu group baru
	- sendmail_path
	- newaliases_path
	- mailq_path
	- setgid_group
	
	![postfix](images/postfix/13.jpg)
16. Comment out baris directory-directory
	```bash
	# line 679 : comment out
	#html_directory =
	
	# line 683 : comment out
	#manpage_directory =
	
	# line 688 : comment out
	#sample_directory =
	
	# line 692 : comment out
	#readme_directory =
 	```

17. Ubah inet protocol menjadi IPv4, disable SMTP VRFY command, required HELO command, atur message size limit, dan tambahkan SMTP Auth Settings
	![postfix](images/postfix/14.jpg)
	
18. Jalan command newaliases dan restart postfix
	```bash
	root@mail:~# newaliases
	root@mail:~# systemctl restart postfix
	```

Konfigurasi Additional Settings
Konfigurasi ini digunakan untuk menolak spam emails, tetapi harus berhati-hati karena juga bisa menolak normal emails jika ada konfigurasi yang tidak match.

![postfix](images/postfix/15.jpg)

## Davecot Configuration

Konfigurasi Fungsi SASL ke Postfix

1. Instalasti dovecot-core dovecot-pop3d dovecot-imapd
	![postfix](images/Dovecot/1.jpg)
2. Uncomment baris yang menentukan alamat IP yang akan digunakan Dovecot untuk mendengarkan koneksi masuk.
	Penjelasan rinci:
	- `*` berarti semua alamat IPv4 pada sistem (misalnya `0.0.0.0`).
	- `::` berarti semua alamat IPv6 pada sistem.
	
	![postfix](images/Dovecot/2.jpg)
3. Uncomment dan ubah untuk allow plain text auth
	![postfix](images/Dovecot/3.jpg)
4. Tambahkan mekanisme auth
	![postfix](images/Dovecot/4.jpg)
5. Ubah mail location ke Maildir
	![postfix](images/Dovecot/5.jpg)
6. Mengaktifkan otentikasi SMTP (SMTP AUTH) antara Postfix dan Dovecot melalui socket UNIX.
	Penjelasan fungsi:
	- `unix_listener /var/spool/postfix/private/auth`  
		Menyediakan **socket UNIX** di path tersebut yang akan digunakan oleh Postfix untuk berkomunikasi dengan Dovecot **auth service**.
	- `mode = 0666`  
		Mengatur **permission** socket menjadi "read/write" untuk semua user (ini aman karena path-nya berada di direktori yang hanya dapat diakses oleh root dan pengguna tepercaya seperti `postfix`).
	- `user = postfix` dan `group = postfix`  
		Mengatur **kepemilikan** socket supaya **Postfix** bisa mengaksesnya, karena proses Postfix berjalan sebagai user dan group `postfix`.
	
	![postfix](images/Dovecot/6.jpg)
7. Restart Dovecot
	```bash
	root@mail:~# systemctl restart dovecot
	```
## Add Mail User Accounts 

Menambahkan Mail user account untuk menggunakan Mail Service, pada contoh kasus ini menggunakan akun OS User.

1. Instalasi Mailutils
	```bash
	root@mail:~# apt -y install mailutils
	```

2. Atur environment variables untuk menggunakan Maildir dan tambahkan OS user baru
	![postfix](images/1.jpg)
	
3. Login sebagai user dan coba untuk mengirimkan email
	![postfix](images/1.jpg)
	
	![postfix](images/2.jpg)
	
	Dapat dilihat email sudah terkirim dan diterima.