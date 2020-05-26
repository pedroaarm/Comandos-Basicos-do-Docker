# Comandos-Basicos-do-Docker
Alguns comandos pra quem está iniciando no Docker não sse perder
Abaixo, segue alguns comandos trivias do docker, muito importante para quem está iniciando no estudo.


Alguns comandos básico Docker

**Comando "Docker Image"**

Listar todas as imagens, os dois comandos abaixo fazem exatamente o mesmo trabalho

```docker image list```
ou
```docker image ls```

Baixar uma imagem, o comando abaixo baixará a imagem desejada a partir do docker hub:
```docker image pull $nome da imagem$```

Ex.: ```docker image pull python```

Ex2. ```docker image pull clojure```

Para listar os dados de uma imagem, tais como tamanho, hostname,etc...,
```docker inspect $nome da imagem$```

**Comando "Docker Container"**


criar um container
```docker container run [parâmetros] [imagem] [cmd] [argumentos]```

Ex.: ```docker container run -it --rm --name meu-primeiro-container-run python```




Nesse exemplo usamos run para rodar o container e utilizamos a flag -it para que o terminal fosse interativo, “--rm” para que após que acabasse a execução do container ele seria removido automaticamente, em “--name” definimos o nome do container, no caso “meu-primeiro-container-run” e python é o nome da imagem (mude isso se for o seu caso), nesse caso o container exibirá um shell python (pois como não passamos argumentos no final, o container procurará o argumento padrão da imagem), um exemplo com argumentos no final é:

```docker container run -it --rm --name meu-primeiro-container-run pyt\```
   && ```hon bash```
No caso, esse comando executará um comando bash, teste!
Veja mais exemplos de flags [AQUI](https://docs.docker.com/engine/reference/commandline/container_run/)

Para listar o container, assim como a image, utiliza-se o comando “ls” ou list, acrescentando-se (se necessário) algumas flags, que podem ser vistas aqui: https://docs.docker.com/engine/reference/commandline/container_ls/

```docker container ls```

Parar um container -> ```docker contaienr stop nome_ou_id_do_container```

caso deseje reiniciar um container, basta utilizar -> ```docker container start nome_ou_id_do_container```

Mapeamento de volume: Basicamente, a flag “-v” permite que tudo que for gravado no container será gravado em uma pasta do host, modelo:

```docker container run  -v <host> : <container> nome_imagem```

Mapeamento de porta: Mapeia qual porta do host vai ser mapeada e qual porta do container vai receber a conexão.

```docker container run -p  “<host>:<container>” nome_imagem```
```ex.: docker container run -it --rm -p 80:8000 python```

Ou seja, nesse exemplo a porta 80 do host receberá uma certa informação e mandata para a porta 8000 do container.

##### Gerenciar Recursos

Para limitar o uso de RAM, você poderá utilizar a flag “-m” mais o valor em MB que deseja limitar, exemplo:

``` docker container run -it --rm -m 240M python```

isso quer dizer que você está limitando o container a usar 240 MB de memória RAM.

Gerenciar o uso da CPU: Para balancear o uso da CPU, utilizamos a flag “-c” acompanhado pelo peso do balanceamento, que varia de 0 a 1024, quanto menor o peso, menor será a prioridade de uso, o valor padrão dessa flag é 1024, ou seja, se não for especificado, o container está livre para usar a quantidade de CPU que achar necessário, por exemplo:

```docker container run --it --rm -c 100 python```


Criar sua propria imagem Docker.

Quase sempre será necessário criar imagens modificadas, a melhor forma é utilizando o arquivo Dockerfile, porém existe o comando “commit” (que quase nunca é utilizado), aqui trataremos do arquivo Dockerfile, que é basicamente um arquivo onde você coloca todos os comandos necessários para criar imagem

Inicialmente, crie um arquivo com o nome “Dockerfile”, é muito importante que a escrita seja exatamente assim.
Dentro do Dockefile estará os comando para a criação da imagem (você pode ver os comandos clicando [AQUI] (https://docs.docker.com/engine/reference/builder/), crie também um arquivo chamado "teste".

um exemplo do Dockerfile 

```
FROM ubuntu:19.10
RUN apt-get update && apt-get install nginx 
COPY teste /tmp/teste
CMD bash
```

O comando FROM especifica que a imagem base do nosso container é o ubuntu versão 19.10, logo abaixo, temos o comando RUN, que é basicamente os comando que serão executados no container depois da criação da imagem basica, nesse caso estamos fazendo o update do sistema e instalando o nginx.
o comando COPY, muito utilizado para enviar arquivos de configuração de ambiente para produção. Nesse caso, apenas copiamos um arquivo chamado teste (que no caso, deve estar presente na diretorio do Dockerfile) e colei em /tmp/teste no container
 
