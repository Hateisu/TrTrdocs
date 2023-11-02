# Django BackEnd TR

### TODO:

1) Аватарки CompanyProfile
2) Модель UserProfile
3) Возможность в бд для изменения: CompanyProfile, UserProfile

<p>Так это подробная докумнетация по использованию этого API</p>
<a href="#models">Модели</a>

* <a href="#almaty_table">almaty_table</a>
* <a href="#user">user</a>
* <a href="#companyprofile">CompanyProfile</a>
* <a href="#userprofile">userProfile</a>

<a href="#requests">Запросы</a>

* <a href="#request_almaty">Запрос по "almaty"</a>
* <a href="#request_almaty_org">Запрос по "almaty" для Организаций</a>

## Модели

<div>
<p id="models">Список всех моделей в базе данных:</p>
<ul>
<li>almaty_table - модель содержащая все туристические услуги.</li>
<li>userCompany - модель содержащая модель компании.</li>
<li>В будущем будет еще customUser и модели других городов</li>

</ul>
<pre>[П/П]: Возможно будет легче объединить все таблицы городов в единую модель, добавив поле город к записи тура</pre>

## almaty_table

<ul id="almaty_table">
<li>id - Integer. Авто заполняемый</li>
<li>name - String. Имя. Максимальная длина - 150 символов. Уникальное поле</li>
<li>image - String. URL картинки. Возвращает абсолютную ссылку на картинку на бэкенде. Может вернуть null, так как картинки может не быть.</li>
<li>description - String. Описание. Максимальная длина - 1000 символов. Может быть null.</li>
<li>price - Integer. Цена. Может быть null. </li>
<li>typeofwonder - String. Тип услуги. Может принимать значения: "Отдых и развлечения"(funny), "Исторический тип"(history), "Природный тип"(nature), "Культурный тип"(culture) </li>
<li>age_type - String. Может принимать значения: "any" если подходит всем возрастам, "x-y", где подходит всем числам в диапазоне от x до y.</li>
<li>time - Integer. Время от центра города до точки. </li>
<li>creator - Integer. Организация которая создала запись. Имеет id из <a href="#companyprofile">CompanyProfile</a></li>
</ul>

<pre>
tour_table
<ul id="tour_table">
<li>id - Integer. Авто заполняемый</li>
<li>name - String. Имя. Максимальная длина - 150 символов. Уникальное поле</li>
<li>image - String. URL картинки. Возвращает абсолютную ссылку на картинку на бэкенде. Может вернуть null, так как картинки может не быть.</li>
<li>description - String. Описание. Максимальная длина - 1000 символов. Может быть null.</li>
<li>price - Integer. Цена. Может быть null. </li>
<li>typeofwonder - String. Тип услуги. Может принимать значения: "Отдых и развлечения"(funny), "Исторический тип"(history), "Природный тип"(nature), "Культурный тип"(culture) </li>
<li>age_type - String. Может принимать значения: "any" если подходит всем возрастам, "x-y", где подходит всем числам в диапазоне от x до y.</li>
<li>time - Integer. Время от центра города до точки. </li>
<li>city - String. Город в котором есть этот тип услуги</li>
<li>rating - Float. Оценка пользователей </li>
<li>user - String. Организация которая создала запись. </li>
</ul>
</pre>

## user

Автоматически созданная модель django для пользователей.
<ul id="user">
<li>id - Integer. Авто заполняемый</li>
<li>username - String. Максимальная длина - 150 символов.</li>
<li>password - String</li>
<li>email - String </li>
<li>first_name - String. Наименование. Максимальная длина - 150 символов. Может быть null.</li>
<li>last_name - String. Наименование. Максимальная длина - 150 символов. Может быть null. </li>
<li>phoneNumber - String. Номер телефона ресепшена. </li>
<li>is_active - Boolean. Вместо удаления аккаунта можно просто отключить. </li>
</ul>
<pre>[П/П]: Использование двух типов пользователя, т. е. Пользователь организации и пользователь человек. </pre>

## CompanyProfile

