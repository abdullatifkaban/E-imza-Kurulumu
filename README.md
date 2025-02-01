# Linux E-İmza Kurulum Rehberi

![acs](acs_beyaz.png)

`ACS - ACR 38T` Model kart okuyucularının Arch Linux ve Ubuntu işletim sistemleri üzerindeki kullanımı için bu rehberi hazırladım. Farklı linux dağıtımlarını kullandıkça buraya eklemeler yapacağım.

## 1. Java Kurulumu


E-imza araçları Java'nın 8. sürümü ile uyumlu çalışmaktadır.

<details>
<summary>Arch Linux</summary>

```
sudo pacman -S jdk8-openjdk
```

Kurulumu kontrol edelim
```
java -version
```
</details>

<details>
<summary>Ubuntu</summary>

```
sudo apt install openjdk-8-jdk
```

Kurulumu kontrol edelim
```
java -version
```
</details>


## 2. E-imza Araçlarını Yükleme

<details>
<summary><b>Arch Linux</b></summary>

Usb Araçlarını kuralım
```
sudo pacman -S usbutils
```
Kart Okuyucu takılımı diye kontrol edelim
```
lsusb
```
PC/SC İstemcisi ve Kütüphaneleri:

ACR 38T kart okuyucusu için gerekli olan libpcsclite paketini yükleyelim
```
sudo pacman -S pcsclite
```
ACR 38T kart okuyucusu için özel bir sürücü gerekebilir. Genellikle, libacsccid gibi bir paket gerekebilir:
```
sudo pacman -S ccid
```
PC/SC servisini başlatmak için:
```
sudo systemctl start pcscd
```
Bu servisin sistem başlangıcında otomatik olarak başlamasını sağlayalım

```
sudo systemctl enable pcscd
```
</details>

<details>
<summary><b>Ubuntu</b></summary>

Kart Okuyucu takılımı diye kontrol edelim
```
lsusb
```
PC/SC İstemcisi ve Kütüphaneleri:

ACR 38T kart okuyucusu için gerekli olan libpcsclite paketini yükleyelim
```
sudo apt install pcscd pcsc-tools
```
Kart okuyucunun bilgisayarına bağlı olduğundan emin olmak için aşağıdaki komutu çalıştırarak okuyucunun tanınıp tanınmadığını kontrol edelim:
```
pcsc_scan
```
</details>

## 3. Atatürk Üniversitesi E-İmza Aracını Kurma

Linux sistemlerinde E-İmza aracı `AtaBaumUbysSigner` `/root` klasörü içinde çalışıyor. Bunun için klasörü buraya kopyalayalım.

> AtaBaumUbysSigner dosyasını [buradan](AtaBaumUbysSigner.zip) indirebilirsiniz.

İndirdiğiniz sıkıştırılmış dosyayı çıkardığınız klasörde aşağıdaki komutu çalıştırıp kopyalama işlemini yapalım:  

```
sudo cp -r AtaBaumUbysSigner /root
```
Yetkili kullanıcı moduna girelim
```
sudo su
```
İlgili klasöre geçelim
```
cd /root/AtaBaumUbysSigner/ 
```
`AtaBaumUbysSigner` aracını çalıştıralım
```
java -jar AtaBaumUbysSigner.jar
```
Bu işlemler bittikten sonra, hemen tarayıcınızı yeniden başlatıp ardından imza atabilirsiniz. Eğer ilk çalıştırmada `AtaBaumUbysSigner` kapanırsa yukarıdaki komutla yeniden çalıştırabilirsiniz. 

>Her seferinde çalıştırmak için yukarıdaki adımları uygulayacak bir script kullanabilirsiniz. Örnek scripti [buradan](eimza.desktop) indirebilirsiniz. İndirdiğiniz dosyayı çalıştırılabilir hale getirmek için dosyanın bulunduğu klasörde aşağıdaki terminal komutunu çalıştırın
```
chmod +x eimza.desktop
```
> Dosya ile işiniz bittiğinde kapatmak için komutun çalıştığı terminalde `Ctrl+C` kısa yolunu kullanabilirsiniz.