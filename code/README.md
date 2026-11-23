# SmartSense – Android Sensor Monitoring App

[![Platform](https://img.shields.io/badge/Platform-Android-green.svg)](https://developer.android.com/)
[![Kotlin](https://img.shields.io/badge/Kotlin-2.0.21-blue.svg)](https://kotlinlang.org/)
[![Jetpack Compose](https://img.shields.io/badge/Jetpack%20Compose-Material%203-blueviolet.svg)](https://developer.android.com/jetpack/compose)
[![Architecture](https://img.shields.io/badge/Architecture-MVVM-orange.svg)](https://developer.android.com/topic/architecture)
[![Database](https://img.shields.io/badge/Database-Room%20%2F%20SQLite-red.svg)](https://developer.android.com/training/data-storage/room)

---

## 1. NAMA APLIKASI
**SmartSense** (Android Sensor Monitoring App)

---

## 2. DESKRIPSI APLIKASI
**SmartSense** adalah aplikasi Android native modern yang dirancang untuk memantau kondisi lingkungan fisik dan aktivitas pengguna secara *real-time* dengan memanfaatkan sensor perangkat keras bawaan (*built-in hardware sensors*) smartphone Android. 

Aplikasi ini membaca data langsung dari **Accelerometer Sensor** (sumbu X, Y, Z dan magnitudo gerak) serta **Light Sensor** (intensitas cahaya dalam satuan lux beserta klasifikasi kondisi pencahayaan). Pengguna dapat melihat hasil pembacaan real-time, menyimpan data ke database lokal SQLite menggunakan Room, meninjau riwayat lengkap, menganalisis statistik visual tren pengukuran, dan memeriksa kompatibilitas sensor perangkat keras smartphone.

---

## 3. TUJUAN DAN MANFAAT APLIKASI

### Tujuan:
1. Menyediakan platform pemantauan kondisi lingkungan (pencahayaan) dan gerak perangkat secara langsung, akurat, dan hemat daya.
2. Mengimplementasikan arsitektur berstandar industri modern Android: **MVVM (Model-View-ViewModel)** dengan **Kotlin Coroutines & Flow**.
3. Menerapkan persistensi data terstruktur menggunakan **SQLite** melalui abstraksi **Room Database**.
4. Memberikan umpan balik visual yang informatif, modern, dan responsif menggunakan **Jetpack Compose** dan **Material Design 3**.

### Manfaat:
- **Bagi Pengguna:** Membantu mengukur tingkat pencahayaan ruangan kerja/belajar apakah telah memenuhi standar ergonomis (redup vs ideal) serta mendeteksi getaran atau pergerakan smartphone.
- **Bagi Pengembang/Pendidikan:** Menjadi contoh referensi implementasi native Android modern dengan integrasi SensorManager, Jetpack Compose, Room Database, dan StateFlow tanpa library pihak ketiga yang berlebihan.

---

## 4. DAFTAR FITUR APLIKASI

### A. Dashboard (Beranda)
- Menampilkan judul aplikasi **SmartSense** dengan banner modern bertema *Modern Smart Technology*.
- Menampilkan ringkasan status sensor aktif/siaga.
- Menampilkan status Accelerometer (indikator gerak real-time & nilai akselerasi).
- Menampilkan intensitas cahaya terbaru (lux) beserta kategori kondisi.
- Menampilkan jumlah total data monitoring yang tersimpan di SQLite.
- Tombol aksi cepat untuk memulai monitoring serta navigasi ke seluruh halaman utama.

### B. Live Sensor Monitoring
- Pemantauan Accelerometer secara real-time dengan pemisahan sumbu X, Y, dan Z lengkap dengan progress bar dinamis.
- Perhitungan magnitudo akselerasi total ($A = \sqrt{X^2 + Y^2 + Z^2}$) dan deteksi status pergerakan (**Relatif Diam** vs **Bergerak**).
- Pengukuran sensor cahaya lingkungan dalam satuan **lux** beserta meter visual indikator.
- Klasifikasi kondisi lingkungan: **Gelap**, **Redup**, **Normal**, dan **Terang**.
- Tombol **Mulai Monitoring** dan **Hentikan Monitoring** yang mengontrol pendaftaran listener sensor secara efisien.
- Tombol **Simpan Manual** untuk menyimpan cuplikan pembacaan saat ini ke database SQLite.
- Fitur **Perekaman Otomatis (Auto-Save)** dengan interval 5 detik untuk mencegah kelebihan data (*throttling/debouncing*).
- Peringatan (*fallback banner*) jika perangkat fisik atau emulator tidak memiliki sensor terkait.

### C. Riwayat Monitoring (History)
- Menampilkan daftar histori seluruh data sensor yang pernah disimpan ke SQLite.
- Disortir otomatis berdasarkan waktu terbaru (*timestamp descending*).
- Menampilkan label tanggal dan jam perekaman terformat (`dd MMM yyyy, HH:mm:ss`).
- Menampilkan chip status visual pencahayaan dan pergerakan.
- Fitur hapus data satuan per item.
- Fitur **Hapus Seluruh Riwayat** dilengkapi dialog konfirmasi keamanan (*AlertDialog*).
- Tampilan placeholder informatif jika belum ada data yang tersimpan.

### D. Detail Monitoring
- Menampilkan rincian lengkap dari suatu rekaman sensor yang dipilih pengguna.
- Menampilkan nilai Accelerometer sumbu X, Y, dan Z dengan indikator visual.
- Menampilkan nilai magnitudo akselerasi total dan klasifikasi status aktivitas.
- Menampilkan intensitas cahaya dalam lux, badge kategori, dan deskripsi kondisi.
- Menampilkan informasi waktu perekaman (tanggal, jam, dan nilai Unix timestamp).
- Tombol pintas untuk menghapus entri dari database dan kembali ke riwayat.

### E. Statistik & Analisis Tren
- Menampilkan metrik **Rata-Rata Intensitas Cahaya**.
- Menampilkan metrik nilai **Cahaya Minimum** dan **Cahaya Maksimum**.
- Menampilkan total jumlah entri tersimpan di SQLite.
- Ringkasan aktivitas pengguna: persentase dan perbandingan jumlah kondisi **Bergerak** vs **Relatif Diam**.
- Grafik garis tren sensor (*Custom Line Chart Canvas*) yang menampilkan fluktuasi intensitas 20 data terakhir dengan gradien warna, titik data, dan garis bantu (*gridlines*).
- Distribusi visual kondisi pencahayaan (Gelap, Redup, Normal, Terang).

### F. Pengaturan & Sistem (Settings)
- Menampilkan informasi detail aplikasi SmartSense (Versi 1.0, arsitektur, database, UI toolkit).
- Ringkasan sensor utama yang diimplementasikan (Accelerometer & Light Sensor).
- Deteksi dan inventarisasi seluruh sensor perangkat keras yang terpasang pada smartphone (`SensorManager.getSensorList(Sensor.TYPE_ALL)`), meliputi nama sensor, vendor, konsumsi daya (mA), resolusi, dan jangkauan maksimum.

---

## 5. TEKNOLOGI YANG DIGUNAKAN

| Komponen | Teknologi | Keterangan |
|---|---|---|
| **Bahasa Pemrograman** | Kotlin 2.0.21 | Bahasa native Android dengan dukungan Coroutines & Flow |
| **UI Toolkit** | Jetpack Compose | UI deklaratif 100% tanpa XML layout |
| **Design System** | Material Design 3 | MaterialTheme, Dynamic Color Scheme, Modern Typography |
| **Arsitektur** | MVVM | Pemisahan Model, View, dan ViewModel yang bersih |
| **Database Lokal** | SQLite via Room 2.6.1 | Persistence abstraction layer dengan KSP compiler |
| **Asynchronous & Stream** | Kotlin Coroutines & StateFlow | Reactive data stream yang lifecycle-aware |
| **Hardware Access** | Android SensorManager API | Akses langsung ke sensor akselerometer dan cahaya |
| **Navigasi** | Navigation Compose 2.8.5 | Single Activity navigation dengan transisi animasi |
| **Build System** | Gradle 9.1.0 & AGP 9.0.1 | Android Gradle Plugin versi modern |

---

## 6. PENJELASAN ARSITEKTUR MVVM

Aplikasi SmartSense menerapkan pola arsitektur **Model-View-ViewModel (MVVM)** sesuai rekomendasi resmi Google Android:

```
┌────────────────────────────────────────────────────────┐
│                   VIEW (Jetpack Compose)               │
│  HomeScreen, MonitoringScreen, HistoryScreen,          │
│  DetailScreen, StatisticsScreen, SettingsScreen        │
└───────────────────────────▲────────────────────────────┘
                            │ Mengamati StateFlow
                            │ Mengirimkan User Events
┌───────────────────────────▼────────────────────────────┐
│                        VIEWMODEL                       │
│  SensorViewModel, HistoryViewModel,                    │
│  StatisticsViewModel                                   │
└─────────────▲────────────────────────────▲─────────────┘
              │                            │
   Flow data  │                 Panggil    │
   real-time  │                 operasi DB │
┌─────────────▼──────────┐      ┌──────────▼─────────────┐
│      SENSOR LAYER      │      │       REPOSITORY       │
│  AccelerometerSensor   │      │    SensorRepository    │
│  LightSensor           │      └──────────▲─────────────┘
│  SensorManagerHelper   │                 │ Query / Insert
└────────────────────────┘      ┌──────────▼─────────────┐
                                │       DATA LAYER       │
                                │  SensorDao / Room DB   │
                                │    (SQLite Storage)    │
                                └────────────────────────┘
```

1. **Model (Domain & Data Layer):**
   - Merepresentasikan entitas data (`SensorEntity`), domain model (`SensorData`), enum kondisi (`LightCondition`, `MotionCondition`), serta antarmuka akses database (`SensorDao`).
   - `SensorRepository` bertindak sebagai *single source of truth* yang mengisolasi logika database dari lapisan UI.
2. **ViewModel (Presentation Logic):**
   - Mengelola state UI menggunakan `StateFlow` yang aman terhadap perubahan konfigurasi (*configuration change* seperti rotasi layar).
   - `SensorViewModel` mengontrol listener sensor, menghitung status pergerakan & cahaya, serta mengatur interval auto-save.
   - `HistoryViewModel` mengelola daftar riwayat, penghapusan item, dan dialog konfirmasi.
   - `StatisticsViewModel` memproses agregasi data numerik (rata-rata, min, max, persentase).
3. **View (UI Layer):**
   - Dibangun sepenuhnya menggunakan Jetpack Compose.
   - Komponen UI bersifat *stateless* dan hanya bertugas merender state yang dipancarkan oleh ViewModel serta meneruskan aksi pengguna (klik, toggle) ke ViewModel.

---

## 7. PENJELASAN DATABASE SQLITE / ROOM

Data hasil monitoring disimpan secara permanen di database lokal SQLite menggunakan **Room Database**.

### Skema Tabel `sensor_data`:
| Nama Kolom | Tipe Data | Keterangan |
|---|---|---|
| `id` | `INTEGER` (Long) | Primary Key, Auto Increment |
| `accelerometerX` | `REAL` (Float) | Pembacaan akselerasi sumbu X ($m/s^2$) |
| `accelerometerY` | `REAL` (Float) | Pembacaan akselerasi sumbu Y ($m/s^2$) |
| `accelerometerZ` | `REAL` (Float) | Pembacaan akselerasi sumbu Z ($m/s^2$) |
| `lightLevel` | `REAL` (Float) | Pembacaan intensitas cahaya dalam satuan lux ($lx$) |
| `timestamp` | `INTEGER` (Long) | Waktu perekaman dalam format Unix timestamp (milidetik) |

### Operasi Database (`SensorDao`):
- `insert(sensorData: SensorEntity): Long` – Menyimpan 1 data perekaman sensor ke SQLite.
- `getAllData(): Flow<List<SensorEntity>>` – Mengambil seluruh data tersimpan terurut dari yang terbaru (*timestamp DESC*).
- `getDataById(id: Long): Flow<SensorEntity?>` – Mengambil 1 entri data berdasarkan ID unik.
- `getRecentData(limit: Int): Flow<List<SensorEntity>>` – Mengambil N data terbaru untuk keperluan plotting grafik.
- `deleteById(id: Long): Int` – Menghapus satu rekaman tertentu.
- `deleteAll(): Int` – Mengosongkan seluruh isi tabel sensor data.
- `getCount(): Flow<Int>` – Mengambil total jumlah entri tersimpan.
- `getAverageLight(): Flow<Float?>` – Menghitung rata-rata intensitas cahaya menggunakan agregasi SQL `AVG()`.
- `getMinLight(): Flow<Float?>` – Mengambil nilai cahaya terendah menggunakan `MIN()`.
- `getMaxLight(): Flow<Float?>` – Mengambil nilai cahaya tertinggi menggunakan `MAX()`.

---

## 8. PENJELASAN ACCELEROMETER SENSOR

### Karakteristik & Fungsi:
- **Tipe Sensor:** `Sensor.TYPE_ACCELEROMETER` (Hardware Motion Sensor).
- Mengukur percepatan linear yang dialami smartphone pada tiga sumbu ortogonal:
  - **Sumbu X:** Percepatan horizontal ke kanan (+) dan kiri (-).
  - **Sumbu Y:** Percepatan vertikal ke atas (+) dan bawah (-).
  - **Sumbu Z:** Percepatan tegak lurus terhadap layar ke depan (+) dan belakang (-).
- Saat perangkat diletakkan diam mendatar di atas meja, sensor mengukur percepatan gravitasi bumi sebesar kurang lebih $\approx 9.81\ m/s^2$ pada sumbu Z.
- **Logika Deteksi Gerakan:**
  Magnitudo percepatan total dihitung menggunakan rumus:
  $$A_{\text{total}} = \sqrt{X^2 + Y^2 + Z^2}$$
  Selisih terhadap gravitasi bumi dihitung dengan:
  $$\Delta A = |A_{\text{total}} - 9.81|$$
  - Jika $\Delta A > 1.2\ m/s^2$: Perangkat diklasifikasikan **"Bergerak"**.
  - Jika $\Delta A \le 1.2\ m/s^2$: Perangkat diklasifikasikan **"Relatif Diam"**.

---

## 9. PENJELASAN LIGHT SENSOR (AMBIENT LIGHT)

### Karakteristik & Fungsi:
- **Tipe Sensor:** `Sensor.TYPE_LIGHT` (Hardware Environment Sensor).
- Mengukur intensitas pencahayaan di sekitar perangkat dalam satuan **lux** ($lx$).
- Digunakan smartphone untuk menyesuaikan kecerahan layar secara otomatis (*auto brightness*).
- **Klasifikasi Kondisi Pencahayaan pada SmartSense:**
  | Kategori | Rentang Nilai (Lux) | Deskripsi Kondisi Lingkungan |
  |---|---|---|
  | **Gelap** | $< 10\ lx$ | Kondisi malam hari, ruangan tanpa lampu, atau sensor tertutup. |
  | **Redup** | $10 - 50\ lx$ | Pencahayaan temaram, lorong remang, atau waktu senja. |
  | **Normal** | $50 - 500\ lx$ | Pencahayaan standar ruangan kerja, kantor, atau ruang belajar. |
  | **Terang** | $> 500\ lx$ | Pencahayaan sangat terang, dekat jendela, atau di luar ruangan (*outdoor*). |

---

## 10. STRUKTUR FOLDER PROJECT

```
com.example.smartsense/
│
├── data/
│   ├── local/
│   │   ├── SensorEntity.kt          # Entitas tabel Room 'sensor_data'
│   │   ├── SensorDao.kt             # Antarmuka DAO query SQLite
│   │   └── SensorDatabase.kt        # Singleton RoomDatabase
│   │
│   └── repository/
│       └── SensorRepository.kt      # Repository penghubung data & ViewModel
│
├── domain/
│   └── model/
│       └── SensorData.kt            # Domain model, enum Light/MotionCondition & mapper
│
├── sensor/
│   ├── AccelerometerSensor.kt       # SensorEventListener Flow untuk Accelerometer
│   ├── LightSensor.kt               # SensorEventListener Flow untuk Ambient Light
│   └── SensorManagerHelper.kt       # Helper inventaris & pengecekan sensor perangkat
│
├── ui/
│   ├── screens/
│   │   ├── HomeScreen.kt            # Halaman Dashboard ringkasan kondisi
│   │   ├── MonitoringScreen.kt      # Halaman Live Monitoring real-time sensor
│   │   ├── HistoryScreen.kt         # Halaman Riwayat penyimpanan SQLite
│   │   ├── DetailScreen.kt          # Halaman Detail satu rekaman sensor
│   │   ├── StatisticsScreen.kt      # Halaman Statistik & analisis distribusi
│   │   └── SettingsScreen.kt        # Halaman Pengaturan & sensor terdeteksi
│   │
│   ├── components/
│   │   ├── BottomNavigationBar.kt   # Komponen navigasi bawah (5 menu)
│   │   ├── SensorCard.kt            # Kartu visual akselerometer, lux meter & banner
│   │   └── SensorChart.kt           # Custom Line Chart Canvas untuk visualisasi tren
│   │
│   └── theme/
│       ├── Color.kt                 # Palet warna Modern Smart Technology
│       ├── Theme.kt                 # Konfigurasi Material 3 Theme
│       └── Type.kt                  # Tipografi sistem
│
├── viewmodel/
│   ├── SensorViewModel.kt           # State management live monitoring & auto-save
│   ├── HistoryViewModel.kt          # State management daftar & penghapusan histori
│   └── StatisticsViewModel.kt       # State management statistik & data grafik
│
├── navigation/
│   └── AppNavigation.kt             # Host navigasi Compose & route navigation
│
└── MainActivity.kt                  # Entry point aplikasi Android
```

---

## 11. SCREENSHOT SELURUH HALAMAN APLIKASI

Folder `screenshots/` disediakan pada root repository untuk menyimpan tangkapan layar setiap halaman.

| No | Halaman | Deskripsi Tampilan | File Target |
|:---:|---|---|---|
| 1 | **Dashboard (Home)** | Menampilkan nama SmartSense, status sensor, count SQLite, dan navigasi cepat | `screenshots/01_dashboard_home.png` |
| 2 | **Live Monitoring** | Real-time gauge sumbu X, Y, Z, lux meter, tombol Mulai/Stop & Auto-Save | `screenshots/02_live_monitoring.png` |
| 3 | **Riwayat Monitoring** | Daftar kartu histori tersimpan terurut waktu terbaru beserta badge status | `screenshots/03_history_list.png` |
| 4 | **Detail Monitoring** | Rincian lengkap rekaman tertentu, visual bar, dan tombol hapus | `screenshots/04_detail_monitoring.png` |
| 5 | **Statistik & Grafik** | Kartu rata-rata, min/max lux, grafik tren Canvas, dan persentase aktivitas | `screenshots/05_statistics_chart.png` |
| 6 | **Pengaturan & Sensor** | Informasi aplikasi, arsitektur, dan daftar sensor hardware pada perangkat | `screenshots/06_settings_sensors.png` |

> *Catatan: Jalankan aplikasi di Android Studio Emulator atau Smartphone fisik, lalu gunakan fitur **Take Screenshot** pada tab Running Devices / Logcat untuk menyimpan tangkapan layar ke folder `screenshots/`.*

---

## 12. CARA INSTALASI DAN MENJALANKAN APLIKASI

### Prasyarat Sistem:
1. **Android Studio:** Android Studio Koala / Ladybug / Meerkat atau yang lebih baru.
2. **Java Development Kit:** JDK 17 atau JDK 21 (sudah include di Android Studio jbr).
3. **Android SDK:** SDK API Level 24 (Android 7.0 Nougat) hingga API Level 35 (Android 15).

### Langkah-Langkah Menjalankan:
1. Buka Android Studio.
2. Pilih menu **File -> Open...**, lalu arahkan ke direktori project:
   ```
   SensorUjian
   ```
3. Tunggu hingga proses **Gradle Sync** selesai secara otomatis.
4. Hubungkan smartphone Android fisik melalui kabel USB (aktifkan *USB Debugging*) atau jalankan Android Virtual Device (AVD Emulator).
5. Klik tombol **Run 'app'** (ikon panah hijau ▶ atau `Shift + F10`).
6. Aplikasi **SmartSense** akan ter-compile, terpasang, dan terbuka di perangkat.

### Menjalankan Build via Terminal (Command Line):
```bash
# Build Debug APK
./gradlew assembleDebug

# Menjalankan Unit Test
./gradlew testDebugUnitTest
```
File APK siap instalasi tersimpan di:
`app/build/outputs/apk/debug/app-debug.apk`

---

## 13. CARA MELAKUKAN PENGUJIAN SENSOR

### A. Pengujian pada Perangkat Smartphone Fisik:
1. **Uji Accelerometer:**
   - Letakkan ponsel di atas meja datar: Perhatikan bahwa status menunjukkan **"Relatif Diam"** dengan nilai sumbu Z mendekati $+9.8\ m/s^2$.
   - Angkat dan goyangkan ponsel perlahan: Nilai sumbu X, Y, dan Z akan bergerak dinamis dan status badge berubah menjadi **"Bergerak"**.
   - Miringkan ponsel ke kiri atau kanan untuk mengamati perubahan nilai pada sumbu X.
2. **Uji Light Sensor:**
   - Dekatkan ponsel ke lampu ruangan atau bawa ke luar ruangan: Nilai lux akan naik di atas $500\ lx$ dan badge berubah menjadi **"Terang"**.
   - Tutup area sensor cahaya (biasanya di samping kamera depan bagian atas layar) dengan telapak tangan: Nilai lux akan turun drastis ke $< 10\ lx$ dan badge berubah menjadi **"Gelap"**.
3. **Uji Penyimpanan SQLite:**
   - Tekan tombol **Simpan**: Buka tab **Riwayat**, periksa bahwa data baru langsung muncul di baris teratas.
   - Aktifkan toggle **Perekaman Otomatis**: Data akan tersimpan berkala setiap 5 detik.
   - Tutup aplikasi sepenuhnya (*kill app*), lalu buka kembali: Seluruh data riwayat tetap tersimpan utuh di database SQLite.

### B. Pengujian pada Android Emulator (Virtual Device):
1. Buka jendela **Extended Controls** emulator (ikon tiga titik `...` pada toolbar emulator).
2. Pilih tab **Virtual Sensors**:
   - Pada sub-menu **Accelerometer**: Geser slider sumbu X, Y, Z atau putar model 3D perangkat untuk menyimulasikan orientasi ponsel.
   - Pada sub-menu **Light**: Geser slider intensitas cahaya dari 0 lux hingga 40.000 lux untuk melihat responsivitas meter dan badge kategori pencahayaan.

---

## 14. INFORMASI KOMPATIBILITAS PERANGKAT

- **Minimum SDK (minSdk):** API Level 24 (Android 7.0 Nougat) – Kompatibel dengan $> 95\%$ perangkat Android aktif di seluruh dunia.
- **Target SDK (targetSdk):** API Level 35 (Android 15).
- **Compile SDK (compileSdk):** API Level 35.
- **Dukungan Arsitektur CPU:** `arm64-v8a`, `armeabi-v7a`, `x86`, `x86_64`.
- **Ketahanan Sensor (Sensor Fallback):**
  Aplikasi secara otomatis mendeteksi ketersediaan sensor hardware saat runtime. Jika smartphone atau emulator tidak memiliki sensor tertentu, aplikasi menampilkan *informative banner* dan **tidak akan crash**, sehingga seluruh fitur lainnya (riwayat data, database, pengaturan, dan sensor yang tersedia) tetap dapat digunakan dengan sempurna.

---

*Dikembangkan dengan ❤️ menggunakan Kotlin, Jetpack Compose, dan Material Design 3.*
