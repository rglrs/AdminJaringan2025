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

## Install Debian di komputer lab

## Table content

- [Solve LAN Wired Not Connected](#solve-lan-wired-not-connected)
- [IP Komputer Lab](#ip-komputer-lab)
- [Clone Github](#clone-github)
- [Download Virtual Box](#download-virtual-box)
- [Download ISO Debian 12](#download-iso-debian-12)
- [Install VirtualBox](#install-virtualbox)
- [Setelah proses instalasi, buka aplikasi virtualbox](#setelah-proses-instalasi-buka-aplikasi-virtualbox)
- [New Virtual Machine](#new-virtual-machine)

### Solve LAN Wired Not Connected

![dhclient.jpg](assets/dhclient.jpg)

```bash
sudo dhclient -v
```

Perintah `sudo dhclient -v` digunakan untuk meminta atau memperbarui alamat IP dari server DHCP dengan menampilkan output secara rinci.

### IP Komputer Lab

![ip-komputer-lab.jpg](assets/ip-komputer-lab.jpg)

Setelah Berhasil connect dengan LAN maka komputer akan mendapatkan ip address

### Clone Github

Install git di komputer lab

![install-git.jpg](assets/install-git.jpg)

```bash
sudo apt install git
```

clone with git clone 

![clone-github-pak-ferry.jpg](assets/clone-github-pak-ferry.jpg)

```bash
git clone https://github.com/ferryastika/unix-and-linux-sysadmin-notes.git
```

Cek OS 

![cek-use-os.jpg](assets/cek-use-os.jpg)

```bash
lsb_release -a
```

### Download Virtual Box

![download-vm.jpg](assets/download-vm.jpg)

https://www.virtualbox.org/wiki/Linux_Downloads

### Download ISO Debian 12

![download-debian.jpg](assets/download-debian.jpg)

https://www.debian.org/download

### Install VirtualBox

![image.png](assets/image.png)

```bash
sudo dpkg -i virtualbox-7.1_7.1.6-167084~Debian~bookworm_amd64.deb
```

### Setelah proses instalasi, buka aplikasi virtualbox

akan muncul error seperti gambar dibawah ini:

![error_afteropenvm.jpg](assets/error_afteropenvm.jpg)

![vboxusers.jpg](assets/vboxusers.jpg)

Solve menggunakan perintah :

```bash
sudo usermod -a -G vboxusers $USERS
```

Perintah ini menambahkan pengguna yang sedang login ke dalam grup `vboxusers`, yang biasanya diperlukan agar bisa mengakses fitur tertentu di VirtualBox, seperti USB passthrough.

### New Virtual Machine

Sesuaikan Name dan Operating System seperti gambar dibawah ini

![cvm-name-os.jpg](assets/cvm-name-os.jpg)

Sesuaikan Unattended Install seperti gambar dibawah ini

![cvm-ui.jpg](assets/cvm-ui.jpg)

Sesuaikan Hardware seperti gambar dibawah ini

![cvm-h.jpg](assets/cvm-h.jpg)

Sesuaikan Hard Disk seperti gambar dibawah ini

![cvm-hd.jpg](assets/cvm-hd.jpg)

Langkah selanjutnya klik finish dan tunggu loading hingga selesai 

![cvm-i-cnwDHCP.jpg](assets/cvm-i-cnwDHCP.jpg)

![cvm-i-configapt.jpg](assets/cvm-i-configapt.jpg)

![cvm-i-ibs.jpg](assets/cvm-i-ibs.jpg)

Jika sudah seperti gambar dibawah ini bisa dipastikan install debian 12 telah berhasil

![cvm-db12-welcome.jpg](assets/cvm-db12-welcome.jpg)

Selanjutnya klik next next hingga done

![cvm-db12-typing.jpg](assets/cvm-db12-typing.jpg)

![cvm-db12-privacy.jpg](assets/cvm-db12-privacy.jpg)

![cvm-db12-oa.jpg](assets/cvm-db12-oa.jpg)

![cvm-db12-done.jpg](assets/cvm-db12-done.jpg)
