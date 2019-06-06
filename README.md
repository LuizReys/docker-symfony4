# Ambiente para Symfony 4
Ambiente Docker para projetos Symfony 4 utilizando o compose, arquivo de configuração com variáveis de ambiente, containers Nginx, PHP-FPM e Postgres.

## Instruções
Para configurar o projeto, algumas etapas são necessárias:

## Instale o Composer
O mesmo pode ser baixado e configurado conforme documentação encontrada no link abaixo:

	https://getcomposer.org/

## Instale o GIT
O mesmo pode ser baixado e configurado conforme documentação encontrada no link abaixo:

	https://git-scm.com/

## Clone o projeto
Clone o projeto na sua máquina:

	$ git clone https://github.com/LuizReys/docker-symfony4.git

## Ajuste as variáveis de ambiente
Entre na pasta docker-symfony4 e copie o arquivo env-example para .env:

	$ cp env-example .env

## Crie os ambientes
Execute os contêineres:

	$ docker-compose up -d

## Ajuste o hosts
Adicione o domínio no arquivo de hosts:

	$ vim /etc/hosts

	172.20.128.1 myapp.desenv

## Acesse o shell do container php-fpm:
Execute o comando para acessar:

	$ docker exec -it php-fpm bash

## Configurar projeto
Para projeto novo:

	$ composer create-project symfony/website-skeleton myapp

Para projeto existente, criar diretório principal do projeto:

	$ mkdir myapp

## Acessar projeto
Abra seu navegador e acesse o endereço:
	
	http://myapp.desenv

## Pronto! Projeto configurado! :)
