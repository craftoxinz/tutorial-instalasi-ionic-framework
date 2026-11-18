# Tutorial Lengkap Instalasi Ionic Framework

Panduan dari nol: menyiapkan tools, membuat project, sampai aplikasi mobile berjalan di browser, emulator, maupun perangkat fisik.

> **Catatan versi:** Ionic, Capacitor, dan Android Studio sering diperbarui. Kebutuhan versi minimum (terutama JDK dan Node.js) bisa berubah, jadi cek dokumentasi resmi di <https://ionicframework.com/docs> dan <https://capacitorjs.com/docs> jika ada error terkait versi.

---

## Daftar Isi

1. [Gambaran Umum](#1-gambaran-umum)
2. [Kebutuhan Sistem](#2-kebutuhan-sistem)
3. [Install Kode Editor (VS Code)](#3-install-kode-editor-vs-code)
4. [Install Git](#4-install-git)
5. [Install Node.js dan npm](#5-install-nodejs-dan-npm)
6. [Install Ionic CLI](#6-install-ionic-cli)
7. [Membuat Project Pertama](#7-membuat-project-pertama)
8. [Menjalankan di Browser](#8-menjalankan-di-browser)
9. [Menjalankan di Android](#9-menjalankan-di-android)
10. [Menjalankan di iOS (macOS)](#10-menjalankan-di-ios-macos)
11. [Live Reload di Perangkat](#11-live-reload-di-perangkat)
12. [Struktur Project](#12-struktur-project)
13. [Troubleshooting](#13-troubleshooting)
14. [Cheat Sheet Perintah](#14-cheat-sheet-perintah)

---

## 1. Gambaran Umum

Ionic adalah framework UI open-source untuk membangun aplikasi mobile, web, dan desktop dari satu codebase menggunakan teknologi web (HTML, CSS, JavaScript/TypeScript).

Komponen yang akan kita pakai:

| Komponen | Fungsi |
|---|---|
| **Ionic Framework** | Kumpulan komponen UI (button, list, modal, dll.) |
| **Ionic CLI** | Command line untuk membuat, menjalankan, dan membangun project |
| **Capacitor** | Native runtime yang membungkus web app menjadi aplikasi Android/iOS |
| **Angular / React / Vue** | Framework web pilihan untuk logika aplikasi |

Alur kerja secara umum:

```
Kode web (Angular/React/Vue) -> build -> Capacitor -> project native Android/iOS -> APK/IPA
```

---

## 2. Kebutuhan Sistem

| Kebutuhan | Keterangan |
|---|---|
| OS | Windows 10/11, macOS, atau Linux |
| RAM | Minimal 8 GB (16 GB disarankan jika memakai emulator Android) |
| Penyimpanan | Minimal 15 GB kosong (Android Studio + SDK + emulator cukup besar) |
| Koneksi internet | Dibutuhkan untuk mengunduh paket dan SDK |
| iOS | **Wajib macOS** + Xcode untuk build aplikasi iOS |

> Jika hanya ingin belajar atau membuat aplikasi yang diuji di browser, kamu **tidak perlu** Android Studio. Langkah 9-10 hanya untuk menjalankan di perangkat/emulator.

---

## 3. Install Kode Editor (VS Code)

1. Unduh Visual Studio Code dari <https://code.visualstudio.com>.
2. Jalankan installer. Pada Windows, centang opsi:
   - **Add to PATH**
   - **Add "Open with Code" action** (opsional, tapi praktis)
3. Buka VS Code, lalu install ekstensi berikut lewat panel **Extensions** (`Ctrl+Shift+X`):

| Ekstensi | Kegunaan |
|---|---|
| **Ionic** (resmi) | Integrasi Ionic di VS Code (menjalankan app, manajemen project) |
| **Angular Language Service** | Jika memilih Angular |
| **ES7+ React/Redux/React-Native snippets** | Jika memilih React |
| **Vue - Official** | Jika memilih Vue |
| **ESLint** | Linting JavaScript/TypeScript |
| **Prettier - Code formatter** | Format kode otomatis |
| **Tailwind CSS IntelliSense** | Opsional, jika memakai Tailwind |

Alternatif editor: WebStorm, Sublime Text, atau editor lain yang kamu nyaman pakai. Ionic tidak mewajibkan editor tertentu.

---

## 4. Install Git

Git dibutuhkan oleh beberapa starter template dan sangat berguna untuk version control.

- **Windows:** unduh dari <https://git-scm.com/download/win>, lalu install dengan opsi default.
- **macOS:** jalankan `xcode-select --install` atau `brew install git`.
- **Linux (Debian/Ubuntu):** `sudo apt install git`.

Verifikasi:

```bash
git --version
```

---

## 5. Install Node.js dan npm

Ionic CLI berjalan di atas Node.js. Gunakan versi **LTS** (Long Term Support).

### Opsi A: Installer resmi (paling sederhana)

1. Buka <https://nodejs.org>.
2. Unduh versi **LTS**, lalu install.
3. Restart terminal setelah instalasi.

### Opsi B: Node Version Manager (disarankan untuk developer)

Cocok jika kamu mengerjakan beberapa project dengan versi Node berbeda.

- **Windows:** install [nvm-windows](https://github.com/coreybutler/nvm-windows/releases), lalu:

  ```powershell
  nvm install lts
  nvm use lts
  ```

- **macOS/Linux:** install [nvm](https://github.com/nvm-sh/nvm), lalu:

  ```bash
  nvm install --lts
  nvm use --lts
  ```

### Verifikasi

```bash
node -v
npm -v
```

Kedua perintah harus menampilkan nomor versi.

---

## 6. Install Ionic CLI

Install secara global:

```bash
npm install -g @ionic/cli
```

Verifikasi:

```bash
ionic --version
```

Jika muncul nomor versi, Ionic CLI siap dipakai.

> **Error permission di macOS/Linux?** Jangan pakai `sudo npm install -g`. Lebih aman gunakan nvm (Opsi B di langkah 5) agar global package terpasang di direktori user.

---

## 7. Membuat Project Pertama

Pindah ke folder tempat kamu menyimpan project, lalu jalankan:

```bash
ionic start myApp blank
```

CLI akan menanyakan beberapa pilihan secara interaktif:

1. **Framework:** Angular, React, atau Vue.
2. **Template** (jika tidak ditentukan): `blank`, `tabs`, atau `sidemenu`.
3. *(Khusus Angular)* **Standalone components atau NgModules.** Standalone adalah pilihan yang direkomendasikan untuk project baru.

### Cara non-interaktif (langsung tentukan opsi)

```bash
# Angular
ionic start myApp tabs --type=angular

# React (TypeScript)
ionic start myApp tabs --type=react

# Vue
ionic start myApp tabs --type=vue
```

Template yang tersedia:

| Template | Deskripsi |
|---|---|
| `blank` | Satu halaman kosong, cocok sebagai awal |
| `tabs` | Navigasi tab di bagian bawah |
| `sidemenu` | Menu samping (drawer) |

Setelah selesai, CLI akan menginstall dependency dan membuat folder `myApp`. Masuk ke folder tersebut:

```bash
cd myApp
```

Buka di VS Code:

```bash
code .
```

---

## 8. Menjalankan di Browser

Cara tercepat untuk melihat hasilnya:

```bash
ionic serve
```

Perintah ini menjalankan development server dan otomatis membuka browser di `http://localhost:8100` (Angular/Vue/React dengan Vite bisa memakai port lain, lihat output terminal). Setiap perubahan kode akan di-reload otomatis.

### Melihat tampilan mobile di browser

1. Buka DevTools (`F12`).
2. Aktifkan **Device Toolbar** (`Ctrl+Shift+M`).
3. Pilih perangkat seperti iPhone atau Pixel.

### Opsi tambahan

```bash
ionic serve --lab        # tampilan iOS & Android berdampingan (perlu @ionic/lab)
ionic serve --external   # bisa diakses dari perangkat lain di jaringan yang sama
```

---

## 9. Menjalankan di Android

Untuk menjalankan sebagai aplikasi native, kita butuh Android Studio, JDK, dan Android SDK.

### 9.1 Install Android Studio

1. Unduh dari <https://developer.android.com/studio>.
2. Jalankan installer dan ikuti wizard dengan setting default. Pastikan komponen berikut terpilih:
   - **Android SDK**
   - **Android SDK Platform**
   - **Android Virtual Device** (jika ingin memakai emulator)
3. Buka Android Studio, lalu masuk ke **More Actions -> SDK Manager** (atau **Settings -> Languages & Frameworks -> Android SDK**).
4. Di tab **SDK Platforms**, pastikan minimal satu API level terbaru terpasang.
5. Di tab **SDK Tools**, pastikan terpasang:
   - Android SDK Build-Tools
   - Android SDK Command-line Tools
   - Android SDK Platform-Tools
   - Android Emulator

### 9.2 JDK

Android Studio sudah menyertakan JDK sendiri (JetBrains Runtime), dan Capacitor memakainya saat build lewat Android Studio. Untuk build via command line, pastikan versi JDK sesuai kebutuhan Capacitor di dokumentasi resminya (versi terbaru umumnya membutuhkan JDK 21).

Verifikasi (jika JDK terpasang terpisah):

```bash
java -version
```

### 9.3 Set Environment Variable

**Windows (PowerShell, permanen):**

```powershell
[Environment]::SetEnvironmentVariable("ANDROID_HOME", "$env:LOCALAPPDATA\Android\Sdk", "User")
```

Lalu tambahkan ke **Path** (System Properties -> Environment Variables):

```
%ANDROID_HOME%\platform-tools
%ANDROID_HOME%\emulator
```

**macOS/Linux** (tambahkan ke `~/.zshrc` atau `~/.bashrc`):

```bash
export ANDROID_HOME=$HOME/Library/Android/sdk   # macOS
# export ANDROID_HOME=$HOME/Android/Sdk         # Linux
export PATH=$PATH:$ANDROID_HOME/platform-tools
export PATH=$PATH:$ANDROID_HOME/emulator
```

Terapkan perubahan dengan membuka terminal baru, lalu verifikasi:

```bash
adb --version
```

### 9.4 Buat Emulator (AVD)

1. Di Android Studio, buka **More Actions -> Virtual Device Manager**.
2. Klik **Create Device**, pilih perangkat (misalnya Pixel 7).
3. Pilih system image (unduh jika belum ada), lalu **Finish**.
4. Klik tombol **Play** untuk menjalankan emulator.

> **Emulator lambat atau tidak jalan?** Aktifkan virtualisasi (Intel VT-x / AMD-V) di BIOS. Di Windows, pastikan **Windows Hypervisor Platform** aktif.

### 9.5 Tambahkan Platform Android ke Project

Dari folder project:

```bash
ionic build
ionic cap add android
```

Perintah ini membuat folder `android/` berisi project native.

### 9.6 Jalankan Aplikasi

**Cara 1: lewat command line**

```bash
ionic cap run android
```

CLI akan menampilkan daftar perangkat/emulator yang tersedia, lalu menginstall dan menjalankan aplikasi.

**Cara 2: lewat Android Studio**

```bash
ionic cap sync
ionic cap open android
```

Di Android Studio, tunggu Gradle sync selesai, pilih perangkat target, lalu klik tombol **Run** (ikon segitiga hijau).

### 9.7 Menjalankan di HP Android Fisik

1. Di HP, buka **Settings -> About phone**, ketuk **Build number** 7 kali untuk mengaktifkan Developer Options.
2. Buka **Developer options**, aktifkan **USB debugging**.
3. Sambungkan HP ke komputer dengan kabel USB, lalu izinkan debugging pada prompt di HP.
4. Cek perangkat terdeteksi:

   ```bash
   adb devices
   ```

5. Jalankan `ionic cap run android` dan pilih perangkat tersebut.

---

## 10. Menjalankan di iOS (macOS)

> Build iOS hanya bisa dilakukan di **macOS**. Pengguna Windows/Linux tidak bisa menjalankan simulator atau build iOS secara lokal.

1. Install **Xcode** dari Mac App Store.
2. Install Command Line Tools:

   ```bash
   xcode-select --install
   ```

3. Install CocoaPods:

   ```bash
   brew install cocoapods
   ```

4. Dari folder project:

   ```bash
   ionic build
   ionic cap add ios
   ionic cap run ios
   ```

   Atau buka di Xcode:

   ```bash
   ionic cap sync
   ionic cap open ios
   ```

5. Di Xcode, pilih simulator atau perangkat, lalu klik **Run**. Untuk perangkat fisik, atur **Signing & Capabilities** dengan Apple ID kamu.

---

## 11. Live Reload di Perangkat

Agar perubahan kode langsung muncul di emulator/HP tanpa build ulang:

```bash
ionic cap run android -l --external
```

Penjelasan flag:

- `-l` (`--livereload`): aktifkan live reload.
- `--external`: buka server agar bisa diakses dari perangkat.

Pastikan komputer dan HP berada pada **jaringan WiFi yang sama** (untuk emulator tidak perlu).

---

## 12. Struktur Project

Contoh struktur untuk project Angular (React/Vue serupa dengan perbedaan di folder `src`):

```
myApp/
├── android/              # Project native Android (setelah cap add android)
├── ios/                  # Project native iOS (setelah cap add ios)
├── src/
│   ├── app/              # Komponen, halaman, dan service
│   ├── assets/           # Gambar, ikon, dll.
│   ├── theme/            # Variabel tema Ionic (warna, dll.)
│   ├── global.scss       # Style global
│   └── index.html
├── capacitor.config.ts   # Konfigurasi Capacitor (appId, appName, webDir)
├── ionic.config.json     # Konfigurasi Ionic CLI
├── package.json
└── tsconfig.json
```

File `capacitor.config.ts` penting untuk diatur:

```ts
import type { CapacitorConfig } from '@capacitor/cli';

const config: CapacitorConfig = {
  appId: 'com.example.myapp',  // ganti dengan ID unik, misal com.namakamu.myapp
  appName: 'myApp',
  webDir: 'www',               // folder hasil build (Angular: www, React/Vue Vite: dist)
};

export default config;
```

> Pastikan `webDir` sesuai dengan folder output build framework yang kamu pilih. Jika salah, aplikasi akan blank di perangkat.

---

## 13. Troubleshooting

| Masalah | Solusi |
|---|---|
| `ionic: command not found` | Restart terminal. Pastikan folder global npm ada di PATH (`npm config get prefix`). |
| `EACCES` saat install global (macOS/Linux) | Gunakan nvm, jangan pakai `sudo`. |
| `ionic serve` gagal karena port terpakai | Gunakan `ionic serve --port=8200`. |
| `ANDROID_HOME` / SDK tidak ditemukan | Cek environment variable (langkah 9.3) dan buka terminal baru. |
| `adb devices` kosong | Aktifkan USB debugging, ganti kabel/port USB, pilih mode **File Transfer**. |
| Layar blank di perangkat | Cek `webDir` di `capacitor.config.ts`, lalu jalankan `ionic build` dan `ionic cap sync`. |
| Gradle sync / build gagal | Buka project di Android Studio, ikuti saran perbaikan di panel Build, pastikan versi JDK sesuai. |
| Emulator sangat lambat | Aktifkan virtualisasi di BIOS, alokasikan RAM lebih besar untuk AVD. |
| Perubahan kode tidak muncul di perangkat | Jalankan `ionic build` lalu `ionic cap sync` (tanpa live reload, build harus diulang). |
| Error versi Node | Gunakan versi Node LTS dan cek persyaratan di dokumentasi framework yang dipilih. |

---

## 14. Cheat Sheet Perintah

```bash
# Setup awal
npm install -g @ionic/cli
ionic start myApp tabs --type=react
cd myApp

# Development di browser
ionic serve

# Tambah platform native
ionic build
ionic cap add android
ionic cap add ios

# Sinkronisasi setelah ubah kode web atau tambah plugin
ionic build
ionic cap sync

# Jalankan di perangkat/emulator
ionic cap run android
ionic cap run android -l --external   # dengan live reload
ionic cap run ios

# Buka di IDE native
ionic cap open android
ionic cap open ios

# Tambah plugin Capacitor (contoh: Camera)
npm install @capacitor/camera
ionic cap sync
```

---

## Langkah Selanjutnya

- Pelajari komponen UI: <https://ionicframework.com/docs/components>
- Dokumentasi Capacitor dan plugin native: <https://capacitorjs.com/docs>
- Panduan publikasi ke Play Store/App Store: <https://ionicframework.com/docs/deployment>

Selamat mencoba!
