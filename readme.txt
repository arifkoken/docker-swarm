İhtiyaç duyulabilecek hazır image lar
ozgurozturknet/web
ozgurozturknet/fakedb

Clustor kurulum için gerekli kodlar
docker swarm init --advertise-addr 192.168.1.106
docker node ls
docker swarm join-token manager
docker swarm join-token worker

Swarm cluster temel işlem komutları
docker service create —name test nginx 
docker service ps
docker service inspect test
docker service logs test
docker service ps test
docker service scale test=3
docker service rm test
docker service ls

Swarm cluster global modda service oluşturma komutu
docker service create —name glb —mode=global nginx
docker service ps glb


Overlay Network  ihtiyaç duyulacak swarm özellikleri
docker network create -d overlay over-net
docker network inspect over-net
docker network ls



docker service ps web
Not: service mash test et
docker service create —name db —network overlay-net ozgurozturknet/fakedb
docker ps db

Db servisine bağlan
docker container exec -it …….. sh

Not: Vip adresini kontrol et
ping web
Not: load balancer test et
curl http://web ->

Service oluşturma, Güncelleme ve Rollback işlemleri için gerekli temel komutlar.
docker service create —name websrv —network over-net -p 8080:80 —replicas=10 ozgurozturknet/web:v1
docker service update —detach —update-delay 5s —update-parallelism 2 —image ozgurozturknet/web:v2 websrv
watch docker service ps websrv
docker service rollback —detach websrv


Docker stack deploy -c .\docker-compose.yml
docker stack services ilk stack 
