---
title: 'Linux Komutları Rehberi'
slug: 'linux-komutlari'
description: 'nmap kullanma'
pubDate: 'April 26 2026'
heroImage: '../../../assets/linux-komutlari.png'
category: "software"
---

# 🐧 

> Tüm temel Linux komutları, açıklamaları ve örnekleriyle birlikte.

---

## 📁 1. Dosya ve Dizin İşlemleri

### `ls` — Dizin içeriğini listele
```bash
ls              # Mevcut dizini listele
ls -l           # Ayrıntılı liste (izinler, boyut, tarih)
ls -a           # Gizli dosyaları da göster
ls -lh          # İnsan okunabilir dosya boyutları
ls -R           # Alt dizinleri de listele
ls /home/user   # Belirli dizini listele
```

### `cd` — Dizin değiştir
```bash
cd /var/log         # Belirli dizine git
cd ..               # Bir üst dizine çık
cd ~                # Ana dizine (home) git
cd -                # Önceki dizine geri dön
cd /                # Kök dizine git
```

### `pwd` — Mevcut dizini göster
```bash
pwd             # /home/eyup/projects gibi çıktı verir
```

### `mkdir` — Dizin oluştur
```bash
mkdir projeler              # Tek dizin oluştur
mkdir -p a/b/c              # İç içe dizinleri oluştur
mkdir -m 755 public_html    # İzinli dizin oluştur
```

### `rm` — Dosya/dizin sil
```bash
rm dosya.txt            # Dosya sil
rm -r dizin/            # Dizini ve içeriğini sil
rm -rf dizin/           # Zorla sil (uyarısız)
rm -i dosya.txt         # Silmeden önce sor
rm *.log                # Tüm .log dosyalarını sil
```

### `cp` — Dosya/dizin kopyala
```bash
cp kaynak.txt hedef.txt         # Dosya kopyala
cp -r dizin1/ dizin2/           # Dizini kopyala
cp -p dosya.txt yedek.txt       # İzin ve tarihi koru
cp -u *.txt /backup/            # Sadece yenileri kopyala
```

### `mv` — Dosya/dizin taşı veya yeniden adlandır
```bash
mv eski.txt yeni.txt            # Yeniden adlandır
mv dosya.txt /home/user/        # Taşı
mv *.jpg /resimler/             # Birden fazla dosya taşı
```

### `touch` — Boş dosya oluştur / tarihi güncelle
```bash
touch dosya.txt             # Boş dosya oluştur
touch dosya1.txt dosya2.txt # Birden fazla dosya oluştur
touch -t 202401011200 d.txt # Belirli tarih ata
```

### `ln` — Sembolik/sabit bağlantı oluştur
```bash
ln -s /var/www/html webroot     # Sembolik link oluştur
ln dosya.txt sabit_link.txt     # Sabit link oluştur
```

### `find` — Dosya ara
```bash
find / -name "nginx.conf"           # İsme göre ara
find . -name "*.js" -type f        # JS dosyalarını bul
find /var -size +100M              # 100MB'dan büyük dosyalar
find . -mtime -7                   # Son 7 günde değiştirilen
find . -perm 777                   # İzinlerine göre ara
find . -empty                      # Boş dosya/dizinler
```

### `locate` — Hızlı dosya ara
```bash
locate nginx.conf       # Veritabanından hızlı ara
updatedb                # Veritabanını güncelle
```

---

## 📄 2. Dosya İçerik İşlemleri

### `cat` — Dosya içeriğini göster
```bash
cat dosya.txt               # İçeriği ekrana yaz
cat -n dosya.txt            # Satır numarasıyla göster
cat dosya1.txt dosya2.txt   # Birleştirerek göster
cat > yeni.txt              # Klavyeden içerik yaz (Ctrl+D ile bitir)
cat >> mevcut.txt           # Dosyaya ekle
```

### `less` — Sayfalı görüntüle
```bash
less dosya.txt      # Sayfa sayfa oku (q ile çık)
less +F log.txt     # Canlı log takibi (tail -f gibi)
```

### `more` — İleriye doğru sayfalı görüntüle
```bash
more dosya.txt      # Boşluk: ileri, q: çık
```

### `head` — Dosyanın başını göster
```bash
head dosya.txt          # İlk 10 satır
head -n 20 dosya.txt    # İlk 20 satır
head -c 100 dosya.txt   # İlk 100 byte
```

