

# symfony 5 in a NUTshell
symfony practice

### things to install:
//TODO به اینا لینک و کد اضافه کن

 - [composer](https://getcomposer.org/download/) (global) [2](https://www.ionos.com/community/hosting/php/install-and-use-php-composer-on-ubuntu-1604/)
 - php
 - symfony
 - [elastic search](https://www.digitalocean.com/community/tutorials/how-to-install-and-configure-elasticsearch-on-ubuntu-16-04)
 - PHPStorm
	 - PHP Annotations
	 - and Symfony plugin

and other stuff :)))

to check requirements on machine [link](https://symfony.com/doc/current/setup.html#technical-requirements) 

symfony check:requirements

everything is fine, next:

 - full bundle:
	 - `symfony new my_project_name --full`
 - command line app:
	 - `symfony new my_project_name`
 - to set  versions at lts or currently developing version:
	 - `symfony new my_project_name --version=lts`
	 - `symfony new my_project_name --version=next`
 - demo project
	 - `symfony new my_project_name --demo`

 
 
start server: `symfony server:start`  
default server: `http://localhost:8000/`  
information about the project: `php bin/console about`
to automate downloading [bundles](https://symfony.com/doc/current/bundles.html) and the most common tasks of Symfony applications we use Flex.
به زبان ساده کامندهایی به کامپوزر اضافه می‌کنه که استفاده ازش رو راحت می‌کنه. مثلا قبلا باید کلی می‌نوشتی الان یه کلمه می‌نویسی فلان چیز رو بگیر و می‌گیره
we call bundel**s** as **recepie** 

to add Flex: `composer require symfony/flex` [more here](https://symfony.com/doc/current/setup/flex.html)

to add more bundles and recepie:
`composer require annotations asset orm-pack twig logger mailer form security translation validator`
to be in dev env:
`composer require `**`--dev`**` dotenv maker-bundle orm-fixtures profiler`


Reinstall all dependencies: ( puting junk in config/ )
```bash
 $ rm -rf vendor/*
 $ composer install
 ```
 default services in [services.yaml](https://github.com/symfony/recipes/blob/master/symfony/framework-bundle/3.3/config/services.yaml)
//TODO 6 and after from flex are not done [link](https://symfony.com/doc/current/setup/flex.html)


**packs**: include several dependencies:

 - `composer require --dev debug` installs
	 - `symfony/debug-pack` contains
		 - `symfony/debug-bundle`
		 - `symfony/monolog-bundle`
		 - `symfony/var-dumper`
# First Page:
### create a Controller:
in namespace controller create a class containing functions:
```php
<?php
namespace App\Controller;
use Symfony\Component\HttpFoundation\Response;
class Main
{
    public function main()
    {
        return new Response(
            '<html><body>hello world!</body></html>');
    }
}
```
### route by yaml (not suggested)
```yml
main:
    path: /main
    controller: App\Controller\Main::main
```
### route by annotation:
install annotations: `composer require annotations` (thx flex)
on top of each function or class as an annotation:

**`@Route("/main", name="myRoute")`**

 - to see list of all routes:
	 - `php bin/console debug:router`
- to see more detail on one specific route:
	- `php bin/console debug:router route_name`
- to see what route matches
	- php bin/console router:match /route/address

route table has 4 properties:  
  
|Name   |Method|Scheme|Host|Path|  
|-------|------|------|----|----|  
|myRoute|ANY   |ANY   |ANY |main|

to use twig our controller should `extends AbstractController`

 @Route attributes
 - `name="myRoute"` set a name
 - set methods from HTML verbs`methods={"GET"}`
	 - POST - GET - PUT - PATCH - DELETE
 - route can contain condition based on context from request



## Services
- to see all services:
	- `php bin/console debug:container`
- to see more detail on one specific service:
	- `php bin/console debug:container ServiceName`
	
Autoconfigure sets the tags for us.

## DB
no direct component for DB but we can use `Doctrine`
Doctrine = 
- ORM (Object Relational Mapping)
	- mapping objects to classes and vice versa
- ODM (Object Document Mapper)
	- used for MongoDB (NoSQL)
- DBAL (DB Abstraction Layer)
	- Abstraction over PHP PDO

**to install** `composer require doctrine maker` 
to warm-up cache (not important):
`php bin/console cache:warmup --env=our_env --no-debug`

to create DB for first time:
`php bin/console doctrine:databse:create`
**to create Entity:**
`php bin/console make:entity EntityName`

- Annotations on top of class:
	- Entity
	- Table
  
after create or editing Entities generate migrations.
to generate migrations:  
`php bin/console doctrine:migrations:diff`
to use it:  
`php bin/console doctrine:migrations:migrate`
to undo migrations:  
`php bin/console doctrine:migrations:migrate prev`

