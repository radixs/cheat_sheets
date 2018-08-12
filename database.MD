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
Also a repository class will be created. All extra specialized methods for entity manipulation should go to this class.

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

Other way to create migraitons is via
```
php bin/console doctrine:migrations:diff
```
that will generate migration files by comparing Entities with the database.

###### Entity creation and manipulation.

First get the entity manager:
```
$entityManager = $this->getDoctrine()->getManager();
```
then create and manipulate the entity (example entity called Product):
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
Once persisted the Entity has an id:
```
$product->getId();
```

###### Entity fetching.
```
$product = $this->getDoctrine()->getRepository(Product::class)->find($id);

if (!$product) {
    throw $this->createNotFoundException(
        'No product found for id '.$id
    );
}
```
Repository is a class that helps fetching entities of a certain class.
Other methods of fetching:
```
// look for a single Product by name
$product = $repository->findOneBy(['name' => 'Keyboard']);
// or find by name and price
$product = $repository->findOneBy([
    'name' => 'Keyboard',
    'price' => 1999,
]);

// look for multiple Product objects matching the name, ordered by price
$products = $repository->findBy(
    ['name' => 'Keyboard'],
    ['price' => 'ASC']
);

// look for *all* Product objects
$products = $repository->findAll();
```
###### Deleting an entity.
```
$entityManager->remove($product);
$entityManager->flush();
```
###### Query builder example. More detailed here https://www.doctrine-project.org/projects/doctrine-orm/en/latest/reference/query-builder.html
```
// src/Repository/ProductRepository.php

// ...
class ProductRepository extends ServiceEntityRepository
{
    public function __construct(RegistryInterface $registry)
    {
        parent::__construct($registry, Product::class);
    }

    /**
     * @param $price
     * @return Product[]
     */
    public function findAllGreaterThanPrice($price): array
    {
        // automatically knows to select Products
        // the "p" is an alias you'll use in the rest of the query
        $qb = $this->createQueryBuilder('p')
            ->andWhere('p.price > :price')
            ->setParameter('price', $price)
            ->orderBy('p.price', 'ASC')
            ->getQuery();

        return $qb->execute();

        // to get just one result:
        // $product = $qb->setMaxResults(1)->getOneOrNullResult();
    }
}
```

##### Relationships. https://www.doctrine-project.org/projects/doctrine-orm/en/latest/reference/association-mapping.html
Relationship types:
- OneToOne (in practice similar to ManyToOne) - direct FK mapping
- ManyToOne/OneToMany - direct FK mapping
- ManyToMany - requires a join table

###### ManyToOne.
Use maker to create FK relation, with optional CASCADE (orphan)
```
 php bin/console make:entity

Class name of the entity to create or update (e.g. BraveChef):
> Product

 to stop adding fields):
> category

Field type (enter ? to see all types) [string]:
> relation

What class should this entity be related to?:
> Category

Relation type? [ManyToOne, OneToMany, ManyToMany, OneToOne]:
> ManyToOne

Is the Product.category property allowed to be null (nullable)? (yes/no) [yes]:
> no

Do you want to add a new property to Category so that you can access/update
getProducts()? (yes/no) [yes]:
> yes

New field name inside Category [products]:
> products

Do you want to automatically delete orphaned App\Entity\Product objects
(orphanRemoval)? (yes/no) [no]:
> no

 to stop adding fields):
>
(press enter again to finish)
```

Related Entities can be then accessed by standard getters or a query builder can be used that will automatically create necessary Entity instances.

###### ManyToMany.
TODO











