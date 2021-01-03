---
layout: post
title: Menghubungkan Unity Profiler dengan Emulator Android Seperti NOX dan MEMU
author: magicjar
categories: unity blog
tags: blog unity profiler nox memu android emulator game
comments: true
cover: "/assets/images/2021/01/unity-nox-memu.jpg"
date: 2021-01-03 08:19 +0700
---
Siapa disini yang kesusahan menghubungkan Unity *Profiler* dengan *emulator* Android seperti NOX dan MEMU?

Kalau kalian baca ini berarti pertanyaan saya diatas sangat relevan.

Kali ini saya akan membahas cara menyambungkan / mengonekkan Unity *Profiler* dengan NOX dan MEMU. Hal ini saya bahas karena saya juga mengalami kesusahan saat ingin *testing* game saya di *emulator* tersebut karena belum tahu caranya.

* Content
{:toc}

## Apa itu Unity *Profiler*?
Sebelum kita bahas lebh lanjut, apa sih *Unity Profiler* itu? *Unity Profiler* adalah alat yang digunakan untuk mengetahui seberapa besar penggunaan *resource hardware device* pada game atau aplikasi yang kita buat di Unity. Karena kegunaan itulah, kita dapat mengetahui komponen-komponen mana yang memakan *resource* banyak sehingga kita dapat mengoptimalkannya. Hal ini sangat penting apa lagi jika target pengguna kalian kelas *low-end* yang mempunyai spesifikasi *hardware* rendah agar tidak *lag* saat memainkan game kalian. *Unity Profiler* umumnya dapat dihubungkan dengan semua perangkat yang bersistem operasi Android dan mendukung perintah *adb*. Kalian dapat menyambungkannya dengan gawai kalian dan juga bisa dengan *emulator* Android.

## Langkah Menghubungkan Unity Profiler dengan Emulator Android
Sebagai catatan saya menggunakan Unity3D 2019.4.16f1, NOX 6.6.1.3, dan MEMU 7.3.0.

### Cara 1
Cara ini akan memadukan fitur Unity *Build And Run* dengan *Profiler*. Jadi ketika proses *build* selesai, Unity akan secara otomatis menginstall dan menjalankan aplikasi yang baru saja di-*build* ke *emulator* dan otomatis membuka jendela Unity *Profiler* dan menyambungkannya dengan *emulator*.

