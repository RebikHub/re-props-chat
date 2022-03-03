[![Build status](https://ci.appveyor.com/api/projects/status/bc82orj4mvfxkj7p/branch/master?svg=true)](https://ci.appveyor.com/project/RebikHub/re-props-chat/branch/master)

[История чата](https://rebikhub.github.io/ra-props-chat/)

===

Необходимо реализовать один из компонентов чата — историю сообщений:
![Чат](./assets/preview.png)

## Данные

Список сообщений, передаваемый в компонент, представляет собой _массив объектов_, каждый из которых представляет собой сообщение, которое необходимо отразить в истории. Сообщение имеет следующие свойства:
- `id` — уникальный идентификатор сообщения, _строка_;
- `from` — автор сообщения, _объект_;
- `type` — тип сообщения, _строка_, варианты значений: `response`, `message`, `typing`;
- `time` — время публикации сообщения, _строка_;
- `text` — текст сообщения, _строка_, может отсутствовать.

## Описание компонента

Для отображения списка создайте компонент `MessageHistory`, который принимает следующие атрибуты:
- `list` — список сообщений, _массив объектов_, по умолчанию пустой массив.

Если список сообщений пуст, то компонент не должен иметь какого-либо представления в DOM.

Компонент должен создавать на основе списка предложений следующий HTML-код:
```html
<ul>
  <li class="clearfix">
    <div class="message-data align-right">
      <span class="message-data-time">10:10</span> &nbsp; &nbsp;
      <span class="message-data-name">Ольга</span>
      <i class="fa fa-circle me"></i>
    </div>
    <div class="message other-message float-right">
      Привет, Виктор. Как дела? Как идет работа над проектом?
    </div>
  </li>
  <li>
    <div class="message-data">
      <span class="message-data-name"><i class="fa fa-circle online"></i> Виктор</span>
      <span class="message-data-time">10:12</span>
    </div>
    <div class="message my-message">
      Привет. Давай сегодня созвонимся. Проект практически готов, и у меня есть что показать.
    </div>
  </li>
  <!-- … и так далее -->
</ul>
```

Где каждый тег `<li>` — сообщение из массива. Для отображения сообщений в чате необходимо использовать следующие компоненты:
- `Message` — если тип сообщения равен `message`,
- `Response` — если тип сообщения равен `response`,
- `Typing` — если тип сообщения равен `typing`.

Все три компонента принимают следующие аргументы:
- `from` — автор сообщения, _объект_,
- `message` — сообщение, _объект_.

## Пример использования

```jsx
const messages = [{
  id: 'chat-5-1090',
  from: { name: 'Ольга' },
  type: 'response',
  time: '10:10',
  text: 'Привет, Виктор. Как дела? Как идет работа над проектом?'
}];

// в компоненте App:
return (
  <div className="clearfix container">
    <div className="chat">
      <div className="chat-history">
        <MessageHistory list={messages} />
      </div>
    </div>  
  </div>
);
```

Данные для сообщений:
```js
const messages = [{
  id: 'chat-5-1090',
  from: { name: 'Ольга' },
  type: 'response',
  time: '10:10',
  text: 'Привет, Виктор. Как дела? Как идет работа над проектом?'
}, {
  id: 'chat-5-1091',
  from: { name: 'Виктор' },
  type: 'message',
  time: '10:12',
  text: 'Привет. Давай сегодня созвонимся. Проект практически готов, и у меня есть что показать.'
}, {
  id: 'chat-5-1092',
  from: { name: 'Ольга' },
  type: 'response',
  time: '10:14',
  text: 'Не уверена что сегодня получится. Не все еще в офисе. Давай уточню через час. Возникли ли какие-либо проблемы на последней стадии проекта?'
}, {
  id: 'chat-5-1093',
  from: { name: 'Виктор' },
  type: 'message',
  time: '10:20',
  text: 'Нет, все прошло гладко. Очень хочу показать всё команде.'
}, {
  id: 'chat-5-1094',
  from: { name: 'Виктор' },
  type: 'typing',
  time: '10:31'
}];
```

## Реализация

Необходимо реализовать компонет `MessageHistory`. Важно: вам нужно реализовать только список истории (аватарки и боковую панель реализовывать не нужно).

Используйте файл из каталога css для стилизации.