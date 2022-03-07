## Spark Development

Imagem utilizada para o desenvolvimento, testes e debug de códigos *Spark 3.1*, com suporte para GLUE

## AWS

As conexões aos serviços aws são feitos através da **Access Key** e **Secret Key** do usuário *IAM* que deverão ser passadas para o container como variáveis de ambiente (`AWS_ACCESS_KEY_ID` e `AWS_SECRET_ACCESS_KEY`)

OU

A conexão poderá ser feita, atraves da criação da pasta .aws, no diretorio do repositorio.
Seguindo a seguinte estrutura

 - config
 - credentials

Que após a criação poderá ser copiado para dentro do container da seguinte forma

```sh
    docker cp .aws/ nome_container:/home/glue_user/
```

## Docker Hub

Para usufruir da imagem basta fazer o pull do docker hub.

```sh
    docker pull tagliani30/spark-etl:3.1.1
```

## Run

O comando a seguir, cria a primeira interação com o container.

```sh
docker run -it -p 8888:8888 -p 4040:4040 --name spark-etl tagliani30/spark-etl:3.1.1
```

Caso queira alocar um volume ao container, e acessar os notebooks que estão sendo executando
dentro do mesmo basta, criar uma pasta chamado notebooks, dentro do repositorio, e rodar o seguinte comando.

```sh
docker run -it -v $(pwd)/notebooks:/home/glue_user/jupyter/jupyter_workspace -p 8888:8888 -p 4040:4040 --name spark-etl tagliani30/spark-etl:3.1.1
```

## Jupyter Lab

Para acessar o jupyter no navegador, após a execução do RUN, rodar o seguinte comand dentro do container.

```sh
    bash /home/glue_user/workspace/start.sh
```

### Portas

+ Jupyter Notebook: `8888`
+ Console Spark: `4040`

### Build

Caso necessite realizar alguma alteração na imagem, basta rodar o seguinte comando, para criar
uma nova versão para mesma.

```sh
docker image build -t <<IMG_NAME> .
```

### Fonte

https://github.com/awslabs/aws-glue-libs