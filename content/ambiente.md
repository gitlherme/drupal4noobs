# Configurando o ambiente


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

# Ao finalizar esse comando, uma senha admin será gerada, guarde ela.

# Mostrando informações da aplicação criada
lando info
```
## Acessando a aplicação
Após a aplicação ter sido criada, você pode rodar o comando `lando info` para saber onde a aplicação foi iniciada e o endereço para acessar.
![](./assets/lando-info.png)

Você pode acessar a aplicação através de qualquer um dos endereços listados acima.

Ao acessar a aplicação, você deverá se deparar com uma tela como essa.
![](./assets/aparencia-inicial.png)

## Acessando o Drupal como admin
Existem basicamente duas formas de acessar o Drupal como admin, a basta rodar o comando `lando drush uli` dentro do seu terminal, ele irá gerar uma url, basta copiar essa url e acessar, trocando o **default** pelo sua url localhost.
![](./assets/drush-uli.png)

A segunda é acessar a rota `/user` e entrar com o usuário `admin` e a senha que foi gerada ao usar o comando `lando drush site:install --db-url=mysql://drupal9:drupal9@database/drupal9 -y` nos passos acima.

Após acessar como admin, você terá acesso ao painel de controle do Drupal, como mostrado na imagem abaixo.
![](./assets/primeira-tela-admin.png)

Após isso, podemos começar a entender melhor sobre o Drupal, indo para o próximo tópico.

Ir para [Conhecendo o Drush](/content/conhecendo-o-drush.md)