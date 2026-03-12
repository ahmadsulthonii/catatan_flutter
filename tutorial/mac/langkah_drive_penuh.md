Ya, ini sudah jelas penyebabnya 👍
Folder **Xcode** kamu memakan **≈70 GB**, dan itu **normal terjadi pada developer iOS** karena banyak cache dan simulator.

![Image](https://global.discourse-cdn.com/ionicframework/optimized/3X/d/d/ddf8f8eaf6eeccf2810b6b3c0f2626be1579b87f_2_690x473.png)

![Image](https://images.squarespace-cdn.com/content/v1/4f3b434c8754e3c85b69cfb7/1565164861937-C2IDBO5P22PGG2MGJX3M/xcode0.png)

![Image](https://i.sstatic.net/YE3u3.png)

![Image](https://i.sstatic.net/SSvKs.png)

Di dalam folder Xcode biasanya yang membuat storage besar adalah 4 hal ini:

---

# 1. DerivedData (Cache Build) – Bisa 20-40 GB

Setiap kali kamu build project di Xcode, dia membuat cache di:

```
~/Library/Developer/Xcode/DerivedData
```

Ini **100% aman dihapus** karena hanya cache.

### Cara hapus

Buka Terminal lalu jalankan:

```bash
rm -rf ~/Library/Developer/Xcode/DerivedData
```

Biasanya langsung **hemat 10-40 GB**.

---

# 2. iOS Simulator – Bisa 10-30 GB

Setiap simulator iPhone menyimpan:

* OS simulator
* aplikasi yang diinstall
* data testing

Lokasinya:

```
~/Library/Developer/CoreSimulator
```

### Cara hapus semua simulator data

```bash
xcrun simctl delete unavailable
```

Atau hapus manual:

```bash
rm -rf ~/Library/Developer/CoreSimulator
```

---

# 3. DeviceSupport – Bisa 5-15 GB

Saat kamu test iPhone fisik, Xcode menyimpan support file untuk tiap iOS version.

Lokasi:

```
~/Library/Developer/Xcode/iOS DeviceSupport
```

Kalau banyak iOS version lama, folder ini bisa sangat besar.

Aman hapus **versi lama**.

---

# 4. Archives (Build Release)

Jika pernah build untuk App Store.

Lokasi:

```
~/Library/Developer/Xcode/Archives
```

Kadang bisa **10GB+**.

---

# Cara Paling Cepat Bersihkan 50GB 🚀

Jalankan ini di Terminal:

```bash
rm -rf ~/Library/Developer/Xcode/DerivedData
rm -rf ~/Library/Developer/CoreSimulator
rm -rf ~/Library/Developer/Xcode/Archives
```

Biasanya langsung **70GB → 10GB saja**.

---

💡 **Tips penting untuk Flutter / iOS developer**

Tambahkan juga:

```bash
flutter clean
```

di setiap project supaya build tidak menumpuk.

---

✅ Kalau kamu mau, saya bisa kasih **cara bersihkan storage Mac developer sampai lega 100GB** (ada 7 folder tersembunyi yang biasanya sangat besar).
