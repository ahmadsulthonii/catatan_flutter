Dari screenshot Xcode yang kamu kirim, ada **satu masalah yang langsung kelihatan** 👇

👉 File **`GoogleService-Info.plist` ada tanda `?`**

Di Xcode, tanda **`?` berarti file tidak terhubung dengan benar ke project** (belum masuk ke target Runner). Akibatnya Firebase tidak bisa membaca konfigurasi → muncul error:

```
[FirebaseCore][I-COR000005] No app has been configured yet.
```

Dan karena Firebase tidak aktif, **FCM token tidak akan muncul.**

---

# 🔧 Cara Memperbaiki (Paling Aman)

## 1️⃣ Hapus file yang bermasalah di Xcode

Klik kanan:

```
GoogleService-Info.plist
```

lalu pilih:

```
Delete
```

⚠️ Pilih **Remove Reference** (jangan Move to Trash).

---

## 2️⃣ Tambahkan ulang file dari Finder

1. Buka folder project di Finder

```
ios/Runner/GoogleService-Info.plist
```

2. Drag file tersebut ke **Runner di Xcode**

Saat popup muncul, centang:

```
☑ Copy items if needed
☑ Runner
```

Seperti ini:

```
Add to targets:
☑ Runner
```

---

## 3️⃣ Pastikan sudah masuk ke Target

Klik file:

```
GoogleService-Info.plist
```

Di panel kanan **File Inspector** pastikan:

```
Target Membership
☑ Runner
```

---

## 4️⃣ Clean build

Di terminal project jalankan:

```bash
flutter clean
flutter pub get
cd ios
pod install
```

lalu run lagi:

```bash
flutter run
```

---

# ✅ Jika berhasil

Console akan menampilkan:

```
Firebase initialized
```

dan token bisa muncul dengan:

```dart
String? token = await FirebaseMessaging.instance.getToken();
print(token);
```

---

# ⚠️ 1 Hal Penting Lagi (Sering Terjadi)

Pastikan **Bundle ID sama dengan Firebase**.

Cek di:

```
Xcode → Runner → Signing & Capabilities
```

contoh:

```
com.example.app
```

Harus sama dengan yang ada di **Firebase Console**.

---

💡 Kalau kamu mau, kirim juga screenshot:

1️⃣ **AppDelegate.swift**
2️⃣ **Firebase Console → iOS App setting**

Karena dari pengalaman saya, **90% kasus FCM iOS tidak muncul tokennya cuma karena 2 hal ini**. Saya bisa bantu cek sampai tokennya keluar.