### `tail` — Dosyanın sonunu göster
```bash
tail dosya.txt          # Son 10 satır
tail -n 50 dosya.txt    # Son 50 satır
tail -f /var/log/syslog # Canlı log takibi
tail -F app.log         # Dosya dönse bile takip et
```

### `grep` — Metin arama
```bash
grep "hata" log.txt             # Metin ara
grep -i "error" log.txt         # Büyük/küçük harf duyarsız
grep -r "TODO" /proje/          # Dizinde özyinelemeli ara
grep -n "main" kod.c            # Satır numarasıyla göster
grep -v "debug" log.txt         # Eşleşmeyenleri göster
grep -c "ERROR" log.txt         # Kaç satır eşleşiyor
grep -E "^[0-9]+" dosya.txt     # Regex ile ara
grep -l "hata" *.log            # Hangi dosyalarda var
```

### `sed` — Akış düzenleyici
```bash
sed 's/eski/yeni/' dosya.txt            # İlk eşleşmeyi değiştir
sed 's/eski/yeni/g' dosya.txt           # Tüm eşleşmeleri değiştir
sed -i 's/eski/yeni/g' dosya.txt        # Dosyayı yerinde düzenle
sed -n '5,10p' dosya.txt                # 5-10. satırları göster
sed '/yorum/d' dosya.txt                # Satır sil
sed 's/^/>> /' dosya.txt                # Her satıra önek ekle
```

### `awk` — Metin işleme dili
```bash
awk '{print $1}' dosya.txt              # İlk sütunu yazdır
awk -F: '{print $1}' /etc/passwd        # : ile böl, ilk alanı al
awk '{sum+=$1} END{print sum}' d.txt    # Toplam al
awk 'NR==5' dosya.txt                   # 5. satırı yazdır
awk '/hata/{print}' log.txt             # Hata içerenleri yazdır
```

### `sort` — Sırala
```bash
sort dosya.txt              # Alfabetik sırala
sort -r dosya.txt           # Ters sırala
sort -n sayilar.txt         # Sayısal sırala
sort -u dosya.txt           # Tekrarları kaldır
sort -k2 tablo.txt          # 2. sütuna göre sırala
```

### `uniq` — Tekrarlı satırları kaldır
```bash
uniq dosya.txt          # Ardışık tekrarları kaldır
uniq -c dosya.txt       # Kaç kez tekrarlandığını say
uniq -d dosya.txt       # Sadece tekrarlıları göster
```

### `wc` — Kelime/satır/karakter say
```bash
wc dosya.txt            # Satır, kelime, karakter
wc -l dosya.txt         # Sadece satır sayısı
wc -w dosya.txt         # Sadece kelime sayısı
wc -c dosya.txt         # Sadece byte sayısı
```

### `cut` — Sütun/alan kes
```bash
cut -d: -f1 /etc/passwd         # : ile böl, 1. alan
cut -c1-10 dosya.txt            # İlk 10 karakter
cut -d, -f2,4 veri.csv          # 2. ve 4. sütunlar
```

### `tr` — Karakter dönüştür/sil
```bash
tr 'a-z' 'A-Z' < dosya.txt     # Küçüğü büyüğe çevir
tr -d '\n' < dosya.txt          # Yeni satırları sil
tr -s ' ' < dosya.txt           # Birden fazla boşluğu teke indir
```

### `diff` — Dosyaları karşılaştır
```bash
diff dosya1.txt dosya2.txt      # Farkları göster
diff -u eski.txt yeni.txt       # Unified format (patch için)
diff -r dizin1/ dizin2/         # Dizinleri karşılaştır
```

---

## 🔐 3. İzin ve Sahiplik İşlemleri

### `chmod` — Dosya izinlerini değiştir
```bash
chmod 755 script.sh         # rwxr-xr-x
chmod 644 index.html        # rw-r--r--
chmod +x script.sh          # Çalıştırma izni ekle
chmod -w dosya.txt          # Yazma iznini kaldır
chmod u+x,g-w script.sh     # Kullanıcıya ekle, gruba kaldır
chmod -R 755 /var/www/      # Özyinelemeli izin
```

> **İzin rakamları:** r=4, w=2, x=1 | Kullanıcı/Grup/Diğer

### `chown` — Sahipliği değiştir
```bash
chown eyup dosya.txt            # Sahibi değiştir
chown eyup:www-data dosya.txt   # Sahip ve grup değiştir
chown -R nginx /var/www/html    # Özyinelemeli
chown :developers proje/        # Sadece grup değiştir
```

### `chgrp` — Grup değiştir
```bash
chgrp www-data /var/www/html
chgrp -R developers /proje/
```

