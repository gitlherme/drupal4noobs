# Instalação do Drupal


## Requisitos
Podemos começar a instalar o Drupal de várias maneiras, aqui nesse tutorial usaremos o Lando, uma ferramenta que cria todo o nosso ambiente usando Docker por trás dos panos, assim deixamos tudo em containers, podendo parar e continuar sem problemas. Para instalarmos o Lando, primeiros precisamos ter o Docker instalado na nossa máquina. Para isso, pode ser seguido o seguinte [tutorial](https://docs.docker.com/get-docker/).

Outro ponto importante é que usaremos um ambiente Linux nesse tutorial, porém ele também servirá para Windows e MacOS, basta instalar os requisitos da forma necessária para o seu sistema operacional.

## Instalação do Lando
Para instalar o Lando, basta rodar os seguintes comandos dentro do seu terminal.
```bash
wget https://files.lando.dev/installer/lando-x64-stable.deb
sudo dpkg -i lando-x64-stable.deb
```
Você pode verificar se o Lando foi instalado com sucesso utilizando o comando `lando version`.

Caso você não use Linux, poderá instalar o Lando seguindo esse [tutorial](https://docs.lando.dev/getting-started/installation.html).

## Criando a aplicação Drupal
Para criar uma aplicação Drupal, você pode rodar os seguintes comando:
```bash
# Criando a pasta example-project, entrando nela e iniciando uma aplicação Drupal 9 utilizando a receita do Lando.
mkdir example-project \
  && cd example-project \
  && lando init \
    --source remote \
    --remote-url https://www.drupal.org/download-latest/tar.gz \
    --remote-options="--strip-components 1" \
    --recipe drupal9 \
    --webroot . \
    --name example-project

# Iniciando o projeto (aqui o Lando cria o container com as imagens do banco de dados e servidor).
lando start

# Instalando o Drush, uma ferramenta de linha de comando que vamos entender melhor um pouco mais pra frente
lando composer require drush/drush

# Utilizando o Drush para instalar o Drupal
lando drush site:install --db-url=mysql://drupal9:drupal9@database/drupal9 -y

# Mostrando informações da aplicação criada
lando info
```



Ir para [Content Types](/content/content-types.md)