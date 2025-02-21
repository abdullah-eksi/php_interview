
# **2. Nesne Yönelimli Programlama (OOP)**  

### **2.1 PHP'de late static binding (geç statik bağlama) nedir?**  
✍ **Cevap:**  

**Late Static Binding (Geç Statik Bağlama)**, PHP'de bir sınıfın statik metodunu çağırırken, hangi sınıfın metodunun kullanılacağını doğru şekilde belirlemeye yarayan bir özelliktir. 

Bu, özellikle kalıtımda (inheritance) faydalıdır. Normalde statik metodlar, sınıf ismiyle çağrılır ama `static::` kullanarak, türetilen sınıfların doğru metodunu çağırmak mümkündür.

Örnek:

```php
<?php
class A {
    public static function test() {
        echo "A\n";
    }
}

class B extends A {
    public static function test() {
        echo "B\n";
    }
}

B::test(); // B
?>
```

Burada, `B::test()` çağrıldığında `B` sınıfının metodu çalışır.

### **2.2 PHP’de trait nedir ve nasıl kullanılır?**  
✍ **Cevap:** 

 **Trait**, PHP'de bir sınıfa tekrar kullanılabilir metodlar eklemek için kullanılan bir yapıdır. Kalıtımda sınıflar birden fazla özellik veya metod alabilir, ancak trait ile bu özellikler birden fazla sınıfa kolayca eklenebilir.

Örnek:

```php
<?php
trait MyTrait {
    public function greet() {
        echo "Merhaba!";
    }
}

class MyClass {
    use MyTrait;
}

$obj = new MyClass();
$obj->greet(); // Merhaba!
?>
```

Burada `MyClass` sınıfı, `MyTrait` trait'ini kullanarak `greet()` metodunu alır.

### **2.3 Interface ile abstract class arasındaki farklar nelerdir?**  
✍ **Cevap:**  
**Interface** ve **abstract class** arasındaki farklar şunlardır:

1. **Metod Tanımlamaları:**
   - **Interface**: Yalnızca metod imzalarını (declaration) içerir, metodların gövdesi olmaz.
   - **Abstract class**: Hem metod imzalarını hem de metod gövdelerini (implementation) içerebilir.

2. **Kalıtım:**
   - **Interface**: Bir sınıf birden fazla interface'i implement edebilir.
   - **Abstract class**: Bir sınıf yalnızca bir abstract class’ı extend edebilir.

3. **Özellikler (Properties):**
   - **Interface**: Sadece sabitler (constants) tanımlanabilir, değişken tanımlanamaz.
   - **Abstract class**: Değişkenler ve sabitler tanımlanabilir.

4. **Kullanım Amacı:**
   - **Interface**: Farklı sınıfların benzer metodları uygulamasını sağlamak için kullanılır.
   - **Abstract class**: Ortak özellikleri ve metodları bir temel sınıfta toplamak için kullanılır.

Örnek:

```php
<?php
interface MyInterface {
    public function myMethod();
}

abstract class MyAbstractClass {
    abstract public function myMethod();
}
?>
```

### **2.4 Dependency Injection (Bağımlılık Enjeksiyonu) nedir? Örnek bir kullanım senaryosu anlatınız.**  
✍ **Cevap:**  

**Dependency Injection (Bağımlılık Enjeksiyonu)**, bir sınıfın ihtiyaç duyduğu bağımlılıkları (başka sınıfları veya servisleri) dışarıdan almasını sağlayan bir tasarım desenidir. Bu yöntem, sınıfların birbirine sıkı sıkıya bağlı olmasını engeller ve daha esnek, test edilebilir kod yazılmasını sağlar.

**Örnek Senaryo:**

Bir `UserService` sınıfı, bir `DatabaseService` sınıfına bağımlı olsun. Bu bağımlılığı, `UserService` sınıfına dışarıdan (constructor ile) enjeksiyon yaparak verebiliriz.

