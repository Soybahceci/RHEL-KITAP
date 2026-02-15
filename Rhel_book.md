# Table of Contents {#table-of-contents .TOC-Heading}

# 🐧 RHEL (Red Hat Enterprise Linux) --- Sıfırdan İleri Seviyeye Kapsamlı Öğrenim Kitabı

**Yazar:** AI Asistan\
**Tarih:** Şubat 2026\
**Hedef Kitle:** Linux'a yeni başlayanlardan, profesyonel sunucu
yöneticiliğine geçmek isteyenlere\
**Kapsam:** RHEL 8 / RHEL 9

------------------------------------------------------------------------

## Önsöz

Bu kitap, Red Hat Enterprise Linux (RHEL) işletim sistemini sıfırdan
öğrenmek ve profesyonel bir sistem yöneticisi seviyesine ulaşmak
isteyenler için hazırlanmıştır. Kitap boyunca sadece "ne yapılır" değil,
**"neden yapılır", "nasıl çalışır", "sorun çıkarsa ne yapılır"**
sorularına da cevap verilmektedir.

Her bölüm: - **Teorik bilgi** ile başlar - **Pratik komutlar ve
örnekler** ile devam eder - **Sık karşılaşılan sorunlar ve çözümleri**
ile biter - **Gerçek dünya senaryoları** ile pekiştirilir

Bu kitabı bitirdiğinizde, bir RHEL sunucusunu kurabilecek,
yapılandırabilecek, yönetebilecek, güvenliğini sağlayabilecek ve
sorunlarını çözebilecek seviyeye geleceksiniz.

------------------------------------------------------------------------

## İçindekiler

### BÖLÜM I --- TEMELLer (Sıfırdan Başlangıç)

1.  **Linux ve RHEL Nedir?** --- İşletim sistemi kavramları, Linux
    tarihi, dağıtımlar, RHEL'in yeri
2.  **RHEL Kurulumu** --- Adım adım kurulum, disk bölümleme, ağ
    yapılandırma
3.  **Komut Satırı Temelleri** --- Terminal, kabuk, temel komutlar,
    yardım alma
4.  **Dosya Sistemi ve Dizin Yapısı** --- FHS standardı, dosya türleri,
    izinler
5.  **Metin Editörleri** --- vi/vim, nano, sed, awk

### BÖLÜM II --- SİSTEM YÖNETİMİ

6.  **Kullanıcı ve Grup Yönetimi** --- Hesap oluşturma, parola
    politikaları, sudo
7.  **Dosya İzinleri ve Sahiplik** --- chmod, chown, ACL, özel izinler
8.  **Paket Yönetimi** --- DNF/YUM, RPM, repo yönetimi
9.  **Süreç (Process) Yönetimi** --- ps, top, kill, systemd, cron
10. **Servis Yönetimi ve Systemd** --- systemctl, unit dosyaları,
    hedefler

### BÖLÜM III --- AĞ ve DEPOLAMA

11. **Ağ Yapılandırması** --- IP, DNS, NetworkManager, nmcli, nmtui
12. **Disk ve Depolama Yönetimi** --- Bölümleme, LVM, RAID, dosya
    sistemleri
13. **NFS ve Samba** --- Dosya paylaşımı, ağ dosya sistemleri
14. **Firewall Yönetimi** --- firewalld, iptables, nftables

### BÖLÜM IV --- GÜVENLİK

15. **SELinux** --- Kavramlar, modlar, politikalar, sorun giderme
16. **SSH ve Uzaktan Erişim** --- Anahtar tabanlı kimlik doğrulama,
    tünelleme
17. **Sistem Güvenliği** --- Sertleştirme, PAM, audit, güvenlik
    güncellemeleri

### BÖLÜM V --- SUNUCU SERVİSLERİ

18. **Web Sunucusu (Apache/Nginx)** --- Kurulum, yapılandırma, sanal
    sunucular, SSL
19. **DNS Sunucusu (BIND)** --- Alan adı çözümleme, zone dosyaları
20. **DHCP Sunucusu** --- Otomatik IP dağıtımı
21. **E-posta Sunucusu (Postfix)** --- MTA yapılandırması
22. **Veritabanı Sunucusu (MariaDB/PostgreSQL)** --- Kurulum, yönetim,
    yedekleme

### BÖLÜM VI --- İLERİ SEVİYE

23. **Kabuk Programlama (Bash Scripting)** --- Değişkenler, döngüler,
    fonksiyonlar, otomasyon
24. **Performans İzleme ve Optimizasyon** --- sar, vmstat, iostat,
    tuning
25. **Log Yönetimi** --- rsyslog, journald, logrotate, merkezi loglama
26. **Yedekleme ve Kurtarma** --- tar, rsync, dump, felaket kurtarma
    planları
27. **Konteyner Teknolojileri** --- Podman, Docker kavramları, container
    yönetimi
28. **Otomasyon (Ansible Temelleri)** --- Playbook, modüller, rol
    tabanlı yapılandırma
29. **Kernel Yönetimi ve Parametreleri** --- Modüller, sysctl, kernel
    güncelleme
30. **Sorun Giderme Rehberi** --- Sistematik yaklaşım, araçlar, gerçek
    senaryolar

------------------------------------------------------------------------

> **Not:** Her bölüm bağımsız olarak okunabilir şekilde tasarlanmıştır,
> ancak sıralı okuma önerilir.

# BÖLÜM 1: Linux ve RHEL Nedir?

------------------------------------------------------------------------

## 1.1 İşletim Sistemi Nedir?

Bir **işletim sistemi (Operating System --- OS)**, bilgisayar donanımı
ile kullanıcı (ve uygulamalar) arasındaki köprüdür. İşletim sistemi
olmadan bilgisayar donanımı tek başına bir işe yaramaz.

### İşletim Sisteminin Görevleri

  ------------------------------------------------------------
  Görev                    Açıklama
  ------------------------ -----------------------------------
  **Donanım Yönetimi**     CPU, RAM, disk, ağ kartı gibi
                           donanımları yönetir

  **Süreç Yönetimi**       Çalışan programları (süreçler)
                           yönetir, CPU zamanını paylaştırır

  **Bellek Yönetimi**      RAM'i programlalar arasında
                           paylaştırır, sanal bellek kullanır

  **Dosya Sistemi          Dosyaları düzenler, saklar, erişim
  Yönetimi**               izinlerini kontrol eder

  **Kullanıcı Yönetimi**   Kullanıcı hesaplarını ve
                           yetkilerini yönetir

  **Ağ Yönetimi**          Ağ bağlantılarını ve iletişimi
                           yönetir

  **Güvenlik**             Yetkisiz erişimi engeller, verileri
                           korur
  ------------------------------------------------------------

### İşletim Sistemi Katmanları

    ┌─────────────────────────────────────┐
    │         UYGULAMALAR                 │
    │   (Firefox, Apache, MySQL vb.)     │
    ├─────────────────────────────────────┤
    │         KABUK (Shell)               │
    │   (bash, zsh — kullanıcı arayüzü)  │
    ├─────────────────────────────────────┤
    │         KERNEL (Çekirdek)           │
    │   (Linux Kernel — donanım yönetimi) │
    ├─────────────────────────────────────┤
    │         DONANIM                     │
    │   (CPU, RAM, Disk, NIC vb.)        │
    └─────────────────────────────────────┘

**Kernel (Çekirdek):** İşletim sisteminin kalbidir. Donanımla doğrudan
iletişim kuran tek bileşendir. Uygulamalar, donanıma erişmek için
kernel'a "sistem çağrıları (system calls)" yapar.

------------------------------------------------------------------------

## 1.2 Linux Nedir?

### Kısa Tarihçe

  ------------------------------------------------------------
  Yıl                         Olay
  --------------------------- --------------------------------
  **1969**                    AT&T Bell Labs'ta **UNIX**
                              işletim sistemi geliştirildi
                              (Ken Thompson, Dennis Ritchie)

  **1983**                    Richard Stallman **GNU
                              Projesi**'ni başlattı (Free
                              Software hareketi)

  **1985**                    **Free Software Foundation
                              (FSF)** kuruldu

  **1991**                    Linus Torvalds, Helsinki
                              Üniversitesi'nde **Linux
                              çekirdeğini** yazdı

  **1992**                    Linux çekirdeği GNU araçlarıyla
                              birleştirilerek tam bir işletim
                              sistemi oluşturuldu

  **1993**                    İlk ticari dağıtımlar:
                              **Slackware**, **Debian**

  **1994**                    **Red Hat Linux** yayınlandı

  **2003**                    Red Hat, kurumsal ürün olarak
                              **RHEL**'i piyasaya sürdü
  ------------------------------------------------------------

### Linux = Kernel + GNU Araçları

Teknik olarak "Linux" sadece çekirdeğin adıdır. Günlük kullanımda
"Linux" dediğimizde, aslında **GNU/Linux** kombinasyonunu kastediyoruz:

- **Linux Kernel:** Donanım yönetimi, süreç zamanlama, bellek yönetimi
- **GNU Araçları:** Kabuk (bash), dosya araçları (ls, cp, mv), metin
  araçları (grep, sed, awk), derleyiciler (gcc)
- **Ek Yazılımlar:** Paket yöneticileri, masaüstü ortamları, sunucu
  servisleri

### Linux'un Temel Felsefesi

1.  **Her şey bir dosyadır** --- Donanımlar bile `/dev/` altında dosya
    olarak temsil edilir
2.  **Küçük, tek işe odaklı programlar** --- Her program bir işi iyi
    yapar
3.  **Programlar birbirine bağlanabilir** --- Pipe (`|`) ile çıktılar
    birleştirilebilir
4.  **Metin tabanlı yapılandırma** --- Ayarlar metin dosyalarında
    saklanır
5.  **Açık kaynak** --- Kaynak kodu herkese açıktır

------------------------------------------------------------------------

## 1.3 Linux Dağıtımları

Bir **Linux dağıtımı (distribution/distro)**, Linux çekirdeği üzerine
farklı yazılımlar, araçlar ve yapılandırma felsefesiyle oluşturulan
paket bir işletim sistemidir.

### Başlıca Dağıtım Aileleri

                             ┌──────────┐
                             │  LINUX   │
                             │  KERNEL  │
                             └────┬─────┘
                                  │
                  ┌───────────────┼───────────────┐
                  │               │               │
            ┌─────┴─────┐  ┌─────┴─────┐  ┌──────┴──────┐
            │  Red Hat   │  │  Debian   │  │   SUSE      │
            │  Ailesi    │  │  Ailesi   │  │   Ailesi    │
            └─────┬─────┘  └─────┬─────┘  └──────┬──────┘
                  │               │               │
            ┌─────┼─────┐    ┌───┼───┐       ┌───┼───┐
            │     │     │    │   │   │       │       │
           RHEL Fedora CentOS Ubuntu Mint  SLES  openSUSE
                  │          Stream     │
            AlmaLinux         │
            Rocky Linux    Kubuntu
                           Pop!_OS

### Red Hat Ailesi Karşılaştırması

  --------------------------------------------------------------------------
  Dağıtım         Amaç          Destek       Paket Yöneticisi     Maliyet
  --------------- ------------- ------------ -------------------- ----------
  **RHEL**        Kurumsal      Red Hat      DNF/YUM (RPM)        Ücretli
                  üretim        resmi                             abonelik
                  ortamları     desteği                           
                                (7-10 yıl)                        

  **Fedora**      Son           Topluluk     DNF (RPM)            Ücretsiz
                  teknoloji,    desteği                           
                  geliştirici                                     

  **CentOS        RHEL'in       Topluluk     DNF (RPM)            Ücretsiz
  Stream**        geliştirme    desteği                           
                  dalı                                            

  **AlmaLinux**   RHEL uyumlu,  Topluluk +   DNF (RPM)            Ücretsiz
                  topluluk      kurumsal                          
                  destekli                                        

  **Rocky Linux** RHEL uyumlu,  Topluluk     DNF (RPM)            Ücretsiz
                  topluluk                                        
                  destekli                                        
  --------------------------------------------------------------------------

------------------------------------------------------------------------

## 1.4 RHEL (Red Hat Enterprise Linux) Nedir?

**Red Hat Enterprise Linux (RHEL)**, Red Hat şirketi tarafından
geliştirilen, **kurumsal kullanım** için tasarlanmış, ticari destekli
bir Linux dağıtımıdır.

### RHEL'in Öne Çıkan Özellikleri

1.  **Kararlılık:** Paketler kapsamlı test süreçlerinden geçer. Üretim
    ortamları için güvenilirdir.
2.  **Uzun Ömürlü Destek:** Her ana sürüm 10 yıla kadar destek alır
    (güvenlik yamaları, hata düzeltmeleri).
3.  **Sertifikasyon:** SAP, Oracle, VMware gibi büyük yazılım
    üreticileri RHEL üzerinde sertifikalıdır.
4.  **Güvenlik:** SELinux varsayılan olarak etkindir. FIPS 140-2
    uyumluluğu mevcuttur.
5.  **Otomasyon:** Ansible, Satellite, Insights gibi yönetim araçlarıyla
    entegre çalışır.
6.  **Konteyner Desteği:** Podman, Buildah, Skopeo gibi araçlarla
    konteyner yönetimi.

### RHEL Sürüm Yaşam Döngüsü

    RHEL Sürüm Yaşam Döngüsü (10 Yıl)
    =========================================================
    Yıl 1-5  │ FULL SUPPORT (Tam Destek)
             │ ─ Yeni özellikler
             │ ─ Güvenlik yamaları
             │ ─ Hata düzeltmeleri
             │ ─ Donanım desteği genişletmeleri
    ─────────┼──────────────────────────────────
    Yıl 5-10 │ MAINTENANCE SUPPORT (Bakım Desteği)
             │ ─ Kritik güvenlik yamaları
             │ ─ Kritik hata düzeltmeleri
             │ ─ Yeni özellik YOK
    ─────────┼──────────────────────────────────
    Yıl 10+  │ EXTENDED LIFE PHASE
             │ ─ Yalnızca ek ücretli destek
    =========================================================

### RHEL Versiyonları

  ------------------------------------------------------------
  Sürüm    Çıkış Yılı      Kernel    Öne Çıkan Özellikler
  -------- --------------- --------- -------------------------
  RHEL 7   2014            3.10      systemd'ye geçiş, XFS
                                     varsayılan dosya sistemi

  RHEL 8   2019            4.18      DNF paket yöneticisi,
                                     Application Streams,
                                     Cockpit

  RHEL 9   2022            5.14      Gelişmiş güvenlik,
                                     WireGuard, kernel live
                                     patching
  ------------------------------------------------------------

### RHEL Nasıl Edinilir?

