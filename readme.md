<p align="center">
  <img src="https://github.com/awelmisin/KenshiGO/assets/73443933/8f4fe2a3-e4bc-4e9e-b55f-2455d7eea9bb">
</p> 
<h1 align="center">Kenshi GO</h1>
<p align="center">
Herkese merhabalar,
<p align="center">	
Kenshi yakın zamanda .js'yi bırakıp golang'e geçti.
<p align="center">
Bu repo'da sizlere sıfırdan kurulumundan ve eğer varsa nasıl eski .js'den transfer edebileceğinizden bahsedeceğim.
<p align="center">
Lütfen bir hatayla karşılaşmamak için önce repo'ya bir göz atınız!
<p align="center">
Adım adım gittiğiniz taktirde sıkıntısız bir kurulum olacaktır. Komutları tek tek giriniz.
</p>

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
    wget https://github.com/KenshiTech/unchained/releases/download/v0.11.6/unchained-v0.11.6-docker.zip
    unzip unchained-v0.11.6-docker.zip
    cd unchained-v0.11.6-docker

  Unutmayın, son sürüm neyse onu kullanın ve dosyaları ona göre düzenleyin. 
  
  HANGİ KLASÖRDE OLDUĞUNUZA DİKKAT EDİN. DEVAM ETMEK İÇİN, ~/unchained-v0.11.6-docker#  klasöründe işlem yapmanız gerekli!


# 1.3 Node Düzenlemesi
    cp conf.worker.yaml.template conf.worker.yaml
    nano conf.worker.yaml


Burada "şimdilik" sadece bir name parametresi ekleyeceğiz. 
Ekledikten sonra böyle gözükecek:

![image](https://github.com/awelmisin/KenshiGO/assets/73443933/09fdf2d9-3a70-400d-ac2f-93ca56933d4c)

#
    log: info
name: <name>

plugins:
  uniswap:
    rpc:
      ethereum:
        - https://ethereum.publicnode.com
        - https://eth.llamarpc.com
        - wss://ethereum.publicnode.com
        - https://eth.rpc.blxrbdn.com

    tokens:
      - name: ethereum
        pair: "0x88e6a0c2ddd26feeb64f039a2c41296fcb3f5640"
        delta: 6
        invert: true
        unit: USDT

      - name: arbitrum
        pair: "0x59354356Ec5d56306791873f567d61EBf11dfbD5"
        delta: 0
        invert: false
        unit: ETH

      - name: bitcoin
        pair: "0x9db9e0e53058c89e5b94e29621a205198648425b"
        delta: 2
        invert: false
        unit: USDT

CTRL+X Y ve Enter yaparak kaydedelim ve çıkalım.

# 1.4 Node Çalıştırma
    ./unchained.sh worker up 
![image](https://github.com/awelmisin/KenshiGO/assets/73443933/657b5a64-4067-47f2-9ee3-b67bb8dd0b04)

Docker'ı aktif hale getirelim ve başlatalım. Eğer üstteki ekran geldiyse işlem tamam demektir. Leaderboard'dan kendinize bakabilirsiniz.
Eğer sıfırdan kuruyorsanız buraya kadardı. Bundan sonrası taşıma yapmak isteyenler için. 


# 2.0 Eski Keyi Yedekleyin
    cd $home
    nano conf.yaml
Eğer daha önce .js üzerinde Kenshi kurduysanız o zaman bazı şeyler yapmanız gerekecek. Öncelikle  WinSCP ya da "nano" komutu aracılığıyla eski Kenshi'ye ait "secretKey ve publicKey" keylerini almanız gerekecek. Daha önce aldıysanız yapmanıza gerek yok.
![image](https://github.com/awelmisin/KenshiGO/assets/73443933/97ccd66e-e373-4e8e-a97f-5ed5669aec97)

Keyleri yedekledikten sonra eski .js ile çalışan Kenshi'yi kapatın. CTRL+C yapıp, "screen -ls" kullanıp, çıkan 123123.kenshi screenini "screen -X -S 123123.kenshi kill" yaparak kapatın.


# 2.1 Tekrar Node Çalıştırma
    cd unchained-v0.11.6-docker
    ./unchained.sh worker up 
![image](https://github.com/awelmisin/KenshiGO/assets/73443933/45497c0b-096d-4ea8-a6df-8a2c4cdb238f)

DOCKER klasöründe olduğunuzdan emin olduktan sonra(cd unchained-v0.11-6-docker), tekrar node'u çalıştırın.

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


CTRL+X Y ve Enter yaparak kaydedelim ve çıkalım. Screen oluşturalım.

# 2.3 Screen
    screen -S kenshi
    cd unchained-v0.11.6-docker
    ./unchained.sh worker up

Bu komutları kullanarak screen oluşturabilir ve CTRL+A ve D yaparak çıkabilirsiniz.

# 2.4 Yardımcı Olacak Komutlar
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
    ./unchained.sh worker up -d --force-recreate

eğer kopyalamada sıkıntı çıkarsa, conf klasörü içerisindeki "conf.worker.yaml" dosyasını değiştirmeyi unutmayın!
# 
    nano unchained-v0.11.6-docker/conf/conf.worker.yaml


Bu kadardı. Sizlere yardımcı olmak için hızlıca yazmaya çalıştım, 



