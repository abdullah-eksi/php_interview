
# **5. Performans ve Optimizasyon**  

### **5.1 PHP’de opcode caching (opcode önbellekleme) nedir ve nasıl kullanılır?**  
✍ **Cevap:**  
Opcode caching, PHP’nin derlenmiş byte kodlarını önbelleğe alarak tekrar derlemeyi önler, böylece uygulama daha hızlı çalışır. OPcache PHP’nin standart opcode cache mekanizmasıdır ve opcache.enable direktifi ile etkinleştirilebilir.

### **5.2 PHP’de `array_map()` ile `foreach` arasındaki performans farkları nelerdir?**  
✍ **Cevap:**  
array_map(), daha fonksiyonel ve daha kısa yazım sağlar, ancak foreach genellikle daha hızlıdır, çünkü array_map() her zaman bir fonksiyon çağrısı yapar.

### **5.3 Büyük boyutlu verileri işlerken bellek tüketimini azaltmak için hangi PHP tekniklerini kullanırsınız?**  
✍ **Cevap:**  
Veri setini parçalara bölerek işleme, yield kullanarak jeneratörlerle veri akışını kontrol etme, büyük dosyalarla çalışırken fgetcsv() gibi okuma fonksiyonlarını tercih etme.

### **5.4 Laravel gibi frameworklerde cache mekanizmalarını nasıl optimize edersiniz?**  
✍ **Cevap:**  
Cache türlerini doğru seçmek (Redis, Memcached), veri önbelleklemeyi doğru zamanlarda yaparak, önbellek temizleme stratejileri uygulayarak, gereksiz cache veri yükünü azaltmak.

### **5.5 PHP’de asenkron işlemler nasıl gerçekleştirilir?**  
✍ **Cevap:**  
popen(), exec(), shell_exec() gibi fonksiyonlarla dış işlemleri asenkron başlatmak, ReactPHP veya Swoole gibi kütüphaneler kullanarak asenkron programlamayı mümkün kılmak.

### **5.6 PHP’de session optimizasyonu nasıl yapılır?**  
✍ **Cevap:**  
Session veri boyutlarını küçültmek, veritabanı yerine dosya tabanlı session yönetimini optimize etmek, session çöp temizleme süresini doğru ayarlamak.

### **5.7 PHP’de yük dengeleme (load balancing) nasıl yapılır?**  
✍ **Cevap:**  
PHP uygulamalarını birden fazla sunucuya dağıtarak, bir proxy (nginx, HAProxy) veya cloud load balancing hizmeti (AWS ELB) kullanarak trafiği yönlendirmek.

### **5.8 PHP’de işlemciyi yormadan büyük verileri nasıl işleriz?**  
✍ **Cevap:**  
Veri işlemesini paralel hale getirmek, yield ile jeneratörler kullanmak, işlemciden bağımsız olarak verileri arka planda işlemek.

### **5.9 PHP’de `ob_start()` fonksiyonunun performansa etkisi nedir?**  
✍ **Cevap:**  
ob_start(), çıktı tamponlaması yaparak verinin daha verimli bir şekilde gönderilmesini sağlar; ancak fazla tamponlama belleği arttırabilir ve gecikmelere yol açabilir.

### **5.10 PHP’de veritabanı sorgularını optimize etmek için en iyi yöntemler nelerdir?**  
✍ **Cevap:**  
İndeksleme kullanmak, gereksiz sorguları optimize etmek, JOIN'lerden kaçınmak, WHERE koşullarını doğru kullanmak, LIMIT ile sorguları sınırlandırmak.

### **5.11 PHP’de `isset()`, `empty()` ve `is_null()` fonksiyonlarının performans farkları nelerdir?**  
✍ **Cevap:**  
isset() daha hızlıdır çünkü sadece değişkenin varlığını kontrol eder. empty() ise değeri ve varlığı kontrol eder, is_null() ise sadece null olup olmadığını kontrol eder.

### **5.12 PHP’de `file_get_contents()` ile `fopen()` kullanımı arasındaki farklar ve performansa etkileri nelerdir?**  
✍ **Cevap:**  
file_get_contents() tüm dosyayı hafızaya alır, küçük dosyalar için hızlıdır. fopen() ise daha büyük dosyalarla çalışırken belleği daha verimli kullanarak satır satır okuma sağlar.

### **5.13 PHP’de JSON işlemlerini hızlandırmak için hangi teknikler kullanılabilir?**  
✍ **Cevap:**  
PHP’nin json_encode() ve json_decode() fonksiyonlarını doğrudan kullanmak, veri yapılarının basitleştirilmesi, sık kullanılan JSON verilerini önbelleğe almak.

### **5.14 PHP’de CDN kullanımı performansı nasıl etkiler?**  
✍ **Cevap:**  
CDN, statik içerikleri (resimler, CSS, JS) kullanıcıya daha yakın bir sunucudan sunarak yükleme hızını artırır ve sunucu üzerindeki yükü azaltır.

### **5.15 PHP’de GZIP sıkıştırma nasıl yapılır ve sayfa yükleme süresine etkisi nedir?**  
✍ **Cevap:**  
GZIP sıkıştırma, sayfa boyutunu küçültür ve sayfa yükleme süresini azaltır. PHP’de ob_start("ob_gzhandler") kullanarak etkinleştirilebilir.

### **5.16 PHP’de uzun süre çalışan scriptler nasıl optimize edilir?**  
✍ **Cevap:**  
Zaman uyumsuz işlemler (asenkron), işlem sürelerini parçalayarak küçük işlemler yapmak, işlemci ve bellek optimizasyonları.

### **5.17 PHP’de indeksleme (indexing) ve partitioning veritabanı performansını nasıl etkiler?**  
✍ **Cevap:** 
İndeksleme, sorguları hızlandırır. Partitioning, veritabanı tablosunun bölünmesini sağlayarak büyük veri setleriyle çalışırken daha verimli sorgular yapılmasını sağlar.

### **5.18 PHP’de bellek yönetimi nasıl optimize edilir? (`gc_collect_cycles()` gibi fonksiyonların kullanımı)**  
✍ **Cevap:**  
Çöpleri temizlemek için gc_collect_cycles() fonksiyonu kullanılabilir. Bellek kullanımını izlemek ve envanterlere gerekirse unset() ile bellek boşaltmak.

### **5.19 PHP’de çoklu işlem (multi-threading) nasıl gerçekleştirilir?**  
✍ **Cevap:**  
PHP'de çoklu işlem için pthreads veya Swoole gibi kütüphaneler kullanılabilir, ancak PHP çoklu iş parçacığına doğrudan destek vermez.

### **5.20 PHP’de API performansını artırmak için hangi yöntemler kullanılır?**  
✍ **Cevap:**  
Veri önbellekleme (cache), hızlı JSON işleme, API limitleri kullanarak aşırı yükü engelleme, API yanıtlarını sıkıştırma, asenkron işlemler kullanmak.

