
# **4. Güvenlik**

Tabii, işte istenilen formatta soruların cevapları:

### **4.1 SQL Injection nedir? PHP’de nasıl önlenir?**  
✍ **Cevap:** SQL Injection, kötü niyetli kullanıcıların veritabanına zararlı SQL komutları göndermesiyle gerçekleşen bir saldırıdır. PHP’de önlemek için **prepared statements** (hazırlanmış ifadeler) ve **PDO** (PHP Data Objects) kullanılmalıdır.

### **4.2 XSS (Cross-Site Scripting) saldırısı nedir? PHP ile nasıl önüne geçilir?**  
✍ **Cevap:** XSS, saldırganların zararlı script kodlarını web sayfasına ekleyerek, kullanıcının tarayıcısında çalıştırmalarını sağlar. PHP'de **output encoding** ve **htmlspecialchars()** fonksiyonu kullanarak önlenebilir.

### **4.3 CSRF (Cross-Site Request Forgery) saldırılarına karşı PHP’de nasıl önlem alınır?**  
✍ **Cevap:** CSRF saldırılarında, kötü niyetli bir site kullanıcının kimliğini taklit eder. PHP’de **CSRF token** kullanarak her form için benzersiz bir token eklenebilir.

### **4.4 PHP’de parola güvenliği sağlamak için `password_hash()` ve `password_verify()` nasıl kullanılır?**  
✍ **Cevap:** `password_hash()` parolayı güvenli bir şekilde şifreler, `password_verify()` ise girilen parolanın doğruluğunu kontrol eder.

### **4.5 PHP'de güvenli oturum yönetimi için alınması gereken önlemler nelerdir?**  
✍ **Cevap:** Oturum ID’si sabit olmamalı, **session_regenerate_id()** kullanılmalı, ve **secure**, **HttpOnly** ve **SameSite** cookie ayarları yapılmalıdır.

### **4.6 HTTPS ve SSL kullanımının PHP projelerinde önemi nedir?**  
✍ **Cevap:** HTTPS ve SSL, veri iletimini şifreler ve iletişim güvenliğini sağlar. PHP projelerinde **SSL sertifikası** kullanarak şifreli bağlantı sağlanmalıdır.

### **4.7 PHP ile güvenli API authentication nasıl yapılır? (JWT, OAuth vs.)**  
✍ **Cevap:** JWT (JSON Web Token) ve OAuth, API’lerde güvenli kimlik doğrulama sağlar. PHP’de JWT ile her API isteği için geçerli bir token gönderilmelidir.

### **4.8 PHP’de kullanıcı doğrulaması nasıl yapılır? En iyi doğrulama yöntemleri nelerdir?**  
✍ **Cevap:** Kullanıcı doğrulaması için **email doğrulama**, **Captcha** kullanımı ve **OAuth** gibi üçüncü taraf doğrulama yöntemleri önerilir.

### **4.9 PHP’de session hijacking ve session fixation saldırılarına karşı nasıl önlem alınır?**  
✍ **Cevap:** **session_regenerate_id()** fonksiyonu kullanılmalı, ve güvenli session cookie ayarları yapılmalıdır.

### **4.10 PHP’de güvenli şifre sıfırlama mekanizması nasıl olmalıdır?**  
✍ **Cevap:** Şifre sıfırlama linki geçici olmalı, **hashing** ile doğrulama yapılmalı ve kullanıcıya yeni şifreyi kendisi belirleme imkanı sunulmalıdır.

### **4.11 PHP’de input validation (girdi doğrulama) ve output encoding (çıktı kodlama) nasıl yapılır?**  
✍ **Cevap:** Girdi doğrulama için **filter_var()** fonksiyonu kullanılmalı, çıktı kodlaması içinse **htmlspecialchars()** ve **htmlentities()** gibi fonksiyonlar kullanılmalıdır.

### **4.12 PHP'de cookie güvenliği nasıl sağlanır?**  
✍ **Cevap:** Cookie güvenliği için **secure**, **HttpOnly** ve **SameSite** attribute'ları kullanılmalı ve cookies şifreli olmalıdır.

### **4.13 SQL Injection ve XSS dışında PHP projelerinde yaygın olan güvenlik açıkları nelerdir?**  
✍ **Cevap:** Diğer yaygın güvenlik açıkları arasında **XML External Entity (XXE)** saldırıları, **file inclusion** açıkları ve **misconfigured permissions** yer alır.

### **4.14 PHP’de dosya yükleme güvenliği nasıl sağlanır?**  
✍ **Cevap:** Dosya türü ve boyutu doğrulanmalı, dosya adı rastgele oluşturulmalı ve dosyalar güvenli bir dizine yüklenmelidir.

