# 4- Güvenlik

### **4.1 SQL Injection nedir? PHP’de nasıl önlenir?**  
✍ **Cevap:**  
SQL Injection, kullanıcı girdilerinin doğrudan SQL sorgularına eklenmesiyle oluşan bir güvenlik açığıdır. Bu, saldırganların veritabanını manipüle etmesine veya hassas verilere erişmesine neden olabilir.  
**Önlemler:**  
- **Prepared Statements (Hazırlanmış İfadeler):** PDO veya MySQLi kullanarak parametreli sorgular yazılmalıdır.  
- **PDO Örneği:**  
  ```php
  $stmt = $pdo->prepare("SELECT * FROM users WHERE email = :email");
  $stmt->execute(['email' => $email]);
  $user = $stmt->fetch();
  ```  
- **MySQLi Örneği:**  
  ```php
  $stmt = $mysqli->prepare("SELECT * FROM users WHERE email = ?");
  $stmt->bind_param("s", $email);
  $stmt->execute();
  $result = $stmt->get_result();
  ```  
- **Girdi Doğrulama:** Kullanıcı girdileri mutlaka doğrulanmalı ve temizlenmelidir.  

---

### **4.2 XSS (Cross-Site Scripting) saldırısı nedir? PHP ile nasıl önüne geçilir?**  
✍ **Cevap:**  
XSS, saldırganların zararlı JavaScript kodlarını web sayfasına enjekte etmesiyle gerçekleşir. Bu, kullanıcıların tarayıcısında çalışarak oturum bilgilerini çalma gibi sonuçlara yol açabilir.  
**Önlemler:**  
- **Output Encoding:** Kullanıcıdan gelen verileri ekrana yazdırırken `htmlspecialchars()` fonksiyonu kullanılmalıdır.  
  ```php
  echo htmlspecialchars($userInput, ENT_QUOTES, 'UTF-8');
  ```  
- **Content Security Policy (CSP):** Tarayıcıya hangi kaynakların güvenilir olduğunu belirtmek için CSP başlıkları kullanılmalıdır.  

---

### **4.3 CSRF (Cross-Site Request Forgery) saldırılarına karşı PHP’de nasıl önlem alınır?**  
✍ **Cevap:**  
CSRF, saldırganların kullanıcının oturumunu kullanarak istek göndermesine neden olur.  
**Önlemler:**  
- **CSRF Token:** Her form için benzersiz bir token oluşturulmalı ve doğrulanmalıdır.  
  ```php
  session_start();
  if ($_SERVER['REQUEST_METHOD'] === 'POST') {
      if (!isset($_POST['csrf_token']) || $_POST['csrf_token'] !== $_SESSION['csrf_token']) {
          die("CSRF saldırısı tespit edildi!");
      }
  }
  $_SESSION['csrf_token'] = bin2hex(random_bytes(32));
  ```  
- **SameSite Cookie Attribute:** Cookie'lerde `SameSite=Strict` veya `SameSite=Lax` kullanılmalıdır.  

---

### **4.4 PHP’de parola güvenliği sağlamak için `password_hash()` ve `password_verify()` nasıl kullanılır?**  
✍ **Cevap:**  
- **password_hash():** Parolayı güvenli bir şekilde şifreler.  
  ```php
  $password = "sifre123";
  $hashedPassword = password_hash($password, PASSWORD_DEFAULT);
  ```  
- **password_verify():** Girilen parolanın doğruluğunu kontrol eder.  
  ```php
  if (password_verify($password, $hashedPassword)) {
      echo "Parola doğru!";
  } else {
      echo "Parola yanlış!";
  }
  ```  

---

### **4.5 PHP'de güvenli oturum yönetimi için alınması gereken önlemler nelerdir?**  
✍ **Cevap:**  
- **Oturum ID’sini Yenileme:** Her oturum açıldığında `session_regenerate_id(true)` kullanılmalıdır.  
- **Güvenli Cookie Ayarları:**  
  ```php
  session_set_cookie_params([
      'lifetime' => 3600,
      'path' => '/',
      'domain' => 'example.com',
      'secure' => true, // Sadece HTTPS üzerinden
      'httponly' => true, // JavaScript erişimine kapat
      'samesite' => 'Strict'
  ]);
  ```  
- **Oturum Süresi:** Oturum süresi kısa tutulmalı ve zaman aşımına uğratılmalıdır.  

---

### **4.6 HTTPS ve SSL kullanımının PHP projelerinde önemi nedir?**  
✍ **Cevap:**  
HTTPS, verilerin şifrelenerek iletilmesini sağlar. Bu, kullanıcı bilgilerinin ve oturum bilgilerinin güvenliğini artırır.  
**Önlemler:**  
- **SSL Sertifikası:** Sunucuda geçerli bir SSL sertifikası kullanılmalıdır.  
- **HTTP’den HTTPS’e Yönlendirme:**  
  ```php
  if ($_SERVER['HTTPS'] !== 'on') {
      header("Location: https://" . $_SERVER['HTTP_HOST'] . $_SERVER['REQUEST_URI']);
      exit();
  }
  ```  

