# Database, doctrine

###### To add doctrine run:
```
composer require symfony/orm-pack
composer require symfony/maker-bundle --dev
```
unless it is already included in composer.json
orm-pack is the doctrine, maker-bundle is the command line tool for making entities

###### DB configuration goes into .env in the root dir:
```
DATABASE_URL="mysql://db_user:db_password@127.0.0.1:3306/db_name"
```

###### Entity creation.
```
php bin/console make:entity
```
Then answert questions about the Entity parameters/db fields. An entity class wil be created in `src/Entity`
Available mapping types: https://www.doctrine-project.org/projects/doctrine-orm/en/latest/reference/basic-mapping.html#doctrine-mapping-types

###### Migration.
If entities were modified with the maker:
```
php bin/console make:migration
```
this will generate migration files,
```
php bin/console doctrine:migrations:migrate
```
this will apply migrations into the database.

###### Entity fetching.


###### Entity manipulation.

First get the entity manager:
```
$entityManager = $this->getDoctrine()->getManager();
```
then manipulate the entity (example entity called Product):
```
$product = new Product();
$product->setName('Keyboard');
$product->setPrice(1999);
$product->setDescription('Ergonomic and stylish!');
```
finally set the object to be updated and then call flush to write to the db all set to be updated
```
// tell Doctrine you want to (eventually) save the Product (no queries yet)
$entityManager->persist($product);

// actually executes the queries (i.e. the INSERT query)
$entityManager->flush();
```








