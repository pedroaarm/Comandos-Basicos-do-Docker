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

criar um container
```docker container run [parâmetros] [imagem] [cmd] [argumentos]```

Ex.: ```docker container run -it --rm --name meu-primeiro-container-run python```


**Comando "Docker Container"**

Nesse exemplo usamos run para rodar o container e utilizamos a flag -it para que o terminal fosse interativo, “--rm” para que após que acabasse a execução do container ele seria removido automaticamente, em “--name” definimos o nome do container, no caso “meu-primeiro-container-run” e python é o nome da imagem (mude isso se for o seu caso), nesse caso o container exibirá um shell python (pois como não passamos argumentos no final, o container procurará o argumento padrão da imagem), um exemplo com argumentos no final é:

```docker container run -it --rm --name meu-primeiro-container-run pyt\```
   && ```hon bash```
No caso, esse comando executará um comando bash, teste!
Veja mais exemplos de flags [AQUI](https://docs.docker.com/engine/reference/commandline/container_run/)

