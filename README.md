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
