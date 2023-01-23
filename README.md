# Kotlin Ders Notları 
## Syntax Ve Temel Bilgiler
+ Kotlinde java kodlarını da kullanabiliriz.
+ ; kullanımı kotlinde yok. Kullanınca hata vermez, ama ide kullanmamayı öneri verir.
+ Kod parçalarına isimlendirme yaparken türkçe karakter kullanılmaz. (Genel bilgi)

### Yorum Satırları:
+ **//:** tek satırda yorum yazma için kullanılır.
+ **/\* yorum \*/:** çoklu satırda yorum yazmak için kullanılır
```kotlin
// Tek satırda yorum
/*	Çoklu 
		satırda
			yorum */
```

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

<br>
<br>

## 1) Değişkenler
+ val = (val)ue - immutable
+ var = (var)iable - mutable
+ val değeri daha sonradan değiştirilemez.
+ Var değeri daha sonradan değişebilir.
+ Değişkene ilk değer ataması veriliyorsa değikene değişken tipi vermek gerekmez.
+ Sayısal değerler sıfırla başlanamaz.
+ Kolay okumak için sayıda _ kullanabilirsiniz. derlemede _'ler kaldırılır.
	+ Sayısal değer olarak 1000000 ve 1_000_000 aynıdır.

<br>

### 1.1) Değişken tanımı

```kotlin
// degisimKarari degiskenAdi: degiskenTuru
val name: String = "isim"
val name = "isim"
```
### 1.2) Nullable değişken tanımlama
```kotlin
// degisimKarari degiskenAdi?: degiskenTuru
val name: String? = null
```
> Değişken tanımını ilk olarak val ile yapmak daha mantıklı. Eğer değişken değeri daha sonrasında değişecekse var olarak değiştirebiliriz.

### 1.3) Tür Dönüşümü
İki değer toplanıp yeni bir değişkene değer olarak atanır ve belirli bir tip verilmez ise uygun olan tipe dönüşür.
	
### 1.3.1) Kotlin kodlarını kullanarak tür dönüşümü yapmak
```kotlin
// donusturulecekDeger.toDonusturulecekTip()
x.toInt()
```
### 1.3.2) Java kodlarını kullanarak tür dönüşümü yapmak
```kotlin
// donusturulecekTur.parseDonusturulecekTur(donusturulecekDeger)
Integer.parseInt(x)
```
> kotlin'de "int degiskenAdi = (int) donusturulecekDeger" gibi bir kullanım yok.

<br>
<br>

## 2) String
Karakterlerden(char) oluşmuş bir dizidir. String ifadeler " çift tırnak içerisine yazılır. Metinsel veriler belirli kurallar çerçevesinde String değişkenlerin içerisine yazılabilir.


### 2.1)Basit bir String tanımı:

```kotlin
val str = "abcd 123"
val str2: String = "abcd 123"
```

### 2.2) Kaçış Karakterleri
+ \\t - Tab ekler.
+ \\b - Solundan bir karakter siler.
+ \\n - Bulunduğu yerden gelen sonraki string ifadeleri bir alt satırdan başlatır.
+ \\r - Bulunduğu konumu yeni satır başı yapar. Eğer bulunduğu satırda önce yazılar varsa, onları siler.
+ \\' - Tek tırnak ekler.
+ \\" - Çift tırnak ekler.
+ \\\\ - \ karakteri ekler
+ \\$ - $ karakteri ekler


### 2.3) Raw String Kullanımı
Birden fazla satırda String bir ifade yazılacaksa """ üç çift tırnak kullanılarak yazılabilir. Yazı boşluklar dahil yazıldığı şeklide çıktısı sağlanır.
```kotlin
fun main() {

	val myString = """
	for (character in "Hey!")
		println(character)
