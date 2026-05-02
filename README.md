# Nickel Chrome Plating Simulator

Web-based simulator untuk proses **Nickel Chrome Plating**.  
Aplikasi ini dibuat untuk membantu menghitung waktu Proses Plating, kebutuhan Tank tambahan, Cycle Time Output, serta visualisasi alur **Rack Hanger** dari proses Loading sampai Unloading.

## Overview

Simulator ini digunakan untuk menganalisis flow process Nickel Chrome Plating berdasarkan data proses aktual. Sistem dapat menghitung:

- Total waktu dipping.
- Total waktu transfer antar tank.
- Lead time 1 Rack Hanger.
- Output Rack Hanger per jam.
- Output produk per jam.
- Rekomendasi jumlah tank tambahan.
- Visualisasi Rack Hanger saat melewati setiap tank.
- Total Rack Hanger yang selesai diproses.

Tank tambahan hanya dapat diterapkan pada proses berikut:

1. Semibright Nickel
2. High Sulfur Nickel
3. Bright Nickel
4. Micro Porous Nickel

## Features

### 1. Cycle Time Calculation

User dapat memasukkan target cycle time output dalam satuan:

```text
menit / Rack Hanger
````

Sistem akan menghitung apakah target tersebut dapat dicapai berdasarkan bottleneck proses.

### 2. Tank Recommendation

Sistem menghitung jumlah minimum tank yang dibutuhkan menggunakan rumus:

```text
Jumlah tank minimum = ceil(waktu proses / target cycle time)
```

Contoh:

```text
Semibright Nickel = 60 menit
Target cycle time = 20 menit / Rack Hanger

Jumlah tank minimum = ceil(60 / 20)
Jumlah tank minimum = 3 tank
```

Jika existing tank hanya 1, maka tambahan tank yang direkomendasikan adalah:

```text
3 - 1 = 2 tank tambahan
```

### 3. Dynamic Flow Process

Jumlah tank aktual pada flow process akan berubah otomatis mengikuti rekomendasi tank tambahan.

Contoh:

```text
Existing tank = 29 tank
Tambahan Semibright Nickel = 2 tank
Tambahan Bright Nickel = 1 tank

