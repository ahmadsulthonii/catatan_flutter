# aplikasi mobile dengan fitur multi bahasa di flutter,

## 1. Konsep Singkat

Kita akan:
- Pakai flutter_localizations
- Pakai Intl
- Gunakan ARB file (.arb) untuk terjemahan
- Contoh bahasa: Indonesia (id) & Inggris (en)

## 2. Tambahkan Dependency

Di pubspec.yaml:
```
dependencies:
  flutter:
    sdk: flutter
  flutter_localizations:
    sdk: flutter
  intl: ^0.19.0

flutter:
  generate: true
```

Lalu jalankan:

```
flutter pub get
```
## 3. Struktur Folder
```
lib/
 ├─ main.dart
 └─ l10n/
     ├─ app_en.arb
     └─ app_id.arb
```

## 4. File Terjemahan (20+ Kata)
🇺🇸 lib/l10n/app_en.arb

``` json
{
  "appTitle": "Multi Language App",
  "home": "Home",
  "profile": "Profile",
  "settings": "Settings",
  "language": "Language",
  "welcome": "Welcome",
  "login": "Login",
  "logout": "Logout",
  "register": "Register",
  "email": "Email",
  "password": "Password",
  "confirmPassword": "Confirm Password",
  "save": "Save",
  "cancel": "Cancel",
  "delete": "Delete",
  "search": "Search",
  "notification": "Notification",
  "darkMode": "Dark Mode",
  "lightMode": "Light Mode",
  "about": "About",
  "help": "Help"
} 
```

🇮🇩 lib/l10n/app_id.arb

``` json
{
  "appTitle": "Aplikasi Multi Bahasa",
  "home": "Beranda",
  "profile": "Profil",
  "settings": "Pengaturan",
  "language": "Bahasa",
  "welcome": "Selamat Datang",
  "login": "Masuk",
  "logout": "Keluar",
  "register": "Daftar",
  "email": "Email",
  "password": "Kata Sandi",
  "confirmPassword": "Konfirmasi Kata Sandi",
  "save": "Simpan",
  "cancel": "Batal",
  "delete": "Hapus",
  "search": "Cari",
  "notification": "Notifikasi",
  "darkMode": "Mode Gelap",
  "lightMode": "Mode Terang",
  "about": "Tentang",
  "help": "Bantuan"
}
```


## 5. main.dart

``` dart
import 'package:flutter/material.dart';
import 'package:flutter_localizations/flutter_localizations.dart';
import 'package:flutter_gen/gen_l10n/app_localizations.dart';

void main() {
  runApp(const MyApp());
}

class MyApp extends StatefulWidget {
  const MyApp({super.key});

  @override
  State<MyApp> createState() => _MyAppState();
}

class _MyAppState extends State<MyApp> {
  Locale _locale = const Locale('en');

  void _changeLanguage(Locale locale) {
    setState(() {
      _locale = locale;
    });
  }

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      locale: _locale,
      supportedLocales: const [
        Locale('en'),
        Locale('id'),
      ],
      localizationsDelegates: const [
        AppLocalizations.delegate,
        GlobalMaterialLocalizations.delegate,
        GlobalWidgetsLocalizations.delegate,
        GlobalCupertinoLocalizations.delegate,
      ],
      home: HomePage(onLanguageChange: _changeLanguage),
    );
  }
}

class HomePage extends StatelessWidget {
  final Function(Locale) onLanguageChange;

  const HomePage({super.key, required this.onLanguageChange});

  @override
  Widget build(BuildContext context) {
    final t = AppLocalizations.of(context)!;

    return Scaffold(
      appBar: AppBar(
        title: Text(t.appTitle),
      ),
      body: Padding(
        padding: const EdgeInsets.all(16),
        child: Column(
          crossAxisAlignment: CrossAxisAlignment.start,
          children: [
            Text(t.welcome, style: const TextStyle(fontSize: 22)),
            const SizedBox(height: 16),

            Text(t.home),
            Text(t.profile),
            Text(t.settings),
            Text(t.notification),
            Text(t.about),
            Text(t.help),

            const SizedBox(height: 24),

            Row(
              children: [
                ElevatedButton(
                  onPressed: () => onLanguageChange(const Locale('en')),
                  child: const Text("English"),
                ),
                const SizedBox(width: 12),
                ElevatedButton(
                  onPressed: () => onLanguageChange(const Locale('id')),
                  child: const Text("Indonesia"),
                ),
              ],
            ),
          ],
        ),
      ),
    );
  }
}
```

## 6. Hasil

Tombol English / Indonesia
Semua teks otomatis berubah
Mudah ditambah bahasa lain (tinggal tambah .arb)