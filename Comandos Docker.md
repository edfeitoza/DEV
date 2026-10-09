***
***
INSTALAÇÃO DO DOCKER EM UM ROCKLINUX:
(opcional) remover pacotes que podem conflitar
```bash
sudo dnf remove docker docker-client docker-common docker-engine podman runc
```
```bash
sudo dnf check-update
sudo dnf install -y dnf-plugins-core
sudo dnf config-manager --add-repo https://download.docker.com/linux/rhel/docker-ce.repo
sudo dnf install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
sudo systemctl --now enable docker
sudo systemctl status docker
```
***
MANIPULANDO IMAGENS
***

PUXANDO UMA IMAGEM DO DOCKER-HUB, SERÁ PRECISO SABER O NOME A IMAGEM:
```bash
docker pull <nome da imagem>
docker pull hello-world
```
LISTA AS IMAGENS BAIXAS:
```bash
docker images
```
RENOMEANDO AS IMAGENS
```bash
docker tag <id> <novo nome>
```
REMOVENDO AS IMAGENS OU TAGs, A PARTIR DO NOME OU ID:
```bash
docker rmi <image/tag/id>
```
***
MANIPULANDO CONTAINER
***
INICIANDO CONTAINER, CASO NÃO EXISTA A IMAGEM SOLICITADA NO COMANDO, O DOCKER BAIXARÁ A ULTIMA VERSÃO DA IMAGEM SOLICITADA:
```bash
docker run hello-world
```
INICIANDO O CONTAINER JÁ BAIXADA PELO ID:
```bash
docker run <id>
```
INICIANDO O CONTAINER A PARTIR DE UMA PORTA ESPECIFICA:
```bash
docker run -p <porta local>:<porta container> <id da imagem>
```
STATUS DOS CONTAINERS ATIVOS/RODANDO:
```bash
docker ps
```
LISTANDO TODOS OS CONTAINERs INICIADOS/PARADOS:
```bash
docker ps -a
```
INICIANDO UM CONTAINER JÁ CRIADO ANTERIORMENTE:
```bash
docker start <id>
```
PARANDO UM CONTAINER
```bash
docker stop <id>
```
RESTARTANDO UM CONTAINER
```bash
docker restart <id>
```
RENOMEANDO O CONTAINER
```bash
docker rename <id container/nome> <novo nome>
```
INSPECIONANDO UM DOCKER, CHECANDO A VARIAVEL DE AMBIENTE
```bash
docker inspect <id container/nome> 
```
CRIANDO UM APELIDO AO CONTAINER:
```bash
docker run --name <apelido do container> <nome da imagem>
```
CHECANDO RECURSOS CONSUMIDOS PELOS CONTAINER ATIVOS:
```bash
docker stats
```
RECONFIGURANDO A MEMORIA DE UM CONTAINER QUE ESTEJA RODANDO, É PRECISO ACERTAR O SWAP
```bash
docker update --memory <qtd memoria>g --memory-swap <qtd memoria>g <id container/nome>
```
ANALISANDO LOGs DO CONTAINER:
```bash
docker logs <id container/nome>
docker logs -f <id container/nome>
docker logs --tail 10 <id container/nome>
docker logs --since 1m <id container/nome>
docker logs -f --since 1m <id container/nome>
docker logs -f --tail 10 <id container/nome>
```
INICIANDO UM CONTAINER TEMPORARIO, É APAGADO AO DAR stop:
```bash
docker run --rm -d <id container/nome>
```
INICIANDO UM CONTAINER EM MODO DEAMON:
```bash
docker run -d <id container>
docker run -dt --name ubuntu-server ubuntu
docker run -d --name web-server -p 80:80 nginx
```
INICIA A IMAGEM INTERATIVA, O SHELL ATUAL SE TRANSFORMA NO SHELL DO CONTAINER
```bash
docker run -it <id container/nome> sh
docker run -it <id container/nome> bash

docker run <flags> <imagem> <comando>
            -p      id imagem sh/bash
            -d                 ls /
            -it                env
            -rm                whoami
```
O PROMPT ABAIXO DETERMINA QUE ESTAMOS EM UM CONTAINER:
root@cb563106fcc1:/#

REMOVENDO UM CONTAINER DESDE QUE ESTEJA PARADO:
```bash
docker rm <nome do docker/id>
```
REALIZAR FAXINA NO AMBIENTE, USAR COM CUIDADO, APAGA CONTAINERs PARADOS E INTERFACE DE REDE:
```bash
docker system prune <all>
```
***
MANIPULANDO VOLUMES
***
CRIANDO UM VOLUME
```bash
docker volume create <nome do volume>
```
LISTANDO VOLUMES CRIADOS
```bash
docker volume ls
```
***
EXEMPLO DE USO DOS VOLUMES
docker run --name nginx-web -p 3001:80 -d -v harddisk:/usr/share/nginx/html/ f9ea18bfa4fa
-v flag relacionada ao volume 
harddisk: nome do volume
/usr/share/nginx/html/ caminho indicado pela documentacao da imagem
***
INSPECIONANDO VOLUMES
```bash
docker volume inspect <nome do volume> 
```
REMOVENDO UM VOLUME CRIADO, só apaga se o container estiver parado.
```bash
docker volume rm <nome volume>
```
***
BIND MOUNT
***
```bash
docker run -d -v <caminho do sistema operacional>:<caminho da documentação do docker> <id da imagem>
```