### **4.15 PHP ile dosya erişim kontrolü nasıl yapılır? Özellikle dışarıya açık dosyaların güvenliğine dikkat edilmelidir?**  
✍ **Cevap:** Dosya erişim kontrolü için **file permissions** ve **directory restrictions** ayarlanmalı, dışarıya açık dosyalar şifrelenmeli veya güvenlik katmanları eklenmelidir.

### **4.16 Web uygulamaları için güvenlik testleri ve denetimleri nasıl yapılır? PHP’de bu testleri nasıl uygulayabiliriz?**  
✍ **Cevap:** Güvenlik testleri için **penetration testing**, **vulnerability scanning** ve **code review** yapılmalı. PHP’de güvenlik testleri için **OWASP ZAP** gibi araçlar kullanılabilir.

### **4.17 PHP projelerinde Dependency Injection kullanarak güvenliği nasıl artırabiliriz?**  
✍ **Cevap:** Dependency Injection, kodun test edilebilirliğini ve bakımını artırır, ayrıca **loose coupling** sağlayarak güvenliği iyileştirir.

### **4.18 PHP’de X-Content-Type-Options başlığının önemi nedir ve nasıl kullanılır?**  
✍ **Cevap:** Bu başlık, tarayıcıların içerik türünü belirlemesini zorunlu kılar, **X-Content-Type-Options: nosniff** kullanarak MIME sniffing saldırılarına karşı korunabilir.

### **4.19 PHP’de Content Security Policy (CSP) nasıl uygulanır ve güvenliği nasıl artırır?**  
✍ **Cevap:** CSP, yalnızca güvenilir kaynaklardan gelen içeriklerin yüklenmesine izin verir. PHP’de CSP başlıkları, **header()** fonksiyonu ile ayarlanabilir.

### **4.20 PHP’de Logging (loglama) güvenliğinin sağlanması nasıl yapılır?**  
✍ **Cevap:** Log dosyaları şifrelenmeli, hassas bilgiler içermemeli ve **rotate log** sistemiyle düzenli olarak temizlenmelidir.

### **4.21 PHP’de güvenli bir şekilde e-posta gönderimi nasıl yapılır?**  
✍ **Cevap:** E-posta gönderimi için **PHPMailer** gibi güvenli bir kütüphane kullanılmalı, SMTP üzerinden güvenli iletişim sağlanmalıdır.

### **4.22 PHP'de 2FA (İki faktörlü kimlik doğrulama) nasıl implement edilir?**  
✍ **Cevap:** 2FA için **Google Authenticator** veya **TOTP** (Time-based One-Time Password) kullanılabilir, her oturum açmada ek doğrulama gerektirilebilir.

### **4.23 PHP projelerinde güvenli yazılım geliştirme yaşam döngüsü (SDLC) nasıl uygulanır?**  
✍ **Cevap:** Güvenli yazılım geliştirme süreci, **güvenlik gereksinimlerinin** baştan belirlenmesi, **kod incelemeleri** ve **penetration testing** ile sağlanmalıdır.

### **4.24 PHP’de güvenlik güncellemeleri ve yamalar nasıl yönetilir?**  
✍ **Cevap:** Güvenlik güncellemeleri düzenli olarak takip edilmeli, **composer update** ve **PHP sürüm yükseltmeleri** yapılmalıdır.

### **4.25 PHP’de Veritabanı ve Uygulama Sunucusu arasındaki güvenli iletişim nasıl sağlanır?**  
✍ **Cevap:** Veritabanı ve sunucu arasındaki iletişim şifreli bağlantılarla sağlanmalı ve **SSL/TLS** protokolleri kullanılmalıdır.

### **4.26 PHP projelerinde ağ güvenliği için hangi önlemler alınmalıdır?**  
✍ **Cevap:** Ağ güvenliği için **firewall**, **VPN** ve **IDS/IPS** gibi önlemler alınmalı ve güvenli portlar kullanılmalıdır.

### **4.27 PHP projelerinde API rate limiting (sınırlama) nasıl uygulanır?**  
✍ **Cevap:** API rate limiting, **Redis** veya **nginx** gibi araçlarla uygulanabilir ve aşırı kullanım sınırlanabilir.

### **4.28 PHP’de brute-force saldırılarına karşı nasıl koruma sağlanır?**  
✍ **Cevap:** Brute-force saldırılarına karşı **login denemeleri** sınırlanmalı, **CAPTCHA** eklenmeli ve **hesap kilitleme** özellikleri kullanılmalıdır.

### **4.29 PHP’de Web Application Firewall (WAF) kullanımı nasıl olmalıdır?**  
✍ **Cevap:** WAF, saldırı ve kötüye kullanım tespit sistemleri ile yapılandırılmalı, PHP projelerinde uygulama katmanında güvenliği sağlamalıdır.
