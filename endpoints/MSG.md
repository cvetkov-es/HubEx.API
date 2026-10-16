# MSG — справочник ручек

> **Что здесь:** все ручки сервиса MSG (API for MSG in HubEx): сигнатуры, параметры, права. Типы — schemas/MSG.md.
> **Когда сюда идти:** найти ручку и её вход/выход. Типы — `schemas/MSG.md`; грабли — `notes/MSG.md` (если есть).

Base: `{BASE_URL}/MSG`
> Примеры ответов вынесены в [../examples/MSG.md](../examples/MSG.md).

**Оглавление**

- ContentTypes — строки 24–27
- CriticalityForTriggers — строки 29–31
- MailBoxes — строки 33–67
- MessageTemplates — строки 69–86
- NavigateTo — строки 88–91
- Notifications — строки 93–106
- Protocols — строки 108–111
- Providers — строки 113–116
- RecipientSelectionRules — строки 118–134
- TriggerRecipientSelectionRules — строки 136–138
- Triggers — строки 140–164
- Webhooks — строки 166–185

## ContentTypes
- `GET /ContentTypes` — Возвращает список типов контента. · paginated · коды: 200, 204, 206 · примеры
  → map<RCTListResult>
  Поддерживает ограничение результата через заголовок `Range`.

## CriticalityForTriggers
- `POST /CriticalityForTriggers` — Добавляет или изменяет критичности для триггера. · коды: 202, 400 · примеры
  ← body: MSGCFTMergeData[]

## MailBoxes
- `GET /MailBoxes` — Возвращает список почтовых ящиков. · paginated · коды: 200, 204, 206 · примеры
  → map<RMBListResult>
  Поддерживает ограничение результата через заголовок `Range`.
- `POST /MailBoxes` — Создаёт или обновляет почтовые ящики. · коды: 201, 400 · примеры
  ← body: MSGMBMergeData[] → int[]
- `DELETE /MailBoxes` — Помечает почтовые ящики как удалённые. · коды: 202 · примеры
  ← body: int[]
- `PUT /MailBoxes/activate` — Активирует почтовые ящики. · коды: 202 · примеры
  ← body: int[]
- `PUT /MailBoxes/activate/{id}` — Активирует почтовый ящик. · коды: 202 · примеры
  ← path: id:int
- `PUT /MailBoxes/deactivate` — Деактивирует почтовые ящики. · коды: 202 · примеры
  ← body: int[]
- `PUT /MailBoxes/deactivate/{id}` — Деактивирует почтовый ящик. · коды: 202 · примеры
  ← path: id:int
- `GET /MailBoxes/regexactions` — Возвращает список действий при неудачном применении регулярного выражения. · paginated · коды: 200, 204, 206 · примеры
  → map<RRNMAListResult>
  Справочник действий, которые выполняются, если регулярное выражение для темы или тела письма не совпало. Поддерживает ограничение результата через заголовок `Range`.
- `GET /MailBoxes/{id}` — Возвращает почтовый ящик по идентификатору. · коды: 200, 204 · примеры
  ← path: id:int → RMBGetResult
- `DELETE /MailBoxes/{id}` — Помечает почтовый ящик как удалённый. · коды: 202 · примеры
  ← path: id:int
- `GET /MailBoxes/{id}/errors` — Возвращает ошибки чтения почтового ящика. · paginated · коды: 200, 204, 206 · примеры
  ← path: id:int; query: occurredFrom?:datetime, occurredTill?:datetime → MailBoxErrorsEntity[]
  Поддерживает фильтрацию по дате возникновения ошибки и ограничение результата через заголовок `Range`.
- `GET /MailBoxes/{mailBoxID}/senders` — Возвращает список отправителей почтового ящика. · paginated · коды: 200, 204, 206 · примеры
  ← path: mailBoxID:int → map<RMBSListResult>
  Поддерживает ограничение результата через заголовок `Range`.
- `DELETE /MailBoxes/{mailBoxID}/senders` — Помечает отправителей почтового ящика как удалённых. · коды: 202 · примеры
  ← path: mailBoxID:int; body: int[]
- `DELETE /MailBoxes/{mailBoxID}/senders/{id}` — Помечает отправителя почтового ящика как удалённого. · коды: 202 · примеры
  ← path: mailBoxID:int, id:int