### `umask` — Varsayılan izin maskesi
```bash
umask           # Mevcut maskeyi göster (örn: 022)
umask 027       # Yeni dosyalar için maske ayarla
```

---

## 🖥️ 4. Süreç Yönetimi

### `ps` — Çalışan süreçler
```bash
ps              # Mevcut shell süreçleri
ps aux          # Tüm süreçler (ayrıntılı)
ps -ef          # Tam format, tüm süreçler
ps aux | grep nginx     # Nginx süreçlerini bul
```

### `top` — Canlı süreç izleme
```bash
top             # Canlı izleme (q: çık, k: öldür, h: yardım)
top -u eyup     # Belirli kullanıcı süreçleri
```

### `htop` — Gelişmiş süreç izleme
```bash
htop            # Renkli ve etkileşimli (önce kurulum gerekebilir)
```

### `kill` — Süreci sonlandır
```bash
kill 1234               # PID ile sinyali gönder (varsayılan: SIGTERM)
kill -9 1234            # Zorla öldür (SIGKILL)
kill -15 1234           # Nazikçe bitir (SIGTERM)
kill -HUP 1234          # Yeniden başlat (SIGHUP)
```

### `killall` — İsme göre öldür
```bash
killall nginx           # Tüm nginx süreçlerini öldür
killall -9 firefox      # Zorla
```

### `pkill` — Örüntüyle öldür
```bash
pkill -f "python app.py"    # Komut satırına göre
pkill -u eyup               # Kullanıcıya göre
```

### `nice` / `renice` — Süreç önceliği
```bash
nice -n 10 ./agir_islem.sh      # Düşük öncelikle başlat (-20 en yüksek, 19 en düşük)
renice -n 5 -p 1234             # Mevcut süreç önceliğini değiştir
```

### `jobs` / `bg` / `fg` — Arka plan işleri
```bash
jobs                # Arka plan işleri listele
Ctrl+Z              # Süreci duraklat
bg                  # Arka plana gönder
fg                  # Ön plana getir
fg %2               # 2. işi ön plana getir
./script.sh &       # Arka planda başlat
```

### `nohup` — Oturum kapansa da çalış
```bash
nohup ./script.sh &             # Arka planda, çıktı nohup.out'a
nohup python app.py > app.log & # Çıktıyı dosyaya yönlendir
```

### `screen` / `tmux` — Terminal çoğullayıcı
```bash
screen              # Yeni oturum
screen -S isim      # İsimli oturum
screen -ls          # Oturumları listele
screen -r isim      # Oturuma bağlan
```

---

## 💾 5. Disk ve Depolama

### `df` — Disk kullanımı
```bash
df -h               # İnsan okunabilir
df -hT              # Dosya sistemi türüyle
df /home            # Belirli dizin
```

### `du` — Dizin boyutu
```bash
du -sh /var/log         # Özet, insan okunabilir
du -sh *                # Mevcut dizindeki her şey
du -h --max-depth=1     # Bir seviye derinlik
du -sh /home/* | sort -h # Sıralı
```

### `mount` / `umount` — Disk bağla/ayır
```bash
mount /dev/sdb1 /mnt/disk       # Diski bağla
mount -t ext4 /dev/sdb1 /mnt/   # Tür belirterek
mount | grep sdb                 # Bağlı diskleri listele
umount /mnt/disk                 # Diski ayır
```

### `lsblk` — Blok aygıtları listele
```bash
lsblk               # Disk ve bölümleri göster
lsblk -f            # Dosya sistemi bilgisiyle
```

### `fdisk` — Disk bölümleme
```bash
fdisk -l                # Tüm diskleri listele
fdisk /dev/sdb          # Diski bölümle (etkileşimli)
```

### `dd` — Ham veri kopyala
```bash
dd if=/dev/sda of=/dev/sdb bs=4M status=progress   # Disk kopyala
dd if=/dev/zero of=test.img bs=1M count=100         # Boş dosya oluştur
```

---

## 🌐 6. Ağ İşlemleri

### `ip` — Ağ arayüzleri
```bash
ip addr                     # IP adreslerini göster
ip addr show eth0           # Belirli arayüz
ip link set eth0 up/down    # Arayüzü aç/kapat
ip route                    # Yönlendirme tablosu
ip route add default via 192.168.1.1    # Varsayılan ağ geçidi
```

### `ping` — Bağlantı testi
```bash
ping google.com             # Sürekli ping
ping -c 4 8.8.8.8           # 4 kez ping at
ping -i 0.5 192.168.1.1     # 0.5 saniye aralık
```

