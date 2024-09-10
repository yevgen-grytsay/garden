---
{"dg-publish":true,"permalink":"/loading-controllers/","tags":["webdev","symfony"]}
---

## `exclude`
Щоб працював параметр `exclude`, як видно з коду [FileLoader.php#L71](https://github.com/symfony/config/blob/7.1/Loader/FileLoader.php#L71), потрібно, щоб виконувались такі вимоги:
- Значення `resource` має бути типу `string`
- Значення `resource` повинно містити якийсь glob-паттерн (із символами `*?{[`)
- Значення `resource` не повинно містити символ нового рядка `\n`
Ось приклад робочого конфігу:
```yaml
# config/routes/attributes.yaml
controllers:
  resource: '../../src/Controller/{*Controller.php}'
  exclude: '../../src/Controller/{Alice,Bob}'
#  resource:
#    path: '../../src/Controller/{*Controller.php}'
#    namespace: App\Controller
  type: attribute
```
Отак `exclude` працювати не буде (при цьому ніяких помилок ми не отримаємо):
```yaml
# config/routes/attributes.yaml
controllers:
  resource:
    path: '../../src/Controller/{*Controller.php}'
    namespace: App\Controller
  exclude: '../../src/Controller/{Alice,Bob}'
  type: attribute
```
## Rendering Templates
Щоб рендерити HTML, треба
- `composer require symfony/twig-bundle`
- `MyController extends Symfony\Bundle\FrameworkBundle\Controller\AbstractController`
- `templates/index.html.twig`
- `return $this->render('index.html.twig');`
- `config/packages/framework.yaml`
```yaml
# see https://symfony.com/doc/current/reference/configuration/framework.html  
framework:  
  secret: '%env(APP_SECRET)%'
```

## `controller.service_arguments`
```
InvalidArgumentException: "The controller for URI "/" is not callable: Controller "App\Controller\HomeController" cannot be fetched from the container because it is private. Did you forget to tag the service with "controller.service_arguments"?" at ControllerResolver.php line 97
```
https://symfony.com/doc/current/controller/service.html