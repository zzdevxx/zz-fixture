# CLAUDE.md: zz-fixture Technical Directive & Fixture Profiling Guide

Dokumen ini menjadi sumber kebenaran operasional untuk Claude Code, agen AI, dan pengembang dalam memetakan, memvalidasi, dan mengintegrasikan profil lampu panggung `zz-fixture` ke dalam ekosistem riset skripsi dan konsol ZZLUXORA v10.

---

## 1. Identitas dan Ruang Lingkup Proyek

- **Nama Proyek:** `zz-fixture` (Stage Lighting Fixture Definitions)
- **Remote Sinkronisasi (Triple Cloud):**
  - GitLab (`origin`): `https://gitlab.com/zzdevxx/zz-fixture.git`
  - Codeberg (`codeberg`): `https://codeberg.org/zzdevxx/zz-fixture.git`
  - GitHub (`github`): `https://github.com/zzdevxx/zz-fixture.git`
- **Peneliti / Pengembang:** Andreas Restuawanta Christwara (`NIM: 5312422036`)
- **Institusi:** Program Studi S1 Teknik Komputer, Fakultas Teknik, Universitas Negeri Semarang (UNNES)
- **Format Berkas Sumber:** XML QLC+ `FixtureDefinition` (`.qxf`, dibuat dengan QLC+ `v4.14.4`, author `zzdree_`)
- **Format Target Konsol:** JSON ZZLUXORA Fixture Definition (`.zfx`)
- **Total Profil di Katalog:** 5 berkas `.qxf` (`zzdree-36X.qxf`, `Alien-AL36.qxf`, `Illumsolid-YSP01.qxf`, `Kumastb-STL47.qxf`, `Wisdom-54X3.qxf`)

---

## 2. Konfigurasi Rig Panggung Aktif (Active Stage Rig)

Rig panggung aktif di GIA Deliksari Semarang menggunakan **4 unit `zzdree 36X`** (`zzdree-36X.qxf`) yang dirangkai secara *daisy-chain* RS-485 (XLR 3-pin) menuju node hardware ESP32 Art-Net to DMX512 (`esp32-artnet-dmx`):

- **Model Aktif:** `zzdree 36X` (3CH RGB murni, 36 W per unit, tanpa kanal Master Dimmer terpisah).
- **Skema Addressing (16-channel stride):**
  - Unit 1: DMX `001` (Ch 1 = R, Ch 2 = G, Ch 3 = B)
  - Unit 2: DMX `017` (Ch 17 = R, Ch 18 = G, Ch 19 = B)
  - Unit 3: DMX `033` (Ch 33 = R, Ch 34 = G, Ch 35 = B)
  - Unit 4: DMX `049` (Ch 49 = R, Ch 50 = G, Ch 51 = B)
- **Implikasi Kontrol Software:** Karena tidak ada kanal Master Dimmer terpisah, skala kecerahan master harus diterapkan secara perangkat lunak langsung pada kanal R, G, dan B sebelum paket Art-Net DMX dikirim.

---

## 3. Spesifikasi Teknis Lengkap (5 Fixture Katalog)

Seluruh spesifikasi di bawah ini diambil langsung dari tag XML `<Manufacturer>`, `<Model>`, `<Channel>`, `<Mode>`, dan `<Physical>` pada masing-masing berkas `.qxf`.

### A. zzdree 36X (`zzdree-36X.qxf`) [Rig Panggung Aktif]

- **Pabrikan & Model:** `zzdree` / `36X`
- **Tipe & Mode:** `Color Changer` / `Modes` (3 Channels)
- **Fisik:** Bulb `LED`, Dimensions `750 x 750 x 100 mm`, Power `36 W`, DMX `3-pin`
- **Emisi Warna:** RGB murni (3 kanal langsung via QLC+ Preset)
- **Status:** Rig panggung aktif (4 unit, DMX `001`, `017`, `033`, `049`).
- **Pemetaan Kanal DMX (3-Channel Mode):**
  ```text
  Ch 1 [Offset 0]: Red   (Preset="IntensityRed", 0-255)
  Ch 2 [Offset 1]: Green (Preset="IntensityGreen", 0-255)
  Ch 3 [Offset 2]: Blue  (Preset="IntensityBlue", 0-255)
  ```