### `curl` — HTTP/FTP istekleri
```bash
curl https://example.com                            # Sayfa içeriğini al
curl -o dosya.html https://example.com             # Dosyaya kaydet
curl -I https://example.com                        # Sadece header
curl -X POST -d '{"key":"val"}' -H "Content-Type: application/json" https://api.example.com
curl -u user:pass https://api.example.com          # Kimlik doğrulama
curl -L https://example.com                        # Yönlendirmeleri takip et
```

### `wget` — Dosya indir
```bash
wget https://example.com/dosya.zip          # İndir
wget -O yeni_isim.zip https://...           # İsim belirterek
wget -c https://...                          # Yarım kalan indirmeye devam et
wget -r https://example.com                 # Özyinelemeli indir
```

### `ssh` — Uzak bağlantı
```bash
ssh user@192.168.1.10               # Bağlan
ssh -p 2222 user@sunucu.com         # Port belirterek
ssh -i ~/.ssh/id_rsa user@sunucu    # Anahtar ile
ssh -L 8080:localhost:80 user@s     # Tünel (port yönlendirme)
```

### `scp` — Güvenli dosya kopyala
```bash
scp dosya.txt user@sunucu:/tmp/         # Uzağa kopyala
scp user@sunucu:/tmp/d.txt ./           # Uzaktan al
scp -r dizin/ user@sunucu:/backup/      # Dizin kopyala
scp -P 2222 dosya.txt user@sunucu:/tmp/ # Port belirterek
```

### `rsync` — Dosya senkronizasyonu
```bash
rsync -av kaynak/ hedef/                        # Yerel sync
rsync -avz /local/ user@sunucu:/remote/         # Uzak sync
rsync -avz --delete kaynak/ hedef/              # Silinen dosyaları da sil
rsync -avz --exclude='*.log' kaynak/ hedef/     # Hariç tut
```

### `netstat` / `ss` — Ağ bağlantıları
```bash
ss -tuln            # Dinleyen portlar
ss -tulnp           # Süreç bilgisiyle
netstat -tulnp      # Eski alternatif
ss -s               # Özet istatistikler
```

### `nmap` — Ağ tarama
```bash
nmap 192.168.1.1            # Host tara
nmap -p 80,443 192.168.1.1  # Belirli portlar
nmap -sV 192.168.1.0/24     # Ağı tara
```

### `dig` / `nslookup` — DNS sorgusu
```bash
dig google.com              # DNS sorgula
dig +short google.com       # Kısa çıktı
dig MX google.com           # MX kaydı
nslookup google.com         # Alternatif
```

### `hostname` — Sistem adı
```bash
hostname                    # Hostname göster
hostname -I                 # IP adreslerini göster
hostnamectl set-hostname yeni-isim  # Değiştir
```

---

## 👤 7. Kullanıcı ve Grup Yönetimi

### `useradd` / `adduser` — Kullanıcı ekle
```bash
useradd eyup                        # Kullanıcı ekle
useradd -m -s /bin/bash eyup        # Home ve shell ile
adduser eyup                        # Etkileşimli (Debian)
useradd -G sudo,www-data eyup       # Gruplara ekleyerek
```

### `userdel` — Kullanıcı sil
```bash
userdel eyup            # Kullanıcıyı sil
userdel -r eyup         # Home dizini de sil
```

### `usermod` — Kullanıcıyı değiştir
```bash
usermod -aG sudo eyup           # Gruba ekle
usermod -s /bin/zsh eyup        # Shell değiştir
usermod -l yeni_isim eski_isim  # Kullanıcı adı değiştir
usermod -L eyup                 # Hesabı kilitle
usermod -U eyup                 # Kilidi aç
```

### `passwd` — Parola değiştir
```bash
passwd                  # Kendi parolanı değiştir
passwd eyup             # Başka kullanıcı (root)
passwd -l eyup          # Hesabı kilitle
passwd -d eyup          # Parolayı sil
```

### `groups` / `id` — Grup bilgisi
```bash
groups                  # Hangi gruplarda olduğumu göster
groups eyup             # Belirli kullanıcı
id                      # UID, GID bilgisi
id eyup                 # Belirli kullanıcı
```

### `su` / `sudo` — Yetki yükseltme
```bash
su                      # Root ol
su - eyup               # Kullanıcı değiştir
sudo komut              # Root olarak çalıştır
sudo -u www-data komut  # Belirli kullanıcı olarak
sudo -i                 # Root shell aç
sudo !!                 # Son komutu sudo ile tekrar çalıştır
```

