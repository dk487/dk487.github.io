---
title: Багатомовність
date: 2017-11-01 15:34:36 +0200
lang: uk
---

Робити багатомовні сайти складно.

Що я тільки не робив. Я писав власні CMS з підтримкою багатомовності.
Я використовував поширені системи, такі як Drupal, щоб створювати
багатомовні сайти. У своїх PHP-скриптах я використовував Gettext,
або вбудований у Symfony компонент перекладача, або робив у БД таблиці
з жалюгідними колонками `title_en`, `title_uk` та `title_ru` (адже перелік
підтримуваних мов завжди відомий, _чі не так?_). Я знаю, як декодувати
рядок HTTP-запита `Accept-Language`, а ще я знаю, що на `Accept-Language`
не можна покладатися. Інколи я навіть мав справу з `mod_negotiation`.

Нажаль, Jekyll не дуже зручний для створення багатомовних сайтів.
Але я спробую. У мене є відносно проста ідея:

- має бути сторінка-оригінал та декілька сторінок-перекладів;
- переклади посилаються на один і той же оригінал;
- додавання перекладу не потребує змін у оригіналі;
- все інше (посилання на інші версії) має робитися автоматично.

Ось як виглядає front matter у файлі `_posts/2017-10-23-hello-world.ru.md`:

```yaml
title: Привет, мир!
date: 2017-10-23 14:43:00 +0300
lang: ru
```

А так виглядає front matter у файлі `_posts/2017-10-23-hello-world.en.md`,
що містить переклад англійською:

```yaml
title: Hello, world!
date: 2017-10-23 14:43:00 +0300
lang: en
translation_of: _posts/2017-10-23-hello-world.ru.md
```

Це не ідеальна схема, але з нею можна побудувати багатомовний сайт.

Далі буде.