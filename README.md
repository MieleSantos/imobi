# imobi
Projeto Django da PyStack Week 2.0
# Configuranco projeto usando Poetry
#### O que é?

Poetry é uma ferramenta de gerenciamento de dependências do python. Auxilia na instalação de pacotes e ajuda na configuração do ambiente de desenvolvimento.

#### Para que serve?
Utilizaremos o poetry para controlar a versão das bibliotecas utilizadas para desenvolvimento do sistema. Com ele podemos baixar uma versão específica de uma biblioteca ou facilmente atualizar suas dependências.

Ele também nos ajuda a manter um ambiente isolado de desenvolvimento entre pacotes e dependências.

O poetry nos ajuda a ter um ambiente separado para cada projeto.

### Como instalar?

`curl -sSL https://raw.githubusercontent.com/python-poetry/poetry/master/get-poetry.py | python3 -`

Abra um terminal e digite:

`poetry --version`

Obs: `caso não apareça fecha o terminal oou reiniciar o pc`

Caso já tem o `poetry.lock`, use o comando 
`poetry shell` para criar o ambiente  depois use `poetry install` ele vai instalar todas as bibliotecas do arquivo poetry.lock

Se não segue o passo a passo para configura

#### Iniciando um projeto Python

Agora com o repositório criado, vamos começar a criar um projeto Python.

Execute o comando:

`poetry init -n`

Obs:``` A opção -n evita que o poetry fique perguntando algumas opções do projeto. Considere remove-la em próximos projetos.```

Este comando iniciliza um arquivo `pyproject.toml` de configuração do projeto.

Com o projeto iniciado, vamos instalar as dependências.

Exemplo de instalação

Execute o comando:

`poetry add django`

Vamos verificar se deu tudo certo?
Execute

`poetry run python -c "import django"`

### isort

#### O que é?

isort é uma ferramenta que ordena de forma alfabética as importações, separando as bilbiotecas que são padrões da linguagem, as externas ao sistema e as nativas do próprio sistema.

#### Para que serve?

O isort irá modificar o seu código ordenando as importações alfabéticamente. Dessa forma, o bloco de importações fica organizado e padronizado no projeto.

#### Como instalar

Execute o comando abaixo:

`poetry add isort --dev`
Obs: `Utilizamos a opção --dev pois é um pacote necessário somente durante o desenvolvimento e não durante a execução do software.`

#### Configuração

Precisamos adicionar no arquivo `pyproject.toml` a seguinte configuração
```bash
   [tool.isort]
   profile = "black"
   line_length = 80
```
Como executar
`poetry run isort .`

#### Black

#### O que é?

Black é o formatador de código Python intransigente. Ao usá-lo, você concorda em ceder o controle sobre as minúcias da formatação manual. Em troca, o black dá a você velocidade, determinismo e liberdade do irritante pycodestyle sobre formatação. Você economizará tempo e energia mental para assuntos mais importantes.

#### Para que serve?

O black é um formatador automático de código, ele irá modificar o seu código seguindo o guia de estilo do Python. Iremos configurá-lo junto ao nosso editor para que a formatação seja feita através de um atalho do teclado como shift + ctrl + i.

Como instalar
Execute o comando abaixo:

`poetry add black --dev`

#### Configuração

Precisamos adicionar no arquivo pyproject.toml a seguinte configuração
```bash
[tool.isort]
profile = "black"
line_length = 80
```
Como executar
`poetry run black .`

Para remover uma biblioteca com poetry:
```bash
poetry remove <nome>
```

Habilitar ambiente virtual:
```bash
poetry shell
```

Para instalar a partir dos arquivos poetry.lock
```bash
poetry install
```

# DJANGO

## Criando um projeto

você precisará gerar automaticamente algum código que estabeleça um projeto Django - uma coleção de configurações para uma instância do Django, incluindo configuração de banco de dados, opções específicas do Django e configurações específicas do aplicativo.

Na linha de comando, `cd` em um diretório onde deseja armazenar seu código, execute o seguinte comando:

```bash
django-admin startproject mysite
```
Estrutura do projeto
```bash
mysite/
   manage.py
   mysite/
      __init__.py
      settings.py
      urls.py
      asgi.py
      wsgi.py
```
Esses arquivos são:

- O `mysite/diretório` raiz externo é um contêiner para seu projeto. Seu nome não importa para Django; você pode renomeá-lo como quiser.

