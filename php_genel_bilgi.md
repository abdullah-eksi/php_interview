---

# **1. Genel PHP Bilgisi**  

### **1.1 PHP'de `==` ile `===` operatörleri arasındaki fark nedir?**  
✍ **Cevap:**  
- "==", sadece iki değeri karşılaştırırken, "===" hem değeri hem de veri türünü karşılaştırır.

### **1.2 `include`, `require`, `include_once` ve `require_once` arasındaki farklar nelerdir?**  
✍ **Cevap:**  
- **include** dosyayı dahil eder Eğer dosya bulunamazsa, sadece bir uyarı verir fakat kod calısmaya devam eder  

- **require** Belirtilen dosyayı, dosyanın içine dahil eder. Eğer dosya bulunamazsa, bir hata (Fatal Error) verir ve script çalışmayı durdurur.

- **include_once**  Belirtilen dosyayı sadece bir kez dahil eder. Aynı dosya tekrar dahil edilmeye çalışılırsa, işlem yapılmaz. dosya bulunamazsa kod çalışmaya devam eder

- **require_once** Belirtilen dosyayı sadece bir kez dahil eder. Aynı dosya tekrar dahil edilmeye çalışılırsa, işlem yapılmaz. eğer dosya bulunmazsa bir hata (Fatal Error) verir ve script çalışmayı durdurur.

### **1.3 PHP’de static değişkenler nedir ve nasıl kullanılır ?**  
✍ **Cevap:**  PHP'de static değişkenler, bir fonksiyon veya metot içerisinde tanımlandığında, o fonksiyon her çağrıldığında değişkenin değerinin korunmasını sağlar.
- Bir fonksiyon içinde static bir değişken tanımladığınızda, o değişkenin değeri fonksiyon dışındaki çağrılarda da korunur.
- Bu, genellikle sayaçlar, geçmiş değerler veya kalıcı veri tutmak için kullanılır.

### Örnek:

```php
<?php
function sayac() {
    static $count = 0;  // Static değişken
    $count++;
    echo $count . "\n";
}

sayac();  // Çıktı: 1
sayac();  // Çıktı: 2
sayac();  // Çıktı: 3
?>
```



### **1.4 `unset()` ile `$var = null;` arasındaki fark nedir?**  
✍ **Cevap:**  
- *unset:* Bu, değişkeni bellekten siler, yani değişkenin ismi artık mevcut olmaz.
- *null:*  bir değişkene null değerini atar.
Bu, değişkenin içeriğini sıfırlar ancak değişkenin kendisini korur.

### **1.5 PHP’de değişkenlerin kapsamları (global, local, static) nelerdir?**  
✍ **Cevap:**  
- *Global:* Global değişkenler, fonksiyon dışında tanımlanmış olan değişkenlerdir ve tüm script içinde erişilebilirler.

```php
<?php
$globalVar = "Global değişken";
function myFunction() {
    global $globalVar;
    echo $globalVar; // Global değişkene erişim sağlanır.
}
myFunction();
?>
```

- *Local:* Bir fonksiyon içinde tanımlanan değişkenler yerel değişkenlerdir ve sadece o fonksiyon içinde erişilebilir.


```php
<?php
function myFunction() {
    $localVar = "Yerel değişken";
    echo $localVar; // Bu fonksiyon içinde geçerlidir.
}
myFunction();
// echo $localVar; // Hata! Çünkü $localVar fonksiyon dışında geçerli değil.
?>
```

- *Static:* static anahtar kelimesi ile tanımlanan değişkenler, bir fonksiyon içinde olsa bile değeri korunur ve fonksiyon tekrar çağrıldığında önceki değeri hatırlar.

```php
<?php
function counter() {
    static $count = 0;
    $count++;
    echo $count;
}
counter(); // 1
counter(); // 2
counter(); // 3
?>
```


### **1.6 PHP’de referans ile değişken atamanın (`&` işareti ile) avantajları ve dezavantajları nelerdir?**  
✍ **Cevap:**  PHP’de referans ile değişken atama (&), bir değişkenin değerini değil, bellekteki adresini kopyalar. Kodun okunabilirliğini zorlaştırabilir. Performans sorunlarına neden olabilir.