- `GET /MailBoxes/{mailBoxID}/senders/{senderID}` — Возвращает отправителя почтового ящика по идентификатору. · коды: 200, 204 · примеры
  ← path: mailBoxID:int, senderID:int → RMBSGetResult

## MessageTemplates
- `GET /MessageTemplates` — Возвращает список шаблонов уведомлений. · paginated · коды: 200, 204, 206 · примеры
  ← query: isDeleted?:bool → map<RMTListResult>
  Поддерживает фильтрацию по query-параметрам и ограничение результата через заголовок `Range`.
- `POST /MessageTemplates` — Создает шаблоны уведомлений. · коды: 201, 400 · примеры
  ← body: MSGMTAddData[] → int[]
- `PUT /MessageTemplates` — Изменяет шаблоны уведомлений. · коды: 202, 400 · примеры
  ← body: MSGMTUpdateData[]
- `DELETE /MessageTemplates` — Помечает шаблоны уведомлений как удаленные. · коды: 202, 409 · примеры
  ← body: int[]
- `GET /MessageTemplates/{id}` — Возвращает шаблон уведомлений по идентификатору. · коды: 200, 204 · примеры
  ← path: id:int → RMTGetResult
  Используется для просмотра и редактирования карточки шаблона уведомления.
- `DELETE /MessageTemplates/{id}` — Помечает шаблон уведомлений как удаленный. · коды: 202, 409 · примеры
  ← path: id:int
- `PUT /MessageTemplates/{id}/validate` — Валидирует шаблон уведомлений и сохраняет результат проверки. · коды: 200, 204, 400 · примеры
  ← path: id:int
  Проверяет корректность шаблонов темы и содержимого через MessageBuilder.

## NavigateTo
- `GET /NavigateTo` — Возвращает список переходов. · paginated · коды: 200, 204, 206 · примеры
  → map<RNTListResult>
  Поддерживает ограничение результата через заголовок `Range`.

## Notifications
- `GET /Notifications` — Возвращает список уведомлений пользователя. · paginated · коды: 200, 204, 206 · примеры
  ← query: includeIsViewed?:bool → map<RNListResult>
  Поддерживает ограничение результата через заголовок `Range`.
- `POST /Notifications` — Отправляет запрос на интеграцию с внешней системой. · коды: 202, 400 · примеры
  ← query: integratedSystemName?:str
- `PUT /Notifications` — Устанавливает признак просмотра уведомлений. · коды: 202, 400 · примеры
  ← body: SetViewedData
- `HEAD /Notifications` — Возвращает заголовок с количеством уведомлений пользователя. · коды: 200 · примеры
  ← query: includeIsViewed?:bool
- `PUT /Notifications/all` — Отмечает все уведомления пользователя как просмотренные. · коды: 202 · примеры
- `GET /Notifications/fields` — Возвращает список полей, используемых в шаблонах уведомлений. · paginated · коды: 200, 204, 206 · примеры
  → map<str>
  Поддерживает ограничение результата через заголовок `Range`.

## Protocols
- `GET /Protocols` — Возвращает список протоколов. · paginated · коды: 200, 204, 206 · примеры
  → map<RProtocolsListResult>
  Поддерживает ограничение результата через заголовок `Range`.

## Providers
- `GET /Providers` — Возвращает список провайдеров сообщений. · paginated · коды: 200, 204, 206 · примеры
  → map<RProvidersListResult>
  Поддерживает ограничение результата через заголовок `Range`.

## RecipientSelectionRules
- `GET /RecipientSelectionRules` — Возвращает список правил выбора получателя. · paginated · коды: 200, 204, 206 · примеры
  ← query: isDeleted?:bool, triggerID?:int → map<RRSRListResult>
  Поддерживает фильтрацию по query-параметрам и ограничение результата через заголовок `Range`.
- `POST /RecipientSelectionRules` — Создает правила выбора получателя. · коды: 201, 400 · примеры
  ← body: MSGRSRAddData[] → int[]
- `PUT /RecipientSelectionRules` — Изменяет правила выбора получателя. · коды: 202, 400 · примеры
  ← body: MSGRSRUpdateData[]
