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
CRIANDO UM APELIDO AO CONTAINER:
```bash
docker run --name <apelido do container> <nome da imagem>
```
INICIANDO UM CONTAINER EM MODO DEAMON:
```bash
docker run -d <id container>
docker run -dt --name ubuntu-server ubuntu
docker run -d --name web-server -p 80:80 nginx
```
PARANDO UM CONTAINER:
```bash
docker stop <nome do docker/id>
```
INICIA A IMAGEM INTERATIVA, O SHELL ATUAL SE TRANSFORMA NO SHELL DO CONTAINER
```bash
docker run -it rockylinux
docker run -it ubuntu bash
```
O PROMPT ABAIXO DETERMINA QUE ESTAMOS EM UM CONTAINER:
root@cb563106fcc1:/#

REMOVENDO UM CONTAINER:
```bash
docker rm <nome do docker/id>
```
SABER O CONSUMO DOS CONTAINERs:
```bash
docker stats
```
REALIZAR FAXINA NO AMBIENTE, USAR COM CUIDADO, APAGA CONTAINERs PARADOS E INTERFACE DE REDE:
```bash
docker system prune <all>
```