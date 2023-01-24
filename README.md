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
+ Türkçe karakter kullanılmaz.
+ Sayısal değerler sıfırla başlanamaz.
+ val değeri daha sonradan değiştirilemez.
+ Var değeri daha sonradan değişebilir.
+ Değişkene ilk değer ataması veriliyorsa değikene değişken tipi vermek gerekmez.
+ Kolay okumak için sayıda _ kullanabilirsiniz. derlemede _'ler kaldırılır.
	+ Sayısal değer olarak 1000000 ve 1_000_000 aynıdır.

>val = (val)ue - immutable = değiştirilemez

>var = (var)iable - mutable = değiştirilebilir

<br>

Değişken, değişim kararı, değişken adı, ":" sembolü, değişken türü ve "=" atama operatörü kullanıldıktan sonra değişken değeri verilerek tanımlanır.

```kotlin
// degisimKarari degiskenAdi: degiskenTuru
// degisimKarari degiskenAdi = degiskeneUygunDeger

// Değiştirilemez
val name: String = "isim"
val name2 = "isim" // <-- değişkene ilk değer verilip değişken tipi verilmemiş

// Değiştirilebilir
var name3: String = "isim"
var name4 = "isim" // <-- değişkene ilk değer verilip değişken tipi verilmemiş
```
> Değişken tanımını ilk olarak val ile yapmak daha mantıklı. Eğer değişken değeri daha sonrasında değişecekse var olarak değiştirebiliriz.

Bir değişkenin null değer alabilmesi için değiken tipinin sonuna ? işareti koyulur.
```kotlin
// degisimKarari degiskenAdi?: degiskenTuru
val name: String? = null
```
Nullable olmayan integer değişkenlerin java karşılığı int iken Nullable integer değişkenlerin java karşılığı Integer şeklindedir.
```kotlin
// Java karşılığı int
val number: Int // UnBoxed	: Değişken primitive tip olarak tutulur.

// Java karşılığı Integer
val number2: Int? // Boxed	: Değişken obje referansı olarak tutulmuştur.
```
> Küçük veriler ile çalışırken performans kaybı çok değildir. Ama primitive tip olarak tutulması daha performanslıdır. Değişkene null değer gelmeyecekse, oluşturacağınız değişkeni nullable yapmamanızı öneririm.

```kotlin
fun main() {
    val number: Int = 1000
    val number2: Int? = number
    val number3: Int? = number
    println(number2===number3) // false
    println(number2==number3) // true

    println("-----------------")

    val number4: Int = number
    val number5: Int = number
    println(number4===number5) // true
    println(number4==number5) // true
}
```

