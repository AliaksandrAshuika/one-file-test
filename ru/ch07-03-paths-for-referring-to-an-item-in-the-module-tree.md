## Ссылаемся на элементы дерева модулей при помощи путей

Чтобы показать Rust, где найти элемент в дереве модулей, мы используем путь так же, как мы используем путь при навигации по файловой системе. Например, если мы хотим вызвать функцию, то нам нужно знать её путь.

Пути бывают двух видов:

- *абсолютный путь* берет своё начало с корня крейта: названия крейта или ключевого слова `crate`,
- *относительный путь* начинается с текущего модуля и использует ключевые слова `self`, `super` или идентификатор в текущем модуле.

Как абсолютные, так и относительные, пути сопровождаются одним или несколькими идентификаторами разделёнными двойными двоеточиями (`::`).

Давайте вернёмся к примеру в листинге 7-1. Как бы мы вызывали функцию `add_to_waitlist`? Наш вызов был бы похож на путь к функции `add_to_waitlist`? В листинге 7-3 мы немного упростили код листинга 7-1, удалив ненужные модули и функции. Мы покажем два способа вызова функции `add_to_waitlist` из новой функции `eat_at_restaurant` определённой в корне крейта. Функция `eat_at_restaurant` является частью нашей библиотеки публичного API, поэтому мы помечаем её ключевым словом `pub`. В разделе <a data-md-type="raw_html" href="ch07-03-paths-for-referring-to-an-item-in-the-module-tree.html#exposing-paths-with-the-pub-keyword">"Раскрытие путей с помощью ключевого слова `pub`"</a><!--  -->, мы рассмотрим более подробно `pub`. Обратите внимание, что этот пример ещё не компилируется; мы скоро объясним почему.

<span class="filename">Файл: src/lib.rs</span>

```rust,ignore,does_not_compile
{{#rustdoc_include ../listings/ch07-managing-growing-projects/listing-07-03/src/lib.rs}}
```

<span class="caption">Листинг 7-3. Вызов функции <code>add_to_waitlist</code> с использованием абсолютного и относительного пути</span>

Первый раз, когда мы вызываем функцию `add_to_waitlist` в функции `eat_at_restaurant` мы используем абсолютный путь. Функция `add_to_waitlist` определена в том же крейте что и `eat_at_restaurant` и это означает, что мы можем использовать ключевое слово `crate` в начале абсолютного пути.

После ключевого слова `crate` мы включаем каждый из последующих дочерних модулей, пока не составим путь до `add_to_waitlist`. Вы можете представить файловую систему с такой же структурой, где мы указали бы путь `/front_of_house/hosting/add_to_waitlist` для запуска программы `add_to_waitlist`; мы используем слово `crate`, чтобы начать путь из корня крейта, подобно тому как используется `/` для указания корневой директории файловой системы.

Второй раз, когда мы вызываем `add_to_waitlist` внутри `eat_at_restaurant`, мы используем относительный путь. Путь начинается с имени модуля `front_of_house`, определённого на том же уровне дерева модулей, что и модуль `eat_at_restaurant`. Для относительного пути эквивалентный путь в вымышленной файловой системе выглядел бы так: `front_of_house/hosting/add_to_waitlist`. Начало пути совпадает с именем модуля, что указывает на то, что перед нами относительный путь.

Выбор, использовать относительный или абсолютный путь, является решением, которое вы примете на основании вашего проекта. Решение должно зависеть от того, с какой вероятностью вы переместите объявление элемента отдельно от или вместе с кодом использующим этот элемент. Например, в случае перемещения модуля `front_of_house` и его функции `eat_at_restaurant` в другой модуль с именем `customer_experience`, будет необходимо обновить абсолютный путь до `add_to_waitlist`, но относительный путь все равно будет действителен. Однако, если мы переместим отдельно функцию `eat_at_restaurant` в модуль с именем `dining`, то абсолютный путь вызова `add_to_waitlist` останется прежним, а относительный путь нужно будет обновить. Мы предпочитаем указывать абсолютные пути, потому что это позволяет проще перемещать определения кода и вызовы элементов независимо друг от друга.

Давайте попробуем скомпилировать листинг 7-3 и выяснить, почему он ещё не компилируется. Ошибка, которую мы получаем, показана в листинге 7-4.

```console
{{#include ../listings/ch07-managing-growing-projects/listing-07-03/output.txt}}
```

<span class="caption">Листинг 7-4. Ошибки компиляции при сборке кода из листинга 7-3</span>

Сообщения об ошибках говорят о том, что модуль `hosting` является приватным. Таким образом, у нас есть правильные пути к модулю `hosting` и функции `add_to_waitlist`, но Rust не позволяет использовать их, потому что он не имеет доступа к разделам которые являются приватными, как в нашем случае.

