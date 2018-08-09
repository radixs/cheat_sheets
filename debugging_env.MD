# Debugging

###### Default targets:
```
/var/logs/dev.log
appPath/_profiler/
```

###### Environment: set it in .env in root dir
```
APP_ENV=dev
APP_ENV=prod
APP_ENV=test
```
specific settings configurable in config/packages

app constants for services are best placed in services.yaml in parameters, can also be accessed by doing `$adminEmail = $this->container->getParameter('admin_email');`