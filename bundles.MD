# Bundles.
Bundles are plugins for Symfony and can be defined in `config/bundles.php`

In Symfony versions prior to 4.0, it was recommended to organize your own application code using bundles. This is no longer recommended and bundles should only be used to share code and features between multiple applications.


```
return [
    // 'all' means that the bundle is enabled for any Symfony environment
    Symfony\Bundle\FrameworkBundle\FrameworkBundle::class => ['all' => true],
    Symfony\Bundle\SecurityBundle\SecurityBundle::class => ['all' => true],
    Symfony\Bundle\TwigBundle\TwigBundle::class => ['all' => true],
    Symfony\Bundle\MonologBundle\MonologBundle::class => ['all' => true],
    Symfony\Bundle\SwiftmailerBundle\SwiftmailerBundle::class => ['all' => true],
    Doctrine\Bundle\DoctrineBundle\DoctrineBundle::class => ['all' => true],
    Sensio\Bundle\FrameworkExtraBundle\SensioFrameworkExtraBundle::class => ['all' => true],
    // this bundle is enabled only in 'dev'  and 'test', so you can't use it in 'prod'
    Symfony\Bundle\WebProfilerBundle\WebProfilerBundle::class => ['dev' => true, 'test' => true],
];
```