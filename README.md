# Коллоквиум 4 модуль

# Сеть

## 1. Что такое WebSocket и как он отличается от HTTP? В каких случаях целесообразно использовать WebSocket? Опишите процесс установления WebSocket соединения и его закрытия.

**WebSocket** - это  это коммуникационный протокол, предназначенный для реализации постоянного, двунаправленного соединения между клиентом и сервером. В отличие от традиционных HTTP-запросов, которые являются одноразовыми и требуют многократного установления соединения для каждой передачи данных, WebSocket обеспечивает постоянное соединение, что позволяет передавать данные в режиме реального времени.

### Отличия WebSocket от HTTP
Двунаправленность:

- HTTP: Клиент инициирует запрос, сервер отвечает. Это модель запрос-ответ, где каждый обмен данных требует нового HTTP-запроса.
WebSocket: После установления соединения как клиент, так и сервер могут обмениваться данными в любом направлении в любое время без необходимости повторного установления соединения.
Постоянное соединение:

- HTTP: Соединение устанавливается и закрывается для каждого запроса.
WebSocket: Соединение устанавливается один раз и сохраняется до явного закрытия, что позволяет передавать данные с минимальными задержками.
Производительность и масштабируемость:

- HTTP: Каждый запрос содержит заголовки, что увеличивает накладные расходы. Постоянное установление и закрытие соединений также потребляет ресурсы.
WebSocket: Позволяет избежать накладных расходов на установление новых соединений и передачи заголовков, что улучшает производительность, особенно при частом обмене небольшими данными.


### Целесообразность использования WebSocket
WebSocket целесообразно использовать в следующих случаях:

Чат-приложения: Обеспечивает мгновенный обмен сообщениями между пользователями.
Реальное время: Приложения, требующие обновлений в реальном времени, например, финансовые биржи или системы мониторинга.
Онлайн-игры: Обеспечивает низкую задержку и быструю передачу данных между игроками и сервером.
Потоковая передача данных: Потоковая передача мультимедийных данных или данных с датчиков, где важна минимальная задержка.
Коллаборативные приложения: Приложения, где несколько пользователей работают над одним документом в реальном времени.

### Процесс установления WebSocket соединения

1) Инициация соединения:

Клиент отправляет HTTP-запрос с методом GET и заголовком Upgrade, указывающим на желание перейти на протокол WebSocket.

2) Подтверждение от сервера:

Если сервер поддерживает WebSocket и согласен на установление соединения, он отвечает с кодом статуса 101 Switching Protocols, подтверждая обновление протокола.

3) Установление постоянного соединения:

После подтверждения от сервера, соединение считается установленным, и обе стороны могут начинать обмен данными.

### Процесс закрытия WebSocket соединения
1) Инициация закрытия:
Любая сторона (клиент или сервер) может инициировать закрытие соединения, отправив контрольное сообщение с кодом закрытия.

2) Ответное закрытие:
Получив сообщение о закрытии, другая сторона отправляет ответное контрольное сообщение о закрытии.

3) Завершение соединения:
После обмена контрольными сообщениями соединение закрывается, и оба конца освобождают ресурсы, связанные с этим соединением.  


## 2. Что такое STOMP и как он работает поверх WebSocket? Каковы преимущества использования STOMP? Какие основные команды STOMP вы знаете и для чего они используются?

**STOMP** (Simple Text Oriented Messaging Protocol) — это простой текстовый протокол для обмена сообщениями, который работает поверх различных протоколов транспортного уровня, включая WebSocket

WebSocket протокол не определяет форматы сообщений, поддерживает передачу в текстовом виде и bit. 
Поэтому поверх WebSocket используют другие суб-протоколы, например, STOMP. STOMP чем-то похож на HTTP и работает поверх TCP.

### Как работает STOMP поверх WebSocket?
Установление WebSocket соединения:

Клиент устанавливает соединение с сервером, используя WebSocket.
Взаимодействие через STOMP:

После установления WebSocket соединения начинается обмен сообщениями с использованием STOMP.
STOMP использует текстовые фреймы для передачи команд и сообщений. Каждый фрейм состоит из команды, набора заголовков и тела сообщения (если требуется).
Использование команд STOMP:

Команды STOMP отправляются и принимаются через WebSocket соединение, позволяя клиенту и серверу обмениваться информацией и сообщениями.

**Преимущества использования STOMP**
Простота и читаемость:
STOMP использует текстовые сообщения, что делает его простым для понимания и отладки.

Стандартизация:
STOMP предоставляет стандартные команды и заголовки для обмена сообщениями, что упрощает интеграцию с различными системами и брокерами сообщений.

Поддержка различных транспортных протоколов:
STOMP может работать поверх различных транспортных протоколов, включая WebSocket, TCP и HTTP, обеспечивая гибкость в выборе транспортного уровня.

### Основные команды STOMP
- CONNECT:
Использование: Устанавливает соединение с сервером STOMP.

