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