```php
<?php
class DatabaseService {
    public function connect() {
        echo "Veritabanına bağlanıldı!";
    }
}

class UserService {
    private $database;

    // Bağımlılık enjeksiyonu
    public function __construct(DatabaseService $database) {
        $this->database = $database;
    }

    public function getUserData() {
        $this->database->connect();
        echo "Kullanıcı verisi alındı!";
    }
}

// Bağımlılığı dışarıdan sağlıyoruz
$dbService = new DatabaseService();
$userService = new UserService($dbService);
$userService->getUserData(); // Veritabanına bağlanıldı! Kullanıcı verisi alındı!
?>
```

Burada, `UserService` sınıfı `DatabaseService`'e dışarıdan bağımlı olarak enjekte edilir, bu sayede bağımlılıklar daha esnek hale gelir ve test edilebilirlik artar.

### **2.5 PHP’de çoklu kalıtım (multiple inheritance) neden desteklenmez?**  
✍ **Cevap:**  
PHP, **çoklu kalıtımı** (multiple inheritance) desteklemez çünkü bu, bazı sorunlara yol açabilir:

1. **Çakışan Metodlar**: Bir sınıf birden fazla sınıfı miras aldığında, aynı isme sahip metodlar çakışabilir. PHP, hangi metodun kullanılacağına karar veremeyebilir.

2. **Karmaşıklık**: Çoklu kalıtım, sınıflar arasındaki ilişkileri karmaşıklaştırabilir ve kodun anlaşılmasını zorlaştırabilir.

Bu yüzden PHP, **interface** ve **trait** gibi alternatif yollar sunarak, aynı işlevselliği daha kontrollü ve esnek bir şekilde sağlamayı tercih eder. 

Örnek olarak, PHP'de **trait** kullanılarak aynı işlevsellik sağlanabilir:

```php
<?php
trait TraitA {
    public function methodA() {
        echo "TraitA method\n";
    }
}

trait TraitB {
    public function methodB() {
        echo "TraitB method\n";
    }
}

class MyClass {
    use TraitA, TraitB;
}

$obj = new MyClass();
$obj->methodA(); // TraitA method
$obj->methodB(); // TraitB method
?>
```

### **2.6 PHP’de final anahtar kelimesinin kullanımı nedir?**  
✍ **Cevap:**  
**final** anahtar kelimesi, PHP'de iki şekilde kullanılır:

1. **Final Sınıf**: Bir sınıfın türetilmesini engeller. Yani, o sınıftan başka bir sınıf türetilemez.
   
   ```php
   <?php
   final class MyClass {
       // Sınıf içerikleri
   }
   ?>
   ```

2. **Final Metod**: Bir metodun, alt sınıflar tarafından override edilmesini (geçersiz kılınmasını) engeller.
   
   ```php
   <?php
   class MyClass {
       final public function myMethod() {
           echo "Bu metod değiştirilemez.";
       }
   }
   ?>
   ```

Bu kullanım, belirli sınıf ve metodların değiştirilmesini engelleyerek, güvenli ve sabit bir yapı sağlar.

### **2.7 SOLID prensiplerinden herhangi birini açıklayarak örnek bir PHP kodu yazınız.**  
✍ **Cevap:**  

**SOLID** prensipleri, yazılım geliştirmede esnek, sürdürülebilir ve bakımı kolay kod yazmak için takip edilmesi gereken 5 temel prensiptir. İşte her bir prensip açıklamalarıyla birlikte örnek PHP kodu:

### 1. **Single Responsibility Principle (SRP) - Tek Sorumluluk Prensibi**  
Bir sınıf sadece bir sorumluluğa sahip olmalı, yani sadece bir işi yapmalı.

**Örnek:**
```php
<?php
class User {
    public function getUserData() {
        // Kullanıcı verilerini getir
    }
}

class UserDataPrinter {
    public function printUserData(User $user) {
        // Kullanıcı verilerini yazdır
    }
}
?>
```

Burada, `User` sınıfı sadece kullanıcı verilerini alırken, `UserDataPrinter` sınıfı kullanıcı verilerini yazdırır. Her sınıfın bir sorumluluğu vardır.

### 2. **Open/Closed Principle (OCP) - Açık/Kapalı Prensibi**  
Bir sınıf, yeni işlevler eklemek için **açık**, fakat değişiklik yapmak için **kapalı** olmalıdır.