---

### **4.7 PHP ile güvenli API authentication nasıl yapılır? (JWT, OAuth vs.)**  
✍ **Cevap:**  
- **JWT (JSON Web Token):** Her istekte geçerli bir token gönderilir.  
  ```php
  use Firebase\JWT\JWT;
  $key = "gizli_anahtar";
  $payload = [
      "user_id" => 123,
      "exp" => time() + 3600 // 1 saat geçerli
  ];
  $jwt = JWT::encode($payload, $key);
  ```  
- **OAuth:** Üçüncü taraf kimlik doğrulama için kullanılır.  

---

### **4.8 PHP’de kullanıcı doğrulaması nasıl yapılır? En iyi doğrulama yöntemleri nelerdir?**  
✍ **Cevap:**  
- **Email Doğrulama:** Kullanıcıya doğrulama linki gönderilir.  
- **Captcha:** Otomatik bot saldırılarını önlemek için kullanılır.  
- **OAuth:** Google, Facebook gibi üçüncü taraf kimlik doğrulama yöntemleri kullanılabilir.  

---

### **4.9 PHP’de session hijacking ve session fixation saldırılarına karşı nasıl önlem alınır?**  
✍ **Cevap:**  
- **session_regenerate_id(true):** Oturum ID’sini yenileyerek fixation saldırılarını önler.  
- **Güvenli Cookie Ayarları:** `secure`, `httponly` ve `samesite` özellikleri kullanılmalıdır.  

---

### **4.10 PHP’de güvenli şifre sıfırlama mekanizması nasıl olmalıdır?**  
✍ **Cevap:**  
- **Geçici Token:** Şifre sıfırlama linki geçici bir token içermelidir.  
- **Token Süresi:** Token’ın geçerlilik süresi kısa tutulmalıdır (örneğin, 1 saat).  
- **Güvenli Şifreleme:** Token, güvenli bir şekilde şifrelenmelidir.  

---

### **4.11 PHP’de input validation (girdi doğrulama) ve output encoding (çıktı kodlama) nasıl yapılır?**  
✍ **Cevap:**  
- **Input Validation:**  
  ```php
  $email = filter_var($_POST['email'], FILTER_VALIDATE_EMAIL);
  if (!$email) {
      die("Geçersiz email!");
  }
  ```  
- **Output Encoding:**  
  ```php
  echo htmlspecialchars($userInput, ENT_QUOTES, 'UTF-8');
  ```  

---

### **4.12 PHP'de cookie güvenliği nasıl sağlanır?**  
✍ **Cevap:**  
- **secure:** Cookie’ler sadece HTTPS üzerinden gönderilmelidir.  
- **httponly:** JavaScript’in cookie’lere erişimi engellenmelidir.  
- **samesite:** Cross-site request forgery saldırılarını önlemek için kullanılır.  

---

### **4.13 SQL Injection ve XSS dışında PHP projelerinde yaygın olan güvenlik açıkları nelerdir?**  
✍ **Cevap:**  
- **File Inclusion:** `include` veya `require` ile dosya yolu kullanıcı girdisine bağlı olmamalıdır.  
- **XML External Entity (XXE):** XML dosyaları işlenirken dış entity’ler devre dışı bırakılmalıdır.  
- **Misconfigured Permissions:** Dosya ve dizin izinleri doğru ayarlanmalıdır.  

---

### **4.14 PHP’de dosya yükleme güvenliği nasıl sağlanır?**  
✍ **Cevap:**  
- **Dosya Türü Doğrulama:**  
  ```php
  $allowedTypes = ['image/jpeg', 'image/png'];
  if (!in_array($_FILES['file']['type'], $allowedTypes)) {
      die("Geçersiz dosya türü!");
  }
  ```  
- **Dosya Adı Rastgeleleştirme:**  
  ```php
  $fileName = uniqid() . "_" . basename($_FILES['file']['name']);
  ```  
- **Dosya Boyutu Sınırlama:**  
  ```php
  if ($_FILES['file']['size'] > 5000000) {
      die("Dosya boyutu çok büyük!");
  }
  ```  

---

### **4.15 PHP ile dosya erişim kontrolü nasıl yapılır? Özellikle dışarıya açık dosyaların güvenliğine dikkat edilmelidir?**  
✍ **Cevap:**  
- **Dosya İzinleri:** Dosyalar ve dizinler için uygun izinler ayarlanmalıdır (örneğin, 644 veya 755).  
- **Dosya Yolu Kontrolü:** Kullanıcı girdisi ile dosya yolu oluşturulmamalıdır.  
- **.htaccess ile Koruma:** Dışarıya açık dosyalar `.htaccess` ile korunabilir.  

