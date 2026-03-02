# 📜 Scroll di Flutter — Panduan Lengkap

Dokumen ini menjelaskan konsep, jenis, dan implementasi **scroll di Flutter** secara lengkap, mulai dari dasar hingga penggunaan lanjutan. File ini bisa langsung disimpan sebagai `scroll_flutter.md`.

---

## 1️⃣ Apa Itu Scroll di Flutter?

Scroll di Flutter adalah mekanisme untuk menggulir (menggeser) tampilan ketika konten melebihi ukuran layar.

Flutter menyediakan berbagai widget scrollable seperti:

* `SingleChildScrollView`
* `ListView`
* `GridView`
* `CustomScrollView`
* `PageView`

Semua widget scroll di Flutter dibangun di atas sistem **Scrollable & ScrollController**.

---

# 2️⃣ SingleChildScrollView

Digunakan untuk **konten tunggal** (biasanya Column atau Row) yang perlu discroll.

### ✅ Cocok untuk:

* Form panjang
* Halaman statis dengan banyak widget
* Konten kecil hingga menengah

### 📌 Contoh:

```dart
import 'package:flutter/material.dart';

class ExampleSingleScroll extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text("SingleChildScrollView")),
      body: SingleChildScrollView(
        child: Column(
          children: List.generate(
            20,
            (index) => Container(
              margin: EdgeInsets.all(8),
              height: 100,
              color: Colors.blue,
              child: Center(
                child: Text(
                  "Item $index",
                  style: TextStyle(color: Colors.white),
                ),
              ),
            ),
          ),
        ),
      ),
    );
  }
}
```

### ⚠️ Kekurangan

* Semua child dirender sekaligus (tidak efisien untuk data besar)

---

# 3️⃣ ListView

Digunakan untuk daftar data yang bisa di-scroll.

## Jenis ListView

### 1. ListView Biasa

```dart
ListView(
  children: [
    ListTile(title: Text("Item 1")),
    ListTile(title: Text("Item 2")),
  ],
)
```

---

### 2. ListView.builder (Paling Disarankan)

Digunakan untuk data besar karena hanya merender item yang terlihat.

```dart
ListView.builder(
  itemCount: 100,
  itemBuilder: (context, index) {
    return ListTile(
      title: Text("Item $index"),
    );
  },
)
```

---

### 3. ListView.separated

Digunakan jika ingin memberi separator antar item.

```dart
ListView.separated(
  itemCount: 20,
  separatorBuilder: (context, index) => Divider(),
  itemBuilder: (context, index) {
    return ListTile(
      title: Text("Item $index"),
    );
  },
)
```

---

# 4️⃣ GridView

Digunakan untuk menampilkan item dalam bentuk grid (kotak-kotak).

### 📌 Contoh:

```dart
GridView.builder(
  gridDelegate: SliverGridDelegateWithFixedCrossAxisCount(
    crossAxisCount: 2,
  ),
  itemCount: 20,
  itemBuilder: (context, index) {
    return Card(
      child: Center(
        child: Text("Item $index"),
      ),
    );
  },
)
```

---

# 5️⃣ CustomScrollView & Sliver

Digunakan untuk layout kompleks dan fleksibel.

### 🔥 Kelebihan:

* Bisa menggabungkan berbagai jenis scrollable
* Support efek seperti collapsing AppBar

### 📌 Contoh:

```dart
CustomScrollView(
  slivers: [
    SliverAppBar(
      expandedHeight: 200,
      flexibleSpace: FlexibleSpaceBar(
        title: Text("Sliver AppBar"),
      ),
      pinned: true,
    ),
    SliverList(
      delegate: SliverChildBuilderDelegate(
        (context, index) => ListTile(
          title: Text("Item $index"),
        ),
        childCount: 20,
      ),
    ),
  ],
)
```

---

# 6️⃣ ScrollController

Digunakan untuk:

* Mengontrol posisi scroll
* Mendapatkan posisi scroll
* Membuat animasi scroll

### 📌 Contoh:

```dart
class ExampleScrollController extends StatefulWidget {
  @override
  _ExampleScrollControllerState createState() =>
      _ExampleScrollControllerState();
}

class _ExampleScrollControllerState
    extends State<ExampleScrollController> {
  final ScrollController _controller = ScrollController();

  void scrollToTop() {
    _controller.animateTo(
      0,
      duration: Duration(seconds: 1),
      curve: Curves.easeInOut,
    );
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      floatingActionButton: FloatingActionButton(
        onPressed: scrollToTop,
        child: Icon(Icons.arrow_upward),
      ),
      body: ListView.builder(
        controller: _controller,
        itemCount: 50,
        itemBuilder: (context, index) =>
            ListTile(title: Text("Item $index")),
      ),
    );
  }
}
```

---

# 7️⃣ Scroll Physics

Mengatur perilaku scroll.

Contoh:

```dart
ListView(
  physics: BouncingScrollPhysics(), // iOS style
)
```

Jenis physics:

* `BouncingScrollPhysics()` → efek pantul
* `ClampingScrollPhysics()` → default Android
* `NeverScrollableScrollPhysics()` → nonaktif scroll

---

# 8️⃣ Nested Scroll

Jika ingin scroll di dalam scroll, gunakan:

* `NestedScrollView`
* `shrinkWrap: true`
* `physics: NeverScrollableScrollPhysics()`

Contoh:

```dart
ListView(
  children: [
    ListView.builder(
      shrinkWrap: true,
      physics: NeverScrollableScrollPhysics(),
      itemCount: 5,
      itemBuilder: (context, index) {
        return Text("Sub item $index");
      },
    ),
  ],
)
```

---

# 9️⃣ Perbandingan Singkat

| Widget                | Cocok Untuk     | Performa         |
| --------------------- | --------------- | ---------------- |
| SingleChildScrollView | Konten kecil    | Kurang efisien   |
| ListView.builder      | Data besar      | Sangat efisien   |
| GridView.builder      | Grid data       | Efisien          |
| CustomScrollView      | Layout kompleks | Sangat fleksibel |

---

# 🔟 Best Practice

✅ Gunakan `ListView.builder` untuk data dinamis
✅ Hindari `SingleChildScrollView` untuk data besar
✅ Gunakan `ScrollController` untuk kontrol manual
✅ Gunakan Sliver untuk layout kompleks
✅ Jangan nested scroll tanpa pengaturan `shrinkWrap`

---

# 🎯 Kesimpulan

Flutter menyediakan sistem scroll yang sangat fleksibel:

* Scroll sederhana → `ListView`
* Scroll grid → `GridView`
* Scroll kompleks → `CustomScrollView`
* Kontrol manual → `ScrollController`

Memahami perbedaan dan penggunaan yang tepat akan membuat aplikasi lebih **efisien, halus, dan profesional**.

---

Jika kamu mau, saya juga bisa buatkan:

* Versi dengan ilustrasi diagram
* Versi untuk materi presentasi
* Versi lengkap dengan best practice arsitektur
* Versi dengan contoh kasus real project

Tinggal bilang saja 🚀
