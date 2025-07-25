# <a name="up" /> Проект Я.Маршруты
Я.Маршруты это сервис, который строит маршруты для транспорта разных видов, рассчитывает время и стоимость поездки.
Тестирование веб-приложения

## Содержание
- [Задачи тестировщика](#задачи-тестировщика)
- [Требования по проекту](#требования-по-проекту)
- [Инструменты](#инструменты)
- [Процесс работы](#процесс-работы)
  - [1 спринт](#1-спринт)
  - [2 спринт](#2-спринт)

## Задачи тестировщика

<details>
<summary> 1-спринт </summary> 

#### Задачи для 1 спринта

1. Анализ документации (требований) к сервису Яндекс.Маршруты 1.0
2. Выделить классы эквивалентности и граничные значения для полей ввода (часы, минуты, откуда и куда)
3. Проектировка тестов для расчёта стоимости и времени поездки

***

</details>

<details>
<summary> 2-спринт </summary> 

#### Задачи для 2 спринта
 
1. Проанализировать требования к функциональности "Каршеринг"
2. Подготовить тестовую документацию, для проверки вёрстки формы бронирования 
3. Подготовить тестовую документацию, для проверки логики окон "Способ оплаты", "Добавление карты" и кнопки "Забронировать"
4. Протестировать приложение и завести баг-репорты

***
   
</details>


## Требования по проекту

<details>
<summary>Требования к сервису Яндекс Маршруты 1.0 </summary>

### Общее описание
Яндекс.Маршруты — сервис, который строит маршруты для транспорта разных видов. Рассчитывает время и стоимость поездки.  
В этом сервисе доступны несколько режимов: «Оптимальный», «Быстрый», «Свой».  
В режиме «Свой» панель видов транспорта активна, можно выбрать тип транспорта. Система построит маршрут.   
Если выбрать режим «Оптимальный» или «Быстрый», система автоматически определит вид транспорта и построит маршрут. Панель видов транспорта станет неактивна.  

### Макеты
![макет1](https://github.com/user-attachments/assets/7906d45b-422d-4615-9c04-25236e51c78e)
![макет2](https://github.com/user-attachments/assets/b1dfc578-c3d0-4bc2-b32b-147dcc33809e)
![макет3](https://github.com/user-attachments/assets/efb87969-7133-4e5d-af0b-dcf8ac6dc5a9)

### Интерфейс
В интерфейсе есть поля «Время начала поездки», «Откуда», «Куда». Переключатели режимов маршрута: «Оптимальный», «Быстрый» и «Свой», а также переключатели видов транспорта: свой автомобиль, каршеринг, такси, самокат, велосипед и пешком.  
Пользователь вводит время отправления. Чтобы построить маршрут, нужно ввести улицу и номер дома в поля «Откуда» и «Куда». В начале и конце адреса могут быть пробелы: они допустимы, но при снятии фокуса система удалит их.  

#### Описание работы интерфейса
В стартовом состоянии поля «Время начала поездки», «Откуда» и «Куда» пустые. Режимы маршрутов «Оптимальный», «Быстрый и «Свой» не выбраны; панель переключения видов транспорта неактивна.

#### Логика работы полей «Откуда» и «Куда»
Если поля адреса заполнены корректно, на карте отображаются точки А и В. Если поле «Откуда» заполнено некорректно, точка А не отображается. Если поле «Куда» заполнено некорректно, точка В не отображается. При некорректном значении поле подсвечивается красным; появляется сообщение об ошибке.  
Примеры тестовых адресов есть в таблице.

#### Режим «Оптимальный» и «Быстрый»
Если выбрать режим «Оптимальный» или «Быстрый», система автоматически назначит вид транспорта; построится маршрут; отобразится время и стоимость поездки. Выбрать транспорт в этих режимах нельзя — панель видов транспорта неактивна.

#### Режим «Свой»
Если выбрать режим «Свой», панель видов транспорта активна — можно переключать. Под каждый вид транспорта строится маршрут; рассчитывается время и стоимость поездки.  
Если сменить вид транспорта или поменять значение в любом поле, маршрут перестроится; время и стоимость поездки пересчитается.

#### Ограничения
![макет4](https://github.com/user-attachments/assets/76a7c5ef-218d-4bc8-aa6e-79e174fae72d)

### Логика расчёта
Система получает данные о начале поездки, точке А и точке В. После этого рассчитывает продолжительность и стоимость поездки по определённому алгоритму.
![макет5](https://github.com/user-attachments/assets/33b8096b-0be6-4031-a5c4-1ffa9350c60f)

#### Алгоритм: формулы
Стоимость и время поездки зависят от скорости и длины маршрута.  
Скорость зависит от времени начала поездки.  
Длина маршрута – от точек А и Б на карте и построенного маршрута.  
Расчёт времени поездки происходит по формуле:   
t = S/V  
Расчёт стоимости поездки происходит по формуле:   
Р (итоговая) = S * P (за километр) ИЛИ t * P (за время).  
Вид транспорта, скорость и стоимость  
Расстояние, скорость и стоимость за минуту или километр можно получить из таблиц. Этих данных достаточно, чтобы рассчитать время и стоимость поездки для каждого вида транспорта.  

![макет6](https://github.com/user-attachments/assets/1c92f6e1-aa33-4322-af6f-ec8f4e0e19c4)

#### Средняя скорость автомобиля

<img width="544" height="254" alt="2025-07-17_13-11-51" src="https://github.com/user-attachments/assets/848aaa45-99b3-4656-a566-94c6998405c5" />

#### Средняя скорость такси с учётом движения по выделенным полосам

<img width="536" height="250" alt="2025-07-17_13-13-37" src="https://github.com/user-attachments/assets/c7aee758-1077-42d0-9f74-d32cb534527d" />

#### Матрица расстояний между адресами для автомобильных дорог, в километрах

<img width="574" height="712" alt="2025-07-17_13-22-38" src="https://github.com/user-attachments/assets/8e64f805-c1d7-4beb-9dec-edecd9ea6d2b" />

#### Матрица расстояний между адресами для пешеходов, в километрах

<img width="573" height="711" alt="2025-07-17_13-24-02" src="https://github.com/user-attachments/assets/70a39ff2-fc3b-43db-8541-60d12d5651a7" />

### Дополнительная информация
#### Алгоритм
Чтобы рассчитать время и стоимость маршрута, тестировщикам доступны таблицы со скоростью движения разных видов транспорта в разное время суток.   
Если взять такие тестовые значения, что поездка захватит несколько временных интервалов, алгоритм выберет скорость автомобиля из того диапазона, в котором поездка началась.

![Скриншот 17-07-2025 132637](https://github.com/user-attachments/assets/cbc4bcac-e22d-486f-882c-55ceb8bb23e9)

#### Фокус
На макете есть несколько полей: «Время начала поездки», «Откуда» и «Куда». Валидация полей срабатывает, если фокус уходит из поля.   
Фокус — это состояние элемента интерфейса, когда элемент активен. К нему относятся все действия пользователя. 

#### Часы
В интерфейсе есть часы. Внутри — два поля ввода: часы и минуты. Обязательно применять ноль в начале, если число однозначное. Например: 09:09.  
Это значит, что длина строки — всегда два символа. Чтобы проверить, что поля работают правильно, нужно указать и корректный, и неразрешённый вариант длины.   

***

</details>

<details>
<summary>Требования к функциональности «Каршеринг»</summary>

#### Общее описание функциональности "Каршеринг"
Пользователю нужно открыть Яндекс.Маршруты и корректно заполнить поля «Откуда» и «Куда». Приложение построит маршрут, а под полями «Откуда» и «Куда» отобразятся режимы поездки: «Оптимальный», «Быстрый», «Свой».  
- Если выбрать режим «Оптимальный» или «Быстрый», система автоматически назначит способ передвижения: на авто, пешком, на такси, на самокате, на велосипеде, на каршеринге. Выбрать его самостоятельно нельзя — иконки неактивны.  
- Если выбрать режим «Свой», способ передвижения можно поменять — иконки активны.

#### Аренда машины
Арендовать машину можно в двух случаях:   
- Если приложение предлагает тип транспорта «Каршеринг» в режиме «Оптимальный» или «Быстрый».
- Если пользователь выбирает тип транспорта «Каршеринг» в режиме «Свой».  
Под названиями режимов появится информация о стоимости и продолжительности поездки, а также кнопка «Забронировать».

![Скриншот 17-07-2025 132935](https://github.com/user-attachments/assets/0d896056-245e-44b0-a5ac-aaabb09dbf88)

Если нажать кнопку «Забронировать», вместо панели с названиями режимов появится форма бронирования. В форме нужно выбрать тариф, добавить информацию о водительских правах, указать способ оплаты. Дополнительно можно перечислить требования к заказу.   
Под «Требованиями к заказу» расположена кнопка «Забронировать». См. таблицу [«Состояние кнопки»] ![Скриншот 17-07-2025 171310](https://github.com/user-attachments/assets/aaced127-f305-4dc0-a2c4-434e1fe9baf5)
 
Если пользователь передумал арендовать машину, он может вернуться назад — это иконка со стрелкой влево. На экране снова откроется блок, где нужно выбрать способ передвижения.

#### Форма бронирования
На экране бронирования можно удалять адреса — они необязательны для заказа каршеринга. Пользователь может выбрать нужную машину на карте.

Ограничения полей

![Скриншот 17-07-2025 171820](https://github.com/user-attachments/assets/331f89ea-be72-4bcf-88b9-7d63555145ec)


<img width="834" height="1216" alt="Untitled" src="https://github.com/user-attachments/assets/82a38c6c-68ab-4e11-a7fe-f8882df0dafb" />

По умолчанию выбран тариф «Повседневный», поля «Добавить права» и «Способ оплаты» не заполнены.   
Выбранный тариф подсвечивается серым. Под ним расположен блок с деталями тарифа и информацией о ближайшей машине:   
- марка;  
- описание тарифа;  
- время в пути от пункта «Откуда» до машины — не будет отображаться, если пользователь удалит адрес в поле «Откуда»;  
- время бесплатного ожидания;  
- изображение машины;  
- дополнительные параметры.    
Система автоматически выбирает ту машину, которая находится ближе всего к пользователю. На карте иконка ближайшей машины увеличивается, над ней появляется чёрная плашка с маркой машины.   
Остальные свободные машины продолжают отображаться на карте в виде иконок. При этом показываются автомобили всех тарифов. Пользователь может выбрать машину на карте и забронировать: он нажимает на иконку, она увеличивается, над ней появляется чёрная плашка с маркой, а на левой панели — обновлённая информация о машине.  
Если пользователь ещё не привязал банковскую карту, вместо слова «Карта» стоит слово «Добавить». Без карты забронировать машину нельзя.  
По умолчанию приложение показывает точную стоимость поездки. Она рассчитывается по формуле — см. пункт «Формула расчёта тарифов». Если удалить хотя бы один адрес из полей «Откуда» или «Куда», отобразится стартовая цена за минуту.

![Скриншот 17-07-2025 172200](https://github.com/user-attachments/assets/49fefbe7-7085-4326-89a3-50712772626a)

#### **Панель «Выбор тарифа»**
Есть три тарифа. Каждый элемент состоит из иконки автомобиля, названия тарифа, цены.  
Один из тарифов всегда выбран. По умолчанию это тариф «Повседневный», но его можно изменить. 

#### Описания тарифов
Под списком тарифов есть блок с подробным описанием выбранного тарифа.

![Скриншот 17-07-2025 172243](https://github.com/user-attachments/assets/8ac1321c-d925-4acc-9d7b-1b67be878206)

![Скриншот 17-07-2025 172312](https://github.com/user-attachments/assets/f6609cd4-5b22-4703-97a4-ff62482bb32c)

#### Формула расчёта стоимости тарифов
Стоимость тарифа рассчитывается по формуле:  
*фиксированная стоимость аренды в рублях + (60 * стоимость минуты поездки в рублях * продолжительность поездки в часах) * коэффициент тарифа = стоимость поездки*    
Например, стоимость поездки по тарифу «Повседневный»:  
*150 + (60 * 6 * 1.25) * 1.5 = 825*  
Пояснения к формуле:  
- **150** — фиксированная стоимость аренды в рублях;  
- **60** — минут в одном часе;  
- **6** — стоимость минуты поездки на каршеринге в рублях;  
- **1.25** — продолжительность поездки в часах;  
- **1.5** — коэффициент тарифа «Повседневный».  

**Коэффициенты:**
- Повседневный: 1.5.  
- Походный: 2.  
- Роскошный: 3.  

**Продолжительность поездки** **в часах** рассчитывается так: расстояние / скорость. 
- Расстояние — см. таблицу с адресами в общих требованиях.  
- Скорость — см. таблицу со скоростями в общих требованиях.  

#### Поле «Добавить права»

![Скриншот 17-07-2025 172408](https://github.com/user-attachments/assets/8c11e8cc-f87f-4544-aed7-f067c6c65720)


Если не добавить водительское удостоверение, забронировать машину не получится.     
По умолчанию поле «Добавить права» не заполнено. Когда пользователь нажимает на поле, появляется окно «Добавление прав». В нём нужно ввести имя, фамилию, дату рождения и номер водительского удостоверения.   
Текст, который вводит пользователь, чёрного цвета.   
Когда пользователь внёс все данные, появляется сообщение: «Спасибо! Документы отправлены на проверку. Скоро расскажем о результатах». Под сообщением — кнопка «Понятно».   
Если нажать кнопку «Понятно», окно закроется, а в поле «Добавить права» появится таймер на 30 секунд. Через 30 секунд система сообщает, прошли ли документы верификацию. 

#### Ограничения поля "Добавить права"

![Скриншот 17-07-2025 172554](https://github.com/user-attachments/assets/af579c3b-95a0-4294-9236-0866daa89a1f)


#### После верификации
Если документы прошли верификацию, рамка поля подсвечивается зелёным, у правого края внутри поля появляется зелёная галочка. Пользователь больше не сможет редактировать данные водительского удостоверения. Несколько водительских удостоверений добавить нельзя.   
Если документы не прошли верификацию, рамка поля подсвечивается красным, у правого края внутри поля появляется красный крестик. Если нажать на поле, снова откроется форма «Добавление прав». Над формой — текст сообщения: «Ваши документы не прошли верификацию. Попробуйте ещё раз».

#### Поле «Способ оплаты»
По умолчанию поле не заполнено. Чтобы забронировать машину, нужно ввести реквизиты хотя бы одной карты и нажать кнопку «Привязать». Можно добавить неограниченное количество карт.   
При нажатии на поле «Способ оплаты» открывается окно «Способ оплаты» с возможностью привязать новую карту или выбрать уже привязанную.  
Чтобы добавить новую, нужно нажать на кнопку «Добавить карту». После этого откроется окно «Добавление карты».  
При успешном добавлении новой карты и нажатии на кнопку «Привязать» происходит переход обратно на форму выбора карт.  
Чтобы выбрать карту, её нужно отметить и нажать на кнопку выхода из формы. Если карта одна, она выбирается автоматически.  
После выхода из формы поле «Способ оплаты» заполнено данными выбранной карты.

#### Окно «Добавление карты»:
Внутри есть поле «Номер карты», поле «Код», кнопка «Привязать» и кнопка «Отмена». Кнопка «Привязать» активируется, когда пользователь ввёл реквизиты карты — номер и код.

![Скриншот 17-07-2025 172717](https://github.com/user-attachments/assets/f24fba24-ffc5-4621-8421-b48d40c107d3)

#### Ограничение окна "Добавление карты"

![Скриншот 17-07-2025 172851](https://github.com/user-attachments/assets/beaa7e20-8b61-4e10-8eb3-8f080065ab12)


Когда карта добавлена, в интерфейсе отображаются последние 4 цифры её номера. Так пользователь может узнавать и отличать свои карты.

#### Панель «Требования к заказу»
Это выпадающий список. Он свёрнут, если выбран тариф по умолчанию — «Повседневный». Если пользователь выбирает другой тариф, список автоматически раскрывается. И наоборот: если вернуться к тарифу «Повседневный», панель «Требования к заказу» свернётся.   
У каждого тарифа содержимое панели разное.   
Панель можно скроллить.

![Скриншот 17-07-2025 172927](https://github.com/user-attachments/assets/abf1d6b9-63bc-478a-8c82-9c441f831cd0)


#### Кнопка «Забронировать»
Кнопка закреплена в левом нижнем углу экрана.

![Скриншот 17-07-2025 173110](https://github.com/user-attachments/assets/0ce1e8b9-24ae-4034-9cca-533fb3cf0b3b)


#### Бронь машины
Если пользователь корректно заполнил все поля и нажал кнопку «Забронировать», в центре экрана появится окно с заголовком «Машина забронирована». Внутри — марка, номер, иконка и адрес машины, а также стоимость поездки и таймер, который отсчитывает время бесплатного ожидания.   
Если поля «Откуда» и «Куда» заполнены, отображается точная стоимость поездки. Если нет — стоимость за минуту.

#### Таймер
- Таймер начинает отсчитывать время бесплатного ожидания, когда пользователь нажимает кнопку «Забронировать».  
- Пока таймер работает, можно бесплатно отменить заказ.  
- Когда время бесплатного ожидания заканчивается, таймер начинает отсчитывать время пользования каршерингом.

  ***

  </details>


## Инструменты для тестирования

<p align="left"> 
  <a href="https://docs.google.com/" target="_blank" rel="noreferrer"><img src="https://w7.pngwing.com/pngs/240/1015/png-transparent-g-suite-google-docs-google-angle-rectangle-logo.png" width="36" height="36" alt="Google Sheets" /></a>
  <a href="https://www.figma.com/" target="_blank" rel="noreferrer"><img src="https://raw.githubusercontent.com/danielcranney/readme-generator/main/public/icons/skills/figma-colored.svg" width="36" height="36" alt="Figma" /></a>
  <a><img src="https://d33wubrfki0l68.cloudfront.net/38b5c953a4667366685d55db55d057c86db1fc54/a0fdc/static/acae6b24d940347661ca901ea07f47c1/chrome-dev-logo-icon.png" width="36" height="36" alt="Devtools" /></a>
  <a href="https://www.jetbrains.com/youtrack/" target="_blank" rel="noreferrer"><img src="https://upload.wikimedia.org/wikipedia/commons/9/95/YouTrack_Icon.png" width="36" height="36" alt="Youtrack" /></a>
  <a href="https://www.charlesproxy.com/" target="_blank" rel="noreferrer"><img src="https://davidwalsh.name/demo/charlesproxyicon.svg" width="36" height="36" alt="Charles" /></a>
</p> 

## Процесс тестирования 
### 1-й спринт
В ходе тест-анализа требований, была применена техника тест-дизайна: Классы эквивалентности и граничные значения для полей ввода (откуда, куда, часы и минут)

[Вся тестовая документация 1-го спринта доступна также по ссылке](https://docs.google.com/spreadsheets/d/1PNU6NS9hVmhvp_0OIpC-5Ylx5ndRhMvnTTpufuO_SyI/edit?usp=sharing)

#### Классы эквивалентности и граничные значения


<details>
<summary>КЭ и ГЗ для полей ввода - откуда, куда, часы, минуты </summary>


<img width="1127" height="1753" alt="2025-07-17_175503" src="https://github.com/user-attachments/assets/ef1ccb73-7565-4950-ad7c-6605037017b1" />

 </details>


#### Разработаны тест-кейсы


<details>
<summary>Тест-кейсы </summary>

<img width="1264" height="6739" alt="2025-07-17_201250" src="https://github.com/user-attachments/assets/ddf57504-521e-439b-b07c-f34b1657f1ab" />

 </details>


#### Заведены баг-репорты

<details>
<summary>Баг-репорты </summary>

<img width="1202" height="1354" alt="2025-07-17_202006" src="https://github.com/user-attachments/assets/ead6196e-9773-47d5-b587-ad49c524fdfc" />

 </details>

### 2-й спринт

[Вся тестовая документация 2-го спринта доступна также по ссылке](https://docs.google.com/spreadsheets/d/1ael1V46r1TpgPtpqRVUEZNGCRysRYFpejl2xaL0v5-Q/edit?usp=sharing)

#### Составлен чек-лист на верстку 

<details>
<summary>Чек-лист на верстку </summary>


<img width="1259" height="3486" alt="1" src="https://github.com/user-attachments/assets/95bbcdc3-db54-4ee0-85c2-5740c0afdf75" />

 </details>

#### Также составлен чек-лист и результаты выполнения тестов: тестирование окон «Способ оплаты» и «Добавление карты»	

<details>
<summary>Чек-лист на верстку окон "Способ оплаты" и "Добавление карты" </summary>

<img width="1172" height="1119" alt="2" src="https://github.com/user-attachments/assets/a03b6fd4-c690-4517-b38a-2f28fd4866af" />

 </details>

#### Разработаны тест-кейсы на логику кнопки "Забронировать"

<details>
<summary>Тест-кейсы на кнопку "Забронировать" </summary>

<img width="1212" height="928" alt="3" src="https://github.com/user-attachments/assets/4dc4ecd3-a5b7-428f-a406-08b074880c88" />

 </details>

#### Заведены следующие баг-репорты


<details>
 <summary> Баг-репорты </summary>

<img width="1268" height="4012" alt="4" src="https://github.com/user-attachments/assets/c16b37c1-f10a-4f86-b119-87183cc235f9" />

 </details>