### `who` / `w` / `last` — Oturum bilgisi
```bash
who                     # Kim oturum açmış
w                       # Ayrıntılı oturum bilgisi
last                    # Oturum geçmişi
last eyup               # Belirli kullanıcı geçmişi
lastlog                 # Son giriş bilgileri
```

---

## 📦 8. Paket Yönetimi

### APT (Debian/Ubuntu)
```bash
apt update                          # Paket listesini güncelle
apt upgrade                         # Paketleri güncelle
apt install nginx                   # Paket kur
apt remove nginx                    # Paketi kaldır
apt purge nginx                     # Yapılandırmayla birlikte kaldır
apt autoremove                      # Gereksiz paketleri kaldır
apt search nginx                    # Paket ara
apt show nginx                      # Paket bilgisi
apt list --installed                # Kurulu paketler
dpkg -l                             # Tüm kurulu paketler
dpkg -i paket.deb                   # .deb dosyası kur
```

### YUM/DNF (RHEL/CentOS/Fedora)
```bash
dnf update                          # Sistemi güncelle
dnf install httpd                   # Paket kur
dnf remove httpd                    # Paketi kaldır
dnf search httpd                    # Ara
yum install nginx                   # Eski alternatif
rpm -ivh paket.rpm                  # .rpm dosyası kur
```

### Snap / Flatpak
```bash
snap install code --classic         # VS Code kur
snap list                           # Kurulu snaplar
flatpak install flathub com.spotify.Client
```

---

## ⚙️ 9. Sistem Yönetimi

### `systemctl` — Servis yönetimi (systemd)
```bash
systemctl start nginx               # Servisi başlat
systemctl stop nginx                # Servisi durdur
systemctl restart nginx             # Yeniden başlat
systemctl reload nginx              # Yapılandırmayı yeniden yükle
systemctl status nginx              # Durum göster
systemctl enable nginx              # Otomatik başlatmayı etkinleştir
systemctl disable nginx             # Devre dışı bırak
systemctl list-units --type=service # Tüm servisleri listele
systemctl daemon-reload             # systemd yapılandırmasını yenile
```

### `journalctl` — Sistem logları
```bash
journalctl -u nginx                 # Nginx logları
journalctl -f                       # Canlı log takibi
journalctl --since "1 hour ago"     # Son 1 saat
journalctl -b                       # Bu önyüklemeden itibaren
journalctl -p err                   # Sadece hatalar
journalctl --disk-usage             # Log disk kullanımı
```

### `cron` / `crontab` — Zamanlanmış görevler
```bash
crontab -e          # Cron görevlerini düzenle
crontab -l          # Mevcut görevleri listele
crontab -r          # Tüm görevleri sil

# Cron sözdizimi: dakika saat gün ay haftanın-günü komut
# Örnekler:
# * * * * * /script.sh              → Her dakika
# 0 * * * * /script.sh              → Her saat başı
# 0 3 * * * /backup.sh              → Her gece 03:00
# 0 3 * * 0 /weekly.sh              → Her Pazar 03:00
# */5 * * * * /monitor.sh           → Her 5 dakikada bir
# @reboot /script.sh                → Açılışta
```

### `uname` — Sistem bilgisi
```bash
uname -a            # Tüm sistem bilgisi
uname -r            # Kernel versiyonu
uname -m            # Mimari (x86_64 vs)
```

### `uptime` — Çalışma süresi
```bash
uptime              # Çalışma süresi ve yük
uptime -p           # Okunabilir format
```

### `date` — Tarih ve saat
```bash
date                        # Mevcut tarih/saat
date +"%Y-%m-%d"            # Özel format
date +"%d/%m/%Y %H:%M"      # Gün/Ay/Yıl Saat:Dakika
date -s "2024-01-01 12:00"  # Tarih ayarla (root)
timedatectl                 # Zaman dilimi yönetimi
timedatectl set-timezone Europe/Istanbul
```

### `shutdown` / `reboot` — Kapat/yeniden başlat
```bash
shutdown -h now         # Hemen kapat
shutdown -h +10         # 10 dakika sonra kapat
shutdown -r now         # Hemen yeniden başlat
shutdown -c             # Zamanlanmış kapatmayı iptal et
reboot                  # Yeniden başlat
halt                    # Durdur
```

