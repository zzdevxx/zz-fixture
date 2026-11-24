# zz-fixture: Stage Lighting Fixture Definitions

Koleksi profil definisi fixture lampu panggung (`.qxf`) untuk QLC+ (Q Light Controller Plus v4.14.4+) dan konsol pencahayaan ZZLUXORA v10.
Dirancang, diuji, dan dipelihara oleh Andreas Restuawanta Christwara (`zzdevxx`) untuk riset pencahayaan panggung dan tata ibadah Gereja Isa Almasih (GIA) Deliksari Semarang.

[![Format](https://img.shields.io/badge/Format-QLC%2B%20.qxf-blue?style=flat-square)](https://www.qlcplus.org)
[![License](https://img.shields.io/badge/License-MIT-green?style=flat-square)](LICENSE)
[![Compatibility](https://img.shields.io/badge/Compatibility-QLC%2B%20v4.14.4%20%7C%20v5%20%7C%20ZZLUXORA%20v10-orange?style=flat-square)](https://gitlab.com/zzdevxx/zzluxora-v10)
[![Research](https://img.shields.io/badge/Research-Skripsi%20FT%20UNNES-red?style=flat-square)](https://gitlab.com/zzdevxx/zzluxora-thesis)

---

## Rig Panggung Aktif (Active Stage Rig)

Konfigurasi panggung aktif saat ini menggunakan **4 unit `zzdree 36X`** (`zzdree-36X.qxf`) dalam mode 3 kanal RGB murni (36 W per unit, konektor DMX XLR 3-pin) yang dirangkai secara *daisy-chain* ke node ESP32 Art-Net to DMX512 dengan interval alamat 16 kanal:

| Unit | Fixture | Mode | Alamat DMX Awal | Rentang Kanal Aktif | Daya |
| :---: | :--- | :---: | :---: | :---: | :---: |
| 1 | `zzdree 36X` | 3CH RGB | `001` | Ch 1 - 3 (R, G, B) | 36 W |
| 2 | `zzdree 36X` | 3CH RGB | `017` | Ch 17 - 19 (R, G, B) | 36 W |
| 3 | `zzdree 36X` | 3CH RGB | `033` | Ch 33 - 35 (R, G, B) | 36 W |
| 4 | `zzdree 36X` | 3CH RGB | `049` | Ch 49 - 51 (R, G, B) | 36 W |

---

## Katalog Fixture (5 Profil `.qxf`)

Seluruh berkas definisi menggunakan skema XML QLC+ `FixtureDefinition` (Creator: Q Light Controller Plus `4.14.4`, Author: `zzdree_`, Type: `Color Changer`, Bulb: `LED`, Connector: `3-pin`).

| Berkas | Pabrikan | Model | Kanal | Sistem Warna | Daya | Status / Peran |
| :--- | :--- | :--- | :---: | :--- | :---: | :--- |
| `zzdree-36X.qxf` | `zzdree` | `36X` | 3 CH | RGB (Direct 3CH) | 36 W | **Rig Panggung Aktif (4 unit, DMX 001/017/033/049)** |
| `Alien-AL36.qxf` | `Alien` | `AL36` | 8 CH | RGB + Dimmer + Macro | 36 W | Katalog / Profil PAR 36W 8CH |
| `Illumsolid-YSP01.qxf` | `Illumsolid` | `YSP01` | 8 CH | RGBW + Dimmer + Macro | 30 W | Katalog / Profil PAR RGBW 30W |
| `Kumastb-STL47.qxf` | `Kumastb` | `STL47` | 8 CH | RGBW + Dimmer + Strobe + Macro | 12 W | Katalog / Unit Bench Test RGBW |
| `Wisdom-54X3.qxf` | `Wisdom` | `54X3` | 8 CH | RGB + Dimmer + Strobe + Effect | 162 W | Katalog / Profil High-Power PAR 162W |

---

## Spesifikasi dan Pemetaan Kanal DMX

### 1. zzdree 36X (`zzdree-36X.qxf`) [Rig Panggung Aktif]

- **Pabrikan / Model:** `zzdree` / `36X`
- **Tipe / Mode:** `Color Changer` / `Modes` (3 Channels)
- **Konsumsi Daya:** 36 W, LED, konektor DMX 3-pin
- **Karakteristik:** Kontrol RGB langsung tanpa kanal Master Dimmer terpisah. Intensitas diatur langsung melalui nilai R, G, B menggunakan preset QLC+ (`IntensityRed`, `IntensityGreen`, `IntensityBlue`).
- **Alokasi Panggung Aktif:** 4 unit pada alamat DMX `001`, `017`, `033`, dan `049`.

| QLC+ Index | DMX Channel | Nama Kanal | Preset / Grup XML | Rentang Nilai | Fungsi |
| :---: | :---: | :--- | :--- | :---: | :--- |
| 0 | Ch 1 | `Red` | `Preset="IntensityRed"` | `0 - 255` | Intensitas LED Merah |
| 1 | Ch 2 | `Green` | `Preset="IntensityGreen"` | `0 - 255` | Intensitas LED Hijau |
| 2 | Ch 3 | `Blue` | `Preset="IntensityBlue"` | `0 - 255` | Intensitas LED Biru |

---

### 2. Alien AL36 (`Alien-AL36.qxf`)

- **Pabrikan / Model:** `Alien` / `AL36`
- **Tipe / Mode:** `Color Changer` / `Modes` (8 Channels)
- **Konsumsi Daya:** 36 W, LED, konektor DMX 3-pin
- **Karakteristik:** PAR LED 36W mode 8 kanal dengan Master Dimmer, RGB murni (tanpa kanal White), serta program makro internal dan pengatur kecepatan.

| QLC+ Index | DMX Channel | Nama Kanal | Grup / Warna XML | Rentang Nilai | Fungsi |
| :---: | :---: | :--- | :--- | :---: | :--- |
| 0 | Ch 1 | `Dimmer` | `Intensity` | `0 - 255` | Master dimmer linear (0% - 100%) |
| 1 | Ch 2 | `Red` | `Intensity` / `Red` | `0 - 255` | Intensitas LED Merah |
| 2 | Ch 3 | `Green` | `Intensity` / `Green` | `0 - 255` | Intensitas LED Hijau |
| 3 | Ch 4 | `Blue` | `Intensity` / `Blue` | `0 - 255` | Intensitas LED Biru |
| 4 | Ch 5 | `Empty` | `Nothing` | `0 - 255` | Kanal kosong / tidak terhubung |
| 5 | Ch 6 | `Program` | `Effect` | `0 - 255` | Pola program makro bawaan |
| 6 | Ch 7 | `Speed` | `Speed` | `0 - 255` | Kecepatan program makro Ch 6 |
| 7 | Ch 8 | `Emptz` | `Nothing` | `0 - 255` | Kanal cadangan / tidak terhubung |

---

### 3. Illumsolid YSP01 (`Illumsolid-YSP01.qxf`)

- **Pabrikan / Model:** `Illumsolid` / `YSP01`
- **Tipe / Mode:** `Color Changer` / `Modes` (8 Channels)
- **Konsumsi Daya:** 30 W, LED, konektor DMX 3-pin
- **Karakteristik:** Fixture RGBW 30W mode 8 kanal dengan kanal White fisik di Ch 5 dan Program makro di Ch 6. Kanal 7 dan 8 tidak terpakai (`Nothing`).

| QLC+ Index | DMX Channel | Nama Kanal | Grup / Warna XML | Rentang Nilai | Fungsi |
| :---: | :---: | :--- | :--- | :---: | :--- |
| 0 | Ch 1 | `Dimmer` | `Intensity` | `0 - 255` | Master dimmer (0% - 100%) |
| 1 | Ch 2 | `Red` | `Intensity` / `Red` | `0 - 255` | Intensitas LED Merah |
| 2 | Ch 3 | `Green` | `Intensity` / `Green` | `0 - 255` | Intensitas LED Hijau |
| 3 | Ch 4 | `Blue` | `Intensity` / `Blue` | `0 - 255` | Intensitas LED Biru |
| 4 | Ch 5 | `White` | `Intensity` / `White` | `0 - 255` | Intensitas LED Putih fisik |
| 5 | Ch 6 | `Program` | `Effect` | `0 - 255` | Pola program makro bawaan |
| 6 | Ch 7 | `Empty` | `Nothing` | `0 - 255` | Kanal kosong / tidak terhubung |
| 7 | Ch 8 | `Emptz` | `Nothing` | `0 - 255` | Kanal cadangan / tidak terhubung |

---

### 4. Kumastb STL47 (`Kumastb-STL47.qxf`)

- **Pabrikan / Model:** `Kumastb` / `STL47`
- **Tipe / Mode:** `Color Changer` / `Modes` (8 Channels)
- **Konsumsi Daya:** 12 W, LED, konektor DMX 3-pin
- **Karakteristik:** Mini PAR LED 12W RGBW yang digunakan sebagai unit uji laboratorium (*bench testing*) untuk memvalidasi algoritma dekomposisi 4-kanal RGBW pada ZZLUXORA v10:

$$\begin{aligned}
W &= \min(R, G, B) \\
R' &= R - W \\
G' &= G - W \\
B' &= B - W
\end{aligned}$$

| QLC+ Index | DMX Channel | Nama Kanal | Grup / Warna XML | Rentang Nilai | Fungsi |
| :---: | :---: | :--- | :--- | :---: | :--- |
| 0 | Ch 1 | `Dimmer` | `Intensity` | `0 - 255` | Master dimmer (0% - 100%) |
| 1 | Ch 2 | `Red` | `Intensity` / `Red` | `0 - 255` | Intensitas LED Merah |
| 2 | Ch 3 | `Green` | `Intensity` / `Green` | `0 - 255` | Intensitas LED Hijau |
| 3 | Ch 4 | `Blue` | `Intensity` / `Blue` | `0 - 255` | Intensitas LED Biru |
| 4 | Ch 5 | `White` | `Intensity` / `White` | `0 - 255` | Intensitas LED Putih fisik (target RGBW) |
| 5 | Ch 6 | `Strobe` | `Shutter` | `0 - 255` | Efek kedip strobo fisik |
| 6 | Ch 7 | `Program` | `Effect` | `0 - 255` | Mode otomatis dan makro warna bawaan |
| 7 | Ch 8 | `Speed` | `Speed` | `0 - 255` | Kecepatan eksekusi program Ch 7 |

---

### 5. Wisdom 54X3 (`Wisdom-54X3.qxf`)

- **Pabrikan / Model:** `Wisdom` / `54X3`
- **Tipe / Mode:** `Color Changer` / `Modes` (8 Channels)
- **Konsumsi Daya:** 162 W (54 x 3W), LED, konektor DMX 3-pin
- **Karakteristik:** Fixture PAR LED daya tinggi 162W mode 8 kanal. Berbeda dengan profil 8CH lain di katalog ini, kanal warna RGB berada pada Ch 5, Ch 6, dan Ch 7 (setelah Dimmer, Strobe, Effect, dan Speed).

| QLC+ Index | DMX Channel | Nama Kanal | Grup / Warna XML | Rentang Nilai | Fungsi |
| :---: | :---: | :--- | :--- | :---: | :--- |
| 0 | Ch 1 | `Dimmer` | `Intensity` | `0 - 255` | Master dimmer (0% - 100%) |
| 1 | Ch 2 | `Strobe` | `Shutter` | `0 - 255` | Efek kedip strobo fisik |
| 2 | Ch 3 | `Effect` | `Effect` | `0 - 255` | Efek / makro internal fixture |
| 3 | Ch 4 | `Speed` | `Speed` | `0 - 255` | Kecepatan efek Ch 3 |
| 4 | Ch 5 | `Red` | `Intensity` / `Red` | `0 - 255` | Intensitas LED Merah |
| 5 | Ch 6 | `Green` | `Intensity` / `Green` | `0 - 255` | Intensitas LED Hijau |
| 6 | Ch 7 | `Blue` | `Intensity` / `Blue` | `0 - 255` | Intensitas LED Biru |
| 7 | Ch 8 | `Empty` | `Nothing` | `0 - 255` | Kanal kosong / tidak terhubung |

---

## Panduan Instalasi dan Penggunaan

### 1. Pemasangan Profil ke QLC+

**Windows 10/11:**
Salin seluruh berkas `.qxf` ke direktori fixture pengguna QLC+:

```powershell
Copy-Item *.qxf "$env:USERPROFILE\QLC+\Fixtures\"
```

Atau ke direktori instalasi global `C:\Program Files\QLC+\Fixtures\`.

**Linux (Ubuntu / Debian / Mint):**

```bash
mkdir -p ~/.qlcplus/fixtures/
cp Alien-AL36.qxf Illumsolid-YSP01.qxf Kumastb-STL47.qxf Wisdom-54X3.qxf zzdree-36X.qxf ~/.qlcplus/fixtures/
```

### 2. Memuat Fixture di QLC+

1. Buka aplikasi QLC+ (`v4.14.4` atau `v5`).
2. Buka tab **Fixtures**, lalu klik **Add Fixtures (+)**.
3. Pilih pabrikan dan model sesuai kebutuhan:
   - `zzdree` -> `36X` (rig panggung aktif: 4 unit pada alamat DMX `001`, `017`, `033`, `049`).
   - `Alien` -> `AL36` (8CH RGB, 36 W).
   - `Illumsolid` -> `YSP01` (8CH RGBW, 30 W).
   - `Kumastb` -> `STL47` (8CH RGBW, 12 W, bench testing).
   - `Wisdom` -> `54X3` (8CH RGB, 162 W).
4. Tentukan Universe (Universe 0 atau 1) dan alamat DMX awal.

### 3. Integrasi ke ZZLUXORA v10

- Profil `.qxf` kompatibel dengan parser `core/project_io.py` dan editor `ui/panels/fixture_editor.py` pada konsol ZZLUXORA v10.
- Berkas `.qxf` dapat dikonversi ke format JSON `.zfx` untuk patching kanal DMX pada konsol.

---

## Lisensi

Proyek ini dirilis di bawah [MIT License](LICENSE). Pengembang, operator pencahayaan, dan gereja bebas mengunduh, menggunakan, dan memodifikasi profil fixture ini.