```php
<?php
$a = 10;
$b = &$a; // $b, $a'nın referansını alır

$b = 20; // $b'nin değeri değişince $a da değişir

echo $a; // 20
echo $b; // 20

?>
```


### **1.7 Magic methods (sihirli metotlar) nelerdir? Örnek vererek açıklayınız.**  
✍ **Cevap:**  

PHP’de **sihirli metotlar (magic methods)**, belirli bir işlevi yerine getiren ve özel bir işaretçi ile başlayan metotlardır. Bu metotlar sınıflarda otomatik olarak çağrılır. İşte bazıları:



#### 1. **`__construct()`**: Nesne Oluşturulduğunda Çağrılır

`__construct()` metodu, bir sınıfın nesnesi oluşturulduğunda otomatik olarak çağrılır. Bu metod, sınıfın kurulum işlemlerini yapmak için kullanılır.

**Örnek:**
```php
<?php
class MyClass {
    public function __construct() {
        echo "Nesne oluşturuldu!";
    }
}

$obj = new MyClass(); // Çıktı: "Nesne oluşturuldu!"
?>
```





#### 2. **`__destruct()`**: Nesne Yok Edildiğinde Çağrılır

`__destruct()` metodu, nesne bellekten silindiğinde ya da `unset()` fonksiyonu ile yok edildiğinde çağrılır. Nesne yok edilmeden önce temizleme işlemleri yapmak için kullanılabilir.

**Örnek:**
```php
<?php
class MyClass {
    public function __destruct() {
        echo "Nesne yok edildi!";
    }
}

$obj = new MyClass();
unset($obj); // Çıktı: "Nesne yok edildi!"
?>
```



#### 3. **`__get($property)`**: Var Olmayan Bir Özelliğe Erişildiğinde Çağrılır

`__get($property)` metodu, bir sınıfın var olmayan ya da erişilemiyor bir özelliğine erişilmeye çalışıldığında çağrılır. Bu metod sayesinde özelliklere dinamik olarak değer atanabilir ya da değerler döndürülebilir.

**Örnek:**
```php
<?php
class MyClass {
    private $name = "PHP"; // Private özellik

    public function __get($property) {
        return $this->$property; // Özellik değerini döndürür
    }
}

$obj = new MyClass();
echo $obj->name; // Çıktı: "PHP"
?>
```



#### 4. **`__set($property, $value)`**: Var Olmayan Bir Özelliğe Değer Atandığında Çağrılır

`__set($property, $value)` metodu, var olmayan bir özelliğe değer atandığında otomatik olarak çağrılır. Bu metod, değer atama işlemleri üzerinde kontrol sağlamak için kullanılır.

**Örnek:**
```php
<?php
class MyClass {
    public function __set($property, $value) {
        echo "$property özelliğine $value değeri atandı.";
    }
}

$obj = new MyClass();
$obj->name = "PHP"; // Çıktı: "name özelliğine PHP değeri atandı."
?>
```


#### 5. **`__call($method, $arguments)`**: Var Olmayan Bir Metoda Çağrı Yapıldığında Çağrılır

`__call($method, $arguments)` metodu, sınıfta tanımlı olmayan bir metoda çağrı yapılmaya çalışıldığında devreye girer. Bu metod, var olmayan metotlar için alternatif bir işlem yapabilir.

**Örnek:**
```php
<?php
class MyClass {
    public function __call($method, $arguments) {
        echo "Metod adı: $method, Parametreler: " . implode(", ", $arguments);
    }
}

$obj = new MyClass();
$obj->unknownMethod("param1", "param2"); // Çıktı: "Metod adı: unknownMethod, Parametreler: param1, param2"
?>
```


#### 6. **`__toString()`**: Nesne String'e Dönüştürülmek İstendiğinde Çağrılır

`__toString()` metodu, bir nesne doğrudan string olarak kullanıldığında (örneğin `echo` ile yazdırıldığında) çağrılır. Bu metod, nesnenin string temsilini belirler.

**Örnek:**
```php
<?php
class MyClass {
    public function __toString() {
        return "Bu bir nesnedir.";
    }
}

$obj = new MyClass();
echo $obj; // Çıktı: "Bu bir nesnedir."
?>
```

