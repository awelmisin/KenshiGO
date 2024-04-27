<p align="center">
  <img src="https://github.com/awelmisin/KenshiGO/assets/73443933/8f4fe2a3-e4bc-4e9e-b55f-2455d7eea9bb">
</p> 
<h1 align="center">Kenshi GO</h1>
<p align="center">
Herkese merhabalar,
<p align="center">	
Kenshi yakın zamanda .js'yi bırakıp golang'e geçti.
<p align="center">
Bu repo'da sizlere sıfırdan kurulumundan bahsedeceğim. .js'den geçiş yapmak istiyorsanız ilgili rehbere yukarıdaki dosyalardan bakabilirsiniz.
<p align="center">
Lütfen bir hatayla karşılaşmamak için önce repo'ya bir göz atınız!
<p align="center">
Adım adım gittiğiniz taktirde sıkıntısız bir kurulum olacaktır. Komutları tek tek giriniz.
</p>

# Airdrop'a yaklaşıyoruz ve secrets dosyamızı düzenlememiz lazım. Linkteki kısımları uygulayın. Eğer puan kazanmıyorsanız üstteki dosyalardan ilgili sürümü seçip linke bakın.
[Link](https://github.com/awelmisin/KenshiGO/blob/main/v0.11.17%20Secrets%20Güncellemesi.md)

# KURULUM
> Öncelikle docker'ı yüklememiz lazım.
# 1.1 Sunucu Güncellemesi ve Docker Kurulumu
	sudo apt update 
	sudo apt upgrade
	sudo apt install docker-compose
	sudo apt install git
	sudo apt-get update && sudo apt install jq && sudo apt install apt-transport-https ca-certificates curl software-properties-common -y && curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add - && sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu focal stable" && sudo apt-get install docker-ce docker-ce-cli containerd.io docker-compose-plugin && sudo apt-get install docker-compose-plugin
    sudo systemctl start docker

# 1.2 Kenshi Kurulumu
> Daha sonrasında Kenshi Unchained sayfasından güncel release file'ı çekelim. 
> (https://github.com/KenshiTech/unchained/releases bu sayfadan hangi release'in en güncel olduğunu kontrol ediniz!!)

> Komutları tek tek yazınız.

    sudo apt install unzip
    cd $home
    wget https://github.com/TimeleapLabs/unchained/releases/download/v0.12.0/unchained-v0.12.0-docker.zip
    unzip unchained-v0.12.0-docker.zip
    cd unchained-v0.12.0-docker

 > Unutmayın, son sürüm neyse onu kullanın ve dosyaları ona göre düzenleyin. 
  
 > HANGİ KLASÖRDE OLDUĞUNUZA DİKKAT EDİN. DEVAM ETMEK İÇİN, ~/unchained-v0.12.0-docker#  klasöründe işlem yapmanız gerekli!


# 1.3 Node Düzenlemesi
    cp conf.worker.yaml.template conf.worker.yaml
    nano conf.worker.yaml


> Burada "şimdilik" sadece bir name parametresi ekleyeceğiz. 
> Ekledikten sonra böyle gözükecek:

![image](https://github.com/awelmisin/KenshiGO/assets/73443933/09fdf2d9-3a70-400d-ac2f-93ca56933d4c)

[conf.worker.yaml dosyası](https://github.com/awelmisin/KenshiGO/blob/main/conf.worker.yaml)
	

> CTRL+X Y ve Enter yaparak kaydedelim ve çıkalım.

# 1.4 Node Çalıştırma
    ./unchained.sh worker up 
![image](https://github.com/awelmisin/KenshiGO/assets/73443933/657b5a64-4067-47f2-9ee3-b67bb8dd0b04)

> Docker'ı aktif hale getirelim ve başlatalım. CTRL+C ile durduralım. Bu bize lazım olacak conf dosyalarını yaratacak.



# 1.5 Secrets-Conf Düzenleme
    #1.3 aşamasında düzenlediğimiz dosyayı buraya kopyalayalım. komutu tek tek girin.
    cp -f conf.worker.yaml conf/conf.worker.yaml
    cd conf

> DOCKER Klasörünün içerisindeyken, bu "conf" klasörünün içine girelim.

> Burada "conf.worker.yaml" ve "secrets.worker.yaml" olarak iki dosya var olmuş olacak. 
#  
    nano secrets.worker.yaml

> Yedeğini aldığımız keyleri "secrets.worker.yaml" dosyasına girip değiştirelim.

![image](https://github.com/awelmisin/KenshiGO/assets/73443933/fab49981-e7bc-4c87-af53-1b03136a285f)


> CTRL+X Y ve Enter yaparak kaydedelim ve çıkalım. Screen oluşturalım.

# 1.6 Screen
    screen -S kenshi
    cd
    cd unchained-v0.12.0-docker
    ./unchained.sh worker up

> Bu komutları kullanarak screen oluşturabilir ve CTRL+A ve D yaparak çıkabilirsiniz.



# 2.0 Yardımcı Olacak Komutlar
#  log için
    ./unchained.sh worker logs -f
#  restart için
    ./unchained.sh worker restart
#  başlatmak için
    ./unchained.sh worker up -d
#  durdurmak için
    ./unchained.sh worker stop
    ya da 
    CTRL+C
#  güncelleme için
    ./unchained.sh worker pull
    ./unchained.sh worker up 

> eğer kopyalamada sıkıntı çıkarsa, conf klasörü içerisindeki "conf.worker.yaml" dosyasını değiştirmeyi unutmayın!
# 
    nano unchained-v0.12.0-docker/conf/conf.worker.yaml


> Bu kadardı. Sizlere yardımcı olmak için hızlıca yazmaya çalıştım, 



