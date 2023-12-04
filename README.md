# Template para ambiente de desenvolvimento com Laravel

Este template é um projeto Laravel que usa Docker para criar um ambiente de desenvolvimento com as seguintes características:

-   Servidor web Nginx
-   Banco de dados MariaDB
-   PHP 8.2
-   Composer
-   Laravel 10.x

## Como usar este template

Siga os passos abaixo para configurar e executar este template em sua máquina local.

### Passo 1: Clonar o repositório

Use o comando `git clone` para clonar este repositório em seu diretório de preferência (subistitua caminho/para/seu/projeto pelo caminho no qual deseja clonar o repositório. EX: ~/Projects/app-laravel). Em seguida, navegue até o diretório do projeto e remova o diretório `.git` para iniciar um novo repositório.

```bash
git clone https://github.com/Alan01777/Laravel-template.git caminho/para/seu/projeto
cd caminho/para/seu/projeto
rm -rf .git
git init
```

### Passo 2: Copiar o arquivo .env

Copie o arquivo .`env.example` para um novo arquivo chamado `.env`. Este arquivo contém as variáveis de ambiente que serão usadas pelo Docker e pelo Laravel.

```bash
cp .env.example .env
```

### Passo 3: Configurar o banco de dados

Edite o arquivo `.env` e altere os valores das seguintes variáveis de acordo com as suas preferências. Exemplo:

```bash
DB_CONNECTION=mysql
DB_HOST=db
DB_PORT=3306
DB_DATABASE=laravel-template
DB_USERNAME=root
DB_PASSWORD=root
```

Estas variáveis definem o tipo de conexão, o nome do host, a porta, o nome do banco de dados, o nome de usuário, a senha e a senha do usuário root do MariaDB.

### Passo 4: Iniciar os contêineres Docker

Use o comando `docker compose up -d` para iniciar os contêineres Docker em segundo plano. Este comando irá criar e executar os seguintes serviços:

-   app: o contêiner que executa o código PHP do Laravel.
-   db: o contêiner que executa o servidor MySQL.
-   nginx: o contêiner que executa o servidor web Nginx.

Você pode verificar o status dos contêineres com o comando `docker compose ps`.

```bash
docker compose up -d
```

### Passo 5: Instalar as dependências e gerar a chave do aplicativo

Use o comando `docker compose exec` para executar comandos dentro dos contêineres. Para instalar as dependências do projeto, use o comando `composer install` dentro do contêiner app. Para gerar a chave do aplicativo Laravel, use o comando `php artisan key:generate` dentro do mesmo contêiner.

```bash
docker compose exec app bash -c "composer install"
docker compose exec app bash -c "php artisan key:generate"
```

### Passo 6: Executar as migrações do banco de dados

Para criar as tabelas do banco de dados, use o comando `php artisan migrate` dentro do contêiner app. Este comando irá executar os arquivos de migração que estão na pasta database/migrations.

Observação: Pode ser necessário esperar alguns momentos até que o container do MariaDB esteja pronto para receber novas conexões a partir do momento de sua inicialização.

```bash
docker compose exec app bash -c "php artisan migrate"
```

## Pronto!

Agora você pode acessar o seu projeto Laravel no endereço http://localhost. Você também pode acessar o banco de dados MariaDB com o cliente de sua preferência, usando as credenciais definidas no arquivo `.env`.