### **1.8 PHP’de `__invoke()` metodu ne işe yarar?**  
✍ **Cevap:** PHP'de `__invoke()` metodu, bir sınıfın nesnesi, bir fonksiyon gibi çağrıldığında çalışmasını sağlar. Yani, nesneye fonksiyon gibi erişim yapılmak istendiğinde, PHP bu özel metodu çağırır. Bu özellik, nesneyi fonksiyonel bir yapıya dönüştürmek için kullanılır.

### Örnek:

```php
<?php
class Calculator {
    public function __invoke($a, $b) {
        return $a + $b;
    }
}

$calc = new Calculator();
echo $calc(3, 5);  // Nesne fonksiyon gibi çağrılır, 8 döner
?>
```

Bu örnekte, `Calculator` sınıfındaki `__invoke()` metodu, nesne `$calc` üzerinde çağrıldığında, iki parametre alıp toplamını döndürür.


### **1.9 PHP'de anonymous (isimsiz) fonksiyonlar ve closure'lar nasıl kullanılır?**  
✍ **Cevap:**

**Anonymous Fonksiyonlar**: PHP'de, fonksiyonlar adlandırılmadan da tanımlanabilir Isimsiz fonksiyonlar, genellikle bir değişkenin içine atanarak ya da bir fonksiyona parametre olarak geçirilerek kullanılır.

**Closure'lar**: Closure, bir fonksiyonun dışındaki değişkenlere erişim sağlayabilen isimsiz bir fonksiyon türüdür. Closure'lar, dış çevreden (scope) değişkenleri "capture" (yakalama) edebilirler.

### **Anonymous Fonksiyon Kullanımı:**

```php
<?php
$greeting = function($name) {
    return "Merhaba, $name!";
};

echo $greeting("Abdullah");  // Çıktı: Merhaba, Abdullah!
?>
```

Yukarıdaki örnekte, `greeting` değişkeni bir anonim fonksiyon içeriyor ve bu fonksiyon daha sonra çağrılıyor.

### **Closure Kullanımı (Dış Değişkenlere Erişim):**

```php
<?php
$message = "Merhaba";
$greeting = function($name) use ($message) {
    return $message . ", $name!";
};

echo $greeting("Abdullah");  // Çıktı: Merhaba, Abdullah!
?>
```

Bu örnekte, `use` anahtar kelimesi, dışarıdaki `$message` değişkenini closure içine alır. Bu sayede closure, `$message` değişkenine erişim sağlar.

### **Closure ile Değişkenlerin Değiştirilmesi:**

```php
<?php
$value = 10;
$multiply = function($factor) use (&$value) {
    $value *= $factor;
};

$multiply(2);
echo $value;  // Çıktı: 20
?>
```

Burada, `&$value` ifadesi kullanılarak, dışarıdaki `$value` değişkeni doğrudan değiştirilebilir hale gelir. Bu, closure içinde yapılan değişikliklerin dışarıdaki değişkeni etkilemesini sağlar.

### **Sonuç**:
- **Anonymous Fonksiyonlar**, genellikle kısa ve geçici işlevsellikler için kullanılır.
- **Closure'lar**, fonksiyonların dış değişkenlere erişimini sağlamak için kullanılır ve fonksiyonel programlama yaklaşımını PHP'ye taşır.



### **1.10 PHP’de değişken değişkenler (`$$`) nasıl çalışır? Hangi durumlarda kullanılır?**  
✍ **Cevap:**   $$ operatörü, ilk olarak bir değişkenin değerini alır, ardından bu değeri kullanarak yeni bir değişkenin adını oluşturur.
 Yani, bir değişkenin değeri başka bir değişkenin adını belirleyebilir.

### **Nasıl Çalışır?**

`$$` operatörü, ilk olarak bir değişkenin değerini alır, ardından bu değeri kullanarak yeni bir değişkenin adını oluşturur.

### **Örnek:**

```php
<?php
$a = "merhaba";
$$a = "Dünya!";  // $$a, $merhaba'yı ifade eder.

echo $merhaba;  // Çıktı: Dünya!
?>
```

