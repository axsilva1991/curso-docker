# Curso-docker
* ``docker ps`` - verifica containers em execução.
* ``docker ps -a`` - todos os containers já criados.
* ``docker run -it`` - roda o docker acessando o terminal do container criado.
* ``docker start CONTAINER_ID`` - sobe o container
* ``docker stop CONTAINER_ID`` - desce o container
###### Listando as imagens
* ``docker images``
###### Removendo containers
* ``docker rm CONTAINER_ID`` - remove o container localmente.
* ``docker container prune`` - remove todos os containers inativos.
###### Removendo imagens
* ``docker rmi image_name`` - remove as imagens.
* ``docker`` 
## Principais estados de um container
1 - Runing<br>
2 - Stoped

## Criando uma imagens Docker
* ``docker run dockersamples/static-site``

###### Expondo uma porta de comunicação do Docker
* ``docker run -d -P dockersamples/static-site`` - (P -habilita porta de comunicação aleatoria para o mundo externo) (-d - nao fique atrelado ao terminal) 

* ``docker run -d -P --name NOME_ESCOLHIDO_PARA_O_CONTAINER dockersamples/static-site`` - (P -habilita porta de comunicação aleatoria para o mundo externo) (-d - nao fique atrelado ao terminal) 

* ``docker port CONTAINER_ID`` - Mostra portas ativas.

## Editando uma variável de ambiente 
* ``docker run -d -P -e AUTHOR=""Anderson Xavier da Silva dockersamples/static-site`` - (-e - permite que voce selecione uma váriavel de ambiente.) 

## Para todos os container imediatamente
* ``docker stop -t 0 $(docker ps -q)`` 

## Criando um volume
* ``docker run -v "/var/www" ubuntu`` 
* ``docker run -it -v "C:\Users\Alura\Desktop:/var/www" ubuntu`` 
Lembrando que quando voce remove a imagen o volume fica salvo no <b>Docker Host</b>.
###### Subindo o docker usando um código externo setando a porta 8080 para a porta 3000 do meu container .
* ``docker run -d -p 8080:3000 -v "C:\docker\volume-exemplo:/var/www" -w "/var/www"  node npm start ``
``-w`` working directory onde o comando será executado.
``-d`` faz com o que o terminal não fique travado.
``-v`` determina volume

## Criando uma imagem
- Criando um arquivo Dockerfile
``FROM node:latest
MAINTAINER Anderson Xavier
COPY . /var/www
WORKDIR /var/www
RUN npm install
ENTRYPOINT npm start
EXPOSE 3000``
- Construindo a Imagem
``docker build -f .\Dockerfile -t andersonxs/node .``
- Construindo criando o container
``docker run -d -p 8080:3000 andersonxs/node``
- verificando se o container foi iniciado.
``PS C:\docker\volume-exemplo> docker ps
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
PS C:\docker\volume-exemplo> docker run -d -p 8080:3000 andersonxs/node
cc3c78440f98e4c94ac6bc117c942a16262ce36886a73274bdf2b8b3b94d6b59``

## Docker Compose
Responsável pela orquestração da subida de multiplos containers. configurado através de um arquivo <br>docker-compose.yaml<br>.
````

usando o docker compose eu posso 
``
docker-compose build - monto a imagem
docker-compose up - ativo a imagem
docker-compose down - paro a imagem
docker-compose restart - reinicia as imagens

``
