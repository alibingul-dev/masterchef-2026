# MasterChef 2026 — Kupa Yarışı

Canlı pano: https://alibingul-dev.github.io/masterchef-2026/

Veri `data.json` dosyasında, render `index.html` içinde.

## data.json şeması

```json
{
  "updated": "29 Ekim 2026",
  "roster": [{"n": "Ad Soyad", "t": "kirmizi|mavi", "s": "Sıfat"}],
  "episodes": [{"date": "28 Eki", "evs": [
    {"type": "pota", "who": ["A", "B"],
     "detay": [
       {"n": "A", "yol": "direkt", "gonderen": "C"},
       {"n": "B", "yol": "oy", "oy": 5, "toplam": 7}
     ]}
  ]}],
  "yorum": {"baslik": "...", "tarih": "29 Eki", "haberler": ["..."], "gozlem": ["..."],
            "kaynaklar": [{"ad": "...", "url": "https://..."}]},
  "yakinlik": [{"ad": "Kancalar", "tur": "yakin|gergin", "renk": "#6B2FA3", "kisiler": ["..."], "aciklama": "...", "teyit": "..."}],
  "tahmin": {"eleme": "1 Kas", "tarih": "1 Kasım 2026",
             "adaylar": [{"n": "Ad Soyad", "p": 25, "neden": "..."}], "not": "..."}
}
```

- `type`: kaptanlik, bireysel, takimW, takimL, odulW, pota, elendi
- `kaptanlik` olayında `ikinci`: kazananın seçtiği karşı takım kaptanı (takım güçleri tablosunda (K) olarak iki kaptan da işaretlenir).
- `pota.detay[].not` varsa kartta gönderen yerine aynen yazılır (ör. "oylamasız · kırmızıda aday kalmadı").
- `pota.detay` isteğe bağlı. Varsa üstte "Direkt potaya gönderilen" ve "Oylama ile gönderilen" kartları çıkar; `oy == toplam` ise "TULUM ÇIKARDI" yazar. Yoksa tek "Potaya gönderilen" kartı çıkar.
- `roster[].s` sıfat (ismin yanında etiket), `roster[].sa` sıfatı açıklayan tek cümle.
- `pota.detay[].yol`: direkt (`gonderen`) veya oy (`oy`/`toplam`, yoksa `not`). Kartlar son elemeden bu yana tüm potayı listeler. Oy sayıları haberlerde verilmiyor; sadece bölüm videosundan alınabilir.
- `yakinlik`: "Kim kime yakın" kartı; yakın grupların satırında sol dikey şerit grup renginde, satırda YAKIN/GERGİN etiketleri; potadakilerin satır altında takım rengi–siyah yatay şerit.
- `yorum` isteğe bağlı; "Haftayı kazanma ihtimali" kutusunun sağında görünür. Her hafta yenilenir.
- `tahmin` isteğe bağlı; "Son bölüm" kutularının altında "Eleme tahmini · `eleme`" kartı çıkar. `adaylar[].n` roster'daki tam ad, `p` yüzde (≥22 kırmızı, 16–21 amber, 8–15 gri, <8 yeşil), `neden` satır altı açıklama; `not` kartın altında soluk yazılır.
  `episodes` içinde `date == tahmin.eleme` olan bir `elendi` olayı varsa elenen satırda "ELENDİ" çıkar; elenen en yüksek 2 adaydan biriyse başlıkta "TUTTU", değilse "TUTMADI" yazar. Yeni eleme için alan elle yenilenir.
- Takım güçleri, haftayı kazanma ihtimali ve yükselen yıldız sayfada `takimW/takimL/kaptanlik` olaylarından hesaplanır; elle girilmez.
