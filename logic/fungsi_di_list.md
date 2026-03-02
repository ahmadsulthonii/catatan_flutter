# 📚 List Function pada List di Dart (Flutter)

Dokumentasi ini berisi kumpulan function penting pada `List` di Dart yang sering digunakan dalam pengolahan data di Flutter.

---

# 1️⃣ `fold()`

## 📌 Fungsi

Menggabungkan semua elemen List menjadi satu nilai akhir.

## 🧠 Cocok untuk:

* Menjumlahkan total
* Menghitung akumulasi
* Menggabungkan string
* Perhitungan kompleks

## 🧾 Sintaks

```dart
list.fold<ReturnType>(
  initialValue,
  (previousValue, element) => newValue
);
```

## ✅ Contoh

```dart
int total = angka.fold(0, (sum, item) => sum + item);
```

---

# 2️⃣ `reduce()`

## 📌 Fungsi

Mirip seperti `fold()`, tetapi:

* Tidak punya nilai awal
* Menggunakan elemen pertama sebagai nilai awal otomatis

## ⚠️ Catatan

Tidak bisa digunakan jika List kosong.

## 🧾 Sintaks

```dart
list.reduce((value, element) => newValue);
```

## ✅ Contoh

```dart
int total = angka.reduce((a, b) => a + b);
```

---

# 3️⃣ `map()`

## 📌 Fungsi

Mengubah setiap elemen List menjadi bentuk baru.

## 🧠 Cocok untuk:

* Transform data
* Convert tipe data
* Mengubah object ke widget (di Flutter sering dipakai)

## 🧾 Sintaks

```dart
list.map((element) => hasilBaru).toList();
```

## ✅ Contoh

```dart
var namaHurufBesar = nama.map((e) => e.toUpperCase()).toList();
```

---

# 4️⃣ `where()`

## 📌 Fungsi

Menyaring data berdasarkan kondisi.

## 🧾 Sintaks

```dart
list.where((element) => kondisi).toList();
```

## ✅ Contoh

```dart
var angkaGenap = angka.where((e) => e % 2 == 0).toList();
```

---

# 5️⃣ `firstWhere()`

## 📌 Fungsi

Mengambil elemen pertama yang memenuhi kondisi.

## 🧾 Sintaks

```dart
list.firstWhere(
  (element) => kondisi,
  orElse: () => nilaiDefault
);
```

## ✅ Contoh

```dart
var siswa = daftar.firstWhere(
  (e) => e['id'] == 1,
  orElse: () => null
);
```

---

# 6️⃣ `any()`

## 📌 Fungsi

Mengecek apakah ADA minimal satu elemen yang memenuhi kondisi.

## 🧾 Sintaks

```dart
list.any((element) => kondisi);
```

## ✅ Contoh

```dart
bool adaGenap = angka.any((e) => e % 2 == 0);
```

---

# 7️⃣ `every()`

## 📌 Fungsi

Mengecek apakah SEMUA elemen memenuhi kondisi.

## 🧾 Sintaks

```dart
list.every((element) => kondisi);
```

## ✅ Contoh

```dart
bool semuaLulus = nilai.every((e) => e >= 75);
```

---

# 8️⃣ `forEach()`

## 📌 Fungsi

Melakukan aksi pada setiap elemen (tanpa mengembalikan List baru).

## 🧾 Sintaks

```dart
list.forEach((element) {
  aksi;
});
```

## ✅ Contoh

```dart
angka.forEach((e) {
  print(e);
});
```

---

# 9️⃣ `contains()`

## 📌 Fungsi

Mengecek apakah List mengandung nilai tertentu.

```dart
bool ada = angka.contains(5);
```

---

# 🔟 `length`

## 📌 Fungsi

Menghitung jumlah elemen dalam List.

```dart
int jumlah = angka.length;
```

---

# 1️⃣1️⃣ `isEmpty` & `isNotEmpty`

```dart
if (list.isEmpty) {}
if (list.isNotEmpty) {}
```

---

# 1️⃣2️⃣ `take()` & `skip()`

## 📌 `take(n)`

Mengambil n elemen pertama.

```dart
var tigaPertama = angka.take(3).toList();
```

## 📌 `skip(n)`

Melewati n elemen pertama.

```dart
var setelahTiga = angka.skip(3).toList();
```

---

# 1️⃣3️⃣ `sort()`

## 📌 Fungsi

Mengurutkan List.

```dart
angka.sort();
```

Dengan custom:

```dart
angka.sort((a, b) => b.compareTo(a)); // descending
```

---

# 1️⃣4️⃣ `expand()`

## 📌 Fungsi

Mengubah List di dalam List menjadi satu List datar.

```dart
var hasil = listOfList.expand((e) => e).toList();
```

---

# 📊 Perbandingan Singkat

| Function | Mengubah Data | Filter | Return Value |
| -------- | ------------- | ------ | ------------ |
| fold     | ✅             | ❌      | 1 nilai      |
| reduce   | ✅             | ❌      | 1 nilai      |
| map      | ✅             | ❌      | List baru    |
| where    | ❌             | ✅      | List baru    |
| any      | ❌             | ✅      | bool         |
| every    | ❌             | ✅      | bool         |
| forEach  | ❌             | ❌      | void         |

---

# 🎯 Rekomendasi Belajar Urut

1. map()
2. where()
3. firstWhere()
4. any() & every()
5. reduce()
6. fold()

