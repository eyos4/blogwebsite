---
title: 'Nmap Nedir Nasıl Kullanılır'
slug: 'nmap-nedir'
description: 'nmap kullanma'
pubDate: 'April 02 2026'
heroImage: '../../../assets/nmap.png'
category: "software"
---

# Nmap (Network Mapper) Rehberi

Nmap, ağ uzmanlarının, sistem yöneticilerinin ve güvenlik araştırmacılarının vazgeçilmez "isviçre çakısı"dır. Ağ keşfi ve güvenlik denetimi için kullanılan açık kaynaklı bir araçtır.

---

## 1. Nmap Ne İşe Yarar?

Nmap kullanarak bir ağ veya sistem hakkında şu bilgilere ulaşabilirsiniz:

* **Host Keşfi:** Ağda hangi cihazlar (bilgisayar, telefon, sunucu) aktif?
* **Port Tarama:** Hedef cihazda hangi kapılar (portlar) açık? (Örn: HTTP için 80, SSH için 22).
* **Servis Tespiti:** Açık olan portlarda hangi uygulama ve versiyonu çalışıyor? (Örn: Apache 2.4.41).
* **İşletim Sistemi Analizi:** Hedef cihaz Windows mu, Linux mu yoksa bir IoT cihazı mı?
* **Güvenlik Zafiyeti Taraması:** NSE (Nmap Scripting Engine) kullanarak sistemdeki açıklar tespit edilebilir.

---

## 2. Nmap Nasıl Çalışır?

Nmap, hedef sisteme özel olarak yapılandırılmış **IP paketleri** gönderir ve bu paketlere gelen yanıtları (veya yanıtsızlığı) analiz eder. Gönderilen paketlerin türüne göre (TCP SYN, UDP, ICMP vb.) hedefin durumu hakkında çıkarımlar yapar.

---

## 3. Yaygın Kullanım Tablosu (Parametreler)

Nmap'in gücü kullandığınız parametrelerden gelir. İşte en sık kullanılanlar:

| Parametre | Açıklama |
| :--- | :--- |
| `-sn` | Port taraması yapma, sadece cihazın açık olup olmadığına bak (Ping Scan). |
| `-p [port]` | Belirli bir portu veya aralığı tara. Örn: `-p 80,443` veya `-p 1-1000` |
| `-p-` | Tüm portları (1 ile 65535 arası) tara. |
| `-sV` | Açık portlarda çalışan servislerin versiyon bilgilerini tespit et. |
| `-O` | Hedef sistemin işletim sistemini (OS) tahmin et. |
| `-sS` | TCP SYN taraması (Yarı açık tarama, daha hızlı ve gizli). |
| `-A` | Agresif tarama: OS tespiti, versiyon tespiti, script tarama ve traceroute. |
| `-T[0-5]` | Tarama hızını ayarlar. 0 en yavaş (gizli), 5 en hızlı (gürültülü). |
| `-oN [dosya]` | Tarama sonuçlarını standart metin formatında dosyaya kaydet. |

---

# Nmap Uygulamalı Komut Örnekleri ve Analizi

### A. Tek Bir Hedefi Taramak
Hedef IP veya alan adındaki en yaygın 1000 portu tarar.

```bash
nmap 192.168.1.1
```

B. Belirli Port Aralığını ve Servis Versiyonlarını Taramak
Sadece 80, 443 ve 22 portlarını tarar ve hangi yazılımların çalıştığını söyler.

```bash
nmap -p 80,443,22 -sV 192.168.1.50

```
C. Tüm Ağı Taramak (Host Discovery)
Belirtilen IP aralığındaki (subnet) hangi cihazların aktif ("ayakta") olduğunu bulur.

```bash
nmap -sn 192.168.1.0/24
```

D. Agresif ve Hızlı Güvenlik Analizi
İşletim sistemi tespiti, servis bilgilerini ve traceroute işlemlerini hızlı bir modda (T4) analiz eder.

```bash
nmap -A -T4 scanme.nmap.org
```

E. Script Engine (NSE) ile Zafiyet Taraması
Hedef sistemde bilinen yaygın güvenlik açıklarını (vulnerability) otomatik olarak kontrol eder.

```bash
nmap --script vuln 192.168.1.100
```

5. Örnek Senaryo Analizi
Diyelim ki bir sistem yöneticisisiniz ve şirketinizdeki bir web sunucusunun dışarıya sızdırdığı bilgileri veya açık portlarını kontrol etmek istiyorsunuz:

Kullanılan Komut:

```bash 
nmap -sV -O -p 1-1000 10.0.0.15
```

Olası Çıktı Analizi ve Yorumlama:

Port 80/tcp open http: Sunucuda bir web sitesinin aktif olarak yayında olduğunu gösterir. Portun "open" olması erişilebilir olduğu anlamına gelir.

Version: Apache httpd 2.4.41: Web sunucusunun kullandığı yazılımın tam sürüm bilgisini verir. Eğer bu sürümün bilinen kritik bir açığı (CVE) varsa, sistemin acilen güncellenmesi gerektiğini bu sayede anlarsınız.

OS details: Linux 5.x: Hedef makinenin işletim sistemi çekirdek (kernel) sürümüne bakarak bir Linux cihazı olduğu teyit edilir. Bu bilgi, saldırganların veya yöneticilerin hangi exploit türlerinin çalışabileceğini anlamasını sağlar.

Not: Tarama sonuçlarını daha sonra incelemek üzere bir dosyaya kaydetmek isterseniz komutun sonuna -oN dosya_adi.txt parametresini ekleyebilirsiniz.