### `dmesg` — Kernel mesajları
```bash
dmesg               # Kernel ring buffer
dmesg | tail -20    # Son 20 mesaj
dmesg | grep error  # Hataları filtrele
dmesg -T            # Zaman damgasıyla
```

---

## 🗜️ 10. Arşiv ve Sıkıştırma

### `tar` — Arşiv oluştur/aç
```bash
tar -czvf arsiv.tar.gz dizin/       # Gzip ile sıkıştır
tar -cjvf arsiv.tar.bz2 dizin/      # Bzip2 ile sıkıştır
tar -xzvf arsiv.tar.gz              # Aç
tar -xzvf arsiv.tar.gz -C /hedef/   # Belirli yere aç
tar -tzvf arsiv.tar.gz              # İçeriği listele
tar -czvf - dizin/ | ssh user@s "cat > /backup/arsiv.tar.gz"  # SSH üzerinden
```

> **Seçenekler:** c=oluştur, x=aç, t=listele, z=gzip, j=bzip2, v=ayrıntılı, f=dosya

### `gzip` / `gunzip` — Gzip
```bash
gzip dosya.txt          # Sıkıştır → dosya.txt.gz
gunzip dosya.txt.gz     # Aç
gzip -d dosya.txt.gz    # Alternatif açma
gzip -l dosya.txt.gz    # Sıkıştırma oranı
```

### `zip` / `unzip` — ZIP
```bash
zip arsiv.zip dosya1.txt dosya2.txt     # Zip oluştur
zip -r arsiv.zip dizin/                 # Dizini zip'le
unzip arsiv.zip                         # Aç
unzip arsiv.zip -d /hedef/              # Belirli yere aç
unzip -l arsiv.zip                      # İçeriği listele
```

---

## 🔗 11. Yönlendirme ve Borular

### Yönlendirme operatörleri
```bash
komut > dosya.txt           # Çıktıyı dosyaya yaz (üzerine yaz)
komut >> dosya.txt          # Çıktıyı dosyaya ekle
komut < dosya.txt           # Dosyayı girdi olarak kullan
komut 2> hata.txt           # Hata çıktısını dosyaya yaz
komut 2>&1                  # Hataları standart çıktıya yönlendir
komut > /dev/null 2>&1      # Tüm çıktıyı gizle
komut &> dosya.txt          # Her şeyi dosyaya yaz
```

### Boru (pipe) `|`
```bash
ps aux | grep nginx                         # Filtreleme
cat log.txt | grep ERROR | wc -l            # Zincirleme
ls -lh | sort -k5 -h                        # Boyuta göre sırala
history | grep ssh | tail -10               # Son SSH komutları
cat /etc/passwd | cut -d: -f1 | sort        # Kullanıcıları sırala
```

### `xargs` — Argüman listesi oluştur
```bash
find . -name "*.log" | xargs rm             # Bulunan dosyaları sil
echo "a b c" | xargs mkdir                  # Dizin oluştur
find . -name "*.txt" | xargs grep "hata"    # İçinde ara
cat urls.txt | xargs wget                   # Toplu indirme
```

### `tee` — Hem ekrana hem dosyaya yaz
```bash
komut | tee cikti.txt               # Ekrana ve dosyaya yaz
komut | tee -a cikti.txt            # Dosyaya ekle
```

---

## 🔍 12. Arama ve Metin Araçları

### `which` / `whereis` / `type` — Komut konumu
```bash
which python3           # Komutun tam yolu
whereis nginx           # Binary, kaynak, man sayfası
type ls                 # Komut türü (alias, built-in, etc.)
```

### `history` — Komut geçmişi
```bash
history                 # Tüm geçmiş
history 20              # Son 20 komut
history | grep apt      # Filtreleme
!450                    # 450. komutu tekrar çalıştır
!!                      # Son komutu tekrar çalıştır
!apt                    # apt ile başlayan son komutu çalıştır
Ctrl+R                  # Geçmişte geriye arama
```

### `alias` — Kısayol tanımla
```bash
alias ll='ls -alh'                      # Kısayol oluştur
alias grep='grep --color=auto'          # Renkli grep
alias update='sudo apt update && sudo apt upgrade'
alias ..='cd ..'
unalias ll                              # Kısayolu sil
alias                                   # Tüm kısayolları listele
```

### `man` / `info` / `--help` — Yardım
```bash
man ls              # ls kılavuz sayfası
man -k "copy file"  # Anahtar kelimeyle ara
info bash           # Daha ayrıntılı bilgi
ls --help           # Kısa yardım
tldr ls             # Basitleştirilmiş örnekler (tldr kurulu ise)
```

