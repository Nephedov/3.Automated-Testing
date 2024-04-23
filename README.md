[![Build status](https://ci.appveyor.com/api/projects/status/ac678v0uix87hc0k?svg=true)](https://ci.appveyor.com/project/Nephedov/testapi)

# Домашнее задание к занятию «1.2. Тестирование API, CI»

## Решения
### Задание 1
 * <a href="https://github.com/Nephedov/3.Automated-Testing/blob/427581b7729b140fb92d98c498d6e0120bb9fc9d/.appveyor.yml">.appveyor.yml</a>.
 * <a href="https://github.com/Nephedov/3.Automated-Testing/blob/main/build.gradle">build.gradle</a>.
 * <a href="https://github.com/Nephedov/3.Automated-Testing/tree/427581b7729b140fb92d98c498d6e0120bb9fc9d/src/test/java/ru/netology/rest">src/test/java/ru/netology/rest</a>. - репозиторий с тестами.
### Задание 2
 * <a href="https://github.com/Nephedov/3.Automated-Testing/blob/427581b7729b140fb92d98c498d6e0120bb9fc9d/src/test/resources/accounts.schema.json">accounts.schema.json</a>.
 * <a href="https://github.com/Nephedov/3.Automated-Testing/blob/427581b7729b140fb92d98c498d6e0120bb9fc9d/src/test/java/ru/netology/rest/MobileBankApiTestV4.java">MobileBankApiTestV4.java</a>. - тестовый класс, проверяющий соответствие JSON-схеме.
### Задание 3
  * <a href="https://github.com/Nephedov/3.2.Automated-Testing/blob/d85cee350ae36a2a37f33a09aff34b7a17bf4c41/build.gradle">build.gradle</a>.
  * <a href="https://github.com/Nephedov/3.2.Automated-Testing/blob/d85cee350ae36a2a37f33a09aff34b7a17bf4c41/src/test/java/ru/netology/PostmanEchoTest.java">PostmanEchoTest.java</a> - класс с тестом.
## Что было сделано
  * Создан и настроен Gradle проект с зависимостями:
    * JunitJupier.
    * Rest-Assured.
    * Rest-Assured:json-schema-validator.
  * Подключен к проекту AppVeyor. Настроен appveyor.yml. Добавлен бейдж в README.md, о статусе сборки при пуше.
  * Составлена JSON-схема для валидации JSON документов.
  * Реализованы классы тестирующие API.

## Задача №1: настройка CI

Ваш целевой сервис (SUT — System under test), расположен в файле [app-mbank.jar](app-mbank.jar), этот же файл используется в примерах на лекции. Вам нужно его положить в каталог `artifacts` вашего проекта, который необходимо создать.

Поскольку файлы с расширением `.jar` находятся в списках `.gitignore`, вам нужно принудительно заставить Git следить за ними: `git add -f artifacts/app-mbank.jar`.

После чего сделать `git push`. Обязательно удостоверьтесь, что файл попал в репозиторий.

### AppVeyor

[AppVeyor](https://www.appveyor.com) — одна из платформ, предоставляющих функциональность Continuous integration. В базовом варианте она бесплатна.

#### Конфигурация как код

Поскольку вручную настраивать каждый проект в системе Continuous integration — лишняя трата времени, мы будем хранить всю конфигурацию для AppVeyor в специальном файле с названием `.appveyor.yml`.

Важно: внимательно посмотрите на структуру деморепозитория из ваших лекций. Большинство инструментов используют подход «Configuration by exception», то есть конфигурируется только то, что не соответствует настройкам по умолчанию. Поэтому у вас всего два пути: либо использовать настройки по умолчанию и писать как можно меньше конфигурации, либо идти против системы и писать много конфигурации, а потом ещё и отлаживать её.

## Задача №2: JSON Schema

JSON Schema предлагает нам инструмент валидации JSON-документов. С описанием вы можете познакомиться по [адресу](https://json-schema.org/understanding-json-schema).


#### Шаг 1. Зависимости проекта
#### Шаг 2. JSON схема    

В каталоге `resources` в `src/test` и должен лежать файл схемы.    

#### Шаг 3. Проверка ответа сервиса на соответсвие схеме    

Один из классов проекта должен содержать операцию проверки соответствия ответа схеме. 

В тестовом классе должен быть импорт статического метода        

Удостоверьтесь, что тесты проходят при соответствии ответа схеме и падают, если вы поменяете что-то в схеме, например, тип для `id`.

#### Шаг 4. Доработать схему

Изучите документацию на тип [`object`](https://json-schema.org/understanding-json-schema/reference/object.html) и найдите способ валидации значения поля на два из возможных значений: «RUB» или «USD».

Доработайте схему соответствующим образом, удостоверьтесь, что тесты проходят, в том числе в CI.

## Задача №3: Postman Echo

**Важно**: эту задачу нужно выполнять в отдельном репозитории.

В этой задаче мы сэмулируем ситуацию, в которой SUT уже запущен, а мы из теста просто обращаемся к нему.

Есть специальный сервис, предназначенный для тестирования HTTP-запросов. Называется он [Postman Echo](https://docs.postman-echo.com). Никогда не тестируйте автоматизированными средствами веб-сервисы, если у вас нет на это письменного разрешения или если веб-сервисы специально не предназначены для этого.

Мы можем отправлять туда запросы и получать ответы.

С GET-запросами мы немного потренировались, теперь нас будут интересовать POST-запросы, а именно отправка тела запроса.

Что нужно сделать:
1. Создайте новый проект на базе Gradle.
2. Добавьте необходимые зависимости. Если вы не пишите схему, то только REST assured.
3. Напишите тест, взяв сам запрос из кода выше.
4. Изучите ответ и напишите JSONPath-выражение, которое проверит, что в нужном поле хранятся отправленные вами данные. Обратите внимание, теперь у вас не массив, а объект.
