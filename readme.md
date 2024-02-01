<p align="center">
  <img src="https://github.com/awelmisin/KenshiGO/assets/73443933/8f4fe2a3-e4bc-4e9e-b55f-2455d7eea9bb">
</p> 

Herkese merhabalar,
Kenshi yakın zamanda .js'yi bırakıp golang'e geçti.

Bu repo'da sizlere sıfırdan kurulumundan ve eğer varsa nasıl eski .js'den transfer edebileceğinizden bahsedeceğim.
Lütfen bir hatayla karşılaşmamak için önce repo'ya bir göz atınız!
Adım adım gittiğiniz taktirde sıkıntısız bir kurulum olacaktır.


ARKADAŞLAR LÜTFEN OLDUĞUNUZ KLASÖRE DİKKAT EDİN. DOCKER KLASÖRÜNDE YAZMANIZ GEREKENİ FARKLI KLASÖRDE YAZMAYIN.

# KURULUM
Öncelikle docker'ı yüklememiz lazım.
# 1.1 Sunucu Güncellemesi ve Docker Kurulumu
	sudo apt update 
	sudo apt upgrade
	sudo apt install docker-compose
	sudo apt install git
	sudo apt-get update && sudo apt install jq && sudo apt install apt-transport-https ca-certificates curl software-properties-common -y && curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add - && sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu focal stable" && sudo apt-get install docker-ce docker-ce-cli containerd.io docker-compose-plugin && sudo apt-get install docker-compose-plugin
    sudo systemctl start docker

# 1.2 Kenshi Kurulumu
Daha sonrasında Kenshi Unchained sayfasından güncel release file'ı çekelim. 
(https://github.com/KenshiTech/unchained/releases bu sayfadan hangi release'in en güncel olduğunu kontrol ediniz!!)

Komutları tek tek yazınız.

    sudo apt install unzip
    cd $home
    wget https://github.com/KenshiTech/unchained/releases/download/v0.11.0-alpha.5/unchained-v0.11.0-alpha.5-docker.zip
    unzip unchained-v0.11.0-alpha.5-docker.zip
    cd unchained-v0.11.0-alpha.5-docker

  Unutmayın, son sürüm neyse onu kullanın ve dosyaları ona göre düzenleyin. 
  
  HANGİ KLASÖRDE OLDUĞUNUZA DİKKAT EDİN. DEVAM ETMEK İÇİN, ~/unchained-v0.11.0-alpha.5-docker#  klasöründe işlem yapmanız gerekli!


# 1.3 Node Düzenlemesi
    cp conf.worker.yaml.template conf.worker.yaml
    nano conf.worker.yaml


Burada "şimdilik" sadece bir isim parametresi ekleyeceğiz. 
Ekledikten sonra böyle gözükecek:

![image](https://github.com/awelmisin/KenshiGO/assets/73443933/09fdf2d9-3a70-400d-ac2f-93ca56933d4c)

CTRL+X Y ve Enter yaparak kaydedelim ve çıkalım.

# 1.4 Node Çalıştırma
    ./unchained.sh worker up 
![image](https://github.com/awelmisin/KenshiGO/assets/73443933/657b5a64-4067-47f2-9ee3-b67bb8dd0b04)

Docker'ı aktif hale getirelim ve başlatalım. Eğer üstteki ekran geldiyse işlem tamam demektir. Leaderboard'dan kendinize bakabilirsiniz.
Eğer sıfırdan kuruyorsanız buraya kadardı. Bundan sonrası taşıma yapmak isteyenler için. 


# 2.0 .JS'DEN GO'YA TAŞIMAK İÇİN
    cd $home
    nano conf.yaml
Eğer daha önce .js üzerinde Kenshi kurduysanız o zaman bazı şeyler yapmanız gerekecek. Öncelikle  WinSCP ya da "nano" komutu aracılığıyla eski Kenshi'ye ait "secretKey ve publicKey" keylerini almanız gerekecek. Daha önce aldıysanız yapmanıza gerek yok.
![image](https://github.com/awelmisin/KenshiGO/assets/73443933/97ccd66e-e373-4e8e-a97f-5ed5669aec97)
Keyleri yedekledikten sonra eski .js ile çalışan Kenshi'yi kapatın. CTRL+C yapıp, "screen -ls" kullanıp, çıkan 123123.kenshi screenini "screen -X -S 123123.kenshi kill" yaparak kapatın.


# 2.1 Tekrar Node Çalıştırma
    cd unchained-v0.11.0-alpha.5-docker
    ./unchained.sh worker up 
![image](https://github.com/awelmisin/KenshiGO/assets/73443933/45497c0b-096d-4ea8-a6df-8a2c4cdb238f)

DOCKER klasöründe olduğunuzdan emin olduktan sonra(cd unchained-v0.11.0-alpha.5-docker), tekrar node'u çalıştırın.

Bu bize "conf" adında yeni bir klasör yaratmış olacak. CTRL+C yaparak durduralım.

# 2.2 Key'i taşıma.
    #daha önce düzenlediğimiz dosyayı buraya kopyalayalım. komutu tek tek girin.
    cp -f conf.worker.yaml conf/conf.worker.yaml
    cd conf

DOCKER Klasörünün içerisindeyken, bu "conf" klasörünün içine girelim.

Burada "conf.worker.yaml" ve "secrets.worker.yaml" olarak iki dosya var olmuş olacak. 
#  
    nano secrets.worker.yaml

Öncesinde yedeğini aldığımız keyleri "secrets.worker.yaml" dosyasına girip değiştirelim.

![image](https://github.com/awelmisin/KenshiGO/assets/73443933/fab49981-e7bc-4c87-af53-1b03136a285f)


CTRL+X Y ve Enter yaparak kaydedelim ve çıkalım.


# 2.3 Log
    ./unchained.sh worker logs -f
unchained'in kurulu olduğu klasöre dönerek bunu başlatıp leaderboard'da kendinizi arayabilirsiniz.

Bu kadardı. Sizlere yardımcı olmak için hızlıca yazmaya çalıştım, 

eğer kopyalamada sıkıntı çıkarsa, conf klasörü içerisindeki "conf.worker.yaml" dosyasını değiştirmeyi unutmayın!
#  
    nano unchained-v0.11.0-alpha.5-docker/conf/conf.worker.yaml