Total tank aktual = 32 tank
```

Total waktu transfer juga otomatis berubah mengikuti jumlah tank aktual.

```text
Total transfer = (total tank aktual - 1) × waktu transfer antar tank
```

### 4. Rack Hanger Output

Satuan output utama adalah:

```text
Rack Hanger
```

User dapat memasukkan jumlah produk per Rack Hanger sehingga sistem dapat menghitung:

```text
Output produk / jam = Rack Hanger per jam × jumlah produk per Rack Hanger
```

### 5. Visual Rack Flow Simulation

Simulator menyediakan visual flow Rack Hanger agar user dapat melihat:

* Rack masuk ke tank.
* Rack sedang diproses.
* Rack menunggu tank berikutnya.
* Rack berpindah antar tank.
* Pengaruh penambahan tank paralel terhadap cycle time.
* Total Rack Hanger yang sudah selesai.

### 6. Robot Area

Sistem menggunakan 2 robot:

```text
Robot 1 : Tank 1 sampai Tank 14
Robot 2 : Tank 14 sampai Tank 29
```

Tank 14 menjadi area handover antara Robot 1 dan Robot 2.

## Process Data

Flow process dasar terdiri dari 29 tank:

| Tank No | Process             | Chemical               | Dipping Time | Temp | Robot |
| ------- | ------------------- | ---------------------- | ------------ | ---- | ----- |
| 1       | Loading             | -                      | 0 min        | -    | 1     |
| 2       | Soak clean          | EPINION SERIES         | 20 min       | 50 C | 1     |
| 3       | Electro degreasing  | EPINION SERIES         | 5 min        | 50 C | 1     |
| 4       | Water rinse         | Tap water              | 5 min        | -    | 1     |
| 5       | Water rinse         | Tap water              | 5 min        | -    | 1     |
| 6       | Acid pickling       | HCl                    | 20 min       | RT   | 1     |
| 7       | Water rinse         | Tap water              | 5 min        | -    | 1     |
| 8       | Water rinse         | Tap water              | 5 min        | -    | 1     |
| 9       | Electro clean       | EPINION SERIES         | 10 min       | 40 C | 1     |
| 10      | Water rinse         | Tap water              | 5 min        | -    | 1     |
| 11      | Water rinse         | Tap water              | 5 min        | -    | 1     |
| 12      | Activation          | epiclen P12 (Dry Salt) | 1 min        | RT   | 1     |
| 13      | Water rinse         | Tap water              | 5 min        | -    | 1     |
| 14      | Semibright Nickel   | SFN-206                | 60 min       | 55 C | 1 & 2 |
| 15      | High Sulfur Nickel  | HS 303                 | 10 min       | 55 C | 2     |
| 16      | Bright Nickel       | EPUNION Nitech/BNP     | 40 min       | 55 C | 2     |
| 17      | Micro Porous Nickel | Water                  | 10 min       | -    | 2     |
| 18      | Water rinse         | Tap water              | 5 min        | -    | 2     |
| 19      | Water rinse         | Tap water              | 5 min        | -    | 2     |
| 20      | Water rinse         | Tap water              | 5 min        | -    | 2     |
| 21      | Water rinse         | Tap water              | 5 min        | -    | 2     |
| 22      | Water rinse         | RO Water               | 5 min        | -    | 2     |
| 23      | Water rinse         | RO Water               | 5 min        | -    | 2     |
| 24      | Passivation         | Cr6/Chrome free        | 5 min        | -    | 2     |
| 25      | Water rinse         | -                      | 5 min        | -    | 2     |
| 26      | Water rinse         | -                      | 5 min        | -    | 2     |
| 27      | Water rinse         | -                      | 5 min        | -    | 2     |
| 28      | Drying              | -                      | 5 min        | -    | 2     |
| 29      | Unloading           | -                      | 0 min        | -    | 2     |

## Default Parameters

| Parameter                |          Default Value |
| ------------------------ | ---------------------: |
| Target cycle time output | 20 menit / Rack Hanger |
| Transfer time antar tank |               10 detik |
| Produk per Rack Hanger   |              50 produk |
| Rack simulasi visual     |          8 Rack Hanger |
| Jumlah robot             |                2 robot |

## Calculation Example

Jika target cycle time adalah:

```text
20 menit / Rack Hanger
```

Maka rekomendasi tank:

| Process             |   Time | Tank Minimum | Additional Tank |
| ------------------- | -----: | -----------: | --------------: |
| Semibright Nickel   | 60 min |            3 |               2 |
| High Sulfur Nickel  | 10 min |            1 |               0 |
| Bright Nickel       | 40 min |            2 |               1 |
| Micro Porous Nickel | 10 min |            1 |               0 |

Total tambahan:

```text
3 tank tambahan
```

Total tank aktual:

```text
29 + 3 = 32 tank
```

Total transfer:

```text
(32 - 1) × 10 detik = 310 detik
310 detik = 5 menit 10 detik
```

Jika 1 Rack Hanger berisi 50 produk:

```text
Output Rack Hanger / jam = 60 / 20 = 3 Rack Hanger / jam

Output produk / jam = 3 × 50 = 150 produk / jam
```

## How to Run

Aplikasi ini dibuat menggunakan:

* HTML
* CSS
* JavaScript

Tidak membutuhkan backend atau database.

### Cara menjalankan

1. Clone repository:

```bash
git clone https://github.com/USERNAME/nickel-chrome-plating-simulator.git
```

2. Masuk ke folder project:

```bash
cd nickel-chrome-plating-simulator
```

3. Buka file:

```text
index.html
```

di browser.

Atau jalankan menggunakan Live Server di Visual Studio Code.

## Suggested Project Structure

```text
nickel-chrome-plating-simulator/
├── index.html
├── README.md
└── assets/
    └── images/
```

## Future Development

Beberapa pengembangan yang dapat ditambahkan:

* Simulasi konflik pergerakan Robot 1 dan Robot 2.
* Perhitungan kapasitas berdasarkan shift kerja.
* Export hasil simulasi ke PDF.
* Export hasil simulasi ke Excel.
* Grafik bottleneck proses.
* Grafik output per jam.
* Mode comparison sebelum dan sesudah penambahan tank.
* Database parameter proses.
* Login user dan role operator/engineer.
* Integrasi dashboard produksi.

## Notes

Simulator ini merupakan alat bantu perhitungan dan visualisasi awal.
Untuk implementasi aktual di lapangan, hasil simulasi tetap perlu divalidasi terhadap:

* layout fisik line plating,
* kapasitas robot,
* waktu aktual transfer,
* waktu loading dan unloading,
* jumlah rack aktual,
* safety factor proses,
* kondisi chemical,
* kapasitas rectifier,
* kapasitas tank,
* dan kondisi operasional produksi.

## Copyright

Copyright © 2026
**Automation Team - PT. Garuda Metalindo, Tbk,**

All rights reserved.
