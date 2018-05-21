# Неофициальное, открытое методическое пособие к программе Power BI и надстройкам над Excel Power Query и Power Pivot

### Предисловие

Первая версия данного методического пособия была создана [Максимом Уваровым](https://maximuvarov.ru) в рамках [образовательного проекта NeedForData.ru](https://needfordata.ru/). С 21.05.2018 учебное пособие опубликовано на [GitHub](https://github.com/power-bi/PowerBI-book-ru) под лицензией GPL 3.0 и с этого момента соавтором пособия может стать любой желающий.

Цель данного пособия: помочь начинающим пользователям Power BI, а также надстроек над Excel Power Query и Power Pivot, осваивать эти замечательные инструменты. Предполагается, что методическое пособие когда-нибудь станет более легковесной и человечной альтернативой текущей официальной справки по Power BI, расположенной по адресу: https://docs.microsoft.com/ru-ru/power-bi/

В данном методическом пособии поддерживаются расставление ссылок на подробные разборы описываемых тем в официальной справке Power BI или на других тематических ресурсах. 

### Отказ от ответственности

Авторы данного методического пособия не имеют отношения к корпорации Microsoft и ее продуктам Power BI, Excel, Power Query, Power Pivot. Авторы публикуют в данном методическо пособии собственноручно созданные учебные материалы.

### Лицензия на использование ##

Данное методическое пособие может бесплатно использоваться для обучения. Методическое пособие предлагается к использованию в режиме AS-IS (как есть), под лицензией GPL 3.0. Если вы используете материалы данного учебного пособия в своей документации или своих учебных пособиях, то вы обязательно должны (включая, но не ограничиваясь):

1. Поставить ссылки на первоисточник
2. Обеспечить свободный доступ к вашим материалам

### Добавление информации и внесение изменений в методическое пособие 

Любой желающий может предложить исправления текущего методического пособия на Github. Для этого нужно:  

1. [Сделать Fork проекта](https://github.com/power-bi/PowerBI-book-ru/edit/master/README.md)
2. Внести необходимые изменения на языке разметки в markdown
3. Создать Pull-request в основной репозиторий

Позже [члены редколлегии методического пособия](https://github.com/power-bi/PowerBI-book-ru/issues/1) смогут рассмотреть ваши предложения. 


## Редактор запросов (Query Editor, он же Power Query) ##

#### Что такое Power Query и как его найти в Power BI  

В Power BI Power Query встроенный модуль. В справке и интерфейсе этот модуль называется Query Editor или редактор запросов. Это основной путь загрузки данных в Power BI desktop. Как показано на скриншоте ниже все четыре выделенные кнопки относятся к редактору запросов Power Query.

![](assets/PowerQueryButtonsInPowerBI.png)

#### Что такое Power Query и как его найти в Excel 2010-2013  

Также, Power Query это надстройка над MS Excel 2010 - 2013. Она устанавливается дополнительно. Скачать надстройку можно по [ссылке](https://www.microsoft.com/en-us/download/details.aspx?id=39379). На панели Ribbon в Excel 2010 и 2013 Power Query посвящена отдельная вкладка.

![](assets/PowerQueryInExcel2013.png)  

#### Что такое Power Query и как его найти в Excel 2016  

В Excel 2016 Power Query уже встроена. Найти ее можно на вкладке Data (Данные), блок "Get and Transform".

![](assets/PowerQueryInExcel2016.png)

*В зависимости от версии подписки Excel функционал Power Query может различаться.*


#### Зачем нужен Power Query?

Power Query нужен для удобного преобразования данных (ETL-процесса).

Согласно википедии - [ETL](https://ru.wikipedia.org/wiki/ETL) (от англ. Extract, Transform, Load)  — процесс в управлении хранилищами данных, который включает в себя:

- извлечение данных из внешних источников;
- их трансформация и очистка, чтобы они соответствовали потребностям бизнес-модели;
- и загрузка их в хранилище данных.

Power Query отлично подходит для задач:

- подключения к разнообразным источникам (различным типам файлов, api, базам данных и т.п.);
- для удобного и гибкого преобразования данных в необходимый формат;
- Для создания повторяемых последовательностей обработки данных.


#### Что такое запрос (Query)

Запрос (Query) это программа на языке M, которая представляет собой  последовательность обработки данных. 

В своем теле запрос может обращаться к неограниченному количеству источников данных (включая другие запросы). В результате выполнения запроса на выходе получается: 
- таблица - table
- значение - value, 
- список - list, 
- запись - record и т.д.

Список из всех запросов в Excel можно увидеть в разных местах. 

В списке из запросов книги (Queries Pane) интерфейсе Excel 2016:

![](assets/ListOFQueriesExcel2016.png)



В интерфейсе самого Power Query:


![](assets/PowerQueryShowQueries.png)


![](assets/PowerQueryListOfQueries.png)


У каждого запроса есть свое имя. 

Имя запроса можно увидеть в нескольких местах. Там же его можно изменить: 

В интерфейсе Excel 2016. 

![](assets/PQShowPaneProperties.png)


В интерфейсе Power Query. 

![](assets/PQname.png)


По имени запроса можно обращаться к результатам этого запроса из других запросов.

![](assets/referenceOtherQueries.png)


В случае, если имя запроса содержит пробелы (например, состоит из нескольких слов), то при обращении к этому запросу из других запросов он начинается с `#` и заключается в кавычки:

	#"имя запроса"

#### Действия над запросами (по правому щелчку мыши на них)


#### Duplicate (Дублировать)


Команда Duplicate позволяет создать новый запрос и продублировать в нем все шаги исходного запроса (т.е. при дублировании появляется новый запрос с `#"Имя (2)"`, в котором содержатся все шаги из исходного запроса). Новый запрос, созданный при использовании команды Duplicate, никак не связан с оригинальным запросом. 

![](assets/duplicate.png)

#### Reference (Сослаться)


Создать новый запрос, в первом шаге которого обратиться по имени к оригинальному запросу.

![](assets/referenceOperation.png)

![](assets/referenceOtherQueries-1.png)



#### Шаг (Step)

Отдельный этап обработки данных в рамках конкретного Запроса. 

Запрос состоит из шагов и включает как минимум один шаг. 

На каждое примененное действие в интерфейсе создается новый шаг. 

Список шагов конкретного запроса можно посмотреть в правой части экрана в панели настроек Запроса.

![](assets/stepsPQ.png)


Каждый шаг это отдельная переменная, расположенная на отдельной строчке кода в скрипте запроса на языке программирования M.

Чтобы посмотреть формулу конкретного шага необходимо включить отображение строки формул на вкладке view и выбрать интересующий шаг в панели "Applied Steps".

![](assets/formulaBar.png)


Очередность шагов можно менять через интерфейс, используя контекстное меню.

![](assets/rightClickMoves.png)


А также перетаскивая шаги в списке.

![](assets/dragSteps.png)


#### Загрузка данных из различных источников в Power Query

Для того, чтобы начать работать с Power Query необходимо получить данные из какого-либо источника. Сделать это можно из интерфейса Power Query в Power BI.

![](assets/PQPBIinput.png)

В Excel 2010-2013 сделать это можно нажав на кнопки с указанием различных источников на панели Ribbon. 

![](assets/ribbonButtonsInput.png)


А также из интерфейса Power Query  в Excel.

![](assets/PQInputData.png)

#### Назначение типов данных для столбцов в Power Query


Присвоенные отдельным столбцам типы данных определяют операции, которые применимы к ним.
Если выбрать столбец, то примененные к нему типы данных можно увидеть в следующих местах:

- В Power BI типы данных обозначаются иконками в столбцах:

![](assets/IndicationOfDataTypesInPowerBI.png)

- В Power BI и Excel на вкладке «Home»

![](assets/DataTypeInHomeTabPowerQuery.png)

- В Power BI и Excel на вкладке «Transform»

![](assets/DataTypeInTransformTabPowerQuery.png)

#### Какие типы данных существуют в Power Query?

На момент написания данного пособия в Power Query были следующие типы данных:
![](assets/DataTypesPowerQuery.png)


- Decimal number - десятичное число
- Fixed Decimal number - десятичное округленное до 4 знака
- Whole number - целое число
- Date / Time - дата / время
- Date - дата
- Time - время
- Date / Time / Timezone - дата / время / часовая зона
- Duration - длительность
- Text - текст
- True/False - истина / ложь
- Binary - двоичный код (например, изображение в формате bmp)

К тому же, в отдельных ячейках в Power Query могут быть структурированные типы данных:  

- Table - таблица
- List - список 
`{1,2,4} - список из элементов Чисел со значениями 1, 2, 4`

- Record - запись  
```[field1 = "текст в кавычках", field2 = "текст в кавычках2"]
```


#### Автоматическое определение типов данных

В Power Query есть возможность автоматически определять типы данных. Она будет пытаться сделать это по тысяче первых строчек конкретного столбца. 

![](assets/autmaticDataType.png)



**Создание дубликата столбца**


![](assets/duplicateColumn.png)


Контекстное меню:

![](assets/duplicateContext.png)


#### Переименование столбцов


Чтобы переименовать столбец нужно дважды щелкнуть на его названии:

![](assets/renameHeader.png)

#### Remove Other Columns - удаление прочих столбцов


Для повышения личной эффективности (за счет лучшего фокуса на конкретных цифрах), сохранения оперативной памяти и поддержки быстродействия моделей нужно стараться оставлять в модели только необходимые данные (только необходимые столбцы и строчки).

Для этих целей отлично работает команда "remove other columns" (удалить прочие столбцы). 

![](assets/removeOtherColumns.png)


**Split Column by Delimeter - Разделить текстовый столбец по разделителю**


Кнопка на Ribbon - Split Column

![](assets/splitRibbon.png)

Правой кнопкой на заголовке столбца

![](assets/splitRightMenu.png)


**Разделить столбец по произвольному разделителю**


![](assets/chooseOwnDelimeter.png)

Указать максимальное количество столбцов

![](assets/maxColumns.png)

#### Операции над таблицами в Power Query

#### Append - добавление одной таблице к другой таблице 


Из интерфейса Power Query:

![](assets/appendPQ.png)


![](assets/appendPQ2.png)

Из интерфейса Excel:

![](assets/appendExcel2016.png)

![](assets/apeend2.png)


#### Merge - соединение данных одного запроса с другим запросом по общему ключу (аналог ВПР)


Начало операции из интерфейса Power Query:

![](assets/merge2.png)

Начало операции merge из интерфейса Excel:

![](assets/merge1.png)

Выбор таблицы, из которой будем подтягивать данные, определение ключевых столбцов и типа операции

![](assets/merge3.png)


#### Соединение данных по составному ключ в Power Query


![](assets/merge4.png)



После нажатия на кнопку OK мы видим новый столбец с кнопкой

![](assets/merge6.png)


Нажимаем на кнопку, раскрываем столбец и выбираем желаемую операцию

Expand - развернуть данные из выбранных столбцов

![](assets/merge7.png)



Aggregate - подсчитать данные в конкретных столбцах

![](assets/merge9.png)

![](assets/merge10.png)

Важно помнить что типы данных у ключевых столбцов (в обеих таблицах) должны быть одинаковыми.

#### Извлечение данных из файлов лежащих в папке


Выбираем в качестве типа источника папку.
Далее выбираем конкретную папку с файликами, которые предполагается объединить. 
Файлики должны быть одного типа и с одинаковыми столбцами. 

![](assets/folderFilesPreview.png)


В появившемся окошке предпросмотра данных жмем на кнопочку edit. 


#### Команда Group by (сгруппировать по полю)


Команду можно вызвать по клику на кнопку на панели Ribbon

![](assets/groupByButton.png)

Также команду можно вызвать из контекстного меню (если нажать правой кнопкой на заголовке столбца)

![](assets/groupByRightClick.png)


Интерфейс команды Group By с комментариями представлен на скриншоте ниже:

![](assets/groupBy2.png)


#### Добавление нового столбца в Power Query


![](assets/newColumn2.png)

![](assets/addNewColumn3.png)


**if then else условия**


Для выбора действия в зависимости от условия в Power Query используется структура с оператором if then else

Пример:

if [столбец1] 0 then [столбец2] else [столбец3]

![](assets/ifthenelse1.png)

**Conditional column**


![](assets/conditional1.png)

![](assets/conditional2.png)


#### Изменение типа столбца с текстового на десятичный, в случае если в качестве разделителя десятичной части используется точка вместо запятой


1. Необходимо щелкнуть правой кнопкой на заголовке столбца
2. Выбрать пункт «Change type»
3. И далее выбрать пункт «Using locale»
	 ![](assets/changeAsLocale.png)

4. Выбираем страну, где в качестве разделителя используется точка (например, USA)
![](assets/changeAsLocale2.png)

#### Удалить дубликаты в столбцах


Команда "Remove Duplicates" проходит по выбранным столбцам (если выбрана вся таблица, то по всей таблице) и смотрит в них повторяющиеся ячейки (строчки, в случае если выбрана таблица). Если дубликаты найдены функция оставляет первую попавшуюся уникальную строчку и удаляет все последующие повторяющиеся
Найти команду можно на Ribbon - Home - Remove Duplicates (Удалить дубликаты в выбранных столбцах)

![](assets/removeDuplicates.png)

Либо найти команду можно щелкнув правой кнопкой на заголовке одного или нескольких выбранных столбцов. В случае, если выбраны несколько столбцов, то тогда будут удалены все неуникальные сочетания значений в каждой отдельной строчке в выбранных столбцах.

![](assets/removeDuplicates2.png)


Удалить дубликаты строк в таблице можно нажав на кнопку в левом верхнем углу таблицы предпросмотра.

![](assets/removeDuplicates3.png)


Аналогичного результата можно добиться если использовать команду "Group By"

**Count rows - Подсчитать количество строчек в текущей таблице**


![](assets/countRows2.png)


#### Извлечение шагов в отдельный запрос


Для выполнения необходимо щелкнуть правой кнопкой на конкретном шаге обработки. 
Выбрать пункт меню «Extract previous steps»

![](assets/extract1.png)


ввести имя нового запроса, который будет создан на основе предыдущих шагов

![](assets/extract2.png)

#### Права доступа, Formula.Firewall


Текст взят из [Power bi formula firewall privacy settings - marketing-wiki.ru](http://marketing-wiki.ru/wiki/Power_bi_formula_firewall_privacy_settings)

При работе в Power BI, при обращении к внешним источникам данных вроде различных API могут возникать ошибки вроде:
OLE DB or ODBC error: [information is needed in order to combine data] 

или
Formula.Firewall: Query is accessing data sources that have privacy levels which cannot be used together. Please rebuild this data combination 

Это ошибки, которые возникают из-за встроенного в Power BI Fomrula.Firewall - механизма, который следит, чтобы данные из Power BI передавались только согласно выставленным правилам доступа.

то есть Power Bi пытается защитить нас, чтобы мы случайно не отправили какие-либо данные (вроде токена) на сервер-злоумышленника.

Однако, если мы работаем с API, то нам неминуемо нужно отправлять данные в интернет. Соответственно, чтобы не иметь проблем в этом процессе проще всего в настройках Power BI выключить Formula.Firewall. Это делается в разделе Privacy. Нужно выбрать 3-й пункт - "ignore privacy level settings"


## Power Pivot 

#### Что такое Power Pivot в Excel?

Power Pivot - это надстройка над Excel, представляющая из себя быструю колоночную базу данных VertiPaq с языком запросов DAX (часто вместо VertiPaq говорят Power Pivot).  В отличие от Excel число строк загруженных в Power Pivot ограничено лишь размером доступной оперативной памяти компьютера. Быстродействие Power Pivot во много раз превосходит быстродействие формул в Excel. Также Power Pivot по производительности превосходит и Power Query (при этом часто он потребляет меньше ресурсов). 
Результаты выполнения запросов доступны пользователям в сводных таблицах и сводных диаграмма MS Excel. Таким образом сводные таблицы выступают аналитическим интерфейсом к данным хранящимся в Power Pivot. 

#### Что такое Power Pivot в Power BI?

В Power BI Power Pivot встроен как база данных, к которой присоединяются различные визуализации. 

#### Что такое DAX?

Dax (Data Analysis Expressions) - это язык программирования использующийся для запросов в базе данных VertiPaq. 

#### Модель данных

Модель данных - совокупность таблиц, связей между ними и вычисляемых мер в базе данных VertiPaq. Благодаря своей быстроте модель данных позволяет создавать мгновенно пересчитывающиеся меры, которые, в свою очередь, позволяют создавать интерактивные визуализации. 

#### Таблицы

Таблицы - совокупность строк, разделённых на столбцы. 

У каждого столбца задан тип данных (который, как правило, наследуется из типов данных заданных для столбцов в Power Query). 

У столбцов с числовыми типами данных можно увидеть значок сигмы Слева от них. И такие столбцы по умолчанию будут просуммированы, в случае если добавить их в область значений любой визуализации. 

![](assets/DraggedImage-4.png)

Если же добавить в область значений столбцы с не числовыми типами данных (без значка сигмы), то к ним будет применена операция по умолчанию: count (подсчет количества значений). 

Список из таблиц загруженных в модель данных можно найти в дереве fields в правой части окна Power BI.

![](assets/DraggedImage-5.png)

Каждая таблица имеет название, по которому к данным конкретной таблицы можно обращаться в мерах и вычисляемых столбцах.
В случае если в названии таблицы присутствует пробел или не латинские символы, то при обращении к таблице извне её название заключается в одинарные кавычки автоматически:

`'название с пробелом'`

Однако, если мы заключим в кавычки название таблицы без пробелов, то все будет работать как предполагалось:

`'название'`


#### Функции Dax

Функции языка Dax похожи на функции Excel, с той лишь разницей, что в качестве аргументов используют столбцы, целые таблицы или скалярные выражения (простые значения), а не ячейки.

В качестве разделителей аргументов в зависимости от локали используются:
- ";" (и "," для десятичных)
- "," (и "." для десятичных)

#### Меры (Measures)

Вычисляются только в момент использования.
Рассчитываются в рамках текущего контекста фильтров. Именно это свойство позволяет строить интерактивные визуализации, которые фильтруются при нажатии на определенные области конкретных визуализаций. 
Меры хоть и принадлежат конкретной таблице, но могут безболезненно быть перенесены в любую другую в рамках документа. Поэтому хорошая практика при использовании мер формулах не включать название таблицы, в которой мера лежит. То есть вместо 'таблица'[мера] писать просто [мера]

#### Вычисляемые Столбцы (Calculated Columns)

Рассчитываются однажды во время обновления таблицы в модели данных.
Вычисляемые столбцы занимают место в памяти. 
Вычисляемые столбцы рассчитываются в рамках контекста строки. 
В отличие от мер, вычисляемые столбцы могут использоваться для фильтрации и сортировки таблиц.
Принадлежат конкретной таблице и их лучше указывать в формулах вместе с названием таблицы, даже если Power Pivot позволяет этого не делать.

Подробнее про столбцы и меры читать здесь:  

- [Calculated Columns and Measures in DAX - SQLBI](http://www.sqlbi.com/articles/calculated-columns-and-measures-in-dax/)

#### Контекст выполнения функции (Evaluation context)

В Power Pivot существуют два контекста выполнения формулы, которые действуют одновременно:

- Контекст фильтров (Filter context) 
- Контекст строк (Row context)

Это массивная и сложная тема. На момент написания методички автор так и не разобрался с темой до того уровня, чтобы рассказывать об этом окружающим. Потому рекомендую обратиться к достоверным источникам вроде:  

- Марко Руссо и Альберто Феррари [https://www.sqlbi.com/](https://www.sqlbi.com/).
- Справка Microsoft Power BI: [Основные сведения о DAX в Power BI Desktop](https://docs.microsoft.com/ru-ru/power-bi/desktop-quickstart-learn-dax-basics#context)

#### Связь таблиц в модели данных 

Для связи таблиц в модели данных в одной из таблиц в ключевом поле должны быть уникальные значения. 
Также столбцы должны быть одного типа данных.

Направление связи имеет значение. 
Вычисляемые столбцы могут использоваться для создания связей между таблицами.

Справка:
[Создание связей и управление ими в Power BI Desktop - Power BI | Microsoft Docs](https://docs.microsoft.com/ru-ru/power-bi/desktop-create-and-manage-relationships)

#### Часто используемые функции DAX

`SUM (Столбец)` - Cумма чисел по столбцу

`COUNTA (Столбец)` - Количество значений в столбце

`DISTINCTCOUNT (Столбец)` - Количество уникальных значений в столбце

`SUMX (Таблица, Выражение)` - Сумма значений выражения, которое выполняется для каждой строчки таблицы

`DIVIDE (Значение числителя, значение знаменателя, альтернативный вариант в случае ошибки деления числителя на знаменатель)` - Безопасное деление

`IFERROR (Значение, Значение если ошибка)` - Если ошибка

`IF (Логическое выражение, значение если правда, значение если ложь )` - Если

#### Метрики контекстной рекламы в DAX

CTR (Кликабельность) 

	= SUM ( Показы ) / SUM ( Клики )

CPC (Цена клика) 

	= SUM ( Расход ) / SUM ( Клики )

Ставка (Максимальная цена клика установленная рекламодателем)

Ставка Средняя

	= AVERAGE ( ставка )

Ставка СреднеВзвешенная на клики

	= SUMX ( ставка * клики ) / SUM ( клики )

Ставка СреднеВзвешенная на показы

	= SUMX ( ставка * показы ) / SUM (показы)

CR (Коэффициент конверсии фактический)

	= SUM ( транзакции ) / SUM ( сессии )

Ключевая фраза: количество

	= COUNTA ( ключевая фраза )

Ключевая фраза: количество уникальных

	= DISTINCTCOUNT ( ключевая фраза )


#### Про абсолютные и относительные метрики в выгрузках

Средний показатель отказов рассчитывается по формуле:

	= SUM ( отказы ) / SUM ( визиты ) 


Если в выгрузке нет абсолютного числа ОТКАЗОВ, но есть ПОКАЗАТЕЛЬ ОТКАЗОВ, то для каждой строчки с исходными данными предварительно необходимо рассчитать абсолютное число ОТКАЗОВ. Для этого нужно умножить ПОКАЗАТЕЛЬ ОТКАЗОВ на ЧИСЛО ВИЗИТОВ. После этого у вас появится возможность рассчитывать средний показатель отказов корректно. 

Аналогичным образом следует поступить с глубиной просмотра и временем на сайте. 

Распространенная ошибка рассчитывать СРЕДНИЙ ПОКАЗАТЕЛЬ ОТКАЗОВ в качестве встроенной меры AVERAGE по столбцу ПОКАЗАТЕЛЬ ОТКАЗОВ (см скрин. http://bit.ly/2JMKSl1). 

![](assets/WrongAverageBounceRateCalculationInPowerBI.png)

Так средний показатель отказов рассчитывать некорректно. 

#### Полезные ресурсы по DAX

- [sqlbi.com/articles/calculated-columns-and-measures-in-dax/](http://www.sqlbi.com/articles/calculated-columns-and-measures-in-dax/)
- [powerpivotpro.com/2013/02/when-to-use-measures-vs-calc-columns/](http://www.powerpivotpro.com/2013/02/when-to-use-measures-vs-calc-columns/)
- [Клевый курс на udemy про Power Pivot](https://www.udemy.com/power-pivot-workshop-beginner/learn/v4/overview)
- [Книга: The Definitive Guide to DAX: Business intelligence with Microsoft Excel, SQL Server Analysis Services, and Power BI (Business Skills) 1st Edition](https://www.amazon.com/Definitive-Guide-DAX-intelligence-Microsoft/dp/073569835X/ref=asap_bc?ie=UTF8)
- [Daxpatterns.com](http://www.daxpatterns.com/)
