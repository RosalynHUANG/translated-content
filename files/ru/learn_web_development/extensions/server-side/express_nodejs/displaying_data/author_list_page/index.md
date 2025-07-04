---
title: Список авторов. Тест - список жанров
slug: Learn_web_development/Extensions/Server-side/Express_Nodejs/Displaying_data/Author_list_page
---

Страница списка авторов должна показывать список всех авторов, хранимых в БД, причём каждое имя автора должно быть связано со страницей подробностей для этого автора. Дата рождения автора и дата смерти должны выводиться в одной строке после имени автора.

## Контроллер

Функция контроллера списка авторов должна получить список всех элементов в `Author` , и передать этот список в шаблон для отображения.

Откройте файл **/controllers/authorController.js**. Найдите экспортируемый метод `author_list()` в начале файла и замените его следующим ниже кодом:

```js
// Display list of all Authors.
exports.author_list = function (req, res, next) {
  Author.find()
    .sort([["family_name", "ascending"]])
    .exec(function (err, list_authors) {
      if (err) {
        return next(err);
      }
      //Successful, so render
      res.render("author_list", {
        title: "Author List",
        author_list: list_authors,
      });
    });
};
```

Метод использует такие функции модели как `find()`, `sort()` и `exec()` для того, чтобы вернуть все объекты `Author` отсортированными по `family_name` в алфавитном порядке. В вызове `exec()` колбэк-функция имеет первый параметр- объект ошибок (или `null`) и второй параметр - список всех авторов, если ошибок не было. При ошибках вызывается следующая функция промежуточного слоя с полученным значением объекта ошибок, а если ошибок не было, отображается шаблон **author_list**(.pug), передавая странице `title` и список авторов (`author_list`).

## Представление

Создайте файл **/views/author_list.pug** и поместите в него следующий текст:

```js
extends layout

block content
  h1= title

  ul
    each author in author_list
      li
        a(href=author.url) #{author.name}
        |  (#{author.date_of_birth} - #{author.date_of_death})

    else
      li There are no authors.
```

Представление создано по тому же образцу, что и другие шаблоны.

## Как это выглядит?

Запустите приложение и откройте браузер с адресом <http://localhost:3000/>. Выберите ссылку _All authors_. Если все было сделано правильно, страница должна выглядеть примерно так, как на следующем скриншоте.

![Author List Page - Express Local Library site](locallibary_express_author_list.png)

> [!NOTE]
> Представление дат продолжительности жизни автора выглядит безобразно! Это можно исправить, если использовать [тот же подход](/ru/docs/Learn_web_development/Extensions/Server-side/Express_Nodejs/Displaying_data#date_formatting) , который применялся для списка `BookInstance` (добавить в модель `Author` виртуальное свойство продолжительности жизни). Но в этот раз, однако, некоторые даты могут отсутствовать, и ссылки на несуществующие свойства игнорируются, если не задан строгий режим. Метод `moment()` возвращает текущее время, и нежелательно, чтобы отсутствующие даты форматировались как "сегодня". Один из способов состоит в том, чтобы форматирующая функция возвращала пустую строку, если дата не существует. Например:
>
> `return this.date_of_birth ? moment(this.date_of_birth).format('YYYY-MM-DD') : '';`

## Тест - страница списка жанров!

В этой части требуется создать собственную страницу списка жанров. Страница должна показывать жанры, имеющиеся в БД, а для каждого жанра должна быть создана ссылка на страницу с детальной информацией. Скриншот ожидаемого результата приводится ниже.

![Genre List - Express Local Library site](locallibary_express_genre_list.png)

Функция контроллера списка жанров должна получить список всех экземпляров `Genre`, и передать его в шаблон для отображения.

1. Следует отредактировать `genre_list()` в файле **/controllers/genreController.js**.
2. Реализация почти такая же, как и для контроллера `author_list()` .
   - Sort the results by name, in ascending order.

3. Отображающий шаблон должен быть назван **genre_list.pug**.
4. Шаблону для отображения должны быть переданы переменные `title` (строка 'Genre List') и `genre_list` (the list of список жанров, который вернёт колбэк-функция `Genre.find()`.
5. Представление должно соответствовать скриншоту, приведённому ранее (оно должно иметь структуру и формат, похожие на таковые в представлении списка авторов, за исключением, конечно, продолжительности жизни, так как для жанров даты не заданы).

## Далее

Вернуться к части 5 - [Express Tutorial Part 5: Displaying library data](/ru/docs/Learn_web_development/Extensions/Server-side/Express_Nodejs/Displaying_data).

Перейти к следующему подразделу в части 5: подробная информация о жанрах ([Genre detail page](/ru/docs/Learn_web_development/Extensions/Server-side/Express_Nodejs/Displaying_data/Genre_detail_page)).
