# 🛡️ SQL Injection Lab: Docker & DVWA

Bu proje, bir bilgisayar mühendisi adayı olarak web güvenliğinin temellerini anlamak, **SQL Injection (SQLi)** zafiyetini simüle etmek ve izole bir laboratuvar ortamında sızma testleri gerçekleştirmek amacıyla hazırlanmıştır.

---

## 📖 1. Bölüm: Teorik Temeller (SQL Injection Nedir?)

**SQL Injection**, saldırganın uygulamanın veri tabanı sorgularına müdahale etmesine olanak tanıyan bir zafiyet türüdür. Temel sorun, kullanıcıdan gelen verinin (input) "veri" olarak değil, "komut" olarak işlenmesidir.

### 🧠 Mantıksal Analiz
Yazılımcı, arka planda kullanıcı ID'sine göre arama yapan şu zayıf sorguyu hazırlar:

$$SELECT \text{ first\_name, last\_name } FROM \text{ users } WHERE \text{ user\_id } = \$id$$

Saldırgan, `$id` değişkeni yerine `%' OR '1'='1` yazdığında, SQL motoru sorguyu şu şekilde yorumlar:

$$SELECT \dots WHERE \text{ user\_id } = \% \text{ OR } 1=1$$



**Neden Başarılı Olur?**
* **Tautology (Totoloji):** `1=1` ifadesi her zaman **DOĞRU (True)** olduğu için, `WHERE` koşulu baypas edilir.
* **Veri Sızıntısı:** Filtreleme devre dışı kaldığı için veri tabanı tüm tabloyu saldırgana teslim eder.

---

## 🚀 2. Bölüm: Kurulum ve Uygulama Rehberi

Bu çalışma, **Docker** üzerinde koşan **DVWA (Damn Vulnerable Web Application)** platformu kullanılarak gerçekleştirilmiştir.

### 📦 Gereksinimler & Başlatma
Sistemi ayağa kaldırmak için terminalde şu komut kullanılır:
```bash
docker run --rm -it -p 80:80 vulnerables/web-dvwa

# 🔐 DVWA SQL Injection Lab Raporu

## ⚙️ Aşama 2: Sistem Konfigürasyonu

Uygulama ayağa kalktıktan sonra tarayıcı üzerinden aşağıdaki adımlar sırayla tamamlanır.

### 1. Sistem Erişimi ve Giriş

Tarayıcıdan `http://localhost` adresine gidilir. Karşınıza çıkan ekranda varsayılan kimlik bilgileriyle oturum açılır:

| Alan | Değer |
|------|-------|
| Username | `admin` |
| Password | `password` |

---

### 2. Veri Tabanı Yapılandırması (Initial Setup)

Sisteme ilk girişte veri tabanı tablolarının oluşturulması gerekir.

> **Setup DVWA** sayfasındaki **Create / Reset Database** butonuna tıklanarak gerekli tablolar ve örnek kullanıcılar veri tabanına enjekte edilir.

---

### 3. Güvenlik Seviyesinin Belirlenmesi

Zafiyetin en temel halini gözlemlemek için:

1. Sol menüdeki **DVWA Security** sekmesine gidin
2. Açılır menüden **"Low"** seçeneğini seçin
3. **Submit** butonuna basarak ayarı kaydedin

---

## ⚡ Aşama 3: Zafiyetin İstismarı (Exploitation)

Yapılandırma tamamlandıktan sonra **SQL Injection** sekmesine geçilerek saldırı simülasyonu gerçekleştirilmiştir.

| Parametre | Değer |
|-----------|-------|
| **Hedef** | `users` tablosundaki tüm verileri yetkisiz olarak çekmek |
| **Kullanılan Payload** | `` %' OR '1'='1 `` |

| Durum | Görsel Kanıt |
|-------|-------------|
| Saldırı Girişi | *(ekran görüntüsü eklenecek)* |
| Veri Sızıntısı | *(ekran görüntüsü eklenecek)* |

---

## 🔍 Sonuç ve Değerlendirme

Bu laboratuvar çalışması sonucunda:

- Girdi temizleme (**input validation**) yapılmayan sistemlerin basit mantıksal ifadelerle nasıl manipüle edilebileceği gözlemlenmiştir.
- Savunma mekanizması olarak **Prepared Statements** kullanımının önemi uygulamalı olarak kavranmıştır.

---

## 🎓 Hazırlayan

| Alan | Bilgi |
|------|-------|
| **Ad Soyad** | [Adınız Soyadınız] |
| **Üniversite** | [Üniversite Adı] — Bilgisayar Mühendisliği |
| **Öğrenci No** | [Numaranız]
