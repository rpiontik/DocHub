## Введение

DocHub - инструмент описания архитектуры через код (Architecture as a code). Код архитектуры - ансамбль 
файлов на [языках](#langs), решающих задачу описания архитектуры. 

Функциональность DocHub можно представить Mind Map:
![Карта памяти DocHub](@document/dochub_mindmap)

![](@anchor/problems)
## Решаемые проблемы

1. [Управление версиями архитектуры](#versions);
2. [Управление децентрализованной архитектурой в Agile-ориентированных компаниях](#distrib);
3. [Управление архитектурой холдинга (экосистем)](#ecosystem);
4. [Создание архитектурных фасадов](#facade).

![](@anchor/versions)
## 1. Управление версиями архитектуры 
![>Управление версиями](@document/dochub_archver)

В развивающихся проектах архитектура мутабельна. Стандартной ситуацией является одновременная проработка нескольких 
архитектурных решений, которые должны стать единым целым. Особенно выражена данная проблема при наличии нескольких
автономных команд создающих единую систему.

Для монокомандых систем проблема остается актуальной. Внезапное изменение приоритетов и требований приводит 
к накапливанию противоречивых архитектурных решений. Формируется технический долг.

Аналогичные проблемы свойственны кодовой базе систем. В процессе параллельной разработки фич, разработчики 
сталкиваются с задачей объединения результата в релизы. Решается она через инкрементальное развитие кода. 
Популярным инструментом является - git. 

Практикуются различные методологии управления кодом. Из популярных можно выделить 
[GitFlow](https://www.atlassian.com/en/git/tutorials/comparing-workflows/gitflow-workflow) и
[GitHub flow](https://docs.github.com/en/get-started/quickstart/github-flow).

Идея заключается в том, что разработчик при создании новой фичи клонирует ветку (branch) общей кодовой базы в 
отдельную. В ней он ведет разработку. По завершению работы создается Pull request / Merge request. Это 
специальный, формализованный запрос в рамках системы управления версиями на объединение веток. Он оценивается 
(Code review) другими разработчиками. В случае положительного решения, изменения внедряются в общий код.

Решать запросы на объединение помогают инструменты сравнения встроенные в системы управления версиями. Они наглядно
отображают изменения в коде. Выявляют конфликты. Позволяют их устранять. 

В отличие от процесса разработки, где все построено на коде, архитектура требует создания графических артефактов.
Для этого используются визуальные редакторы. Объединение версий диаграмм является проблемой. Тратятся значительные
ресурсы на механическую деятельность.

DocHub предлагает отказаться от использования визуальных редакторов в пользу описания архитектуры кодом. Использовать
принципы управления архитектурой аналогично принципам управления кодовой базой. Для этого предоставляются четыре
языка описания архитектуры:

![](@anchor/langs)
* [PlantUML](https://plantuml.com/) - позволяет создавать диаграммы из обычного текстового языка;
* [Markdown](https://ru.wikipedia.org/wiki/Markdown) - язык разметки, созданный с целью обозначения форматирования в тексте;
* [Swagger](https://swagger.io/) - язык описания интерфейсов для описания RESTful API;
* [Манифесты](/docs/dochub_contexts) - структурированные файлы в формате YAML/JSON для описания архитектурных объектов. 

Таким образом, процесс развития архитектуры становится максимально близким к разработке систем. Это дает возможность,
помимо решения основной проблемы (управление версиями), получить дополнительные преимущества:

* Унифицировать процессы развития архитектуры и разработки;
* Архитектурные артефакты могут быть размещены непосредственно в репозитории кодовой базы и развиваться одновременно
с кодовой базой системы;
* Возникает возможность управления архитектурными идеями через Pull request;
* Создается база для взаимного проникновения экспертиз разработки и проектирования.

![](@anchor/distrib)
## 2. Управление децентрализованной архитектурой

Под "децентрализованной" понимается сложная, многокомпонентная архитектура системы, части которой распределены 
по командам разработки. Каждая команда развивает свой сегмент параллельно и независимо, но должна учитывать общую 
концепцию. Ярким примером является микросервисная архитектура.

![>Управление децентрализованной архитектурой](@document/dochub_archdistrib)

На первый план здесь выходит синхронизация решений команд, влияющих на общий архитектурный ландшафт. Остро стоит
вопрос управления технологическим стеком и переиспользование имеющихся в компании наработок.

Управление архитектурой "как код", позволяет применить опыт Open Source сообществ. В этом случае существует 
центральный репозиторий с концептуальной архитектурой (как будет). Все имеют доступ к нему, получая необходимые
сведения о планах развития. Изменения в репозиторий попадают через Pull requests. Ревьюверами являются техлидеры
команд.

Таким образом достигается информирование об архитектурных решениях. Возникает консенсус. Происходит обмен опытом. 

Описание архитектуры “как есть” остается в командах. Т.е. несмотря на то, что имеется централизованный репозиторий
"как будет", у команд остается право на автономное принятие быстрых решений. Этот подход реализует
[Agile манифест](https://wikipedia.org/wiki/Agile_Manifesto). Если необходимо срочно внести обоснованные изменения
в продукт, должна быть возможность это сделать. Такая ситуация считается инцидентом.

Противоречие с центральным репозиторием устраняется путем сверки "как есть" с "как будет". Отклонения обосновываются
и с отставанием вносятся. Таким образом, инцидентные решения остаются в поле управления.  

![](@anchor/ecosystem)
## 3. Управление архитектурой холдинга (экосистем)

![>Структура холдинга](@document/dochub_archeco)

Под холдингом понимается группа компаний развивающих цифровые продукты имеющие потребность в интеграции с выраженным
центром стратегического управления.

Холдинги имеют проблемы координации развития архитектуры экосистемы. Контроль достижения стратегических целей 
является ключевым для них.

Компании холдинга имеют разную степень автономности. Часто находятся на различных этапах развития. Это выражается
в неоднородности процессов управления.  

Таким образом, управление архитектурой экосистемы является нетривиальной задачей. DocHub предлагает и тут использовать
принципы развития кодовой базы Open Source сообществами.

![<Управление архитектурой холдинга](@document/dochub_archeco_proc)

Центр в этом случае выступает майнтейнером (Maintainer) архитектурного кода. Он является владельцем центрального
репозитория архитектуры. Устанавливает стандарты работы с ним.

Компании выступают в роли контрибьюторов (Contributors). У них есть собственный форк или ветка в центральном 
репозитори. Развитие архитектуры экосистемы ведется через Pull requests.

DocHub используется как универсальное средство представления артефактов экосистемы.

![](@anchor/facade)
## 4. Архитектурные фасады

![>Архитектурные фасады](@document/dochub_facade)

Под архитектурным фасадом понимается публичная часть архитектуры. Распространенным примером являются API-контракты
сервиса. 

Фасады могут иметь различную степень детализации и состав. В некоторых случаях для клиента достаточно только 
публикации контрактов. Но зачастую, у него возникает ряд вопросов по сценариям использования. Также может
оказаться полезным отразить верхнеуровневую архитектуру внешних сервисов. Для решения этой задачи необходим
комплект публичных артефактов.

DocHub с этой задачей хорошо справляется. Он может быть развернут в качестве архитектурного фасада. Внешние 
пользователи получают удобный интерфейс для изучения публичной архитектуры.