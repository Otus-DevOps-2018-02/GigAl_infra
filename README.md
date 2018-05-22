# GigAl_infra
GigAl Infra repository
#способ подключения 
ssh -i ~/.ssh/gcpkey  gigal70@35.204.12.47 gigal70@10.146.0.3
#Cпособ подключения к someinternalhost в одну команду 

#Указываем ключь агенту  ssh-add ./путь до ключа
#подключение к серверу  10.164.0.3 через сервер  35.204.12.47
#в файл ~/.ssh/config добавляем
Host  someinternalhost	
	ForwardAgent yes
    HostName 10.164.0.3
    User gigal70
    ProxyCommand ssh -W %h:%p gigal70@35.204.12.47

#подключаемся через ssh someinternalhost	


bastion_IP = 35.204.12.47
someinternalhost_IP = 10.164.0.3


## ДЗ № 5 
testapp_IP = 35.204.173.12
testapp_port = 9292  

В процессе сделано:
Созданы скрипты для автоматического разворачивания ВМ и ПО
Создана ВМ средствами GCP
Созданы правила фаервола
Как запустить проект:
в консоле GCP

gcloud compute instances create reddit-app
--boot-disk-size=10GB 
--image-family ubuntu-1604-lts 
--image-project=ubuntu-os-cloud 
--machine-type=g1-small 
--tags puma-server 
--restart-on-failure 
--metadata-from-file startup-script=/PATH/TO/SCRIPT/startup_script.sh

возможны опции --metadata startup-script или startup-script-url

открытие портов
gcloud compute --project=infra-199614 firewall-rules create default-puma-server --allow=tcp:9292 --target-tags=puma-server
