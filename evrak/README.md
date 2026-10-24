# Mamoste evrak şablonları

Mamoste uygulamasındaki **Evraklar** bölümü bu klasörden okur. Uygulamayı yeniden derlemeye gerek yok:
dosyayı buraya koyup `liste.json`'a satırını ekleyip gönderince (git push) öğretmenler birkaç dakika içinde görür.

## Yeni / güncel şablon eklemek

1. Word dosyasını (`.docx`) bu klasöre koy. Dosya adı Türkçe karakter ve boşluk içermesin (ör. `zumre-2-donem-sonu.docx`).
2. `liste.json` → `evraklar` listesine bir satır ekle (ya da aynı `id`'li satırı güncelle):

```json
{
  "id": "zumre-2-donem-sonu",
  "kategori": "zumre",
  "ad": "Zümre öğretmenler kurulu tutanağı — 2. dönem sonu",
  "donem": "2. dönem sonu",
  "dosya": "zumre-2-donem-sonu.docx",
  "brans": null,
  "tarih": "2027-06-10"
}
```

- `kategori`: `zumre` · `sok` · `yillik-plan` · `kulup` · `veli` · `rehberlik`
- `brans`: `null` = bütün öğretmenler; yalnız bir branşa ise branş kimliği (`ingilizce`, `turkce`, `matematik`, `fen`, `sosyal`, `inkilap`, `din`, `teknoloji-tasarim`, `gorsel`, `muzik`, `beden`, `bilisim`)
- `tarih`: güncelleme günü (YYYY-AA-GG). Tarih değişince öğretmende **YENİ** etiketi çıkar.
- Yıllık planlar `yillik-plan/<branş>-<sınıf>.docx` (MEB 2026-2027 çerçeve planlarından, `brans` dolu: yalnız o branşın öğretmeni görür).
- Ana Mamoste deposunda `node tools/evrak/sablon.mjs` bütün tutanakları ve yıllık planları yeniden üretir (mevzuat değişince metinleri orada güncelle).

## Uygulamanın kendiliğinden doldurduğu yer tutucular

Şablonun içinde aynen bu şekilde yaz (süslü parantezle, büyük harf):

| Yer tutucu | Yerine yazılan |
|---|---|
| `{OGRETMEN}` | Öğretmenin adı soyadı |
| `{OKUL}` | Okul adı |
| `{IL}` / `{ILCE}` | İl / ilçe |
| `{MUDUR}` | Okul müdürünün adı soyadı |
| `{BRANS}` | Branş (ör. İngilizce) |
| `{TARIH}` | İndirildiği gün (GG.AA.YYYY) |
| `{EGITIM_YILI}` | Eğitim yılı (ör. 2026-2027) |

Satır tamamen büyük harfse (ör. `{ILCE} KAYMAKAMLIĞI`) bilgi de büyük harfle yazılır. Öğretmen bir bilgiyi girmediyse yerine `……` yazılır.
Yer tutucunun bulunduğu paragraf tek biçime iner (yarısı kalın gibi farklar kalkar); yer tutucuyu kendi satırına ya da tablo hücresine koymak en iyisidir.
