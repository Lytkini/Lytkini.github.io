---
title: Плитка приложения на главном экране смарт-терминала
keywords: sample
summary: "Раздел содержит требования к плитке приложения, а также информацию о том как добвить плитку на главный экран смарт-терминала."
sidebar: evotordoc_sidebar
permalink: doc_smart_terminal_native.html
folder: smart_terminal_SDK
---

Вы можете интегрировать своё приложение в существующий процесс смарт-терминала, например, продажу, работу с товарами или оборудованием, или добавить плитку приложения на главный экран. Вы также можете добавить несколько разных плиток, если приложение реализует несколько независимых действий, например, плитки "Продать товар" и "Вернуть товар".

### Требования к плитке

Добавляйте плитку приложения если:
 * у приложения есть свой интерфейс;
 * приложение реализует полезное действие и / или предоставляет сотруднику магазина доступ к аналитической информации.

Вы можете изменять следующие параметры плитки:
* Цвет. Может быть любым, пока на его фоне нормально читаются название приложения и иконка.

  > Как правило цвет плитки делают таким же как и цвет главных кнопок в интерфейсе приложения.

* Название плитки. Может быть названием приложения или полезного действия, например "Продажи за неделю", "Запросить помощь". На плитке отображается до 20 символов. Остальные символы скрываются под многоточием.
* Иконка приложения. Иконка должна быть квадратной – 64 dpi. Требуется предоставить набор иконок в трёх разрешениях: 96, 192, 256px.

### Нативное приложение

Чтобы добавить плитку нативного приложения на главный экран смарт-терминала, в манифесте приложения, модифицируйте соответствующий элемент `<Activity>` следующим образом:
```1xml
<activity
    android:name="<Название Activity>"
    android:icon="<Путь к иконке>"
    android:label="<Название плитки>"
    >
    <meta-data
        android:name="ru.evotor.launcher.BACKGROUND_COLOR"
        android:value="#133788" />
    <intent-filter>
        <action android:name="android.intent.action.MAIN" />
        <category android:name="android.intent.category.EVOTOR" />
    </intent-filter>
</activity>
```
, где
* Атрибут `android:icon` указывает расположение иконки приложения. Требования к иконке см. выше.
* Атрибут `android:label` указывает название приложения, которое отображается на плитке. Требования к названию приложения см. выше.
* Необязательный тег `<meta-data>`, содержит атрибуты, которые задают основной цвет плитки (`android:name="ru.evotor.launcher.BACKGROUND_COLOR"`) в шестнадцатиричной кодировке (`android:value="#133788"`).
* Интент фильтр содержит соответствующие элементы action (`android:name="android.intent.action.MAIN"`) и category (`android:name="android.intent.category.EVOTOR"`).


### Вебвью приложение

Чтобы добавить плитку вебвью приложения на главный экран смарт-терминала, в файле *client.yaml*, модифицируйте список `views` следующим образом:
```yaml1
views:
  - name: <Название>
    header: "Заголовок окна"
    launcher_label: "Название приложения для плитки"
    launcher_icon_96: client/views/example/icon-96.png
    launcher_icon_192: client/views/example/icon-192.png
    launcher_icon_256: client/views/example/icon-256.png
    launcher_color: #133788
    source: client/views/example/view.html
    scripts:
      - no-script
    styles:
      - "*.css"
```
,где:
* `name` – указывает название элемента списка `views`.
* `header` – указывает заголовок окна, которое открывается по нажатию на плитку.
* `launcher_label` – указывает название приложения, которое отображается на плитке.
* `launcher_icon_96` – указывает путь к иконке в разрешении 96 х 96 пикселей. Иконка копируется в папку drawable-hdpi, файл переименовывается в `<Название>-icon.png`.
* `launcher_icon_192` – указывает путь к иконке в разрешении 192 х 192 пикселя. Иконка копируется в папку xxdrawable-hdpi, файл переименовывается в `<Название>-icon.png`.
* `launcher_icon_256` – указывает путь к иконке в разрешении 256 х 256 пикселей. Иконка копируется в папку xxxdrawable-hdpi, файл переименовывается в `<Название>-icon.png`.
* `launcher_color` – указывает цвет плитки в шестнадцатиричной кодировке.
* `source` – указывает полный путь к html-файлу, который открывается по нажатию на плитку.
* `scripts` – содержит список подключаемых скриптов.
* `styles` – содержит список подключаемых стилей.