Модули не только полезны для организации кода. Они также определяют *границы конфиденциальности* (privacy boundary) в Rust: граница, которая инкапсулирует детали реализации, которые внешний код не может знать, вызывать или полагаться на них. Итак, если вы хотите сделать элемент приватным, например функцию или структуру, то разместите его в модуль.

В Rust конфиденциальность (privacy) работает так, что все элементы (функции, методы, структуры, перечисления, модули и константы) являются по умолчанию приватными. Элементы в родительском модуле не могут использовать приватные элементы внутри дочерних модулей, но элементы в дочерних модулях могут использовать элементы у своих родительских модулей. Причина в том, что дочерние модули оборачивают и скрывают детали своей реализации, но модули могут видеть контекст, в котором они определены. Продолжая метафору с рестораном, думайте о правилах конфиденциальности как о задней части ресторана: то что там происходит скрыто от клиентов ресторана, но открыто для менеджеров ресторана: они могут видеть и управлять рестораном в котором они все работают.

В Rust решили, что система модулей должна функционировать таким образом, чтобы по умолчанию скрывать детали реализации. Таким образом, вы знаете, какие части внутреннего кода вы можете изменять не нарушая работы внешнего кода. Но у нас всё же остаётся возможность раскрывать внутренние части кода дочерних модулей для внешних модулей - предков. Чтобы сделать элемент публичным мы можем использовать ключевое слово `pub`.

### Раскрываем приватные пути с помощью ключевого слова `pub`

Давайте вернёмся к ошибке в листинге 7-4, которая говорит что модуль `hosting` является приватным. Мы хотим, чтобы функция `eat_at_restaurant` представленная в родительском модуле `eat_at_restaurant` имела доступ к функции `add_to_waitlist` в дочернем модуле, поэтому мы помечаем модуль `hosting` с ключевым словом <code>pub</code>, как показано в листинге 7-5.

<span class="filename">Файл: src/lib.rs</span>

```rust,ignore,does_not_compile
{{#rustdoc_include ../listings/ch07-managing-growing-projects/listing-07-05/src/lib.rs}}
```

<span class="caption">Листинг 7-5. Объявление модуля <code>hosting</code> как <code>pub</code> для его использования из <code>eat_at_restaurant</code></span>

К сожалению, код в листинге 7-5 всё ещё приводит к ошибке, как показано в листинге 7-6.

```console
{{#include ../listings/ch07-managing-growing-projects/listing-07-05/output.txt}}
```

<span class="caption">Листинг 7-6: Ошибки компиляции при сборке кода в листинге 7-5</span>

Что произошло? Добавление ключевого слова `pub` перед `mod hosting` сделало модуль публичным. После этого изменения, если мы можем получить доступ к модулю `front_of_house`, то мы можем доступ к модулю `hosting`. Но *содержимое* модуля `hosting` всё ещё является приватным: превращение модуля в публичный не делает его содержимое публичным. Ключевое слово `pub` позволяет внешнему коду в модулях предках обращаться только к модулю.

Ошибки в листинге 7-6 говорят, что функция `add_to_waitlist` является закрытой. Правила конфиденциальности применяются к структурам, перечислениям, функциям и методам, также как и к модулям.

Давайте также сделаем функцию `add_to_waitlist` общедоступной, добавив ключевое слово `pub` перед её определением, как показано в листинге 7-7.

<span class="filename">Файл: src/lib.rs</span>

```rust,noplayground,test_harness
{{#rustdoc_include ../listings/ch07-managing-growing-projects/listing-07-07/src/lib.rs}}
```

<span class="caption">Листинг 7-7. Добавление ключевого слова <code>pub</code> у модуля <code>mod hosting</code> и функции <code>fn add_to_waitlist</code> позволяет вызывать ранее скрытую функцию из функции <code>eat_at_restaurant</code></span>

Теперь код компилируется! Давайте посмотрим на абсолютный и относительный путь и перепроверим, почему добавление ключевого слова `pub` позволяет использовать эти пути в `add_to_waitlist` с учётом правила конфиденциальности.

В случае абсолютного пути мы начинаем с `crate`, корня дерева модуля нашего крейта. Затем в корне крейта определён модуль `front_of_house`. Модуль `front_of_house` приватный, потому что функция `eat_at_restaurant` определена в том же модуле, что и `front_of_house` (то есть `eat_at_restaurant` и `front_of_house` являются родственными), мы можем сослаться на `front_of_house` из `eat_at_restaurant`. Затем идёт модуль `hosting`, он также помечен с помощью `pub`. Мы можем получить доступ к родительскому модулю `hosting`, по этому `hosting` также доступен. Наконец функция `add_to_waitlist` тоже помечена как <code>pub</code>, и в то же время можно получить доступ к её родительскому модулю, значит вызов функции работает!

В случае относительного пути логика совпадает со случаем абсолютного пути, за исключением первого шага: вместо того, чтобы начинать с корня крейта, путь начинается с `front_of_house`. Модуль `front_of_house` определён в том же модуле, что и `eat_at_restaurant`, поэтому относительный путь, начинающийся с модуля в котором определён `eat_at_restaurant` тоже работает. Тогда, по причине того, что `hosting` и `add_to_waitlist` помечены как `pub`, остальная часть пути работает и вызов функции действителен!