Burada:
- `$a = "merhaba";` ifadesiyle `$a` değişkenine `"merhaba"` değeri atanıyor.
- `$$a = "Dünya!";` ifadesi ise `$$a` ile `$merhaba` değişkenine `"Dünya!"` değerini atıyor.




### **1.11 PHP’de `list()` fonksiyonu ne işe yarar? Örnek vererek açıklayınız ?**  
✍ **Cevap:**  PHP’de list() fonksiyonu, bir dizinin elemanlarını, değişkenlere atamak için kullanılır. Özellikle sıralı dizilerle çalışırken, dizinin her bir elemanını kolayca ayrı değişkenlere yerleştirmeyi sağlar.

 **Örnek - Dizinin Elemanlarını Değişkenlere Atama:**

```php
<?php
$fruits = ["Elma", "Armut", "Kiraz"];

list($fruit1, $fruit2, $fruit3) = $fruits;

echo $fruit1;  // Çıktı: Elma
echo $fruit2;  // Çıktı: Armut
echo $fruit3;  // Çıktı: Kiraz
?>
```

### **1.12 PHP'de `compact()` ve `extract()` fonksiyonları ne işe yarar? Kullanım örnekleri veriniz.**  
✍ **Cevap:**  Bu fonksiyonlar, veri aktarımını kolaylaştırmak ve değişkenlerin dizi içinde yönetilmesini sağlamak için kullanılır.


PHP'de `compact()` ve `extract()` fonksiyonları, değişkenlerin dizilerle işlenmesini sağlayan fonksiyonlardır.

1. **`compact()` Fonksiyonu:**
   - Bu fonksiyon, bir veya birden fazla değişkenin adını alır ve bunları anahtar-değer çiftleri olarak içeren bir dizi döndürür. Değişken isimleri dizi anahtarı, değerleri ise dizi elemanı olur.

   **Örnek:**
   ```php
   <?php
   $ad = "Ali";
   $soyad = "Veli";
   $yas = 25;

   $dizi = compact("ad", "soyad", "yas");
   print_r($dizi);
    ?>
   ```
   **Çıktı:**
   ```bash

   Array
   (
       [ad] => Ali
       [soyad] => Veli
       [yas] => 25
   )
   ```

2. **`extract()` Fonksiyonu:**
   - Bu fonksiyon, bir dizi içindeki anahtarları alır ve bu anahtarları değişken ismi olarak kullanarak değerlerini o değişkenlere atar.

   **Örnek:**
   ```php
      <?php
   $dizi = array("ad" => "Ali", "soyad" => "Veli", "yas" => 25);
   
   extract($dizi);
   echo $ad;    // Ali
   echo $soyad; // Veli
   echo $yas;   // 25
   ?>
   ```


### **1.13 PHP’de `array_map()`, `array_filter()`, `array_reduce()` fonksiyonlarının kullanım farkları nelerdir?**  
✍ **Cevap:**  

- `array_map()`: Her eleman üzerinde işlem yapar ve yeni bir dizi döndürür.
- `array_filter()`: Elemanları filtreler ve belirtilen koşula uyanları döndürür.
- `array_reduce()`: Elemanları birleştirerek tek bir sonuç döndürür.

1. **`array_map()`**:
   - Bu fonksiyon, bir dizideki her bir eleman üzerinde belirtilen bir işlevi uygular ve her elemandan dönen sonuçları içeren yeni bir dizi döndürür.
   
   **Örnek:**
   ```php
    <?php
   $sayilar = [1, 2, 3];
   $yeniSayilar = array_map(function($x) {
       return $x + 1;
   }, $sayilar);
   
   print_r($yeniSayilar); // [2, 3, 4]
   ?>

   ```

2. **`array_filter()`**:
   - Bu fonksiyon, bir dizideki elemanları, belirtilen işlevle test eder ve **doğru** (truthy) değeri döndüren elemanları içeren yeni bir dizi döndürür. Yani, sadece belirli bir kritere uyan elemanları alır.
   
   **Örnek:**
   ```php
   <?php
   $sayilar = [1, 2, 3, 4, 5];
   $ciftSayilar = array_filter($sayilar, function($x) {
       return $x % 2 == 0;
   });
   
   print_r($ciftSayilar); // [2, 4]
 ?>
   ```