1. Pertama-tama, aktifkan *Developer Options* dan hidupkan *USB Debuging* di *emulator* kalian.
2. Buka *Terminal / Command Prompt / PowerShell* dengan mode *Administrator*. Hal ini wajib jika kalian menginstall Android SDK di *Drive C:/*.
3. Buka *emulator* pilihan kalian, bisa NOX atau MEMU, jangan kedua-duanya, bisa bentrokan.
4. Arahkan *terminal* kalian ke folder *adb* didalam installasi Android SDK.
    ``` sh
    cd C:\{Folder-Android-SDK}\platform-tools
    ```
5. Hubungkan *adb* dengan *emulator*.
    ``` sh
    adb connect 127.0.0.1:{port}
    ```
    Berikut port untuk masing-masing emulator:
    
    Emulator|Port
    ---|----
    NOX|127.0.0.1:62001
    MEMU|127.0.0.1:21503

6. Cek dahulu apakah *adb* sudah terhubung dengan *emulator*.
    ``` sh
    adb devices
    ```
    Jika sudah terhubung maka akan muncul daftar perangkat seperti dibawah. Jika belum, ulangi langkah 4.
    ``` sh
    List of devices attached
    127.0.0.1:{port} device
    ```

    Urusan kita dengan *adb* sudah selesai (jangan tutup *terminal*-nya dahulu), sekarang tinggal mengatur Unity.

7. Buka *Build Setting*.
    ```
    File -> Build Setting.
    ```
8. Pada bagian *Run Device* pilih nama *emulator* yang kalian pakai. Jika tidak ada, coba klik *Refresh*.
9. Beri centang pada "Development Build" dan "Autoconnect Profiler".
10. Klik *Build And Run*
11. Tunggu sampai proses *build* selesai dan Unity akan otomatis menginstall game kalian kedalam *emulator* dan jendela Unity *Profiler* akan muncul.
12. Langkah terakhir yaitu memilih *target device* di profiler dengan mengeklik *dropdown* dibagian atas jendela *profiler* dan pilih *AndroidPlayer(ADB@127.0.0.1:34999)*. Unity *Profiler* akan memulai mencatat data penggunaan *resource* game kalian.

### Cara 2
Cara yang kedua ini kita tidak menggunakan fitur *Build And Run*. Cara ini bisa dipakai jika kalian hanya ingin melakukan *profiling* aplikasi yang sudah di-*build* terlebih dahulu.

Untuk cara kedua ini terdapat sedikit perbedaan antara *emulator* NOX dengan MEMU.

#### NOX
1. Arahkan *terminal* ke folder **Android SDK**.
    ``` sh
    cd C:\{Folder-Android-SDK}\platform-tools
    ```

2. Hubungkan *adb* dengan NOX menggunakan *adb connect*.
    ``` sh
    adb connect 127.0.0.1:62001
    ```

3. Arahkan kembali *terminal* ke folder data NOX (biasanya berada di **D:\Program Files**).
    ``` sh
    cd D:\Program Files\Nox\bin
    ```

4. Jalankan perintah *adb forward*
    ``` sh
    adb forward tcp:34999 localabstract:Unity-com.NamaPerusahaan.NamaProduk
    ```

5. Langkah terakhir, jalankan aplikasi yang ingin di *profiling* dan buka jendela *Profiler* lalu pilih *AndroidPlayer(ADB@127.0.0.1:34999)*.

#### Memu
1. Arahkan *terminal* ke folder data MEMU (biasanya berada di **D:\Program Files**).
    ``` sh
    cd D:\Program Files\Microvirt\MEmu
    ```

2. Hubungkan *adb* dengan MEMU menggunakan *adb connect*.
    ``` sh
    adb connect 127.0.0.1:21503
    ```

3. Jalankan perintah *adb forward*
    ``` sh
    adb forward tcp:34999 localabstract:Unity-com.NamaPerusahaan.NamaProduk
    ```

4. Langkah terakhir, jalankan aplikasi yang ingin di *profiling* dan buka jendela *Profiler* lalu pilih *AndroidPlayer(ADB@127.0.0.1:34999)*.

## Kesimpulan
Begitulah tadi cara-cara menghubungkan Unity *Profiler* dengan *emulator* Android. Tinggal pilih cara mana yang cocok dengan kalian, kalau saya sih cara 1, karena tinggal klik *Build And Run* semua selesai. Sebenarnya cara ini juga dapat digunakan untuk *emulator* selain NOX dan MEMU seperti Bluestack dan Genymotion, kalian tinggal cari *port*-nya saja karena tiap *emulator* mempunyai port yang berbeda. Nah setelah ini, tugas kalian adalah mengoptimasi aplikasi yang sudah kalian buat. Selamat bereksperimen.

Jika punya pertanyaan atau mungkin ada yang masih belum berhasil, tulis saja dikolom komentar dibawah.

Kalau artikel ini bermanfaat, bisalah ya bantu share. Terima kasih.

## FAQ (Frequently Asked Questions)
<div class="accordion" id="accordionExample">
  <div class="card">
    <div class="card-header">
      <h5 class="mb-0">
        <button class="btn btn-link" type="button" data-toggle="collapse" data-target="#faq1" aria-controls="faq1">
          #1. Unity <i>Profiler</i> tidak mau tersambung dengan <i>AndroidPlayer (ADB@127.0.0.1:34999)</i>
        </button>
      </h5>
    </div>
    <div id="faq1" class="collapse show">
      <div class="card-body">
        Jalankan perintah berikut:
        <br>
        adb forward tcp:34999 localabstract:Unity-com.NamaPerusahaan.NamaProduk
      </div>
    </div>
  </div>
  <div class="card">
    <div class="card-header">
      <h5 class="mb-0">
        <button class="btn btn-link" type="button" data-toggle="collapse" data-target="#faq2" aria-controls="faq2">
          #2. Build error karena NOX menggunakan OpenGL ES 2.0 sedangkan Unity membutuhkan OpenGL ES 3.0
        </button>
      </h5>
    </div>
    <div id="faq2" class="collapse show">
      <div class="card-body">
        Buka Multi-Drive NOX dan hapus semua player yang ada disana, lalu buat player baru dan jangan utak-atik pengaturannya.
      </div>
    </div>
  </div>
  <div class="card">
    <div class="card-header">
      <h5 class="mb-0">
        <button class="btn btn-link" type="button" data-toggle="collapse" data-target="#faq3" aria-controls="faq3">
          #3. Lebih bagius NOX atau MEMU?
        </button>
      </h5>
    </div>
    <div id="faq3" class="collapse show">
      <div class="card-body">
        Setelah pengamatan dan pemakaian keduanya, menurut saya NOX lah yang paling stabil. Tetapi terkadang NOX suka berulah dan muncullah error seperti di FAQ #2.<br>
        Kalau ingin lebih pasti, coba install keduanya dan bandingkan sendiri.
      </div>
    </div>
  </div>
  <div class="card">
    <div class="card-header">
      <h5 class="mb-0">
        <button class="btn btn-link" type="button" data-toggle="collapse" data-target="#faq4" aria-controls="faq4">
          #4. NOX dan MEMU port-nya berapa?
        </button>
      </h5>
    </div>
    <div id="faq4" class="collapse show">
      <div class="card-body">
        Bacalah wahai manusia
        <br><br>
        NOX     : 127.0.0.1:62001<br>
        MEMU    : 127.0.0.1:21503
      </div>
    </div>
  </div>
  <div class="card">
    <div class="card-header">
      <h5 class="mb-0">
        <button class="btn btn-link" type="button" data-toggle="collapse" data-target="#faq5" aria-controls="faq5">
          #5. Tidak ada pilihan AndroidPlayer(ADB@127.0.0.1:34999)
        </button>
      </h5>
    </div>
    <div id="faq5" class="collapse show">
      <div class="card-body">
        Coba pilih <i>Enter IP</i> dan masukkan 127.0.0.1. Dengan ini unity akan memindai apakah ada player yang dapat dihubungkan dengan profiler.
      </div>
    </div>
  </div>
</div>
