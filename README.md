# BerdeTak

**Heart Rate & SpO₂ Monitoring System berbasis Internet of Things**

## Overview

BerdeTak adalah proyek akhir mata kuliah Internet of Things berupa sistem pemantauan Heart Rate (HR) dan Saturasi Oksigen (SpO₂) berbasis IoT. Sistem ini memanfaatkan sensor MAX30102 dan ESP32 untuk melakukan pengukuran sinyal Photoplethysmography (PPG) secara real-time, kemudian menampilkan hasilnya melalui aplikasi Android.

Pengembangan BerdeTak berfokus pada penerapan metode, parameter, dan algoritma yang mengacu pada literatur ilmiah dan praktik penelitian PPG, sehingga sistem tidak hanya berfungsi secara teknis, tetapi juga memiliki dasar metodologis yang jelas.

## Features

- Real-time monitoring Heart Rate dan SpO₂ (update setiap 1 detik ke layar pengguna)
- Pemrosesan sinyal PPG berbasis algoritma resmi Maxim Integrated
- Hasil pengukuran berbasis rata-rata 60 detik (minute-mean)
- Monitoring kualitas sinyal untuk meminimalkan noise
- Riwayat data per hari ini, kemarin, 7 hari yang lalu, serta custom
- Hasil pengukuran yang dapat diunduh dan dikirim ke berbagai platform
- Riwayat data pengukuran dengan visualisasi grafik tren untuk melihat pola perubahan HR dan SpO₂

## System Architecture

BerdeTak terdiri dari tiga komponen utama:

1. **Sensor Layer**: MAX30102 untuk akuisisi sinyal PPG (IR dan Red LED)
2. **Processing & Communication Layer**: ESP32 untuk pemrosesan sinyal dan pengiriman data
3. **Application Layer**: Aplikasi Android untuk visualisasi data real-time dan riwayat

## Measurement Methodology

Metodologi pengukuran pada BerdeTak dirancang dengan mengacu pada standar dan praktik terbaik dalam penelitian PPG.

### Sampling Configuration

- **Frekuensi sampling**: 100 Hz
- **Durasi pengukuran**: 60 detik
- **Total sampel**: 6.000 sampel per sesi

**Referensi**:
- JoGH 2022 (PMC9041243)
- Sensors 2019 (PMC6514840)

### Signal Processing

- **Sliding window**: 1 detik (100 sampel)
- Pemrosesan berkelanjutan untuk mendukung real-time monitoring
- **Algoritma**: `maxim_heart_rate_and_oxygen_saturation()`

Algoritma ini merupakan algoritma standar industri yang banyak digunakan dalam penelitian dan implementasi pulse oximeter berbasis PPG.

### Signal Quality Control

Untuk menjaga reliabilitas data, dilakukan mekanisme kontrol kualitas sinyal:

- Threshold sinyal IR (< 50.000)
- Evaluasi stabilitas sinyal setiap 5 detik
- Pembacaan tidak stabil tidak digunakan dalam perhitungan akhir

### Result Aggregation

- Update nilai HR dan SpO₂ setiap 1 detik
- Hasil akhir berupa rata-rata pembacaan valid selama 60 detik (minute-mean)

Pendekatan ini mengacu pada praktik umum dalam penelitian HR berbasis PPG.

### Physiological Range Validation

Pembacaan hasil dibatasi pada rentang fisiologis yang umum digunakan:

- **Heart Rate**: 40–220 bpm
- **SpO₂**: 70–100%

**Referensi**:
- ISO 80601-2-61
- Pedoman FDA
- Nature (2025)

## Validation Scope

Validasi yang dilakukan dalam proyek ini mencakup:

- Kesesuaian metode dan algoritma dengan literatur ilmiah
- Validasi kualitas sinyal dan rentang fisiologis

**Tidak termasuk dalam lingkup proyek ini**:
- Uji klinis
- Validasi terhadap ECG atau pulse oximeter medis tersertifikasi

## Disclaimer

⚠️ **BerdeTak merupakan proyek akademik untuk mata kuliah Internet of Things**. Sistem ini dikembangkan untuk tujuan pembelajaran dan penelitian, serta **tidak dimaksudkan sebagai alat medis atau untuk diagnosis klinis**.

## Future Improvements

- Perbandingan hasil dengan pulse oximeter medis sebagai ground truth
- Evaluasi akurasi pada berbagai kondisi aktivitas pengguna
- Kalibrasi sensor berbasis populasi
- Integrasi dashboard berbasis cloud

## Tech Stack

- ESP32
- MAX30102 Sensor
- Android Application
- IoT Communication Protocol

## License

Proyek ini dikembangkan untuk keperluan akademik dan pembelajaran.

---

**Developed with ❤️ for IoT Course**
