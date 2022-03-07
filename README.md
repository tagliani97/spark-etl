# Spark Development

Imagem utilizada para o desenvolvimento, testes e debug de códigos *Spark 3.1*, com suporte para GLUE

# AWS

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

# Run

O comando a seguir, cria a primeira interação com o container após o mesmo ser criado, nele seus arquivos serão salvos e poderam ser acessado atraves do volume notebooks contido no repositório.

```sh
docker run -it -v $(pwd)/notebooks:/home/glue_user/jupyter/jupyter_workspace -p 8888:8888 -p 4040:4040 --name spark-etl tagliani_97/spark-etl
```

# Jupyter Lab

Para acessar o jupyter no navegador, após a execução do RUN rodar o seguinte comando, no path
/home/glue_user/workspace

```sh
bash start.sh
```

### Portas

+ Jupyter Notebook: `8888`
+ Console Spark: `4040`

## Build

```sh
docker image build -t <<IMG_NAME> .
```