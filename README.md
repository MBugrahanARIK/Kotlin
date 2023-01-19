# Kotlin Ders Notları 
# Syntax
+ ; kullanımı kotlinde yok. Kullanınca hata vermez, ama ide kullanmamayı öneri verir.

<br>

# Kişisel Notlarım
## Daha Sonrasında Araştır
+ Paralelleştirme
+ Farklı thread'leri kullanmak
+ Data structures
+ Primitive tipler, referans tipler
+ infix fonksiyonlar

<br>

## Yapmayı Dene
+ Warning'leri çözmeye çalış

## kotlin İş Görüşmelerinde Sorulabilecek Sorular
+ val ve var'ın farkı nedir?
+ const val ve val'ın farkı nedir?

<br>

## Ek Bilgi
+ Android tuş kilidinden çıkılınca bütün widge'ler tekrar yüklenir.

<br>

## Ek Notlar
+ Kotlinde java kodlarını da kullanabiliriz.
+ Kotlin'de primitive tipler direkt olarak tanımlanamaz.
+ Yazdığımız kodlar derlenirken primitive tiplere dönüştürülür.
+ Nullable değişkenler primitive özelliğini kaybeder.
+ [utf-8 encoding bozulması durumunda sorunlar yaşanabileceği için yorumlar bile ingilizce karakterler ile yazılmalı.](https://www.youtube.com/watch?v=eYDZFqnOGC8&t=3226s)
+ [Ülkelerin matematiksel hesaplarda kullanılan ondalık ayırma için kullanılan , veya . sembollerine dikkat edilmeli.](https://youtu.be/eYDZFqnOGC8?t=4984)
	+ try ve catch içerisinde yazarak hem . için hem , için ayrı kodlar yazılarak çözülebilir.
+ Boolean değişkenler için true veya false kullanılır 0 veya 1 kullanılamıyor.


<br>
<br>
<br>

# Değişkenler

+ val = (val)ue - immutable
+ var = (var)iable - mutable
+ val değeri daha sonradan değiştirilemez.
+ Var değeri daha sonradan değişebilir.
+ Değişkene ilk değer ataması veriliyorsa değikene değişken tipi vermek gerekmez.
+ Sayısal değerler sıfırla başlanamaz.
+ Kolay okumak için sayıda _ kullanabilirsiniz. derlemede _'ler kaldırılır.
	+ Sayısal değer olarak 1000000 ve 1_000_000 aynıdır.

## Değişken tanımı
	degisimKarari degiskenAdi: degiskenTuru
	val name: String = "isim"
	val name = "isim"
		
### Nullable değişken tanımlama (değişken isminin sonunda ? var)
	degisimKarari degiskenAdi?: degiskenTuru
	val name: String? = null

> Değişken tanımını ilk olarak val ile yapmak daha mantıklı. Eğer değişken değeri daha sonrasında değişecekse var olarak değiştirebiliriz.

<br>
<br>

# Tür Dönüşümü
İki değer toplanıp yeni bir değişkene değer olarak atanır ve belirli bir tip verilmez ise uygun olan tipe dönüşür.
	
### Kotlin kodlarını kullanarak tür dönüşümü yapmak
	donusturulecekDeger.toDonusturulecekTip()
	x.toInt()
### java özellikleri kullanarak tür dönüşümü yapmak
	donusturulecekTur.parseDonusturulecekTur(donusturulecekDeger)
	Integer.parseInt(x)

<br>
<br>

# Operatörler
### Mantıksal Operatörler
	&& - and - .and(x)	--> ve
	|| - or - .or(x)	--> veya

# Kaynakça
+ ### [Kekod](https://www.youtube.com/@KeKod)