- `manage.py`: Um utilitário de linha de comando que permite que você interaja com este projeto Django de várias maneiras. Você pode ler todos os detalhes sobre `manage.py` em `django-admin` e `manage.py`.

- O `mysite/diretório` interno é o pacote Python real para seu projeto. Seu nome é o nome do pacote Python que você precisará usar para importar qualquer coisa dentro dele (por exemplo `mysite.urls`).

- `mysite/__init__.py`: Um arquivo vazio que informa ao Python que este diretório deve ser considerado um pacote Python. Se você for um iniciante em Python, leia mais sobre pacotes na documentação oficial do Python.
- `mysite/settings.py`: Definições /settings para este projeto Django. As configurações do Django lhe dirão tudo sobre como as configurações funcionam.
- `mysite/urls.py`: As declarações de URL para este projeto Django; um `índice` do seu site com Django. Você pode ler mais sobre URLs no URL dispatcher .
- `mysite/asgi.py`: Um ponto de entrada para servidores da web compatíveis com ASGI para atender ao seu projeto. Veja Como implantar com ASGI para mais detalhes.
- `mysite/wsgi.py`: Um ponto de entrada para servidores da web compatíveis com WSGI para servir ao seu projeto. Veja Como implantar com WSGI para mais detalhes.
### O servidor de desenvolvimento
Vamos verificar se seu projeto Django funciona. Mude para o mysite diretório externo , se ainda não o fez, e execute os seguintes comandos:

```bash
python manage.py runserver
```

### Criando o aplicativo
Agora que seu ambiente - um projeto` - está configurado, você está pronto para começar a trabalhar.

Cada aplicativo que você escreve em Django consiste em um pacote Python que segue uma certa convenção. Django vem com um utilitário que gera automaticamente a estrutura básica de diretórios de um aplicativo, para que você possa se concentrar em escrever código em vez de criar diretórios
```bash
django-admin startapp bigdata_app
```
Estrutura
```bash
bigdata_app/
   __init__.py
   admin.py
   apps.py
   migrations/
      __init__.py
   models.py
   tests.py
   views.py
```

### Migrate
O comando `migrate` analisa a configuração do `INSTALLED_APPS` e cria todas as tabelas de banco de dados necessárias de acordo com as configurações do banco de dados no arquivo `mysite/settings.py` e as migrações de banco de dados enviadas com o aplicativo. Você verá uma mensagem para cada migração aplicada. Se você estiver interessado, execute o cliente de linha de comando para seu banco de dados e digite `\dt(PostgreSQL), (MariaDB, MySQL), (SQLite) ou (Oracle)` para exibir as tabelas que o Django criou.`SHOW TABLES`;.`schema SELECT TABLE_NAME FROM USER_TABLES;`
```bash
python manage.py migrate  
```

### Makemigrations
Ao executar `makemigrations`, você está dizendo ao Django que fez algumas alterações em seus modelos (neste caso, você fez novos) e que gostaria que as alterações fossem armazenadas como uma migração.

As migrações são como o Django armazena as mudanças em seus modelos (e, portanto, em seu esquema de banco de dados) - eles são arquivos em disco. Você pode ler a migração para o seu novo modelo, se desejar; é o arquivo `polls/migrations/0001_initial.py`. Não se preocupe, não se espera que você os leia toda vez que o Django fizer um, mas eles foram projetados para serem editáveis ​​por humanos no caso de você querer ajustar manualmente como o Django muda as coisas.

```bash
python manage.py makemigrations
```
Para ver o SQL que essa migração executaria, usadmos o comando `sqlmigrate` que recebe nomes de migração e retorna seu SQL:

```bash
python manage.py sqlmigrate  <name_app> <migrate_name>
```

### Docker
   Instalação
   `https://docs.docker.com/engine/install/ubuntu/`


Verificar as informações do docker
```bash
docker info
```
Verificar a versão do docker
```bash
docker version
```
Lista as imagens que temos baixadas
```bash
docker images
```
Verificar o status do conteiner
```bash
docker ps
```
Verfirificar as configurações de um container
```bash
docker inspect (id da imagem ou container)
```
Inicializar um container
```bash
docker start (id do container)
```
Parar um container
```bash
docker stop (id ou nome container)
```

### Instalando Postgres com DOCKER

