---
title: 'Git Nedir, Ne İşe Yarar ve Nasıl Kullanılır?'
slug: 'git-nedir'
description: 'git rehberi'
pubDate: 'April 19 2026'
heroImage: '../../../assets/git.png'
category: "software"
---


Yazılım dünyasına adım atan herkesin karşısına çıkan ilk kavramlardan biri **Git**'tir. İster kişisel bir web projesi geliştiriyor olun, ister devasa bir sunucu altyapısını yönetiyor olun, Git olmadan modern bir yazılım süreci düşünmek neredeyse imkânsızdır.

Bu rehberde Git'in ne olduğunu, neden kullanıldığını ve günlük iş akışınızda nasıl uygulayacağınızı adım adım, gerçek dünya örnekleriyle inceleyeceğiz.

---

### 1. Git Nedir?

Git, 2005 yılında Linux çekirdeğinin yaratıcısı **Linus Torvalds** tarafından geliştirilmiş, ücretsiz ve açık kaynaklı bir **Dağıtık Versiyon Kontrol Sistemi**'dir (Distributed Version Control System — DVCS).

En basit tabirle Git, projenizdeki dosyaların (kodlar, yapılandırma dosyaları, metinler) zaman içindeki değişimini adım adım kaydeden bir **"zaman makinesidir"**. Projenizi geliştirirken yaptığınız her önemli değişikliğin bir fotoğrafını (snapshot) çeker.

### Git ve GitHub/GitLab Aynı Şey mi?

**Hayır.** Git, bilgisayarınızda (veya sunucunuzda) çalışan yerel bir araçtır. **GitHub**, **GitLab** veya **Bitbucket** ise Git altyapısını kullanan; projelerinizi internet üzerinde depolamanızı, paylaşmanızı ve diğer geliştiricilerle senkronize çalışmanızı sağlayan bulut tabanlı servislerdir.

---

### 2. Git Ne İşe Yarar? (Neden Kullanmalıyız?)

Bir projeyi Git olmadan yönetmek, klasörleri `proje_son`, `proje_en_son`, `proje_kesin_bitti_v2` şeklinde isimlendirmeye benzer. Bu hem kaotik hem de risklidir. Git'in sağladığı başlıca avantajlar şunlardır:

- **Zaman Yolculuğu (Geri Alma):** Yanlışlıkla çalışan bir kodu mu bozdunuz? Git sayesinde projenizin bir saat, bir gün veya bir ay önceki stabil haline saniyeler içinde geri dönebilirsiniz.
- **Güvenli Deney Ortamı (Branching — Dallanma):** Ana projenizi bozmadan yeni özellikler denemek için ayrı bir "dal" (branch) açabilirsiniz. Deneme başarısız olursa dalı siler geçersiniz; başarılı olursa ana projeyle birleştirirsiniz (merge).
- **Ekip Çalışması:** Birden fazla kişinin aynı dosya üzerinde, birbirinin kodunu ezmeden eşzamanlı çalışmasına olanak tanır.
- **Ne, Neden, Ne Zaman Değişti? (Log):** Hangi satır kodun, kim tarafından ve hangi amaçla değiştirildiğini geçmişe dönük olarak görebilirsiniz.

---

### 3. Git'in Temel İş Akışı (3 Aşamalı Mimari)

Git'i anlamanın yolu, dosyaların geçtiği 3 temel durumu kavramaktan geçer:

1. **Working Directory (Çalışma Dizini):** Dosyalarınızın o an bilgisayarınızda bulunduğu, değişiklik yaptığınız yerdir. Dosya burada `Modified` (Değiştirilmiş) durumdadır.
2. **Staging Area (Hazırlık Alanı):** Yaptığınız değişiklikleri kalıcı olarak kaydetmeden önce "evet, bu değişiklikleri paketlemeye hazırım" dediğiniz bekleme odasıdır. Dosya `Staged` durumundadır.
3. **.git Directory (Repository — Depo):** Değişikliklerin güvenli bir şekilde veritabanına kaydedildiği yerdir. Dosya artık `Committed` (İşlenmiş/Kaydedilmiş) durumundadır.

---

### 4. Adım Adım Git Kullanımı

Öncelikle Git'in sisteminizde kurulu olduğundan emin olun. Linux tabanlı bir sistem (Debian/Ubuntu/Kali) kullanıyorsanız terminale şunu yazın:

```bash
sudo apt install git
```

### A. İlk Ayarlar (Configuration)

Git'i kurduktan sonra ona kim olduğunuzu söylemeniz gerekir; böylece yaptığınız commit'ler sizin imzanızı taşır.

```bash
git config --global user.name "Adınız Soyadınız"
git config --global user.email "eposta@adresiniz.com"
```

### B. Yeni Bir Proje Başlatmak

Yeni bir proje klasörü oluşturup Git'i başlatın:

```bash
cd benim-projem
git init
```

Bu komut, klasörün içine gizli bir `.git` dizini oluşturur ve burayı bir Git deposu (repository) haline getirir.

### C. Dosyaların Durumunu Kontrol Etmek (Status)

Hangi dosyaların değiştiğini, hangilerin staged olduğunu görmek için:

```bash
git status
```

### D. Dosyaları Takibe Almak (Add)

Değişen dosyaları Staging Area'ya almak için:

```bash
# Sadece belirli bir dosyayı eklemek:
git add index.html

# Tüm değişen dosyaları eklemek (en sık kullanılan):
git add .
```

### E. Değişiklikleri Kaydetmek (Commit)

Staging Area'daki dosyaları açıklayıcı bir mesajla projenin tarihçesine kalıcı olarak kaydederiz:

```bash
git commit -m "feat: Astro blog için başlangıç şablonu oluşturuldu"
```

> **İpucu:** Commit mesajları kısa, net ve ne yapıldığını anlatan cümleler olmalıdır. `feat:`, `fix:`, `docs:` gibi ön ekler kullanmak iyi bir alışkanlıktır.

### F. Geçmişi Görüntülemek (Log)

Projenizde bugüne kadar yapılmış commit kayıtlarını görmek için:

```bash
git log

# Daha temiz, tek satırlık görünüm:
git log --oneline
```

### G. Dallanma (Branching)

Diyelim ki blog projenize **Sanity CMS** entegre edeceksiniz. Bunu doğrudan `main` dalı üzerinde yapmak risklidir. Yeni bir dal oluşturun:

```bash
# Yeni dal oluştur ve o dala geç:
git checkout -b feature/sanity-entegrasyonu

# Mevcut dalları listele:
git branch
```

İşiniz bittiğinde, geliştirdiğiniz dalı ana dala birleştirin:

```bash
# Ana dala geri dön:
git checkout main

# Dalı birleştir (merge):
git merge feature/sanity-entegrasyonu

# Artık gerek kalmayan dalı sil:
git branch -d feature/sanity-entegrasyonu
```

### H. Uzak Sunucu ile Çalışmak (Remote / Push / Pull)

Kodlarınızı GitHub'a veya bir VPS üzerindeki uzak bir depoya göndermek için:

```bash
# Uzak depo ekle:
git remote add origin https://github.com/kullanici-adiniz/benim-projem.git

# Kodları uzak depoya gönder:
git push -u origin main

# Uzak depodaki güncel kodları bilgisayara çek:
git pull origin main
```

---

### 5. Sık Karşılaşılan Senaryolar

| Durum | Komut |
|---|---|
| Commit etmeden dosyayı eski haline döndür | `git restore dosya_adi.js` |
| Staging alanından dosyayı çıkar | `git restore --staged yanlis_dosya.js` |
| Son commit mesajını düzelt | `git commit --amend -m "yeni mesaj"` |
| Belirli bir commit'e geri dön (geçici) | `git checkout <commit-hash>` |
| Uzak depodaki branch listesini gör | `git branch -r` |

---

### 6. Günlük İş Akışı (Kopya Kağıdı)

```bash
# 1. Kodlarınızı yazın / değiştirin, ardından:
git status                        # Neyin değiştiğini gör
git add .                         # Değişiklikleri pakete ekle
git commit -m "anlamlı bir mesaj" # Paketi kaydet
git push origin main              # Buluta / sunucuya gönder
```

Bu döngüyü her anlamlı değişiklik sonrasında tekrarlamak, projenizi her zaman güvende tutar ve geçmişe dönük izlenebilirlik sağlar.

### Örnek
```bash
# 1. Aşama: Yerel Bilgisayar (Değişiklikleri Paketleme ve Gönderme) Bilgisayarında (Windows) dosyaları düzenledikten sonra bu değişiklikleri GitHub'a göndermen gerekir.
1 git add .  # Yaptığın tüm değişiklikleri "takibe alır" ve paketlenmeye hazır hale getirir.
2 git commit -m "açıklama" # Değişikliklere bir isim verir (Örn: "Yeni yazı eklendi"). Kayıt noktası oluşturur.
3 git push origin main # Yereldeki tüm bu değişiklikleri internetteki (GitHub) kasanıza yükler.
#2. Aşama: VPS Sunucusu (Kodları Çekme ve Yayına Alma)Kodlar artık GitHub'da ama siten hâlâ eski dosyaları gösteriyor. Sunucuya girip onları güncellemen gerekir.
1 cd /var/www/blogwebsite # VPS içinde projenin olduğu klasöre giriş yapar (Yolu doğru yazdığından emin ol).
2 git pull # GitHub'a gönderdiğin en yeni kodları sunucuya indirir.
3 npm run build # En önemli adım. İnen yeni kodları/yazıları işleyip Nginx'in okuduğu dist klasörünü günceller.
```