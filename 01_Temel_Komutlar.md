# Temel Komutlar

## cut
Dosya veya çıktıların karakter, byte veya alan bazlı belirli kısımlarını çıkartmak için kullanılır.

### -c
Karakterlere göre kesme yapar.
```
echo "abcdef" | cut -c 2-4
```
Çıktı : **bcd**

### -f
Sütunlardan belirtileni seçer.
```
echo "root:x:0:0:root:/root:/bin/bash" | cut -d ":" -f 1
```
Çıktı : **root**

Burada **-d** seçeneği "delimiter" belirlemek için kullanıldı. **-f** ise 1. alanı seçmek için kullanıldı.

Birden fazla alan seçmek için "-f 1,7" kullanılır ve 1. ile 7. alan seçilir.

Aynı şekilde dosyadan sütun çekmek için ise
	```
	cut -d ":" -f 1 file.txt
	```
kullanılır. Bu şekilde dosya içerisindeki sütunlardan ilki seçilir ve bastırılır. Sadece bir satırdan değil tüm satırlardan seçim yapılır.

Delimiter belirlenmezse varsayılan olarak **TAB** (\t) kabul edilir.

## paste
Bir veya daha fazla dosyanın satırlarını yan yana birleştirir ve çıktı verir.
Varsayılan olarak TAB ile birleştirir.
```
paste [seçenekler] [dosya1] [dosya2] ...
```
Delimiter "-d" seçeneğiyle ayarlanır ve TAB yerine belirlenen değer kullanılır.
Birden çok delimiter kullanımı ile girilen dosyalar arası sırasıyla belirlenen delimiterlar kullanılır.

### -s
Tek bir dosyada satırları yan yana birleştirmek için kullanılır.
Örneğin *renkler.txt* adlı bir dosyada alt alta:
```
kırmızı
mavi
yeşil
```
yazıyor. **"paste -s renkler.txt"** komutunu girdiğimizde *"kırmızı	yeşil	mavi"* çıktısını alırız.

## sort
Dosya içeriği veya terminal çıktısını alfabetik, sayısal veya belirlenen şekilde sıralar.
```
sort [seçenekler] [dosya]
```
Varsayılan olarak alfabetik sıralar.

-r : Tersten sıralama yapar.
-n : Sayısal sıralama yapar. (küçükten büyüğe)
-f : Büyük/küçük harf duyarlılığını yok sayar.
## tr
*translate*

Bir karakter kümesini başka bir karakter kümesine çevirir, silebilir veya tekrar eden karakterleri sıkıştırabilir.

Satır değil, karakter odaklı çalışır.

```
tr [seçenekler] [kaynak_karakterler] [hedef_karakterler]
```
**tr** doğrudan dosya işlemez; **stdin** ile çalışır.

### 'a-z' 'A-Z'
Küçük harfleri büyük harfe çevirmek için kullanılır. Tersi için de aynısı geçerlidir.

### -d
Belirli karakterleri silmek için kullanılır. Sayısal aralık (1-9) belirtilebilir ve bu aralıktaki tüm değerler silinir. Veya tırnak içerisine silinmesi istenen karakterler yazılarak o karakterler silinir.
```
echo "abc123def456" | tr -d '0-9'
```
Çıktı: *abcdef*

```
echo "a-b+c=d" | tr -d '-+='
```
Çıktı: *abcd*

### -s
Tekrar eden karakterleri sıkıştırmak için kullanılır.
```
echo "aaabbbbcccdd" | tr -s 'abc'
```
Çıktı: *abcdd*

## head
Herhangi bir dosyanın içeriğini kısaca görmek için kullanılır.

Varsayılan olarak ilk 10 satırı gösterir.
```
head [dosya_adı]
```

Birden fazla dosya ile kullanıldığında iste aynı şekilde bir dosya için yapacağı şeyi birden fazla dosya için de uygular ve hangi çıktının hangi dosyaya ait olduğunu da başlıklarla belirtir.

**-q** (quiet) parametresi kullanıldığında birden çok dosyanın çıktısındaki başlıkları yok sayar ve arada boş satır bırakmaz.

**-v** parametresi ile de tek dosyada bile bu başlığı oluşturur.