---

## 📊 13. Sistem İzleme

### `free` — Bellek kullanımı
```bash
free -h             # İnsan okunabilir
free -s 2           # Her 2 saniyede güncelle
```

### `vmstat` — Sanal bellek istatistikleri
```bash
vmstat              # Anlık
vmstat 2 5          # 2 saniyede bir, 5 kez
```

### `iostat` — Disk I/O istatistikleri
```bash
iostat              # Disk istatistikleri
iostat -x 2         # Ayrıntılı, 2 saniyede bir
```

### `sar` — Sistem aktivite raporu
```bash
sar -u 1 5          # CPU kullanımı, 5 kez
sar -r 1 5          # Bellek kullanımı
```

### `lsof` — Açık dosyalar
```bash
lsof                        # Tüm açık dosyalar
lsof -p 1234                # PID'e göre
lsof -u eyup                # Kullanıcıya göre
lsof -i :80                 # Port 80'i kullananlar
lsof /var/log/syslog        # Dosyayı açan süreçler
```

### `strace` — Sistem çağrısı izle
```bash
strace ls               # ls komutunun sistem çağrıları
strace -p 1234          # Mevcut süreci izle
strace -e open ls       # Sadece open çağrıları
```

---

## 🔒 14. Güvenlik

### `iptables` / `ufw` — Güvenlik duvarı
```bash
ufw status              # Durum göster
ufw enable/disable      # Etkinleştir/devre dışı bırak
ufw allow 80            # Port 80'e izin ver
ufw allow 22/tcp        # SSH izni
ufw deny 23             # Telnet engelle
ufw allow from 192.168.1.0/24   # IP aralığından izin
ufw delete allow 80     # Kuralı sil
```

### `ssh-keygen` — SSH anahtar çifti oluştur
```bash
ssh-keygen -t rsa -b 4096 -C "email@example.com"    # RSA 4096-bit
ssh-keygen -t ed25519 -C "email@example.com"        # Modern algoritma
ssh-copy-id user@sunucu                              # Anahtarı sunucuya kopyala
```

### `openssl` — Şifreleme araçları
```bash
openssl rand -hex 32                # Rastgele string
openssl passwd -6 sifre             # SHA-512 hash
openssl req -newkey rsa:2048 -nodes -keyout key.pem -x509 -days 365 -out cert.pem  # Self-signed SSL
openssl s_client -connect example.com:443   # SSL bağlantı testi
```

### `gpg` — GNU Privacy Guard
```bash
gpg --gen-key                       # Anahtar oluştur
gpg --encrypt -r user@example.com dosya.txt    # Şifrele
gpg --decrypt dosya.txt.gpg         # Şifre çöz
gpg --sign dosya.txt                # İmzala
```

---

## 🛠️ 15. Genel Araçlar

### `echo` — Metin yazdır
```bash
echo "Merhaba Dünya"            # Metin yazdır
echo -n "Satır sonu yok"        # Satır sonu olmadan
echo -e "Satır1\nSatır2"        # Escape karakterleri
echo $HOME                       # Değişken değeri
echo "test" >> dosya.txt         # Dosyaya ekle
```

### `printf` — Biçimlendirilmiş çıktı
```bash
printf "Merhaba %s\n" "Dünya"
printf "Sayı: %d\n" 42
printf "%-10s %5d\n" "isim" 100  # Sola hizalı, sağa hizalı
```

### `read` — Girdi oku
```bash
read isim                       # Değişkene oku
read -p "Adınız: " isim         # İstemli
read -s -p "Şifre: " sifre      # Gizli (parola için)
read -t 5 cevap                 # 5 saniye timeout
```

### `export` — Ortam değişkeni
```bash
export PATH=$PATH:/yeni/yol     # PATH'e ekle
export EDITOR=vim               # Varsayılan editör
export NODE_ENV=production      # Ortam değişkeni
printenv                        # Tüm değişkenler
printenv PATH                   # Belirli değişken
env                             # Ortam değişkenleri
```

### `source` / `.` — Script çalıştır (mevcut shell'de)
```bash
source ~/.bashrc        # Bash yapılandırmasını yenile
. ~/.profile            # Kısayol form
source env.sh           # Ortam değişkenlerini yükle
```

### `exec` — Süreci değiştir
```bash
exec bash               # Mevcut shell'i değiştir
exec > cikti.txt        # Shell çıktısını dosyaya yönlendir
```

### `time` — Komut süresini ölç
```bash
time ls -R /usr         # Çalışma süresini ölç
time ./script.sh
```

