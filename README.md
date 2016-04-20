Symfony 2.8 + Sonata Admin 2.3 + MediaBundle + RTE Boilerplate
================

This is a boilerplate based on the [numerogeek/symfony-sonata-admin](https://github.com/numerogeek/symfony-sonata-admin) repository.

This symfony2 boilerplate comes with preconfigured:

* [SonataUserBundle](https://github.com/sonata-project/SonataUserBundle) : Provides user management for your Symfony2 Project. Compatible with Doctrine ORM & ODM, and Propel.
* [SonataMediaBundle](https://github.com/sonata-project/SonataMediaBundle) : Media management bundle on steroid for Symfony2
* [CoopTilleulsCKEditorSonataMediaBundle](https://github.com/coopTilleuls/CoopTilleulsCKEditorSonataMediaBundle/blob/master/Resources/doc/install.md) : Integrates SonataMediaBundle for Symfony with CKEditor

## Installation

This boilerplate comes with all the Sonata bundles enabled and preconfigured

The easiest way to get started is to clone the repository:

```bash
# Get the latest snapshot
$ git clone https://github.com/mountain-code/symfony-sonata-media-admin myproject
$ cd myproject
$ git remote rm origin

#setup ACL (refer to the symfony documentation.
$ HTTPDUSER=`ps aux | grep -E '[a]pache|[h]ttpd|[_]www|[w]ww-data|[n]ginx' | grep -v root | head -1 | cut -d\  -f1`
$ sudo setfacl -R -m u:"$HTTPDUSER":rwX -m u:`whoami`:rwX app/cache app/logs
$ sudo setfacl -dR -m u:"$HTTPDUSER":rwX -m u:`whoami`:rwX app/cache app/logs

#composer install

$composer install

#install assets

$ php app/console assets:install --symlink

#Create schema with superadmin user with username `admin` and password `admin`

$ php app/console doctrine:database:create
$ php app/console doctrine:schema:update --force
$ php app/console doctrine:fixtures:load

#Create MediaBundle directories

$ mkdir web/uploads
$ mkdir web/uploads/media
$ chmod -R 0777 web/uploads

```

## Starter Kit

Go to http://www.myproject.local/app_dev.php/admin to access the admin and refer the sonata documentation to create new admin panel.

## RTE (CKEditor)

SonataMediaBundle comes with CKEditor. CoopTilleulsCKEditorSonataMediaBundle is already installed and configured in this
boilerplate. You can add a full featured RTE with media integration to your Admin this way:

``` php
protected function configureFormFields(FormMapper $formMapper)
{
    $formMapper
        ->add(
            'mytext',
            'ckeditor',
            array(
              'config' => array(
                'toolbar' => 'full'
              )
            )
          );
}
```
