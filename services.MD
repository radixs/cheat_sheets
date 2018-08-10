# Services, service container

###### To list available services and their aliases:
```
php bin/console debug:autowiring
```

###### Access to service inside a controller: type hint a class or interface
```
public function number($max, LoggerInterface $logger)
{
    $logger->info('We are logging!');
    // ...
}
```

###### Services: go to src/Service/SomeService.php
example:
```
namespace App\Service;

use Symfony\Component\Routing\Generator\UrlGeneratorInterface;

class SomeService
{
    private $router;

    public function __construct(UrlGeneratorInterface $router)
    {
        $this->router = $router;
    }

    public function someMethod()
    {
        $url = $this->router->generate(
            'blog_show',
            ['slug' => 'my-blog-post']
        );
        // ...
    }
}
```

###### Explicit configuration of services for a controller (works with services too. points towards an alias):
```
# config/services.yaml
services:
    # ...

    # explicitly configure the service
    App\Controller\LuckyController:
        bind:
            # for any $logger argument, pass this specific service
            $logger: '@monolog.logger.doctrine'
            # for any $projectDir argument, pass this parameter value
            $projectDir: '%kernel.project_dir%'
```
_defaults can be used as general override

###### Explicit configuration of a service:
```
# config/services.yaml
services:
    # ...

    # makes classes in src/ available to be used as services
    # this creates a service per class whose id is the fully-qualified class name
    App\:
        resource: '../src/*'
        exclude: '../src/{Entity,Migrations,Tests}'

    # explicitly configure the service
    App\Updates\SiteUpdateManager:
        arguments:
            $adminEmail: 'manager@example.com'
```

###### Parameters in service container
```
# config/services.yaml
parameters:
    admin_email: manager@example.com

services:
    # ...

    App\Updates\SiteUpdateManager:
        arguments:
            $adminEmail: '%admin_email%'
```
then it can be accessed direcly via:
```
public function new()
{
    // ...

    // this ONLY works if you extend the base Controller
    $adminEmail = $this->container->getParameter('admin_email');

    // or a shorter way!
    // $adminEmail = $this->getParameter('admin_email');
}
```



