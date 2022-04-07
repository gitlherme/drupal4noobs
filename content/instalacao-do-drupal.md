# Instalação do Drupal


## Requisitos
Para começarmos a trabalhar com o Drupal, precisamos de algumas ferramentas instaladas no nosso computador. São elas
- [PHP](https://www.php.net/manual/en/install.php)
- [Composer](https://getcomposer.org/doc/00-intro.md)
- [MySQL](https://www.digitalocean.com/community/tutorials/how-to-install-mysql-on-ubuntu-20-04-pt)

## Instalação
Existem várias maneiras de instalar o Drupal, mas a mais simples é usar o Composer. Para isso, pode-se rodar os comandos abaixo.

```bash
composer create-project drupal/recommended-project drupal 
cd drupal php -d memory_limit=256M web/core/scripts/drupal quick-start demo_umami
```

Ir para [Content Types](/content/content-types.md)