3. **`array_reduce()`**:
   - Bu fonksiyon, dizinin elemanlarını birleştirerek tek bir değer elde etmek için kullanılır. Her eleman, bir önceki sonucu ve o elemanı işleyen bir işlevle birleştirilir.
   
   **Örnek:**
   ```php
   <?php
   $sayilar = [1, 2, 3];
   $toplam = array_reduce($sayilar, function($carry, $item) {
       return $carry + $item;
   }, 0);
   
   echo $toplam; // 6
   ?>
   ```


### **1.14 PHP’de `serialize()` ve `unserialize()` fonksiyonları ne işe yarar? Hangi durumlarda kullanılır?**  
✍ **Cevap:** 

**`serialize()`** ve **`unserialize()`** fonksiyonları, PHP'deki verileri depolamak veya iletmek için kullanılır.

- **`serialize()`**: PHP değişkenlerini, dizileri, nesneleri gibi veri yapılarını, veritabanına veya dosyaya depolanabilen bir formata dönüştürür. Bu dönüşüm, veriyi metin formatında saklamayı sağlar.
  
  **Örnek Kullanım:**
  ```php
  <?php
  $veri = ['ad' => 'Ali', 'yas' => 25];
  $serileştirilmişVeri = serialize($veri);
  ?>
  ```

- **`unserialize()`**: `serialize()` ile dönüştürülmüş veriyi eski haline getirir, yani orijinal veri yapısına döndürür.

  **Örnek Kullanım:**
  ```php
  <?php
  $orijinalVeri = unserialize($serileştirilmişVeri);
  ?>
  ```

**Kullanım Durumları**:
- Veriyi oturumda (session) saklamak.
- Veritabanına veya dosyaya karmaşık veri yapıları depolamak.
- API'lerle veri iletimi sırasında veri yapılarının taşınması.


### **1.15 PHP'de `json_encode()` ve `json_decode()` fonksiyonları nasıl çalışır?**  
✍ **Cevap:**  

- `json_encode()`, PHP veri yapısını JSON string'ine dönüştürür.
- `json_decode()`, JSON string'ini PHP veri yapısına dönüştürür.

1. **`json_encode()`**: 
   Bu fonksiyon, PHP değişkenlerini JSON formatına dönüştürmek için kullanılır. Örneğin, bir dizi veya nesne, JSON string'e çevrilir.
   ```php
  <?php
   $array = array("isim" => "Abdullah", "yas" => 19);
   $json = json_encode($array);
   echo $json; // Çıktı: {"isim":"Abdullah","yas":19}
  ?>
   ```

2. **`json_decode()`**:
   JSON formatındaki bir string'i, PHP değişkenlerine (dizi veya nesne) dönüştürmek için kullanılır. JSON verisini PHP veri yapısına çevirmek için kullanılır.
   ```php
   <?php
   $json = '{"isim":"Abdullah","yas":19}';
   $array = json_decode($json, true); // true ile dizi formatında döner
   echo $array["isim"]; // Çıktı: Abdullah
   ?>
   ```


### **1.16 PHP’de `preg_match()` ve `preg_replace()` fonksiyonları ne işe yarar? Kullanım örnekleri veriniz.**  
✍ **Cevap:**  PHP’de `preg_match()` ve `preg_replace()` fonksiyonları, düzenli ifadeler (regular expressions) kullanarak metin üzerinde arama ve değiştirme işlemleri yapmayı sağlar. 

### 1. **`preg_match()` Fonksiyonu**
`preg_match()` fonksiyonu, bir düzenli ifade ile metinde arama yapar ve eşleşme bulursa `1`, bulamazsa `0` döner. Bu fonksiyon, sadece ilk eşleşmeyi kontrol eder.

**örnek:**
Aşağıdaki örnekte, bir HTML metninde `<a>` etiketini arıyoruz.

