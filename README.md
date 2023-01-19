# Kotlin Ders Notları 

; kullanımı kotlinde yok. Kullanınca hata vermez, ama ide kullanmamak için öneri verir

## Daha Sonrasında Araştır
	Paralelleştirme
	Farklı thread'leri kullanmak
	Data structures
	Primitive tipler, referans tipler
	infix fonksiyonlar

## Yapmayı Dene
	Warning'leri çözmeye çalış

## kotlin İş Görüşmelerinde Sorulabilecek Sorular
	val ve var'ın farkı nedir?
	const val ve val'ın farkı nedir?

## Ek Bilgi
	Android tuş kilidinden çıkılınca bütün widge'ler tekrar yüklenir.

## Ek Notlar
	Kotlinde java kodlarını da kullanabiliriz.
	Kotlin'de primitive tipler direkt olarak tanımlanamaz.
	Yazdığımız kodlar derlenirken primitive tiplere dönüştürülür.
	Nullable değişkenler primitive özelliğini kaybeder.
	utf-8 encoding bozulması durumunda sorunlar yaşanabileceği için yorumlar bile ingilizce karakterler ile yazılmalı.
	Ülkelerin matematiksel hesaplarda kullanılan ondalık ayırma için kullanılan , veya . sembollerine dikkat edilmeli.
		try ve catch içerisinde yazarak hem . için hem , için ayrı kodlar yazılarak çözülebilir.
	Boolean değişkenler için true veya false kullanılır 0 veya 1 kullanılamıyor.

## Değişkenler
	val = (val)ue - immutable
	var = (var)iable - mutable
	val değeri daha sonradan değiştirilemez.
	var değeri daha sonradan değişebilir.
	değişkene ilk değer ataması veriliyorsa değikene değişken tipi vermek gerekmez.
	sayısal değerler sıfırla başlanamaz.
	kolay okumak için sayıda _ kullanabilirsiniz. derlemede _'ler kaldırılır.
	
	Değişken tanımı: 
		erisimKodu degiskenAdi: degiskenTuru
		val name: String = "isim"
		val name = "isim"
		
		NULLABLE değişken tanımlama (değişken isminin sonunda ? var)
		erisimKodu degiskenAdi?: degiskenTuru
		val name: String? = null
	
	Değişken tanımını ilk olarak val ile yapmak daha mantıklı.
		Eğer değişken değeri daha sonrasında değişecekse var olarak değiştiririz.

## Tür Dönüşümü
	İki değer toplanıp yeni bir değişkene değer olarak atanır ve belirli bir tip verilmez ise uygun olan tipe dönüşür.
	
	Kotlin kodlarını kullanarak tür dönüşümü yapmak:
		donusturulecekDeger.toDonusturulecekTip()
		x.toInt()
	java özellikleri kullanarak tür dönüşümü yapmak:
		donusturulecekTur.parseDonusturulecekTur(donusturulecekDeger)
		Integer.parseInt(x)

## Operatörler
	Mantıksal Operatörler:
		&& - and - .and(x)	--> ve
		|| - or - .or(x)	--> veya