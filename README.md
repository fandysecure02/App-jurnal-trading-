# 📈 SniperLog - Jurnal Trading Scalper

Aplikasi Flutter Android untuk mencatat dan menganalisis trade scalping secara offline.

---

## 🗂️ Struktur File

```
lib/
├── main.dart                    # Entry point + navigasi utama
├── models/
│   └── trade.dart               # Model data Trade
├── helpers/
│   └── database_helper.dart     # SQLite CRUD helper
├── providers/
│   └── trade_provider.dart      # State management + logika kalkulasi
├── screens/
│   ├── input_trade_screen.dart  # Halaman input trade baru
│   ├── dashboard_screen.dart    # Halaman analytics & list trade
│   └── trade_detail_screen.dart # Halaman detail + gambar penuh
└── theme/
    └── app_theme.dart           # Dark theme + konstanta warna
```

---

## 🚀 Cara Setup & Jalankan

### 1. Install dependencies
```bash
flutter pub get
```

### 2. Jalankan di emulator/device
```bash
flutter run
```

### 3. Build APK release
```bash
flutter build apk --release
```
APK tersimpan di: `build/app/outputs/flutter-apk/app-release.apk`

---

## 📦 Packages yang Digunakan

| Package | Versi | Fungsi |
|---------|-------|--------|
| `provider` | ^6.1.1 | State management |
| `sqflite` | ^2.3.0 | Database SQLite lokal |
| `path` | ^1.9.0 | Manipulasi path file |
| `shared_preferences` | ^2.2.2 | Simpan balance awal |
| `image_picker` | ^1.0.7 | Kamera & galeri |
| `path_provider` | ^2.1.1 | Folder dokumen app |
| `share_plus` | ^7.2.1 | Export & share CSV |
| `google_fonts` | ^6.1.0 | Font Poppins |
| `intl` | ^0.19.0 | Format tanggal |

Semua package **gratis** dan open source.

---

## ⚙️ Konfigurasi Penting

### Ubah Multiplier P/L
Di file `lib/providers/trade_provider.dart`:
```dart
// Cari baris ini:
const double multiplierPerLotPerPip = 10.0;
// Ubah sesuai pair masing-masing kalau perlu
```

### Tambah Pair Default
Di file `lib/screens/input_trade_screen.dart`:
```dart
final List<String> _pairs = ['XAUUSD', 'EURUSD', 'GBPUSD', 'USDJPY'];
// Tambah pair di sini
```

---

## 📱 Izin Android yang Diperlukan

- `CAMERA` - Ambil screenshot dari kamera
- `READ_MEDIA_IMAGES` - Pilih gambar dari galeri (Android 13+)
- `READ_EXTERNAL_STORAGE` - Pilih gambar dari galeri (Android ≤12)
- `INTERNET` - Load font Google Fonts

---

## 🎨 Warna Tema

| Nama | Hex | Kegunaan |
|------|-----|----------|
| Background | `#121212` | Background utama |
| Surface | `#1E1E1E` | Background card |
| Accent Blue | `#2196F3` | Tombol, highlight |
| Win Green | `#4CAF50` | Warna WIN / profit |
| Loss Red | `#F44336` | Warna LOSS / rugi |
| BE Gray | `#9E9E9E` | Warna Breakeven |
| Loss Streak Bg | `#2B1B1B` | Background card loss streak |
| Win Streak Bg | `#1B2B1B` | Background card win streak |

---

## 💡 Tips Penggunaan

1. **Set Balance Awal**: Tap icon edit di card "Balance Awal" saat pertama pakai
2. **Auto Hitung Pips**: Isi Entry, SL/TP, pilih Hasil → pips terhitung otomatis
3. **Tambah Pair Custom**: Tap tombol `+` di samping dropdown pair
4. **Export Data**: Tap ikon upload di halaman Dashboard
5. **Reset Data**: Tap ⋮ (tiga titik) → "Reset Semua Data"
6. **Refresh Dashboard**: Tarik ke bawah untuk refresh data

---

## 🔢 Formula Kalkulasi

### P/L
```
P/L = Pips × Lot Size × 10
Contoh: +20 pips × 0.10 lot × 10 = $20
```

### Max Drawdown
```
Peak = equity tertinggi sejak awal
Drawdown = Peak - Equity saat itu
Max DD = nilai Drawdown tertinggi yang pernah terjadi
```

### Consecutive Streak
```
Loop semua trade urut waktu:
- Kalau WIN: increment winStreak, reset lossStreak
- Kalau LOSS: increment lossStreak, reset winStreak  
- Kalau BE: reset kedua streak
```