```php
<?php
$text = '<p>Bu bir <a href="http://example.com">link</a> içeriyor.</p>';

if (preg_match('/<a.*?>(.*?)<\/a>/', $text, $matches)) {
    echo "Link bulundu: " . $matches[1]; // Çıktı: link
} else {
    echo "Link bulunamadı.";
}
?>
```


### 2. **`preg_replace()` Fonksiyonu**
`preg_replace()` fonksiyonu, bir düzenli ifade ile metinde arama yapar ve eşleşen kısmı belirtilen bir değerle değiştirir.

**Kullanım örneği:**
Bu örnekte, metindeki tüm boşlukları _ karakteriyle değiştireceğiz.

```php
<?php
$text = "Bu bir örnek metin.";
$new_text = preg_replace('/\s+/', '_', $text);

echo $new_text; // Çıktı: Bu_bir_örnek_metın.
?>

```


### **1.17 PHP’de `explode()` ve `implode()` fonksiyonlarının farkları nelerdir?**  
✍ **Cevap:**  

- **`explode()`**: String'i böler ve bir dizi oluşturur.
- **`implode()`**: Diziyi birleştirir ve bir string oluşturur.

### **1. `explode()` Fonksiyonu:**
`explode()` fonksiyonu, bir string'i belirli bir ayırıcıya göre böler ve bir dizi (array) döndürür.

**Kullanım örneği:**
```php
<?php
$string = "elma,armut,muz";
$array = explode(",", $string);
print_r($array);
// Çıktı: Array ( [0] => elma [1] => armut [2] => muz )
?>
```
- **Amaç**: Bir string'i ayırıcıya göre dizilere böler.

 **2. `implode()` Fonksiyonu:**
`implode()` fonksiyonu, bir diziyi belirli bir ayırıcı ile birleştirir ve tek bir string döndürür.

**Kullanım örneği:**
```php
<?php
$array = ['elma', 'armut', 'muz'];
$string = implode(",", $array);
echo $string;
// Çıktı: elma,armut,muz
?>
```
- **Amaç**: Bir diziyi, belirtilen ayırıcı ile birleştirerek tek bir string oluşturur.


### **1.18 PHP’de `session` ve `cookie` farkları nelerdir? Hangi durumlarda kullanılır?**  
✍ **Cevap:**  


**`session`** ve **`cookie`** arasındaki farklar:

- **`session`**: Sunucuda veri saklar, tarayıcıda sadece oturum kimliği saklanır. Oturum süresince geçerlidir. Kullanıcı giriş bilgileri gibi güvenli veriler için kullanılır.
  
- **`cookie`**: Tarayıcıda veri saklar, belirli bir süre boyunca geçerlidir. Kullanıcı tercihleri, dil seçimi gibi veriler için kullanılır.

**Farklar**:
- **`session`**: Sunucuda, oturum bazlı.
- **`cookie`**: Tarayıcıda, belirli bir süre için geçerli.

**Kullanım Durumu**:
- **`session`**: Kısa vadeli, güvenli veri saklama.
- **`cookie`**: Uzun vadeli veri saklama.

### **1.19 PHP’de `header()` fonksiyonu nasıl çalışır? Hangi durumlarda kullanılır?**  
✍ **Cevap:**  
**PHP'deki `header()` fonksiyonu**, HTTP başlıkları (headers) göndermek için kullanılır. Bu başlıklar, tarayıcıya veya diğer istemcilere yönlendirme, içerik tipi belirtme, CORS ayarları yapma gibi işlemler için kullanılır.

### **Nasıl Çalışır?**
`header()` fonksiyonu, HTTP yanıt başlıklarını tarayıcıya göndermek için kullanılır. Başlıklar gönderilmeden önce herhangi bir çıktı yapılmamalıdır (örneğin, `echo` veya boşluk).



### **Kullanım Durumları:**

1. **Yönlendirme (Redirect)**: Kullanıcıyı başka bir sayfaya yönlendirmek için kullanılır.
   ```php
  <?php
   header("Location: yeni_sayfa.php");
   exit();
   ?>
   ```

2. **CORS Ayarları**: Farklı domainlerden gelen isteklere izin vermek için kullanılır.
   ```php
      <?php
   header("Access-Control-Allow-Origin: *");  // Tüm domainlerden gelen isteklere izin verir
      ?>
   ```