"""
    print(myString)
}
```
	#### Program çıktısı ####
		for (character in "Hey!")
			println(character)


### 2.4) trimMargin()
Boşlukları trimMargin() fonksiyonu ile silebiliriz.
```kotlin
fun main() {

	println("trimMargin() fonksiyonu kullanmadan program çıktısı:")

	val myString = """
	|Kotlin is interesting.
	|Kotlin is sponsored and developed by JetBrains.
"""
	println(myString)

	println("trimMargin() fonksiyonu kullanarak program çıktısı:\n")
	println(myString.trimMargin())
}
```
	#### Program Çıktısı ####
	trimMargin() fonksiyonu kullanmadan program çıktısı:

		|Kotlin is interesting.
		|Kotlin is sponsored and developed by JetBrains.

	trimMargin() fonksiyonu kullanarak program çıktısı:

	Kotlin is interesting.
	Kotlin is sponsored and developed by JetBrains.

Belirli karakterleri silmek için
```kotlin
fun main() {

	val myString = """
	!!! Kotlin is interesting.
	!!! Kotlin is sponsored and developed by JetBrains.
"""
	println(myString.trimMargin("!!! "))
}
```
	#### Program Çıktısı ####
	Kotlin is interesting.
	Kotlin is sponsored and developed by JetBrains.

### 2.5) trimIndent() -----------------------------------------------

### 2.6) String Şablon İfadeler
String bir ifadenin içerisinde belirli ifadeleri dışarıdan dahil etmek veya küçük kodlar yazmak için $ simgesini kullanıyoruz.
```kotlin
fun main() {
	val myInt = 5;
	val myString = "myInt = $myInt"

	println(myString)
}
```
	#### Program Çıktısı ####
	myInt = 5

```kotlin
// Değer aldığınız yerin herhangi bir özelliğini kullanacaksanız {}'ler içerisinde yazmanız gerekiyor.
fun main() {
	val a = 5
	val b = 6
	val myString = """
	|${if (a > b) a else b}
	"""
	println("Larger number is: ${myString.trimMargin()}")
}
```
	#### Program Çıktısı ####
	Larger number is: 6

### 2.7) String İfadeler İle Kullanılan Bazı Fonksiyonlar
+ **length:** String karakter uzunluğunu verir.
+ **compareTo:** String ifadeyi belirtilen nesneyle karşılaştırır. Nesne belirtilen nesneye eşitse 0 döndürür.
+ **get:** Belirtilen bir konumdaki karakteri geri döndürür. Konum 0'dan başlar.
+ **plus:** İki String ifadeyi birleştirmeye yarar. Aynı şekilde + operatörünü kullanarak da aynı işlev yapılabilir.
+ **subSequence:** Belirtilen konumlar arasındaki String ifadeyi geri döndürür.
```kotlin
fun main() {

	val s1  = "Hey there!"
	val s2 = "Hey there!"
	var result: String

	println("Length of s1 string is ${s1.length}.")

	result = if (s1.compareTo(s2) == 0) "equal" else "not equal"
	println("Strings s1 and s2 are $result.")

	// s1.get(2) is equivalent to s1[2]
	println("Third character is ${s1.get(2)}.")

	result = s1.plus(" How are you?") // result = s1 + " How are you?"
	println("result = $result")

	println("Substring is \"${s1.subSequence(4, 7)}\"")

}
```

### 2.8) Bazı Detay Bilgiler

```kotlin
// Kotlinde String Değerler Immutable(değiştirilemez) Şekildedir.
// Değişken içerisindeki karakterleri değiştiremeyiz. Ama değişken değerini tamamen değiştirmekte bir sakınca yoktur.

// Hatalı kullanım.
var myString = "Hey!"
myString[0] = 'h'

// Doğru kullanım.
var myString = "Hey!"
myString = "hey!"

// String bir ifade ile (önde olmak koşulu ile) farklı bir ifadeyi toplarsanız, sonuç String olur.
// String ifadenin önünde farklı bir ifade ile toplarsanız kod çalışmaz.
val numbersValue: String = "value" + (4 + 2 + 8) // <-- çalışır
val numbersValue: String = (4 + 2 + 8) + "value" // <-- çalışmaz

```



<br>
<br>

## 3) Operatörler
+ Matematiksel operatörler: ```+```, ```-```, ```*```, ```/```, ```%```
+ Mantıksal operatörler:
```kotlin 
&& - and - .and(x)	--> ve
|| - or - .or(x)	--> veya
! - not - .not(x)	--> değilse
```
+ Atama operatörü: ``` = ```
+ Arttırılmış atama operatörleri: ```+=```, ```-=```, ```*=```, ```/=```, ```%=```
+ Arttırma operatörleri: ```++```, ```--```
+ Eşitlik karşılaştırma operatörleri: ```==```, ```!=```
+ Referans eşitliği karşılaştırma operatörleri: ```===```, ```!==``` ve primitive(ilkel) olmayan türler için ```equals()```
+ Sayısal verilerin karşılaştırlılması: ```<```, ```>```, ```<=```, ```>=``` ve primitive(ilkel) olmayan türler için ```compareTo()```
+ İndexlenmiş verilere erişim operatörü: ```[```, ```]```
+ [Daha detaylı ve farklı operatörlere bakmak için](https://kotlinlang.org/docs/keyword-reference.html#operators-and-special-symbols)

<br>
<br>

## 4) Diziler
### 4.1) Dizi oluşturmak
```kotlin
// Parametreleri vererek dizi oluşturmak
val dizi = arrayOf(13,12,55,23)
val dizi = arrayOf("Ali","Veli","Ayşe","Burcu")
val dizi = arrayOf<Any>(12,"Ali",'a',true)

// Başlangıç değeri null olan dizi oluşturmak
val dizi = arrayOfNulls<String>(4)

// Başlangıç değeri verilerek dizi oluşturmak
// Array<diziTuru>(diziUzunlugu){aktarilacakDegerler}
// Bütün değerleri 3 olarak initialize etti.
val dizi = Array<Int>(5){3} // <-- higher-order fonksiyon alıyor

// Primitive array tanımı
// Bir önceki tanımla benzer ancak higher-order fonksiyon almıyor.
val dizi = CharArray(5) // <-- higher-order fonksiyon almıyor

// Dizi değişkenlerini val olarak tanımlamak içindeki değerlerin değişemez olduğu anlamına gelmiyor. Ancak diziyi tanımladığınız değişkene farklı bir atama yapamazsınız.

	// Bu kullanım doğrudur.
    val dizi = arrayOf(4,2,3,4,5)
	dizi[0]=3

	// Bu kullanım hatalıdır.
    val dizi = arrayOf(4,2,3,4,5)
    val dizi2 = arrayOf(3,4,5,6)
    dizi = dizi2
```
### 4.2) Dizilere Erişmek
```kotlin
// Diziden veri almak
// dizi[indexNumber] ve/veya dizi.get(indexNumber)
val dizi = arrayOf(4,2,3,4,5)
dizi[0] // 4
dizi[4] // 5
dizi[2] // 3
dizi.get(1) // 2


// Diziye değer ataması yapmak
// dizi[indexNumber] = Türe uygun değer ve/veya dizi.set(indexNumber, atanacakDeger)
val dizi = arrayOf(4,2,3,4,5)
dizi[0]=1 // index'i 0 olan 4 değerini 1 ile değiştirdi.
dizi.set(3,2) // index'i 3 olan 4 değerini 2 ile değiştirdi.
```
>dizilere erişmek için dizi[indexNumber] yöntemini kullanmanızı tavsiye ederim.

<br>
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
+ #### [Kotlin Official](https://kotlinlang.org/)
+ #### [Kekod](https://www.youtube.com/@KeKod)
+ #### [Programiz -> Kotlin String and String Templates](https://www.programiz.com/kotlin-programming/string)

