# ⌚ Akıllı Saat GPS Mesafe Takip Sistemi (TinyML Tensor Library)

Bu proje, kısıtlı kaynaklara sahip mikrodenetleyiciler (Arduino, ESP32 vb.) için tasarlanmış, bellek dostu bir **Dinamik Tensör** yapısıdır.

## 🎯 Proje Amacı
Gömülü sistemlerde 32-bit (Float) veri saklamak RAM'i hızla doldurur. Bu kütüphane, GPS'ten gelen kilometre verilerini **Quantization (Nicemleme)** yöntemiyle 8-bit tamsayılara sıkıştırarak bellekte **%75 tasarruf** sağlar.

## 🛠 Teknik Özellikler & Soruların Cevapları
- **Tensör Nedir?**: Verilerin çok boyutlu diziler halinde saklandığı temel yapıdır. Burada, tipi ve ölçeği içinde barındıran "ilkel" (primitive) bir formda kullanılmıştır.
- **Union & Tip Dönüşümü**: `union` kullanılarak `float*` ve `int8_t*` aynı bellek adresinde çakıştırılmıştır. Bu sayede fiziksel RAM alanı en verimli şekilde yönetilir.
- **Quantization**: Hassas ondalıklı sayıları, düşük bitli tam sayılara dönüştürme işlemidir. Bu projede doğrusal ölçekleme yöntemi uygulanmıştır.
- **Bellek Yönetimi**: `malloc` ile dinamik yer ayrılmış ve `free` ile bellek sızıntıları (memory leak) önlenmiştir.

## 🤖 Geliştirme Süreci (Agentic Coding)
Bu proje, **Gemini 2.0 Flash** modeli ile iş birliği içerisinde geliştirilmiştir. Model, bir gömülü sistem mühendisi rolünde:
1. Bellek mimarisinin `union` ile kurulmasını önermiş,
2. Nicemleme (Quantization) formüllerini optimize etmiş,
3. Hata payı analizlerini (Quantization Loss) gerçekleştirmemde rehberlik etmiştir.

## 💻 Çalıştırma
1. `gcc kosu_mesafe_tensor.c -o odev`
2. `./odev`
