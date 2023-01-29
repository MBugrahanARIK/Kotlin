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

İki nullable değişken aynı değişkenden referans alsa da hafızada referans ettikleri yerler farklıdır. Nullable olmayan değişkenlerde ise aynıdır.

```kotlin
fun main() {
    val number: Int = 1000
    val number2: Int = number
    val number3: Int = number
    println(number2 === number3) // false
    println(number2 == number3) // true

    println("-----------------")

    val number4: Int = number
    val number5: Int = number
    println(number4 === number5) // true
    println(number4 == number5) // true
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
// Hata: Exception in thread "main" java.lang.NullPointerException
```

>[Değişkenlere daha detaylı bakmak isterseniz](https://kotlinlang.org/docs/basic-types.html)

<br>
<br>

## 2) Tür Dönüşümü
İki değer toplanıp yeni bir değişkene değer olarak atanır ve tip verilmez ise uygun olan tipe dönüşür. İki değer toplandığında eğer ondalıklı sayı değilse, dönüşeceği en az veri alan tip Int'tir

```kotlin
val byte: Byte = 10
val byte2: Byte = 20
val topla = byte + byte2 // <-- Int olarak işaretlendi.
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
    val myInt = 5
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

    val s1 = "Hey there!"
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

>[Daha detaylı ve farklı operatörlere bakmak için](https://kotlinlang.org/docs/keyword-reference.html#operators-and-special-symbols)

<br>
<br>

## 5) Diziler

Parametreleri vererek dizi oluşturmak

```kotlin
val dizi = arrayOf(13, 12, 55, 23)
val dizi = arrayOf("Ali", "Veli", "Ayşe", "Burcu")
val dizi = arrayOf<Any>(12, "Ali", 'a', true)
```

Başlangıç değeri null olan dizi oluşturmak

```kotlin
val dizi = arrayOfNulls<String>(4)
```

Başlangıç değeri verilerek dizi oluşturmak

```kotlin
// Array<diziTuru>(diziUzunlugu){aktarilacakDegerler}
// Bütün değerleri 3 olarak initialize etti.
val dizi = Array<Int>(5) { 3 } // <-- higher-order fonksiyon alıyor
```

Primitive array oluşturmak:

```kotlin
// Bir önceki tanımla benzer ancak higher-order fonksiyon almıyor.
// ByteArray() ShortArray() IntArray()
// LongArray() DoubleArray() FloatArray()
val dizi = IntArray(5) // <-- higher-order fonksiyon almıyor
```

Dizi oluşturma yöntemlerinin java dilindeki karşılıkları:

```kotlin
// Java karşılığı int olan dizi oluşturur.
val dizi = IntArray(5)

// Java karşılığı Integer olan dizi oluşturur.
val dizi = arrayOf(13, 12, 55, 23)

// Java karşılığı String olan dizi oluşturur.
val dizi = arrayOf("Ali", "Veli", "Ayşe", "Burcu")

// Java karşılığı Object olan dizi oluşturur.
val dizi = arrayOf<Any>(12, "Ali", 'a', true)

// Java karşılığı String olan dizi oluşturur.
val dizi = arrayOfNulls<String>(4)

// Java karşılığı Integer olan dizi oluşturur.
// Döngü ile bütün değerlerini 3 olarak değiştirir.
val dizi = Array<Int>(5) { 3 }
```

Dizilere erişmek için köşeli parantezleri ve index numaralarını kullanırız. Index numaraları 0'dan başlar.

```kotlin
// Diziden veri almak
// dizi[indexNumber] ve/veya dizi.get(indexNumber)
val dizi = arrayOf(4, 2, 3, 4, 5)
dizi[0] // 4
dizi[4] // 5
dizi[2] // 3
dizi.get(1) // 2
```

Diziye değer ataması yapmak

```kotlin
// dizi[indexNumber] = Türe uygun değer ve/veya dizi.set(indexNumber, atanacakDeger)
val dizi = arrayOf(4, 2, 3, 4, 5)
dizi[0]=1 // index'i 0 olan 4 değerini 1 ile değiştirdi.
dizi.set(3,2) // index'i 3 olan 4 değerini 2 ile değiştirdi.
```

>Dizilere erişmek için dizi[indexNumber] yöntemini kullanmanızı tavsiye ederim.

Dizi değişkenlerini val olarak tanımlamak içindeki değerlerin değişemez olduğu anlamına gelmiyor. Ancak diziyi tanımladığınız değişkene farklı bir atama yapamazsınız.

```kotlin
// Bu kullanım doğrudur.
val dizi = arrayOf(4, 2, 3, 4, 5)
dizi[0]=3

// Bu kullanım hatalıdır.
val dizi = arrayOf(4, 2, 3, 4, 5)
val dizi2 = arrayOf(3, 4, 5, 6)
dizi = dizi2
// Hata: Val cannot be reassigned
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
val numbers = 1..100 step (2) // 1,3,5,...,97,99
val numbers2 = 1.rangeTo(100) step 2 // <-- step infix fonksiyondur.
val numbers = 100.downTo(1) step (2) // 100,98,96,...,4,2
```

Oluşturduğumuz range hakkında bazı bilgileri alabiliyoruz.

```kotlin
val numbers = 100.downTo(1) step (2)
println(numbers.step)
println(numbers.first)
println(numbers.last)
```

<br>
<br>


## 7) Kontrol Yapıları
### 7.1) if - else - else if

+ if kontrol yapısının parantezleri içerisi doğru veya yanlış belirtecek şeklide değer almalıdır.
+ Yazacağımız kodları süslü parantezler içerisine yazarız.
+ if süslü parantezleri içerisindeki kod, kontrolün doğru olması durumunda çalışır.
+ Kontrolün yanlış olması durumunda else süslü parantezleri içerisi çalışır.
+ Sadece if bloğu yazılabilir ancak sadece else bloğu yazılamaz.

```kotlin
fun main() {
    // State kullanımı
    print("Öğrenci misiniz?: ")

    val answer = readln() // <-- Kullanıcıdan değer almak için kullanıyoruz

    if (answer == "Evet") { // <-- Kontrol ediyoruz.
        println("Öğrenci") // <-- Kontrol sonucu doğru ise burası çalışır.
    } else {
        println("Öğrenci Değil") // <-- Kontrol sonucu yanlış ise burası çalışır.
    }
}
```

Kontrolün sonucu bir değişkene değer olarak atanacaksa, değişken atama operatöründen sonra if else blokları yazılabilir ve atanacak değerler süslü parantezler içerisinde verilebilir. {} içerisindeki son satir değer olarak verilir.

```kotlin
fun main() {
    // Expression kullanımı
    print("Öğrenci misiniz?: ")

    val answer = readln()

    val ogrenci = if (answer == "Evet") { // <-- Kontrol (gelen değer "Evet ise")
        "Öğrenci" // <-- Kontrol sonucu doğru ise değişkene değer olarak atanacak değer
    } else {
        "Öğrenci Değil" // <-- Kontrol sonucu yanlış ise değişkene değer olarak atanacak değer
    }
}
```

>[Expression kullanımları hakkında daha fazla bilgi almak için](https://kotlinlang.org/spec/expressions.html#expressions)

Kotlinde expression kullanımı olduğundan dolayı ternary operatörü yoktur.

```kotlin
val isStudent = false
val isStudent2 = isStudent ? "true" : "false" // <-- Şeklinde kullanılmaz
val isStudent2 = if (isStudent2) "true" else "false" // <-- Şeklinde kullanılabilir.
```

Aynı değer için birden fazla kontrol sağlanması ve sağlandığında belirli bir işlemin yapılması isteniyorsa, else if kullanılır. (Şartlar teker teker kontrol edilir. Eğer şartı sağlayan bir kontrol bloğuna denk gelinir ise şartı sağlayan blok çalışır ve diğer şart blokları kontrol edilmez, atlanır.)

```kotlin
fun main() {
    print("Notunuz: ")
    val not = readln()
    if (not.toInt() >= 85) {
        println("Harf Notunuz: AA")
    } else if (not.toInt() >= 75) {       // Eğer not 75 - 84 arası girildiyse
        println("Harf Notunuz: BA")   // <-- Bu alan çalışır.
    } else if (not.toInt() >= 65) {
        println("Harf Notunuz: BB")
    } else if (not.toInt() >= 50) {
        println("Harf Notunuz: CC")
    } else {
        println("Harf Notunuz: FF")
    } // Diğer kontroller atlanır ve bu satırdan kod akmaya devam eder.
}
```

[Yukarıdaki örnekte birden fazla if bloğu şeklinde yazılsaydı ve 100 değeri girilseydi koşulu sağlayan bütün if blokları çalışırdı.](https://youtu.be/q9zuhv0ErXg?t=5413)

```kotlin
fun main() {
    print("Notunuz: ")
    val not = readln()
    if (not.toInt() >= 85) {
        println("Harf Notunuz: AA")
    }
    if (not.toInt() >= 75) {
        println("Harf Notunuz: BA")
    }
    if (not.toInt() >= 65) {
        println("Harf Notunuz: BB")
    }
    if (not.toInt() >= 50) {
        println("Harf Notunuz: CC")
    }
    if (not.toInt() < 50) {
        println("Harf Notunuz: FF")
    }
}
```

	#### Program Çıktısı ####
	Harf Notunuz: AA
	Harf Notunuz: BA
	Harf Notunuz: BB
	Harf Notunuz: CC

Birden fazla koşulun kontolünü aynı if parantezler içerisinde kontrol etmek istiyorsak Mantıksal operatörleri kullanabiliriz.

+ && - and - .and(x)	--> ve
+ || - or - .or(x)	--> veya
+ ! - not - .not(x)	--> değilse

Yukarıda birden fazla çıktı veren ard arda if oluşturduğumuz blokta mantıksal operatörleri deneyecek olursak. Alttaki kodda 0-100 arasında verilen değerlerde sadece tek blok çalışacaktır.

```kotlin
fun main() {
    print("Notunuz: ")
    val not = readln()
    if (not.toInt() >= 85 && not.toInt() <= 100) {
        println("Harf Notunuz: AA")
    }
    if (not.toInt() >= 75 && not.toInt() < 85) {
        println("Harf Notunuz: BA")
    }
    if (not.toInt() >= 65 && not.toInt() < 75) {
        println("Harf Notunuz: BB")
    }
    if (not.toInt() >= 50 && not.toInt() < 65) {
        println("Harf Notunuz: CC")
    }
    if (not.toInt() < 50 && not.toInt() >= 0) {
        println("Harf Notunuz: FF")
    }
}
```

> Bu kod her if bloğunun için kontrol edildiğinden dolayı performans kaybına sebep olacaktır. Mantıksal operatörlere örnek göstermek amacı ile yazılmıştır. Doğru bir if kullanımı değildir. else if kullanılmalıydı.

iki sayısal değer karşılaştırılıyorsa ve değerlerin tipleri farklı ise ilk önce tür dönüşümü yapılmalıdır.

```kotlin
if(10==10L.toInt()){ // <-- Çalışır
    print("true")
}
if(10.toLong()==10L){ // <-- Çalışır
    print("true")
}
if(10==10L){ // <-- Çalışmaz
    print("true")
}
```

<br>

### 7.2) when
switch case yapısı ile genel olarak aynıdır. case içerisine break komutu yazmaya gerek yoktur. Parantezler içerisine kontrol edilecek deger yazılır. Hangi değerle karşılaştırılacağı, "->" operatörü ve yapılacak işlemler yazılır. Bir satırda farklı koşulların aynı işlemi yapmasını istiyorsak koşulları virgül ile ayırırız.

```kotlin
fun main() {
    val ulke = readln()
    when (ulke) {
        "tr", "az" -> println("Türkiye") // <-- Virgül veya anlamındadır.
        "fr" -> println("Fransa")
        "jp" -> println("Japonya")
        "us" -> println("Amerika")
    }
}
```

İşlemleri süslü parantezler içerisinde de yazabiliriz.

```kotlin
fun main() {
    // {} ile kullanım
    val ulke = readln()
    when (ulke) {
        "tr", "az" -> {
            println("Türkiye")
        }

        "fr" -> {
            println("Fransa")
        }

        "jp" -> {
            println("Japonya")
        }

        "us" -> {
            println("Amerika")
        }
    }
}
```

if - else tarzında da kullanabiliz. Kontrol edilecek değer parantezler içerisinde olmaz, kontrol eden değerin olduğu bölümde yazılır. when parantezleri kaldırılır. Bu kullanımın getirisi &&, ||, and, or, xor gibi ifadeleri kullanabilmemizdir. 

```kotlin
fun main() {
    val ulke = readln()
    when { // <-- parantezler silinir
        ulke == "tr" || ulke == "az" -> println("Türkiye")
        ulke == "fr" -> println("Fransa")
        ulke == "jp" -> println("Japonya")
        ulke == "us" -> println("Amerika")
    }
}
```

if - else gibi expression kullanımına sahiptir. Hiç bir koşulun sağlanmadığı durumda değişkene değer atayabilmek için else bloğu yazmak zorunludur.

```kotlin
fun main() {
    val ulkeKisaltmasi = "tr"
    val ulkeAdi = when (ulkeKisaltmasi) { // <-- parantezler silinir
        "tr", "az" -> {
            println("Türkiye") // Gelen değer tr olduğu için ilk önce Türkiye yazdırır
            "Türkiye" // sonra değişkene Türkiye değerini atar.
        }

        "fr" -> {
            println("Fransa")
            "Fransa"
        }

        "jp" -> {
            println("Japonya")
            "Japonya"
        }

        "us" -> {
            println("Amerika")
            "Amerika"
        }

        else -> { // <-- else bloğu
            println("Bilinmeyen ülke kodu.")
            "x"
        }
    }
}
```

> is anahtar sözcüğü bir class'ın referansı olup olmadığına bakar

<br>
<br>

## 8) Döngüler
Aynı işlemi belirli şartlan sağlandığı taktirde tekrar terkar belirli bir düzende yapmaya yarar.

### 8.1) For Döngüsü

```kotlin

fun main() {
    // C#, java'daki gibi for(int i=0;i<10;i++) şeklinde bir yapıda değildir.
    // for(value in Range), for(value in Array) benzeri bir yapısı vardır.
    // value ismi bir belirteçtir istenilen mantıklır bir şey yazılabilir
    for (value in 1..100) {
        println("$value") // 1'den 100'e kadar yazı yazar.
    }
}
```

Bir dizi ile kullanımı

```kotlin
fun main() {
    // Dizideki verileri teker teker yazar.
    val name = arrayOf("Ali", "Ayşe", "Tezcan", "Veli", "Burak")

    for (value in name) {
        println(value) // <-- Zaten String bir değer
    }
}
```
Bir diziyiden veriyi indexleri ile çekmek

```kotlin
fun main() {
    val name = arrayOf("Ali", "Ayşe", "Tezcan", "Veli", "Burak")

    for (value in name.indices) {
        println("$value.indexteki değer: ${name[value]}")
    }
}
```
Bir diziden hem index bilgisini hem içindeki veriyi almak. ([Destructuring declarations](https://kotlinlang.org/docs/destructuring-declarations.html) kullanımı)

```kotlin
fun main() {
    val name = arrayOf("Ali", "Ayşe", "Tezcan", "Veli", "Burak")

    for ((index, value) in name.withIndex()) {
        println("$index.indexteki değer: $value")
    }
}
```

### 8.2) Repeat
Parantezler içerisine kaç defa tekrarlanacağı yazar. "it" ile hangi aşamada olduğunu görebiliriz. it 0'dan başlar.

```kotlin
fun main() {
    // repeat(size){}
    // aşağıdaki program 0'dan 9'a kadar rakamları yazacak
    repeat(10) { // <-- higher-order fonksiyon
        println(it)
    }
}
```

### 8.3) While
Diğer dillerdeki kullanımı ile aynıdır. parantezler içerisine koşul verilir, koşul doğru olduğu taktirde döngü süslü parantezleri içerisindeki işlemler yapılır.

```kotlin
fun main() {
    // 1'den 10'a kadar sayıları yazdıran program
    var i = 0
    while (i < 10) {
        println(++i) // i++ olsaydı 0'dan 9'a kadar yazardı
    }
}
```

### 8.4) Continue, Break Ve Label
Döngüde ilerlerken eğer kod continue karşılaşırsa döngü süslü parantezleri içerisinde continue'dan sonraki kodları işlemeden bulunduğu döngünün bir sonraki adımına geçer.

```kotlin
fun main() {
    // Sadece çift sayıları yazan for döngüsü
    for (value in 1..100) {
        if (value % 2 == 1) { // <-- Eğer 2'ye bölümünden kalan 1 ise
            continue // <-- Devam et
        }
        println(value)
    }
}
```

Birden fazla döngüde continue'nun farklı bir döngüden devam etmesini istersek

```kotlin
fun main() {
    // iç içe for döngülerinde continue'nun label kullanarak ilk döngüye dönmesi
    // Dönülecek döngü için labelAdi@
    // Dömeyi istediğimiz kod için continue@labelAdi
    // Aşağıdaki kod 1 ve 2 rakamlarını yazcak ve bunu 5 defa tekrarlayacaktır.
    returnLabel@ for (i in 1..5) {
        for (j in 1..5) {
            if (j == 3) { // <-- j eğer 3'e eşitse
                continue@returnLabel // <-- Belirtilen label'a dön
            }
            println(j)
        }
    }
}
```

Döngüde ilerlerken eğer kod break karşılaşırsa döngü süslü parantezleri içerisinde break'den sonraki kodları işlemez ve bulunduğu döngüyü kırar(döngüden çıkar).

```kotlin
fun main() {
    // 1'den 5'e kadar olan rakamları yazdıran for döngüsü
    for (value in 1..100) {
        if (value % 5 == 0) { // <-- Eğer 5'e bölümünden kalan 0 ise
            break // <-- Döngüyü kır
        }
        println(value)
    }
}
```

İç içe döngülerde break kullanıldığında, içteki döngüyü kırar ve bir üstteki döngüden devam eder.

```kotlin
fun main() {
    // İkinci döngünün j değeri 3 olduğunda döngü kırılacak ve ilk döngüden devam edecek
    // Aşağıdaki kod 1 ve 2 rakamlarını yazcak ve bunu 5 defa tekrarlayacaktır.
    for (i in 1..5) {
        for (j in 1..5) {
            if (j == 3) { // <-- j eğer 3'e eşitse
                break // Bu döngüyü kır
            }
            println(j)
        }
    }
}
```
Label ve break kullanarak istenilen döngü için break kodunun işlenmesi ve döngüden çıkmak.

```kotlin
fun main() {
    // İkinci döngünün j değeri 3 olduğunda ilk döngü kırılacak
    // Aşağıdaki kod 1 ve 2 rakamlarını yazcak
    breakLabel@ for (i in 1..5) {
        for (j in 1..5) {
            if (j == 3) { // <-- j eğer 3'e eşitse
                break@breakLabel // <-- Belirtilen döngüyü kır
            }
            println(j)
        }
    }
}
```

<br>
<br>

## 9) Fonksiyonlar
### 9.1) Temel Fonksiyon Bilgisi

Bir veya bir çok işlemin tekrar tekrar aynı şekilde yapılması gerektiği durumlarda fonksiyonları kullanırız. Fonksiyonlar "fun" ("fun"ction) keyword'ü (anahtar kelimesi) ile başlar. Fonksiyon adı verilir. Parametre parantezleri açılır "()" ve süslü parantezler açılır "{}". İki nokta üst üste ile geri dönüş değeri yazılabilir. Her fonksiyonun bir geri dönüş değeri vardır. Geri dönüş değeri verilmeyen fonksiyonlar Unit boş tipini geri döndürür.

```kotlin
// Her program açtığımızda bir main fonksiyonu çalışır.
fun main() {
}

// Geri dönüş değeri olmadığı için main fonksiyonu,
// aslında ": Unit" değerini gizli olarak alır.
fun main(): Unit {
}
```

> Bir fonksiyon bir sınıfın(class) içerisinde değil, bir dosyanın içerisinde boşlukta tanımlanıyorsa buna top level function adı verilir.

Geri dönüş değeri Unit'ten farklı fonksiyonlar return anahtar kelimesi ile belirtilen geri dönüş tipine göre uygun bir geri dönüş sağlamalıdır.

```kotlin
// sum fonksiyonu Int tipinden geri dönüş sağlıyor
fun sum(): Int {
    return 0 // <-- geri dönüşü 0
}
```

parametre almış bir fonksiyon tanımı

```kotlin
// sum fonksiyonu Int tipinden geri dönüş sağlıyor.
// Gelen iki sayıyı toplayıp geri döndürüyor.
fun sum(number: Int, number2: Int): Int {
    return number + number2
}
```

Oluşturulmuş bir fonksiyonu çağırmak

```kotlin
// sum fonksiyonu Int tipinden geri dönüş sağlıyor.
// Gelen iki sayıyı toplayıp geri döndürüyor.
fun sum(number: Int, number2: Int): Int {
    return number + number2
}

fun main() {
    val topla = sum(10, 20) // <-- bir değişkene değer olarak atamak
    println(topla) // <-- değişkenden yazdırmak
    println(sum(20, 30)) // <-- Direkt fonksiyondan gelen değeri yazdırmak
}
```

Bir fonksiyonun parametresine "=" atama operatörü ile varsayılan(default) değer atayabiliriz.

```kotlin
// mesaj ve lang alanına eğer bir değer gelmez ise "" ve "tr" olarak kabul et
// Bu yapı aynı zamanda bir foksiyon overloading işlemidir.
fun message(i: Int, message: String = "", date: String, lang: String = "tr")
{ /* ... */ }

// Fonksiyonu çağırırken parametreler yazılarak ya da direkt değer verilebilir.
// Direkt
message(1,"deneme","10.10.2023", "tr")

// Parametreler belirtilerek
message(i=1, message = "deneme2", date = "10.10.2023", lang = "tr")

// Eğer varsayılan parametreye değer vermeyeceksek,
// parametre adlarını kullanarak değer vermemiz gerekir.
message(i = 1, date = "deneme")
```

Bir fonksiyon Unit değilse ve süslü parantez içerisindeki kod sadece tek satırda geri dönüş değeri sağlayacaksa bunu "=" operatörü ile yapabiliriz. Bu foksiyonlar için expression kullanımıdır.

```kotlin
fun sum(first: Int, second: Int): Int {
    return first + second
}

// Aynı işlevi görür
fun sum(first: Int, second: Int): Int = first + second
```

Sayısını tam olarak bilmediğimiz, bir çok aynı tipte parametreye sahip bir fonksiyon yazmamız gerekirse "vararg" kullanırız.

```kotlin
// Eğer vararg'dan sonra başka bir parametre var ise java karşılığı olarak array'dir.
// Eğer sonunda bir parametre yoksa java karşılığı String... şeklindedir.
// Çok küçükte olsa String... daha performanslıdır.
// Bir fonksiyonun içerisine iki defa vararg yazılamaz
fun getUserMessage(vararg message: String, key: Int) {
    // message verilerine erişmek için
    message[0]
    message.get(0)
}
getUserMessage("Merhabaa","Nasılsın?","Bugün hava kapalı.", key = 1)
getUserMessage("Merhabaa","Nasılsın?", key = 2)
getUserMessage("Merhabaa", key = 1)

// Eğer parametre olarak array verilecekse başına yıldız * koyulması gerekir.
getUserMessage(*arrayOf("Merhabaa","Nasılsın?","Bugün hava kapalı."), key = 1)
```

Kendini çağıran fonksiyonlar yazabiliriz.

```kotlin
// Faktöriyel hesabı yapan bir fonksiyon
fun factorial(i: Int): Int {
    if (i >= 2) {
        return i * factorial(i - 1)
    }
    return i
}

fun main() {
    println(factorial(5))
}
```

Fonksiyon içerisinde fonksiyon tanımı yapılabiliyor. Ancak içteki fonksiyona dışarıdan erişim mümkün değildir. -------------------------- Daha sonra detaylı anlatımı yapılacak

```kotlin
fun takeCube(number: Int): Int {
    fun takeSquare(number: Int): Int {
        return number * number
    }
    return number * takeSquare(number)
}
```

Kotlinde java kodlarını kullanırken çok sorunla karşılaşmazken java'da kotlin kodlarını kullanırken bazı sorunlarla karşılaşabiliyoruz. Bunlardan birisi default değer ataması yaptığımız fonksiyonlardır. Java methodlarında default değer ataması olmadığı için kotlin'de kullandığımız default değer alan fonksiyonların başına @JvmOverloads annotation(dipnotu) koymamız gerekir.

```kotlin
@JvmOverloads
fun print(message: String = "Message") { /*...*/ }
```

Bir x class'ı y class'ını miras alıyor ise ve y class'ında oluşturduğumuz bir fonksiyonun default parametresi var ise fonksiyonu override ettiğimizde tekrar default değer ataması yapamıyoruz. (Kodlama ve class yapılarına hakim değilseniz class anlatımından sonra tekrar bakmanızda fayda var. Şuan anlamıyor olmanız normal.)

```kotlin
open class y {
    open fun foo(i: Int = 10) {
    }
}

open class x : y() {
    override fun foo(i: Int = 5) { // <-- = 5 değeri hata verir
    }
}
// Hata: An overriding function is not allowed to specify default values for its parameters
```

<br>

### 9.2) Scope

Bir fonksiyon içerisine yazılmış fonksiyona local fonksiyon denir.

```kotlin
fun takeCube(number: Int): Int {
    fun takeSquare(number: Int): Int { // takeSquare local bir fonksiyondur.
        return number * number
    }
    return number * takeSquare(number)
}
```

Bir sınıf içerisine yazılmış fonksiyona üye fonksiyon denir.

```kotlin
class car{
    fun setColor(colorCodeId: Int){
    }
}
```

Bir fonksiyon Generic tip alıyorsa buna Generic Fonksiyon denir.

```kotlin
fun <T> setColor(colorCodeId: T){
}
```

<br>

### 9.3) Fonksiyon Tipleri
#### İnfix Fonksiyonlar
Infix fonksiyonlar daha okunaklı bir kod yazmamızı sağlar. Fonksiyona ulaşmak için kullandığımız "."'yı kaldırır. Bir fonksiyonun infix fonksiyon olabilmesi için bazı kurallar vardır.
+ infix keyword'u ile başlar.
+ infix fonksiyon bir üye fonksiyon ya da extension fonksiyon olmalıdır.
+ infix fonksiyon sadece bir parametre almalıdır. Bu parametre vararg olamaz.
+ infix fonksiyon parametresi default değer alamaz.

```kotlin
// infix fun infixFonksiyon(birParametre: parametreTipi): geriDönüşTipi{ ... }
// Kullanım:
class car {
    infix fun carColor(colerCodeId: Int) { /*...*/ }
}

// class içerisinde veya extension fonksiyon olmadığı için çalışmaz
infix fun carColor(colerCodeId: Int) { /*...*/ }
/* Hata: 'infix' modifier is inapplicable on this function:
   must be a member or an extension function */

// Default değer alamadığı için çalışmaz
class car {
    infix fun carColor(colerCodeId: Int = "0") { /*...*/ }
}
/* Hata: 'infix' modifier is inapplicable on this function:
   should not have varargs or parameters with default values */
```

Oluşturulan infix fonksiyonun kullanımı

```kotlin
// Bir class'ın veya interface'in içerisinde this kullanılıyor ise
// this bulunduğu class'ı veya interface'i işaret eder.
class AwesomeClass {
    infix fun downloadImage(imageUrl: String) { /*...*/ }

    // Sınıf içerisinde kullanımı
    fun logWhenImageDownloaded(imageUrl: String) {
        downloadImage(imageUrl) // Doğru kullanım.
        this downloadImage imageUrl // Doğru kullanım.
        downloadImage imageUrl // Yanlış Kullanım. Hata verir.
    }
}

fun main() {
    // Sınıf dışarısındaki kullanımı
    val awesomeInstance: AwesomeClass = AwesomeClass() // Sınıftan nesne oluşturmak.
    awesomeInstance downloadImage "https://www.google.com/" // Doğru kullanım
}
```

infix fonksiyon örneği
```kotlin
// operatör olan && -- and -- .and()
if (isStudent && isTeacher) {} // operatör kullanımı
if (isStudent.and(isTeacher)) {} // fonksiyon kullanımı
if (isStudent and isTeacher) {} // infix fonksiyon kullanımı

// operatör olan || -- or -- .or()
if (isStudent || isTeacher) {} // operatör kullanımı
if (isStudent.or(isTeacher)) {} // fonksiyon kullanımı
if (isStudent or isTeacher) {} // infix fonksiyon kullanımı
```

<br>

#### Extension Fonksiyonlar

Extension fonksiyonlar üzerinde değişiklik yapamadığımız Readonly class'ların veya değişiklik yapmak istemediğimiz bizim oluşturduğumuz class'ın içerisine yazmadan fonksiyon tanımlamamızı sağlar. Bu şekilde o sınıfa bir üye fonksiyon yazabiliriz. Bunu yaptığımızda, yazdığımız fonksiyon aslında o sınıfın gerçek bir fonksiyonu olmayacaktır. Extension fonksiyonlar Receiver(alıcıya) diye adlandırılan bir sınıfa ihtiyaç duyar. 

```kotlin
// fun receiverClass.fonksiyonAdi(parametre: ParametreTipi): GeriDonusDegeri { /*...*/ }
// String class'ına Example bir fonksiyon eklemek
fun String.Example(i: Int): String { /*...*/ }

// Yukarıdaki örnek şartları sağladığı için infix fonksiyon olarak da yazılabilir
infix fun String.Example(i: Int): String { /*...*/ }
```

Extension fonksiyon bir class içerisine yazılırsa, o class içerisinde kullanılabilir olurlar.

```kotlin
// top level function olarak tanımlanmış Example
infix fun Int.Example(i: Int) { /*...*/ }

// class içerisinde tanımlanmış Example2
class count {
    infix fun Example2(i: Int) { /*...*/ }
}

fun main() {
    123 Example 10 // Kullanılabilir
    123 Example2 10 // Kullanılamaz

    val say: count = count()
    say 123 Example2 10 // Kullanılamaz
}
```

Extension fonksiyon içerisinde this kullanırsak, this receiver olan class'ın içerisini işaret eder. Extension fonksiyon yazılı olan class'ı işaret etmesini istiyorsa this'e işaret edeceği class adını vermek gerekir.

```kotlin
class count {
    infix fun String.Example(i: Int) {
        /* Aynı isime sahip bir fonksiyonu çağırmaya çalışırsak,
           kendisini tekrar çağırır. Çünkü receiver olan class'ta sadece kendini bulacaktır. */
        this.Example(10) // Kendisini tekrar çağırdı.
        Example(10) // Kendisini tekrar çağırdı.

        // Farkı isime sahip class'ları çağırmakta bir sorun yoktur.
        anyNumber(10)
        // Ancak this ile kullanmak istersek this receiver class'ı işaret edecektir.
        // String class'ı içerisinde anyNumber fonksiyonu bulunmadığı için hata verir.
        this.anyNumber(10) // hata verir

        /* Extension fonksiyon içerisindeki this'in receiver class'ı değil
           Extension fonksiyonun yazılı olduğu class'ı işaret etmesini istiyorsak
           this@classAdi şeklinde kullanırız */
        this@count.Example(10) // Aşağıda yazılı olan "Example" fonsiyonunu çağırdı.
    }

    fun anyNumber(j: Int) {
    }

    fun Example(j: Int) {
    }
}
```

Extension fonksiyonu yazdığımız class'ta aynı isimle, aynı sayıda aynı parametreye sahip, yapısı aynı olan bir başka fonksiyon varsa yazılan extension fonksiyon geçersizdir.

```kotlin
open class numbers {
    infix fun Example(i: Int) { /*...*/ }
}
infix fun numbers.Example(j:Int){/*...*/}
// Uyarı: Extension is shadowed by a member:
// public final infix fun Example(i: Int): Unit
```

Bir class'a extension fonksiyon yazılabildiği gibi extension property de yazılabilir.
> Kotlinde field tanımı aslında bir property tanımıdır.

```kotlin
// get ve set bloklarını yazmak zorunludur.
// = ile direkt değer ataması yapamıyoruz.
class numbers

var numbers.Example: Int
    get() = 10
    set(value) {
        Example = value
    }
```

Extension fonksiyon yazılı bir class başka bir class tarafından kalıtım alırsa, extension fonksiyonu o class içerisinde de kullanabiliriz.

```kotlin
open class numbers {
    infix fun Int.Example(i: Int) { /*...*/ }
}
class count: numbers(){
    fun numberCall(){
        10 Example 10
    }
}
```

<br>
#### higher-order Fonksiyonlar










<br>
<br>









<br>
<br>

## Kişisel Notlarım
#### Daha Sonrasında Araştır
+ Destructuring declarations
+ infix fonksiyonlar
+ inline function
+ first class citizen
+ Fonksiyonel ve nesne yönelimli programlama arasında ne fark var?
+ Agile Metodolojisi
+ Paralelleştirme
+ Farklı thread'leri kullanmak
+ Data structures
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