### B. Alien AL36 (`Alien-AL36.qxf`)

- **Pabrikan & Model:** `Alien` / `AL36`
- **Tipe & Mode:** `Color Changer` / `Modes` (8 Channels)
- **Fisik:** Bulb `LED`, Dimensions `750 x 750 x 100 mm`, Power `36 W`, DMX `3-pin`
- **Emisi Warna:** RGB aditif (tidak memiliki kanal White fisik; Ch 5 adalah `Empty`)
- **Status:** Katalog fixture (profil 8CH PAR 36W).
- **Pemetaan Kanal DMX (8-Channel Mode):**
  ```text
  Ch 1 [Offset 0]: Dimmer  (Intensity, 0-255)
  Ch 2 [Offset 1]: Red     (Intensity/Red, 0-255)
  Ch 3 [Offset 2]: Green   (Intensity/Green, 0-255)
  Ch 4 [Offset 3]: Blue    (Intensity/Blue, 0-255)
  Ch 5 [Offset 4]: Empty   (Nothing, 0-255)
  Ch 6 [Offset 5]: Program (Effect, 0-255)
  Ch 7 [Offset 6]: Speed   (Speed, 0-255)
  Ch 8 [Offset 7]: Emptz   (Nothing, 0-255)
  ```

### C. Illumsolid YSP01 (`Illumsolid-YSP01.qxf`)

- **Pabrikan & Model:** `Illumsolid` / `YSP01`
- **Tipe & Mode:** `Color Changer` / `Modes` (8 Channels)
- **Fisik:** Bulb `LED`, Dimensions `750 x 750 x 100 mm`, Power `30 W`, DMX `3-pin`
- **Emisi Warna:** Physical 4-Kanal RGBW (memiliki kanal White di Ch 5; tanpa kanal Strobe/Speed terpisah)
- **Status:** Katalog fixture (profil 8CH PAR RGBW 30W).
- **Pemetaan Kanal DMX (8-Channel Mode):**
  ```text
  Ch 1 [Offset 0]: Dimmer  (Intensity, 0-255)
  Ch 2 [Offset 1]: Red     (Intensity/Red, 0-255)
  Ch 3 [Offset 2]: Green   (Intensity/Green, 0-255)
  Ch 4 [Offset 3]: Blue    (Intensity/Blue, 0-255)
  Ch 5 [Offset 4]: White   (Intensity/White, 0-255)
  Ch 6 [Offset 5]: Program (Effect, 0-255)
  Ch 7 [Offset 6]: Empty   (Nothing, 0-255)
  Ch 8 [Offset 7]: Emptz   (Nothing, 0-255)
  ```

### D. Kumastb STL47 (`Kumastb-STL47.qxf`)

- **Pabrikan & Model:** `Kumastb` / `STL47`
- **Tipe & Mode:** `Color Changer` / `Modes` (8 Channels)
- **Fisik:** Bulb `LED`, Dimensions `750 x 750 x 100 mm`, Power `12 W`, DMX `3-pin`
- **Emisi Warna:** Physical 4-Kanal RGBW (Red, Green, Blue, dan Dedicated Pure White)
- **Status:** Katalog fixture dan unit uji laboratorium (*bench testing*) untuk validasi dekomposisi RGBW pada `core/color_engine.py` ZZLUXORA v10:
  $$W = \min(R, G, B)$$
  $$R' = R - W, \quad G' = G - W, \quad B' = B - W$$
- **Pemetaan Kanal DMX (8-Channel Mode):**
  ```text
  Ch 1 [Offset 0]: Dimmer  (Intensity, 0-255)
  Ch 2 [Offset 1]: Red     (Intensity/Red, 0-255)
  Ch 3 [Offset 2]: Green   (Intensity/Green, 0-255)
  Ch 4 [Offset 3]: Blue    (Intensity/Blue, 0-255)
  Ch 5 [Offset 4]: White   (Intensity/White, 0-255) -> Target Dekomposisi Physical RGBW
  Ch 6 [Offset 5]: Strobe  (Shutter, 0-255)
  Ch 7 [Offset 6]: Program (Effect, 0-255)
  Ch 8 [Offset 7]: Speed   (Speed, 0-255)
  ```

