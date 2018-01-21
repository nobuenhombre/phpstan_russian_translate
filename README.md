# phpstan_russian_translate
Перевод на русский для phpstan

# PHPStan - PHP Static Analysis Tool

[![Build Status](https://travis-ci.org/phpstan/phpstan.svg)](https://travis-ci.org/phpstan/phpstan)
[![Latest Stable Version](https://poser.pugx.org/phpstan/phpstan/v/stable)](https://packagist.org/packages/phpstan/phpstan)
[![License](https://poser.pugx.org/phpstan/phpstan/license)](https://packagist.org/packages/phpstan/phpstan)
[![PHPStan](https://img.shields.io/badge/PHPStan-enabled-brightgreen.svg?style=flat)](https://github.com/phpstan/phpstan)

[![Donate on PayPal](https://www.paypalobjects.com/en_US/i/btn/btn_donateCC_LG.gif)](https://paypal.me/phpstan)

PHPStan фокусируется на поиске ошибок в вашем коде, без его непосредственного запуска. 
Он ловит целые классы ошибок еще до написания тестов для кода.

![PHPStan](build/phpstan.gif)

PHPStan приближает PHP ближе к компилируемым языкам программирования в том смысле, 
что правильность каждой строчки кода можно проверить перед фактическим запуском.

**[Read more about PHPStan on Medium.com »](https://medium.com/@ondrejmirtes/phpstan-2939cd0ad0e3)**

**[Try out PHPStan on the on-line playground! »](https://phpstan.org/)**

## помогает ли вам PHPStan избежать ошибок на продакшене?
## Consider [supporting it on Patreon](https://www.patreon.com/phpstan) so I'm able to make it even more awesome!

*I offer to issue invoices for contributions on PayPal and Patreon! [Contact me](mailto:ondrej@mirtes.cz) for details.*

В данный момент он выполняет следующие проверки в вашем коде:

* Существование классов и интерфейсов в `instanceof`, `catch`, typehints, других языковых конструкциях и даже в аннотациях. PHP не делает этого и просто молчит.
* Существование переменных в области условных переходов и циклов.
* Существование и видимость вызываемых методов и функций.
* Существование и видимость доступных свойств и констант.
* Корректность типов, назначенных свойствам.
* Корректность количества и типов параметров, передаваемых конструкторам, методам и функциям.
* Корректность типов, возвращаемых методами и функциями.
* Корректность количества параметров, передаваемых в `sprintf`/`printf` вызовах базирующихся на формате строк.
* Бесполезные приведения типа (string)'foo'.
* Неиспользуемые параметры конструктора - их можно удалить или автор забыл
использовать их в теле метода.
* Требуемые вызовы `parent::__construct()` если конструктор родителя существует.
* Использование только допустимых типов ключей массива 
(только целые числа, строки, float, логические значения и значения NULL).
* Дублирование ключей массива в массивах литералов.
* Только итерируемые объекты передаются к `foreach`.
* Корректность высоты регистра букв в названии классов при ссылке на классы. Имена классов нечувствительны к регистру, но использование этого преимущества опасно с автоматической загрузкой на чувствительных к регистру файловых системах.
* Невозможные проверки (мертвый код) несовместимых типов с помощью оператора `instanceof`, `===`, `!== ` и различные проверки функций, такие как `is_int` или `is_null`.
* Всегда определенные и никогда не определенные переменные в вызове isset().
* Проверка phpDocs - поиск несовместимых типов между phpDocs и нативными typehints.
* Только объекты передаются в функцию `clone`.

## Расширяемость

Уникальной особенностью PHPStan является способность определять и статически проверять "магическое" поведение классов - 
доступ к свойствам, которых не определен в классе, но создается в '__get' и '__set'
и вызов методов с помощью '__call'.

See [Class reflection extensions](#class-reflection-extensions) and [Dynamic return type extensions](#dynamic-return-type-extensions).

You can also install official framework-specific extensions:

* [Doctrine](https://github.com/phpstan/phpstan-doctrine)
* [PHPUnit](https://github.com/phpstan/phpstan-phpunit)
* [Nette Framework](https://github.com/phpstan/phpstan-nette)
* [Dibi - Database Abstraction Library](https://github.com/phpstan/phpstan-dibi)
* [PHP-Parser](https://github.com/phpstan/phpstan-php-parser)

Unofficial extensions for other frameworks and libraries are also available:

* [Phony](https://github.com/eloquent/phpstan-phony)
* [Symfony Framework](https://github.com/lookyman/phpstan-symfony)
* [Prophecy](https://github.com/Jan0707/phpstan-prophecy)

New extensions are becoming available on a regular basis!

## Условия

PHPStan требует PHP > = 7.0. Вы должны запустить его в среде с PHP 7.x, но фактический код может но, не обязан использовать PHP 7.x особенности. 
(код, написанный для PHP 5.6 и более ранних версий, может работать на 7.x в основном немодифицированным.)

PHPStan лучше всего работает с современным объектно-ориентированным кодом. 
Чем более строго типизирован ваш код, тем больше информации Вы даете PHPStan для работы.

Правильно аннотированный и типизированный код (свойства класса, аргументы функции и метода, возвращаемые типы) помогает
не только инструментам статического анализа, но и другим людям, которые работают с кодом, чтобы понять его.

## Установка

Чтобы начать выполнение анализа кода, требуется PHPStan in [Composer](https://getcomposer.org/):

```
composer require --dev phpstan/phpstan
```

Composer установит PHPStan's исполняемый файл в  его `bin-dir` по умолчанию в `vendor/bin`.

Если у вас есть конфликты зависимостей в композере или вы хотите установить PHPStan глобально, лучший путь через PHAR архив.Вы всегда можете найти последние стабильные PHAR архивы по этому адресу [release notes](https://github.com/phpstan/phpstan/releases). Также вы можете использовать [phpstan/phpstan-shim](https://packagist.org/packages/phpstan/phpstan-shim) пакет для инсталляции PHPStan через Composer без риска конфликта зависимостей.
Также вы можете использовать докер образ [PHPStan via Docker](https://github.com/phpstan/docker-image).

## Первый запуск

Чтобы позволить PHPStan проанализировать ваш код, вы должны использовать команду `analyse` и указать на каталоги где находится ваш код

Таким образом если ваши классы лежат в каталогах `src` and `tests`, вы можете запустить PHPStan вот так:

```bash
vendor/bin/phpstan analyse src tests
```

PHPStan, вероятно, найдет некоторые ошибки, но не волнуйтесь, ваш код может быть просто отличным. 
Обнаружены ошибки на первом запуске, как правило:

* Дополнительные аргументы, передаваемые функции (например, функция требует два аргумента, код проходит три)
* Дополнительные аргументы, передаваемые функции Print/sprintf (например, строка форматирования содержит один местозаполнитель, код передает два значения для замены)
* Очевидные ошибки в Мертвом коде
* Магическое поведение, которое должно быть определено. См [расширяемость] (#extensibility).

После исправления очевидных ошибок в коде, посмотрите на следующий раздел
для всех параметров конфигурации, которые приведут число зарегистрированных ошибок к нулю
это делает PHPStan подходящим для запуска как части вашего сценария непрерывной интеграции.

## Уровни проверок

Если вы хотите использовать PHPStan, но вашему коду не до сильной типизации
и строгих проверкок PHPStan, вы можете выбрать некоторые из в настоящее время 8 уровней проверки.
(0 является самым свободным и 7 является самым строгим) путем передачи `--level` в `analyse`. Уровень по умолчанию равен "0".

Эта функция позволяет постепенное принятие PHPStan проверок. Вы можете начать использовать PHPStan
с более низким уровнем правила и увеличить его, когда вы чувствуете, что это нужно.

Вы также можете использовать `--level max` в качестве псевдонима для самого высокого уровня. Это гарантирует, что вы всегда будете использовать наивысший уровень при обновлении до новых версий PHPStan. Обратите внимание, что это может создать значительное препятствие при обновлении до более новой версии, поскольку может потребоваться исправить много кода, чтобы довести количество ошибок до нуля.

## Конфигурация

PHPStan можно запустить с указанием конфигурационного файла через опцию `-c`:

```bash
vendor/bin/phpstan analyse -l 4 -c phpstan.neon src tests
```

When using a custom project config file, you have to pass the `--level` (`-l`)
option to `analyse` command (default value does not apply here).

При использовании пользовательского файла конфигурации проекта, вы должны передать `--level` (`-l`)
опция `analyse` (значение по умолчанию здесь не применяется).

[NEON file format](https://ne-on.org/) очень близок к YAML.
Все перечисленные ниже параметры являются частью раздела `parameters`.

### Автозагрузка

PHPStan использует Composer автозагрузчик так что самый простой способ, как автозагрузку классов
через `autoload`/`autoload-dev` разделы в composer.json.

#### Определение путей сканирования

If PHPStan complains about some non-existent classes and you're sure the classes
exist in the codebase AND you don't want to use Composer autoloader for some reason,
you can specify directories to scan and concrete files to include using
`autoload_directories` and `autoload_files` array parameters:

Если PHPStan жалуется на некоторые несуществующие классы, и вы уверены, что классы
существует в базе кода, и вы не хотите использовать Composer autoloader по некоторым причинам,
Вы можете указать каталоги для сканирования и конкретные файлы для включения с помощью
`autoload_directories` and `autoload_files`:


```
parameters:
	autoload_directories:
		- %rootDir%/../../../build
	autoload_files:
		- %rootDir%/../../../generated/routes/GeneratedRouteList.php
```

`%rootDir%` is expanded to the root directory where PHPStan resides.

#### Автозагрузка для глобальной установки

PHPStan поддерживает глобальную установку [`composer global`](https://getcomposer.org/doc/03-cli.md#global) или [PHAR archive](#installation).

В этом случае он не является частью автозагрузчика проекта, но поддерживает автозагрузку автозагрузчика композитора
из текущего рабочего каталога, проживающего в `vendor/`:

```bash
cd /path/to/project
phpstan analyse src tests # looks for autoloader at /path/to/project/vendor/autoload.php
```

If you have your dependencies installed at a different path
or you're running PHPStan from a different directory,
you can specify the path to the autoloader with the `--autoload-file|-a` option:

Если ваши зависимости установлены по другому пути
или вы запускаете PHPStan из другого каталога,
Вы можете указать путь к автозагрузчику с опцией  `--autoload-file|-a`:

```bash
phpstan analyse --autoload-file=/path/to/autoload.php src tests
```

### Исключение файлов из анализа

Если база кода содержит некоторые файлы, которые разбиты по назначению
(т.е. для проверки поведения вашего приложения на файлах с неверным кодом PHP),
их можно исключить с помощью параметра массива `excludes_analyse`. Строка в каждой строке
используется в качестве шаблона для функции [`fnmatch`](https://secure.php.net/manual/en/function.fnmatch.php) .

```
parameters:
	excludes_analyse:
		- %rootDir%/../../../tests/*/data/*
```

### Анализ файлов с другим расширением

Если ваш код содержит php файлы с расширением отличающимся от стандартного .php 
вы можете добавить его через параметр `fileExtensions`:

```
parameters:
	fileExtensions:
		- php
		- module
		- inc
```

### Универсальные объекты

Классы без предопределенной структуры бывает присутсвуют в PHP приложениях.
Они используются как универсальные контейнеры для данных - любое свойство может быть установлено и прочитано.
Примеры
`stdClass`, `SimpleXMLElement` (они включены по умолчанию), объекты с результатами запроса из базы данных и т.п.
Используйте `universalObjectCratesClasses` параметр чтобы дать PHPStan знать какие классы
и какие их параметры используются в вашем коде:

```
parameters:
	universalObjectCratesClasses:
		- Dibi\Row
		- Ratchet\ConnectionInterface
```

### Добавление неявно назначенных переменных в область

Если вы используете некоторые переменные из вашего try блока в блоке catch, установите `polluteCatchScopeWithTryAssignments` boolean параметр в `true`.

```php
try {
	$author = $this->getLoggedInUser();
	$post = $this->postRepository->getById($id);
} catch (PostNotFoundException $e) {
	// $author is probably defined here
	throw new ArticleByAuthorCannotBePublished($author);
}
```

If you are enumerating over all possible situations in if-elseif branches
and PHPStan complains about undefined variables after the conditions, you can write
an else branch with throwing an exception:

Если вы перечисляете над всеми по возможности ситуациями внутри If-ElseIf ветви
и PHPStan жалуется на неопределенные переменные после условия, вы можете написать
ветвь Else с исключением:

```php
if (somethingIsTrue()) {
	$foo = true;
} elseif (orSomethingElseIsTrue()) {
	$foo = false;
} else {
	throw new ShouldNotHappenException();
}

doFoo($foo);
```

Я рекомендую оставлять `polluteCatchScopeWithTryAssignments` установленным в  `false` потому что это позволит иметь более чистый и поддерживаемый код.

### Пользовательские ранние завершающие вызовы метода

Предыдущий пример показал, что если ветви условия заканчиваются выбросом исключения, 
эта ветвь не имеет определения переменной, используемой после окончания ветвей условия.

Но исключения — это не единственный способ преждевременного завершения выполнения метода. 
Некоторые конкретные вызовы методов могут быть восприняты разработчиками проекта также как раннее завершение - как `redirect()`, 
который останавливает выполнение, выбрасывая внутреннее исключение.

```php
if (somethingIsTrue()) {
	$foo = true;
} elseif (orSomethingElseIsTrue()) {
	$foo = false;
} else {
	$this->redirect('homepage');
}

doFoo($foo);
```

Эти методы можно настроить, указав класс, на экземпляре которого они вызываются так:

```
parameters:
	earlyTerminatingMethodCalls:
		Nette\Application\UI\Presenter:
			- redirect
			- redirectUrl
			- sendJson
			- sendResponse
```

### Игнорировать сообщения об ошибках с регулярными выражения

Если некоторые проблемы в вашей базе кода не легко исправить или просто хотите иметь дело с ним позже,
можно исключить сообщения об ошибках из результатов анализа с регулярными выражениями:

```
parameters:
	ignoreErrors:
		- '#Call to an undefined method [a-zA-Z0-9\\_]+::method\(\)#'
		- '#Call to an undefined method [a-zA-Z0-9\\_]+::expects\(\)#'
		- '#Access to an undefined property PHPUnit_Framework_MockObject_MockObject::\$[a-zA-Z0-9_]+#'
		- '#Call to an undefined method PHPUnit_Framework_MockObject_MockObject::[a-zA-Z0-9_]+\(\)#'
```

Если некоторые из шаблонов не фигурируют больше в результатах сканирования, PHPStan даст вам знать
и вам придется удалить шаблон из конфигурации. Вы можете выключить
Это поведение, установив `reportUnmatchedIgnoredErrors` to `false` в конфигурации PHPStan.

### Bootstrap file

Если вам нужно инициализировать что-то в PHP Runtime до PHPStan запускается (например, ваш собственный автопогрузчик),
Вы можете предоставить свой собственный файл Bootstrap:

```
parameters:
	bootstrap: %rootDir%/../../../phpstan-bootstrap.php
```

### Специальные правила

PHPStan позволяет написать специальные правила для проверки специфических ситуаций в вашем коде. 
Ваш класс правил необходимо имплементировать с интерфейсом `PHPStan\Rules\Rule` и зарегистрировать как сервис в конфигурационном файле:

```
services:
	-
		class: MyApp\PHPStan\Rules\DefaultValueTypesAssignedToPropertiesRule
		tags:
			- phpstan.rules.rule
```

Чтобы посмотреть как писать правила проверок посмотрите вот эту ссылку [src/Rules](https://github.com/phpstan/phpstan/tree/master/src/Rules)
и вы увидите несколько готовых правил.

Также проверте [phpstan-strict-rules](https://github.com/phpstan/phpstan-strict-rules) это дополнительный репозиторий строгих и дополнительных правил для PHPStan!

### Специальное форматирование ошибок

По умолчанию, PHPStan выводит ошибки в таблицы сгруппированые по файлам для наиболее удобного чтения. 
Что-бы изменить вывод, вы можете использовать `--errorFormat` опцию командной строки. 
Она представляет дополнительный `raw` формат с одной ошибкой на строку для легкого парсинга.
Вы также можете создать свой формат имплементировав `PHPStan\Command\ErrorFormatter\ErrorFormatter` интерфейс:

```php
interface ErrorFormatter
{

	/**
	 * Formats the errors and outputs them to the console.
	 *
	 * @param \PHPStan\Command\AnalysisResult $analysisResult
	 * @param \Symfony\Component\Console\Style\OutputStyle $style
	 * @return int Error code.
	 */
	public function formatErrors(
		AnalysisResult $analysisResult,
		\Symfony\Component\Console\Style\OutputStyle $style
	): int;

}
```

Регистрация вашего формата в классе конфигурации `phpstan.neon`:

```
errorFormatter.awesome:
	class: App\PHPStan\AwesomeErrorFormatter
```

используйте имя вашего шаблона в командной строке вот так через параметр `errorFormatter.`:

```bash
vendor/bin/phpstan analyse -c phpstan.neon -l 4 --errorFormat awesome src tests
```

## Class reflection extensions

Classes in PHP can expose "magical" properties and methods decided in run-time using
class methods like `__get`, `__set` and `__call`. Because PHPStan is all about static analysis
(testing code for errors without running it), it has to know about those properties and methods beforehand.

When PHPStan stumbles upon a property or a method that is unknown to built-in class reflection, it iterates
over all registered class reflection extensions until it finds one that defines the property or method.

Class reflection extension cannot have `PHPStan\Broker\Broker` (service for obtaining class reflections) injected in the constructor due to circular reference issue, but the extensions can implement `PHPStan\Reflection\BrokerAwareClassReflectionExtension` interface to obtain Broker via a setter.

### Properties class reflection extensions

This extension type must implement the following interface:

```php
namespace PHPStan\Reflection;

interface PropertiesClassReflectionExtension
{

	public function hasProperty(ClassReflection $classReflection, string $propertyName): bool;

	public function getProperty(ClassReflection $classReflection, string $propertyName): PropertyReflection;

}
```

Most likely you will also have to implement a new `PropertyReflection` class:

```php
namespace PHPStan\Reflection;

interface PropertyReflection
{

	public function getType(): Type;

	public function getDeclaringClass(): ClassReflection;

	public function isStatic(): bool;

	public function isPrivate(): bool;

	public function isPublic(): bool;

}
```

This is how you register the extension in project's PHPStan config file:

```
services:
	-
		class: App\PHPStan\PropertiesFromAnnotationsClassReflectionExtension
		tags:
			- phpstan.broker.propertiesClassReflectionExtension
```

### Methods class reflection extensions

This extension type must implement the following interface:

```php
namespace PHPStan\Reflection;

interface MethodsClassReflectionExtension
{

	public function hasMethod(ClassReflection $classReflection, string $methodName): bool;

	public function getMethod(ClassReflection $classReflection, string $methodName): MethodReflection;

}
```

Most likely you will also have to implement a new `MethodReflection` class:

```php
namespace PHPStan\Reflection;

interface MethodReflection
{

	public function getDeclaringClass(): ClassReflection;

	public function getPrototype(): self;

	public function isStatic(): bool;

	public function isPrivate(): bool;

	public function isPublic(): bool;

	public function getName(): string;

	/**
	 * @return \PHPStan\Reflection\ParameterReflection[]
	 */
	public function getParameters(): array;

	public function isVariadic(): bool;

	public function getReturnType(): Type;

}
```

This is how you register the extension in project's PHPStan config file:

```
services:
	-
		class: App\PHPStan\EnumMethodsClassReflectionExtension
		tags:
			- phpstan.broker.methodsClassReflectionExtension
```

## Dynamic return type extensions

If the return type of a method is not always the same, but depends on an argument passed to the method,
you can specify the return type by writing and registering an extension.

Because you have to write the code with the type-resolving logic, it can be as complex as you want.

After writing the sample extension, the variable `$mergedArticle` will have the correct type:

```php
$mergedArticle = $this->entityManager->merge($article);
// $mergedArticle will have the same type as $article
```

This is the interface for dynamic return type extension:

```php
namespace PHPStan\Type;

use PhpParser\Node\Expr\MethodCall;
use PHPStan\Analyser\Scope;
use PHPStan\Reflection\MethodReflection;

interface DynamicMethodReturnTypeExtension
{

	public function getClass(): string;

	public function isMethodSupported(MethodReflection $methodReflection): bool;

	public function getTypeFromMethodCall(MethodReflection $methodReflection, MethodCall $methodCall, Scope $scope): Type;

}
```

And this is how you'd write the extension that correctly resolves the EntityManager::merge() return type:

```php
public function getClass(): string
{
	return \Doctrine\ORM\EntityManager::class;
}

public function isMethodSupported(MethodReflection $methodReflection): bool
{
	return $methodReflection->getName() === 'merge';
}

public function getTypeFromMethodCall(MethodReflection $methodReflection, MethodCall $methodCall, Scope $scope): Type
{
	if (count($methodCall->args) === 0) {
		return $methodReflection->getReturnType();
	}
	$arg = $methodCall->args[0]->value;

	return $scope->getType($arg);
}
```

And finally, register the extension to PHPStan in the project's config file:

```
services:
	-
		class: App\PHPStan\EntityManagerDynamicReturnTypeExtension
		tags:
			- phpstan.broker.dynamicMethodReturnTypeExtension
```

There's also an analogous functionality for:

* **static methods** using `DynamicStaticMethodReturnTypeExtension` interface
and `phpstan.broker.dynamicStaticMethodReturnTypeExtension` service tag.
* **functions** using `DynamicFunctionReturnTypeExtension` interface and `phpstan.broker.dynamicFunctionReturnTypeExtension` service tag.

## Known issues

* If `include` or `require` are used in the analysed code (instead of `include_once` or `require_once`),
PHPStan will throw `Cannot redeclare class` error. Use the `_once` variants to avoid this error.
* If PHPStan crashes without outputting any error, it's quite possible that it's
because of a low memory limit set on your system. **Run PHPStan again** to read a couple of hints
what you can do to prevent the crashes.

## Code of Conduct

This project adheres to a [Contributor Code of Conduct](https://github.com/phpstan/phpstan/blob/master/CODE_OF_CONDUCT.md). By participating in this project and its community, you are expected to uphold this code.

## Contributing

Any contributions are welcome.

### Building

You can either run the whole build including linting and coding standards using

```bash
vendor/bin/phing
```

or run only tests using

```bash
vendor/bin/phing tests
```
