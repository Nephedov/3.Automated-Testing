[![Build status](https://ci.appveyor.com/api/projects/status/ac678v0uix87hc0k?svg=true)](https://ci.appveyor.com/project/Nephedov/testapi)

# «Тестирование API, CI»

## Решения
### Задание 1, 2
* <a href="https://github.com/Nephedov/3.Automated-Testing/blob/main/.appveyor.yml">.appveyor.yml</a> - для CI. Запускает SUT и прогоняет тесты.
* <a href="https://github.com/Nephedov/3.Automated-Testing/tree/main/src/test/java/ru/netology/rest">src/test/java/ru/netology/rest</a>. - репозиторий с тестами.
* <a href="https://github.com/Nephedov/3.Automated-Testing/blob/main/src/test/resources/accounts.schema.json">accounts.schema.json</a> - для валидации JSON документов.
* <a href="https://github.com/Nephedov/3.Automated-Testing/blob/main/src/test/java/ru/netology/rest/MobileBankApiTestV4.java">MobileBankApiTestV4.java</a>. - тестовый класс, проверяющий соответствие JSON-схеме.

<a href="https://github.com/Nephedov/3.Automated-Testing/tree/main">Репозиторий</a> с проектом.
### Задание 3
* <a href="https://github.com/Nephedov/3.2.Automated-Testing/blob/main/src/test/java/ru/netology/PostmanEchoTest.java">PostmanEchoTest.java</a> - класс с тестом.

<a href="https://github.com/Nephedov/3.2.Automated-Testing/tree/main">Репозиторий</a> с проектом.
## Что было сделано
### Задание 1, 2
* Настроен <a href="https://github.com/Nephedov/3.Automated-Testing/blob/main/build.gradle">build.gradle</a> с зависимостями:
  * JunitJupier.
  * Rest-Assured.
  * Rest-Assured:json-schema-validator.
* Подключен к проекту AppVeyor. Настроен <a href="https://github.com/Nephedov/3.Automated-Testing/blob/main/.appveyor.yml">appveyor.yml</a>. Добавлен бейдж в README.md, о статусе сборки при пуше.
* Составлена <a href="https://github.com/Nephedov/3.Automated-Testing/blob/main/src/test/resources/accounts.schema.json">JSON-схема</a> для валидации JSON документов.
* Дописаны тестовые классы проверяющие API:
  * <a href="https://github.com/Nephedov/3.Automated-Testing/blob/main/src/test/java/ru/netology/rest/MobileBankApiTestV1.java">MobileBankApiTestV1.java</a>.
  * <a href="https://github.com/Nephedov/3.Automated-Testing/blob/main/src/test/java/ru/netology/rest/MobileBankApiTestV2.java">MobileBankApiTestV2.java</a>.
  * <a href="https://github.com/Nephedov/3.Automated-Testing/blob/main/src/test/java/ru/netology/rest/MobileBankApiTestV3.java">MobileBankApiTestV3.java</a>.
  * <a href="https://github.com/Nephedov/3.Automated-Testing/blob/main/src/test/java/ru/netology/rest/MobileBankApiTestV4.java">MobileBankApiTestV4.java</a>.
  * <a href="https://github.com/Nephedov/3.Automated-Testing/blob/main/src/test/java/ru/netology/rest/MobileBankApiTestV5.java">MobileBankApiTestV5.java</a>.
  * <a href="https://github.com/Nephedov/3.Automated-Testing/blob/main/src/test/java/ru/netology/rest/MobileBankApiTestV6.java">MobileBankApiTestV6.java</a>.

 ### Задание 3
* Настроен <a href="https://github.com/Nephedov/3.2.Automated-Testing/tree/main">build.gradle</a> с зависимостями:
  * JunitJupier.
  * Rest-Assured.
* Подключен к проекту AppVeyor. Настроен <a href="https://github.com/Nephedov/3.2.Automated-Testing/blob/main/.appveyor.yml">appveyor.yml</a>. Добавлен бейдж в README.md, о статусе сборки при пуше.
* Реализован класс <a href="https://github.com/Nephedov/3.2.Automated-Testing/blob/main/src/test/java/ru/netology/PostmanEchoTest.java">PostmanEchoTest.java</a> c тестовым сценарием API запроса.
 
## Описание Задания №1: настройка CI

Ваш целевой сервис (SUT — System under test), расположен в файле [app-mbank.jar](app-mbank.jar), этот же файл используется в примерах на лекции. Вам нужно его положить в каталог `artifacts` вашего проекта, который необходимо создать.

Поскольку файлы с расширением `.jar` находятся в списках `.gitignore`, вам нужно принудительно заставить Git следить за ними: `git add -f artifacts/app-mbank.jar`.

После чего сделать `git push`. Обязательно удостоверьтесь, что файл попал в репозиторий.

### AppVeyor

[AppVeyor](https://www.appveyor.com) — одна из платформ, предоставляющих функциональность Continuous integration. В базовом варианте она бесплатна.

#### Конфигурация как код

Поскольку вручную настраивать каждый проект в системе Continuous integration — лишняя трата времени, мы будем хранить всю конфигурацию для AppVeyor в специальном файле с названием `.appveyor.yml`.

Важно: внимательно посмотрите на структуру деморепозитория из ваших лекций. Большинство инструментов используют подход «Configuration by exception», то есть конфигурируется только то, что не соответствует настройкам по умолчанию. Поэтому у вас всего два пути: либо использовать настройки по умолчанию и писать как можно меньше конфигурации, либо идти против системы и писать много конфигурации, а потом ещё и отлаживать её.

## Описание Задания №2: JSON Schema

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

Доработайте схему соответствующим образом.

## Описание Задания №3: Postman Echo

В этой задаче мы сэмулируем ситуацию, в которой SUT уже запущен, а мы из теста просто обращаемся к нему.

Что нужно сделать:
1. Создайте новый проект на базе Gradle.
2. Добавьте необходимые зависимости. Если вы не пишите схему, то только REST assured.
3. Напишите тест, взяв сам запрос из кода выше.
4. Изучите ответ и напишите JSONPath-выражение, которое проверит, что в нужном поле хранятся отправленные вами данные. Обратите внимание, теперь у вас не массив, а объект.