3. **İçerik Tipi Belirleme**: Tarayıcıya içerik türünü belirtmek için kullanılır.
   ```php
   <?php
   header("Content-Type: application/json");
   ?>
   ```

### **Önemli Noktalar:**
- `header()` fonksiyonu **çıkış yapılmadan önce** kullanılmalıdır.
- CORS ayarları, API'lerin başka domainlerden erişilmesine izin vermek için önemlidir.

### **1.20 PHP’de `ob_start()` ve `ob_get_clean()` fonksiyonları ne işe yarar?**  
✍ **Cevap:**  
`ob_start()` ve `ob_get_clean()` PHP'de çıktı tamponlama (output buffering) işlemleri için kullanılır.

- **`ob_start()`**: Çıktıyı ekrana yazdırmak yerine bir tamponda (buffer) tutmaya başlar. Yani, PHP scripti çalışırken üretilen çıktı ekrana yazdırılmaz, önce tamponda birikir.
  
- **`ob_get_clean()`**: Tampondaki çıktıyı alır ve tamponu temizler. Bu şekilde, çıktıyı bir değişkene atayıp, başka bir işlem yapmadan önce kullanabilirsiniz.

Tampon (buffer), verilerin geçici olarak saklandığı bir bellek alanıdır. PHP'deki çıktı tamponlaması da bu konsepti kullanır. Normalde PHP, script çalıştıkça ürettiği verileri doğrudan ekrana gönderir. Ancak tampon kullanıldığında, bu veriler önce bellekte biriktirilir ve sonradan bir işlem yapılmadan ekrana basılmaz.

### **1.21 PHP’de `str_replace()` ve `substr_replace()` fonksiyonlarının farkları nelerdir?**  
✍ **Cevap:**  **`str_replace()`** ve **`substr_replace()`** fonksiyonları arasındaki farklar şunlardır:

- **`str_replace()`**: Belirtilen bir metindeki bir veya birden fazla karakteri başka bir karakterle değiştirmek için kullanılır. Bu fonksiyon, tüm metni tarar ve bulduğu eşleşmeleri değiştirir.
  
  Örnek:  
  ```php
    <?php
  $metin = "Merhaba Dünya";
  echo str_replace("Dünya", "PHP", $metin);  // Çıktı: Merhaba PHP
  ?>
  ```

- **`substr_replace()`**: Bir metnin belirli bir kısmını, belirtilen pozisyondan başlayarak değiştirmek için kullanılır. Burada, değiştirilmek istenen kısmın başlangıç ve uzunluğu belirtilir.
  
  Örnek:  
  ```php
  <?php
  $metin = "Merhaba Dünya";
  echo substr_replace($metin, "PHP", 8, 5);  // Çıktı: Merhaba PHP
  ?>
  ```

Özetle, `str_replace()` tüm metni tarar ve belirli bir kelimeyi değiştirirken, `substr_replace()` metnin belirli bir kısmını değiştirir.

### **1.22 PHP’de hata seviyeleri nelerdir (`E_ERROR`, `E_WARNING`, `E_NOTICE`, vb.)?**  
✍ **Cevap:**  
PHP’de farklı hata seviyeleri şunlardır:

- **`E_ERROR`**: Kritik hatalar. Scriptin çalışmasını durdurur. (Örneğin, bir fonksiyonun bulunamaması)
- **`E_WARNING`**: Uyarılar. Scriptin çalışmasını durdurmaz, fakat potansiyel sorunları bildirir. (Örneğin, bir dosyanın bulunamaması)
- **`E_NOTICE`**: Bildirimler. Çoğunlukla kodda potansiyel hatalar veya iyileştirme fırsatları olduğunu belirtir. (Örneğin, tanımlanmamış bir değişken kullanımı)
- **`E_PARSE`**: Derleme hataları. PHP kodunun sözdizimi hatalarından kaynaklanır.
- **`E_DEPRECATED`**: Kullanımdan kaldırılan özellikler. Kodda kullanılan eski fonksiyonların veya yapılarının kullanımı uyarılır.
- **`E_USER_ERROR`, `E_USER_WARNING`, `E_USER_NOTICE`**: Kullanıcı tarafından tetiklenen hata seviyeleri. `trigger_error()` fonksiyonu ile tetiklenebilirler.
- **`E_ALL`**: Tüm hata seviyelerini içerir. Genellikle geliştirme aşamasında kullanılır.