### E. Wisdom 54X3 (`Wisdom-54X3.qxf`)

- **Pabrikan & Model:** `Wisdom` / `54X3`
- **Tipe & Mode:** `Color Changer` / `Modes` (8 Channels)
- **Fisik:** Bulb `LED`, Dimensions `750 x 750 x 100 mm`, Power `162 W`, DMX `3-pin`
- **Emisi Warna:** RGB aditif (tanpa kanal White fisik; urutan RGB berada di Ch 5-7, bukan Ch 2-4)
- **Status:** Katalog fixture (profil 8CH High-Power PAR 162W).
- **Pemetaan Kanal DMX (8-Channel Mode):**
  ```text
  Ch 1 [Offset 0]: Dimmer (Intensity, 0-255)
  Ch 2 [Offset 1]: Strobe (Shutter, 0-255)
  Ch 3 [Offset 2]: Effect (Effect, 0-255)
  Ch 4 [Offset 3]: Speed  (Speed, 0-255)
  Ch 5 [Offset 4]: Red    (Intensity/Red, 0-255)
  Ch 6 [Offset 5]: Green  (Intensity/Green, 0-255)
  Ch 7 [Offset 6]: Blue   (Intensity/Blue, 0-255)
  Ch 8 [Offset 7]: Empty  (Nothing, 0-255)
  ```

---

## 4. Pedoman Teknis untuk Agen AI dan Pengembang

1. **Jangan Mengasumsikan Layout Kanal Seragam:**
   - `zzdree-36X` adalah **3CH RGB** tanpa Master Dimmer (`Offset 0=RED, 1=GRN, 2=BLU`).
   - `Alien-AL36` adalah **8CH RGB** dengan `DIM` di Offset 0 dan `Empty` di Offset 4.
   - `Illumsolid-YSP01` adalah **8CH RGBW** dengan `WHT` di Offset 4, `Program` di Offset 5, dan tanpa `Strobe`/`Speed`.
   - `Kumastb-STL47` adalah **8CH RGBW** dengan `WHT` di Offset 4, `STR` di Offset 5, `Program` di Offset 6, `Speed` di Offset 7.
   - `Wisdom-54X3` adalah **8CH RGB** dengan `STR`/`Effect`/`Speed` di Offset 1-3 dan `RED`/`GRN`/`BLU` bergeser ke Offset 4-6.
2. **Kode Singkatan Kanal Tab Address ZZLUXORA:**
   - `DIM` = Master Dimmer (Amber/Yellow)
   - `RED` = Red Intensity (Pure Red)
   - `GRN` = Green Intensity (Pure Green)
   - `BLU` = Blue Intensity (Pure Blue)
   - `WHT` = White Intensity (Pure White; hanya aktif pada `Illumsolid-YSP01` dan `Kumastb-STL47`)
   - `STR` = Strobe / Shutter (Cyan/Purple; aktif pada `Kumastb-STL47` dan `Wisdom-54X3`)
3. **Pengujian Loopback / SITL QLC+:**
   - Gunakan template workspace di `D:\ANDREAS\PERSONAL\zzluxora\showfiles\qlcplus_template.qxw` (atau proyek `.qxw` uji lokal).
   - Arahkan output Art-Net ke `127.0.0.1:6454` (Universe 0/1) dengan mode Passthrough aktif di QLC+.
4. **Standar Ekstensi Berkas:**
   - Profil QLC+: `.qxf` (XML)
   - Profil fixture ZZLUXORA: `.zfx` (JSON)
   - Showfile proyek panggung: `.zlx` (JSON terkompresi)
5. **Validasi XML Sebelum Commit:**
   - Setiap penambahan atau perubahan berkas `.qxf` wajib lolos parsing `xml.etree.ElementTree.parse()` tanpa error dan tabel kanal pada `README.md` serta `CLAUDE.md` harus cocok dengan isi XML.
