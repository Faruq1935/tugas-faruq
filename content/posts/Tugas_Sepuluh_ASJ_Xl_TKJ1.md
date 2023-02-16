---
title: "Tugas_Sepuluh_ASJ_Xl_TKJ1"
date: 2022-06-03T21:52:16+07:00
draft: false
tags: "Administrasi_Sistem_Jaringan"
---

**Nama : Muhammad Faruq Syarifudin**

**No Nisn : 5925**

**Kelas : Xl TKJ 1**

**Tugas 10 B-6 cara install samba dan quota di debian 8 untuk membatasi penyimpanan setiap user**

Cara install dan konfigurasi file sharing samba dengan quota di Debian 8

*===*

1. Install sistem operasi Debian 11 untuk Sisi server.

2. Jika sudah selesai lakukan update pada sistem dengan perintah apt update.

3. Kemudian install paket samba dengan perintah apt install samba.

4. Setelah selesai lakukan konfigurasi pada file sharing samba dengan perintah "nano /etc/samba/smb.conf".

5. Ctrl + w tuliskan read-only kemudian enter setelah itu ubah read-only = yes ke
read-only = no dan tambahkan di bawahnya security = user

6. Kemudian menambahkan user yang berguna untuk client dengan perintah "adduser namauser" Enter terus sampai ada pilihan y/n kemudian pilih y enter.

7. Kemudian buat password untuk user tersebut dengan perintah "smbpasswd -a namauser" masukaan password yang mudah diingat misal 12345

8. Setelah itu kita tinggal restart service samba dengan perintah "/etc/init.d/samba restart"

9. Kita bisa mengecek samba berjalan dengan normal dengan perintah "/etc/init.d/samba status" jika bertuliskan active running berarti konfigurasi berhasil.

10. Kemudian tambahkan repo nya :
edit source list dengan perinth nano /etc/apt /source.list
# deb http://ftp.us.debian.org/debian/ jessie main contrib non-free
# deb-src http://ftp.us.debian.org/debian/ jessie main contrib non-free
seperti biasa setelah update repo haris update “apt update”

11. Kita langsung ke quota disk dengan perintah "apt install quota" untuk menginstall quota disk pada Debian.

12. Kemudian kita perlu memperbaharui opsi pemsangan sistem file dengan perintah "nano /etc/fstab"

13. Akan muncul isi file sebagai berikut :
# /etc/fstab: static file system information.
UUID=06b2aae3-b525-4a4c-9549-0fc6045bd08e        /        ext4        errors=remount-ro        0        1
Kemudian kalian ubah Dan tambahkan seperti berikut :
# /etc/fstab: static file system information.
UUID=06b2aae3-b525-4a4c-9549-0fc6045bd08e        /        ext4        errors=remount-ro,usrquota,grpquota        0        1
Keterangan :
Perubahan di atas akan memungkinkan kita untuk mengaktifkan kuota berbasis pengguna ( usrquota) dan berbasis grup ( ) pada sistem file. grpquota Jika Kalian hanya membutuhkan satu atau yang lain, Kalian dapat mengabaikan opsi yang tidak digunakan.

14. Pasang kembali sistem file dengan perintah "mount -o remount /".

15. Kita bisa memverifikasi bahwa opsi baru digunakan untuk memasang sistem file dengan melihat  /proc/mounts file. Di sini, kami menggunakan grepuntuk hanya menampilkan entri sistem file root di file itu : 
cat /proc/mounts | grep ' / '
Hasilnya :
/dev/vda1 / ext4 rw,relatime,quota,usrquota,grpquota,errors=remount-ro,data=ordered 0 0

16. Ketelah itu ketikan “quotacheck -ugm /”

17. Lanjutkan dengan “quotaon -v /”

18. Terakhir ketikan “edquota -u namasiswa”
hasilnya : ubah ukuran soft dari 0 ke 102400 lalu juga dengan hard dari 0 ke 102400

19. Pengujina di lakukan di client windows dengan membuka file manager lalu klik kanan “This Pc” pilih map newtwork ketikan di kolom \\192.168.23.2\namasiswa alamat ip tadi dari eth0

20. masukan user namasisawa dan password 123 klik enter

21. cobalah untuk mengirim file lebih dari 102400 jika gagal maka anda berhasil :D

22. coba juga kirim file lebih kecil dari 102400 jika berhasil maka anda dapar nilai dari guru kalian :D