<ul id="companyprofile">
<li>user - id. Имеет значения из пользователей, то есть это связанное поле</li>
<li>avatar - String. Возвращает абсолютный путь до файла. </li>
<li>phoneNumber - String. Номер телефона ресепшена. </li>
<li>description - String. Описание организации. Максимальная длина - 1000 символов. Может быть null.</li>
<li>canAdd - Integer. Сколько записей может добавить организация. (При этом каждую из них организация может редактировать) </li>
</ul>
<pre>
[П/П]: Вызов профиля компании происходит при условии если он существует и выглядит так:<br>
        CompanyProfile.objects.get(user = request.user.id)
</pre>

## UserProfile

<ul id="userprofile">
<li>user - id. Имеет значения из пользователей, то есть это связанное поле</li>
<li>avatar - String. Возвращает абсолютный путь до файла. </li>
<li>phoneNumber - String. Номер телефона ресепшена. </li>
<li>recent_list_id - Array Integer. Список просмотренного пользователем. Может быть null.</li>
<li>favourite_list_id - Array Integer. Список отмеченного пользователем. Может быть null. </li>
</ul>
<pre>
[П/П]: Вызов профиля клиента-пользователя происходит при условии если он существует и выглядит так:<br>
        UserProfile.objects.get(user = request.user.id)
</pre>
</div>

https://reintech.io/blog/building-multi-user-application-django   - связанные таблицы
alias
asd21Q!dsa
d588b4b3630d094f74f1b32f3a262918fdf5361c

## Возможные запросы

<p id="requests">
У всех запросов есть схожесть: общий домен - <a>https://timkaqwerty.pythonanywhere.com/api/</a>
</p>

#### Запрос по "almaty" для пользователя <p id = "request_almaty"></p>

Абсолютный url - https://timkaqwerty.pythonanywhere.com/almaty/
<br>Эта ссылка подходит для всех пользователей. Возвращает объекты из бд.

* Метод GET принимает (все параметры опциональные, то есть могут не использоваться):
<br>wonder - тип достопримечательности варианты [ funny , history , nature , culture ]
<br>time - время от центра города до достопримечательности в минутах
<br>age - Возраст кому подходит эта услуга
<br>price - Цена в тенге за услугу.<br>
<br>Он возвращает JSON массив results и имеет внутри себя другие JSON объекты услуги, которые имеют модель <a href="#almatytable">almaty_table</a>, за исключением не возвращаются id и creator



#### Запрос по "almaty" для Организаций <p id = "request_almaty_org"></p>

Абсолютный url - https://timkaqwerty.pythonanywhere.com/api/almaty/v3
<br>Эта ссылка подходит для всех пользователей, которые имеют CompanyProfile и токен авторизации, который проходит в
заголовке запроса. Токен указывается через: Authorization и имеет значение токена: Token
c72645b205267aca6b15056bdbb1eaed92b91813

* Метод GET принимает множества значений <a href="#almatytable">almaty_table</a>, кроме id и creator. Они все не обязательные, то есть фильтр значений будет по этим компонентам если они есть. Возвращает все посты, которые написал текущий пользователь.
<br> Он возвращает JSON массив results и имеет внутри себя другие JSON объекты услуги, которые имеют модель <a href="#almatytable">almaty_table</a>, за исключением не возвращаются id и creator.
<br><br>

* Метод POST принимает множество значений для <b>ДОБАВЛЕНИЯ НОВОЙ</b> записи в базу данных. Все элементы должны быть из <a href="#almatytable">almaty_table</a>, кроме id и creator. <br><br>
* Метод PUT принимает множество значений для <b>ОБНОВЛЕНИЯ ИЛИ ИЗМЕНЕНИЯ <strong>ОДИНОЧНОГО</strong></b> объекта из базы  данных. Принимает обязательный id для объекта <a href="#almatytab le">almaty_table</a>, который принадлежит именно этому <a href="#companyprofile">пользователю с CompanyProfile</a> , и необязательный данные объекта <a href="#almatytable">almaty_table</a>.<br><br>
* Метод DELETE принимает множество значений для <b>УДАЛЕНИЯ ОДИНОЧНОГО</b> объекта из базы данных. Принимает обязательный id для объекта <a href="#almatytable">almaty_table</a>, который принадлежит именно этому <a href="#companyprofile">пользователю с CompanyProfile</a>. <br><br>

#### Запрос по url

http://127.0.0.1:8000/api/auth/token/login/
в боди запроса передаем логин пароль и возвращает токен

Тут будут запросы для обращения к userCompany

* Метод get
* Метод post
* Метод put
