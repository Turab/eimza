# eimza
Arch Linux için E-tugra, E-Güven, Tübitak vb. e-imza işlemleri için bağımlılık paketleri.

Bu paket genellikle ilgili e-imza firmasının programlarını kurmaya ihtiyaç kalmadan PTT KEP, E-Devlet gibi uygulamalarda e-imzanızı rahatlıkla kullanmanızı sağlar.

Bu paket herhangi bir program içermez. Sadece söz konusu paketlerin çalışması için gerekli bağımlılıkları kurar. Bu paketin yapılma sebebi, Türkiye'deki e-imza şirketlerinin Linux desteği vermemesidir. Sadece Windows için driver, paket ve kurulum desteği verdiklerinden dolayı Linux kullanıcıları ortada kalıyor.

Paketi `yay` veya `paru` vb. bir AUR yardımcısı ile kurabilirsiniz. (Örneğin `paru eimza`) ACS tipi kart okuyucusu olanların e-imzalarının direkt çalışması gerekir. Farklı türde cihazı olanlar (omnikey, scm vb.) kendi cihazlarına uygun sürücüyü de ayrıca kurmalıdır.

> [!IMPORTANT]
> E-imzanızın daha önceden etkinleştirilmiş ve kullanıma açılmış olması gerekiyor. E-imza firmaları Linux desteği vermediğinden dolayı etkinleştirme programları sadece Windows'ta çalışıyor. Bu nedenle Linux'ta kullanmaya başlamadan önce etkinleştirme/kullanıma açma işlemini bir defaya mahsus Windows'ta yapmanız gerekecektir.

> [!IMPORTANT]
> Kurulum tamamlandıktan sonra `pcscd` servisini çalıştırmanız gerekir:
> ```bash
> systemctl start pcscd
> ```
> Eğer sık sık e-miza kullanıyorsanız servisi etkinleştirmeyi düşünün:
> ```bash
> systemctl enable pcscd
> ```

> [!TIP]
> Linux üzerinde Java Web Start (`javaws`) (Yani .jnlp dosyası çalıştırma) desteği biraz problemli. Bu yüzden JNLP dosyası ile çalışması gereken e-imza uygulamalarını (örneğin turkiye.gov.tr 'deki E-Devlet uygulaması) önce bilgisayarınıza indirin. Ardından bir metin düzenleyici ile açarak .jar dosyasının konumunu kopyalayın ve o dosyayı bilgisayarınıza indirerek direkt çalıştırın. Dileyenler JNLP desteği için `icedtea-web` kullanabilir ancak paket artık güncellenmiyor, son sürümü 2021 yılında yayınlanmış ve yeni Java ortamları ile uyumsuzluk problemleri çıkarabiliyor.

> [!NOTE]
> PTT Kep (ve bazı benzeri uygulamalar) ek paket tanımlarına ihtiyaç duyabilir. Örnek olarak PTT KEP e-imza uygulamasının JAR dosyasını indirdikten sonra şu komutla çalıştırabilirsiniz:
> ```bash
> java --add-exports jdk.crypto.cryptoki/sun.security.pkcs11=ALL-UNNAMED --add-exports jdk.crypto.cryptoki/sun.security.pkcs11.wrapper=ALL-UNNAMED --add-opens java.base/java.security=ALL-UNNAMED --add-exports java.base/sun.security.action=ALL-UNNAMED --add-exports java.base/sun.security.rsa=ALL-UNNAMED --add-opens java.base/sun.security.util=ALL-UNNAMED -jar /dosya/konumu/PTT.jar
> ```
> Bu komutu bir `sh` dosyasına kaydedip çalıştırılabilir yapıp PTT e-imza uygulamasını onunla da başlatabilirsiniz veya örneğin masaüstü ortamında (örneğin KDE) bir menü oluşturup program olarak `java` ve parametre olarak da yukarıdaki komutun kalan kısımlarını girebilirsiniz. Böylece o menüye tıkladığınızda PTT e-imza uygulaması otomatik açılır.

> [!NOTE]
> PDF imzalamak için `jsignpdf` kullanabilirsiniz. Ayrıca LibreOffice de tüm doküman imzalamalarını destekliyor. Okular'da da e-imza desteği var ancak bunun için e-imzanızı sertifika deposuna yüklemeniz gerekiyor.
