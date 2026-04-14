# SQL Injection Lab: Docker & DVWA

Bu proje, web uygulamalarındaki en kritik zafiyetlerden biri olan **SQL Injection (SQLi)** konusunu anlamak ve pratik yapmak amacıyla oluşturulmuş bir laboratuvar çalışmasıdır.

## 1. SQL Injection Nedir? (Teorik Bakış)

SQL Injection, bir saldırganın web uygulamasının veri tabanı sorgularına kötü niyetli SQL kodları enjekte etmesiyle oluşan bir zafiyettir. Temelde, kullanıcıdan gelen girdilerin (input) yeterince temizlenmemesi ve "veri" yerine "komut" olarak algılanması sonucu ortaya çıkar.

**Neden Oluşur?**
Yazılımcının kullanıcı girdilerini doğrudan SQL sorgusunun içine yerleştirmesi (String Concatenation) bu açığa davetiye çıkarır. Örneğin:
`SELECT * FROM users WHERE id = '` + **user_input** + `'`

**Mantık:**
Saldırgan, `' OR '1'='1` gibi bir girdi kullanarak sorgunun mantıksal akışını değiştirir ve veri tabanını tüm kayıtları dökmeye zorlar.

---

## 2. Kurulum ve Çalıştırma (Setup Guide)

Bu laboratuvar, **Docker** kullanılarak izole bir konteyner içerisinde **DVWA (Damn Vulnerable Web Application)** platformu üzerinde koşturulmaktadır.

### Gereksinimler
* Docker Desktop (Kurulu ve çalışır durumda olmalı)

### Adım Adım Kurulum

1.  **Laboratuvarı Başlatın:**
    Terminali açın ve aşağıdaki komutu çalıştırarak zafiyetli konteyner imajını indirin ve ayağa kaldırın:
    ```bash
    docker run --rm -it -p 80:80 vulnerables/web-dvwa
    ```

2.  **Erişim Sağlayın:**
    Tarayıcınızdan `http://localhost` adresine gidin.
    * **Username:** `admin`
    * **Password:** `password`

3.  **Veri Tabanı Yapılandırması:**
    Giriş yaptıktan sonra sayfanın altındaki **"Create / Reset Database"** butonuna tıklayarak tabloların oluşturulmasını sağlayın.

4.  **Güvenlik Seviyesini Ayarlayın:**
    Sol menüden **"DVWA Security"** sekmesine gidin ve başlangıç için seviyeyi **"Low"** olarak işaretleyin.

---

### Katkıda Bulunanlar
* **Elif Perincek** - *Konya Teknik Üniversitesi Bilgisayar Mühendisliği Öğrencisi*
