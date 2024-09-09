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
  type: attribute
```