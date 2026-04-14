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