- `DELETE /RecipientSelectionRules` — Помечает правила выбора получателя как удаленные. · коды: 202, 409 · примеры
  ← body: int[]
- `GET /RecipientSelectionRules/recipients` — Возвращает список получателей уведомлений. · paginated · коды: 200, 204, 206 · примеры
  ← query: isHidden?:bool → map<RecipientListResult>
  Поддерживает фильтрацию по query-параметрам и ограничение результата через заголовок `Range`.
- `GET /RecipientSelectionRules/{id}` — Возвращает правило выбора получателя по идентификатору. · коды: 200, 204 · примеры
  ← path: id:int → RRSRGetResult
- `DELETE /RecipientSelectionRules/{id}` — Помечает правило выбора получателя как удаленное. · коды: 202, 409 · примеры
  ← path: id:int

## TriggerRecipientSelectionRules
- `POST /TriggerRecipientSelectionRules` — Добавляет или изменяет правила выбора получателя для триггера. · коды: 202, 400 · примеры
  ← body: MSGTRSRMergeData[]

## Triggers
- `GET /Triggers` — Возвращает список триггеров. · paginated · коды: 200, 204, 206 · примеры
  ← query: isDeleted?:bool, isEnabled?:bool → map<RTListResult>
  Поддерживает фильтрацию по query-параметрам и ограничение результата через заголовок `Range`.
- `POST /Triggers` — Создает триггеры. · коды: 201, 400 · примеры
  ← body: MSGTAddData[] → int[]
- `PUT /Triggers` — Изменяет триггеры. · коды: 202, 400 · примеры
  ← body: MSGTUpdateData[]
- `DELETE /Triggers` — Помечает триггеры как удалённые. · коды: 202, 400, 409 · примеры
  ← body: int[]
- `PUT /Triggers/activate` — Активирует триггеры. · коды: 202, 400 · примеры
  ← body: int[]
- `PUT /Triggers/deactivate` — Деактивирует триггеры. · коды: 202, 400 · примеры
  ← body: int[]
- `GET /Triggers/{id}` — Возвращает триггер по идентификатору. · коды: 200, 204 · примеры
  ← path: id:int → RTGetResult
- `DELETE /Triggers/{id}` — Помечает триггер как удалённый. · коды: 202, 409 · примеры
  ← path: id:int
- `GET /Triggers/{id}/criticalities` — Возвращает список критичностей для триггера. · paginated · коды: 200, 204, 206 · примеры
  ← path: id:int → IdNameResultOfShort[]
  Поддерживает ограничение результата через заголовок `Range`.
- `PUT /Triggers/{triggerID}/activate` — Активирует триггер. · коды: 202 · примеры
  ← path: triggerID:int
- `PUT /Triggers/{triggerID}/deactivate` — Деактивирует триггер. · коды: 202 · примеры
  ← path: triggerID:int

## Webhooks
- `GET /Webhooks` — Возвращает список webhook-ов. · paginated · коды: 200, 204, 206 · примеры
  → map<RWListResult>
  Поддерживает ограничение результата через заголовок `Range`.
- `POST /Webhooks` — Добавляет или обновляет webhook-и. · коды: 201, 400 · примеры
  ← body: MSGWMergeData[] → int[]
- `DELETE /Webhooks` — Помечает webhook-и как удаленные. · коды: 202 · примеры
  ← body: int[]
- `PUT /Webhooks/activate` — Активирует webhook-и. · коды: 202 · примеры
  ← body: int[]
- `PUT /Webhooks/activate/{id}` — Активирует webhook. · коды: 202 · примеры
  ← path: id:int
- `PUT /Webhooks/deactivate` — Деактивирует webhook-и. · коды: 202 · примеры
  ← body: int[]
- `PUT /Webhooks/deactivate/{id}` — Деактивирует webhook. · коды: 202 · примеры
  ← path: id:int
- `GET /Webhooks/{id}` — Возвращает детальную информацию о webhook-е по идентификатору. · коды: 200, 204 · примеры
  ← path: id:int → RWGetResult
- `DELETE /Webhooks/{id}` — Помечает webhook как удаленный. · коды: 202 · примеры
  ← path: id:int
