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

## Setting Modul untuk Gaussian 16
Menyiapkan modul untuk Gaussian 16 untuk mempermudah penggunaannya:
1. **Membuat Modul**: Buat file modul untuk Gaussian 16 di direktori `modules`.
2. **Memuat Modul**: Muat modul yang telah dibuat agar Gaussian 16 bisa digunakan.

## Menjalankan Gaussian 16
Langkah-langkah dasar untuk menjalankan Gaussian 16:
1. **Menyiapkan File Input** untuk perhitungan.
2. **Menjalankan Gaussian 16** dengan file input yang telah disiapkan.

## Menjalankan Batch
Jika ingin menjalankan perhitungan di server menggunakan **job scheduler**:
1. **Buat Skrip Batch** untuk SLURM atau PBS.
2. **Jalankan Skrip** dengan job scheduler (misalnya, `sbatch`).

## Troubleshooting
Solusi untuk masalah umum yang mungkin terjadi selama instalasi dan penggunaan Gaussian 16.

## Penutup
Ringkasan dan tips akhir untuk menggunakan Gaussian 16 dengan sukses.