Eğer bir değişkene tip verilmez ve direkt null değer ataması yapılırsa, IDE tip çıkarımı yapamaz ve bu değişkenin tipini Nothing? olarak işaretler.
```kotlin
// degisimKarari degiskenAdi = null
val name = null // <-- ile aynıdır --> val name:Nothing? = null 
```
İçerisi null olan bir değişkeni ile direkt matematiksel işlem yapamazsınız. !! veya ? operatörlerini kullanmak gerekir. 
>+ !! değer null ise hata ver
>+ ? eğer değer null ise işlemi yapma
```kotlin
val result: Int? = null
result?.plus(100) // <-- işlemi yapmaz
result!!.plus(100) // <-- hata verir
```
[Değişkenlere daha detaylı bakmak isterseniz](https://kotlinlang.org/docs/basic-types.html)

<br>
<br>

## 2) Tür Dönüşümü
İki değer toplanıp yeni bir değişkene değer olarak atanır ve tip verilmez ise uygun olan tipe dönüşür. İki değer toplandığında eğer ondalıklı sayı değilse, dönüşeceği en az veri alan tip Int'tir
```kotlin
val byte: Byte = 10
val byte2: Byte= 20
val topla = byte+byte2 // <-- Int olarak işaretlendi.
```
Kotlin kodlarını kullanarak tür dönüşümü yapmak
```kotlin
// donusturulecekDeger.toDonusturulecekTip()
x.toInt()
```
Java kodlarını kullanarak tür dönüşümü yapmak
```kotlin
// donusturulecekTur.parseDonusturulecekTur(donusturulecekDeger)
Integer.parseInt(x)
```
> kotlin'de "int degiskenAdi = (int) donusturulecekDeger" gibi bir kullanım yok.

<br>
<br>

## 3) String
Karakterlerden(char) oluşmuş bir dizidir. String ifadeler " çift tırnak içerisine yazılır. Metinsel veriler belirli kurallar çerçevesinde String değişkenlerin içerisine yazılabilir.


String tanımı:

```kotlin
val str: String = "abcd 123"
val str2 = "abcd 123"
```
Birden fazla satırda String bir ifade yazılacaksa """ üç çift tırnak kullanılarak yazılabilir. Buna Raw String Kullanımı deniyor. Yazı boşluklar dahil yazıldığı şeklide çıktısı sağlanır.
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

String bir ifadenin içerisinde belirli ifadeleri dışarıdan veri dahil etmek için \$ simgesini ya da \${ } kullanıyoruz.

```kotlin
fun main() {
	val myInt = 5;
	val myString = "myInt = $myInt"

	println(myString)

	val myString2 = "myInt = ${myInt}"

	println(myString2)
}
```
	#### Program Çıktısı ####
	myInt = 5
	myInt = 5

Değer aldığınız yerin herhangi bir özelliğini kullanacaksanız {}'ler içerisinde yazmanız gerekiyor.
```kotlin
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

<br>

### 3.1) Kaçış Karakterleri
+ \\t - Tab ekler.
+ \\b - Solundan bir karakter siler.
+ \\n - Bulunduğu yerden gelen sonraki string ifadeleri bir alt satırdan başlatır.
+ \\r - Bulunduğu konumu yeni satır başı yapar. Eğer bulunduğu satırda önce yazılar varsa, onları siler.
+ \\' - Tek tırnak ekler.
+ \\" - Çift tırnak ekler.
+ \\\\ - \ karakteri ekler
+ \\$ - $ karakteri ekler

### 3.2) String İfadeler İle Kullanılan Bazı Özellik Ve Fonksiyonlar
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

### 3.3) trimMargin()
Boşlukları trimMargin() fonksiyonu ile silebiliriz. Parantezler içerisinde belirli bir karakter belirtirseniz, her satırın ilk karakterine bakar ve belirtilen karakteri bulduğunda karakter de dahil olmak üzere solundaki boşlukları siler.
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

```kotlin
// Parantezler içerisinde karakter belirtip,
// karakter de dahil olmak üzere boşlukları silmek
fun main() {

	val myString = """
	$!!! Kotlin is interesting.
	!!! Kotlin is sponsored and developed by JetBrains.
"""
	println(myString.trimMargin("$"))
}
```
	#### Program Çıktısı ####
	!!! Kotlin is interesting.
		!!! Kotlin is sponsored and developed by JetBrains.

### 3.4) trimIndent()
Raw String'lerde en soldaki karakteri baz alarak boşlukları silip sol karaktere hizalar.
```kotlin
val rawPineTree = """
	      *
	     ***
	    *****
""".trimIndent()
println(rawPineTree)
```
	#### Program Çıktısı ####
	  *
	 ***
	*****
```kotlin
val rawPineTree = """
	      *
$	     ***
	    *****
""".trimIndent()
println(rawPineTree)
```
	#### Program Çıktısı ####
			  *
	$	     ***
			*****

### 3.5) indices Kullanımı ------------------- TODO -------------------

### 3.6) Bazı Detay Bilgiler

```kotlin
// Kotlinde String Değerler Immutable(değiştirilemez) Şekildedir.
// Değişken içerisindeki karakterleri değiştiremeyiz.
// Ama değişken değerini tamamen değiştirmekte bir sakınca yoktur.

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

```kotlin
// Raw Stringler içerisinde kaçış karakterleri çalışmaz
val myString = """
	|Kotlin is interesting. \n
	|Kotlin is sponsored and developed by JetBrains.
"""
println(myString)
```
	#### Program Çıktısı ####

		|Kotlin is interesting. \n
		|Kotlin is sponsored and developed by JetBrains.

<br>
<br>

## 4) Operatörler
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
+ Eşitlik karşılaştırma operatörleri: ```==```, ```!=``` ve primitive(ilkel) olmayan türler için ```equals()```
+ Referans eşitliği karşılaştırma operatörleri: ```===```, ```!==```
+ Sayısal verilerin karşılaştırlılması: ```<```, ```>```, ```<=```, ```>=``` ve primitive(ilkel) olmayan türler için ```compareTo()```
+ İndexlenmiş verilere erişim operatörü: ```[```, ```]```
+ [Daha detaylı ve farklı operatörlere bakmak için](https://kotlinlang.org/docs/keyword-reference.html#operators-and-special-symbols)

<br>
<br>

## 5) Diziler

Parametreleri vererek dizi oluşturmak
```kotlin
val dizi = arrayOf(13,12,55,23)
val dizi = arrayOf("Ali","Veli","Ayşe","Burcu")
val dizi = arrayOf<Any>(12,"Ali",'a',true)
```
Başlangıç değeri null olan dizi oluşturmak
```kotlin
val dizi = arrayOfNulls<String>(4)
```
Başlangıç değeri verilerek dizi oluşturmak
```kotlin
// Array<diziTuru>(diziUzunlugu){aktarilacakDegerler}
// Bütün değerleri 3 olarak initialize etti.
val dizi = Array<Int>(5){3} // <-- higher-order fonksiyon alıyor
```

Primitive array oluşturmak:
```kotlin
// Bir önceki tanımla benzer ancak higher-order fonksiyon almıyor.
val dizi = IntArray(5) // <-- higher-order fonksiyon almıyor
```
Dizi oluşturma yöntemlerinin java dilindeki karşılıkları:
```kotlin
// Java karşılığı int olan dizi oluşturur.
val dizi = IntArray(5)

// Java karşılığı Integer olan dizi oluşturur.
val dizi = arrayOf(13,12,55,23)

// Java karşılığı String olan dizi oluşturur.
val dizi = arrayOf("Ali","Veli","Ayşe","Burcu")

// Java karşılığı Object olan dizi oluşturur.
val dizi = arrayOf<Any>(12,"Ali",'a',true)

// Java karşılığı String olan dizi oluşturur.
val dizi = arrayOfNulls<String>(4)

// Java karşılığı Integer olan dizi oluşturur.
// Döngü ile bütün değerlerini 3 olarak değiştirir.
val dizi = Array<Int>(5){3}
```
Dizilere erişmek için köşeli parantezleri ve index numaralarını kullanırız. Index numaraları 0'dan başlar.
```kotlin
// Diziden veri almak
// dizi[indexNumber] ve/veya dizi.get(indexNumber)
val dizi = arrayOf(4,2,3,4,5)
dizi[0] // 4
dizi[4] // 5
dizi[2] // 3
dizi.get(1) // 2
```
Diziye değer ataması yapmak
```kotlin
// dizi[indexNumber] = Türe uygun değer ve/veya dizi.set(indexNumber, atanacakDeger)
val dizi = arrayOf(4,2,3,4,5)
dizi[0]=1 // index'i 0 olan 4 değerini 1 ile değiştirdi.
dizi.set(3,2) // index'i 3 olan 4 değerini 2 ile değiştirdi.
```
>dizilere erişmek için dizi[indexNumber] yöntemini kullanmanızı tavsiye ederim.

Dizi değişkenlerini val olarak tanımlamak içindeki değerlerin değişemez olduğu anlamına gelmiyor. Ancak diziyi tanımladığınız değişkene farklı bir atama yapamazsınız.

```kotlin
// Bu kullanım doğrudur.
val dizi = arrayOf(4,2,3,4,5)
dizi[0]=3

// Bu kullanım hatalıdır.
val dizi = arrayOf(4,2,3,4,5)
val dizi2 = arrayOf(3,4,5,6)
dizi = dizi2
```

<br>
<br>

## 6) Range
Belirli bir aralıkta sıralı liste oluşturmaya yarar. İki nokta ".." operatörü ya da rangeTo() fonksiyonu kullanılır.
```kotlin
val numbers = 1..100 // [1,100] 
val numbers2 = 1.rangeTo(100)
```
Büyükten küçüğe doğru liste için .. operatörü çalışmaz downTo() fonksiyonu kullanılır.

```kotlin
val numbers = 100..1 // <-- Çalışır ancak boş liste döner
val numbers2 = 100.downTo(1)
val numbers3 = 100 downTo 1 // <-- infix fonksiyondur.
```
Oluşturduğumuz listenin tersini almak için reversed() özelliğini kullanabiliriz.
```kotlin
// Parantezli kullanım şarttır.
val numbers1 = 1.rangeTo(100).reversed()
val numbers2 = 100.downTo(1).reversed()
```
Başlangıç değeri dahil, bitiş değeri dahil olmayan liste için until() fonksiyonu kullanılır
```kotlin
val numbers2 = 1.until(100) // [1,100)
val numbers3 = 1 until 100 // <-- infix fonksiyondur.
val numbers = 1.rangeTo(99) // Aynı işlevi yapar
```
Belirli bir artış miktarı vererek liste oluşturmak
```kotlin
val numbers = 1..100 step(2) // 1,3,5,...,97,99
val numbers2 = 1.rangeTo(100) step 2 // <-- step infix fonksiyondur.
val numbers = 100.downTo(1) step(2) // 100,98,96,...,4,2
```
Oluşturduğumuz range hakkında bazı bilgileri alabiliyoruz.
```kotlin
val numbers = 100.downTo(1) step(2)
println(numbers.step)
println(numbers.first)
println(numbers.last)
```

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