- SEND:
Использование: Отправка сообщения на указанную конечную точку.

- SUBSCRIBE:
Использование: Подписка на указанный канал или очередь для получения сообщений.

- UNSUBSCRIBE:
Использование: Отмена подписки на указанный канал или очередь.

- ACK:
Использование: Подтверждение получения сообщения (при использовании подтверждений сообщений).

- DISCONNECT:
Использование: Закрытие соединения с сервером STOMP.

- MESSAGE:
Использование: Сообщение, отправляемое сервером клиенту по подписке.

## 3. Дайте определение GraphQL. Какие проблемы он решает по сравнению с RESTful API? Опишите основные типы запросов в GraphQL и приведите примеры каждого из них.
GraphQL — это язык запросов к API и среда выполнения. GraphQL позволяет клиентам запрашивать только те данные, которые им действительно нужны, а также предоставляет гибкие и эффективные инструменты для работы с данными.

### Проблемы, которые решает GraphQL по сравнению с RESTful API

- Запрос только необходимых данных:
REST: Обычно возвращает фиксированные структуры данных, что может привести к получению лишних данных.
GraphQL: Клиенты могут запрашивать только те поля, которые им нужны, что уменьшает объем передаваемых данных.

-Объединение нескольких запросов в один:
REST: Получение связанных данных часто требует нескольких запросов к разным конечным точкам.
GraphQL: Позволяет получить все необходимые данные в одном запросе, что снижает количество запросов и ускоряет получение данных.

- Гибкость и версияция:
REST: Добавление новых версий API часто требует создания новых конечных точек или значительных изменений в существующих.
GraphQL: Позволяет добавлять новые поля и типы без нарушения существующих запросов, что упрощает управление версиями.

### Основные типы запросов в GraphQL
- Query (запрос):
Используется для чтения данных.

```
{
  user(id: "1") {
    id
    name
    email
  }
}

```

- Mutation (мутация):
Используется для изменения данных (создание, обновление, удаление).
```
mutation {
  createUser(input: { name: "John Doe", email: "john@example.com" }) {
    id
    name
    email
  }
}
```

- Subscription (подписка):
Используется для подписки на изменения данных в реальном времени.
```
subscription {
  userAdded {
    id
    name
    email
  }
}

```

## 4. Какие недостатки и вызовы могут возникнуть при использовании GraphQL? В каких случаях вы бы рекомендовали использовать REST API вместо GraphQL и почему?

- Проблема N+1 запросов заключается в том, что при выполнении запроса в базу данных отправляется несколько запросов, что приводит к лишней нагрузке на сервер.
- Перегрузка сервера:
Запросы: Клиенты могут отправлять очень сложные или глубоко вложенные запросы, что может привести к значительным нагрузкам на сервер и увеличению времени выполнения запросов.
Защита от злоупотреблений: Требуется внедрение механизмов для предотвращения злоупотреблений, таких как лимиты глубины запросов и ограничение на количество запрашиваемых полей.
- Проблемы с кешированием:
Кеширование: В REST API кеширование можно легко настроить на уровне HTTP, тогда как в GraphQL необходимо внедрять более сложные механизмы кеширования, так как каждый запрос может быть уникальным.
- Серверная часть: Разработка и поддержка GraphQL сервера может быть сложнее, чем RESTful API. Необходимо обеспечить безопасность, контроль доступа и оптимизацию запросов.
Типизация: Нужна четкая схема типов, что требует дополнительных усилий по проектированию и поддержке.

Случаи, когда стоит использовать REST API вместо GraphQL
- Простые API:
Маленькие проекты: Для небольших проектов с простыми и статическими требованиями REST API проще и быстрее в реализации.

- Традиционное кеширование:
Кеширование: Когда требуется использовать стандартные механизмы HTTP кеширования, REST API будет предпочтительнее, так как он лучше поддерживает кеширование на уровне HTTP.

- Ограниченные ресурсы:
Ресурсы разработки: Если команда разработки не имеет опыта работы с GraphQL, может потребоваться больше времени и ресурсов на обучение и внедрение, что не всегда оправдано.

## 5. HTTP/1.1 и HTTP/2?

### Что такое HTTP?

**HTTP (HyperText Transfer Protocol)** — это протокол передачи данных в интернете. Изначально для передачи данных в виде гипертекстовых документов в формате HTML, сегодня — для передачи произвольных данных.

### Разница между HTTP/1.1 и HTTP/2

**HTTP/1.1** был стандартом для передачи данных в Интернете на протяжении многих лет, но он имеет ряд ограничений, которые могут снижать производительность и масштабируемость веб-приложений. **HTTP/2** был разработан для устранения этих ограничений и предлагает ряд улучшений:

