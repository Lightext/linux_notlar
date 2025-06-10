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

