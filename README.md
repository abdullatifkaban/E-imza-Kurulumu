# Linux E-İmza Kurulum Rehberi

`ACS - ACR 38T` Model kart okuyucularının Arch Linux sistemi üzerindeki kullanımı için bu rehberi hazırladım. Farklı linux dağıtımlarını kullandıkça buraya eklemeler yapacağım.

## 1. Java Kurulumu

#### Arch Linux

E-imza araçları Java'nın 8. sürümü ile uyumlu çalışmaktadır.
```
sudo pacman -S jdk8-openjdk
```
Kurulumu kontrol edelim
```
java -version
```

## E-imza Araçlarını Yükleme

### Arch Linux

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
## Atatürk Üniversitesi E-İmza Aracını Kurma

Linux sistemlerinde E-İmza aracı `AtaBaumUbysSigner` `/root` klasörü içinde çalışıyor. Bunun için klasörü buraya kopyalayalım.

> AtaBaumUbysSigner dosyasını [buradan](AtaBaumUbysSigner.zip) indirebilirsiniz.

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
Bu işlemler bittikten sonra, hem tarayıcınızı yeniden başlattıktan sonra imza atabilirsiniz. Eğer ilk çalıştırmada `AtaBaumUbysSigner` kapanırsa yukarıdaki komutla yeniden çalıştırabilirsiniz. 