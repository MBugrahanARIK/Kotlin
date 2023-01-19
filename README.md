# Kotlin Ders Notları 
## Syntax Ve Temel Bilgiler
+ Kotlinde java kodlarını da kullanabiliriz.
+ ; kullanımı kotlinde yok. Kullanınca hata vermez, ama ide kullanmamayı öneri verir.

## İçerik
1. [Değişkenler](#1-de%C4%9Fi%C5%9Fkenler)
	1. [Değişken tanımı](#de%C4%9Fi%C5%9Fken-tan%C4%B1m%C4%B1)
	2. [Nullable değişken tanımlama](#nullable-de%C4%9Fi%C5%9Fken-tan%C4%B1mlama-de%C4%9Fi%C5%9Fken-isminin-sonunda--var)
2. [Tür Dönüşümü](#2-t%C3%BCr-d%C3%B6n%C3%BC%C5%9F%C3%BCm%C3%BC)
	1. [Kotlin kodlarını kullanarak tür dönüşümü yapmak](#kotlin-kodlar%C4%B1n%C4%B1-kullanarak-t%C3%BCr-d%C3%B6n%C3%BC%C5%9F%C3%BCm%C3%BC-yapmak)
	2. [Java kodlarını kullanarak tür dönüşümü yapmak](#java-kodlar%C4%B1n%C4%B1-kullanarak-t%C3%BCr-d%C3%B6n%C3%BC%C5%9F%C3%BCm%C3%BC-yapmak)
3. [Operatörler](#3-operat%C3%B6rler)
	1. [Mantıksal Operatörler](#mant%C4%B1ksal-operat%C3%B6rler)
4. [Kişisel Notlarım](#ki%C5%9Fisel-notlar%C4%B1m)
5. [Kaynakça](#kaynak%C3%A7a)

## 1) Değişkenler

+ val = (val)ue - immutable
+ var = (var)iable - mutable
+ val değeri daha sonradan değiştirilemez.
+ Var değeri daha sonradan değişebilir.
+ Değişkene ilk değer ataması veriliyorsa değikene değişken tipi vermek gerekmez.
+ Sayısal değerler sıfırla başlanamaz.
+ Kolay okumak için sayıda _ kullanabilirsiniz. derlemede _'ler kaldırılır.
	+ Sayısal değer olarak 1000000 ve 1_000_000 aynıdır.

#### Değişken tanımı
	degisimKarari degiskenAdi: degiskenTuru
	val name: String = "isim"
	val name = "isim"
		
#### Nullable değişken tanımlama (değişken isminin sonunda ? var)
	degisimKarari degiskenAdi?: degiskenTuru
	val name: String? = null

> Değişken tanımını ilk olarak val ile yapmak daha mantıklı. Eğer değişken değeri daha sonrasında değişecekse var olarak değiştirebiliriz.

<br>

## 2) Tür Dönüşümü
İki değer toplanıp yeni bir değişkene değer olarak atanır ve belirli bir tip verilmez ise uygun olan tipe dönüşür.
	
#### Kotlin kodlarını kullanarak tür dönüşümü yapmak
	donusturulecekDeger.toDonusturulecekTip()
	x.toInt()
#### Java kodlarını kullanarak tür dönüşümü yapmak
	donusturulecekTur.parseDonusturulecekTur(donusturulecekDeger)
	Integer.parseInt(x)
> kotlin'de "int degiskenAdi = (int) donusturulecekDeger" gibi bir kullanım yok.

<br>

## 3) Operatörler
#### Mantıksal Operatörler
	&& - and - .and(x)	--> ve
	|| - or - .or(x)	--> veya

<br>

## Kişisel Notlarım
#### Daha Sonrasında Araştır
+ Paralelleştirme
+ Farklı thread'leri kullanmak
+ Data structures
+ Primitive tipler, referans tipler
+ infix fonksiyonlar
#### Yapmayı Dene
+ Warning'leri çözmeye çalış
#### Kotlin İş Görüşmelerinde Sorulabilecek Sorular
+ val ve var'ın farkı nedir?
+ const val ve val'ın farkı nedir?
#### Ek Bilgi
+ Android tuş kilidinden çıkılınca bütün widge'ler tekrar yüklenir.
#### Ek Notlar
+ Kotlin'de primitive tipler direkt olarak tanımlanamaz.
+ Yazdığımız kodlar derlenirken primitive tiplere dönüştürülür.
+ Nullable değişkenler primitive özelliğini kaybeder.
+ [utf-8 encoding bozulması durumunda sorunlar yaşanabileceği için yorumlar bile ingilizce karakterler ile yazılmalı.](https://www.youtube.com/watch?v=eYDZFqnOGC8&t=3226s)
+ [Ülkelerin matematiksel hesaplarda kullanılan ondalık ayırma için kullanılan , veya . sembollerine dikkat edilmeli.](https://youtu.be/eYDZFqnOGC8?t=4984)
	+ try ve catch içerisinde yazarak hem . için hem , için ayrı kodlar yazılarak çözülebilir.
+ Boolean değişkenler için true veya false kullanılır 0 veya 1 kullanılamıyor.

<br>

## Kaynakça
+ #### [Kekod](https://www.youtube.com/@KeKod)
