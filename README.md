### Описание задачи

Задача: создать прототип микросервиса, обеспечивающий эмуляцию отправки сообщений в популярные месседжеры (Viber, Telegram, WhatsApp).

Приложение должно обладать следующим функционалом:

* Прием сообщений по API и отправка их в мессенджеры (с указанием идентификатора пользователя для каждого мессенджера);

* Возможность отложенной отправки сообщений по дате/времени;

* В случае неудачной отправки сообщения, нужно повторить попытку N-ое количество раз, но это не должно влиять на доставляемость других сообщений;

* Исключение возможности многократной отправки одного и того же сообщения (с одним и тем же содержимым) одному получателю;

* Возможность отправки одного сообщения нескольким получателям на несколько мессенджеров в рамках одного запроса;

* Параметры запроса должны проходить валидацию (требования валидации на усмотрение разработчика).

* Важно: нужно сделать именно эмуляцию отправки, непосредственную интеграцию с мессенджерами делать не нужно.

### Установка приложения

```
git clone git@github.com:AgeevAndrew/send_message_emulator.git
bundle install
rake db:create
rake db:migrate
rake docs:generate RAILS_ENV=test
```

### Запуск приложения

```
foreman start
```

### Описание API

```
http://localhost:3000/api/docs
```

### Проверка работы приложения

```
curl -XPOST \
     -H "Content-Type: application/json" \
     -H "Accept: application/json" \
     -d '{"body": "Тестовое сообщение", "messengers":[{"name": "Telegram", "user_id": "1234567890"}]}' \
     http://localhost:3000/messages
```

### Используемые библиотеки

* `sqlite3` база данных

* `trailblazer` для логики

* `reform` для валидации входящих параметров

* `sidekiq` для бекграунд задач

* `foreman` для удобства запуска приложения

* `rspec` для тестирования

* `rspec_api_documentation` для acceptance тестов и документирования API

* `factory_bot_rails` для фабрик

* `faker` для генерации фейковых данных

* `apitome` для просмотра документации API

* `guard` для непрерывной прогонки тестов
