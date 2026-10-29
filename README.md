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
  "yorum": {"baslik": "...", "tarih": "29 Eki",
            "maddeler": ["..."], "kaynaklar": [{"ad": "...", "url": "https://..."}]}
}
```

- `type`: kaptanlik, bireysel, takimW, takimL, odulW, pota, elendi
- `pota.detay` isteğe bağlı. Varsa üstte "Direkt potaya gönderilen" ve "Oylama ile gönderilen" kartları çıkar; `oy == toplam` ise "TULUM ÇIKARDI" yazar. Yoksa tek "Potaya gönderilen" kartı çıkar.
- `roster[].s` isteğe bağlı sıfat; ismin yanında etiket olarak görünür.
- `yorum` isteğe bağlı; "Haftayı kazanma ihtimali" kutusunun sağında görünür. Her hafta yenilenir.
- Takım güçleri, haftayı kazanma ihtimali ve yükselen yıldız sayfada `takimW/takimL/kaptanlik` olaylarından hesaplanır; elle girilmez.
