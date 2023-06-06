# Orange Pi 5 için Ubuntu Kurulum Rehberi

Orange Pi 5, yüksek performanslı ve düşük maliyetli bir tek kartlı bilgisayar (SBC) olarak piyasaya sürülen popüler Orange Pi serisinin bir üyesidir. Bu rehberde, Orange Pi 5 için Ubuntu işletim sistemi kurulum adımlarını detaylı olarak anlatacağız.

## Gereksinimler

- Orange Pi 5 SBC
- MicroSD kart (en az 8 GB, sınıf 10 veya daha hızlı)
- MicroSD kart okuyucu
- HDMI monitör
- USB klavye
- İnternet bağlantısı (Ethernet veya Wi-Fi)

## Adım 1: Ubuntu İmajını İndirme

Öncelikle, Orange Pi 5 için uygun olan resmi Ubuntu Server imajını indirin. İmajı indirebileceğiniz bağlantıyı Orange Pi'nin [resmi web sitesinde](http://www.orangepi.org/html/hardWare/computerAndMicrocontrollers/service-and-support/Orange-pi-5.html) bulabilirsiniz:

[Orange Pi 5 için Ubuntu Server İmajı](https://drive.google.com/file/d/1KTxWVNmq6QAYdLAHPKBY544RSIlMGrlT/view) (focal ve jammy olmak üzere 2 farklı imaj var biz focal server indirecğiz)

İmaj dosyasını bilgisayarınıza indirin ve zip dosyasını çıkarın. İçinde bulunan .img dosyasını kullanarak SD karta yazdıracağız.

## Adım 2: SD Karta İmaj Yazdırma

SD karta imaj yazdırmak için, öncelikle [balenaEtcher](https://www.balena.io/etcher/) gibi bir SD kart yazıcı yazılımı indirin ve kurun.

1. balenaEtcher'ı açın ve "Select Image" düğmesine tıklayarak, indirdiğiniz ve çıkarttığınız Ubuntu .img dosyasını seçin.
2. "Select Target" düğmesine tıklayarak, SD kartı seçin.
3. "Flash" düğmesine tıklayarak, SD karta yazma işlemini başlatın.

Yazma işlemi tamamlandığında, balenaEtcher otomatik olarak SD kartı doğrulayacak ve yazılım başarıyla yazılıp yazılmadığını kontrol edecektir.

## Adım 3: Orange Pi 5'i Hazırlama

1. SD kartı Orange Pi 5'in SD kart yuvasına takın.
2. USB klavye ve HDMI monitörü bağlayın.
3. Ethernet kablosunu veya Wi-Fi adaptörünü bağlayarak internet bağlantısı sağlayın.
4. Orange Pi 5'i güç kaynağına bağlayarak cihazı açın.

## Adım 4: İlk Yapılandırma

Orange Pi 5 başlatıldığında, Ubuntu Server otomatik olarak SD karttan başlayacaktır. İlk yapılandırma adımlarını tamamlamanız gerekecektir:

1. İlk oturum açma ekranında (SSH için normal bağlantıda sistem direkt açılacaktır), kullanıcı adı olarak `root` ve şifre olarak `orangepi` girin.
2. Sistem güncellemelerini ve yamalarını kontrol etmek ve yüklemek için aşağıdaki komutları girin:

```bash
sudo apt update
sudo apt upgrade
```

4. Kablosuz ağ bağlantısı kullanıyorsanız, Wi-Fi yapılandırmasını gerçekleştirin:

```bash
sudo nmtui
```
`nmtui` aracını kullanarak, "Activate a connection" seçeneğini belirleyin ve Wi-Fi ağınızı seçin. Şifreyi girin ve bağlantıyı etkinleştirin.

5. Gerekli dil ve bölge ayarlarını yapılandırın:

```bash
sudo dpkg-reconfigure locales
sudo dpkg-reconfigure tzdata
```

Bu komutlar, dil ve saat dilimi yapılandırma araçlarını başlatır. İstediğiniz ayarları seçin ve onaylayın.

6. Orange Pi 5'i yeniden başlatın:

```bash
sudo reboot
```

Bu noktada, Ubuntu Server kurulumunuz tamamlanmış olmalıdır. Sistem yeniden başladığında, yeni yapılandırma ayarlarıyla oturum açabilirsiniz.

## Adım 5: NVME M.2 SSD bağlantısı (isteğe bağlı)

ÖNEMLİ !!
- Sadece SSD ile kurulum yapılamıyor önce SD karta imaj'ı yazdırıp daha sonra gerekli ayarları yaptıktan sonra SSD üzerinden boot edilebiliyor !!
- NVME M.2 SSD olarak 2230-2243 modelleri tercih ediliyor fakat 2280'ide kullanabilirsiniz

### 1.Yol

1. Yukarıda Adım 2'de yaptığımız işlemleri SSD için yapacağız, imaj seçip "Select Target" düğmesine tıklayarak SSD'mizi seçiyoruz.
2. Orange Pi 5'inizi kapatın ve güç kaynağını çıkarın.
3. NVMe M.2 SSD'yi Orange Pi 5'in M.2 yuvasına takın ve gerektiğinde vidaları kullanarak (2230-2243 için) güvenli bir şekilde sabitleyin.
4. Orange Pi 5'i tekrar güç kaynağına bağlayarak cihazı açın.
5. Orange Pi 5 başlatıldığında, terminali açarak aşağıdaki komutları girin:
```bash
sudo orangepi-config
```
6. Açılan ekranda en üst seçenekteki `System`'e giriyoruz.
![IMG_8983](https://user-images.githubusercontent.com/120671243/234844961-f09f5fb4-da09-4ec1-91f2-3693362cf1cb.jpg)

7. Daha sonra yine en üstteki seçenek olan `Install`'e giriyoruz. 
![IMG_8984](https://user-images.githubusercontent.com/120671243/234845083-bffbaa12-e863-4e35-a217-15d7d094d04e.jpg)

8. Çıkan ekranda `Install/Update the bootloade on SPI Flash`'ı okeyliyoruz, yaklaşık 5-10dk sonra kurulum tamamlanacaktır, bu noktada tekrar terminal'e geri dönebiliriz ve ardından sistemi şu komut ile kapatalım :
![IMG_8985](https://user-images.githubusercontent.com/120671243/234845434-ac1a636b-f81a-4c56-8975-c3a9f99f368b.jpg)

```bash
sudo poweroff
```

9. Artık NVME M.2 SSD ile sistemi boot edebiliriz, SD kartı çıkarıp M.2 slotuna SSD'yi takıp Orange Pi 5'i başlatabiliriz .


### 2.Yol (SSH ile Bağlantı)

1. Orange Pi 5'inizi kapatın ve güç kaynağını çıkarın.
2. NVMe M.2 SSD'yi Orange Pi 5'in M.2 yuvasına takın ve gerektiğinde vidaları kullanarak (2230-2243 için) güvenli bir şekilde sabitleyin.
3. Orange Pi 5'i tekrar güç kaynağına bağlayarak cihazı açın.
4. Bilgisayarınızdan imaj dosyasının bulunduğu klasöre giderek imajı Orange Pi 5'e kopyalayalım.

```bash
scp Orangepi5_1.1.4_ubuntu_focal_server_linux5.10.110.img root@<your_ip>:/home/orangepi
```

5. Kopyalama işlemi bittikten sonra Orange Pi 5'e SSH ile bağlanalım.

```bash
ssh root@<your_ip>
```

6. Terminalden aşağıdaki komutları girin:
```bash
sudo orangepi-config
```
6. Açılan ekranda en üst seçenekteki `System`'e giriyoruz.
![IMG_8983](https://user-images.githubusercontent.com/120671243/234844961-f09f5fb4-da09-4ec1-91f2-3693362cf1cb.jpg)

7. Daha sonra yine en üstteki seçenek olan `Install`'e giriyoruz. 
![IMG_8984](https://user-images.githubusercontent.com/120671243/234845083-bffbaa12-e863-4e35-a217-15d7d094d04e.jpg)

8. Çıkan ekranda `Install/Update the bootloade on SPI Flash`'ı okeyliyoruz, yaklaşık 5-10dk sonra kurulum tamamlanacaktır, bu noktada tekrar terminal'e geri dönebiliriz.

9. Aşağıdaki komutla imaj dosyasını kopyaladığımız klasöre gidelim:

```bash
cd /home/orangepi
```

10. İmaj dosyasını SSD diskimize yüklüyelim:

```bash
sudo dd bs=1M if=Orangepi5_1.1.4_ubuntu_focal_server_linux5.10.110.img of=/dev/nvme0n1 status=progress
```

11. Aşağıdaki komutla sistemi kapatıp sd kartımızı çıkaralım. Yeniden başlattığımızda cihamıza SSD'den başlayacak. Modem arayüzünden cihazımızın yeni IP'sinin öğrenebilirsiniz.


```
shutdown -h now
```