**Örnek:**
```php
<?php
class Shape {
    public function area() {
        // Alan hesaplama
    }
}

class Circle extends Shape {
    public function area() {
        return pi() * 4; // Çemberin alanı
    }
}

class Rectangle extends Shape {
    public function area() {
        return 5 * 4; // Dikdörtgenin alanı
    }
}
?>
```

Yeni şekiller eklenebilir, ancak mevcut kodda değişiklik yapmamız gerekmez.

### 3. **Liskov Substitution Principle (LSP) - Liskov Değiştirme Prensibi**  
Bir sınıf, alt sınıflarıyla değiştirilebilir olmalıdır. Yani, alt sınıflar üst sınıfın yerini alabilmeli ve beklenen davranışı sergilemelidir.

**Örnek:**
```php
<?php
class Bird {
    public function fly() {
        echo "Uçuyor!";
    }
}

class Sparrow extends Bird {
    // Uçabilen kuşlar
}

class Ostrich extends Bird {
    public function fly() {
        // Struç kuşu uçamaz, bu metod doğru olmaz
        throw new Exception("Uçamaz!");
    }
}
?>
```

`Ostrich` sınıfı, `Bird` sınıfından türetilse de, beklenen davranışın dışında bir şey yaparsa (uçamıyorsa), bu prensibe uymaz.

### 4. **Interface Segregation Principle (ISP) - Arayüz Ayrım Prensibi**  
Bir sınıf, kullanmadığı metodları içeren bir arayüzü implement etmemelidir.

**Örnek:**
```php
<?php
interface Printable {
    public function print();
}

interface Scannable {
    public function scan();
}

class Printer implements Printable {
    public function print() {
        echo "Yazdırma işlemi yapılıyor!";
    }
}

class Scanner implements Scannable {
    public function scan() {
        echo "Tarama işlemi yapılıyor!";
    }
}
?>
```

Burada, `Printer` sadece yazdırma işleviyle, `Scanner` ise sadece tarama işleviyle ilgilenir. Her arayüz sadece ihtiyacı olan metodları içerir.

### 5. **Dependency Inversion Principle (DIP) - Bağımlılık Tersine Çevirme Prensibi**  
Yüksek seviyeli modüller, düşük seviyeli modüllere bağımlı olmamalıdır. Her iki modül de soyutlamaya (interface veya abstract class) bağımlı olmalıdır.

**Örnek:**
```php
<?php
interface Database {
    public function connect();
}

class MySQLDatabase implements Database {
    public function connect() {
        echo "MySQL Bağlantısı kuruluyor!";
    }
}

class UserService {
    private $db;

    public function __construct(Database $db) {
        $this->db = $db;
    }

    public function getUserData() {
        $this->db->connect();
    }
}

$db = new MySQLDatabase();
$userService = new UserService($db);
$userService->getUserData();
```

`UserService` sınıfı, veri tabanına bağlı değildir. Bağımlılık dışarıdan, `Database` arayüzü aracılığıyla enjeksiyonla sağlanır.
?>
---




### **2.8 Singleton tasarım deseni nasıl uygulanır? Avantajları ve dezavantajları nelerdir?**  
✍ **Cevap:**  

**Singleton tasarım deseni**, bir sınıfın yalnızca bir örneğinin oluşturulmasını garanti eden bir tasarım desenidir. Bu, sınıfın tek bir nesnesinin tüm uygulama boyunca kullanılmasını sağlar.

### **Uygulama:**

```php
<?php
class Singleton {
    private static $instance = null;

    // private constructor, dışarıdan nesne oluşturulamaz
    private function __construct() {}

    // nesneye erişim sağlayan statik metod
    public static function getInstance() {
        if (self::$instance === null) {
            self::$instance = new Singleton();
        }
        return self::$instance;
    }

    public function sayHello() {
        echo "Merhaba, Singleton Deseni!";
    }
}

// Kullanım:
$singleton = Singleton::getInstance();
$singleton->sayHello();  // Merhaba, Singleton Deseni!
?>
```

