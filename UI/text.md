
Berikut versi **full Markdown (.md)** yang sudah rapi dan siap langsung kamu copy:

---

# Flutter Text Widget Notes

Catatan pribadi tentang **Text Widget di Flutter** untuk menampilkan dan mengatur teks dalam berbagai kebutuhan UI.

---

## 1. Apa itu Text Widget?

**Text** adalah widget dasar di Flutter yang digunakan untuk menampilkan teks ke layar.

Text sangat penting untuk:

* Menampilkan informasi
* Judul halaman
* Label tombol
* Deskripsi konten
* UI berbasis teks lainnya

Singkatnya:

> Text adalah widget utama untuk menampilkan tulisan di Flutter.

---

## 2. Struktur Dasar Text

```dart
Text(
  'Hello Flutter',
)
```

Versi dengan styling:

```dart
Text(
  'Hello Flutter',
  style: TextStyle(
    fontSize: 20,
    color: Colors.blue,
  ),
)
```

---

## 3. Properti Penting pada Text

### 3.1 style (Mengatur Tampilan Teks)

```dart
Text(
  'Belajar Flutter',
  style: TextStyle(
    fontSize: 24,
    fontWeight: FontWeight.bold,
    fontStyle: FontStyle.italic,
    color: Colors.black,
    letterSpacing: 1.5,
    wordSpacing: 2,
    height: 1.5,
    decoration: TextDecoration.underline,
  ),
)
```

Properti umum `TextStyle`:

* `fontSize`
* `fontWeight`
* `fontStyle`
* `color`
* `letterSpacing`
* `wordSpacing`
* `height` (line height)
* `decoration`
* `backgroundColor`
* `fontFamily`

---

### 3.2 textAlign (Posisi Teks)

```dart
Text(
  'Hello Flutter',
  textAlign: TextAlign.center,
)
```

Pilihan alignment:

* `TextAlign.left`
* `TextAlign.right`
* `TextAlign.center`
* `TextAlign.justify`
* `TextAlign.start`
* `TextAlign.end`

---

### 3.3 maxLines (Batas Baris)

```dart
Text(
  'Teks panjang sekali yang mungkin lebih dari satu baris',
  maxLines: 2,
)
```

Digunakan untuk:

* Membatasi jumlah baris
* Mencegah overflow layout

---

### 3.4 overflow (Jika Teks Kepanjangan)

```dart
Text(
  'Teks sangat panjang yang tidak muat dalam satu baris',
  maxLines: 1,
  overflow: TextOverflow.ellipsis,
)
```

Pilihan overflow:

* TextOverflow.ellipsis	Memotong teks dengan tiga titik di akhir (...)
* TextOverflow.fade	Teks memudar secara perlahan di bagian akhir.
* TextOverflow.clip	Teks langsung dipotong tanpa tanda apa pun.
* TextOverflow.visible	Teks tetap muncul meski menabrak batas (default).


---

### 3.5 softWrap

Mengatur apakah teks boleh pindah ke baris baru.

```dart
Text(
  'Teks panjang',
  softWrap: false,
)
```

---

## 4. RichText dan TextSpan

Digunakan jika ingin beberapa style berbeda dalam satu teks.

```dart
RichText(
  text: TextSpan(
    text: 'Hello ',
    style: TextStyle(color: Colors.black),
    children: [
      TextSpan(
        text: 'Flutter',
        style: TextStyle(
          color: Colors.blue,
          fontWeight: FontWeight.bold,
        ),
      ),
    ],
  ),
)
```

Digunakan untuk:

* Highlight kata tertentu
* Kombinasi warna dalam satu kalimat
* Link teks
* Custom text styling kompleks

---

## 5. DefaultTextStyle

Mengatur style default untuk semua Text di dalamnya.

```dart
DefaultTextStyle(
  style: TextStyle(
    fontSize: 18,
    color: Colors.grey,
  ),
  child: Column(
    children: [
      Text('Teks 1'),
      Text('Teks 2'),
    ],
  ),
)
```

Cocok untuk:

* Konsistensi desain
* Mengurangi penulisan style berulang

---

## 6. Menggunakan Theme (Best Practice)

Lebih profesional menggunakan Theme:

```dart
Text(
  'Judul',
  style: Theme.of(context).textTheme.titleLarge,
)
```

Keuntungan:

* Konsisten
* Mudah ubah global style
* Cocok untuk production app
* Mendukung dark mode otomatis

---

## 7. Text dalam Layout (Row & Column)

Masalah umum: overflow dalam Row.

Solusi:

```dart
Row(
  children: [
    Expanded(
      child: Text(
        'Teks panjang dalam row yang bisa overflow',
        overflow: TextOverflow.ellipsis,
      ),
    ),
  ],
)
```

Alternatif:

* `Flexible`
* `FittedBox`

---

## 8. Text dan Responsiveness

Menggunakan MediaQuery untuk ukuran font responsif:

```dart
Text(
  'Responsive Text',
  style: TextStyle(
    fontSize: MediaQuery.of(context).size.width * 0.05,
  ),
)
```

Penjelasan:

* Ukuran font mengikuti lebar layar
* Cocok untuk tablet dan mobile

---

## 9. SelectableText

Jika ingin teks bisa di-copy:

```dart
SelectableText(
  'Teks ini bisa disalin',
)
```

Cocok untuk:

* Menampilkan kode
* Token API
* Informasi penting

---

## 10. Text dan Aksesibilitas

Flutter otomatis mengikuti pengaturan ukuran teks sistem.

Kamu bisa mengecek:

```dart
final textScale = MediaQuery.of(context).textScaleFactor;
```

Best practice:

* Jangan mematikan scaling kecuali benar-benar perlu
* Pastikan layout tetap aman saat textScale besar

---

## 11. Custom Font

Tambahkan font di `pubspec.yaml`:

```yaml
fonts:
  - family: Poppins
    fonts:
      - asset: assets/fonts/Poppins-Regular.ttf
```

Lalu gunakan:

```dart
Text(
  'Custom Font',
  style: TextStyle(
    fontFamily: 'Poppins',
  ),
)
```

---

## 12. Best Practice Menggunakan Text

✔ Gunakan `Theme.of(context).textTheme`
✔ Hindari hardcode font size berlebihan
✔ Gunakan `maxLines` + `overflow`
✔ Gunakan `RichText` jika butuh multiple style
✔ Perhatikan accessibility
✔ Gunakan Expanded/Flexible dalam Row

---

## Kesimpulan

* Text adalah widget paling dasar dan paling sering digunakan di Flutter
* Memiliki banyak properti untuk styling dan kontrol layout
* Bisa dibuat sangat fleksibel dan responsif
* Sangat penting untuk dipahami dalam pengembangan Flutter profesional
* Gunakan Theme untuk aplikasi production

---

Kalau mau, saya bisa lanjut buat:

* 📘 Flutter TextFormField Notes
* 📘 Flutter Typography System Notes
* 📘 Responsive UI Complete Guide
* 📘 LayoutBuilder Notes

Tinggal bilang saja 👍
