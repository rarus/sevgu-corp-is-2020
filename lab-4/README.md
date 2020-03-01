# Лабораторная работа №4 – Symfony (черновик)

## Задание
1. Создать новый проект на Symfony
2. Создать заглушки для всех методов API из ЛР №3
3. Создать набор для тестирования
4. Разместить проект в отдельном репозитории Github

## Критерии
1. В репозитории на github лежит проект на Symfony
2. Для всех методов из ЛР №3 существует заглушка
3. Есть коллекция Postman (или аналог) для проверки запросов

## Подробное описание
Что бы создать проект вам нужен установленный php и composer.

Вам необходимо будет создать набросок API по созданному ранее описанию OpenAPI 3.0.

В рамках этой лабораторной работы необходимо только создать все необходимые роуты и контроллеры,
которые возвращают заглушку (json с примером ответа как в OpenAPI)

1. Установите Symfony CLI с сайта разработчика

https://symfony.com/download

2. В желаемой директории выполните команду и перейдите в неё

`symfony new cis-lab`
`cd cis-lab`

3. Запустите локальный сервер 

`symfony server:start`

Он будет доступен по адресу http://127.0.0.1:8000

4. Создайте контроллеры и их методы в соответствии с API definition из ЛР №3

Каждый контроллер должен располагаться в папке `src/Controller`
Например, файл `src/Controller/LuckyController.php`
```php
namespace App\Controller;

use Symfony\Component\HttpFoundation\Response;

class LuckyController
{
    public function number($max)
    {
        $number = random_int(0, $max);

        return $this->json(['number' => $number]);
    }
}
```

Что бы метод `number` контроллера стал доступен через API – в файле `config/routes.yaml` необходимо добавить следующее:
```yaml
GetLuckyNumber:
    path:       /lucky/number/{max}
    controller: App\Controller\LuckyController::nuber
    methods:    GET
```

Эта запись создаёт роут с именем `GetLuckyNumber`, доступный
через метод `GET` по пути `/lucky/number/{max}` (где {max} это любое значение) 
и обрабатываемый методом `number` класса `App\Controller\LuckyController`

5. Проверьте, что все ваши методы работают и возвращается правильный ответ с помощью Postman или любого другого средства

Для защиты вам необходимо будет показать эту работу так что сохраните коллекцию Postman, набор команд для curl или что вы там решите использовать)

## Советы
Если что-то не запускается в Symfony – воспользуйтесь `symfony check:requirements`, возможно что-то не установлено

## Полезные ссылки
1. https://getcomposer.org/download/
2. https://symfony.com/download
3. https://symfony.com/doc/current/setup.html
4. https://symfony.com/doc/current/controller.html
5. https://symfony.com/doc/current/routing.html
