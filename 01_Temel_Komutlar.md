# Temel Komutlar

## ls
Listeleme yapar.
```bash
ls -la
```
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
