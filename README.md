# CK IDE

CK programlama dili için geliştirilmiş modern masaüstü IDE'si.

## Özellikler

- 🎨 Modern, VSCode-benzeri arayüz
- 📝 Sözdizimi vurgulama (CK dili için özelleştirilmiş)
- 📁 Dosya gezgini
- 📋 Sekmeli editör
- ▶️ Tek tıkla çalıştırma
- 🖥️ Yerleşik konsol
- 🌙/☀️ Koyu/Açık tema desteği
- ⌨️ Klavye kısayolları

## Kurulum

### Gereksinimler

1. **Node.js** (v18+)
2. **CK Derleyicisi** (`ckc.exe`)
3. **NASM** (Netwide Assembler)
4. **Microsoft Visual C++ Build Tools** (linking için)

### NASM Kurulumu

1. [NASM'ı indirin](https://www.nasm.us/pub/nasm/releasebuilds/)
2. NASM'ı yükleyin ve PATH'e ekleyin
3. Terminalde `nasm -v` komutuyla test edin

### Visual C++ Build Tools Kurulumu

1. [Visual Studio Installer](https://visualstudio.microsoft.com/downloads/) indirin
2. "C++ build tools" workload'ını yükleyin
3. `link.exe` komutunun erişilebilir olduğunu kontrol edin

### IDE Kurulumu

```bash
# Bağımlılıkları yükle
npm install

# Development modunda çalıştır
npm run dev

# Production build
npm run build
npm start

# Executable package oluştur
npm run dist
```

## Kullanım

### Temel İşlemler

- **Yeni Dosya**: `Ctrl+N` veya Dosya → Yeni
- **Dosya Aç**: `Ctrl+O` veya Dosya → Aç
- **Kaydet**: `Ctrl+S` veya Dosya → Kaydet
- **Çalıştır**: `Ctrl+R` veya ▶️ butonuna tıklayın
- **Tema Değiştir**: `Ctrl+T` veya status bar'daki tema butonuna tıklayın

### CK Dosyası Çalıştırma

1. Bir `.ck` dosyası oluşturun veya açın
2. CK kodunuzu yazın
3. `Ctrl+S` ile kaydedin
4. `Ctrl+R` ile çalıştırın veya ▶️ butonuna tıklayın

IDE otomatik olarak şu işlemleri gerçekleştirir:
1. Dosyayı kaydeder
2. `ckc.exe` ile NASM assembly'sine derler
3. NASM ile object dosyasına çevirir
4. MSVC linker ile executable oluşturur
5. Programı çalıştırır ve çıktıyı konsolda gösterir

### Örnek CK Kodu

```ck
yaz("Merhaba Dünya!")

a = 42
eğer a > 40 ise
    yaz("Sayı büyük")
değilse
    yaz("Sayı küçük")
bitti
```

## Proje Yapısı

```
ck-ide/
├── src/
│   ├── main/           # Electron ana süreç
│   │   └── main.ts
│   └── renderer/       # React UI
│       ├── components/
│       ├── styles/
│       ├── App.tsx
│       └── index.tsx
├── dist/               # Derlenmiş dosyalar
├── package.json
├── tsconfig.json
├── webpack.config.js
└── README.md
```

## Yapılandırma

### CK Derleyici Yolu

IDE, CK derleyicisini şu konumda arar:
```
../compiler/build/Debug/ckc.exe
```

Farklı bir konumdaysa, `src/main/main.ts` dosyasındaki `ckcPath` değişkenini güncelleyin.

### Build Klasörü

Derleme çıktıları her projenin kendi `build/` klasöründe saklanır:
- `dosya.asm` - NASM assembly kodu
- `dosya.obj` - Object dosyası
- `dosya.exe` - Çalıştırılabilir dosya

## Sorun Giderme

### "ckc.exe bulunamadı" Hatası

CK derleyicisinin doğru konumda olduğundan emin olun ve `main.ts` dosyasındaki yolu kontrol edin.

### "NASM bulunamadı" Hatası

NASM'ın PATH'e eklendiğinden emin olun:
```bash
nasm -v
```

### "Link hatası" 

Visual C++ Build Tools'un yüklü olduğundan emin olun:
```bash
link /?
```

### Türkçe Karakter Sorunları

IDE UTF-8 kodlamayı destekler. Dosyalarınızın UTF-8 olarak kaydedildiğinden emin olun.

## Geliştirme

### Development Modunda Çalıştırma

```bash
npm run dev
```

Bu komut şunları yapar:
- TypeScript'i watch modunda derler
- Webpack'i watch modunda çalıştırır
- Electron'u başlatır

### Değişiklik Yapma

- Ana süreç kodları: `src/main/`
- UI kodları: `src/renderer/`
- Stiller: `src/renderer/styles/`

### Yeni Özellik Ekleme

1. Gerekli bileşenleri `src/renderer/components/` altında oluşturun
2. IPC komunikasyonu gerekiyorsa `main.ts`'ye handler ekleyin
3. UI'da gerekli state'leri `App.tsx`'te yönetin

## Lisans

MIT License

## Katkıda Bulunma

1. Bu repo'yu fork edin
2. Feature branch oluşturun
3. Değişikliklerinizi commit edin
4. Push yapın ve Pull Request açın

---

**CK IDE** - Türkçe programlama dili CK için geliştirilmiş modern IDE