Her hata seviyesi farklı önemdeki sorunları belirtir ve hataların tespiti ile çözüm için yardımcı olur.

### **1.23 PHP'de `try-catch-finally` yapısı nasıl çalışır? Hata yönetimi için en iyi uygulamalar nelerdir?**  
✍ **Cevap:**  
**`try-catch-finally` yapısı**, PHP'de hata yönetimi için kullanılır. Çalışma mantığı şu şekildedir:

- **`try`**: Hata oluşması muhtemel kodlar burada yazılır. Eğer bu blokta bir hata oluşursa, `catch` bloğuna geçilir.
- **`catch`**: Hata oluştuğunda çalışacak kodlar burada yazılır. `try` bloğunda oluşan hata burada yakalanır ve işlenir.
- **`finally`**: Hata oluşsa da oluşmasa da her durumda çalışacak olan kod burada bulunur. Genellikle temizlik işlemleri veya kaynakları serbest bırakma gibi işler için kullanılır.

### Örnek:
```php
<?php
try {
    // Hata oluşturabilecek kod
    $x = 1 / 0;  // Bu sıfıra bölme hatası yaratır
} catch (Exception $e) {
    // Hata yakalandığında yapılacak işlemler
    echo "Hata: " . $e->getMessage();
} finally {
    // Her durumda yapılacak işlemler
    echo "Bu blok her durumda çalışır.";
}
?>
```

**Hata yönetimi için en iyi uygulamalar**:
- 1. **Spesifik hataları yakalayın**: `catch` bloğunda çok genel yerine daha spesifik hata türlerini kullanın.
- 2. **Hata mesajlarını gizleyin**: Kullanıcılara detaylı hata mesajları vermek yerine genel bir mesaj gösterin.
- 3. **Loglama yapın**: Hataları bir log dosyasına kaydedin, böylece hatalar sonradan analiz edilebilir.
- 4. **Temiz kaynak yönetimi**: `finally` bloğunda kaynakları serbest bırakın veya temizleme işlemleri yapın.

Bu yapı, uygulamanın hatalı durumlar karşısında daha sağlam ve kontrollü bir şekilde çalışmasını sağlar.

### **1.24 PHP’de `mysqli` ve `PDO` arasındaki farklar nelerdir? Hangisi ne zaman tercih edilmelidir?**  
✍ **Cevap:**  

**`mysqli`** ve **`PDO`** PHP'deki iki farklı veritabanı bağlantı yöntemidir. Aralarındaki farklar şunlardır:

- **`mysqli`**: 
  - Sadece MySQL veritabanlarını destekler.
  - Hem prosedürel hem de nesne yönelimli (OOP) olarak kullanılabilir.
  - Daha fazla MySQL'e özgü özellik sunar (örneğin, hazırlanan ifadeler).
  - Performans açısından genellikle daha hızlıdır.

- **`PDO`**:
  - Birden fazla veritabanı türünü (MySQL, PostgreSQL, SQLite, vb.) destekler.
  - Yalnızca nesne yönelimli (OOP) olarak kullanılır.
  - Veritabanı bağımsızlığı sağlar, yani farklı veritabanlarına kolayca geçiş yapılabilir.
  - Hazırlanan ifadelerle birlikte çalışabilir, ancak bazı veritabanı özelliklerine `mysqli` kadar doğrudan erişim sağlamaz.

### Ne zaman hangisi tercih edilmelidir?
- **`mysqli`**: Eğer sadece MySQL kullanıyorsanız ve MySQL'e özgü gelişmiş özelliklere ihtiyacınız varsa, `mysqli` daha uygun olabilir.
- **`PDO`**: Birden fazla veritabanı kullanmayı planlıyorsanız veya veritabanı bağımsızlığı istiyorsanız, `PDO` tercih edilmelidir. Ayrıca, modern uygulamalar için daha esneklik sağlar.




---