### `watch` — Komutu tekrar et
```bash
watch -n 2 'df -h'      # Her 2 saniyede disk kullanımı
watch -n 1 'ps aux | grep nginx'    # Süreç izle
watch -d 'ls -l'        # Değişiklikleri vurgula
```

### `at` — Tek seferlik zamanlama
```bash
at 15:30                # 15:30'da çalıştır (komutları gir, Ctrl+D ile bitir)
at now + 1 hour         # 1 saat sonra
atq                     # Bekleyen görevler
atrm 3                  # 3. görevi iptal et
```

---

## 🧮 16. Hesaplama ve Metin İşleme

### `bc` — Hesap makinesi
```bash
echo "5 * 3.14" | bc -l         # Ondalıklı hesap
echo "sqrt(144)" | bc -l        # Karekök
echo "obase=2; 255" | bc        # Binary'e çevir
```

### `expr` — İfade hesapla
```bash
expr 5 + 3          # 8
expr 10 \* 4        # 40
expr length "Merhaba"   # 7
```

### `base64` — Kodlama
```bash
echo "Merhaba" | base64          # Kodla
echo "TWVyaGFiYQ==" | base64 -d  # Çöz
base64 dosya.txt > kodlanmis.b64
```

### `md5sum` / `sha256sum` — Hash kontrolü
```bash
md5sum dosya.txt                # MD5 hash
sha256sum dosya.txt             # SHA-256 hash
sha256sum -c kontrol.txt        # Hash doğrula
```

---

## 🎨 17. Shell Özellikleri

### Değişkenler
```bash
isim="Eyup"                 # Değişken tanımla
echo $isim                  # Kullan
echo ${isim}                # Süslü parantezli kullanım
unset isim                  # Değişkeni sil
readonly SABIT=42           # Salt okunur değişken
```

### Koşul ifadeleri
```bash
if [ -f dosya.txt ]; then
    echo "Dosya var"
elif [ -d dizin ]; then
    echo "Dizin var"
else
    echo "Hiçbiri yok"
fi

# Test operatörleri
[ -f dosya ]    # Dosya var mı?
[ -d dizin ]    # Dizin var mı?
[ -x script ]   # Çalıştırılabilir mi?
[ -z "$str" ]   # String boş mu?
[ "$a" = "$b" ] # String eşit mi?
[ $n -gt 5 ]    # Sayı büyüklüğü
```

### Döngüler
```bash
# For döngüsü
for i in 1 2 3 4 5; do
    echo "Sayı: $i"
done

for dosya in *.txt; do
    echo "İşleniyor: $dosya"
done

# While döngüsü
while [ $i -lt 10 ]; do
    echo $i
    ((i++))
done

# Until döngüsü
until [ $i -ge 10 ]; do
    echo $i
    ((i++))
done
```

### Fonksiyonlar
```bash
selamla() {
    echo "Merhaba, $1!"
}
selamla "Eyup"      # Merhaba, Eyup!

# Değer döndür
topla() {
    return $(( $1 + $2 ))
}
topla 3 7
echo "Sonuç: $?"
```

---

## 📋 Hızlı Referans Tablosu

| Kategori | Komut | Açıklama |
|----------|-------|----------|
| Dosya | `ls`, `cd`, `pwd`, `mkdir`, `rm`, `cp`, `mv` | Temel dosya işlemleri |
| İçerik | `cat`, `less`, `grep`, `sed`, `awk` | Metin görüntüleme/işleme |
| İzin | `chmod`, `chown`, `sudo` | Yetki yönetimi |
| Süreç | `ps`, `top`, `kill`, `systemctl` | Süreç yönetimi |
| Disk | `df`, `du`, `mount`, `lsblk` | Disk işlemleri |
| Ağ | `ip`, `ping`, `curl`, `ssh`, `netstat` | Ağ araçları |
| Arşiv | `tar`, `gzip`, `zip` | Sıkıştırma |
| Sistem | `uname`, `date`, `uptime`, `journalctl` | Sistem bilgisi |
| Paket | `apt`, `dnf`, `snap` | Paket yönetimi |
| Güvenlik | `ufw`, `ssh-keygen`, `openssl` | Güvenlik araçları |

---

> 💡 **İpucu:** Herhangi bir komut hakkında daha fazla bilgi için `man <komut>` veya `<komut> --help` kullanın.

> ⚠️ **Uyarı:** `rm -rf`, `dd`, `chmod 777` gibi güçlü komutları dikkatli kullanın!