---

### **4.16 Web uygulamaları için güvenlik testleri ve denetimleri nasıl yapılır? PHP’de bu testleri nasıl uygulayabiliriz?**  
✍ **Cevap:**  
- **Penetration Testing:** OWASP ZAP veya Burp Suite gibi araçlarla testler yapılabilir.  
- **Code Review:** Kod içinde güvenlik açıkları taranmalıdır.  
- **Vulnerability Scanning:** Otomatik tarama araçları kullanılabilir.  

---

### **4.17 PHP projelerinde Dependency Injection kullanarak güvenliği nasıl artırabiliriz?**  
✍ **Cevap:**  
Dependency Injection, bağımlılıkları dışarıdan enjekte ederek kodun test edilebilirliğini ve güvenliğini artırır. Örneğin, veritabanı bağlantısı dışarıdan enjekte edilerek SQL Injection riski azaltılabilir.  

---

### **4.18 PHP’de X-Content-Type-Options başlığının önemi nedir ve nasıl kullanılır?**  
✍ **Cevap:**  
Bu başlık, tarayıcıların içerik türünü belirlemesini zorunlu kılar.  
```php
header("X-Content-Type-Options: nosniff");
```  

---

### **4.19 PHP’de Content Security Policy (CSP) nasıl uygulanır ve güvenliği nasıl artırır?**  
✍ **Cevap:**  
CSP, yalnızca güvenilir kaynaklardan gelen içeriklerin yüklenmesine izin verir.  
```php
header("Content-Security-Policy: default-src 'self'; script-src 'self' https://trusted.cdn.com");
```  

---

### **4.20 PHP’de Logging (loglama) güvenliğinin sağlanması nasıl yapılır?**  
✍ **Cevap:**  
- **Log Dosyaları Şifrelenmeli:** Hassas bilgiler içermemelidir.  
- **Rotate Log:** Log dosyaları düzenli olarak temizlenmelidir.  
- **Log Erişimi Kısıtlanmalı:** Log dosyalarına sadece yetkili kişiler erişebilmelidir.  

---

### **4.21 PHP’de güvenli bir şekilde e-posta gönderimi nasıl yapılır?**  
✍ **Cevap:**  
- **PHPMailer Kullanımı:**  
  ```php
  use PHPMailer\PHPMailer\PHPMailer;
  $mail = new PHPMailer(true);
  $mail->isSMTP();
  $mail->Host = 'smtp.example.com';
  $mail->SMTPAuth = true;
  $mail->Username = 'user@example.com';
  $mail->Password = 'password';
  $mail->SMTPSecure = 'tls';
  $mail->Port = 587;
  $mail->setFrom('from@example.com', 'From Name');
  $mail->addAddress('to@example.com', 'To Name');
  $mail->Subject = 'Subject';
  $mail->Body = 'Email body';
  $mail->send();
  ```  

---

### **4.22 PHP'de 2FA (İki faktörlü kimlik doğrulama) nasıl implement edilir?**  
✍ **Cevap:**  
- **Google Authenticator veya TOTP:**  
  ```php
  use OTPHP\TOTP;
  $totp = TOTP::create();
  $secret = $totp->getSecret();
  $qrCode = $totp->getProvisioningUri();
  ```  

---

### **4.23 PHP projelerinde güvenli yazılım geliştirme yaşam döngüsü (SDLC) nasıl uygulanır?**  
✍ **Cevap:**  
- **Güvenlik Gereksinimleri:** Proje başlangıcında güvenlik gereksinimleri belirlenmelidir.  
- **Kod İncelemeleri:** Kod içinde güvenlik açıkları taranmalıdır.  
- **Penetration Testing:** Uygulama test edilerek açıklar tespit edilmelidir.  

---

### **4.24 PHP’de güvenlik güncellemeleri ve yamalar nasıl yönetilir?**  
✍ **Cevap:**  
- **Composer Update:** Bağımlılıklar düzenli olarak güncellenmelidir.  
- **PHP Sürüm Yükseltme:** Eski PHP sürümleri güvenlik açıkları içerebilir.  

---

### **4.25 PHP’de Veritabanı ve Uygulama Sunucusu arasındaki güvenli iletişim nasıl sağlanır?**  
✍ **Cevap:**  
- **SSL/TLS:** Veritabanı bağlantıları şifrelenmelidir.  
- **Güvenli Portlar:** Varsayılan portlar yerine güvenli portlar kullanılmalıdır.  

---

### **4.26 PHP projelerinde ağ güvenliği için hangi önlemler alınmalıdır?**  
✍ **Cevap:**  
- **Firewall:** Ağ trafiği kontrol edilmelidir.  
- **VPN:** Güvenli iletişim sağlanmalıdır.  
- **IDS/IPS:** Saldırı tespit ve önleme sistemleri kullanılmalıdır
