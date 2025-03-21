[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-22041afd0340ce965d47ae6ef1cefeee28c7c493a6346c4f15d667ab976d596c.svg)](https://classroom.github.com/a/7TXVPuTD)


## Why we need to use OOP? Some major OOP languages?

OOP, özellikle karmaşık yazılım projelerini objeler ile modelleyip bu objelere özellikler ekleyerek gerçek hayata yakınlaştırarak yazılım projelerini daha yönetilebilir, bakımı kolay bir hale getirerek bizlere büyük avantaj sağlar.

Başlıca sayabileceğim OOP dilleri şunlardır: Java, C# , Swift ve Kotlin.

## Interface vs Abstract Class

| Özellik | **Interface (Arayüz)** | **Abstract Class (Soyut Sınıf)** |
|---------|------------------------|----------------------------------|
| **Amaç** | Ne yapılması gerektiğini tanımlar (sözleşme) | Ne yapılacağı ve nasıl yapılacağı hakkında kısmi uygulama sağlar |
| **Metotlar** | Sadece metot imzaları (Java 8+ ile default/static metot olabilir) | Hem soyut (abstract) hem somut (gövdesi olan) metotlar içerebilir |
| **Alanlar (Fields)** | Sadece `public static final` sabitler | Her türden değişken tanımlanabilir (erişim belirteçleriyle birlikte) |
| **Çoklu Kalıtım** | Bir sınıf birden fazla interface’i **implemente** edebilir | Bir sınıf yalnızca bir abstract sınıfı **extend** edebilir |
| **Yapıcı Metot (Constructor)** | Tanımlanamaz | Tanımlanabilir |
| **Erişim Belirteçleri** | Metotlar varsayılan olarak `public abstract` | `public`, `protected`, `private` gibi belirteçler kullanılabilir |
| **Kullanım Durumu** | Sadece ne yapılmalı sorusunun cevabı verilecekse tercih edilir | Hem ne yapılmalı hem de nasıl yapılmalı sorularına cevap verilecekse tercih edilir |


## Why we need equals and hashcode? When to override? 


Java'da `equals()` ve `hashCode()` metotları, nesnelerin karşılaştırılmasını ve koleksiyon yapılarında doğru şekilde çalışmasını sağlamak için gereklidir. `equals()` metodu, iki nesnenin eşit olup olmadığını belirler. Varsayılan olarak, `Object` sınıfındaki `equals()` metodu bellek adreslerini karşılaştırır. Ancak, genellikle nesnelerin içeriklerine göre kıyaslama yapmak isteriz. Örneğin, iki öğrenci nesnesinin yalnızca `id` alanına göre eşit olup olmadığını belirlemek istediğimiz durumlarda `equals()` metodunu override etmek gerekir.Benzer şekilde, `hashCode()` metodu, bir nesneye özel bir tamsayı (integer) değeri döndürür. Koleksiyon yapılarında (`HashMap`, `HashSet`, `HashTable` gibi) nesnelerin verimli bir şekilde saklanmasını sağlar. Eğer `hashCode()` doğru tanımlanmazsa, nesneler yanlış karşılaştırılabilir ve koleksiyonlarda hatalı davranışlar görülebilir. 

Eğer bir sınıfta içerik bazlı eşitlik kontrolü yapmak istiyorsak, **hem `equals()` hem de `hashCode()` metodunu override etmeliyiz**. Bu özellikle bir nesnenin `HashMap` veya `HashSet` gibi koleksiyonlarda **anahtar (key) olarak kullanılacağı** durumlarda büyük önem taşır. Aynı şekilde, iki nesneyi içeriklerine göre karşılaştırmak istiyorsak, `equals()` metodunu mutlaka override etmeliyiz yoksa referans karşılaştırması yaparız. 

## Diomand problem in java and how to fix it?


Java'da **Diamond Problemi**, bir sınıfın iki farklı interface’ten aynı isimde bir metodu miras alması sonucu ortaya çıkan çakışma durumudur. Java, birden fazla sınıftan kalıtımı desteklemediği için sınıflar arasında klasik diamond problemi yaşanmaz. Ancak **Java 8 ile gelen `default` metotlar** sayesinde interface'lerde bu problem oluşabilir. Eskiden, interface'lerde sadece metot imzaları bulunurken, artık `default` metotlar sayesinde belirli bir implementasyon içerebilirler.

Eğer iki farklı interface aynı isimde `default` bir metot tanımlarsa ve bir sınıf bu iki interface'i implemente ederse, derleyici hangi metodu çağıracağını bilemez ve hata verir. Bu durumu çözmek için, **sınıf içinde `equals()` metodunu override ederek hangi interface'in metodunun kullanılacağını açıkça belirtmemiz gerekir**. Java, bu gibi çakışmalarda **`InterfaceName.super.methodName();`** kullanarak belirli bir interface'in metodunu çağırmamıza izin verir.

## Why we need Garbage Collector? How does it run?

Java'da bellek yönetimi, **Garbage Collector (Çöp Toplayıcı)** tarafından otomatik olarak yapılır. **Garbage Collector**, artık kullanılmayan ve herhangi bir referansa sahip olmayan nesneleri tespit edip belleği geri kazandıran bir mekanizmadır.  

Eğer **Garbage Collection (Çöp Toplama)** mekanizması olmasaydı, programcıların bellek yönetimini manuel olarak yapması gerekecekti. Bu, **memory leak (bellek sızıntısı)** ve **dangling pointer (boşta kalan bellek adresleri)** gibi ciddi problemlere yol açabilirdi.

**Garbage Collector Nasıl Çalışır?**  
**JVM (Java Virtual Machine)**, garbage collector'ü belirli aralıklarla **otomatik olarak** çalıştırır. Bu süreç birkaç adımdan oluşur:

1. **İşaretleme (Marking)** – Hâlâ kullanılan nesneler belirlenir, kullanılmayan nesneler tespit edilir.
2. **Temizleme (Sweeping)** – Kullanılmayan nesneler bellekten silinir.
3. **Düzenleme (Compacting - Opsiyonel)** – Bellek parçalanmasını önlemek için nesneler sıkıştırılır ve yeniden düzenlenir.


## Java 'static' keyword usage?

Java'da **`static` anahtar kelimesi**, bir değişkenin, metodun veya blokun **sınıfa ait** olduğunu belirtir. Yani, **nesne oluşturulmadan** kullanılabilir. Normalde, bir sınıfın değişkenlerine ve metodlarına erişmek için **bir nesne oluşturulması gerekir**, ancak `static` anahtar kelimesi ile tanımlanan elemanlar **sınıfa ait olduğu için doğrudan erişilebilir**.Bu sayede **her nesne için ayrı bir kopya oluşturulmaz**, bellekte **tek bir defa saklanır** ve doğrudan sınıf adı ile erişilebilir. 

## Immutability means? Where, How and Why to use it?

Immutability, bir nesnenin **oluşturulduktan sonra değiştirilememesi** anlamına gelir. Java'da **immutable nesneler**, değerleri değiştirilemeyen nesnelerdir. Bunun en bilinen örneği **`String` sınıfıdır**. `String` nesneleri üzerinde yapılan değişiklikler, orijinal nesneyi değiştirmez, bunun yerine **yeni bir nesne oluşturur**.

- **Çok iş parçacıklı (multi-threaded) programlamada güvenlik sağlar.**
- **Yan etkileri (side-effects) engelleyerek hata riskini azaltır.**
- **Önbellekleme (caching) ve veri paylaşımında veri bütünlüğünü korur.**

Bir sınıfı immutable yapmak için:
1. **Sınıfı `final` yaparak miras almayı önleriz.**
2. **Tüm değişkenleri `private final` olarak tanımlarız.**
3. **Setter metotlarını tanımlamayız.**
4. **Değerleri yalnızca constructor içinde atarız.**

## Composition and Aggregation means and differences.

Composition, bir nesnenin başka bir nesnenin **ayrılmaz bir parçası** olduğu ve **bağımlı** olduğu ilişki türüdür. Eğer **ana nesne yok edilirse, alt nesne de yok olur**.**Örnek:** Bir **Araba** olmadan **Motor** var olamaz.
Aggregation, bir nesnenin başka bir nesneyle ilişkili olduğu ancak ona bağımlı olmadığı ilişki türüdür. Eğer **ana nesne yok edilirse, alt nesne var olmaya devam edebilir**.

## Cohesion and Coupling means and differences.

Cohesion, bir sınıfın veya modülün **tek bir sorumluluğa odaklanmasını** ifade eder.  
- **Yüksek Cohesion** → Bir sınıf **yalnızca belirli bir işle ilgilenir**, böylece kod daha modüler ve sürdürülebilir olur.  
- **Düşük Cohesion** → Bir sınıf **çok fazla sorumluluk** üstlenirse, kod karmaşık hale gelir ve bakım zorlaşır.  

**Örnek:**  
- **Yüksek Cohesion:** Bir **`FileManager`** sınıfı yalnızca dosya işlemlerini yönetir.  
- **Düşük Cohesion:** Aynı sınıf hem dosya işlemlerini hem de veritabanı bağlantısını yönetiyorsa cohesion düşüktür.

## Heap and Stack means and differences?
Heap ve Stack, Java'da bellek yönetiminde kullanılan iki temel bölümdür.  

- **Stack (Yığın):**  
  - Metod çağrıları ve yerel değişkenler (local variables) için kullanılır.
  - LIFO (Last In, First Out) prensibiyle çalışır.  
  - Hızlıdır ve yönetimi otomatiktir.
  - Sınırlı bellek alanına sahiptir.  

- **Heap (Yığın Belleği):**  
  - Nesnelerin (Objects) tutulduğu bellek alanıdır. 
  - Garbage Collector tarafından yönetilir.
  - Daha büyük ancak Stack'e göre daha yavaştır. 
  - Tüm uygulama boyunca kalıcı olabilir.



## Exception means and type of exceptions?

Exception, programın çalışması sırasında meydana gelen **hata durumlarını** ifade eder. Java'da istisnalar, programın beklenmeyen durumları yönetmesini sağlar.

### 🔹 **Exception Türleri**
1. **Checked Exceptions (Denetlenen İstisnalar)**  
   - Derleme (compile-time) sırasında kontrol edilir.  
   - Örneğin: `IOException`, `SQLException`.  
2. **Unchecked Exceptions (Denetlenmeyen İstisnalar)**  
   - Çalışma zamanı (runtime) sırasında meydana gelir.  
   - Örneğin: `NullPointerException`, `ArrayIndexOutOfBoundsException`.  
3. **Error (Hata)**  
   - JVM kaynaklı ciddi hatalardır, yakalanmazlar.  
   - Örneğin: `OutOfMemoryError`, `StackOverflowError`.  



## How to summarize clean code as short as possible?
"Temiz kod, okunabilir, anlaşılır ve sürdürülebilir koddur.Hiç yazılım ile uğtaşmayan biri bile göz gezdirdiğnde bilgi sahibi olmalıdır.

## What is the method of hiding in java?

Method Hiding, **bir alt sınıfın (subclass) bir üst sınıfta (superclass) bulunan `static` metodu gizlemesi (hiding) durumudur**.  
- **Metot gizleme, yalnızca `static` metotlar için geçerlidir.**  
- **Override'dan farklıdır**, çünkü `static` metotlar **polimorfizm desteklemez** ve çalışma zamanında (`runtime`) değil, derleme zamanında (`compile-time`) bağlanır.

## What is the difference between abstraction and polymorphism?

Abstraction, **gereksiz detayları gizleyerek sadece önemli bilgilerin gösterilmesini sağlayan bir OOP prensibidir**.  
- `abstract` sınıflar (`abstract class`) ve arayüzler (`interface`) ile sağlanır.  
- Kullanıcı, **bir nesnenin nasıl çalıştığını değil, ne yaptığını** bilir.  
- **Kod tekrarını önler, bakımı kolaylaştırır ve modülerliği artırır.**  

Polymorphism, **aynı metodun farklı nesneler üzerinde farklı davranışlar gösterebilmesini sağlayan bir OOP prensibidir**.  
- **Method Overriding (Geçersiz Kılma)** ve **Method Overloading (Aşırı Yükleme)** ile sağlanır.  
- Aynı metod adıyla **farklı implementasyonlar** oluşturulabilir.  
- **Kod esnekliğini artırır ve genişletilebilir yapılar oluşturur.**


