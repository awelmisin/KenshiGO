Herkese merhabalar,
Kenshi yakın zamanda .js'yi bırakıp golang'e geçti. Vakit kaybetmeden sizlere hızlıca sıfırdan kurulumundan ve varsa eğer nasıl eski .js'den transfer edebileceğinizden bahsedeceğim.
Adım adım gittiğiniz taktirde sıkıntısız bir kurulum olacaktır.

KURULUM
Öncelikle docker'ı yüklememiz lazım.
# 1.1 Komutları tek tek girelim.
	sudo apt update 
	sudo apt upgrade
	sudo apt install docker-compose
	sudo apt install git
	sudo apt-get update && sudo apt install jq && sudo apt install apt-transport-https ca-certificates curl software-properties-common -y && curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add - && sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu focal stable" && sudo apt-get install docker-ce docker-ce-cli containerd.io docker-compose-plugin && sudo apt-get install docker-compose-plugin
    sudo systemctl start docker

# 1.2 Kenshi Kurulumu
Daha sonrasında Kenshi Unchained sayfasından güncel release file'ı çekelim. 
(https://github.com/KenshiTech/unchained/releases bu sayfadan hangi release'in en güncel olduğunu kontrol ediniz!!)

    sudo apt install unzip
    cd $home
    wget https://github.com/KenshiTech/unchained/releases/download/v0.11.0-alpha.5/unchained-v0.11.0-alpha.5-docker.zip
    unzip unchained-v0.11.0-alpha.5-docker.zip
    cd unchained-v0.11.0-alpha.5-docker

  Unutmayın, son sürüm neyse onu kullanın ve dosyaları ona göre düzenleyin.

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
Eğer sıfırdan kuruyorsanız buraya kadardı.

# 1.5 .JS'DEN GO'YA TAŞIMAK İÇİN
    cd
	  nano conf.yaml
Eğer daha önce .js üzerinde Kenshi kurduysanız o zaman bazı şeyler yapmanız gerekecek. Öncelikle  WinSCP ya da "nano" komutu aracılığıyla eski Kenshi'ye ait "secretKey ve publickey" keylerini almanız gerekecek.

![image](https://github.com/awelmisin/KenshiGO/assets/73443933/97ccd66e-e373-4e8e-a97f-5ed5669aec97)


Bunları aldıktan sonra 1.4'teki Node Çalıştırma eylemini yapalım ve sonra CTRL+C yaparak kurduğumuz node'u kapatalım.

![image](https://github.com/awelmisin/KenshiGO/assets/73443933/45497c0b-096d-4ea8-a6df-8a2c4cdb238f)

Bu bize bir klasör yaratmış olacak.

# 1.5.1 Key'i taşıma.
    cd conf
Bu klasörün içine girelim.

Burada "conf.worker.yaml" ve "secrets.worker.yaml" olarak iki dosya var olmuş olacak. Yedeğini aldığımız keyleri "secrets.worker.yaml" dosyasına girip değiştirelim.
#  
    nano secrets.worker.yaml

![image](https://github.com/awelmisin/KenshiGO/assets/73443933/fab49981-e7bc-4c87-af53-1b03136a285f)

CTRL+X Y ve Enter yaparak kaydedelim ve çıkalım.

"conf.worker.yaml" dosyasını da kontrol edelim ve eğer farklıysa 1.3teki gibi düzenleyelim.
# 1.6 Log
    ./unchained.sh worker logs -f
unchained'in kurulu olduğu klasöre dönerek bunu başlatıp leaderboard'da kendinizi arayabilirsiniz.

Bu kadardı. Sizlere yardımcı olmak için hızlcıa yazmaya çalıştım, conf.worker.yaml dosyasını değiştirmeyi unutmayın!




