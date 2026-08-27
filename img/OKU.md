# Fotoğraflar buraya

Dosyaları aşağıdaki isimlerle bu klasörlere koyun. Doğru isimle konan her dosya,
sitede yer tutucunun yerine **kendiliğinden** geçer — kod değiştirmeye gerek yok.

## Makinalar → `img/makinalar/`

```
ofset-1.jpg          Ofset baskı  (kapak — üretim hattında görünür)
ofset-2.jpg          Ofset — ikinci açı
ofset-3.jpg          Ofset — üçüncü açı
dijital-1.png        Dijital baskı           ⟵ fonu kesilmiş
dijital-2.png        Dijital — ikinci makina ⟵ fonu kesilmiş
dijital-3.png        Dijital — üçüncü makina ⟵ fonu kesilmiş
dis-mekan-1.png      Dış mekan baskı         ⟵ fonu kesilmiş
harf-kesim-1.png     Harf kesim & bas-kes    ⟵ fonu kesilmiş
kesim-1.png          Giyotin & kesim         ⟵ fonu kesilmiş
```

Bir makinanın kaç fotoğrafı olacağı serbest. Yeni açı eklemek için dosyayı
koyup `src/data/makinalar.ts` içindeki `gorseller` dizisine adını yazmanız
yeterli. İlk sıradaki fotoğraf kapak olur, diğerleri teknik föyün altında
"diğer açılar" olarak çıkar.

## Dükkân → `img/`

```
dukkan-genis.jpg    Binanın tamamı, çatıdan kaldırıma  ⟵ ana sayfa hero fonu
```

İkisi de `Fotolar/dukkan2.jpg.jpeg` ham karesinden çıkarıldı — sokaktaki
araçların rötuşla silindiği sürüm. Ana sayfada fotoğraf
zemin olarak, çok soluk ve kenarları kağıda karışacak biçimde duruyor; yoğunluğu
tek satırdan ayarlanır: `src/pages/AnaSayfa.tsx` → `FON_YOGUNLUK`.

## Baskı örnekleri → `img/ornekler/`

```
kartvizit-01.jpg  kartvizit-02.jpg     davetiye-01.jpg  davetiye-02.jpg
brosur-01.jpg     brosur-02.jpg        kase-01.jpg      etiket-01.jpg
evrak-01.jpg      branda-01.jpg        folyo-01.jpg     arac-01.jpg
afis-01.jpg
```

Bu fotoğraflar **iki yerde birden** kullanılıyor: Örnekler galerisinde ve
İşler sayfalarında. Aynı işin fotoğrafını iki klasöre kopyalamıyoruz —
`src/data/isler.ts` doğrudan bu yollara bakıyor.

Yeni örnek eklemek için fotoğrafı bu klasöre koyup `src/data/ornekler.ts`
dosyasına tek satır ekleyin. Satırdaki `genis` / `dikey` bayrağını
fotoğrafın **gerçek en-boy oranına göre** seçin (geniş 16/9, dikey 3/4,
işaretsiz 4/3); uymayan bayrak fotoğrafın kenarlarını kestirir.

## İş kategorileri → `img/isler/`

```
tabela-1.jpg    ⟵ tek eksik: tabela işi
```

Diğer on kategori örnekler klasöründeki fotoğrafları kullanıyor.

---

## Fotoğraf çekerken

- **Yatay çekin.** Site yatay görsellere göre kurgulandı.
- **Gündüz, pencere ışığında** çekin. Flaş kullanmayın — kağıt parlar, renk kaçar.
- Makinaları **çalışırken** çekmek, boş çekmekten çok daha iyi durur.
- Telefon kamerası yeterli. Stok fotoğraf kullanmayın; gerçek dükkânın fotoğrafı
  her zaman daha ikna edici.

## Dosya boyutu — bunu elle yapmayın

Fotoğrafları klasöre koyduktan sonra bir kez şunu çalıştırın:

```bash
npm run gorseller
```

Bu araç hepsini otomatik olarak 1800 piksele indirir, sıkıştırır, telefon
fotoğraflarının yan yatmasına yol açan EXIF döndürmesini uygular ve yanına
`.webp` sürümünü üretir. Zaten hazırlanmış dosyaya tekrar dokunmaz, istediğiniz
kadar çalıştırabilirsiniz.

Telefondan çıkan bir fotoğraf 3–5 MB olur; beş makina fotoğrafı 20 MB eder ve
mobil veriyle giren müşteri o sayfayı açamaz. Araç aynı fotoğrafı gözle ayırt
edilemeyecek şekilde ~200 KB'ye indirir.

## JPG mi PNG mi? — dosya uzantısı davranışı belirler

Site, uzantıya bakarak görselin türünü anlıyor:

| Uzantı | Ne demek | Sitede nasıl davranır |
|---|---|---|
| `.jpg` | **Fotoğraf** — atölyede çekilmiş kare | Alanı tamamen doldurur, gerekirse kenarları kırpılır |
| `.png` | **Fonu kesilmiş ürün görseli** | Zemini şeffaf kabul edilir, kırpılmaz, sayfanın kağıdı arkasından görünür |

Yani dükkânda çekilmiş fotoğrafları `.jpg`, fonu temizlenmiş katalog görsellerini
`.png` olarak kaydedin. `npm run gorseller` da bu ayrımı korur — şeffaf PNG'leri
JPG'ye çevirip fonlarını beyaz kutuya dönüştürmez.

## Fotoğraflar sitede nasıl görünür

Makina fotoğrafları sayfada **soluk** gösterilir: gri-sıcak ton, düşük kontrast,
üstünde ince bir kağıt yıkaması. Böylece dağınık atölye arka planı geri gider,
göz makinanın silüetine takılır ve fotoğraf sayfanın kağıt paletine oturur.
Fotoğrafın üzerine gelindiğinde gerçek rengine döner.

Arka planı bilerek kesmiyoruz: makinaların ince kolları, milleri ve merdaneleri
otomatik kesimde tırtıklı kenar bırakır, sonuç orijinalinden kötü görünür.
Çalışan bir atölye arka planı zaten sitenin iddiasını destekliyor — burası
gerçek bir dükkân.