##### Atributo `-d`

Este parâmetro determina que o container em questão será executado como um serviço em background
##### Porta Externa

Por padrão, o Postgres roda na porta 5432, mas isso fica disponível apenas dentro do container, para permitir que ele acessado pela máquina local, precisamos fazer um mapping da porta interna, para porta externa. 

Fazemos isso com o parametro `-p`, logo após, indicamos uma porta local e para qual porta deve redirecionar
por exemplo:
```bash
 -p 5432:5432
```

##### Definindo senha e usuario

Para definirmos qual a senha do banco, devemos alterar uma variável de ambiente `-e`
por exemplo:

Senha

```bash
-e POSTGRES_PASSWORD=suasenha
```
Usuario

```bash
-e POSTGRES_USER=user
```

##### Volume

padrão, todos os dados são armazenados internamente dentro do container, e quando paramos ele, perdemos tudo. 
Para que possamos gravar os dados permanente, utilizaremos os `volumes do docker`, iremos definir uma pasta da máquina que será responsável pelo armazenamento,

Exemplo:

Criei uma pasta com o nome database no diretório `/home/derpy/Documentos/database_postgres`. Feito isto, vamos mapear a pasta de armazenamento dentro do container, para nossa pasta que criamos, para fazer esse mapeamento usamos o `-v`

```bash
-v /home/derpy/Documentos/database_postgres:/var/lib/postgresql/data
```

Agora só roda o comando:

```bash
docker run -d -i -t -p 5432:5432 -v /home/derpy/Documentos/database_postgres:/var/lib/postgresql/data -e POSTGRES_DB=postgres -e POSTGRES_USER=postgres -e POSTGRES_PASSWORD=postgres postgres:13-alpine
```


### Conectar ao Postgresql em um contêiner docker local

Com as porta 5432 do seu contêiner para a porta 5432 do seu servidor.`-p <Host_port>:<container_port>`.
O postgres está acessível a partir do seu `public-server-ip:5432`

Vá para o seu localhost (onde você tem alguma ferramenta ou o cliente psql).

```bash
psql -h public-ip-server -p 5432 -U postgres
```

Exemplo

```bash
➜ psql -h 172.17.0.2 -p 5432 -U postgres
Password for user postgres: 
psql (14.1 (Ubuntu 14.1-2.pgdg20.04+1), server 13.4)
Type "help" for help.

postgres=# \l
                                 List of databases
   Name    |  Owner   | Encoding |  Collate   |   Ctype    |   Access privileges   
-----------+----------+----------+------------+------------+-----------------------
 postgres  | postgres | UTF8     | en_US.utf8 | en_US.utf8 | 
 template0 | postgres | UTF8     | en_US.utf8 | en_US.utf8 | =c/postgres          +
           |          |          |            |            | postgres=CTc/postgres
 template1 | postgres | UTF8     | en_US.utf8 | en_US.utf8 | =c/postgres          +
           |          |          |            |            | postgres=CTc/postgres
(3 rows)

postgres=# 
```


### Backup do banco de dados PostgreSQL

O PostgreSQL vem com `pg_dump`e `pg_dumpall`ferramentas que ajudam a bancos de dados de backup fácil e eficaz.

Para quem deseja ver o comando para fazer backup de bancos de dados compactado rapidamente, aqui está:

- `-h` é o host(docker)
- `-p` é a porta(docker)

```bash
pg_dump -h 172.17.0.2 -p 5432 -d postgres -U postgres | gzip > test_db_backup.sql.gz

```

OBS: Caso aconteça o seguinte error:

```bash
pg_dump: server version: 13.4; pg_dump version: 10.19 (Ubuntu 10.19-0ubuntu0.18.04.1) 
pg_dump: aborting because of server version mismatch
```

Você tera que atualizar o postgresql-client para versão pedida, para uso execute os comandos e
especifique a versão do postgresql-client
```bash
➜ sudo sh -c 'echo "deb http://apt.postgresql.org/pub/repos/apt/ `lsb_release -cs`-pgdg main" >> /etc/apt/sources.list.d/pgdg.list'
➜ wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | sudo apt-key add -
➜ sudo apt-get update
➜ sudo apt-get install -y postgresql-client-13
```

Mais referência: https://computingforgeeks.com/how-to-install-postgresql-13-on-ubuntu/