### Начинаем относительный путь с помощью `super`

Также можно построить относительные пути, которые начинаются в родительском модуле, используя ключевое слово `super` в начале пути. Это похоже на синтаксис начала пути файловой системы `..`. Зачем нам так делать?

Рассмотрим код в листинге 7-8, который моделирует ситуацию в которой повар исправляет неправильный заказ и лично выдаёт его клиенту. Функция `fix_incorrect_order` вызывает функцию `serve_order`, указывая путь к `serve_order` начинающийся со super:

<span class="filename">Файл: src/lib.rs</span>

```rust,noplayground,test_harness
{{#rustdoc_include ../listings/ch07-managing-growing-projects/listing-07-08/src/lib.rs}}
```

<span class="caption">Листинг 7-8: Вызов функции с использованием относительного пути, начинающегося со <code>super</code></span>

Функция `fix_incorrect_order` находится в модуле `back_of_house`, поэтому мы можем использовать `super` для перехода к родительскому модулю `back_of_house`, который в этом случае является корнем `crate`. Из корня мы пытаемся найти `serve_order` и находим его. Успех! Мы считаем, что модуль `back_of_house` и функция `serve_order` остаются в одинаковых отношениях друг с другом и должны быть перемещены вместе, если мы решим реорганизовать дерево модулей крейта. Поэтому мы использовали `super`. В итоге, в будущем нам не понадобится обновлять путь до модуля, при перемещении кода в другой модуль.

### Делаем публичными структуры и перечисления

Мы также можем использовать `pub`, чтобы сделать структуры и перечисления публичными, но есть несколько дополнительных деталей. Если используется `pub` перед определением структуры, то структура становится публичной, но поля структуры все ещё остаются приватными. Делать ли каждое поле публичным или нет решается в каждом конкретном случае. В листинге 7-9 мы определили публичную структуру `back_of_house::Breakfast` с открытым полем `toast`, но оставили приватным поле `seasonal_fruit`. Это моделирует случай в ресторане, когда клиент может выбрать тип хлеба к блюду, но повар решает, какие фрукты сопровождают блюдо на основании того, какой сейчас сезон и что есть на складе. Доступные фрукты быстро меняются, поэтому покупатели не могут выбирать фрукты или даже посмотреть, какие фрукты они получат.

<span class="filename">Файл: src/lib.rs</span>

```rust
{{#rustdoc_include ../listings/ch07-managing-growing-projects/listing-07-09/src/lib.rs}}
```

<span class="caption">Листинг 7-9: Структура с публичными и приватными полями</span>

Поскольку поле `toast` в структуре `back_of_house::Breakfast` является открытым, то в функции `eat_at_restaurant` можно писать и читать поле `toast`, используя точечную нотацию. Обратите внимание, что мы не можем использовать поле `seasonal_fruit` в `eat_at_restaurant`, потому что `seasonal_fruit` является приватным. Попробуйте убрать комментирование с последней строки для значения поля `seasonal_fruit`, чтобы увидеть какую ошибку вы получите!

Также обратите внимание, что поскольку `back_of_house::Breakfast` имеет приватное поле, то структура должна предоставить публичную ассоциированную функцию, которая создаёт экземпляр `Breakfast` (мы назвали её `summer`). Если `Breakfast` не имел бы такой функции, мы бы не могли создать экземпляр `Breakfast` внутри `eat_at_restaurant`, потому что мы не смогли бы установить значение приватного поля `seasonal_fruit` в функции `eat_at_restaurant`.

В отличии от структуры, если мы сделаем публичным перечисление, то все его варианты будут публичными. Нужно только указать `pub` перед ключевым словом `enum`, как в листинге 7-10.

<span class="filename">Файл: src/lib.rs</span>

```rust
{{#rustdoc_include ../listings/ch07-managing-growing-projects/listing-07-10/src/lib.rs}}
```

<span class="caption">Листинг 7-10. Определяя перечисление публичным мы делаем все его варианты публичными</span>

Поскольку мы сделали публичным список `Appetizer`, то можно использовать варианты `Soup` и `Salad` в функции `eat_at_restaurant`. Перечисления не очень полезны, если их варианты являются приватными: было бы досадно каждый раз аннотировать все перечисленные варианты как `pub`. По этой причине по умолчанию варианты перечислений являются публичными. Структуры часто полезны, если их поля не являются открытыми, поэтому поля структуры следуют общему правилу, согласно которому всё по умолчанию является приватными, если не указано `pub`.

Есть ещё одна ситуация с `pub` которую мы не освещали, и это последняя особенность модульной системы: ключевое слово `use`. Мы сначала опишем `use` само по себе, а затем покажем как сочетать `pub` и `use` вместе.

