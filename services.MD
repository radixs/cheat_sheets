# Services

###### To list available services:
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

###### Explicit configuration of services for a controller:
```
# config/services.yaml
services:
    # ...

    # explicitly configure the service
    App\Controller\LuckyController:
        public: true
        bind:
            # for any $logger argument, pass this specific service
            $logger: '@monolog.logger.doctrine'
            # for any $projectDir argument, pass this parameter value
            $projectDir: '%kernel.project_dir%'
```
_defaults can be used as general override