- Множественные потоки: В **HTTP/1.1** каждый запрос обрабатывается последовательно, что может привести к задержкам, особенно в условиях высокой загрузки. **HTTP/2** позволяет обрабатывать несколько запросов одновременно в рамках одного соединения, что улучшает производительность.
- Сжатие заголовков: **HTTP/1.1** требует отправку заголовков для каждого запроса, что может быть неэффективным, особенно если заголовки остаются неизменными между запросами. **HTTP/2** использует сжатие заголовков для уменьшения объема передаваемых данных.
- Приоритизация запросов: В **HTTP/1.1** запросы обрабатываются в порядке их поступления, что может привести к задержкам для менее важных запросов. **HTTP/2** позволяет клиенту указывать приоритеты запросов, чтобы сервер мог обрабатывать более важные запросы первыми.
- Серверный пуш: **HTTP/2** вводит концепцию серверного пуша, позволяя серверу активно отправлять данные клиенту без предварительного запроса. Это может улучшить время загрузки веб-страниц, отправляя данные заранее.
- Бинарный протокол: В отличие от **HTTP/1.1**, который использует текстовый протокол, **HTTP/2** является бинарным протоколом. Это упрощает обработку и уменьшает объем передаваемых данных.

**HTTP/2** был разработан для улучшения производительности и масштабируемости веб-приложений, устраняя некоторые из ограничений **HTTP/1.1**. Однако, несмотря на эти улучшения, **HTTP/2** требует поддержки со стороны клиента и сервера, и не все клиенты и серверы могут поддерживать **HTTP/2**.


## 6. Протоколы транспортного уровня: TCP, UDP

**TCP (Transmission Control Protocol)** 

- Протокол надежной и упорядоченной доставки данных
- Обеспечивает контроль передачи данных, управление потоком, обнаружение ошибок и повторную передачу данных при необходимости

**UDP (User Datagram Protocol)**

- Простой протокол без гарантии доставки данных, контроля потока или механизмов повторной передачи данных
- Представляет собой менее надежную альтернативу TCP

### Разница между TCP и UDP

- **Надежность:** TCP обеспечивает надежную передачу данных, используя механизмы подтверждения получения, повторной передачи потерянных пакетов и контроля потока. UDP не предоставляет таких гарантий, что делает его более подходящим для приложений, где скорость важнее надежности, например, в потоковом видео или игровых приложениях
- **Соединение:** TCP использует соединение для обмена данными между отправителем и получателем, что обеспечивает упорядоченную и безошибочную передачу. UDP не использует соединение, что позволяет ему быстрее передавать данные, но также означает, что он не может гарантировать упорядоченность или доставку данных
- **Заголовки:** TCP заголовки содержат больше информации, чем UDP заголовки, включая номера последовательности, контрольные суммы и флаги управления соединением. UDP заголовки значительно меньше и содержат только порты отправителя и получателя
- **Применение:** TCP часто используется в приложениях, где важна надежность и целостность данных, таких как веб-сервисы, электронная почта и файловые передачи. UDP часто используется в приложениях, где скорость важнее, и потеря некоторых пакетов приемлема, например, в потоковом видео, онлайн-играх и VoIP



# Тестирование

## 1. Что такое unit-тестирование и какова его цель? 

**Unit-тестирование (модульное тестирование)** — это процесс тестирования отдельных модулей или компонентов программы для проверки их корректной работы.

### Цель:
- Найти дефекты в компонентах (классы/модули/функции)
- Сформировать уверенность (на каком-то уровне), что компонент
работает
- Заложить базу для следующих уровней тестирования

Объекты тестирования: 
- Классы
- Компоненты, модули

Типичные ошибки/дефекты:
- Проблемы с потоком данных и потоком управления
- Неверная логика
- Не вписываемся в требования

## 2. Как создать и запустить простой unit-тест с использованием JUnit? Что такое аннотация @Test? Какие аннотации JUnit можно использовать при написании тестов? Приведите примеры.

## 3. Какие проблемы решает Mockito при написании тестов? Как использовать Mockito для создания mock-объектов? Приведите примеры.

## 4. В чем разница между @Mock и @InjectMocks аннотациями в Mockito? Какие основные методы Mockito используются для задания поведения mock-объектов?

## 5. Что такое интеграционное тестирование? Объясните разницу между unit-тестами и интеграционными тестами.

## 6. Инструменты для написания тестов: JUnit и Mockito


# Безопасность

## 1. Дайте определение понятиям идентификации, аутентификации и авторизации. В чем различие между ними?

## 2. Что такое password-based authentication и какие у нее есть преимущества и недостатки? Объясните, как работает протокол HTTP Basic Authentication.

## 3. Что такое аутентификация по токенам? Приведите пример flow такого способа аутентификации.

## 4. Объясните, что такое Single Sign-On (SSO) и в чем его преимущества.

## 5. Что такое JSON Web Token? Из каких основных частей формируется данный токен?

## 6. Объясните разницу между access-токенами и refresh-токенами (и id-токеном?). Как происходит обновление access-токена с использованием refresh-токена?

## 7. Объясните, как работают фильтры безопасности (security filters) в Spring Security и приведите примеры их использования. Как настроить аутентификацию с использованием JWT в Spring Security?
