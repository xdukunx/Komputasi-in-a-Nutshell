# Gaussian16 - Perhitungan DFT - TD DFT Kimia Komputasi
Gaussian16 adalah perangkat lunak kimia komputasi yang digunakan untuk perhitungan energi, struktur molekul, sifat optik, dan banyak lagi, terutama untuk perhitungan kimia kuantum. Ini sangat berguna dalam simulasi molekul, DFT (Density Functional Theory), dan post-Hartree-Fock methods untuk perhitungan sifat molekul seperti spektrum UV-VIS dan analisis dinamik reaksi kimia. [(unduh di sini)](https://gaussian.com/)

## Daftar Isi
- [Pendahuluan](#pendahuluan)
- [Persyaratan Sistem](#persyaratan-sistem)
- [Instalasi Gaussian 16](#instalasi-gaussian-16)
- [Setting Modul untuk Gaussian 16](#setting-modul-untuk-gaussian-16)
- [Menjalankan Gaussian 16](#menjalankan-gaussian-16)
- [Menjalankan Batch](#menjalankan-batch)
- [Troubleshooting](#troubleshooting)
- [Penutup](#penutup)

## Pendahuluan
Panduan ini menjelaskan cara menginstal, mengonfigurasi, dan menjalankan **Gaussian 16**, perangkat lunak kimia komputasi untuk perhitungan energi, struktur molekul, serta spektrum optik dan reaksi kimia.

## Persyaratan Sistem
- Sistem operasi Linux/Windows/MacOS (dengan akses ke terminal dan hak akses penuh ke directory masing2)
- Ruang penyimpanan yang cukup untuk instalasi
- Akses ke server dengan Gaussian 16

## Instalasi Gaussian 16
Langkah-langkah untuk menginstal Gaussian 16 di sistem Anda:
1. **Persiapkan Direktori** tempat instalasi, anda bebas menggunakan metode apapun (Terminal/SFTP). Sebagai contoh, saya menaruh Gaussian 16 di 

```bash
/home/mfadhana/software/g16
```

2. **Unduh dan Ekstrak Paket** Gaussian 16 ke dalam direktori tersebut.

```bash
cd /home/username/software/g16
tar -xvzf gaussian16.tar.gz
Ganti username dengan milik masing2
```

3. **Instalasi Gaussian 16**
Pastikan file sudah diekstrak dengan benar, hal ini ditandai dengan adanya folder seperti g16,lib,bin, dan lainnya.
Gaussian 16 menyediakan skrip install yang terletak di dalam folder bsd/. Anda harus menjalankan skrip ini untuk melakukan instalasi lebih lanjut.
```bash
cd bsd
./install
```
Agar sistem dapat mengenali perintah g16, kita harus mengenalkan tempat instalasi g16 kita agar diketahui oleh lingkungan sistem. Edit file **~/.bashrc**
```bash
nano ~/.bashrc
#tambahkan baris kode berikut
export g16root=$HOME/software/g16 #sesuai tempat gaussian diinstall
export PATH=$g16root:$PATH
export GAUSS_SCRDIR=$HOME/software/g16/scratch
export GAUSS_EXEDIR=$g16root
#lalu save 
#(bila menggunakan text editor, bisa langsung ctrl+s.)
#(bila menggunakan nano, bisa save dengan menekan ctrl+X, kemudian tekan Y untuk menyimpan perubahan, dan tekan Enter untuk keluar.)
```
Agar perubahan tersebut dapat diterapkan, kita perlu memuat ulang konfigurasi di terminal, lakukan dengan perintah berikut:
```bash
source ~/.bashrc
```
## Pengujian Keberhasilan Instalasi
Jalankan perintah berikut untuk memeriksa apakah Gaussian 16 terinstal dengan benar:
```bash
g16
```
Jika instalasi berhasil, Anda akan melihat output yang menunjukkan versi Gaussian 16 yang terinstal beserta informasi lainnya.
Untuk memeriksa apakah variabel GAUSS_EXEDIR dan g16root sudah diatur dengan benar, Anda bisa menjalankan:
```bash
echo $GAUSS_EXEDIR
echo $g16root
# Hasilnya harus mengarah ke direktori di mana Anda menginstal Gaussian 16, misalnya /home/username/software/g16.
```

## Setting Modul untuk Gaussian 16
Untuk mempermudah penggunaan Gaussian 16 di server atau HPC, buat modul untuk mengatur lingkungan Gaussian. Berikut adalah langkah-langkah membuat file modul:
1. **Membuat Modul**: Buat folder dan file modul untuk Gaussian 16 di direktori `modules`.
```bash
mkdir -p /mgpfs/home/username/modules/g16
nano /mgpfs/home/username/modules/g16/g16
```
Isi file g16 dengan konfigurasi berikut:
```bash
#%Module1.0
# Module file for Gaussian16

setenv GAUSS_EXEDIR /mgpfs/home/username/software/g16
setenv GAUSS_SCRDIR /mgpfs/home/username/software/g16/scratch
prepend-path PATH /mgpfs/home/username/software/g16
setenv GAUSS_MEM 2GB # sesuaikan dengan spesifikasi yang diperlukan
setenv GAUSS_NPROC 4 # sesuaikan dengan spesifikasi yang diperlukan
```
2. **Memuat Modul**: Muat modul yang telah dibuat agar Gaussian 16 bisa digunakan, muat modul tersebut dengan perintah berikut:
```bash 
module use /mgpfs/home/username/modules
module load g16
# anda juga bisa menaruh ini di bashrc agar tidak mengulangi proses load module terus menerus
```
Lakukan konfigurasi ulang shell untuk menambahkan sistem module di 'bashrc'
```bash
nano ~/.bashrc
# Tambahkan baris berikut
module use /mgpfs/home/username/modules
module load g16
export MODULEPATH=$MODULEPATH:$HOME/modules
```
Jangan lupa untuk menetapkan konfigurasi terbaru yang sudah kita susun:
```bash
source ~/.bashrc
```

# Menjalankan Gaussian 16
Setelah Anda berhasil menginstal Gaussian 16, langkah selanjutnya adalah menyiapkan file input yang akan digunakan untuk perhitungan kimia komputasi. File input untuk Gaussian 16 dapat berupa dua format utama: .com dan .gjf. Kedua format ini pada dasarnya memiliki fungsi yang sama, yaitu untuk memberikan instruksi kepada Gaussian 16 mengenai perhitungan yang akan dilakukan, tetapi .com lebih umum digunakan, sedangkan .gjf lebih sering digunakan untuk file yang dihasilkan atau diekspor dari aplikasi lain, seperti GaussView.

[GaussView](https://drive.google.com/file/d/12rvIudLKtjXZCQGpXtvfxb-rztYlLvnd/view?usp=drive_link) adalah antarmuka grafis untuk Gaussian 16 yang dirancang untuk membantu pengguna dalam memodelkan struktur molekul, menyiapkan file input, dan membaca hasil output dari perhitungan Gaussian 16.

![tampilanGaussView](https://github.com/user-attachments/assets/df93734e-308d-40d8-8863-991c1926d208)

Setelah molekul dimodelkan, GaussView memungkinkan Anda untuk menyimpan file input untuk Gaussian 16 dalam format .com atau .gjf. Anda dapat memilih jenis perhitungan yang ingin dilakukan, seperti optimasi geometri atau perhitungan energi.

![pembuatangjf](https://github.com/user-attachments/assets/e7ae1486-889e-451e-b70b-97c2ca2496b5)

Setelah file input dibuat, tahapan selanjutnya yaitu menguji molekul yang kita buat di Gaussian. Pindahkan file input ke Server untuk proses kalkulasi.
Setelah file input siap, jalankan Gaussian 16 dengan perintah berikut:
```bash
g16 input_file.gjf > output_file.log & # Penggunaan tanda "&" yaitu agar proses kalkulasi berjalan di background dan kita bisa beraktivitas yang lain
# Gantilah input_file dengan nama file input yang telah Anda buat dan output_file dengan nama yang anda inginkan
```
Untuk memeriksa proses kalkulasi, jalankan perintah berikut:
```bash
tail -f output_file.log
```
Apabila berhasil berjalan, nantinya akan muncul beberapa baris yang sedang melakukan proses kalkulasi matematis. Apabila proses kalkulasi, akan muncul berbagai data seperti **waktu yang ditempuh**,**energi optimasi**, dan **quotes** dari berbagai ilmuwan yang khas dari Gaussian.

![g16berhasil](https://github.com/user-attachments/assets/c857bfda-04e0-4210-b04f-45c77cfe4a98)

## Menjalankan Batch
Jika ingin menjalankan perhitungan di server menggunakan **job scheduler**:
1. **Buat Skrip Batch** untuk SLURM atau PBS.
2. **Jalankan Skrip** dengan job scheduler (misalnya, `sbatch`).

## Troubleshooting
Solusi untuk masalah umum yang mungkin terjadi selama instalasi dan penggunaan Gaussian 16.

## Penutup
Ringkasan dan tips akhir untuk menggunakan Gaussian 16 dengan sukses.