### **Avantajları:**
1. **Tek örnek (Instance)**: Uygulama boyunca tek bir nesne kullanılır, bellek tasarrufu sağlar.
2. **Global Erişim**: Nesneye global bir erişim noktası sağlar.
3. **Kontrol**: Nesne oluşturulmasını kontrol eder, sınıfın kontrolsüz bir şekilde örneği alınamaz.

### **Dezavantajları:**
1. **Test Edilebilirlik**: Singleton'lar test yazmayı zorlaştırabilir, çünkü global bir durum oluşturur.
2. **Sıkı Bağlılık**: Singleton, sınıfları birbirine sıkı sıkıya bağlayarak, esneklik ve genişletilebilirliği zorlaştırabilir.
3. **Çoklu İşlem**: Çoklu iş parçacığı (multithreading) ortamlarında dikkatli kullanılmazsa, eşzamanlı erişim sorunlarına yol açabilir.

Singleton, belirli durumlarda faydalı olabilir, ancak dikkatli ve yerinde kullanılması gerekmektedir.

### **2.9 PHP’de observer design pattern nasıl uygulanır?**  
✍ **Cevap:**  


**Observer Design Pattern** (Gözlemci Deseni), bir nesne (subject) değiştiğinde, ona bağlı olan diğer nesnelerin (observers) otomatik olarak bilgilendirildiği bir tasarım desenidir.

### **Uygulama:**
```php
<?php
// Observer Arayüzü
interface Observer {
    public function update($data);
}

// Subject (Gözlemlenen) Sınıfı
class Subject {
    private $observers = [];

    public function addObserver(Observer $observer) {
        $this->observers[] = $observer;
    }

    public function notifyObservers($data) {
        foreach ($this->observers as $observer) {
            $observer->update($data);
        }
    }
}

// Concrete Observer
class ConcreteObserver implements Observer {
    public function update($data) {
        echo "Güncelleme alındı: $data\n";
    }
}

// Kullanım:
$subject = new Subject();
$observer = new ConcreteObserver();
$subject->addObserver($observer);

$subject->notifyObservers("Yeni Veri!");
?>
```

### **Çıktı:**
```bash
Güncelleme alındı: Yeni Veri!
```

Bu desende, **Subject** (gözlemlenen) bir değişiklik yapınca, **Observer** (gözlemci) bilgilendirilir. Bu, sistemin daha esnek ve bağımsız olmasını sağlar.

### **2.10 Factory Design Pattern nasıl çalışır?**  
✍ **Cevap:**  

### **2.11 Builder Design Pattern nedir ve PHP’de nasıl uygulanır?**  
✍ **Cevap:**  

### **2.12 Prototype Design Pattern PHP’de nasıl kullanılır?**  
✍ **Cevap:**  

### **2.13 Strategy Design Pattern nasıl çalışır?**  
✍ **Cevap:**  

### **2.14 PHP’de Reflection API nedir ve nasıl kullanılır?**  
✍ **Cevap:**  

### **2.15 Magic Methods (sihirli metotlar) nedir? Örnek vererek açıklayınız.**  
✍ **Cevap:**  


### **2.16 PHP’de nesne klonlama nasıl yapılır? (`clone` anahtar kelimesi ve `__clone()` metodu nasıl çalışır?)**  
✍ **Cevap:**  

### **2.17 PHP’de immutable (değiştirilemez) nesneler nasıl oluşturulur?**  
✍ **Cevap:**  

### **2.18 Fluent Interface (zincirleme metod çağrımı) nedir? Örnek vererek açıklayınız.**  
✍ **Cevap:**  

### **2.19 OOP'de Dependency Inversion Principle (Bağımlılığı Tersine Çevirme Prensibi) nasıl uygulanır?**  
✍ **Cevap:**  

### **2.20 PHP’de Object Pooling nedir ve ne zaman kullanılır?**  
✍ **Cevap:**  

### **2.21 Data Mapper ve Active Record desenleri arasındaki farklar nelerdir?**  
✍ **Cevap:**  

### **2.22 PHP’de Middleware mantığı nasıl çalışır?**  
✍ **Cevap:**  

### **2.23 PHP’de Polymorphism (çok biçimlilik) nasıl çalışır?**  
✍ **Cevap:**  

