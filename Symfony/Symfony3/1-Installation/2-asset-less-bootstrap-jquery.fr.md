# Installation de Bootstrap et Jquery avec Composer

Ce Document présente l'installation de Bootstrap, Jquery et un compilateur Less avec Composer pour Symfony 3.
Beaucoup de documentation proposent d'utiliser le compilateur lessphp de leafo avec symfony, seulement il ne sait pas compiler Boostrap 3.3. Je vous propose donc une alternative avec less.php de oyejorge.

## 1 - Installation de Assetic

```shell
$ composer require symfony/assetic-bundle
```

Puis ajouter les assetic

```php
# app/AppKernel.php
new Symfony\Bundle\AsseticBundle\AsseticBundle(),
```

## 2 - Installation de less.php

```shell
$ composer require oyejorge/less.php
```

Éditer le fichier de configuration, pour ajouter less.php en tant que filtre :

```php
# app/config/config.yml

assetic:
    debug:          '%kernel.debug%'
    use_controller: '%kernel.debug%'
    filters:
        cssrewrite: ~
        lessphp:
            file: %kernel.root_dir%/../vendor/oyejorge/less.php/lessc.inc.php
            apply_to: '\.less$'
```

## 3 - Installation de Boostrap

```shell
$ composer require twbs/bootstrap
```

On défini les themes bootstrap dans symfony et on créé des alias pour boostrap
```php
# app/config/config.yml
twig:
    debug:            "%kernel.debug%"
    strict_variables: "%kernel.debug%"
    form_themes:
        # Default:
        - form_div_layout.html.twig

        # Bootstrap:
        - bootstrap_3_layout.html.twig
        - bootstrap_3_horizontal_layout.html.twig
assetic:
    assets:
        bootstrap_js:
            inputs:
                - '%kernel.root_dir%/../vendor/twbs/bootstrap/js/affix.js'
                - '%kernel.root_dir%/../vendor/twbs/bootstrap/js/alert.js'
                - '%kernel.root_dir%/../vendor/twbs/bootstrap/js/button.js'
                - '%kernel.root_dir%/../vendor/twbs/bootstrap/js/carousel.js'
                - '%kernel.root_dir%/../vendor/twbs/bootstrap/js/collapse.js'
                - '%kernel.root_dir%/../vendor/twbs/bootstrap/js/dropdown.js'
                - '%kernel.root_dir%/../vendor/twbs/bootstrap/js/modal.js'
                - '%kernel.root_dir%/../vendor/twbs/bootstrap/js/tooltip.js'
                - '%kernel.root_dir%/../vendor/twbs/bootstrap/js/popover.js'
                - '%kernel.root_dir%/../vendor/twbs/bootstrap/js/scrollspy.js'
                - '%kernel.root_dir%/../vendor/twbs/bootstrap/js/tab.js'
                - '%kernel.root_dir%/../vendor/twbs/bootstrap/js/transition.js'
              filters: [?yui_js]
        bootstrap_less:
            inputs:
                - '%kernel.root_dir%/../vendor/twbs/bootstrap/less/bootstrap.less'
            filters: [lessphp]
```

## 4 - Installation de Jquery

```shell
$ composer require components/jquery
```

Puis on créé les alias :

```php
# app/config/config.yml
assetic:
    assets:
        jquery_js:
            inputs:
                - '%kernel.root_dir%/../vendor/components/jquery/jquery.js'
            filters: [?yui_js]
```
            
## 5 - Utilisation

Inserer les CSS :

```html
{% block stylesheets %}
    {% stylesheets '@bootstrap_less' combine=true filter='cssrewrite' %}
    <link href="{{ asset_url }}" type="text/css" rel="stylesheet" />
    {% endstylesheets %}
{% endblock %}
```

Insere les fichiers JS :

```html
{% block body %}{% endblock %}
{% block javascripts %}
    {% javascripts '@jquery_js' '@bootstrap_js' filter='?yui_js' combine=true %}
    <script src="{{ asset_url }}"></script>
    {% endjavascripts %}
{% endblock %}
```
            