1.  **Developer Subscription (Ücretsiz):**
    [developers.redhat.com](https://developers.redhat.com) adresinden
    ücretsiz geliştirici aboneliği alarak 16 sisteme kadar
    kullanabilirsiniz.
2.  **Ticari Abonelik:** Üretim ortamları için Red Hat'ten satın alınır.
3.  **Deneme Sürümü:** 60 günlük değerlendirme lisansı mevcuttur.
4.  **AlmaLinux/Rocky Linux:** RHEL ile birebir uyumlu, ücretsiz
    alternatifler (öğrenim için idealdir).

------------------------------------------------------------------------

## 1.5 Neden RHEL Öğrenmelisiniz?

### İş Piyasasında RHEL

- **Fortune 500** şirketlerinin %90'ından fazlası RHEL kullanır
- **Bankacılık, sağlık, devlet kurumları** RHEL tercih eder
- **RHCSA (Red Hat Certified System Administrator)** ve **RHCE (Red Hat
  Certified Engineer)** sertifikaları, IT sektöründe en değerli Linux
  sertifikalarıdır
- Ortalama RHEL sistem yöneticisi maaşı, genel Linux yöneticilerinden
  %15-25 daha yüksektir

### RHEL Bilgisi ile Neler Yapabilirsiniz?

- Kurumsal sunucuları yönetebilirsiniz
- Bulut altyapılarını (AWS, Azure, GCP) yönetebilirsiniz
- CI/CD pipeline'ları kurabilirsiniz
- Konteyner ve Kubernetes ortamlarını yönetebilirsiniz
- DevOps mühendisi olarak çalışabilirsiniz

------------------------------------------------------------------------

## 1.6 Sık Karşılaşılan Sorular ve Sorunlar

### ❓ "Linux mu yoksa Windows mu öğrenmeliyim?"

Her iki işletim sistemi de farklı alanlarda güçlüdür:

  ---------------------------------------------------------------
  Kriter          Linux/RHEL           Windows Server
  --------------- -------------------- --------------------------
  **Sunucu Pazar  \~75-80% (web        \~20-25%
  Payı**          sunucuları)          

  **Bulut         AWS/Azure/GCP'de     Azure'da güçlü
  Kullanımı**     baskın               

  **Maliyet**     Düşük (özellikle     Yüksek lisans maliyeti
                  AlmaLinux)           

  **Güvenlik**    SELinux, AppArmor    Windows Defender,
                                       BitLocker

  **Otomasyon**   Bash, Python,        PowerShell, SCCM
                  Ansible              

  **Öğrenme       Dik (komut satırı    Daha kolay (GUI odaklı)
  Eğrisi**        odaklı)              
  ---------------------------------------------------------------

**Sonuç:** Sunucu yönetimi, bulut bilişim veya DevOps alanında çalışmak
istiyorsanız Linux bilgisi **zorunludur**.

### ❓ "RHEL mi, Ubuntu mu öğrenmeliyim?"

- **Kurumsal ortamlar** → RHEL (ve CentOS/Alma/Rocky ailesi)
- **Kişisel kullanım ve başlangıç** → Ubuntu
- **İkisini de bilmek** en idealdir, ancak kurumsal IT'de RHEL bilgisi
  daha değerlidir

### ❓ "RHEL yerine ücretsiz AlmaLinux kullanabilir miyim?"

Evet! AlmaLinux, RHEL ile birebir ikili uyumludur. Öğrenim sürecinizde
AlmaLinux veya Rocky Linux kullanabilirsiniz. Öğrendiğiniz her şey
doğrudan RHEL'e aktarılabilir.

------------------------------------------------------------------------

## 1.7 Bölüm Özeti

Bu bölümde öğrendikleriniz: - ✅ İşletim sistemi kavramı ve katmanları -
✅ Linux'un tarihi ve felsefesi - ✅ Linux dağıtımları ve aileleri - ✅
RHEL'in ne olduğu, özellikleri ve yaşam döngüsü - ✅ Neden RHEL
öğrenmeniz gerektiği - ✅ RHEL nasıl edinilir

**Bir sonraki bölümde:** RHEL kurulumunu adım adım gerçekleştireceğiz.

# BÖLÜM 2: RHEL Kurulumu

------------------------------------------------------------------------

## 2.1 Kurulum Öncesi Hazırlık

### Minimum Donanım Gereksinimleri

  --------------------------------------------------------------
  Kaynak               Minimum              Önerilen (Sunucu)
  -------------------- -------------------- --------------------
  **CPU**              1 GHz x86_64         2+ GHz, çok
                                            çekirdekli

  **RAM**              1.5 GB               4 GB+ (servis
                                            sayısına göre artır)

  **Disk**             10 GB                50 GB+ (ayrı
                                            bölümler için daha
                                            fazla)

  **Ağ**               Opsiyonel            Ethernet kartı
                                            (sunucu için
                                            zorunlu)
  --------------------------------------------------------------

### Kurulum Medyası Hazırlama

#### ISO Dosyasını İndirme

1.  [developers.redhat.com](https://developers.redhat.com) adresine
    gidin
2.  Ücretsiz geliştirici hesabı oluşturun
3.  "Downloads" → "Red Hat Enterprise Linux" seçin
4.  En güncel sürümü (RHEL 9.x) indirin

**İki tür ISO vardır:**

  -------------------------------------------------------------
  ISO Türü               Boyut           Açıklama
  ---------------------- --------------- ----------------------
  **Boot ISO**           \~800 MB        Sadece kurucu,
                                         paketleri internetten
                                         indirir

  **DVD ISO**            \~8 GB          Tüm paketleri içerir,
                                         çevrimdışı kurulum
                                         yapılabilir
  -------------------------------------------------------------

> 💡 **Önerilen:** İnternet bağlantınız varsa Boot ISO yeterlidir.
> Sunucu ortamında çevrimdışı kurulum gerekiyorsa DVD ISO kullanın.

#### Önyüklenebilir USB Hazırlama

**Windows'ta:**

    # Rufus aracını kullanın (rufus.ie)
    1. Rufus'u indirin ve çalıştırın
    2. "Aygıt" bölümünden USB belleginizi seçin
    3. "Önyükleme seçimi"nde RHEL ISO'yu seçin
    4. "Bölüm şeması" olarak GPT seçin (UEFI için)
    5. "Başlat" düğmesine basın

**Linux'ta:**

    # USB cihazınızı belirleyin
    lsblk

    # ISO'yu USB'ye yazın (sdX yerine USB cihazınızı yazın!)
    sudo dd if=rhel-9.x-x86_64-dvd.iso of=/dev/sdX bs=4M status=progress oflag=sync

    # DİKKAT: /dev/sdX yerine doğru cihazı yazın! 
    # Yanlış cihaz seçerseniz tüm verilerinizi kaybedersiniz!

### Sanal Makine ile Kurulum (Öğrenim İçin Önerilir)

Öğrenim amaçlı, fiziksel bir makineye kurmadan önce **sanal makine
(VM)** kullanmanız şiddetle önerilir.

#### VirtualBox ile VM Oluşturma

    1. VirtualBox'ı indirin ve kurun (virtualbox.org)
    2. "Yeni" → Makine adı: "RHEL9"
    3. Tip: Linux, Sürüm: Red Hat (64-bit)
    4. Bellek: 4096 MB (4 GB)
    5. Sanal Disk: 50 GB (Dinamik olarak ayrılan)
    6. Ayarlar → Depolama → ISO'yu optik sürücüye bağlayın
    7. Ayarlar → Ağ → "Köprü Bağdaştırıcı" seçin (gerçek IP almak için)
    8. Başlat

#### KVM/QEMU ile VM Oluşturma

    # KVM desteğini kontrol edin
    egrep -c '(vmx|svm)' /proc/cpuinfo
    # Sonuç 0'dan büyükse KVM destekleniyor

    # Gerekli paketleri kurun
    sudo dnf install qemu-kvm libvirt virt-install virt-manager

    # libvirtd servisini başlatın
    sudo systemctl enable --now libvirtd

    # VM oluşturun
    sudo virt-install \
      --name rhel9-lab \
      --ram 4096 \
      --vcpus 2 \
      --disk size=50 \
      --os-variant rhel9.0 \
      --cdrom /path/to/rhel-9.x-x86_64-dvd.iso \
      --network bridge=virbr0 \
      --graphics spice

------------------------------------------------------------------------

## 2.2 Kurulum Adımları

### Adım 1: Önyükleme ve Kurulum Başlatma

Sistem ISO'dan önyüklediğinde şu seçenekler gelir:

    ┌────────────────────────────────────────┐
    │  Install Red Hat Enterprise Linux 9    │  ← Bunu seçin
    │  Test this media & install RHEL 9      │
    │  Troubleshooting                       │
    └────────────────────────────────────────┘

- **"Install...":** Doğrudan kuruluma başlar
- **"Test this media...":** Önce ISO'nun bozuk olmadığını kontrol eder,
  sonra kurar (ilk kurulumda önerilir)
- **"Troubleshooting":** Sorun giderme seçenekleri (temel grafik modu,
  bellek testi vb.)

### Adım 2: Dil ve Klavye Seçimi

- **Dil:** Türkçe veya İngilizce (sunucu ortamı için İngilizce önerilir)
- **Klavye:** Türkçe Q klavye

> 💡 **Neden İngilizce?** Hata mesajları İngilizce olur, internetten
> çözüm bulmak kolaylaşır. Log dosyaları İngilizce olur, sorun giderme
> hızlanır.

### Adım 3: Kurulum Hedefi (Installation Destination)

Bu en kritik adımdır: **Disk bölümleme.**

#### Otomatik Bölümleme

Yeni başlayanlar için "Otomatik" seçeneği uygundur. RHEL şu bölümleri
oluşturur:

  --------------------------------------------------------------
  Bölüm                Boyut                Açıklama
  -------------------- -------------------- --------------------
  `/boot`              1 GB                 Kernel ve önyükleme
                                            dosyaları

  `/boot/efi`          600 MB               UEFI önyükleme (UEFI
                                            sistemlerde)

  `swap`               RAM boyutu kadar     Sanal bellek

  `/` (root)           Kalan alan           İşletim sistemi ve
                                            veriler
  --------------------------------------------------------------

#### Manuel Bölümleme (Önerilen --- Sunucu Ortamı)

Sunucu ortamında ayrı bölümler oluşturmak **güvenlik** ve **yönetim**
açısından kritiktir:

  --------------------------------------------------------------
  Bölüm         Önerilen Boyut             Neden Ayrı?
  ------------- -------------------------- ---------------------
  `/boot`       1 GB                       Kernel
                                           güncellemelerinde
                                           sorun çıkmasını önler

  `/boot/efi`   600 MB                     UEFI önyükleme
                                           (gerekiyorsa)

  `swap`        RAM'in 1-2 katı            Bellek tükenmesi
                                           durumu için

  `/` (root)    20-30 GB                   Temel sistem
                                           dosyaları

  `/home`       10+ GB                     Kullanıcı verileri
                                           (dolu olsa bile
                                           sistem çalışır)

  `/var`        20+ GB                     Loglar,
                                           veritabanları, web
                                           içerikleri

  `/var/log`    10+ GB                     Log dosyaları (taşma
                                           durumunda sistemi
                                           etkilemez)

  `/tmp`        5 GB                       Geçici dosyalar
                                           (güvenlik için ayrı
                                           bağlanır)

  `/opt`        10+ GB                     Üçüncü parti
                                           uygulamalar
  --------------------------------------------------------------

> ⚠️ **Kritik:** `/var/log` bölümünü ayırmak çok önemlidir! Log
> dosyaları diski doldurursa ve `/var/log` ayrı bir bölüm değilse, tüm
> sistem çökebilir.

#### LVM (Logical Volume Manager) Kullanımı

Manuel bölümlemede **LVM** kullanmanız şiddetle önerilir:

**LVM'in Avantajları:** - Bölüm boyutlarını sonradan
**büyütebilirsiniz** - Anlık görüntü (snapshot) alabilirsiniz - Birden
fazla diski tek bir mantıksal birim olarak kullanabilirsiniz

    Fiziksel Diskler          LVM Katmanları           Bağlama Noktaları
    ================         ==================        =================

    ┌──────────┐            ┌──────────────┐
    │ /dev/sda │──→ PV ──→  │  Volume      │──→ LV /  ──→  /
    │          │            │  Group       │──→ LV home ──→ /home
    └──────────┘            │  (vg_rhel)   │──→ LV var ──→  /var
    ┌──────────┐            │              │──→ LV swap ──→ swap
    │ /dev/sdb │──→ PV ──→  │              │
    │          │            └──────────────┘
    └──────────┘

    PV = Physical Volume (Fiziksel Hacim)
    VG = Volume Group (Hacim Grubu)
    LV = Logical Volume (Mantıksal Hacim)

### Adım 4: Ağ ve Ana Bilgisayar Adı

    Ana Bilgisayar Adı (Hostname): sunucu01.sirket.local
    Ağ:
      ├── Ethernet (ens192 / enp0s3)
      │   ├── IPv4: DHCP veya Manuel
      │   │   ├── IP Adresi: 192.168.1.100
      │   │   ├── Alt Ağ Maskesi: 255.255.255.0 (/24)
      │   │   ├── Ağ Geçidi: 192.168.1.1
      │   │   └── DNS: 8.8.8.8, 8.8.4.4
      │   └── IPv6: Otomatik veya Devre dışı
      └── Bağlantıyı AÇ!

> ⚠️ **Önemli:** "Bağlan" düğmesini açmayı **unutmayın!** Varsayılan
> olarak ağ bağlantısı kapalıdır.

### Adım 5: Yazılım Seçimi

  ----------------------------------------------------------------
  Profil            Açıklama          Kullanım Alanı
  ----------------- ----------------- ----------------------------
  **Minimal         Sadece temel      Sunucu (önerilen)
  Install**         sistem, GUI yok   

  **Server**        Temel sunucu      Genel sunucu
                    araçları          

  **Server with     GNOME masaüstü +  Yönetim kolaylığı
  GUI**             sunucu araçları   

  **Workstation**   Tam masaüstü      Geliştirici iş istasyonu
                    ortamı            
  ----------------------------------------------------------------

> 💡 **Sunucu için en iyi pratik:** "Minimal Install" seçin, ihtiyacınız
> olan paketleri sonra kurun. Ne kadar az paket kurarsanız, saldırı
> yüzeyi o kadar küçük olur.

### Adım 6: Saat Dilimi ve NTP

- **Saat Dilimi:** Europe/Istanbul (UTC+3)
- **Ağ Zamanı (NTP):** **Açık** olmalı!

<!-- -->

    NTP Sunucuları:
      ├── 0.rhel.pool.ntp.org
      ├── 1.rhel.pool.ntp.org
      ├── 2.rhel.pool.ntp.org
      └── 3.rhel.pool.ntp.org

> ⚠️ **Neden önemli?** Yanlış saat, Kerberos kimlik doğrulamasını bozar,
> sertifika doğrulamalarında hata verir, log dosyalarında tutarsızlık
> oluşturur.

### Adım 7: Root Parolası ve Kullanıcı Oluşturma

**Root Parolası:** - En az 12 karakter - Büyük harf, küçük harf, rakam
ve özel karakter - Sözlük kelimelerinden kaçının

**Normal Kullanıcı:** - "Bu kullanıcıyı yönetici yap" seçeneğini
işaretleyin (sudo yetkisi verir) - Günlük işlemlerde root yerine bu
kullanıcıyı kullanın

> ⚠️ **Güvenlik Kuralı:** Root hesabıyla doğrudan oturum açmayın! Normal
> kullanıcı ile giriş yapıp, gerektiğinde `sudo` kullanın.

### Adım 8: Kurulumu Başlatın

"Kurulumu Başlat" düğmesine basın. Kurulum genellikle 15-30 dakika sürer
(donanıma ve seçilen paketlere bağlı).

------------------------------------------------------------------------

## 2.3 Kurulum Sonrası İlk Yapılandırmalar

### Sisteme İlk Giriş

    # Oturum açın (normal kullanıcı ile)
    login: kullanici
    Password: ****

    # root yetkisi alın
    sudo -i
    # veya
    su -

### Sistemi Güncelleyin

    # Mevcut paketleri güncelle
    sudo dnf update -y

    # Yeniden başlat (kernel güncellemesi varsa gerekli)
    sudo reboot

### Abonelik Kaydı

    # RHEL aboneliğini kaydet
    sudo subscription-manager register --username KULLANICI_ADINIZ --password PAROLANIZ

    # Mevcut abonelikleri listele
    sudo subscription-manager list --available

    # Abonelik ekle
    sudo subscription-manager attach --auto

    # Depo listesini kontrol et
    sudo dnf repolist

### Temel Araçları Kurun

    # Sık kullanılan araçlar
    sudo dnf install -y vim wget curl net-tools bind-utils \
      bash-completion tree htop lsof telnet traceroute

    # Geliştirme araçları (gerekirse)
    sudo dnf groupinstall -y "Development Tools"

### Hostname Ayarlama

    # Mevcut hostname'i görüntüle
    hostnamectl

    # Hostname değiştir
    sudo hostnamectl set-hostname sunucu01.sirket.local

    # /etc/hosts dosyasını düzenle
    sudo vim /etc/hosts

`/etc/hosts` dosyası:

    127.0.0.1   localhost localhost.localdomain
    ::1         localhost localhost.localdomain
    192.168.1.100  sunucu01.sirket.local sunucu01

------------------------------------------------------------------------

## 2.4 Kickstart ile Otomatik Kurulum

Çok sayıda RHEL sunucusu kuracaksanız, her seferinde elle kurulum yapmak
pratik değildir. **Kickstart** dosyası ile kurulumu tamamen otomatik
hale getirebilirsiniz.

### Kickstart Dosyası Örneği

    # /root/anaconda-ks.cfg dosyasından şablon alabilirsiniz
    # veya sıfırdan yazabilirsiniz:

    cat > /var/www/html/ks.cfg << 'EOF'
    #version=RHEL9

    # Dil ve klavye
    lang tr_TR.UTF-8
    keyboard --vckeymap=trq --xlayouts='tr'

    # Ağ yapılandırması
    network --bootproto=dhcp --device=ens192 --activate
    network --hostname=sunucu01.sirket.local

    # Root parolası (SHA512 hash)
    rootpw --iscrypted $6$xxxxxxxxxxxx

    # Saat dilimi
    timezone Europe/Istanbul --utc
    timesource --ntp-server=0.rhel.pool.ntp.org

    # Disk bölümleme
    ignoredisk --only-use=sda
    autopart --type=lvm
    clearpart --all --initlabel

    # Yazılım seçimi
    %packages
    @^minimal-environment
    vim-enhanced
    wget
    curl
    net-tools
    bash-completion
    %end

    # Kurulum sonrası komutlar
    %post
    # Sistemi güncelle
    dnf update -y

    # SSH root girişini kapat
    sed -i 's/^PermitRootLogin yes/PermitRootLogin no/' /etc/ssh/sshd_config

    # Firewall'u etkinleştir
    systemctl enable firewalld
    %end

    # Kurulum tamamlandığında yeniden başlat
    reboot
    EOF

### Kickstart ile Kurulum Başlatma

Kurulum başlatılırken boot menüsünde `Tab` veya `e` tuşuna basıp şu
parametreyi ekleyin:

    inst.ks=http://sunucu-ip/ks.cfg
    # veya
    inst.ks=nfs:sunucu-ip:/paylasim/ks.cfg
    # veya
    inst.ks=cdrom:/ks.cfg

------------------------------------------------------------------------

## 2.5 Sık Karşılaşılan Kurulum Sorunları ve Çözümleri

### ⚠️ Sorun 1: "No bootable device found"

**Neden:** BIOS/UEFI boot sırası yanlış veya USB doğru hazırlanmamış.

**Çözüm:** 1. BIOS/UEFI'ye girin (F2, F12, Del) 2. Boot sırasını kontrol
edin, USB'yi ilk sıraya alın 3. **Secure Boot** kapalıysa açın veya tam
tersi deneyin 4. USB'yi farklı bir porta takın 5. ISO'yu yeniden yazın
(dd veya Rufus ile)

### ⚠️ Sorun 2: Grafik ekranı gelmiyor / siyah ekran

**Neden:** Ekran kartı sürücüsü uyumsuz.

**Çözüm:**

    # Boot menüsünde Tab/e tuşuna basın ve satırın sonuna ekleyin:
    inst.text                # Metin modunda kurulum
    # veya
    nomodeset                # Grafik sürücüsünü devre dışı bırakır
    # veya  
    inst.resolution=1024x768 # Çözünürlüğü düşürür

### ⚠️ Sorun 3: Disk görünmüyor

**Neden:** RAID kontrolcüsü sürücüsü eksik veya disk formatı tanınmıyor.

**Çözüm:** 1. BIOS'ta SATA modunu **AHCI** olarak ayarlayın (IDE veya
RAID modundan çevirin) 2. Varsa RAID kontrolcü sürücüsünü (driver disk)
yükleyin:

    # Boot menüsünde:
    inst.dd    # Sürücü diski yükleme modunu açar

### ⚠️ Sorun 4: Ağ bağlantısı çalışmıyor (kurulum sırasında)

**Neden:** Ağ kartı sürücüsü yok veya DHCP hizmeti mevcut değil.

**Çözüm:** 1. Manuel IP yapılandırması deneyin 2. Farklı ağ kartı
kullanın (USB Ethernet adaptörü) 3. DVD ISO kullanarak çevrimdışı
kurulum yapın

### ⚠️ Sorun 5: "Not enough space" hatası

**Neden:** Seçilen disk yeterli boyutta değil veya eski bölümler var.

**Çözüm:** 1. "Kurulum Hedefi"nde "Yer açmak istiyorum" seçin 2. Eski
bölümleri silin 3. Daha büyük bir disk kullanın 4. Minimal kurulum seçin

### ⚠️ Sorun 6: UEFI vs Legacy BIOS karışıklığı

**Neden:** ISO, UEFI modunda hazırlanmış ama sistem Legacy BIOS
kullanıyor (veya tam tersi).

**Çözüm:**

    UEFI Sistemi:
    - Rufus'ta GPT + UEFI seçin
    - /boot/efi bölümü (600 MB, FAT32) oluşturun
    - Secure Boot ayarını kontrol edin

    Legacy BIOS Sistemi:
    - Rufus'ta MBR + BIOS seçin
    - /boot/efi gerekmez
    - /boot bölümü yeterlidir

------------------------------------------------------------------------

## 2.6 Bölüm Özeti

Bu bölümde öğrendikleriniz: - ✅ Donanım gereksinimleri ve ISO
hazırlama - ✅ Sanal makine oluşturma (VirtualBox, KVM) - ✅ Adım adım
RHEL kurulumu - ✅ Disk bölümleme stratejileri ve LVM - ✅ Kurulum
sonrası ilk yapılandırmalar - ✅ Kickstart ile otomatik kurulum - ✅ Sık
karşılaşılan kurulum sorunları ve çözümleri

**Bir sonraki bölümde:** Komut satırı temellerini öğreneceksiniz ---
Linux'un gerçek gücü burada!

# BÖLÜM 3: Komut Satırı Temelleri

------------------------------------------------------------------------

## 3.1 Terminal ve Kabuk (Shell)

### Terminal Nedir?

**Terminal (konsol)**, kullanıcının kabuk (shell) ile etkileşim kurduğu
metin tabanlı arayüzdür. Fiziksel bir terminale ihtiyaç yoktur ---
modern sistemlerde bir **terminal emülatörü** kullanılır.

Terminal erişim yolları: - **Fiziksel konsolda:** `Ctrl + Alt + F2` ile
`F6` arası (tty2 -- tty6) - **GUI'den geri dönüş:** `Ctrl + Alt + F1`
(GUI oturumu) - **GUI üzerinde terminal:** GNOME Terminal, Konsole -
**Uzaktan erişim:** SSH ile (`ssh kullanici@sunucu-ip`)

### Kabuk (Shell) Nedir?

Kabuk, yazdığınız komutları yorumlayan ve çekirdeğe (kernel) ileten
programdır.

#### Mevcut Kabuklar

    # Sistemde kurulu kabukları listele
    cat /etc/shells

  --------------------------------------------------------------
  Kabuk                Açıklama             Komut
  -------------------- -------------------- --------------------
  **bash**             Bourne Again Shell   `/bin/bash`
                       --- varsayılan, en   
                       yaygın               

  **sh**               Bourne Shell ---     `/bin/sh`
                       temel, POSIX uyumlu  

  **zsh**              Z Shell --- gelişmiş `/bin/zsh`
                       özellikler, tema     
                       desteği              

  **csh**              C Shell --- C diline `/bin/csh`
                       benzer söz dizimi    

  **ksh**              Korn Shell ---       `/bin/ksh`
                       ticari UNIX'lerde    
                       yaygın               
  --------------------------------------------------------------

    # Kullandığınız kabuğu öğrenin
    echo $SHELL

    # Geçici olarak farklı kabuk kullanın
    zsh
    # Geri dönmek için:
    exit

### Komut İstemi (Prompt)

    [kullanici@sunucu01 ~]$ 
     │          │        │ │
     │          │        │ └─ $ = normal kullanıcı, # = root kullanıcı
     │          │        └─── Mevcut dizin (~ = ev dizini)
     │          └──────────── Hostname
     └─────────────────────── Kullanıcı adı

> 💡 **Kural:** `$` işareti görüyorsanız normal kullanıcısınız, `#`
> görüyorsanız root'sunuz. Root iken dikkatli olun!

------------------------------------------------------------------------

## 3.2 Komut Yapısı

### Genel Söz Dizimi

    KOMUT [SEÇENEKLER] [ARGÜMANLAR]

Örnekler:

    ls                          # Komut (argümansız)
    ls -l                       # Komut + seçenek
    ls -la /var/log              # Komut + seçenekler + argüman
    ls --all --human-readable -l # Uzun seçenek formatı

### Seçenek Türleri

  -------------------------------------------------------------
  Tür           Söz Dizimi                   Örnek
  ------------- ---------------------------- ------------------
  **Kısa        Tek `-` ve tek harf          `ls -l`, `ls -a`
  seçenek**                                  

  **Birleşik    Birden fazla harf            `ls -la` (=
  kısa                                       `ls -l -a`)
  seçenek**                                  

  **Uzun        Çift `--` ve tam kelime      `ls --all`,
  seçenek**                                  `ls --long`
  -------------------------------------------------------------

------------------------------------------------------------------------

## 3.3 Temel Komutlar

### Dizin İşlemleri

    # Mevcut dizini göster
    pwd
    # Çıktı: /home/kullanici

    # Dizin değiştir
    cd /var/log          # Belirtilen dizine git
    cd                   # Ev dizinine dön
    cd ~                 # Ev dizinine dön (aynı şey)
    cd ..                # Bir üst dizine çık
    cd -                 # Önceki dizine dön
    cd ../..             # İki üst dizine çık

    # Dizin içeriğini listele
    ls                   # Temel listeleme
    ls -l                # Uzun format (izinler, boyut, tarih)
    ls -la               # Gizli dosyalar dahil
    ls -lh               # Boyutları okunabilir formatta
    ls -lt               # Zamana göre sırala (en yeni ilk)
    ls -lS               # Boyuta göre sırala (en büyük ilk)
    ls -R                # Alt dizinleri de listele (recursive)
    ls -ld /dizin        # Dizinin kendisinin bilgisi

    # Dizin oluştur
    mkdir yenidizin                    # Tek dizin
    mkdir -p proje/src/main/java       # İç içe dizinler
    mkdir -m 755 yenidizin             # İzinle birlikte oluştur

    # Dizin sil
    rmdir bosdizin                     # Sadece boş dizin silinir
    rm -r doluizin                     # Dolu dizini sil (dikkatli!)
    rm -rf dizin                       # Sormadan sil (ÇOK DİKKATLİ!)

> ⚠️ **UYARI:** `rm -rf /` komutu TÜM SİSTEMİ SİLER! Bu komutu asla root
> olarak çalıştırmayın. RHEL 7+'da `--no-preserve-root` olmadan çalışmaz
> ama yine de dikkatli olun.

### Dosya İşlemleri

    # Dosya oluştur
    touch dosya.txt                    # Boş dosya oluştur (veya zaman damgasını güncelle)

    # Dosya kopyala
    cp kaynak.txt hedef.txt            # Dosya kopyala
    cp -r kaynakdizin/ hedeftizin/     # Dizin kopyala (recursive)
    cp -p dosya.txt yedek.txt          # İzinleri ve zaman damgasını koru
    cp -a kaynakdizin/ hedeftizin/     # Arşiv modu (her şeyi korur)
    cp -i dosya.txt hedef.txt          # Üzerine yazmadan önce sor

    # Dosya taşı / yeniden adlandır
    mv dosya.txt yeniad.txt            # Yeniden adlandır
    mv dosya.txt /var/backups/         # Taşı
    mv -i kaynak hedef                 # Üzerine yazmadan önce sor

    # Dosya sil
    rm dosya.txt                       # Sil
    rm -i dosya.txt                    # Onay iste
    rm -f dosya.txt                    # Zorla sil (hata mesajı vermez)

    # Dosya içeriğini görüntüle
    cat dosya.txt                      # Tümünü göster
    less dosya.txt                     # Sayfa sayfa göster (q ile çık)
    more dosya.txt                     # Sayfa sayfa göster (eski versiyon)
    head dosya.txt                     # İlk 10 satır
    head -n 20 dosya.txt               # İlk 20 satır
    tail dosya.txt                     # Son 10 satır
    tail -n 20 dosya.txt               # Son 20 satır
    tail -f /var/log/messages          # Canlı takip (yeni satırları göster)

    # Dosya türünü belirle
    file dosya.txt                     # Dosya türünü göster
    # Çıktı: dosya.txt: UTF-8 Unicode text

### Dosya Arama

    # find — dizin ağacında dosya ara
    find / -name "dosya.txt"                      # İsme göre ara
    find / -iname "dosya.txt"                     # Büyük/küçük harf duyarsız
    find /var -name "*.log"                       # Joker karakter ile
    find / -type f -name "*.conf"                 # Sadece dosyalar
    find / -type d -name "config"                 # Sadece dizinler
    find / -size +100M                            # 100 MB'den büyük dosyalar
    find / -mtime -7                              # Son 7 günde değişenler
    find / -user root -perm 777                   # root'a ait, 777 izinli
    find / -empty                                 # Boş dosya ve dizinler
    find /tmp -name "*.tmp" -delete               # Bul ve sil
    find / -name "*.log" -exec gzip {} \;         # Bul ve sıkıştır

    # locate — veritabanında hızlı arama
    sudo dnf install mlocate                      # Kur
    sudo updatedb                                 # Veritabanını güncelle
    locate dosya.txt                              # Hızlı arama

    # which — komutun yolunu bul
    which bash
    # /usr/bin/bash

    # whereis — komut, kaynak ve man sayfasını bul
    whereis ls
    # ls: /usr/bin/ls /usr/share/man/man1/ls.1.gz

------------------------------------------------------------------------

## 3.4 Giriş/Çıkış Yönlendirme ve Boru Hattı (Pipe)

### Standart Akımlar

    ┌────────────┐     ┌──────────┐     ┌─────────────┐
    │  stdin (0)  │────→│  PROGRAM │────→│ stdout (1)  │
    │  (Klavye)  │     │          │     │ (Ekran)      │
    │            │     │          │     │              │
    │            │     │          │────→│ stderr (2)  │
    │            │     └──────────┘     │ (Ekran)      │
    └────────────┘                      └─────────────┘

  ---------------------------------------------------------------
  Akım            Dosya           Varsayılan      Açıklama
                  Tanımlayıcı                     
  --------------- --------------- --------------- ---------------
  **stdin**       0               Klavye          Program girdisi

  **stdout**      1               Ekran           Program çıktısı
                                                  (normal)

  **stderr**      2               Ekran           Hata mesajları
  ---------------------------------------------------------------

### Yönlendirme Operatörleri

    # stdout yönlendirme
    ls -l > liste.txt                    # Çıktıyı dosyaya yaz (üzerine yazar!)
    ls -l >> liste.txt                   # Çıktıyı dosyaya ekle (append)

    # stderr yönlendirme
    find / -name "*.conf" 2> hatalar.txt         # Hataları dosyaya yaz
    find / -name "*.conf" 2>/dev/null            # Hataları gizle

    # stdout + stderr birlikte
    find / -name "*.conf" > sonuc.txt 2>&1       # Her ikisini de dosyaya
    find / -name "*.conf" &> sonuc.txt           # Kısa yazım (aynı şey)

    # stdin yönlendirme
    sort < isimler.txt                   # Dosyadan girdi al

    # Here Document (çok satırlı girdi)
    cat << EOF > yenidosya.txt
    Satır 1
    Satır 2
    Satır 3
    EOF

### Boru Hattı (Pipe)

Pipe (`|`), bir komutun çıktısını başka bir komutun girdisi olarak
kullanır:

    # Temel pipe kullanımı
    ls -la | less                                 # Çıktıyı sayfalı göster
    ls -la | wc -l                                # Satır sayısını bul
    cat /etc/passwd | grep "bash"                 # bash kullananları filtrele
    ps aux | grep httpd                           # httpd süreçlerini bul
    dmesg | tail -20                              # Son 20 kernel mesajı

    # Çoklu pipe
    cat /etc/passwd | grep "/bin/bash" | cut -d: -f1 | sort
    # 1. passwd dosyasını oku
    # 2. bash kullananları filtrele
    # 3. sadece kullanıcı adını al (: ile ayrılmış 1. alan)
    # 4. sırala

    # Pipe ile tee (hem dosyaya yaz, hem ekranda göster)
    ls -la | tee liste.txt                        # Ekran + dosya
    ls -la | tee -a liste.txt                     # Ekran + dosyaya ekle

------------------------------------------------------------------------

## 3.5 Joker Karakterler (Wildcards / Globbing)

    # * — Sıfır veya daha fazla herhangi karakter
    ls *.txt                 # .txt ile biten tüm dosyalar
    ls rapor*                # "rapor" ile başlayan tüm dosyalar
    ls *2024*                # İçinde "2024" geçen tüm dosyalar

    # ? — Tam olarak bir karakter
    ls dosya?.txt            # dosya1.txt, dosyaA.txt vb.
    ls ????                  # Tam 4 karakterli dosyalar

    # [] — Belirtilen karakterlerden biri
    ls dosya[123].txt        # dosya1.txt, dosya2.txt, dosya3.txt
    ls dosya[a-z].txt        # dosyaa.txt ... dosyaz.txt
    ls dosya[!0-9].txt       # Rakam OLMAYAN: dosyaa.txt vb.

    # {} — Virgülle ayrılmış alternatifler (Brace Expansion)
    mkdir {proje1,proje2,proje3}       # 3 dizin oluştur
    cp dosya.{txt,bak}                 # dosya.txt'yi dosya.bak olarak kopyala
    touch dosya{1..10}.txt             # dosya1.txt ... dosya10.txt
    echo {A..Z}                        # A B C ... Z

------------------------------------------------------------------------

## 3.6 Yardım Alma

### Man Sayfaları (Manual Pages)

    # Man sayfası aç
    man ls                   # ls komutunun kılavuzu
    man 5 passwd             # passwd dosyasının formatı (bölüm 5)
    man -k "disk"            # "disk" ile ilgili tüm man sayfalarını ara
    man -f ls                # ls hakkında kısa bilgi (whatis)

    # Man sayfası bölümleri:
    # 1 — Kullanıcı komutları
    # 2 — Sistem çağrıları
    # 3 — Kütüphane fonksiyonları
    # 4 — Özel dosyalar (/dev)
    # 5 — Dosya formatları (/etc/passwd gibi)
    # 6 — Oyunlar
    # 7 — Çeşitli
    # 8 — Sistem yönetim komutları

    # Man sayfasında gezinme:
    # Space / PgDn   → İleri sayfa
    # b / PgUp       → Geri sayfa
    # /ARAMA         → İleri arama
    # ?ARAMA         → Geri arama
    # n              → Sonraki sonuç
    # N              → Önceki sonuç
    # q              → Çıkış

### Diğer Yardım Kaynakları

    # --help seçeneği
    ls --help                # Kısa yardım

    # info sayfaları (daha detaylı)
    info ls

    # whatis — kısa açıklama
    whatis ls
    # ls (1) - list directory contents

    # apropos — konuya göre arama
    apropos "copy file"
    apropos network

------------------------------------------------------------------------

## 3.7 Komut Geçmişi ve Kısayollar

### Komut Geçmişi (History)

    # Geçmişi görüntüle
    history                  # Tüm geçmiş
    history 20               # Son 20 komut

    # Geçmişten çalıştır
    !!                       # Son komutu tekrar çalıştır
    sudo !!                  # Son komutu sudo ile çalıştır
    !52                      # 52 numaralı komutu çalıştır
    !find                    # "find" ile başlayan son komutu çalıştır

    # Geçmişte arama
    Ctrl + R                 # Geriye doğru arama (çok kullanışlı!)
    # (aranan kelimeyi yazın, tekrar Ctrl+R ile sonraki sonuç)

    # Geçmişi temizle
    history -c               # Mevcut oturumun geçmişini temizle

    # Geçmiş dosyası
    cat ~/.bash_history      # Kaydedilmiş geçmiş

### Bash Kısayolları

  -------------------------------------------------------------
  Kısayol                        İşlem
  ------------------------------ ------------------------------
  `Ctrl + A`                     Satır başına git

  `Ctrl + E`                     Satır sonuna git

  `Ctrl + U`                     İmleçten satır başına kadar
                                 sil

  `Ctrl + K`                     İmleçten satır sonuna kadar
                                 sil

  `Ctrl + W`                     Son kelimeyi sil

  `Ctrl + Y`                     Silinen metni yapıştır

  `Ctrl + L`                     Ekranı temizle (clear)

  `Ctrl + C`                     Çalışan komutu durdur

  `Ctrl + Z`                     Komutu arka plana al
                                 (duraksak)

  `Ctrl + D`                     Oturumu kapat (exit)

  `Tab`                          Otomatik tamamla

  `Tab Tab`                      Tüm olasılıkları göster
  -------------------------------------------------------------

> 💡 **Profesyonel İpucu:** `Tab` tuşunu sık kullanın! Komut adları,
> dosya yolları ve hatta seçenekleri otomatik tamamlar. Bu hem hızınızı
> artırır hem de yazım hatalarını önler.

------------------------------------------------------------------------

## 3.8 Ortam Değişkenleri

    # Tüm ortam değişkenlerini göster
    env
    printenv

    # Belirli bir değişkeni göster
    echo $HOME               # Ev dizini: /home/kullanici
    echo $USER               # Kullanıcı adı
    echo $SHELL              # Kullanılan kabuk
    echo $PATH               # Komut arama yolları
    echo $LANG               # Sistem dili
    echo $HOSTNAME           # Makine adı
    echo $PWD                # Mevcut çalışma dizini

    # Değişken tanımla
    ISIM="Ahmet"
    echo $ISIM

    # Ortam değişkeni olarak dışa aktar (alt süreçlere de aktarılır)
    export JAVA_HOME=/usr/lib/jvm/java-17
    export PATH=$PATH:/opt/myapp/bin

    # Kalıcı hale getir
    echo 'export JAVA_HOME=/usr/lib/jvm/java-17' >> ~/.bashrc
    source ~/.bashrc         # Değişiklikleri yükle (veya yeni terminal aç)

### PATH Değişkeni

`PATH`, kabukpun komutları aradığı dizinlerin listesidir:

    echo $PATH
    # /usr/local/bin:/usr/bin:/usr/local/sbin:/usr/sbin:/home/kullanici/.local/bin

    # PATH'e yeni dizin ekleme
    export PATH=$PATH:/opt/mytools/bin

    # Komutun hangi PATH'den geldiğini bul
    which python3
    # /usr/bin/python3
    type ls
    # ls is aliased to 'ls --color=auto'

------------------------------------------------------------------------

## 3.9 Takma Adlar (Alias)

    # Mevcut alias'ları göster
    alias

    # Alias tanımla
    alias ll='ls -la'
    alias la='ls -la'
    alias grep='grep --color=auto'
    alias rm='rm -i'                     # Silmeden önce sor
    alias cls='clear'
    alias ..='cd ..'
    alias ...='cd ../..'
    alias ports='ss -tulnp'
    alias myip='ip addr show | grep inet'

    # Alias'ı kaldır
    unalias rm

    # Kalıcı hale getir
    echo "alias ll='ls -la'" >> ~/.bashrc
    source ~/.bashrc

------------------------------------------------------------------------

## 3.10 Sık Karşılaşılan Sorunlar ve Çözümleri

### ⚠️ Sorun 1: "command not found" hatası

**Nedenler:** 1. Komut kurulu değil 2. PATH'te doğru dizin yok 3. Yazım
hatası var

**Çözüm:**

    # 1. Komutun kurulu olup olmadığını kontrol et
    which komut_adi
    # veya
    rpm -q paket_adi

    # 2. PATH'i kontrol et
    echo $PATH

    # 3. Komutun hangi pakette olduğunu bul
    sudo dnf provides "*/komut_adi"
    # Bulunan paketi kur:
    sudo dnf install paket_adi

    # 4. Tab ile doğru yazdığınızı kontrol edin

### ⚠️ Sorun 2: "Permission denied" hatası

**Çözüm:**

    # 1. Dosya izinlerini kontrol et
    ls -la dosya.sh

    # 2. Çalıştırma izni ver
    chmod +x dosya.sh

    # 3. Root yetkisi gerekiyorsa
    sudo ./dosya.sh

### ⚠️ Sorun 3: Terminal donuyor / yanıt vermiyor

**Nedenler:** - `Ctrl + S` yanlışlıkla basıldı (terminal çıktısını
durdurur) - Sonsuz döngüde bir komut çalışıyor

**Çözüm:**

    # Terminal donması
    Ctrl + Q                 # Çıktıyı devam ettir (Ctrl+S'i geri al)

    # Çalışan komutu durdurmak
    Ctrl + C                 # Komutu sonlandır
    Ctrl + Z                 # Komutu arka plana al (durdur)

### ⚠️ Sorun 4: Türkçe karakterler bozuk görünüyor

**Çözüm:**

    # Mevcut locale'i kontrol et
    locale

    # UTF-8'e ayarla
    export LANG=en_US.UTF-8
    # veya Türkçe:
    export LANG=tr_TR.UTF-8

    # Kalıcı yapmak:
    sudo localectl set-locale LANG=tr_TR.UTF-8

------------------------------------------------------------------------

## 3.11 Bölüm Özeti

Bu bölümde öğrendikleriniz: - ✅ Terminal, kabuk ve komut istemi
kavramları - ✅ Komut söz dizimi ve seçenek türleri - ✅ Temel dosya ve
dizin komutları (ls, cd, cp, mv, rm, find) - ✅ Giriş/Çıkış yönlendirme
ve pipe kullanımı - ✅ Joker karakterler (wildcards) - ✅ Yardım alma
yöntemleri (man, --help, info) - ✅ Komut geçmişi ve bash kısayolları -
✅ Ortam değişkenleri ve PATH - ✅ Alias tanımlama

**Bir sonraki bölümde:** Linux dosya sistemi hiyerarşisini ve yapısını
derinlemesine öğreneceksiniz.

# BÖLÜM 4: Dosya Sistemi ve Dizin Yapısı

------------------------------------------------------------------------

## 4.1 Linux Dosya Sistemi Hiyerarşisi (FHS)

Linux'ta her şey `/` (kök/root) dizininden başlayan tek bir ağaç
yapısındadır. Windows'taki gibi `C:`, `D:` sürücü harfleri yoktur ---
her şey `/` altında bağlama noktalarına (mount point) monte edilir.

### FHS Standart Dizin Yapısı

    /  (root — kök dizin)
    ├── bin/       → Temel kullanıcı komutları (/usr/bin'e sembolik bağ)
    ├── boot/      → Kernel ve önyükleyici dosyaları
    │   ├── grub2/           → GRUB yapılandırması
    │   ├── vmlinuz-*        → Linux kernel
    │   └── initramfs-*      → Başlangıç RAM dosya sistemi
    ├── dev/       → Aygıt dosyaları
    │   ├── sda              → İlk SCSI/SATA disk
    │   ├── sda1             → İlk diskin ilk bölümü
    │   ├── null             → Kara delik (/dev/null)
    │   ├── zero             → Sıfır kaynağı
    │   ├── random           → Rastgele veri
    │   └── tty              → Terminal aygıtları
    ├── etc/       → Sistem yapılandırma dosyaları
    │   ├── fstab            → Disk bağlama tablosu
    │   ├── passwd           → Kullanıcı bilgileri
    │   ├── shadow           → Şifrelenmiş parolalar
    │   ├── group            → Grup bilgileri
    │   ├── hostname         → Makine adı
    │   ├── hosts            → Statik DNS çözümleme
    │   ├── resolv.conf      → DNS sunucuları
    │   ├── sysconfig/       → Sistem yapılandırma alt dizini
    │   ├── systemd/         → Systemd yapılandırması
    │   ├── ssh/             → SSH yapılandırması
    │   ├── yum.repos.d/     → Paket depo tanımları
    │   └── cron.d/          → Zamanlanmış görevler
    ├── home/      → Kullanıcı ev dizinleri
    │   ├── ahmet/
    │   └── mehmet/
    ├── lib/       → Temel paylaşılan kütüphaneler (/usr/lib'e bağ)
    ├── lib64/     → 64-bit kütüphaneler (/usr/lib64'e bağ)
    ├── media/     → Çıkarılabilir medya otomatik bağlama noktası
    ├── mnt/       → Manuel bağlama noktası
    ├── opt/       → Üçüncü parti uygulamalar
    ├── proc/      → Sanal dosya sistemi (çalışan süreç bilgileri)
    │   ├── cpuinfo          → CPU bilgisi
    │   ├── meminfo          → Bellek bilgisi
    │   ├── PID/             → Her sürecin bilgileri
    │   └── sys/             → Kernel parametreleri
    ├── root/      → Root kullanıcısının ev dizini
    ├── run/       → Çalışma zamanı verileri (PID dosyaları, soketler)
    ├── sbin/      → Sistem yönetim komutları (/usr/sbin'e bağ)
    ├── srv/       → Servis verileri (web, FTP içerikleri)
    ├── sys/       → Sanal dosya sistemi (donanım/kernel bilgileri)
    ├── tmp/       → Geçici dosyalar (yeniden başlatmada silinebilir)
    ├── usr/       → Kullanıcı programları ve verileri (salt okunur)
    │   ├── bin/             → Kullanıcı komutları
    │   ├── sbin/            → Sistem yönetim komutları
    │   ├── lib/             → Kütüphaneler
    │   ├── lib64/           → 64-bit kütüphaneler
    │   ├── local/           → Elle kurulan yazılımlar
    │   ├── share/           → Paylaşılan veriler (man sayfaları vb.)
    │   └── src/             → Kaynak kodlar
    └── var/       → Değişken veriler
        ├── log/             → Log dosyaları
        │   ├── messages     → Genel sistem logları
        │   ├── secure       → Güvenlik logları
        │   ├── audit/       → Audit logları
        │   └── httpd/       → Apache logları
        ├── spool/           → Kuyruk verileri (yazıcı, posta)
        ├── cache/           → Önbellek verileri
        ├── lib/             → Değişken kütüphane verileri
        ├── tmp/             → Kalıcı geçici dosyalar
        └── www/             → Web sunucusu içerikleri

### Her Dizinin Detaylı Açıklaması

#### `/etc` --- Yapılandırma Merkezi

Tüm sistem yapılandırmaları burada tutulur. Herhangi bir servisi
yapılandırmak istiyorsanız, büyük ihtimalle `/etc` altında bir dosya
düzenlemeniz gerekecek.

    # En önemli yapılandırma dosyaları:
    cat /etc/hostname          # Makine adı
    cat /etc/os-release        # İşletim sistemi bilgisi
    cat /etc/fstab             # Disk bağlama noktaları
    cat /etc/passwd            # Kullanıcı listesi
    cat /etc/group             # Grup listesi
    cat /etc/resolv.conf       # DNS yapılandırması
    cat /etc/hosts             # Statik isim çözümleme

#### `/proc` --- Sanal Dosya Sistemi (Çalışan Sistem Bilgileri)

`/proc` diskte yer kaplamaz --- kernel tarafından anında oluşturulur:

    # Donanım bilgileri
    cat /proc/cpuinfo          # CPU detayları
    cat /proc/meminfo          # Bellek durumu
    cat /proc/version          # Kernel versiyonu
    cat /proc/partitions       # Disk bölümleri
    cat /proc/mounts           # Bağlı dosya sistemleri
    cat /proc/uptime           # Çalışma süresi (saniye)
    cat /proc/loadavg          # Sistem yükü

    # Süreç bilgileri
    ls /proc/1/                # PID 1 (systemd) bilgileri
    cat /proc/1/cmdline        # Sürecin komut satırı
    cat /proc/1/status         # Süreç durumu

#### `/dev` --- Aygıt Dosyaları

Linux'ta "her şey dosyadır" ilkesi gereği, donanımlar da dosya olarak
temsil edilir:

    # Disk aygıtları
    /dev/sda        # İlk SCSI/SATA/SAS disk
    /dev/sdb        # İkinci disk
    /dev/sda1       # İlk diskin 1. bölümü
    /dev/nvme0n1    # İlk NVMe SSD
    /dev/vda        # KVM sanal disk

    # Özel aygıtlar
    /dev/null       # Kara delik — yazılan her şey kaybolur
    /dev/zero       # Sonsuz sıfır kaynağı
    /dev/random     # Rastgele veri (yavaş, yüksek entropi)
    /dev/urandom    # Rastgele veri (hızlı)
    /dev/tty        # Mevcut terminal

    # Kullanım örnekleri:
    echo "test" > /dev/null          # Çıktıyı at
    dd if=/dev/zero of=bos.img bs=1M count=100  # 100 MB boş dosya oluştur
    dd if=/dev/urandom of=rastgele.bin bs=1M count=1  # 1 MB rastgele veri

------------------------------------------------------------------------

## 4.2 Dosya Türleri

Linux'ta 7 dosya türü vardır:

  ----------------------------------------------------------------------------
  Simge          Tür        Açıklama             Örnek
  -------------- ---------- -------------------- -----------------------------
  `-`            Normal     Metin, ikili, resim  `-rw-r--r-- rapor.txt`
                 dosya      vb.                  

  `d`            Dizin      Klasör               `drwxr-xr-x belgeler/`

  `l`            Sembolik   Kısayol (başka       `lrwxrwxrwx lib -> usr/lib`
                 bağ        dosyaya işaretçi)    

  `b`            Blok aygıt Diskler (blok blok   `brw-rw---- sda`
                            erişim)              

  `c`            Karakter   Terminaller, seri    `crw-rw-rw- null`
                 aygıt      portlar              

  `p`            Named pipe Süreçler arası       `prw-r--r-- mypipe`
                 (FIFO)     iletişim             

  `s`            Soket      Ağ/süreç iletişimi   `srwxrwxrwx mysql.sock`
  ----------------------------------------------------------------------------

    # Dosya türünü belirleme
    ls -la                   # İlk karakter türü gösterir
    file dosya.txt           # Detaylı tür bilgisi
    stat dosya.txt           # Tam inode bilgisi

------------------------------------------------------------------------

## 4.3 Bağlantılar (Links)

### Sembolik Bağlantı (Symbolic / Soft Link)

Windows'taki kısayol gibi düşünebilirsiniz. Orijinal dosyaya **işaret**
eder:

    # Sembolik bağ oluştur
    ln -s /var/log/messages /home/kullanici/loglar

    # Dosya bilgisini gör
    ls -la /home/kullanici/loglar
    # lrwxrwxrwx 1 kullanici kullanici 18 ... loglar -> /var/log/messages

**Özellikleri:** - Farklı dosya sistemlerinde çalışır - Dizinlere de bağ
oluşturulabilir - Orijinal silinirse bağ **bozulur** (dangling link) -
Kendi inode numarası vardır

### Sabit Bağlantı (Hard Link)

Diskteki veriye doğrudan ikinci bir isim verir. Aynı inode'u
paylaşırlar:

    # Sabit bağ oluştur
    ln /var/log/messages /home/kullanici/messages_kopya

    # inode numaralarını karşılaştır
    ls -li /var/log/messages /home/kullanici/messages_kopya
    # Aynı inode numarasına sahip olduklarını göreceksiniz

**Özellikleri:** - Aynı dosya sistemi içinde olmalı - Dizinlere sabit
bağ **oluşturulamaz** (root hariç) - Orijinal silinse bile veri
erişilebilir (link sayacı \> 0 olduğu sürece) - Aynı inode numarasını
paylaşır

### Karşılaştırma

    SEMBOLIK BAĞ:                     SABIT BAĞ:
    ┌──────────┐    ┌──────────┐      ┌──────────┐   ┌──────────┐
    │  Link    │───→│ Orijinal │      │ Dosya A  │   │ Dosya B  │
    │ (inode X)│    │(inode Y) │      │(inode Y) │   │(inode Y) │
    └──────────┘    └────┬─────┘      └────┬─────┘   └────┬─────┘
                         │                  │              │
                         ▼                  └──────┬───────┘
                    ┌──────────┐                   ▼
                    │  VERİ    │             ┌──────────┐
                    └──────────┘             │  VERİ    │
                                             └──────────┘

------------------------------------------------------------------------

## 4.4 Dosya Sistemleri

### Linux'ta Kullanılan Dosya Sistemleri

  ---------------------------------------------------------------------
  Dosya Sistemi   Maks Dosya  Maks Hacim  Kullanım        Özellikler
  --------------- ----------- ----------- --------------- -------------
  **XFS**         8 EB        8 EB        RHEL varsayılan Yüksek
                                                          performans,
                                                          büyük
                                                          dosyalar

  **ext4**        16 TB       1 EB        Genel amaçlı    Olgun,
                                                          güvenilir

  **ext3**        2 TB        32 TB       Eski sistemler  Journaling

  **ext2**        2 TB        32 TB       /boot           Journaling
                                          (opsiyonel)     yok

  **Btrfs**       16 EB       16 EB       Deneysel/özel   Snapshot,
                                                          sıkıştırma

  **vfat**        4 GB        2 TB        /boot/efi, USB  Windows
                                                          uyumluluk

  **swap**        ---         ---         Takas alanı     Sanal bellek
  ---------------------------------------------------------------------

> 💡 **RHEL 8/9'da varsayılan:** XFS dosya sistemi kullanılır. XFS,
> büyük dosyalar ve yüksek eşzamanlı I/O yükleri için optimize
> edilmiştir.

### Dosya Sistemi İşlemleri

    # Dosya sistemi oluştur
    sudo mkfs.xfs /dev/sdb1           # XFS formatla
    sudo mkfs.ext4 /dev/sdb2          # ext4 formatla
    sudo mkfs.vfat /dev/sdb3          # FAT32 formatla

    # Dosya sistemi bilgisi
    df -h                              # Disk kullanımı (okunabilir)
    df -Th                             # Dosya sistemi türleri dahil
    du -sh /var/log                    # Dizin boyutu
    du -sh /* 2>/dev/null | sort -rh   # Kök altı dizin boyutları (sıralı)

    # Dosya sistemi kontrolü (bağlı olmayan dosya sisteminde!)
    sudo umount /dev/sdb1
    sudo xfs_repair /dev/sdb1          # XFS onarım
    sudo fsck.ext4 /dev/sdb2           # ext4 kontrol ve onarım

    # Dosya sistemi bilgisi
    sudo xfs_info /dev/sda1            # XFS detayları
    sudo tune2fs -l /dev/sdb2          # ext4 detayları
    lsblk                              # Blok aygıtları listele
    blkid                              # UUID'leri göster

### Dosya Sistemi Bağlama (Mount)

    # Manuel bağlama
    sudo mount /dev/sdb1 /mnt/veri
    sudo mount -t ext4 /dev/sdb2 /mnt/yedek
    sudo mount -o ro /dev/sdb3 /mnt/salt_okunur    # salt okunur

    # Bağlı dosya sistemlerini göster
    mount | column -t
    findmnt
    findmnt -t xfs                    # Sadece XFS olanlar

    # Bağlamayı kaldır
    sudo umount /mnt/veri
    sudo umount -l /mnt/veri          # Lazy: meşgul olsa bile bağlamayı kaldır

    # ISO dosyası bağlama
    sudo mount -o loop rhel9.iso /mnt/iso

### /etc/fstab --- Kalıcı Bağlama

Sistem başlatıldığında otomatik bağlanan dosya sistemleri:

    # /etc/fstab formatı:
    # <cihaz/UUID>  <bağlama noktası>  <dosya sistemi>  <seçenekler>  <dump>  <pass>

    # Örnek /etc/fstab:
    UUID=abc12345-def6-7890-abcd-ef1234567890  /        xfs     defaults        0 0
    UUID=fed09876-5432-1098-fedc-ba9876543210  /boot    xfs     defaults        0 0
    UUID=11223344-5566-7788-9900-aabbccddeeff  /home    xfs     defaults        0 0
    UUID=aabbccdd-eeff-0011-2233-445566778899  swap     swap    defaults        0 0
    /dev/sdb1                                  /mnt/veri xfs    defaults        0 0

**Seçenekler açıklaması:**

  -------------------------------------------------------------
  Seçenek                        Açıklama
  ------------------------------ ------------------------------
  `defaults`                     rw, suid, dev, exec, auto,
                                 nouser, async

  `ro`                           Salt okunur

  `rw`                           Okunur-yazılır

  `noexec`                       Çalıştırılabilir dosyaları
                                 engelle (güvenlik)

  `nosuid`                       SUID bitini yoksay (güvenlik)

  `nodev`                        Aygıt dosyalarını yoksay
                                 (güvenlik)

  `noatime`                      Erişim zamanını güncelleme
                                 (performans)

  `nofail`                       Bağlanamazsa boot'u engellemez
  -------------------------------------------------------------

> ⚠️ **Kritik Uyarı:** `/etc/fstab` dosyasını düzenlerken çok dikkatli
> olun! Hatalı bir giriş, sisteminizin açılmamasına neden olabilir.
> Düzenledikten sonra mutlaka test edin:

    # fstab'ı test et (yeniden başlatmadan)
    sudo mount -a

    # Hata varsa düzeltin, yoksa devam

------------------------------------------------------------------------

## 4.5 İnode Kavramı

Her dosya ve dizinin bir **inode** (index node) numarası vardır. İnode,
dosyanın meta verilerini saklar:

    ┌─────────────────────┐
    │       İNODE         │
    ├─────────────────────┤
    │ Dosya türü          │
    │ İzinler (rwx)       │
    │ Sahip (UID)         │
    │ Grup (GID)          │
    │ Boyut               │
    │ Zaman damgaları     │
    │  ├── atime (erişim) │
    │  ├── mtime (değişim)│
    │  └── ctime (inode)  │
    │ Link sayacı         │
    │ Veri blok adresleri  │
    │  ├── Doğrudan (12)  │
    │  ├── Dolaylı (1)    │
    │  ├── Çift dolaylı   │
    │  └── Üçlü dolaylı   │
    └─────────────────────┘

> ⚠️ **Dikkat:** İnode dosyanın **adını** saklamaz! Dosya adı, dizin
> girişinde saklanır.

    # İnode numaralarını göster
    ls -i dosya.txt
    # 1234567 dosya.txt

    # inode kullanımını kontrol et
    df -i                    # Her dosya sisteminin inode kullanımı

    # inode bitti hatası:
    # "No space left on device" hatası alabilirsiniz ama disk boş görünür!
    # Çözüm: Çok sayıda küçük dosya inode'ları tüketmiş olabilir
    # Kontrol: df -i ile inode kullanımına bakın

------------------------------------------------------------------------

## 4.6 Sık Karşılaşılan Sorunlar ve Çözümleri

### ⚠️ Sorun 1: "No space left on device" --- Ama disk boş!

**Neden:** İnode'lar tükenmiş olabilir (binlerce küçük dosya).

**Teşhis ve Çözüm:**

    # Disk alanını kontrol et
    df -h
    # Eğer alan varsa ama hata alıyorsanız:

    # İnode kullanımını kontrol et
    df -i
    # IUse% %100 ise inode'lar bitmiş!

    # En çok dosya içeren dizini bul
    find / -xdev -printf '%h\n' | sort | uniq -c | sort -rn | head -20

    # Gereksiz dosyaları temizle
    find /tmp -type f -mtime +30 -delete    # 30 günden eski geçici dosyalar

### ⚠️ Sorun 2: Dosya sistemi "read-only" oluyor

**Neden:** Disk hatası algılandı, kernel güvenlik önlemi olarak
read-only'ye geçirdi.

**Çözüm:**

    # Sistem loglarını kontrol et
    dmesg | grep -i "error\|readonly\|read.only"
    journalctl -b | grep -i "i/o error"

    # Dosya sistemini kontrol ve onarım yap (gerekirse rescue modda)
    sudo umount /dev/sdb1
    sudo xfs_repair /dev/sdb1          # XFS için
    # veya
    sudo fsck -y /dev/sdb2             # ext4 için

    # Read-write olarak yeniden bağla
    sudo mount -o remount,rw /

    # Disk sağlığını kontrol et
    sudo smartctl -a /dev/sda          # SMART verileri (smartmontools gerekli)

### ⚠️ Sorun 3: `/etc/fstab` hatası nedeniyle sistem açılmıyor

**Çözüm:**

    # 1. Recovery/Rescue modda açın
    # 2. Root dosya sistemini rw olarak bağlayın
    mount -o remount,rw /

    # 3. fstab'ı düzeltin
    vi /etc/fstab

    # 4. Yeniden başlatın
    reboot

### ⚠️ Sorun 4: "Device is busy" --- umount yapılamıyor

**Neden:** Bir süreç o dosya sistemini kullanıyor.

**Çözüm:**

    # Hangi süreç kullanıyor?
    lsof +D /mnt/veri
    fuser -vm /mnt/veri

    # O süreci sonlandır veya dizinden çık
    cd /

    # Sonra umount
    sudo umount /mnt/veri

    # Son çare: lazy umount
    sudo umount -l /mnt/veri

------------------------------------------------------------------------

## 4.7 Bölüm Özeti

Bu bölümde öğrendikleriniz: - ✅ Linux FHS dizin yapısı ve her dizinin
amacı - ✅ `/proc`, `/dev`, `/sys` sanal dosya sistemleri - ✅ 7 dosya
türü - ✅ Sembolik ve sabit bağlantılar - ✅ Dosya sistemleri (XFS,
ext4) ve işlemleri - ✅ Mount/umount ve `/etc/fstab` yapılandırması - ✅
İnode kavramı - ✅ Disk ve dosya sistemi sorunları ile çözümleri

**Bir sonraki bölümde:** vi/vim metin editörünü ve metin işleme
araçlarını öğreneceksiniz.

# BÖLÜM 5: Metin Editörleri ve Metin İşleme

------------------------------------------------------------------------

## 5.1 Vi/Vim Editörü

`vi` (Visual Editor), UNIX/Linux dünyasının en güçlü ve en yaygın metin
editörüdür. `vim` (Vi IMproved) ise vi'nin geliştirilmiş versiyonudur.
Her RHEL sisteminde varsayılan olarak bulunur.

### Neden Vim Öğrenmeli?

- Her Linux/UNIX sisteminde bulunur
- SSH ile uzak sunucuda çalışırken GUI gerekmez
- RHCSA/RHCE sınavlarında vi/vim kullanılır
- Son derece hızlı düzenleme yapılabilir
- Sistem yapılandırma dosyalarını düzenlemek için standart araçtır

### Vim Modları

    ┌──────────────────────────────────────────────┐
    │                NORMAL MOD                     │
    │          (Varsayılan açılış modu)             │
    │                                              │
    │  i, a, o ──→ INSERT MOD (metin yazma)        │
    │  v, V    ──→ VISUAL MOD (seçim yapma)        │
    │  :       ──→ COMMAND MOD (komut çalıştırma)  │
    │  /       ──→ SEARCH (arama)                  │
    │  R       ──→ REPLACE MOD (üzerine yazma)     │
    │                                              │
    │  Tüm modlardan ESC ile Normal Mod'a dönülür  │
    └──────────────────────────────────────────────┘

### Vim'i Açma ve Kapatma

    vim dosya.txt                  # Dosyayı aç (yoksa oluşturur)
    vim +50 dosya.txt              # 50. satırda aç
    vim +/arama dosya.txt          # "arama" kelimesinin olduğu satırda aç
    vim -R dosya.txt               # Salt okunur modda aç
    view dosya.txt                 # Salt okunur modda aç (aynı şey)

    # Kaydetme ve çıkış (Command modda — : ile girin)
    :w                             # Kaydet
    :q                             # Çık (değişiklik yoksa)
    :wq                            # Kaydet ve çık
    :x                             # Kaydet ve çık (wq ile aynı)
    ZZ                             # Kaydet ve çık (Normal modda)
    :q!                            # Kaydetmeden çık (değişiklikleri at)
    :wq!                           # Zorla kaydet ve çık (izin yoksa bile)
    :w yeni_dosya.txt              # Farklı adla kaydet

### Normal Mod Komutları

#### İmleç Hareketi

  -------------------------------------------------------------
  Komut                          İşlem
  ------------------------------ ------------------------------
  `h`                            Sol

  `j`                            Aşağı

  `k`                            Yukarı

  `l`                            Sağ

  `w`                            Sonraki kelime başı

  `b`                            Önceki kelime başı

  `e`                            Kelime sonu

  `0`                            Satır başı

  `$`                            Satır sonu

  `^`                            İlk boşluk olmayan karakter

  `gg`                           Dosya başı

  `G`                            Dosya sonu

  `50G` veya `:50`               50\. satıra git

  `Ctrl+f`                       Bir sayfa ileri

  `Ctrl+b`                       Bir sayfa geri

  `Ctrl+d`                       Yarım sayfa ileri

  `Ctrl+u`                       Yarım sayfa geri

  `H`                            Ekranın üstüne git

  `M`                            Ekranın ortasına git

  `L`                            Ekranın altına git
  -------------------------------------------------------------

#### Ekleme (Insert Moda Geçiş)

  -------------------------------------------------------------
  Komut                          İşlem
  ------------------------------ ------------------------------
  `i`                            İmleçten önce ekle

  `I`                            Satır başında ekle

  `a`                            İmleçten sonra ekle

  `A`                            Satır sonunda ekle

  `o`                            Altına yeni satır aç

  `O`                            Üstüne yeni satır aç
  -------------------------------------------------------------

#### Silme

  -------------------------------------------------------------
  Komut                          İşlem
  ------------------------------ ------------------------------
  `x`                            İmleç altındaki karakteri sil

  `X`                            İmleçten önceki karakteri sil

  `dd`                           Satırı sil

  `5dd`                          5 satır sil

  `dw`                           Kelimeyi sil

  `d$` veya `D`                  Satır sonuna kadar sil

  `d0`                           Satır başına kadar sil

  `dgg`                          Dosya başına kadar sil

  `dG`                           Dosya sonuna kadar sil
  -------------------------------------------------------------

#### Kopyalama ve Yapıştırma

  -------------------------------------------------------------
  Komut                          İşlem
  ------------------------------ ------------------------------
  `yy`                           Satırı kopyala (yank)

  `5yy`                          5 satır kopyala

  `yw`                           Kelimeyi kopyala

  `y$`                           Satır sonuna kadar kopyala

  `p`                            İmleçten sonra yapıştır

  `P`                            İmleçten önce yapıştır
  -------------------------------------------------------------

#### Geri Alma ve Tekrar

  -------------------------------------------------------------
  Komut                          İşlem
  ------------------------------ ------------------------------
  `u`                            Geri al (undo)

  `Ctrl+r`                       İleri al (redo)

  `.`                            Son komutu tekrar et
  -------------------------------------------------------------

#### Arama ve Değiştirme

    # Arama
    /aranacak_kelime            # İleri arama
    ?aranacak_kelime            # Geri arama
    n                           # Sonraki sonuç
    N                           # Önceki sonuç
    *                           # İmleç altındaki kelimeyi ileri ara
    #                           # İmleç altındaki kelimeyi geri ara

    # Değiştirme (Command modda)
    :s/eski/yeni/               # Satırdaki ilk eşleşmeyi değiştir
    :s/eski/yeni/g              # Satırdaki tüm eşleşmeleri değiştir
    :%s/eski/yeni/g             # Tüm dosyada değiştir
    :%s/eski/yeni/gc            # Tüm dosyada değiştir (onay iste)
    :10,20s/eski/yeni/g         # 10-20. satırlar arasında değiştir

### Vim Yapılandırması

    # ~/.vimrc dosyası oluşturun
    cat > ~/.vimrc << 'EOF'
    " Satır numaralarını göster
    set number

    " Söz dizimi renklendirme
    syntax on

    " Otomatik girinti
    set autoindent
    set smartindent

    " Tab genişliği
    set tabstop=4
    set shiftwidth=4
    set expandtab

    " Arama ayarları
    set ignorecase        " Büyük/küçük harf duyarsız
    set smartcase         " Büyük harf varsa duyarlı
    set hlsearch          " Sonuçları vurgula
    set incsearch         " Yazarken ara

    " İmleç satırını vurgula
    set cursorline

    " Durum satırını her zaman göster
    set laststatus=2

    " Renk şeması
    colorscheme desert
    EOF

------------------------------------------------------------------------

## 5.2 Nano Editörü

Vi'ye alternatif, daha kolay bir editör:

    nano dosya.txt

    # Temel kısayollar (^ = Ctrl):
    # Ctrl + O    → Kaydet
    # Ctrl + X    → Çık
    # Ctrl + K    → Satırı kes
    # Ctrl + U    → Yapıştır
    # Ctrl + W    → Ara
    # Ctrl + \    → Bul ve değiştir
    # Ctrl + G    → Yardım
    # Alt + U     → Geri al

> 💡 **İpucu:** Nano daha kolay öğrenilir, ancak vi/vim bilmeniz gerekir
> çünkü her sunucuda varsayılan olarak bulunur ve RHCSA sınavında vi
> kullanılır.

------------------------------------------------------------------------

## 5.3 Metin İşleme Araçları

### grep --- Metin Arama

    # Temel kullanım
    grep "kelime" dosya.txt                    # Eşleşen satırları göster
    grep -i "kelime" dosya.txt                 # Büyük/küçük harf duyarsız
    grep -n "kelime" dosya.txt                 # Satır numarası ile
    grep -c "kelime" dosya.txt                 # Eşleşen satır sayısı
    grep -v "kelime" dosya.txt                 # Eşleşmeyenleri göster
    grep -r "kelime" /etc/                     # Dizinde recursive arama
    grep -l "kelime" /etc/*.conf               # Dosya adlarını göster
    grep -w "test" dosya.txt                   # Tam kelime eşleşmesi

    # Düzenli ifadeler
    grep "^root" /etc/passwd                   # "root" ile başlayan satırlar
    grep "bash$" /etc/passwd                   # "bash" ile biten satırlar
    grep "^$" dosya.txt                        # Boş satırlar
    grep -E "hata|hata" log.txt               # VEYA eşleşme (egrep)
    grep -E "[0-9]{3}\.[0-9]{3}" dosya.txt     # IP benzeri desen

    # Pratik örnekler
    grep -r "error" /var/log/                  # Log dosyalarında hata arama
    grep "Failed" /var/log/secure              # Başarısız giriş denemeleri
    grep -c "GET" /var/log/httpd/access_log    # Web istek sayısı
    dmesg | grep -i "error"                    # Kernel hatalarını bulma
    ps aux | grep httpd                        # httpd süreçlerini bulma

### sed --- Akış Editörü (Stream Editor)

    # Metin değiştirme
    sed 's/eski/yeni/' dosya.txt               # İlk eşleşmeyi değiştir
    sed 's/eski/yeni/g' dosya.txt              # Tüm eşleşmeleri değiştir
    sed -i 's/eski/yeni/g' dosya.txt           # Dosyayı yerinde değiştir
    sed -i.bak 's/eski/yeni/g' dosya.txt       # Yedek oluşturup değiştir

    # Satır işlemleri
    sed -n '5p' dosya.txt                      # 5. satırı göster
    sed -n '5,10p' dosya.txt                   # 5-10. satırları göster
    sed '5d' dosya.txt                         # 5. satırı sil
    sed '/desen/d' dosya.txt                   # Eşleşen satırları sil
    sed '/^#/d' dosya.txt                      # Yorum satırlarını sil
    sed '/^$/d' dosya.txt                      # Boş satırları sil

    # Satır ekleme
    sed '3a\Yeni satır' dosya.txt              # 3. satırdan sonra ekle
    sed '3i\Yeni satır' dosya.txt              # 3. satırdan önce ekle

    # Pratik örnekler
    # SSH root girişini kapatma
    sed -i 's/^PermitRootLogin yes/PermitRootLogin no/' /etc/ssh/sshd_config

    # IP adresi değiştirme
    sed -i 's/192.168.1.100/192.168.1.200/g' /etc/sysconfig/network-scripts/ifcfg-ens192

    # Yorum satırlarını kaldırma
    sed -i 's/^#Port 22/Port 2222/' /etc/ssh/sshd_config

### awk --- Metin İşleme Dili

    # Temel kullanım (sütun bazlı işleme)
    awk '{print $1}' dosya.txt                 # 1. sütunu yazdır
    awk '{print $1, $3}' dosya.txt             # 1. ve 3. sütunu yazdır
    awk -F: '{print $1}' /etc/passwd           # : ile ayrılmış 1. alan

    # Koşullu işleme
    awk '$3 > 1000 {print $1}' /etc/passwd     # UID > 1000 olan kullanıcılar
    awk -F: '$7 ~ /bash/ {print $1}' /etc/passwd  # bash kullananlar
    awk '/error/ {print}' log.txt              # "error" içeren satırlar

    # Hesaplama
    awk '{sum += $5} END {print sum}' dosya.txt    # 5. sütun toplamı
    awk 'END {print NR}' dosya.txt                 # Toplam satır sayısı
    df -h | awk '$5+0 > 80 {print $1, $5}'        # %80'den fazla dolu diskler

    # Formatlı çıktı
    awk -F: 'BEGIN {printf "%-20s %-10s\n", "KULLANICI", "KABUK"} {printf "%-20s %-10s\n", $1, $7}' /etc/passwd

### cut, sort, uniq, wc --- Yardımcı Araçlar

    # cut — sütun kesme
    cut -d: -f1 /etc/passwd                    # 1. alan
    cut -d: -f1,7 /etc/passwd                  # 1. ve 7. alan
    cut -c1-10 dosya.txt                       # İlk 10 karakter

    # sort — sıralama
    sort dosya.txt                             # Alfabetik sırala
    sort -r dosya.txt                          # Ters sırala
    sort -n dosya.txt                          # Sayısal sırala
    sort -t: -k3 -n /etc/passwd               # 3. alana göre sayısal sırala
    sort -u dosya.txt                          # Tekrarları kaldırarak sırala

    # uniq — tekrar eden satırları işle (sıralı veri gerektirir!)
    sort dosya.txt | uniq                      # Tekrarları kaldır
    sort dosya.txt | uniq -c                   # Tekrar sayısıyla göster
    sort dosya.txt | uniq -d                   # Sadece tekrar edenleri göster

    # wc — sayma
    wc dosya.txt                               # satır, kelime, byte
    wc -l dosya.txt                            # Sadece satır sayısı
    wc -w dosya.txt                            # Kelime sayısı
    wc -c dosya.txt                            # Byte sayısı
    ls -la | wc -l                             # Dizindeki dosya sayısı

### Pratik Metin İşleme Senaryoları

    # Senaryo 1: En çok erişilen URL'leri bul (Apache log)
    awk '{print $7}' /var/log/httpd/access_log | sort | uniq -c | sort -rn | head -10

    # Senaryo 2: Başarısız SSH giriş denemelerinin IP adresleri
    grep "Failed password" /var/log/secure | awk '{print $(NF-3)}' | sort | uniq -c | sort -rn

    # Senaryo 3: En büyük 10 dosyayı bul
    find / -type f -exec du -h {} + 2>/dev/null | sort -rh | head -10

    # Senaryo 4: disk kullanımı %90'ın üzerinde olan bölümleri uyar
    df -h | awk '$5+0 > 90 {print "UYARI: " $1 " %" $5 " dolu!"}'

    # Senaryo 5: /etc/passwd'den kullanıcı listesi oluştur
    awk -F: '$3 >= 1000 && $7 != "/sbin/nologin" {printf "Kullanıcı: %-15s UID: %s\n", $1, $3}' /etc/passwd

------------------------------------------------------------------------

## 5.4 Sık Karşılaşılan Sorunlar ve Çözümleri

### ⚠️ Sorun 1: Vim'de Insert moddan çıkamıyorum

**Çözüm:** `Esc` tuşuna basın. Birden fazla `Esc` basabilirsiniz (zararı
olmaz). Eğer çalışmıyorsa `Ctrl + [` deneyin.

### ⚠️ Sorun 2: Vim'de swap dosyası uyarısı

    E325: ATTENTION
    Found a swap file by the name ".dosya.txt.swp"

**Neden:** Dosya daha önce açıkken düzgün kapatılmamış (çökme, SSH
kopması vb.)

**Çözüm:**

    # Kurtarma yapın
    vim -r dosya.txt

    # Swap dosyasını silin
    rm .dosya.txt.swp

### ⚠️ Sorun 3: sed ile yaptığım değişiklik kayboldu

**Neden:** `-i` parametresi kullanılmadı.

**Çözüm:**

    # Yanlış (ekrana yazar, dosyayı değiştirmez):
    sed 's/eski/yeni/' dosya.txt

    # Doğru (dosyayı yerinde değiştirir):
    sed -i 's/eski/yeni/' dosya.txt

    # Güvenli (yedekle ve değiştir):
    sed -i.bak 's/eski/yeni/' dosya.txt

------------------------------------------------------------------------

## 5.5 Bölüm Özeti

Bu bölümde öğrendikleriniz: - ✅ Vi/Vim modları, komutları ve
yapılandırması - ✅ Nano editörü - ✅ grep ile metin arama - ✅ sed ile
metin düzenleme - ✅ awk ile sütun bazlı veri işleme - ✅ cut, sort,
uniq, wc yardımcı araçları - ✅ Gerçek dünya metin işleme senaryoları

**Bir sonraki bölümde:** Kullanıcı ve grup yönetimini öğreneceksiniz.

# BÖLÜM 6: Kullanıcı ve Grup Yönetimi

------------------------------------------------------------------------

## 6.1 Kullanıcı Hesapları

### Kullanıcı Türleri

  -----------------------------------------------------------------------
  Tür               UID Aralığı            Açıklama          Örnek
  ----------------- ---------------------- ----------------- ------------
  **root**          0                      Süper kullanıcı,  `root`
                                           tüm yetkilere     
                                           sahip             

  **Sistem          1-999                  Servisler için    `apache`,
  kullanıcıları**                          oluşturulmuş,     `mysql`,
                                           giriş yapamaz     `sshd`

  **Normal          1000+                  İnsan             `ahmet`,
  kullanıcılar**                           kullanıcılar      `ayse`
  -----------------------------------------------------------------------

### Kullanıcı Bilgi Dosyaları

#### `/etc/passwd` --- Kullanıcı Bilgileri

    cat /etc/passwd
    # root:x:0:0:root:/root:/bin/bash
    #   │   │ │ │  │     │        │
    #   │   │ │ │  │     │        └── Kabuk (shell)
    #   │   │ │ │  │     └─────────── Ev dizini
    #   │   │ │ │  └───────────────── Açıklama (GECOS)
    #   │   │ │ └──────────────────── GID (Birincil grup)
    #   │   │ └────────────────────── UID (Kullanıcı ID)
    #   │   └──────────────────────── x = parola /etc/shadow'da
    #   └──────────────────────────── Kullanıcı adı

#### `/etc/shadow` --- Parola Bilgileri (Sadece root okuyabilir)

    sudo cat /etc/shadow
    # ahmet:$6$abc123...:19500:0:99999:7:::
    #   │        │          │   │   │    │
    #   │        │          │   │   │    └── Uyarıdan sonra hesap kilitleme
    #   │        │          │   │   └────── Değiştirme uyarısı (7 gün önce)
    #   │        │          │   └────────── Maksimum parola ömrü (99999 = sınırsız)
    #   │        │          └────────────── Son değişiklik (epoch günü)
    #   │        └───────────────────────── Şifreli parola ($6$ = SHA-512)
    #   └────────────────────────────────── Kullanıcı adı

#### `/etc/group` --- Grup Bilgileri

    cat /etc/group
    # wheel:x:10:ahmet,mehmet
    #   │   │  │      │
    #   │   │  │      └── Grup üyeleri
    #   │   │  └───────── GID (Grup ID)
    #   │   └──────────── Parola (genellikle boş)
    #   └──────────────── Grup adı

------------------------------------------------------------------------

## 6.2 Kullanıcı İşlemleri

### Kullanıcı Oluşturma

    # Temel kullanıcı oluşturma
    sudo useradd ahmet

    # Detaylı kullanıcı oluşturma
    sudo useradd -m -d /home/ahmet -s /bin/bash -c "Ahmet Yilmaz" -G wheel,developers ahmet
    # -m: Ev dizini oluştur
    # -d: Ev dizini yolunu belirle
    # -s: Kabuk belirle
    # -c: Açıklama (tam isim)
    # -G: Ek gruplar (virgülle ayrılmış)
    # -g: Birincil grup
    # -u: UID belirle
    # -e: Hesap son kullanma tarihi (YYYY-MM-DD)

    # Parola belirleme
    sudo passwd ahmet
    # Yeni UNIX parolası: ****
    # Parolayı yeniden girin: ****

    # Sistem kullanıcısı oluşturma (servisler için)
    sudo useradd -r -s /sbin/nologin -d /var/lib/myapp myapp_user
    # -r: Sistem kullanıcısı (UID < 1000)
    # -s /sbin/nologin: Oturum açamaz

### Kullanıcı Değiştirme

    # Kabuk değiştir
    sudo usermod -s /bin/zsh ahmet

    # Ev dizini değiştir (dosyaları taşıyarak)
    sudo usermod -m -d /home/ahmet_yeni ahmet

    # Gruba ekle (mevcut grupları koruyarak!)
    sudo usermod -aG docker ahmet
    # -a: Append (ekle, mevcut grupları kaldırma)
    # ⚠️ -a olmadan -G kullanırsanız, diğer tüm gruplardan çıkarılır!

    # Kullanıcıyı kilitle
    sudo usermod -L ahmet

    # Kullanıcının kilidini aç
    sudo usermod -U ahmet

    # Hesap son kullanma tarihi belirle
    sudo usermod -e 2026-12-31 ahmet

    # Kullanıcı adını değiştir
    sudo usermod -l yeni_isim eski_isim

### Kullanıcı Silme

    # Kullanıcıyı sil (ev dizini kalır)
    sudo userdel ahmet

    # Kullanıcıyı ev diziniyle birlikte sil
    sudo userdel -r ahmet
    # ⚠️ Dikkat: Bu işlem geri alınamaz!

    # Önce kontrol edin:
    sudo find / -user ahmet 2>/dev/null     # Bu kullanıcıya ait dosyalar

### Kullanıcı Bilgileri Sorgulama

    id ahmet                   # UID, GID ve gruplar
    id                         # Mevcut kullanıcının bilgileri
    whoami                     # Mevcut kullanıcı adı
    who                        # Sistemde oturum açmış kullanıcılar
    w                          # Kullanıcılar + ne yapıyorlar
    last                       # Son oturum açma geçmişi
    lastlog                    # Tüm kullanıcıların son girişi
    finger ahmet               # Kullanıcı detayları (finger paketi gerekli)

------------------------------------------------------------------------

## 6.3 Grup İşlemleri

    # Grup oluştur
    sudo groupadd developers
    sudo groupadd -g 5000 dbadmin     # GID belirleyerek

    # Gruba kullanıcı ekle
    sudo usermod -aG developers ahmet
    sudo gpasswd -a mehmet developers  # Alternatif yöntem

    # Gruptan kullanıcı çıkar
    sudo gpasswd -d mehmet developers

    # Grubu sil
    sudo groupdel developers

    # Kullanıcının gruplarını göster
    groups ahmet
    id -Gn ahmet

    # Grubun üyelerini göster
    getent group developers

------------------------------------------------------------------------

## 6.4 Parola Politikaları

### Parola Yaşlandırma (Password Aging)

    # Parola yaşlandırma bilgisini göster
    sudo chage -l ahmet

    # Parola politikası ayarla
    sudo chage -M 90 ahmet          # Maksimum 90 gün geçerli
    sudo chage -m 7 ahmet           # En az 7 gün kullanılmak zorunda
    sudo chage -W 14 ahmet          # 14 gün önce uyarı ver
    sudo chage -I 5 ahmet           # Süresi dolduktan 5 gün sonra kilitle
    sudo chage -E 2026-12-31 ahmet  # Hesap son kullanma tarihi

    # İlk girişte parola değiştirmeye zorla
    sudo chage -d 0 ahmet

    # Parola yaşlandırma varsayılanları
    cat /etc/login.defs
    # PASS_MAX_DAYS   90      # Maksimum parola ömrü
    # PASS_MIN_DAYS   7       # Minimum parola ömrü
    # PASS_MIN_LEN    8       # Minimum parola uzunluğu
    # PASS_WARN_AGE   14      # Uyarı günü

### Parola Kalitesi Politikası (PAM)

    # Parola karmaşıklık kuralları
    sudo vim /etc/security/pwquality.conf

    # Önerilen ayarlar:
    minlen = 12              # Minimum 12 karakter
    dcredit = -1             # En az 1 rakam
    ucredit = -1             # En az 1 büyük harf
    lcredit = -1             # En az 1 küçük harf
    ocredit = -1             # En az 1 özel karakter
    maxrepeat = 3            # Aynı karakter en fazla 3 kez tekrarlanabilir
    maxclassrepeat = 4       # Aynı sınıftan en fazla 4 karakter
    retry = 3                # 3 deneme hakkı

------------------------------------------------------------------------

## 6.5 sudo ve su

### su --- Kullanıcı Değiştirme

    su - ahmet               # ahmet olarak oturum aç (ortamını da yükle)
    su ahmet                  # ahmet olarak oturum aç (mevcut ortamda)
    su -                      # root olarak oturum aç
    exit                      # Önceki kullanıcıya dön

> ⚠️ **Fark:** `su -` ortam değişkenlerini yeniden yükler (login shell),
> `su` mevcut ortamı korur. Sunucu yönetiminde `su -` tercih edin.

### sudo --- Yetkili Komut Çalıştırma

    sudo dnf update                      # Tek komutu root olarak çalıştır
    sudo -i                              # root shell aç
    sudo -u apache cat /var/www/html/index.html  # apache kullanıcısı olarak çalıştır
    sudo -l                              # İzinlerinizi görüntüle

### sudoers Yapılandırması

    # sudoers dosyasını GÜVENLE düzenle
    sudo visudo

    # ASLA doğrudan /etc/sudoers'ı düzenlemeyin!
    # visudo söz dizimi kontrolü yapar!

`/etc/sudoers` dosyası:

    # Temel format:
    # KIM    NEREDEN = (KIM_OLARAK)  HANGI_KOMUTLAR

    # Örnekler:
    root    ALL=(ALL)       ALL                 # root herşeyi yapabilir
    %wheel  ALL=(ALL)       ALL                 # wheel grubundakiler herşeyi yapabilir
    ahmet   ALL=(ALL)       NOPASSWD: ALL       # ahmet parolasız herşeyi yapabilir (güvensiz!)
    mehmet  ALL=(ALL)       /usr/bin/systemctl restart httpd  # Sadece httpd restart
    ayse    ALL=(ALL)       /usr/bin/dnf, /usr/bin/systemctl  # Belirli komutlar

    # Alias tanımlama (daha düzenli)
    Cmnd_Alias WEB_CMDS = /usr/bin/systemctl restart httpd, /usr/bin/systemctl status httpd
    User_Alias WEB_ADMINS = ahmet, mehmet
    WEB_ADMINS ALL=(ALL)  WEB_CMDS

> 💡 **En İyi Pratik:** `/etc/sudoers.d/` dizinine ayrı dosyalar
> oluşturun:

    sudo visudo -f /etc/sudoers.d/web_admins

------------------------------------------------------------------------

## 6.6 Sık Karşılaşılan Sorunlar ve Çözümleri

### ⚠️ Sorun 1: "ahmet is not in the sudoers file"

**Neden:** Kullanıcı `wheel` grubunda değil.

**Çözüm:**

    # root olarak giriş yapın
    su -

    # wheel grubuna ekleyin
    usermod -aG wheel ahmet

    # Kullanıcının yeni oturumu başlatması gerekir
    # (veya: su - ahmet)

### ⚠️ Sorun 2: Kullanıcı oturum açamıyor

**Olası Nedenler ve Çözümler:**

    # 1. Hesap kilitli mi?
    sudo passwd -S ahmet
    # ahmet LK ... → "LK" = Kilitli
    sudo passwd -u ahmet     # Kilidi aç

    # 2. Kabuk /sbin/nologin mi?
    grep ahmet /etc/passwd
    # Kabuk /sbin/nologin veya /bin/false ise giriş yapılamaz
    sudo usermod -s /bin/bash ahmet

    # 3. Hesap süresi dolmuş mu?
    sudo chage -l ahmet
    # Account expires alanını kontrol edin

    # 4. Parola süresi dolmuş mu?
    sudo chage -l ahmet
    # Password expires alanını kontrol edin

    # 5. /etc/security/access.conf'ta kısıtlama var mı?
    cat /etc/security/access.conf

### ⚠️ Sorun 3: "usermod -G" kullanıcıyı diğer gruplardan çıkardı

**Neden:** `-a` (append) parametresi kullanılmadı.

**Çözüm:**

    # Yanlış (mevcut gruplardan çıkarır!):
    sudo usermod -G yenigroup ahmet

    # Doğru (mevcut gruplara ekler):
    sudo usermod -aG yenigroup ahmet

### ⚠️ Sorun 4: Root parolasını unuttuğunuzda

**Çözüm (Rescue Mode):**

    # 1. Sistemi yeniden başlatın
    # 2. GRUB menüsünde 'e' tuşuna basın
    # 3. "linux" satırının sonuna "rd.break" ekleyin
    # 4. Ctrl+X ile başlatın
    # 5. Switch root:
    switch_root:/# mount -o remount,rw /sysroot
    switch_root:/# chroot /sysroot
    sh-4.4# passwd root
    # Yeni parola girin
    sh-4.4# touch /.autorelabel    # SELinux etiketlerini yeniden oluştur
    sh-4.4# exit
    switch_root:/# exit
    # Sistem yeniden başlar

------------------------------------------------------------------------

## 6.7 Bölüm Özeti

Bu bölümde öğrendikleriniz: - ✅ Kullanıcı türleri ve ilgili dosyalar
(`/etc/passwd`, `/etc/shadow`, `/etc/group`) - ✅ Kullanıcı oluşturma,
değiştirme ve silme - ✅ Grup yönetimi - ✅ Parola politikaları ve
yaşlandırma - ✅ su ve sudo kullanımı, sudoers yapılandırması - ✅
Kullanıcı hesabı sorunlarını giderme

**Bir sonraki bölümde:** Dosya izinleri ve sahiplik konularını
derinlemesine öğreneceksiniz.

# BÖLÜM 7: Dosya İzinleri ve Sahiplik

------------------------------------------------------------------------

## 7.1 Temel İzin Sistemi

### İzin Alanları

    ls -la dosya.txt
    # -rw-r--r--  1  ahmet  developers  1024  Feb 15 12:00  dosya.txt
    #  │││││││││  │   │        │          │       │            │
    #  │││││││││  │   │        │          │       │            └─ Dosya adı
    #  │││││││││  │   │        │          │       └────────────── Değişiklik zamanı
    #  │││││││││  │   │        │          └────────────────────── Boyut
    #  │││││││││  │   │        └───────────────────────────────── Grup sahip
    #  │││││││││  │   └────────────────────────────────────────── Kullanıcı sahip
    #  │││││││││  └────────────────────────────────────────────── Link sayısı
    #  ││││││││└── Diğerleri: çalıştır
    #  │││││││└─── Diğerleri: yaz
    #  ││││││└──── Diğerleri: oku
    #  │││││└───── Grup: çalıştır
    #  ││││└────── Grup: yaz
    #  │││└─────── Grup: oku
    #  ││└──────── Sahip: çalıştır
    #  │└───────── Sahip: yaz
    #  └────────── Sahip: oku
    # İlk karakter: dosya türü (- = dosya, d = dizin, l = link)

### İzin Değerleri

    ┌──────────────────────────────────────────────┐
    │  İZİNLER                                     │
    │                                              │
    │  r (read)    = 4   → Okuma izni              │
    │  w (write)   = 2   → Yazma izni              │
    │  x (execute) = 1   → Çalıştırma izni         │
    │  - (yok)     = 0   → İzin yok                │
    │                                              │
    │  Toplam: r+w+x = 4+2+1 = 7                  │
    └──────────────────────────────────────────────┘

  --------------------------------------------------------------
  Sayısal              Sembolik             Açıklama
  -------------------- -------------------- --------------------
  0                    `---`                İzin yok

  1                    `--x`                Sadece çalıştır

  2                    `-w-`                Sadece yaz

  3                    `-wx`                Yaz + çalıştır

  4                    `r--`                Sadece oku

  5                    `r-x`                Oku + çalıştır

  6                    `rw-`                Oku + yaz

  7                    `rwx`                Tam yetki
  --------------------------------------------------------------

### Dosya vs Dizin İzinleri

  -------------------------------------------------------------
  İzin            Dosyada                Dizinde
  --------------- ---------------------- ----------------------
  `r` (read)      Dosya içeriğini okuma  Dizin içeriğini
                                         listeleme (`ls`)

  `w` (write)     Dosya içeriğini        Dizinde dosya
                  değiştirme             oluşturma/silme

  `x` (execute)   Dosyayı program olarak Dizine girme (`cd`)
                  çalıştırma             
  -------------------------------------------------------------

> ⚠️ **Önemli:** Bir dizinde `w` izni olmadan dosya oluşturamaz veya
> silemezsiniz. Bir dizinde `x` izni olmadan dizine giremez (`cd`) veya
> içindeki dosyalara erişemezsiniz.

------------------------------------------------------------------------

## 7.2 chmod --- İzin Değiştirme

### Sayısal (Octal) Yöntem

    chmod 755 script.sh          # rwxr-xr-x (sahip: tam, diğerleri: oku+çalıştır)
    chmod 644 dosya.txt          # rw-r--r-- (sahip: oku+yaz, diğerleri: sadece oku)
    chmod 600 gizli.key          # rw------- (sadece sahip okuyabilir/yazabilir)
    chmod 700 dizin/             # rwx------ (sadece sahip erişebilir)
    chmod 777 herkes.sh          # rwxrwxrwx (herkese tam yetki — GÜVENSIZ!)
    chmod 750 grupla.sh          # rwxr-x--- (sahip: tam, grup: oku+çalıştır)
    chmod 440 config.conf        # r--r----- (sahip+grup: salt okunur)

### Sembolik Yöntem

    # u = user (sahip), g = group, o = others, a = all
    # + = ekle, - = kaldır, = = ayarla

    chmod u+x script.sh          # Sahibe çalıştırma izni ekle
    chmod g+w dosya.txt          # Gruba yazma izni ekle
    chmod o-r dosya.txt          # Diğerlerinden okuma iznini kaldır
    chmod a+r dosya.txt          # Herkese okuma izni ekle
    chmod u=rwx,g=rx,o= dosya    # Sahip: rwx, Grup: r-x, Diğer: ---
    chmod go-rwx gizli.key       # Grup ve diğerlerden tüm izinleri kaldır

    # Recursive (dizindeki tüm dosyalara)
    chmod -R 755 /var/www/html/  # Alt dizinler dahil

### Yaygın İzin Şablonları

  -------------------------------------------------------------
  İzin                           Kullanım
  ------------------------------ ------------------------------
  `644`                          Normal dosyalar (oku+yaz
                                 sahip, oku diğerleri)

  `755`                          Scriptler, dizinler
                                 (çalıştır + oku herkes)

  `700`                          Özel dizinler (sadece sahip)

  `600`                          SSH anahtarları, gizli
                                 dosyalar

  `400`                          SSL sertifikaları (salt
                                 okunur)

  `775`                          Paylaşılan dizinler (grup tam
                                 yetki)
  -------------------------------------------------------------

------------------------------------------------------------------------

## 7.3 chown ve chgrp --- Sahiplik Değiştirme

    # Sahip değiştir
    sudo chown ahmet dosya.txt
    sudo chown ahmet:developers dosya.txt      # Sahip ve grup birlikte

    # Sadece grup değiştir
    sudo chgrp developers dosya.txt
    sudo chown :developers dosya.txt           # Aynı şey

    # Recursive sahiplik
    sudo chown -R www-data:www-data /var/www/html/

    # Web sunucusu örneği:
    sudo chown -R apache:apache /var/www/html/
    sudo chmod -R 755 /var/www/html/
    sudo chmod -R 644 /var/www/html/*.html

------------------------------------------------------------------------

## 7.4 Özel İzinler

### SUID (Set User ID) --- 4xxx

Dosya çalıştırıldığında, dosyanın **sahibinin** yetkileriyle çalışır
(çalıştıran kişinin değil):

    # SUID örneği:
    ls -la /usr/bin/passwd
    # -rwsr-xr-x 1 root root ... /usr/bin/passwd
    #    ^
    #    └── s = SUID aktif

    # SUID ayarlama
    chmod u+s dosya                    # SUID ekle
    chmod 4755 dosya                   # Sayısal

    # SUID dosyaları bulma (güvenlik denetimi)
    find / -type f -perm -4000 -ls 2>/dev/null

> ⚠️ **Güvenlik:** SUID root olan dosyalar potansiyel güvenlik
> riskleridir. Root yetkisiyle çalışırlar. Düzenli olarak denetleyin.

### SGID (Set Group ID) --- 2xxx

- **Dosyada:** Dosya çalıştırıldığında, dosyanın grubunun yetkileriyle
  çalışır
- **Dizinde:** Dizinde oluşturulan yeni dosyalar, dizinin grubunu miras
  alır

<!-- -->

    # SGID dizin örneği (en kullanışlı senaryo):
    sudo mkdir /srv/paylasim
    sudo chgrp developers /srv/paylasim
    sudo chmod 2775 /srv/paylasim
    # drwxrwsr-x
    #       ^
    #       └── s = SGID aktif

    # Artık bu dizinde oluşturulan tüm dosyalar
    # "developers" grubuna ait olur

### Sticky Bit --- 1xxx

Dizinde sticky bit açıksa, dosyaları sadece dosyanın sahibi veya root
silebilir. Diğer kullanıcılar yazma izni olsa bile silemez:

    # Sticky bit örneği:
    ls -ld /tmp
    # drwxrwxrwt  root root  ...  /tmp
    #          ^
    #          └── t = Sticky bit aktif

    # Sticky bit ayarlama
    chmod +t /paylasim_dizini
    chmod 1777 /paylasim_dizini

### Özel İzinler Özet Tablosu

  ---------------------------------------------------------------
  İzin         Sayısal          Dosyada          Dizinde
  ------------ ---------------- ---------------- ----------------
  **SUID**     4xxx             Sahibinin        (etkisiz)
                                yetkileriyle     
                                çalışır          

  **SGID**     2xxx             Grubun           Yeni dosyalar
                                yetkileriyle     dizinin grubunu
                                çalışır          alır

  **Sticky**   1xxx             (etkisiz)        Sadece sahip
                                                 silebilir
  ---------------------------------------------------------------

------------------------------------------------------------------------

## 7.5 ACL (Access Control Lists)

Temel Linux izin sistemi sadece sahip/grup/diğer ayrımı yapar. Daha
detaylı kontrol için **ACL** kullanılır.

    # ACL desteğini kontrol et
    mount | grep acl        # XFS'te varsayılan olarak aktif

    # ACL görüntüle
    getfacl dosya.txt

    # Kullanıcıya özel izin ver
    setfacl -m u:mehmet:rwx dosya.txt          # mehmet'e tam yetki
    setfacl -m u:ayse:r-- dosya.txt            # ayse'ye sadece okuma

    # Gruba özel izin ver
    setfacl -m g:muhasebe:rw- dosya.txt        # muhasebe grubuna oku+yaz

    # Varsayılan ACL (dizinde — yeni dosyalara uygulanır)
    setfacl -d -m u:mehmet:rwx /paylasim/      # Yeni dosyalara otomatik
    setfacl -d -m g:developers:rwx /paylasim/

    # ACL kaldır
    setfacl -x u:mehmet dosya.txt              # Belirli kuralı kaldır
    setfacl -b dosya.txt                       # Tüm ACL'leri kaldır

    # Recursive ACL
    setfacl -R -m g:developers:rwx /paylasim/  # Alt dosyalar dahil

    # ACL'li dosya
    ls -la dosya.txt
    # -rw-rwxr--+ 1 ahmet developers ...
    #           ^
    #           └── + işareti ACL olduğunu gösterir

### ACL Pratik Senaryo

Bir proje dizinini birden fazla grupla paylaşma:

    # Dizin oluştur
    sudo mkdir /srv/proje

    # Sahiplik ayarla
    sudo chown root:root /srv/proje
    sudo chmod 770 /srv/proje

    # Farklı gruplara farklı yetkiler
    sudo setfacl -m g:gelistiriciler:rwx /srv/proje
    sudo setfacl -m g:testçiler:rx /srv/proje
    sudo setfacl -m g:yoneticiler:rwx /srv/proje

    # Varsayılan ACL (yeni dosyalar için)
    sudo setfacl -d -m g:gelistiriciler:rwx /srv/proje
    sudo setfacl -d -m g:testçiler:rx /srv/proje

------------------------------------------------------------------------

## 7.6 umask --- Varsayılan İzinler

`umask`, yeni oluşturulan dosya ve dizinler için **varsayılan izinleri**
belirler.

    # Mevcut umask'ı göster
    umask
    # 0022

    # Hesaplama:
    # Dosya varsayılanı:  666 (rw-rw-rw-)
    # umask:             -022
    # Sonuç:              644 (rw-r--r--)

    # Dizin varsayılanı:  777 (rwxrwxrwx)
    # umask:             -022
    # Sonuç:              755 (rwxr-xr-x)

    # umask değiştir (geçici)
    umask 027                    # Dosya: 640, Dizin: 750

    # Kalıcı yapmak:
    echo "umask 027" >> ~/.bashrc

    # Yaygın umask değerleri:
    # 022 → Varsayılan (dosya: 644, dizin: 755)
    # 027 → Daha güvenli (dosya: 640, dizin: 750) — önerilir
    # 077 → En güvenli (dosya: 600, dizin: 700) — kişisel kullanım

------------------------------------------------------------------------

## 7.7 Sık Karşılaşılan Sorunlar ve Çözümleri

### ⚠️ Sorun 1: Web sayfası "403 Forbidden" hatası

**Neden:** İzin veya sahiplik sorunu.

    # Kontrol listesi:
    # 1. Dosya izinlerini kontrol et
    ls -la /var/www/html/
    # Dosyalar: 644, Dizinler: 755 olmalı

    # 2. Sahipliği kontrol et
    # Apache kullanıcısının okuyabilmesi gerekir
    sudo chown -R apache:apache /var/www/html/

    # 3. Üst dizinlerin x izni var mı?
    namei -l /var/www/html/sayfa.html
    # Her dizinde x izni olmalı!

    # 4. SELinux kontrol et (sonraki bölümde detaylı)
    ls -Z /var/www/html/
    sudo restorecon -Rv /var/www/html/

### ⚠️ Sorun 2: Paylaşılan dizinde dosyalar yanlış grupla oluşuyor

**Çözüm:** SGID kullanın:

    sudo chmod g+s /paylasim/
    # Artık yeni dosyalar dizinin grubunu miras alır

### ⚠️ Sorun 3: /tmp dizininde başkasının dosyasını silebiliyorum

**Çözüm:** Sticky bit ekleyin:

    sudo chmod +t /paylasim/

------------------------------------------------------------------------

## 7.8 Bölüm Özeti

Bu bölümde öğrendikleriniz: - ✅ rwx izin sistemi (sembolik ve
sayısal) - ✅ chmod, chown, chgrp komutları - ✅ SUID, SGID ve Sticky
Bit özel izinleri - ✅ ACL ile detaylı erişim kontrolü - ✅ umask ile
varsayılan izin ayarları - ✅ İzin sorunlarını teşhis ve çözme

**Bir sonraki bölümde:** DNF/YUM ile paket yönetimini öğreneceksiniz.

# BÖLÜM 8: Paket Yönetimi

------------------------------------------------------------------------

## 8.1 RPM Paketi Nedir?

**RPM (Red Hat Package Manager)** RHEL'in temel paket formatıdır. Bir
`.rpm` dosyası şunları içerir: - Derlenmiş program dosyaları -
Yapılandırma dosyaları - Bağımlılık bilgileri - Kurulum/kaldırma
betikleri - Doğrulama bilgileri (imza, checksum)

    # RPM dosya adı yapısı:
    # httpd-2.4.57-5.el9.x86_64.rpm
    #   │      │    │  │     │
    #   │      │    │  │     └── Mimari (x86_64, noarch, i686)
    #   │      │    │  └──────── Dağıtım (.el9 = RHEL 9)
    #   │      │    └─────────── Yayın numarası (release)
    #   │      └──────────────── Versiyon
    #   └─────────────────────── Paket adı

------------------------------------------------------------------------

## 8.2 DNF Paket Yöneticisi

**DNF (Dandified YUM)**, RHEL 8+'da varsayılan paket yöneticisidir.
Bağımlılıkları otomatik olarak çözer.

### Paket Arama

    # Paket ara
    dnf search httpd                     # İsim veya açıklamada ara
    dnf search all "web server"          # Tüm alanlarda ara

    # Paket bilgisi
    dnf info httpd                       # Detaylı bilgi
    dnf list installed                   # Kurulu paketler
    dnf list available                   # Kurulabilir paketler
    dnf list updates                     # Güncelleme mevcut paketler

    # Bir dosyanın hangi pakete ait olduğunu bul
    dnf provides /etc/httpd/conf/httpd.conf
    dnf provides "*/bin/dig"             # dig komutunu hangi paket sağlıyor?

### Paket Kurma

    # Paket kur
    sudo dnf install httpd               # Tek paket
    sudo dnf install httpd mariadb php   # Birden fazla paket
    sudo dnf install -y httpd            # Onay sormadan kur

    # Yerel RPM dosyasından kur (bağımlılıkları da çözer)
    sudo dnf localinstall paket.rpm
    # veya
    sudo dnf install ./paket.rpm

    # Paket grubu kur
    sudo dnf grouplist                   # Mevcut grupları listele
    sudo dnf groupinstall "Development Tools"
    sudo dnf groupinstall "Server with GUI"

### Paket Güncelleme

    # Tüm paketleri güncelle
    sudo dnf update -y

    # Belirli paketi güncelle
    sudo dnf update httpd

    # Güvenlik güncellemelerini listele
    sudo dnf updateinfo list security
    sudo dnf updateinfo list security --sec-severity Critical

    # Sadece güvenlik güncellemelerini kur
    sudo dnf update --security

    # Kernel dahil tam güncelleme
    sudo dnf update -y && sudo reboot

### Paket Kaldırma

    # Paket kaldır
    sudo dnf remove httpd

    # Bağımlılıklarıyla birlikte kaldır
    sudo dnf autoremove httpd

    # Artık kullanılmayan bağımlılıkları temizle
    sudo dnf autoremove

### Diğer DNF İşlemleri

    # Önbelleği temizle
    sudo dnf clean all
    sudo dnf makecache                   # Önbelleği yeniden oluştur

    # Geçmişi görüntüle
    sudo dnf history                     # İşlem geçmişi
    sudo dnf history info 15             # 15 numaralı işlemin detayı
    sudo dnf history undo 15             # 15 numaralı işlemi geri al

    # Paket doğrulama
    sudo dnf verify httpd               # Dosya bütünlüğünü kontrol et
    rpm -V httpd                        # RPM seviyesinde doğrulama

------------------------------------------------------------------------

## 8.3 RPM Komutları (Düşük Seviye)

DNF arka planda RPM kullanır. Bazen doğrudan RPM ile çalışmak gerekir:

    # Paket sorgulama
    rpm -qa                              # Tüm kurulu paketleri listele
    rpm -qa | grep httpd                 # httpd ile ilgili paketler
    rpm -qi httpd                        # Paket bilgisi
    rpm -ql httpd                        # Paketin dosya listesi
    rpm -qf /usr/sbin/httpd              # Dosyanın paketi
    rpm -qc httpd                        # Yapılandırma dosyaları
    rpm -qd httpd                        # Dokümantasyon dosyaları

    # RPM ile kurulum (bağımlılık çözmez!)
    sudo rpm -ivh paket.rpm              # Kur (verbose + progress)
    sudo rpm -Uvh paket.rpm              # Güncelle (yoksa kur)
    sudo rpm -e httpd                    # Kaldır

    # Doğrulama
    rpm -V httpd                         # Değişmiş dosyaları kontrol et
    # S.5....T.  c /etc/httpd/conf/httpd.conf
    # S = boyut değişmiş, 5 = MD5 değişmiş, T = zaman değişmiş, c = yapılandırma dosyası

    # GPG imza doğrulama
    rpm --import /etc/pki/rpm-gpg/RPM-GPG-KEY-redhat-release
    rpm -K paket.rpm

------------------------------------------------------------------------

## 8.4 Depo (Repository) Yönetimi

### Depo Yapılandırması

    # Aktif depoları listele
    dnf repolist
    dnf repolist all                     # Etkin+devre dışı depolar

    # Depo dosyaları
    ls /etc/yum.repos.d/

### Yeni Depo Ekleme

    # Yöntem 1: .repo dosyası oluşturma
    sudo cat > /etc/yum.repos.d/myrepo.repo << 'EOF'
    [myrepo]
    name=My Custom Repository
    baseurl=http://repo.sirket.local/rhel9/
    enabled=1
    gpgcheck=1
    gpgkey=http://repo.sirket.local/RPM-GPG-KEY-myrepo
    EOF

    # Yöntem 2: dnf config-manager
    sudo dnf config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo

    # EPEL deposunu ekle (Extra Packages for Enterprise Linux)
    sudo dnf install epel-release
    # veya
    sudo dnf install https://dl.fedoraproject.org/pub/epel/epel-release-latest-9.noarch.rpm

### Depo Etkinleştirme/Devre Dışı Bırakma

    # Depoyu devre dışı bırak
    sudo dnf config-manager --set-disabled myrepo

    # Depoyu etkinleştir
    sudo dnf config-manager --set-enabled myrepo

    # Geçici olarak belirli depodan kur
    sudo dnf install --enablerepo=epel htop

------------------------------------------------------------------------

## 8.5 Application Streams (Modüller)

RHEL 8+'da **Application Streams** (AppStream), aynı yazılımın farklı
sürümlerini paralel olarak sunmanızı sağlar:

    # Mevcut modülleri listele
    dnf module list
    dnf module list php                  # PHP modülleri

    # Modül bilgisi
    dnf module info php:8.1

    # Modül akışını etkinleştir
    sudo dnf module enable php:8.1
    sudo dnf module install php:8.1

    # Modül akışını değiştir
    sudo dnf module reset php
    sudo dnf module enable php:8.2
    sudo dnf module install php:8.2

    # Modül akışını devre dışı bırak
    sudo dnf module disable php

------------------------------------------------------------------------

## 8.6 Yerel Depo Oluşturma (Çevrimdışı Ortam)

İnternet erişimi olmayan sunucularda:

    # ISO'yu bağla
    sudo mkdir /mnt/iso
    sudo mount -o loop /path/to/rhel9.iso /mnt/iso

    # Yerel depo dosyası oluştur
    sudo cat > /etc/yum.repos.d/local.repo << 'EOF'
    [local-baseos]
    name=RHEL 9 BaseOS (Local)
    baseurl=file:///mnt/iso/BaseOS/
    enabled=1
    gpgcheck=0

    [local-appstream]
    name=RHEL 9 AppStream (Local)
    baseurl=file:///mnt/iso/AppStream/
    enabled=1
    gpgcheck=0
    EOF

    # Test
    sudo dnf clean all
    sudo dnf repolist

------------------------------------------------------------------------

## 8.7 Sık Karşılaşılan Sorunlar ve Çözümleri

### ⚠️ Sorun 1: "No match for argument: paket_adi"

**Nedenler:** 1. Paket adı yanlış yazılmış 2. Paketin bulunduğu depo
etkin değil

**Çözüm:**

    # Doğru adı arayın
    dnf search anahtar_kelime

    # Depoları kontrol edin
    dnf repolist

    # EPEL gerekli olabilir
    sudo dnf install epel-release

### ⚠️ Sorun 2: Bağımlılık çakışması

    # Mevcut bağımlılık sorunlarını temizle
    sudo dnf clean all && sudo dnf makecache

    # Bozuk bağımlılıkları düzelt
    sudo dnf distro-sync

    # Belirli bir paketi zorla kaldır (dikkatli!)
    sudo rpm -e --nodeps sorunlu_paket

### ⚠️ Sorun 3: "This system is not registered" / Abonelik sorunu

    # Abonelik durumu
    sudo subscription-manager status
    sudo subscription-manager list --consumed

    # Yeniden kayıt
    sudo subscription-manager unregister
    sudo subscription-manager register --username KULLANICI --password PAROLA
    sudo subscription-manager attach --auto

------------------------------------------------------------------------

## 8.8 Bölüm Özeti

Bu bölümde öğrendikleriniz: - ✅ RPM paket yapısı - ✅ DNF ile paket
kurma, güncelleme, kaldırma - ✅ RPM düşük seviye komutlar - ✅ Depo
yönetimi ve oluşturma - ✅ Application Streams / Modüller - ✅ Yerel
depo oluşturma - ✅ Paket yönetimi sorunlarını çözme

**Bir sonraki bölümde:** Süreç (process) yönetimini öğreneceksiniz.

# BÖLÜM 9: Süreç (Process) Yönetimi

------------------------------------------------------------------------

## 9.1 Süreç Kavramı

**Süreç (Process)**, çalışmakta olan bir programın bellek içindeki
kopyasıdır. Her sürecin benzersiz bir **PID (Process ID)** numarası
vardır.

### Süreç Hiyerarşisi

    systemd (PID 1)
    ├── sshd
    │   └── sshd (oturum)
    │       └── bash
    │           └── vim
    ├── httpd (ana süreç)
    │   ├── httpd (worker)
    │   ├── httpd (worker)
    │   └── httpd (worker)
    ├── crond
    ├── rsyslogd
    └── NetworkManager
    # Süreç ağacını görüntüle
    pstree
    pstree -p                   # PID numaralarıyla
    pstree -u                   # Kullanıcılarla

### Süreç Durumları

  --------------------------------------------------------------
  Durum                Sembol               Açıklama
  -------------------- -------------------- --------------------
  **Running**          R                    Çalışıyor veya
                                            çalışmaya hazır

  **Sleeping**         S                    Bir olayı bekliyor
                                            (uyuyor)

  **Uninterruptible    D                    I/O bekliyor
  Sleep**                                   (kesilemez)

  **Stopped**          T                    Durdurulmuş (Ctrl+Z
                                            veya sinyal)

  **Zombie**           Z                    Sonlandı ama üst
                                            süreç henüz
                                            temizlemedi
  --------------------------------------------------------------

------------------------------------------------------------------------

## 9.2 Süreç İzleme Araçları

### ps --- Anlık Süreç Durumu

    # Temel kullanım
    ps                           # Mevcut terminaldeki süreçler
    ps aux                       # TÜM süreçler (BSD formatı)
    ps -ef                       # TÜM süreçler (UNIX formatı)
    ps -u ahmet                 # Belirli kullanıcının süreçleri

    # Belirli süreçleri filtrele
    ps aux | grep httpd          # httpd süreçleri
    ps -ef | grep sshd           # sshd süreçleri
    ps aux | grep -v grep | grep httpd    # grep kendisini gizle

    # Sütun seçimi
    ps -eo pid,ppid,user,%cpu,%mem,stat,cmd --sort=-%mem | head -20
    # En çok bellek kullanan 20 süreç

    ps -eo pid,ppid,user,%cpu,%mem,stat,cmd --sort=-%cpu | head -20
    # En çok CPU kullanan 20 süreç

### top --- Gerçek Zamanlı İzleme

    top

    # top ekranı:
    #  top - 14:30:22 up 5 days, 2:15, 3 users, load average: 0.15, 0.10, 0.05
    #  Tasks: 195 total, 1 running, 194 sleeping, 0 stopped, 0 zombie
    #  %Cpu(s): 2.3 us, 0.7 sy, 0.0 ni, 96.8 id, 0.2 wa, 0.0 hi, 0.0 si
    #  MiB Mem:  7953.4 total, 3245.8 free, 2107.6 used, 2600.0 buff/cache
    #  MiB Swap: 4096.0 total, 4096.0 free,    0.0 used. 5421.2 avail Mem
    #
    #  PID USER PR NI  VIRT   RES   SHR S %CPU %MEM TIME+     COMMAND

**top içinde tuş kısayolları:**

  -------------------------------------------------------------
  Tuş                            İşlem
  ------------------------------ ------------------------------
  `1`                            Her CPU çekirdeğini ayrı
                                 göster

  `M`                            Belleğe göre sırala

  `P`                            CPU'ya göre sırala

  `T`                            Zamana göre sırala

  `k`                            Süreç öldür (PID gir)

  `r`                            Nice değerini değiştir
                                 (renice)

  `u`                            Kullanıcıya göre filtrele

  `f`                            Sütunları özelleştir

  `c`                            Tam komut satırını göster

  `H`                            Thread'leri göster

  `q`                            Çık
  -------------------------------------------------------------

### htop --- Gelişmiş top

    sudo dnf install htop
    htop

    # Renkli, fare destekli, daha kullanıcı dostu
    # F2: Ayarlar, F3: Arama, F5: Ağaç görünümü, F9: Öldür

------------------------------------------------------------------------

## 9.3 Süreç Kontrolü

### Ön Plan ve Arka Plan

    # Komutu arka planda başlat
    long_running_command &

    # Çalışan komutu arka plana al
    Ctrl + Z                     # Durdur
    bg                           # Arka planda devam et

    # Arka plan süreçlerini listele
    jobs
    # [1]+ Running    long_running_command &

    # Arka plandan ön plana getir
    fg                           # Son arka plan işini getir
    fg %1                        # 1 numaralı işi getir

    # Oturum kapansa bile çalışmaya devam etsin
    nohup long_running_command &
    # Çıktı: nohup.out dosyasına yazılır

    # Veya screen/tmux kullanın (önerilir)
    sudo dnf install tmux
    tmux                         # Yeni oturum
    # Ctrl+B, D → Oturumdan ayrıl
    tmux attach                  # Oturuma geri dön

### Sinyaller ve kill

    # Sinyaller:
    #  1  SIGHUP    → Yapılandırmayı yeniden oku (servisler için)
    #  2  SIGINT    → Ctrl+C (nazikçe durdur)
    #  9  SIGKILL   → Zorla öldür (kesin durdurma, temizlik yapmaz!)
    # 15  SIGTERM   → Düzgün sonlandır (varsayılan)
    # 18  SIGCONT   → Devam et
    # 19  SIGSTOP   → Durdur
    # 20  SIGTSTP   → Ctrl+Z

    # Süreç sonlandırma
    kill PID                     # SIGTERM (düzgün kapanma)
    kill -9 PID                  # SIGKILL (zorla öldürme — son çare!)
    kill -1 PID                  # SIGHUP (yapılandırma yeniden yükleme)

    # İsme göre öldürme
    killall httpd                # httpd adlı tüm süreçleri öldür
    pkill httpd                  # Desen eşleşmesiyle öldür
    pkill -u ahmet               # Kullanıcının tüm süreçlerini öldür

    # Sinyal listesi
    kill -l

> ⚠️ **Kurallar:** 1. Önce `kill PID` (SIGTERM) deneyin --- sürecin
> temizlik yapmasına izin verir 2. Yanıt vermezse 5-10 saniye bekleyin
> 3. Son çare olarak `kill -9 PID` (SIGKILL) kullanın

### Nice ve Renice --- Öncelik Ayarlama

    # Nice değerleri: -20 (en yüksek öncelik) → 19 (en düşük)
    # Varsayılan: 0

    # Düşük öncelikle başlat
    nice -n 10 uzun_islem                # Öncelik 10 (düşük)
    nice -n -5 onemli_islem             # Öncelik -5 (yüksek, root gerekli)

    # Çalışan sürecin önceliğini değiştir
    renice 10 -p 1234                    # PID 1234'ün önceliğini 10 yap
    renice -5 -u ahmet                  # ahmet'in tüm süreçlerini -5 yap

------------------------------------------------------------------------

## 9.4 Zamanlı Görevler

### cron --- Tekrarlayan Görevler

    # Crontab düzenle
    crontab -e                   # Kendi crontab'ını düzenle
    sudo crontab -e -u ahmet    # ahmet'in crontab'ını düzenle
    crontab -l                   # Mevcut crontab'ı listele
    crontab -r                   # Crontab'ı sil

    # Cron formatı:
    # dakika saat gün ay haftanın_günü KOMUT
    # (0-59) (0-23) (1-31) (1-12) (0-7, 0&7=Pazar)

    # Örnekler:
    # Her gün saat 02:00'de yedek al
    0 2 * * * /usr/local/bin/yedek.sh

    # Her 5 dakikada bir kontrol
    */5 * * * * /usr/local/bin/kontrol.sh

    # Hafta içi her gün 08:00'de
    0 8 * * 1-5 /usr/local/bin/rapor.sh

    # Her ayın 1'inde saat 03:00'te
    0 3 1 * * /usr/local/bin/aylik_bakım.sh

    # Her Pazar 04:00'te
    0 4 * * 0 /usr/local/bin/haftalik_temizlik.sh

    # Her 15 dakikada (08:00-17:00 arası, hafta içi)
    */15 8-17 * * 1-5 /usr/local/bin/is_saati_kontrol.sh

### Sistem cron Dosyaları

    # Sistem genelinde cron
    /etc/crontab              # Ana cron dosyası
    /etc/cron.d/              # Ek cron dosyaları
    /etc/cron.hourly/         # Saatlik çalışan scriptler
    /etc/cron.daily/          # Günlük çalışan scriptler
    /etc/cron.weekly/         # Haftalık çalışan scriptler
    /etc/cron.monthly/        # Aylık çalışan scriptler

    # Cron erişim kontrolü
    /etc/cron.allow            # İzin verilen kullanıcılar (varsa sadece bunlar)
    /etc/cron.deny             # Yasaklanan kullanıcılar

### at --- Tek Seferlik Görevler

    # Tek seferlik görev planla
    at 14:30
    > /usr/local/bin/rapor.sh
    > Ctrl+D

    # Örnekler
    echo "/usr/local/bin/temizlik.sh" | at midnight
    echo "/usr/local/bin/yedek.sh" | at now + 2 hours
    echo "reboot" | at 03:00 tomorrow

    # Planlanmış görevleri listele
    atq

    # Görevi iptal et
    atrm JOB_ID

------------------------------------------------------------------------

## 9.5 Sık Karşılaşılan Sorunlar ve Çözümleri

### ⚠️ Sorun 1: Zombie süreçler

**Neden:** Üst süreç, çocuk sürecin çıkış durumunu okumamış.

    # Zombie'leri bul
    ps aux | grep Z
    # veya
    ps -eo pid,ppid,stat,cmd | grep Z

    # Çözüm: Üst süreci yeniden başlatın veya SIGHUP gönderin
    kill -1 UST_SUREC_PID

    # Son çare: Üst süreci öldürün
    kill UST_SUREC_PID

### ⚠️ Sorun 2: Yüksek CPU kullanan süreç

    # 1. Suçluyu bul
    top                          # P ile CPU'ya göre sırala

    # 2. Detaylını incele
    ps -p PID -o pid,ppid,user,%cpu,%mem,cmd

    # 3. Gerekirse önceliğini düşür
    renice 19 -p PID

    # 4. Gerekirse sonlandır
    kill PID

### ⚠️ Sorun 3: Cron görevi çalışmıyor

    # 1. Cron servisi çalışıyor mu?
    systemctl status crond

    # 2. Cron loglarını kontrol et
    grep CRON /var/log/cron

    # 3. Script çalıştırılabilir mi?
    ls -la /path/to/script.sh
    chmod +x /path/to/script.sh

    # 4. Script'te tam yol kullanılıyor mu?
    # YANLIŞ: script.sh içinde "dnf update"
    # DOĞRU:  script.sh içinde "/usr/bin/dnf update"

    # 5. Cron ortam değişkenleri farklıdır!
    # Script'in başına ekleyin:
    #!/bin/bash
    PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin

------------------------------------------------------------------------

## 9.6 Bölüm Özeti

Bu bölümde öğrendikleriniz: - ✅ Süreç kavramı, PID, süreç hiyerarşisi -
✅ ps, top, htop ile süreç izleme - ✅ Ön plan/arka plan süreç
kontrolü - ✅ Sinyaller ve kill komutu - ✅ Nice/renice ile öncelik
ayarlama - ✅ Cron ve at ile zamanlı görevler - ✅ Zombie, yüksek CPU ve
cron sorunları çözümü

**Bir sonraki bölümde:** Systemd ile servis yönetimini öğreneceksiniz.

# BÖLÜM 10: Servis Yönetimi ve Systemd

------------------------------------------------------------------------

## 10.1 Systemd Nedir?

**Systemd**, RHEL 7'den itibaren kullanılan **init sistemi** ve **servis
yöneticisidir**. PID 1 olarak çalışır ve sistem başlatılmasından servis
yönetimine kadar birçok görevi üstlenir.

### systemctl --- Ana Yönetim Aracı

    # Servis durumu
    systemctl status httpd                # Detaylı durum
    systemctl is-active httpd             # Çalışıyor mu?
    systemctl is-enabled httpd            # Otomatik başlıyor mu?
    systemctl is-failed httpd             # Başarısız mı?

    # Servis kontrolü
    sudo systemctl start httpd            # Başlat
    sudo systemctl stop httpd             # Durdur
    sudo systemctl restart httpd          # Yeniden başlat
    sudo systemctl reload httpd           # Yapılandırmayı yeniden yükle (durmadan)
    sudo systemctl reload-or-restart httpd # reload yapabiliyorsa yap, yoksa restart

    # Otomatik başlatma
    sudo systemctl enable httpd           # Açılışta otomatik başla
    sudo systemctl disable httpd          # Otomatik başlamayı kapat
    sudo systemctl enable --now httpd     # Hem etkinleştir hem başlat

    # Servisleri listeleme
    systemctl list-units --type=service               # Yüklü servisler
    systemctl list-units --type=service --state=running # Çalışanlar
    systemctl list-unit-files --type=service           # Tüm servis dosyaları
    systemctl list-units --failed                      # Başarısız olanlar

    # Servis maskeleme (başlatılamaz hale getirme)
    sudo systemctl mask iptables          # Tamamen devre dışı bırak
    sudo systemctl unmask iptables        # Maskeyi kaldır

### Systemd Hedefleri (Targets)

Eski `runlevel` kavramının systemd karşılığı:

  ---------------------------------------------------------------
  Eski Runlevel        Systemd Target        Açıklama
  -------------------- --------------------- --------------------
  0                    `poweroff.target`     Kapatma

  1                    `rescue.target`       Kurtarma modu (tek
                                             kullanıcı)

  3                    `multi-user.target`   Çok kullanıcılı, GUI
                                             yok (sunucu)

  5                    `graphical.target`    GUI ile çok
                                             kullanıcılı

  6                    `reboot.target`       Yeniden başlatma
  ---------------------------------------------------------------

    # Mevcut hedefi göster
    systemctl get-default

    # Varsayılan hedefi değiştir
    sudo systemctl set-default multi-user.target   # GUI'siz sunucu modu
    sudo systemctl set-default graphical.target    # GUI ile açılış

    # Geçici olarak hedef değiştir
    sudo systemctl isolate rescue.target           # Kurtarma moduna geç
    sudo systemctl isolate multi-user.target       # Tekrar çok kullanıcı moda

    # Sistem kontrolü
    sudo systemctl reboot                          # Yeniden başlat
    sudo systemctl poweroff                        # Kapat
    sudo systemctl suspend                          # Uyut
    sudo systemctl hibernate                       # Hazırda beklet

### Özel Unit Dosyası Oluşturma

Kendi servisinizi systemd ile yönetebilirsiniz:

    sudo vim /etc/systemd/system/myapp.service
    [Unit]
    Description=My Custom Application
    Documentation=https://docs.example.com
    After=network.target
    Wants=network.target

    [Service]
    Type=simple
    User=myapp
    Group=myapp
    WorkingDirectory=/opt/myapp
    ExecStart=/opt/myapp/bin/myapp --config /etc/myapp/config.yml
    ExecReload=/bin/kill -HUP $MAINPID
    Restart=on-failure
    RestartSec=5
    StandardOutput=journal
    StandardError=journal

    [Install]
    WantedBy=multi-user.target
    # Unit dosyasını yükle
    sudo systemctl daemon-reload

    # Servisi başlat ve etkinleştir
    sudo systemctl enable --now myapp

    # Logları izle
    journalctl -u myapp -f

------------------------------------------------------------------------

## 10.2 Bölüm Özeti

- ✅ systemctl ile servis yönetimi (start, stop, enable, disable)
- ✅ Systemd hedefleri (targets) ve runlevel karşılıkları
- ✅ Özel unit dosyası oluşturma
- ✅ Servis maskeleme ve bağımlılık yönetimi

# BÖLÜM 11: Ağ Yapılandırması

------------------------------------------------------------------------

## 11.1 Temel Ağ Kavramları

### IP Adresleme

    IPv4 Adresi: 192.168.1.100/24

    192.168.1.100  →  11000000.10101000.00000001.01100100
    255.255.255.0  →  11111111.11111111.11111111.00000000 (Alt ağ maskesi)

    Ağ Adresi:     192.168.1.0     (İlk)
    Yayın Adresi:  192.168.1.255   (Son)
    Kullanılabilir: 192.168.1.1 — 192.168.1.254 (254 host)

    CIDR Gösterimi:
    /8   = 255.0.0.0       (16 milyon host)
    /16  = 255.255.0.0     (65,534 host)
    /24  = 255.255.255.0   (254 host)
    /30  = 255.255.255.252 (2 host — point-to-point bağlantılar)

### Önemli Ağ Dosyaları

  -----------------------------------------------------------------------
  Dosya                               Açıklama
  ----------------------------------- -----------------------------------
  `/etc/hostname`                     Makine adı

  `/etc/hosts`                        Statik isim çözümleme

  `/etc/resolv.conf`                  DNS sunucu yapılandırması

  `/etc/sysconfig/network-scripts/`   Ağ arayüzü yapılandırmaları (RHEL
                                      8-)

  `/etc/NetworkManager/`              NetworkManager yapılandırmaları
  -----------------------------------------------------------------------

------------------------------------------------------------------------

## 11.2 NetworkManager ve nmcli

RHEL'de ağ yönetimi **NetworkManager** servisi ile yapılır.

### nmcli --- Komut Satırı Ağ Yönetimi

    # Genel durum
    nmcli general status                         # Genel NetworkManager durumu
    nmcli device status                          # Ağ arayüzleri durumu
    nmcli connection show                        # Bağlantı profilleri

    # Bağlantı detayları
    nmcli connection show "Wired connection 1"   # Belirli bağlantı detayı
    nmcli device show ens192                     # Arayüz detayı

    # DHCP ile bağlantı (otomatik IP)
    sudo nmcli connection modify "Wired connection 1" ipv4.method auto
    sudo nmcli connection up "Wired connection 1"

    # Statik IP yapılandırma
    sudo nmcli connection modify "Wired connection 1" \
      ipv4.method manual \
      ipv4.addresses 192.168.1.100/24 \
      ipv4.gateway 192.168.1.1 \
      ipv4.dns "8.8.8.8,8.8.4.4" \
      ipv4.dns-search "sirket.local" \
      connection.autoconnect yes

    # Değişiklikleri uygula
    sudo nmcli connection up "Wired connection 1"

    # Yeni bağlantı oluşturma
    sudo nmcli connection add \
      type ethernet \
      con-name "sunucu-ag" \
      ifname ens192 \
      ipv4.method manual \
      ipv4.addresses 192.168.1.100/24 \
      ipv4.gateway 192.168.1.1 \
      ipv4.dns "8.8.8.8"

    # Bağlantıyı sil
    sudo nmcli connection delete "eski-baglanti"

    # Arayüzü kapat/aç
    sudo nmcli device disconnect ens192
    sudo nmcli device connect ens192

### nmtui --- Metin Tabanlı Arayüz

    sudo nmtui                  # Metin tabanlı ağ yapılandırma arayüzü
    # Menüler:
    # 1. Edit a connection      → Bağlantı düzenle
    # 2. Activate a connection   → Bağlantıyı etkinleştir
    # 3. Set system hostname     → Hostname ayarla

------------------------------------------------------------------------

## 11.3 Ağ Teşhis Araçları

    # Bağlantı testi
    ping 8.8.8.8                        # IP ile bağlantı testi
    ping -c 4 google.com                 # 4 paket gönder
    ping -I ens192 8.8.8.8               # Belirli arayüzden

    # DNS çözümleme
    nslookup google.com                  # DNS sorgusu
    dig google.com                       # Detaylı DNS sorgusu
    dig @8.8.8.8 google.com             # Belirli DNS sunucusuna sor
    host google.com                      # Basit DNS sorgusu
    getent hosts google.com              # /etc/hosts + DNS

    # Yol takibi
    traceroute 8.8.8.8                   # Paket yolunu takip et
    tracepath 8.8.8.8                    # Alternatif

    # Port kontrolü
    ss -tulnp                           # Dinlenen portlar
    ss -tulnp | grep :80                # 80 portunu kim dinliyor?
    ss -ant                             # TCP bağlantıları

    # Arayüz bilgileri
    ip addr show                         # IP adresleri
    ip addr show ens192                  # Belirli arayüz
    ip route show                        # Yönlendirme tablosu
    ip link show                         # Arayüz durumu
    ip neigh show                        # ARP tablosu

    # Ağ trafiği izleme
    sudo tcpdump -i ens192               # Tüm trafik
    sudo tcpdump -i ens192 port 80       # Sadece HTTP
    sudo tcpdump -i ens192 host 192.168.1.1 -w kayit.pcap  # Dosyaya kaydet

------------------------------------------------------------------------

## 11.4 Host Adı ve DNS Yapılandırması

    # Hostname ayarlama
    sudo hostnamectl set-hostname sunucu01.sirket.local
    hostnamectl

    # /etc/hosts mantıksal DNS
    sudo vim /etc/hosts
    # 192.168.1.100  sunucu01.sirket.local sunucu01
    # 192.168.1.101  veritabani.sirket.local dbserver

    # DNS sunucu yapılandırması
    cat /etc/resolv.conf
    # nameserver 8.8.8.8
    # nameserver 8.8.4.4
    # search sirket.local

    # DNS önceliği (/etc/nsswitch.conf)
    grep hosts /etc/nsswitch.conf
    # hosts: files dns myhostname
    # "files" = /etc/hosts önce, "dns" = DNS sunucusu sonra

------------------------------------------------------------------------

## 11.5 Sık Karşılaşılan Ağ Sorunları ve Çözümleri

### ⚠️ Sorun 1: İnternet bağlantısı yok

    # Adım adım teşhis:
    # 1. Arayüz aktif mi?
    ip link show ens192
    # state DOWN ise: sudo nmcli device connect ens192

    # 2. IP adresi var mı?
    ip addr show ens192
    # Yoksa: sudo nmcli connection up "baglanti-adi"

    # 3. Gateway'e erişim var mı?
    ping -c 3 192.168.1.1
    # Yoksa: Gateway ayarını kontrol edin

    # 4. DNS çalışıyor mu?
    ping -c 3 8.8.8.8          # IP ile çalışıyorsa ama
    ping -c 3 google.com       # İsimle çalışmıyorsa → DNS sorunu
    # Çözüm: /etc/resolv.conf'u kontrol edin

    # 5. Firewall engelliyor mu?
    sudo firewall-cmd --list-all

### ⚠️ Sorun 2: DNS çözümlemesi çok yavaş

    # /etc/resolv.conf'ta hızlı DNS sunucuları kullanın
    # Google DNS: 8.8.8.8, 8.8.4.4
    # Cloudflare: 1.1.1.1, 1.0.0.1

    # nsswitch.conf'ta DNS önceliğini kontrol edin
    # IPv6 devre dışı bırakmak hızlandırabilir:
    sudo sysctl -w net.ipv6.conf.all.disable_ipv6=1

------------------------------------------------------------------------

## 11.6 Bölüm Özeti

- ✅ IP adresleme ve alt ağ hesaplama
- ✅ nmcli/nmtui ile ağ yapılandırması
- ✅ Ağ teşhis araçları (ping, dig, ss, tcpdump)
- ✅ Hostname ve DNS yapılandırması
- ✅ Ağ bağlantı sorunlarını giderme

# BÖLÜM 12: Disk ve Depolama Yönetimi

------------------------------------------------------------------------

## 12.1 Disk Bölümleme

### Disk Bilgilerini Görüntüleme

    lsblk                                  # Blok aygıtları
    lsblk -f                               # Dosya sistemi bilgileriyle
    fdisk -l                               # Tüm diskler ve bölümler
    blkid                                  # UUID ve dosya sistemi
    cat /proc/partitions                   # Kernel'ın gördüğü bölümler

### fdisk ile MBR Bölümleme

    sudo fdisk /dev/sdb

    # Komutlar:
    # n → Yeni bölüm oluştur
    # d → Bölüm sil
    # p → Bölüm tablosunu göster
    # t → Bölüm türünü değiştir (83=Linux, 82=swap, 8e=LVM)
    # w → Değişiklikleri yaz ve çık
    # q → Kaydetmeden çık

    # Kernel'a bölüm tablosunu yeniden okut
    sudo partprobe /dev/sdb

### parted ile GPT Bölümleme

    sudo parted /dev/sdb
    (parted) mklabel gpt                    # GPT tablo oluştur
    (parted) mkpart primary xfs 0% 50%      # İlk yarısı
    (parted) mkpart primary xfs 50% 100%    # İkinci yarısı
    (parted) print                           # Tabloyu göster
    (parted) quit

    # Tek satırda:
    sudo parted /dev/sdb mkpart primary xfs 0% 100%

### MBR vs GPT

  --------------------------------------------------------------
  Özellik              MBR                  GPT
  -------------------- -------------------- --------------------
  Maksimum disk boyutu 2 TB                 9.4 ZB (sınırsız
                                            denebilir)

  Maksimum bölüm       4 birincil (veya 3+1 128
  sayısı               genişletilmiş)       

  Önyükleme            BIOS/Legacy          UEFI

  Yedekleme            Yok                  Disk sonunda yedek
                                            kopya

  **Tercih**           Eski sistemler       **Modern sistem ---
                                            GPT kullanın**
  --------------------------------------------------------------

------------------------------------------------------------------------

## 12.2 LVM (Logical Volume Manager)

### LVM Mimari

    ┌──────────────────────────────────────────────────┐
    │            Bağlama Noktaları                     │
    │   /          /home       /var        swap        │
    │   ▲           ▲           ▲           ▲          │
    │   │           │           │           │          │
    ├───┴───────────┴───────────┴───────────┴──────────┤
    │         Logical Volumes (LV)                     │
    │   lv_root    lv_home    lv_var     lv_swap       │
    ├──────────────────────────────────────────────────┤
    │              Volume Group (VG)                   │
    │                  vg_rhel                         │
    ├─────────────────────┬────────────────────────────┤
    │   Physical Volume   │    Physical Volume         │
    │     /dev/sda2       │      /dev/sdb1             │
    ├─────────────────────┼────────────────────────────┤
    │      /dev/sda       │       /dev/sdb             │
    │    (Fiziksel Disk)  │     (Fiziksel Disk)        │
    └─────────────────────┴────────────────────────────┘

### LVM Oluşturma

    # 1. Fiziksel hacim (PV) oluşturun
    sudo pvcreate /dev/sdb1
    sudo pvcreate /dev/sdc1
    sudo pvs                         # PV'leri listele
    sudo pvdisplay                   # Detaylı bilgi

    # 2. Hacim grubu (VG) oluşturun
    sudo vgcreate vg_veri /dev/sdb1 /dev/sdc1
    sudo vgs                         # VG'leri listele
    sudo vgdisplay                   # Detaylı bilgi

    # 3. Mantıksal hacim (LV) oluşturun
    sudo lvcreate -n lv_data -L 50G vg_veri        # 50 GB
    sudo lvcreate -n lv_backup -l 100%FREE vg_veri # Kalan alanın tamamı
    sudo lvs                         # LV'leri listele

    # 4. Dosya sistemi oluşturun
    sudo mkfs.xfs /dev/vg_veri/lv_data
    sudo mkfs.ext4 /dev/vg_veri/lv_backup

    # 5. Bağlayın
    sudo mkdir -p /mnt/{data,backup}
    sudo mount /dev/vg_veri/lv_data /mnt/data
    sudo mount /dev/vg_veri/lv_backup /mnt/backup

    # 6. fstab'a ekleyin (kalıcı)
    echo '/dev/vg_veri/lv_data  /mnt/data  xfs  defaults  0 0' | sudo tee -a /etc/fstab
    echo '/dev/vg_veri/lv_backup  /mnt/backup  ext4  defaults  0 0' | sudo tee -a /etc/fstab

### LVM Boyut Değiştirme

    # LV büyütme (EN SIK KULLANILAN İŞLEM)
    sudo lvextend -L +20G /dev/vg_veri/lv_data     # 20 GB ekle
    sudo lvextend -l +100%FREE /dev/vg_veri/lv_data # Tüm boş alanı ekle

    # Dosya sistemini genişlet (LV büyütüldükten sonra!)
    sudo xfs_growfs /mnt/data                       # XFS için
    sudo resize2fs /dev/vg_veri/lv_backup            # ext4 için

    # Tek komutla hem LV hem dosya sistemi büyüt:
    sudo lvextend -r -L +20G /dev/vg_veri/lv_data   # -r = resize otomatik

    # VG'ye yeni disk ekleme
    sudo pvcreate /dev/sdd1
    sudo vgextend vg_veri /dev/sdd1
    # Artık LV'leri büyütebilirsiniz!

> ⚠️ **Önemli:** XFS dosya sistemi **küçültülemez!** Sadece
> büyütülebilir. ext4 ise hem büyütülebilir hem küçültülebilir.

------------------------------------------------------------------------

## 12.3 Swap Alanı Yönetimi

    # Mevcut swap durumu
    free -h
    swapon --show

    # Swap bölümü oluşturma
    sudo lvcreate -n lv_swap -L 4G vg_rhel
    sudo mkswap /dev/vg_rhel/lv_swap
    sudo swapon /dev/vg_rhel/lv_swap

    # Swap dosyası oluşturma
    sudo dd if=/dev/zero of=/swapfile bs=1M count=2048
    sudo chmod 600 /swapfile
    sudo mkswap /swapfile
    sudo swapon /swapfile

    # fstab'a ekle
    echo '/swapfile  swap  swap  defaults  0 0' | sudo tee -a /etc/fstab

    # Swappiness ayarı (ne kadar agresif swap kullanılsın)
    cat /proc/sys/vm/swappiness           # Varsayılan: 60
    sudo sysctl vm.swappiness=10           # Daha az swap kullan
    echo 'vm.swappiness=10' | sudo tee -a /etc/sysctl.d/99-swappiness.conf

------------------------------------------------------------------------

## 12.4 Sık Karşılaşılan Sorunlar

### ⚠️ Sorun: LV büyüttüm ama dosya sistemi hâlâ aynı boyutta

**Çözüm:** LV büyütüldükten sonra dosya sistemini de genişletmelisiniz:

    sudo xfs_growfs /mount_noktasi       # XFS
    sudo resize2fs /dev/vg/lv            # ext4

### ⚠️ Sorun: Disk doldu, VG'de yer yok

**Çözüm:** Yeni fiziksel disk ekleyin:

    sudo pvcreate /dev/sdd1
    sudo vgextend vg_veri /dev/sdd1
    sudo lvextend -r -l +100%FREE /dev/vg_veri/lv_data

------------------------------------------------------------------------

## 12.5 Bölüm Özeti

- ✅ Disk bölümleme (fdisk, parted), MBR vs GPT
- ✅ LVM oluşturma ve yönetimi (PV, VG, LV)
- ✅ LVM boyut değiştirme ve genişletme
- ✅ Swap alanı yönetimi

# BÖLÜM 13-14: Firewall ve SELinux

------------------------------------------------------------------------

# 13. Firewall Yönetimi

## 13.1 firewalld

RHEL'de varsayılan güvenlik duvarı **firewalld**'dir. Bölgelere (zone)
dayalı dinamik bir yapı sunar.

### Temel Komutlar

    # Durum
    sudo systemctl status firewalld
    sudo firewall-cmd --state

    # Aktif bölgeyi göster
    sudo firewall-cmd --get-active-zones
    sudo firewall-cmd --get-default-zone
    sudo firewall-cmd --list-all                      # Tüm kurallar

    # Servis ekleme
    sudo firewall-cmd --add-service=http --permanent   # HTTP izin ver
    sudo firewall-cmd --add-service=https --permanent  # HTTPS izin ver
    sudo firewall-cmd --reload                         # Kuralları uygula

    # Port ekleme
    sudo firewall-cmd --add-port=8080/tcp --permanent
    sudo firewall-cmd --add-port=5000-5100/tcp --permanent  # Port aralığı

    # Kaldırma
    sudo firewall-cmd --remove-service=http --permanent
    sudo firewall-cmd --remove-port=8080/tcp --permanent
    sudo firewall-cmd --reload

    # Kaynak (IP) bazlı kural
    sudo firewall-cmd --add-rich-rule='rule family="ipv4" source address="192.168.1.0/24" service name="ssh" accept' --permanent

    # Belirli IP'yi engelle
    sudo firewall-cmd --add-rich-rule='rule family="ipv4" source address="10.0.0.50" reject' --permanent

    # Port yönlendirme
    sudo firewall-cmd --add-forward-port=port=80:proto=tcp:toport=8080 --permanent
    sudo firewall-cmd --reload

### Firewalld Bölgeleri (Zones)

  ------------------------------------------------------------
  Bölge                    Açıklama
  ------------------------ -----------------------------------
  `public`                 Varsayılan, güvenilmeyen ağlar
                           (sadece ssh, dhcpv6-client)

  `internal`               İç ağ, daha fazla güven

  `trusted`                Tüm trafiğe izin verir

  `drop`                   Tüm gelen trafik düşürülür (yanıt
                           yok)

  `block`                  Tüm gelen trafik reddedilir (ICMP
                           reject)

  `dmz`                    DMZ bölgesi
  ------------------------------------------------------------

    # Bölge değiştir
    sudo firewall-cmd --set-default-zone=internal

    # Arayüzü farklı bölgeye ata
    sudo firewall-cmd --zone=internal --change-interface=ens192 --permanent

------------------------------------------------------------------------

# 14. SELinux

## 14.1 SELinux Nedir?

**Security-Enhanced Linux (SELinux)**, Linux çekirdeğinde zorunlu erişim
kontrolü (MAC --- Mandatory Access Control) uygulayan güvenlik
modülüdür. Normal Linux izinlerinin **üzerine** ek bir güvenlik katmanı
ekler.

### SELinux Modları

  -------------------------------------------------------------
  Mod                  Açıklama
  -------------------- ----------------------------------------
  **Enforcing**        Kurallar uygulanır, ihlaller engellenir
                       ve loglanır (**üretimde bu
                       kullanılmalı!**)

  **Permissive**       Kurallar uygulanmaz ama ihlaller
                       loglanır (sorun giderme için)

  **Disabled**         Tamamen kapalı (**önerilmez!**)
  -------------------------------------------------------------

    # Modu kontrol et
    getenforce                        # Mevcut mod
    sestatus                          # Detaylı durum

    # Geçici mod değişikliği (yeniden başlatmada kaybolur)
    sudo setenforce 0                  # Permissive
    sudo setenforce 1                  # Enforcing

    # Kalıcı mod değişikliği
    sudo vim /etc/selinux/config
    # SELINUX=enforcing

> ⚠️ **ÖNEMLİ:** SELinux'u asla **disabled** yapmayın! Sorun varsa
> **permissive** yaparak loglara bakın.

## 14.2 SELinux Etiketleri (Contexts)

Her dosya, süreç ve port'un bir SELinux etiketi vardır:

    # Dosya etiketlerini göster
    ls -Z /var/www/html/
    # -rw-r--r--. root root unconfined_u:object_r:httpd_sys_content_t:s0 index.html
    #                                              ^^^^^^^^^^^^^^^^
    #                                              Tür etiketi (en önemli kısım)

    # Süreç etiketlerini göster
    ps auxZ | grep httpd
    # system_u:system_r:httpd_t:s0  apache  httpd

    # Port etiketlerini göster
    sudo semanage port -l | grep http
    # http_port_t  tcp  80, 443, 488, 8008, 8009, 8443

## 14.3 SELinux Sorun Giderme

SELinux kaynaklı sorunlar genellikle servisin dosyalara erişememesi
şeklinde ortaya çıkar.

    # 1. Audit loglarını kontrol et
    sudo ausearch -m AVC -ts recent
    sudo cat /var/log/audit/audit.log | grep denied

    # 2. sealert ile okunabilir açıklama al
    sudo dnf install setroubleshoot-server
    sudo sealert -a /var/log/audit/audit.log

    # 3. Dosya etiketini düzelt (en yaygın çözüm)
    sudo restorecon -Rv /var/www/html/
    # Dosyalar yanlış konumdan kopyalandıysa etiketler bozulmuş olabilir

    # 4. Boolean değerleri (özellik açma/kapama)
    sudo getsebool -a | grep httpd           # httpd ile ilgili boolean'lar
    sudo setsebool -P httpd_can_network_connect on    # httpd'nin ağa bağlanmasına izin ver
    sudo setsebool -P httpd_enable_homedirs on        # Kullanıcı ev dizinlerine erişim

    # 5. Özel port ekleme
    sudo semanage port -a -t http_port_t -p tcp 8888   # 8888 portunu httpd için aç

    # 6. Özel dosya etiketi ekleme
    sudo semanage fcontext -a -t httpd_sys_content_t "/web(/.*)?"
    sudo restorecon -Rv /web/

### SELinux Sorun Giderme Akışı

    Servis çalışmıyor veya erişim hatası
                    │
                    ▼
        SELinux loglarını kontrol et
        (ausearch -m AVC -ts recent)
                    │
            ┌───────┴──────┐
            │              │
        AVC var          AVC yok
            │              │
            ▼              ▼
      sealert çalıştır    Sorun SELinux
      önerilen çözümü     kaynaklı değil
      uygula              (izinler, firewall
            │              vb. kontrol et)
            ▼
      ┌─────────────────┐
      │ restorecon      │ → Etiket sorunu
      │ setsebool       │ → Boolean sorunu
      │ semanage port   │ → Port sorunu
      │ semanage fcontext│→ Özel dizin
      └─────────────────┘

------------------------------------------------------------------------

## 14.4 Bölüm Özeti

- ✅ firewalld ile güvenlik duvarı yönetimi (servis, port, zone,
  rich-rule)
- ✅ SELinux modları, etiketleri (contexts)
- ✅ SELinux sorun giderme (restorecon, setsebool, semanage, sealert)
- ✅ SELinux'u kapatmak yerine doğru sorun giderme yaklaşımı

# BÖLÜM 15-17: SSH, Güvenlik ve Uzaktan Erişim

------------------------------------------------------------------------

# 15. SSH ve Uzaktan Erişim

## 15.1 SSH Temelleri

    # Sunucuya bağlan
    ssh kullanici@192.168.1.100
    ssh -p 2222 kullanici@sunucu          # Farklı port
    ssh -v kullanici@sunucu               # Debug modu

    # Uzak komut çalıştır
    ssh kullanici@sunucu "df -h"
    ssh kullanici@sunucu "cat /etc/hostname"

## 15.2 SSH Anahtar Tabanlı Kimlik Doğrulama

    # 1. Anahtar çifti oluştur (istemcide)
    ssh-keygen -t rsa -b 4096 -C "ahmet@sirket.local"
    # Veya daha modern:
    ssh-keygen -t ed25519 -C "ahmet@sirket.local"

    # 2. Genel anahtarı sunucuya kopyala
    ssh-copy-id kullanici@sunucu
    # Veya manuel:
    cat ~/.ssh/id_rsa.pub | ssh kullanici@sunucu 'mkdir -p ~/.ssh && cat >> ~/.ssh/authorized_keys'

    # 3. Anahtarla bağlan (artık parola sormaz)
    ssh kullanici@sunucu

## 15.3 SSH Sertleştirme

    sudo vim /etc/ssh/sshd_config
    # Önerilen güvenlik ayarları:
    PermitRootLogin no              # Root SSH girişini kapat
    PasswordAuthentication no       # Parola ile girişi kapat (anahtar zorunlu)
    Port 2222                       # Varsayılan portu değiştir
    MaxAuthTries 3                  # Maksimum deneme: 3
    ClientAliveInterval 300         # 5 dakika boşta kalınca kes
    ClientAliveCountMax 2           # 2 kez uyar, sonra kes
    AllowUsers ahmet mehmet         # Sadece belirli kullanıcılar
    Protocol 2                      # Sadece SSH v2
    X11Forwarding no                # X11 yönlendirme kapalı
    # Yeniden başlat
    sudo systemctl restart sshd

    # Firewall'da yeni portu aç
    sudo firewall-cmd --add-port=2222/tcp --permanent
    sudo firewall-cmd --remove-service=ssh --permanent
    sudo firewall-cmd --reload

## 15.4 SCP ve SFTP --- Dosya Transferi

    # SCP — Güvenli dosya kopyalama
    scp dosya.txt kullanici@sunucu:/home/kullanici/    # Gönder
    scp kullanici@sunucu:/var/log/messages ./           # Al
    scp -r dizin/ kullanici@sunucu:/opt/               # Dizin kopyala
    scp -P 2222 dosya.txt kullanici@sunucu:~/          # Farklı port

    # SFTP — Etkileşimli dosya transferi
    sftp kullanici@sunucu
    sftp> ls                    # Uzak dizini listele
    sftp> lls                   # Yerel dizini listele
    sftp> put dosya.txt         # Dosya gönder
    sftp> get uzak_dosya.txt    # Dosya al
    sftp> quit

## 15.5 SSH Tünelleme

    # Yerel port yönlendirme (uzak servise yerel erişim)
    ssh -L 8080:localhost:80 kullanici@sunucu
    # Artık tarayıcıdan http://localhost:8080 ile sunucudaki web'e erişin

    # Uzak port yönlendirme (yerel servise uzaktan erişim)
    ssh -R 9090:localhost:3000 kullanici@sunucu
    # Sunucudaki 9090 portu, yerel 3000'e yönlendirilir

    # Dinamik proxy (SOCKS proxy)
    ssh -D 8888 kullanici@sunucu
    # Tarayıcıda SOCKS proxy olarak localhost:8888 kullanın

------------------------------------------------------------------------

# 16. Sistem Güvenliği Sertleştirme

## 16.1 Güvenlik Kontrol Listesi

    # 1. Gereksiz servisleri kapat
    systemctl list-units --type=service --state=running
    sudo systemctl disable --now cups        # Yazıcı servisi (sunucuda gereksiz)
    sudo systemctl disable --now avahi-daemon # mDNS (sunucuda gereksiz)
    sudo systemctl disable --now bluetooth   # Bluetooth

    # 2. Açık portları kontrol et — sadece gerekli portlar açık olsun
    ss -tulnp

    # 3. Güvenlik güncellemelerini otomatik kur
    sudo dnf install dnf-automatic
    sudo vim /etc/dnf/automatic.conf
    # apply_updates = yes
    # emit_via = motd

    sudo systemctl enable --now dnf-automatic.timer

    # 4. Dosya bütünlüğü izleme
    sudo dnf install aide
    sudo aide --init                        # Veritabanı oluştur
    sudo mv /var/lib/aide/aide.db.new.gz /var/lib/aide/aide.db.gz
    sudo aide --check                       # Kontrol et

    # 5. Audit logları etkinleştir
    sudo systemctl enable --now auditd
    sudo auditctl -l                        # Mevcut kurallar
    sudo ausearch -m USER_LOGIN -ts today   # Bugünkü girişler

## 16.2 PAM (Pluggable Authentication Modules)

    # Başarısız giriş denemelerinde hesap kilitleme
    sudo vim /etc/security/faillock.conf
    # deny = 5              # 5 başarısız deneme sonrası kilitle
    # unlock_time = 600     # 10 dakika sonra kilidi aç
    # fail_interval = 900   # 15 dakika penceresi

    # Kilitli hesabı açma
    sudo faillock --user ahmet --reset

------------------------------------------------------------------------

# 17. NFS ve Samba Dosya Paylaşımı

## 17.1 NFS (Linux-Linux Paylaşım)

    # NFS Sunucu:
    sudo dnf install nfs-utils
    sudo systemctl enable --now nfs-server

    # Paylaşım tanımla
    sudo vim /etc/exports
    # /paylasim  192.168.1.0/24(rw,sync,no_root_squash)

    sudo exportfs -rav                  # Paylaşımları uygula
    sudo firewall-cmd --add-service=nfs --permanent
    sudo firewall-cmd --reload

    # NFS İstemci:
    sudo mount -t nfs sunucu:/paylasim /mnt/nfs
    # fstab'a ekle:
    # sunucu:/paylasim  /mnt/nfs  nfs  defaults  0 0

## 17.2 Samba (Linux-Windows Paylaşım)

    # Samba sunucu:
    sudo dnf install samba samba-client
    sudo systemctl enable --now smb nmb

    sudo vim /etc/samba/smb.conf
    # [paylasim]
    #    path = /srv/samba/paylasim
    #    writable = yes
    #    valid users = ahmet

    sudo smbpasswd -a ahmet                # Samba kullanıcısı oluştur
    sudo firewall-cmd --add-service=samba --permanent
    sudo firewall-cmd --reload

    # Test:
    smbclient //sunucu/paylasim -U ahmet

------------------------------------------------------------------------

## Bölüm Özeti

- ✅ SSH yapılandırma ve sertleştirme
- ✅ Anahtar tabanlı kimlik doğrulama
- ✅ SCP/SFTP ile dosya transferi, SSH tünelleme
- ✅ Sistem güvenliği sertleştirme (servis kapatma, auto-update, AIDE,
  audit)
- ✅ NFS ve Samba dosya paylaşımı

# BÖLÜM 18-19: Web Sunucusu ve DNS

------------------------------------------------------------------------

# 18. Web Sunucusu (Apache)

## 18.1 Apache Kurulum ve Yapılandırma

    # Kurulum
    sudo dnf install httpd mod_ssl

    # Başlatma
    sudo systemctl enable --now httpd
    sudo firewall-cmd --add-service={http,https} --permanent
    sudo firewall-cmd --reload

    # Test
    curl http://localhost

### Ana Yapılandırma

    # Ana yapılandırma dosyası
    sudo vim /etc/httpd/conf/httpd.conf

    # Önemli yönergeler:
    ServerRoot "/etc/httpd"
    Listen 80
    ServerAdmin admin@sirket.local
    ServerName sunucu01.sirket.local:80
    DocumentRoot "/var/www/html"
    ErrorLog "logs/error_log"

### Sanal Sunucu (Virtual Host)

    sudo vim /etc/httpd/conf.d/site1.conf
    <VirtualHost *:80>
        ServerName site1.sirket.local
        ServerAlias www.site1.sirket.local
        DocumentRoot /var/www/site1
        ErrorLog /var/log/httpd/site1-error.log
        CustomLog /var/log/httpd/site1-access.log combined
        
        <Directory /var/www/site1>
            Options -Indexes +FollowSymLinks
            AllowOverride All
            Require all granted
        </Directory>
    </VirtualHost>
    # Dizini oluştur, izinleri ayarla
    sudo mkdir -p /var/www/site1
    echo "<h1>Site 1</h1>" | sudo tee /var/www/site1/index.html
    sudo chown -R apache:apache /var/www/site1
    sudo restorecon -Rv /var/www/site1       # SELinux etiketi

    # Yapılandırmayı test et
    sudo apachectl configtest
    sudo systemctl reload httpd

### SSL/TLS Yapılandırma

    # Self-signed sertifika oluştur
    sudo openssl req -x509 -nodes -days 365 -newkey rsa:2048 \
      -keyout /etc/pki/tls/private/sunucu.key \
      -out /etc/pki/tls/certs/sunucu.crt \
      -subj "/C=TR/ST=Istanbul/L=Istanbul/O=Sirket/CN=sunucu01.sirket.local"

    # SSL Virtual Host
    sudo vim /etc/httpd/conf.d/ssl-site1.conf
    <VirtualHost *:443>
        ServerName site1.sirket.local
        DocumentRoot /var/www/site1
        SSLEngine on
        SSLCertificateFile /etc/pki/tls/certs/sunucu.crt
        SSLCertificateKeyFile /etc/pki/tls/private/sunucu.key
    </VirtualHost>

### Apache Sorun Giderme

    # Yapılandırma söz dizimi kontrolü
    sudo apachectl configtest

    # Logları incele
    sudo tail -f /var/log/httpd/error_log
    sudo tail -f /var/log/httpd/access_log

    # Yaygın sorunlar:
    # 403 Forbidden → İzin sorunu (chmod, chown, SELinux)
    # 500 Internal Server Error → .htaccess hatası, modül sorunu
    # 503 Service Unavailable → Backend servis çalışmıyor

------------------------------------------------------------------------

# 19. DNS Sunucusu (BIND)

## 19.1 DNS Temel Kavramlar

    İstemci → DNS Cache → Yetkili DNS Sunucusu
       │                        │
       └── "google.com IP'si ne?" 
                                │
                        ┌───────┴──────┐
                        │ Root DNS (.)  │
                        │ → .com NS    │
                        ├──────────────┤
                        │ .com DS      │
                        │ → google NS  │
                        ├──────────────┤
                        │ google.com   │
                        │ → 142.250.x  │
                        └──────────────┘

### DNS Kayıt Türleri

  -------------------------------------------------------------------------------
  Tür           Açıklama                    Örnek
  ------------- --------------------------- -------------------------------------
  **A**         İsim → IPv4 adresi          `sunucu01 IN A 192.168.1.100`

  **AAAA**      İsim → IPv6 adresi          `sunucu01 IN AAAA ::1`

  **CNAME**     Takma isim                  `www IN CNAME sunucu01`

  **MX**        E-posta sunucusu            `@ IN MX 10 mail.sirket.local.`

  **PTR**       IP → İsim (ters çözümleme)  `100 IN PTR sunucu01.sirket.local.`

  **NS**        Nameserver                  `@ IN NS ns1.sirket.local.`

  **SOA**       Zone yetkisi                Seri no, yenileme süreleri

  **TXT**       Metin kaydı                 SPF, DKIM gibi doğrulamalar
  -------------------------------------------------------------------------------

## 19.2 BIND Kurulumu

    sudo dnf install bind bind-utils
    sudo systemctl enable --now named
    sudo firewall-cmd --add-service=dns --permanent
    sudo firewall-cmd --reload

### Zone Dosyası Örneği

    sudo vim /etc/named.conf
    # İleri yönlü zone ekle:
    zone "sirket.local" IN {
        type master;
        file "sirket.local.zone";
        allow-update { none; };
    };

    # Ters çözümleme zone:
    zone "1.168.192.in-addr.arpa" IN {
        type master;
        file "192.168.1.zone";
        allow-update { none; };
    };
    # İleri yönlü zone dosyası
    sudo vim /var/named/sirket.local.zone
    $TTL 86400
    @   IN  SOA ns1.sirket.local. admin.sirket.local. (
                2026021501  ; Serial (YYYYMMDDNN)
                3600        ; Refresh
                1800        ; Retry
                604800      ; Expire
                86400 )     ; Minimum TTL

        IN  NS  ns1.sirket.local.

    ns1      IN  A    192.168.1.10
    sunucu01 IN  A    192.168.1.100
    mail     IN  A    192.168.1.101
    www      IN  CNAME sunucu01
    @        IN  MX   10 mail.sirket.local.
    # Yapılandırmayı kontrol et
    named-checkconf
    named-checkzone sirket.local /var/named/sirket.local.zone

    # DNS'yi yeniden başlat
    sudo systemctl restart named

    # Test
    dig @localhost sunucu01.sirket.local
    nslookup sunucu01.sirket.local localhost

------------------------------------------------------------------------

## Bölüm Özeti

- ✅ Apache kurulum, yapılandırma ve sanal sunucular
- ✅ SSL/TLS sertifika yönetimi
- ✅ Apache sorun giderme
- ✅ BIND DNS sunucusu kurulumu ve zone dosyaları
- ✅ DNS kayıt türleri (A, CNAME, MX, PTR, NS)

# BÖLÜM 20-23: Bash Scripting, Log Yönetimi, Yedekleme ve Performans

------------------------------------------------------------------------

# 20. Kabuk Programlama (Bash Scripting)

## 20.1 Script Temelleri

    #!/bin/bash
    # İlk satır (shebang) sisteme hangi yorumlayıcıyı kullanacağını söyler

    # Yorum satırı - # ile başlar

    # Değişkenler
    ISIM="Ahmet"
    YAS=30
    echo "Merhaba $ISIM, yaşınız: $YAS"

    # Kullanıcıdan girdi alma
    read -p "Adınız: " KULLANICI_ADI
    echo "Hoş geldiniz, $KULLANICI_ADI"

    # Komut çıktısını değişkene atama
    TARIH=$(date +%Y-%m-%d)
    HOSTNAME=$(hostname)
    DISK_KULLANIM=$(df -h / | awk 'NR==2 {print $5}')

## 20.2 Koşullar

    #!/bin/bash
    # if-elif-else yapısı

    DOSYA="/etc/passwd"

    if [ -f "$DOSYA" ]; then
        echo "$DOSYA mevcut"
    elif [ -d "$DOSYA" ]; then
        echo "$DOSYA bir dizin"
    else
        echo "$DOSYA bulunamadı"
    fi

    # Sayısal karşılaştırma
    DISK=$(df / | awk 'NR==2 {print $5}' | tr -d '%')
    if [ "$DISK" -gt 90 ]; then
        echo "UYARI: Disk %${DISK} dolu!"
    elif [ "$DISK" -gt 70 ]; then
        echo "DİKKAT: Disk %${DISK} dolu"
    else
        echo "Disk durumu normal: %${DISK}"
    fi

    # Test operatörleri:
    # Dosya testleri: -f (dosya), -d (dizin), -e (var mı), -r (okunur), -w (yazılır), -x (çalıştırılır)
    # Sayısal: -eq (eşit), -ne (eşit değil), -gt (büyük), -lt (küçük), -ge (≥), -le (≤)
    # Metin: = (eşit), != (farklı), -z (boş), -n (boş değil)
    # Mantıksal: && (VE), || (VEYA), ! (DEĞİL)

## 20.3 Döngüler

    #!/bin/bash

    # for döngüsü
    for SUNUCU in web01 web02 db01 db02; do
        echo "Kontrol ediliyor: $SUNUCU"
        ping -c 1 -W 2 $SUNUCU > /dev/null 2>&1
        if [ $? -eq 0 ]; then
            echo "  ✅ $SUNUCU erişilebilir"
        else
            echo "  ❌ $SUNUCU erişilemez!"
        fi
    done

    # Sayısal for döngüsü
    for i in {1..10}; do
        echo "Sunucu $i"
    done

    # while döngüsü
    SAYAC=0
    while [ $SAYAC -lt 5 ]; do
        echo "Döngü: $SAYAC"
        SAYAC=$((SAYAC + 1))
    done

    # Dosya satırlarını oku
    while IFS= read -r SATIR; do
        echo "Satır: $SATIR"
    done < /etc/hostname

## 20.4 Fonksiyonlar

    #!/bin/bash

    # Fonksiyon tanımı
    log_yaz() {
        local SEVIYE=$1
        local MESAJ=$2
        echo "[$(date '+%Y-%m-%d %H:%M:%S')] [$SEVIYE] $MESAJ" | tee -a /var/log/myapp.log
    }

    servis_kontrol() {
        local SERVIS=$1
        if systemctl is-active --quiet $SERVIS; then
            log_yaz "INFO" "$SERVIS çalışıyor"
            return 0
        else
            log_yaz "ERROR" "$SERVIS çalışmıyor! Başlatılıyor..."
            systemctl start $SERVIS
            return 1
        fi
    }

    # Fonksiyonları kullan
    log_yaz "INFO" "Script başlatıldı"
    servis_kontrol httpd
    servis_kontrol sshd
    log_yaz "INFO" "Script tamamlandı"

## 20.5 Pratik Script Örnekleri

### Sunucu Sağlık Kontrolü

    #!/bin/bash
    # sunucu_kontrol.sh — Sunucu sağlık raporu

    RAPOR_DOSYA="/tmp/sunucu_rapor_$(date +%Y%m%d).txt"

    {
    echo "========================================"
    echo "SUNUCU SAĞLIK RAPORU"
    echo "Tarih: $(date)"
    echo "Hostname: $(hostname)"
    echo "========================================"

    echo ""
    echo "--- UPTIME ---"
    uptime

    echo ""
    echo "--- CPU YÜKÜ ---"
    top -bn1 | head -5

    echo ""
    echo "--- BELLEK KULLANIMI ---"
    free -h

    echo ""
    echo "--- DİSK KULLANIMI ---"
    df -h | grep -v tmpfs

    echo ""
    echo "--- KRITIK SERVİSLER ---"
    for SERVIS in httpd sshd firewalld crond; do
        STATUS=$(systemctl is-active $SERVIS 2>/dev/null)
        printf "%-20s : %s\n" "$SERVIS" "$STATUS"
    done

    echo ""
    echo "--- SON 10 BAŞARISIZ GİRİŞ ---"
    lastb 2>/dev/null | head -10 || echo "lastb kullanılamıyor"

    echo ""
    echo "--- DISK %90+ DOLU BÖLÜMLER ---"
    df -h | awk '$5+0 > 90 {print "UYARI: " $1 " — " $5 " dolu!"}'

    } > "$RAPOR_DOSYA"

    echo "Rapor oluşturuldu: $RAPOR_DOSYA"
    cat "$RAPOR_DOSYA"

### Otomatik Yedekleme Scripti

    #!/bin/bash
    # yedek.sh — Otomatik yedekleme

    KAYNAK="/var/www /etc /home"
    HEDEF="/backup"
    TARIH=$(date +%Y%m%d_%H%M)
    LOG="/var/log/yedekleme.log"
    SAKLA_GUN=30

    log() { echo "[$(date '+%Y-%m-%d %H:%M:%S')] $1" | tee -a $LOG; }

    log "=== Yedekleme başladı ==="

    # Hedef dizini oluştur
    mkdir -p $HEDEF

    # Tar ile yedek al
    YEDEK_DOSYA="${HEDEF}/yedek_${TARIH}.tar.gz"
    tar czf "$YEDEK_DOSYA" $KAYNAK 2>> $LOG

    if [ $? -eq 0 ]; then
        BOYUT=$(du -h "$YEDEK_DOSYA" | awk '{print $1}')
        log "Yedek başarılı: $YEDEK_DOSYA ($BOYUT)"
    else
        log "HATA: Yedekleme başarısız!"
        exit 1
    fi

    # Eski yedekleri temizle
    find $HEDEF -name "yedek_*.tar.gz" -mtime +$SAKLA_GUN -delete
    log "${SAKLA_GUN} günden eski yedekler temizlendi"

    log "=== Yedekleme tamamlandı ==="

------------------------------------------------------------------------

# 21. Log Yönetimi

## 21.1 rsyslog ve journald

    # Sistem logları
    /var/log/messages          # Genel sistem logları
    /var/log/secure            # Güvenlik ve kimlik doğrulama
    /var/log/cron              # Cron görev logları
    /var/log/boot.log          # Açılış logları
    /var/log/audit/audit.log   # SELinux ve güvenlik audit

    # journalctl — systemd journal logları
    journalctl                         # Tüm loglar
    journalctl -b                      # Bu açılıştan itibaren
    journalctl -u httpd                # Belirli servis
    journalctl -u httpd --since today  # Bugünkü httpd logları
    journalctl -f                      # Canlı takip (tail -f gibi)
    journalctl -p err                  # Sadece hatalar
    journalctl --since "2026-02-15 10:00" --until "2026-02-15 12:00"  # Zaman aralığı
    journalctl --disk-usage            # Journal disk kullanımı

## 21.2 logrotate

    # Log rotasyonu yapılandırması
    cat /etc/logrotate.conf

    # Özel rotasyon kuralı
    sudo vim /etc/logrotate.d/myapp
    /var/log/myapp/*.log {
        daily                    # Günlük rotate et
        rotate 30                # 30 adet sakla
        compress                 # Sıkıştır
        delaycompress            # Bir öncekini sıkıştır
        missingok                # Dosya yoksa hata verme
        notifempty               # Boşsa rotate etme
        create 640 root root     # Yeni dosya oluştur
        postrotate               # Rotate sonrası komut
            systemctl reload myapp > /dev/null 2>&1 || true
        endscript
    }

------------------------------------------------------------------------

# 22. Performans İzleme ve Kernel Yönetimi

## 22.1 Performans Araçları

    # vmstat — Bellek, CPU, I/O genel bakış
    vmstat 2 5                    # 2 saniyede bir, 5 kez

    # iostat — Disk I/O istatistikleri
    sudo dnf install sysstat
    iostat -x 2                   # Genişletilmiş I/O istatistikleri

    # sar — Tarihsel performans verileri
    sar -u                        # CPU kullanım geçmişi
    sar -r                        # Bellek kullanım geçmişi
    sar -b                        # I/O geçmişi
    sar -n DEV                    # Ağ geçmişi

    # free — Bellek durumu
    free -h

    # lsof — Açık dosyalar
    lsof -i :80                   # 80 portunu kullanan süreçler
    lsof -u ahmet                 # ahmet'in açık dosyaları
    lsof +D /var/log              # /var/log altındaki açık dosyalar

    # dmesg — Kernel mesajları
    dmesg | tail -20
    dmesg -T | grep error         # Zaman damgalı, hata filtrelemeli

## 22.2 Kernel Parametreleri (sysctl)

    # Kernel parametrelerini listele
    sysctl -a

    # Belirli parametreyi oku
    sysctl net.ipv4.ip_forward

    # Geçici değiştir
    sudo sysctl -w net.ipv4.ip_forward=1

    # Kalıcı yapılandırma
    sudo vim /etc/sysctl.d/99-custom.conf
    # net.ipv4.ip_forward = 1
    # net.core.somaxconn = 65535
    # vm.swappiness = 10

    sudo sysctl -p /etc/sysctl.d/99-custom.conf     # Uygula

## 22.3 Kernel Modülleri

    # Yüklü modülleri listele
    lsmod

    # Modül bilgisi
    modinfo e1000

    # Modül yükle/kaldır
    sudo modprobe br_netfilter              # Modül yükle
    sudo modprobe -r br_netfilter           # Modül kaldır

    # Kalıcı modül yükleme
    echo "br_netfilter" | sudo tee /etc/modules-load.d/br_netfilter.conf

------------------------------------------------------------------------

# 23. Yedekleme ve Kurtarma

## 23.1 Yedekleme Araçları

    # tar — Arşivleme
    tar czf yedek.tar.gz /etc /home             # Sıkıştırılmış arşiv
    tar xzf yedek.tar.gz                        # Aç
    tar xzf yedek.tar.gz -C /restore/           # Belirtilen dizine aç
    tar tzf yedek.tar.gz                        # İçeriği listele

    # rsync — Artımlı yedekleme (en verimli)
    rsync -avz /kaynak/ /hedef/                 # Yerel kopyalama
    rsync -avz -e ssh /kaynak/ kullanici@sunucu:/hedef/  # Uzak kopyalama
    rsync -avz --delete /kaynak/ /hedef/        # Silinen dosyaları da senkronize et
    rsync -avz --exclude '*.log' /kaynak/ /hedef/  # Log dosyalarını hariç tut

    # dd — Disk düzeyinde yedekleme
    sudo dd if=/dev/sda of=/backup/disk.img bs=4M status=progress  # Tam disk yedeği
    sudo dd if=/dev/sda1 of=/backup/partition.img bs=4M status=progress  # Bölüm yedeği

## 23.2 Felaket Kurtarma Planı

    1. Düzenli yedekler (3-2-1 kuralı):
       ├── 3 kopya veri
       ├── 2 farklı medya (disk + tape/bulut)
       └── 1 kopya offsite (farklı konum)

    2. Kurtarma testi (en az ayda 1):
       ├── Yedeği geri yükle
       ├── Servislerin çalıştığını doğrula
       └── RTO/RPO hedeflerini kontrol et

    3. Rescue Mode ile kurtarma:
       ├── ISO'dan boot et
       ├── "Troubleshooting" → "Rescue a RHEL system" seçin
       ├── chroot /mnt/sysroot
       └── Gerekli onarımları yap

------------------------------------------------------------------------

## Bölüm Özeti

- ✅ Bash scripting: değişkenler, koşullar, döngüler, fonksiyonlar
- ✅ Pratik otomasyon scriptleri (sağlık kontrolü, yedekleme)
- ✅ Log yönetimi (rsyslog, journalctl, logrotate)
- ✅ Performans izleme (vmstat, iostat, sar)
- ✅ Kernel parametreleri ve modülleri
- ✅ Yedekleme stratejileri (tar, rsync, dd)

# BÖLÜM 24-28: Konteynerler, Otomasyon ve DHCP/E-posta/Veritabanı

------------------------------------------------------------------------

# 24. Konteyner Teknolojileri (Podman)

## 24.1 Konteyner Nedir?

Konteyner, bir uygulamayı tüm bağımlılıklarıyla birlikte **izole** bir
ortamda çalıştırma teknolojisidir. Sanal makineden farklı olarak,
konteynerllar host kernel'ı paylaşır --- bu yüzden çok hafif ve
hızlıdır.

    SANAL MAKİNE:                    KONTEYNER:
    ┌─────────────────┐              ┌─────────────────┐
    │    Uygulama A   │              │   Uygulama A    │
    │   Kütüphaneler  │              │  Kütüphaneler   │
    │   İşletim Sis.  │              │                 │
    │   (Guest OS)    │              ├─────────────────┤
    ├─────────────────┤              │   Uygulama B    │
    │    Uygulama B   │              │  Kütüphaneler   │
    │   Kütüphaneler  │              │                 │
    │   İşletim Sis.  │              ├─────────────────┤
    │   (Guest OS)    │              │ Konteyner Engine│
    ├─────────────────┤              │ (Podman/Docker) │
    │   Hypervisor    │              ├─────────────────┤
    ├─────────────────┤              │ Host İşletim S. │
    │ Host İşletim S. │              │ (RHEL Kernel)   │
    └─────────────────┘              └─────────────────┘
     Ağır (~GB), Yavaş                Hafif (~MB), Hızlı

## 24.2 Podman (RHEL'de Varsayılan)

RHEL'de Docker yerine **Podman** kullanılır: daemonsız, rootless, Docker
uyumlu.

    # Kurulum
    sudo dnf install podman

    # İmaj işlemleri
    podman search httpd                          # İmaj ara
    podman pull registry.access.redhat.com/ubi9/httpd-24  # İmaj indir
    podman images                                # Yerel imajlar
    podman rmi IMAGE_ID                          # İmaj sil

    # Konteyner çalıştırma
    podman run -d --name web -p 8080:8080 \
      registry.access.redhat.com/ubi9/httpd-24   # Arka planda çalıştır

    podman run -it --rm ubi9/ubi /bin/bash       # Etkileşimli + çıkınca sil

    # Konteyner yönetimi
    podman ps                                    # Çalışan konteynerlar
    podman ps -a                                 # Tüm konteynerlar
    podman stop web                              # Durdur
    podman start web                             # Başlat
    podman restart web                           # Yeniden başlat
    podman rm web                                # Sil
    podman logs web                              # Loglar
    podman exec -it web /bin/bash                # Konteynera gir

    # Volume (veri kalıcılığı)
    podman run -d --name db -v /data/mysql:/var/lib/mysql:Z \
      -e MYSQL_ROOT_PASSWORD=gizli mariadb       # Z = SELinux etiketi otomatik

    # Konteyner dosyası oluşturma (Containerfile/Dockerfile)
    cat > Containerfile << 'EOF'
    FROM registry.access.redhat.com/ubi9/ubi
    RUN dnf install -y httpd && dnf clean all
    COPY index.html /var/www/html/
    EXPOSE 80
    CMD ["/usr/sbin/httpd", "-D", "FOREGROUND"]
    EOF

    podman build -t my-web .
    podman run -d --name myweb -p 8080:80 my-web

## 24.3 Systemd ile Konteyner Yönetimi

    # Konteyner için systemd unit dosyası oluştur
    podman generate systemd --name web --new > ~/.config/systemd/user/container-web.service

    # Kullanıcı servisi olarak yönet
    systemctl --user enable container-web
    systemctl --user start container-web

------------------------------------------------------------------------

# 25. Otomasyon (Ansible Temelleri)

## 25.1 Ansible Nedir?

**Ansible**, SSH tabanlı, agentsız yapılandırma yönetim ve otomasyon
aracıdır. Sunuculara hiçbir agent/yazılım kurmadan uzaktan yönetim
sağlar.

    # Kurulum
    sudo dnf install ansible-core

    # Envanter dosyası
    cat > /etc/ansible/hosts << 'EOF'
    [webservers]
    web01 ansible_host=192.168.1.101
    web02 ansible_host=192.168.1.102

    [dbservers]
    db01 ansible_host=192.168.1.201

    [all:vars]
    ansible_user=admin
    ansible_ssh_private_key_file=~/.ssh/id_rsa
    EOF

## 25.2 Ad-Hoc Komutlar

    # Tüm sunuculara ping
    ansible all -m ping

    # Komut çalıştır
    ansible webservers -m command -a "uptime"
    ansible webservers -m shell -a "df -h | grep /dev/sda"

    # Paket kur
    ansible webservers -m dnf -a "name=httpd state=present" --become

    # Servis yönetimi
    ansible webservers -m service -a "name=httpd state=started enabled=yes" --become

    # Dosya kopyala
    ansible webservers -m copy -a "src=./index.html dest=/var/www/html/" --become

## 25.3 Playbook

    # web_setup.yml
    ---
    - name: Web Sunucusu Kurulumu
      hosts: webservers
      become: true
      
      vars:
        http_port: 80
        domain: sirket.local

      tasks:
        - name: Apache kurulumu
          dnf:
            name: 
              - httpd
              - mod_ssl
              - php
            state: present

        - name: Apache yapılandırma dosyası
          template:
            src: templates/httpd.conf.j2
            dest: /etc/httpd/conf/httpd.conf
          notify: Restart Apache

        - name: Web içeriğini kopyala
          copy:
            src: files/index.html
            dest: /var/www/html/index.html
            owner: apache
            group: apache
            mode: '0644'

        - name: Firewall HTTP izni
          firewalld:
            service: "{{ item }}"
            permanent: true
            state: enabled
            immediate: true
          loop:
            - http
            - https

        - name: Apache'yi başlat
          service:
            name: httpd
            state: started
            enabled: true

      handlers:
        - name: Restart Apache
          service:
            name: httpd
            state: restarted
    # Playbook çalıştır
    ansible-playbook web_setup.yml

    # Kuru çalıştırma (test)
    ansible-playbook web_setup.yml --check

    # Verbose
    ansible-playbook web_setup.yml -vvv

------------------------------------------------------------------------

# 26. DHCP Sunucusu

    # Kurulum
    sudo dnf install dhcp-server

    # Yapılandırma
    sudo vim /etc/dhcp/dhcpd.conf
    # Genel ayarlar
    option domain-name "sirket.local";
    option domain-name-servers 192.168.1.10, 8.8.8.8;
    default-lease-time 600;
    max-lease-time 7200;
    authoritative;

    # Alt ağ tanımı
    subnet 192.168.1.0 netmask 255.255.255.0 {
        range 192.168.1.50 192.168.1.200;
        option routers 192.168.1.1;
        option subnet-mask 255.255.255.0;
        option broadcast-address 192.168.1.255;
    }

    # Sabit IP ataması (MAC adresine göre)
    host sunucu01 {
        hardware ethernet 00:50:56:ab:cd:ef;
        fixed-address 192.168.1.100;
    }
    sudo systemctl enable --now dhcpd
    sudo firewall-cmd --add-service=dhcp --permanent && sudo firewall-cmd --reload

------------------------------------------------------------------------

# 27. E-posta (Postfix) ve Veritabanı (MariaDB)

## 27.1 Postfix Temelleri

    sudo dnf install postfix
    sudo vim /etc/postfix/main.cf
    # myhostname = mail.sirket.local
    # mydomain = sirket.local
    # myorigin = $mydomain
    # inet_interfaces = all
    # mydestination = $myhostname, $mydomain, localhost
    # mynetworks = 192.168.1.0/24, 127.0.0.0/8

    sudo systemctl enable --now postfix
    sudo firewall-cmd --add-service=smtp --permanent && sudo firewall-cmd --reload

    # Test
    echo "Test mesajı" | mail -s "Test" kullanici@sirket.local

## 27.2 MariaDB

    # Kurulum
    sudo dnf install mariadb-server
    sudo systemctl enable --now mariadb

    # Güvenli ilk yapılandırma
    sudo mysql_secure_installation
    # Root parolası belirle, anonim kullanıcıları sil, uzaktan root girişi kapat

    # Veritabanı yönetimi
    mysql -u root -p

    CREATE DATABASE uygulama_db;
    CREATE USER 'appuser'@'localhost' IDENTIFIED BY 'GuvenliParola123!';
    GRANT ALL PRIVILEGES ON uygulama_db.* TO 'appuser'@'localhost';
    FLUSH PRIVILEGES;

    # Yedekleme
    mysqldump -u root -p --all-databases > tum_veritabanlari.sql
    mysqldump -u root -p uygulama_db > uygulama_yedek.sql

    # Geri yükleme
    mysql -u root -p uygulama_db < uygulama_yedek.sql

------------------------------------------------------------------------

## Bölüm Özeti

- ✅ Konteyner kavramı ve Podman kullanımı
- ✅ Konteyner imajı oluşturma ve yönetimi
- ✅ Ansible ile otomasyon (ad-hoc komutlar, playbook)
- ✅ DHCP sunucusu yapılandırma
- ✅ Postfix e-posta ve MariaDB veritabanı temel kurulumu

# BÖLÜM 29-30: Kapsamlı Sorun Giderme Rehberi ve RHCSA Hazırlık

------------------------------------------------------------------------

# 29. Sistematik Sorun Giderme Yaklaşımı

## 29.1 Sorun Giderme Metodolojisi

    ┌─────────────────────────────────────────────────────┐
    │         SORUN GİDERME AKIŞ ŞEMASI                  │
    │                                                     │
    │  1. Sorunu Tanımla                                  │
    │     ├── Ne çalışmıyor?                              │
    │     ├── Ne zaman başladı?                           │
    │     ├── Son değişiklik ne oldu?                     │
    │     └── Hata mesajı ne?                             │
    │                                                     │
    │  2. Bilgi Topla                                     │
    │     ├── Log dosyalarını incele                      │
    │     ├── Servis durumunu kontrol et                  │
    │     ├── Sistem kaynaklarını kontrol et              │
    │     └── Bağlantıyı test et                         │
    │                                                     │
    │  3. Analiz Et                                       │
    │     ├── Olası nedenleri listele                     │
    │     ├── En olası nedenden başla                     │
    │     └── Bir seferde bir değişiklik yap              │
    │                                                     │
    │  4. Çözümü Uygula                                  │
    │     ├── Değişikliği yap                             │
    │     ├── Test et                                     │
    │     └── Çalışmıyorsa geri al                       │
    │                                                     │
    │  5. Belgeleme                                       │
    │     └── Ne yaptığını kaydet (gelecek için)          │
    └─────────────────────────────────────────────────────┘

------------------------------------------------------------------------

## 29.2 Kategori Bazlı Sorun Giderme

### 🔴 Sistem Açılmıyor

    # Belirti: GRUB menüsü gelmiyor
    # Neden: Bootloader bozulmuş
    # Çözüm:
    # 1. RHEL ISO'dan boot edin
    # 2. Rescue mode seçin
    # 3. chroot /mnt/sysroot
    # 4. grub2-install /dev/sda
    # 5. grub2-mkconfig -o /boot/grub2/grub.cfg
    # 6. exit && reboot

    # Belirti: Kernel panic
    # Neden: Bozuk kernel veya initramfs
    # Çözüm:
    # 1. GRUB'da eski kernel'ı seçin
    # 2. Sisteme girin
    # 3. sudo dnf reinstall kernel
    # 4. sudo dracut --force

    # Belirti: emergency.target'a düşüyor
    # Neden: /etc/fstab hatası
    # Çözüm:
    # 1. Root parolasını girin
    # 2. journalctl -xb | grep -i "mount\|fstab"
    # 3. vim /etc/fstab  → hatalı satırı düzeltin
    # 4. mount -a         → test edin
    # 5. reboot

    # Belirti: Root parolası unutuldu
    # Çözüm: (GRUB'da rd.break metodu — Bölüm 6'da detaylı)

### 🔴 Servis Çalışmıyor

    # Kontrol sırası:
    # 1. Servis durumu
    systemctl status SERVIS
    journalctl -u SERVIS -n 50 --no-pager

    # 2. Yapılandırma söz dizimi
    httpd -t                     # Apache
    named-checkconf              # BIND
    nginx -t                     # Nginx
    sshd -t                      # SSH

    # 3. Port çakışması
    ss -tulnp | grep PORTA_NUMARASI

    # 4. İzinler
    ls -laZ /path/to/config/
    namei -l /path/to/document/root/

    # 5. SELinux
    ausearch -m AVC -ts recent
    sealert -a /var/log/audit/audit.log

    # 6. Firewall
    firewall-cmd --list-all

    # 7. Bağımlılıklar
    systemctl list-dependencies SERVIS

### 🔴 Disk Dolu

    # 1. Hangi bölüm dolu?
    df -h

    # 2. En büyük dizinleri bul
    du -sh /* 2>/dev/null | sort -rh | head -10
    du -sh /var/* 2>/dev/null | sort -rh | head -10

    # 3. En büyük dosyaları bul
    find / -type f -size +100M -exec ls -lh {} \; 2>/dev/null | sort -k5 -rh | head -20

    # 4. Silinmiş ama hâlâ açık dosyalar (alan boşalmaz!)
    lsof | grep deleted | sort -k7 -rn | head -10
    # Çözüm: İlgili süreci yeniden başlatın

    # 5. Log dosyalarını temizle
    sudo truncate -s 0 /var/log/messages    # Dosyayı sıfırla (silme!)
    sudo journalctl --vacuum-size=100M       # Journal boyutunu sınırla

    # 6. Paket önbelleğini temizle
    sudo dnf clean all

    # 7. Eski kernel'ları kaldır (en son 2'si kalır)
    sudo dnf remove --oldinstallonly

    # 8. /tmp temizle
    sudo systemctl restart systemd-tmpfiles-clean

### 🔴 Ağ Bağlantısı Yok

    # Sistematik ağ sorun giderme (aşağıdan yukarıya):

    # Katman 1: Fiziksel
    ip link show ens192                # UP/DOWN durumu
    ethtool ens192                     # Link detected: yes/no

    # Katman 2: Veri Bağlantısı
    ip neigh show                      # ARP tablosu
    arping -c 3 GATEWAY_IP            # ARP testi

    # Katman 3: Ağ
    ip addr show ens192                # IP adresi var mı?
    ping -c 3 GATEWAY_IP              # Gateway'e ulaşılıyor mu?
    ip route show                     # Yönlendirme tablosu doğru mu?

    # Katman 4-7: DNS ve Uygulama
    ping -c 3 8.8.8.8                 # İnternet IP'ye ulaşılıyor mu?
    dig google.com                    # DNS çözümleme çalışıyor mu?
    curl -v http://hedef-sunucu       # HTTP bağlantısı

    # Firewall kontrolü
    sudo firewall-cmd --list-all
    sudo iptables -L -n

### 🔴 Yüksek Yük / Yavaş Sistem

    # 1. Load average kontrol
    uptime
    # load average: 8.50, 6.20, 4.10
    # CPU çekirdek sayısına göre yorumla:
    nproc
    # Load > CPU sayısı ise sorun var

    # 2. CPU kullanan süreçler
    top -bn1 | head -20
    ps aux --sort=-%cpu | head -10

    # 3. Bellek durumu
    free -h
    # available < 500MB tehlikeli
    # swap kullanımı yüksekse RAM yetersiz

    # 4. I/O wait yüksekse (disk darboğazı)
    iostat -x 2 5
    # %util > 90% ise disk darboğazı var
    iotop                              # En çok I/O yapan süreçler

    # 5. OOM (Out of Memory) kontrolü
    dmesg | grep -i "oom\|out of memory"
    journalctl -k | grep -i oom

    # Çözümler:
    # - Gereksiz süreçleri durdurun
    # - Swap ekleyin (kısa vadeli)
    # - RAM artırın (uzun vadeli)
    # - Diskleri SSD'ye geçirin (I/O sorunu)
    # - nice ile süreç önceliğini düşürün

### 🔴 SSH Bağlantı Sorunları

    # 1. SSH servisi çalışıyor mu?
    systemctl status sshd

    # 2. Port açık mı?
    ss -tulnp | grep ssh

    # 3. Firewall izin veriyor mu?
    firewall-cmd --list-services | grep ssh

    # 4. sshd_config söz dizimi doğru mu?
    sshd -t

    # 5. SELinux (özellikle SSH portunu değiştirdiyseniz)
    semanage port -l | grep ssh

    # 6. İstemci tarafında debug
    ssh -vvv kullanici@sunucu

    # 7. /etc/hosts.deny veya /etc/ssh/sshd_config'de engel var mı?
    grep -i "deny\|allow" /etc/hosts.deny /etc/hosts.allow
    grep -i "allowusers\|denyusers" /etc/ssh/sshd_config

    # 8. Anahtar izinleri doğru mu?
    # .ssh dizini: 700, authorized_keys: 600
    chmod 700 ~/.ssh
    chmod 600 ~/.ssh/authorized_keys

------------------------------------------------------------------------

## 29.3 Hızlı Referans Komut Tablosu

  -------------------------------------------------------------
  Sorun Alanı                    İlk Bakılacak Komutlar
  ------------------------------ ------------------------------
  **Sistem geneli**              `uptime`, `dmesg -T`,
                                 `journalctl -xb`

  **Servis**                     `systemctl status X`,
                                 `journalctl -u X`

  **CPU**                        `top`, `ps aux --sort=-%cpu`

  **Bellek**                     `free -h`, `vmstat 2`

  **Disk**                       `df -h`, `df -i`,
                                 `iostat -x 2`

  **Ağ**                         `ip a`, `ss -tulnp`, `ping`,
                                 `traceroute`

  **DNS**                        `dig`, `nslookup`,
                                 `cat /etc/resolv.conf`

  **Firewall**                   `firewall-cmd --list-all`

  **SELinux**                    `getenforce`,
                                 `ausearch -m AVC -ts recent`

  **İzinler**                    `ls -laZ`,
                                 `namei -l /path/to/file`

  **Loglar**                     `tail -f /var/log/messages`,
                                 `journalctl -f`

  **Kullanıcı**                  `id USER`, `passwd -S USER`,
                                 `faillock --user USER`
  -------------------------------------------------------------

------------------------------------------------------------------------

# 30. RHCSA Sınav Hazırlık Rehberi

## 30.1 RHCSA (EX200) Sınav Konuları

RHCSA, Red Hat'in en temel sistem yönetimi sertifikasıdır. Pratik,
laboratuvar tabanlı bir sınavdır.

### Sınav Konuları Kontrol Listesi

    [ ] Temel dosya ve dizin işlemleri
    [ ] Komut satırı operasyonları (pipe, redirect, grep, sed, awk)
    [ ] Yerel ve uzak oturum açma
    [ ] Dosya arşivleme ve sıkıştırma
    [ ] Metin dosyası oluşturma ve düzenleme (vi)
    [ ] Dosya izinleri (chmod, chown, ACL)
    [ ] SUID, SGID, Sticky Bit
    [ ] Kullanıcı ve grup yönetimi
    [ ] Parola yaşlandırma (chage)
    [ ] sudo yapılandırması
    [ ] SELinux: mod ayarlama, booleans, etiketleme
    [ ] firewalld yapılandırması
    [ ] NTP ile zaman senkronizasyonu
    [ ] Paket yönetimi (DNF, RPM)
    [ ] Application Streams (modüller)
    [ ] Systemd servis yönetimi
    [ ] Zamanlanmış görevler (cron, at)
    [ ] Ağ yapılandırması (nmcli)
    [ ] Hostname yapılandırması
    [ ] Disk bölümleme ve dosya sistemi oluşturma
    [ ] LVM oluşturma, genişletme
    [ ] Swap oluşturma
    [ ] /etc/fstab ile kalıcı bağlama
    [ ] NFS istemci bağlama (autofs dahil)
    [ ] Root parolası sıfırlama (rd.break)
    [ ] Bootloader sorunlarını çözme
    [ ] journalctl ile log analizi
    [ ] Container temelleri (Podman)

## 30.2 Sınav İpuçları

1.  **Zaman yönetimi:** 2.5 saat içinde tüm görevleri tamamlamalısınız.
    Takıldığınız görevi geçin, sonra dönün.
2.  **man sayfalarını kullanın:** Sınavda internet yoktur ama man
    sayfaları mevcuttur.
3.  **Her değişikliği test edin:** Servisi yeniden başlatın, fstab'ı
    `mount -a` ile test edin.
4.  **Yeniden başlatma testi:** Tüm görevleri bitirdikten sonra `reboot`
    yapın. Sistem düzgün açılmazsa puan kaybedersiniz!
5.  **SELinux'u kapatmayın:** Sınavda SELinux enforcing olmalıdır.
6.  `firewall-cmd --permanent` **ve** `--reload`**:** Firewall
    kurallarının kalıcı olduğundan emin olun.

## 30.3 Pratik Lab Egzersizleri

### Lab 1: Kullanıcı Yönetimi

    1. "projeler" adlı bir grup oluşturun (GID: 5000)
    2. "dev1", "dev2", "dev3" kullanıcılarını oluşturun, hepsi "projeler" grubunda olsun
    3. "dev1" kullanıcısının parolası 60 günde bir değişmeli
    4. "dev2" sudo ile sadece systemctl komutunu çalıştırabilmeli
    5. "dev3" hesabı 2026-06-30'da sona erzln

### Lab 2: Dosya İzinleri ve Paylaşım

    1. /srv/proje dizini oluşturun
    2. Sahip: root, Grup: projeler
    3. Dizindeki tüm yeni dosyalar "projeler" grubunu miras alsın (SGID)
    4. Sadece dosya sahibi kendi dosyasını silebilsin (Sticky Bit)
    5. "dev1" kullanıcısına ACL ile rwx izni verin
    6. İzinler: 2770

### Lab 3: LVM ve Disk

    1. /dev/sdb üzerinde 2 GB'lık bir bölüm oluşturun
    2. Bu bölümü PV yapın
    3. "vg_lab" adlı VG oluşturun
    4. 1 GB'lık "lv_web" adlı LV oluşturun (XFS)
    5. /web dizinine kalıcı olarak bağlayın
    6. lv_web'i 1.5 GB'a genişletin

### Lab 4: Servis ve Ağ

    1. Statik IP yapılandırın: 192.168.1.50/24, GW: 192.168.1.1, DNS: 8.8.8.8
    2. Hostname: lab01.test.local
    3. Apache kurun, etkinleştirin, başlatın
    4. Firewall'da HTTP ve HTTPS açın
    5. Varsayılan hedefi multi-user.target yapın
    6. Bir cron görevi oluşturun: her gün 02:00'de /tmp'yi temizlesin

------------------------------------------------------------------------

## Son Söz

Bu kitabı tamamladığınızda, RHEL sistemlerini kurmak, yapılandırmak,
yönetmek, güvenliğini sağlamak ve sorunlarını çözmek için gerekli bilgi
ve becerilere sahip olacaksınız.

**Öğrenme yolculuğunuzda başarılar dileriz!** 🐧

### Önerilen Sonraki Adımlar

1.  **Pratik yapın:** Sanal makine ortamında sürekli egzersiz yapın
2.  **RHCSA sertifikası (EX200):** Bilginizi belgelendirin
3.  **RHCE sertifikası (EX294):** Ansible ile otomasyon uzmanlığı
4.  **Kubernetes/OpenShift:** Konteyner orkestrasyon öğrenin
5.  **Bulut:** AWS/Azure/GCP üzerinde Linux yönetimi
6.  **Topluluk:** Red Hat Community, Linux Türkiye forumlarına katılın