### -n
Varsayılan 10 satır yerine satır sayısı belirlemek için kullanılır.
```
head -n [sayı] [dosya_adı]
veya
head -[sayı] [dosya_adı]
```

### -c
Satır yerine byte sayısına göre çıktı verilmesini sağlar.
```
head -c 100 ayarlar.conf
```
Bu komutu girdikten sonra 100 byte (~100 karakter) lık veri ekrana bastırılır.

## tail
Bir veya daha fazla dosyanın sonunu (varsayılan olarak 10 satırını) gösterir.

*head* komutu ile büyük ölçüde benzerdir. head başlığı altındaki parametrelere ek olarak tail da bazı ek parametreler vardır.

### -f
*--follow*

Bir dosyayı takip etmenizi sağlar. Yani bir dosyaya yeni satırlar eklendikçe ekrana basılır.

Genellikle log takibi için kullanılır.

## join
İki metin dosyasını ortak bir alana göre birleştirerek tek çıktı oluşturmayı sağlar.

Verilerin iki metin dosyasındaki ortak alan aynı şekilde sıralanmış olmalıdır.

Eğer iki tarafta ortak olmayan veriler varsa o satırlar çıktıya dahil edilmez.

Varsayılan olarak her iki dosyadaki ilk sütun ortak alan kabul edilir.

### -j
İki dosyadaki ortak alan aynı sütun numarasındaysa kullanılır ve veriler o sütuna göre birleştirilir.

### -1 ve -2
```
-1 [alan_numarası]
-2 [alan_numarası]
```
```
join -1 1 -2 2 a.txt b.txt
```
Bu şekilde 1. dosyanın 1. sütunu ile 2. dosyanın 2. sütununun ortak alan olduğu belirlenir ve buna göre veriler birleştirilir.

### -t
Alan ayıracını belirtmek için kullanılır. Varsayılan olarak boşluk ile ayrıldığı için farklı bir delimiter varsa bu seçenek kullanılır. 

### -a
```
join -a [dosya_numarası] [dosya1] [dosya2]
```
Eşleşmeyen satırları da çıktıya dahil eder. Dosya numarası ile hangi dosyadan gelen eşleşmemiş veri seçilir.

### -o
```
join -o 1.2 1.3 2.2 a.txt b.txt
```
Burada 1.dosyadan 2. sütun, 1. dosyadan 3. sütun ve 2. dosyadan 2. sütun birleştirilir.
Bu parametre sadece istenen değerleri istenilen sırayla birleştirebilmeyi sağlar.

## split
Tek bir dosyayı belirlenen kurallara göre daha küçük yönetilebilir parçalara ayırmak için kullanılır.
Bölünen parçalar "xaa, xab, xac..." şeklinde ayrılır.
Varsayılan olarak 1000 satıra ayrılır.
```
split [seçenekler] [dosya] [önek]
```
En sona girilen önek dosya isimlerini belirlemekte kullanılır. Kullanılmazsa varsayılan adlandırma ile adlandırılır. Kullanıldığında girilen önekin sonuna "aa, ab, ac..." şeklinde adlandırılır.
### -l
Belirlenen satır sayısı kadar parçalara ayrılır.
```
-l [satır_sayısı]
```

### -b
Dosyaları boyutuna göre parçalara ayırmak için boyut belirler.
(..-b 100K, 500M, 10G...)

### -d
Son ekler sayısal bir şekilde adlandırılır. 00, 01, 02...

### -a
Son ekin kaç haneli olacağını belirler. Varsayılan olarak 2 dir.

## tee
Girilen veriyi alır hem ekrana bastırır hem de belirtilen dosyaya yazar.
Genellikle pipe ile kullanılır.
```
{çıktı} | tee [dosya] ...
```
Birden çok dosyaya tek komutla aynı işlem yapılabilir.

### -a --append
**>>** gibi input u dosyanın sonuna ekler.

## nl
Metin dosyalarının satırlarını numaralandırmak için kullanılır.
Boş satırları atlar, numaralandırma şekli değiştirilebilir.

* -b : Neyin numaralandırılacağını belirler.
	* a : Tüm satırları numaralandırır.
	* t : Sadece boş olmayan metin satırlarını numaralandırır. (Varsayılan)
	* n : Hiçbir satırı numaralandırmaz.

