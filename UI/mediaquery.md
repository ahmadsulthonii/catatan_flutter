# Flutter MediaQuery Notes

Catatan pribadi tentang **MediaQuery di Flutter** untuk membuat UI yang responsif di berbagai ukuran layar dan perangkat.

---

## 1. Apa itu MediaQuery?

**MediaQuery** adalah class di Flutter yang digunakan untuk mendapatkan informasi tentang **ukuran layar dan karakteristik perangkat** tempat aplikasi dijalankan.

MediaQuery sangat penting untuk:
- Membuat UI **responsif**
- Menyesuaikan layout berdasarkan **ukuran layar**
- Menghindari masalah **notch, status bar, dan navigation bar**

Singkatnya:
> MediaQuery membantu Flutter menyesuaikan tampilan UI dengan device pengguna.

---

## 2. Cara Mengakses MediaQuery

```dart
final mediaQuery = MediaQuery.of(context);

Catatan penting:
MediaQuery tidak boleh dipanggil di initState()
Gunakan di build() atau didChangeDependencies()
```

## 3. Mengambil Ukuran Layar

```dart
final size = MediaQuery.of(context).size;
final screenWidth = size.width;
final screenHeight = size.height;
```

Digunakan untuk:

UI responsif

Menghindari ukuran hardcode

## 4. Mengetahui Orientasi Layar
``` dart
final orientation = MediaQuery.of(context).orientation;

if (orientation == Orientation.portrait) {
  // Layout portrait
} else {
  // Layout landscape
}
```

Orientasi:

- ``` Orientation.portrait```
- ``` Orientation.landscape```

## 5. Safe Area (Notch, Status Bar, Navigation Bar)
```dart
final padding = MediaQuery.of(context).padding;

final statusBarHeight = padding.top;
final bottomSafeArea = padding.bottom;
```

Contoh penggunaan:
```dart
Padding(
  padding: EdgeInsets.only(top: statusBarHeight),
  child: Widget(),
)
```

## 6. Text Scale Factor (Ukuran Teks Sistem)
```
final textScale = MediaQuery.of(context).textScaleFactor;
```

Digunakan untuk:

- Aksesibilitas
- Menyesuaikan ukuran teks sesuai pengaturan sistem

## 7. Dark Mode / Light Mode Detection
```dart
final brightness = MediaQuery.of(context).platformBrightness;
final isDarkMode = brightness == Brightness.dark;
```

Contoh penggunaan:
```dart
Container(
  color: isDarkMode ? Colors.black : Colors.white,
)
```
## 8. Membuat UI Responsif dengan MediaQuery
```dart
Container(
  width: MediaQuery.of(context).size.width * 0.8,
  height: 200,
  color: Colors.blue,
)
```
Penjelasan:
- Lebar container selalu 80% dari lebar layar
- Cocok untuk berbagai ukuran device

## 9. MediaQuery vs LayoutBuilder
MediaQuery (berdasarkan ukuran layar)
```dart
final screenWidth = MediaQuery.of(context).size.width;
```

Cocok untuk:
- Layout halaman penuh
- Responsive global UI

LayoutBuilder (berdasarkan parent widget)
```dart
LayoutBuilder(
  builder: (context, constraints) {
    if (constraints.maxWidth > 300) {
      return WideWidget();
    } else {
      return SmallWidget();
    }
  },
)
```

Cocok untuk:
- Widget kecil
- Komponen reusable

Kesimpulan
- MediaQuery digunakan untuk mengetahui kondisi layar dan device
- Sangat penting untuk membuat UI Flutter yang fleksibel
- Hampir selalu digunakan di aplikasi Flutter profesional
- Bisa dikombinasikan dengan LayoutBuilder untuk hasil terbaik
