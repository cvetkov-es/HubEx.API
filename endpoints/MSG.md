# MSG — справочник ручек

> **Что здесь:** только read-ручки (GET/HEAD) сервиса MSG (API for MSG in HubEx): сигнатуры, параметры, права. Типы — schemas/MSG.md.
> **Когда сюда идти:** найти ручку и её вход/выход. Типы — `schemas/MSG.md`; грабли — `notes/MSG.md` (если есть).
> **Линза read-only:** здесь только GET/HEAD. Write-ручки (POST/PUT/PATCH/DELETE) и их типы в API **существуют**, но в эту линзу не входят — не делай из их отсутствия здесь вывода, что их нет в API.

Base: `{BASE_URL}/MSG`
> Примеры ответов вынесены в [../examples/MSG.md](../examples/MSG.md).

**Оглавление**

- ContentTypes — строки 23–26
- MailBoxes — строки 28–44
- MessageTemplates — строки 46–52
- NavigateTo — строки 54–57
- Notifications — строки 59–67
- Protocols — строки 69–72
- Providers — строки 74–77
- RecipientSelectionRules — строки 79–87
- Triggers — строки 89–97
- Webhooks — строки 99–104

## ContentTypes
- `GET /ContentTypes` — Возвращает список типов контента. · paginated · коды: 200, 204, 206 · примеры
  → map<RCTListResult>
  Поддерживает ограничение результата через заголовок `Range`.

## MailBoxes
- `GET /MailBoxes` — Возвращает список почтовых ящиков. · paginated · коды: 200, 204, 206 · примеры
  → map<RMBListResult>
  Поддерживает ограничение результата через заголовок `Range`.
- `GET /MailBoxes/regexactions` — Возвращает список действий при неудачном применении регулярного выражения. · paginated · коды: 200, 204, 206 · примеры
  → map<RRNMAListResult>
  Справочник действий, которые выполняются, если регулярное выражение для темы или тела письма не совпало. Поддерживает ограничение результата через заголовок `Range`.
- `GET /MailBoxes/{id}` — Возвращает почтовый ящик по идентификатору. · коды: 200, 204 · примеры
  ← path: id:int → RMBGetResult
- `GET /MailBoxes/{id}/errors` — Возвращает ошибки чтения почтового ящика. · paginated · коды: 200, 204, 206 · примеры
  ← path: id:int; query: occurredFrom?:datetime, occurredTill?:datetime → MailBoxErrorsEntity[]
  Поддерживает фильтрацию по дате возникновения ошибки и ограничение результата через заголовок `Range`.
- `GET /MailBoxes/{mailBoxID}/senders` — Возвращает список отправителей почтового ящика. · paginated · коды: 200, 204, 206 · примеры
  ← path: mailBoxID:int → map<RMBSListResult>
  Поддерживает ограничение результата через заголовок `Range`.
- `GET /MailBoxes/{mailBoxID}/senders/{senderID}` — Возвращает отправителя почтового ящика по идентификатору. · коды: 200, 204 · примеры
  ← path: mailBoxID:int, senderID:int → RMBSGetResult

## MessageTemplates
- `GET /MessageTemplates` — Возвращает список шаблонов уведомлений. · paginated · коды: 200, 204, 206 · примеры
  ← query: isDeleted?:bool → map<RMTListResult>
  Поддерживает фильтрацию по query-параметрам и ограничение результата через заголовок `Range`.
- `GET /MessageTemplates/{id}` — Возвращает шаблон уведомлений по идентификатору. · коды: 200, 204 · примеры
  ← path: id:int → RMTGetResult
  Используется для просмотра и редактирования карточки шаблона уведомления.

## NavigateTo
- `GET /NavigateTo` — Возвращает список переходов. · paginated · коды: 200, 204, 206 · примеры
  → map<RNTListResult>
  Поддерживает ограничение результата через заголовок `Range`.

## Notifications
- `GET /Notifications` — Возвращает список уведомлений пользователя. · paginated · коды: 200, 204, 206 · примеры
  ← query: includeIsViewed?:bool → map<RNListResult>
  Поддерживает ограничение результата через заголовок `Range`.
- `HEAD /Notifications` — Возвращает заголовок с количеством уведомлений пользователя. · коды: 200 · примеры
  ← query: includeIsViewed?:bool
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
- `GET /RecipientSelectionRules/recipients` — Возвращает список получателей уведомлений. · paginated · коды: 200, 204, 206 · примеры
  ← query: isHidden?:bool → map<RecipientListResult>
  Поддерживает фильтрацию по query-параметрам и ограничение результата через заголовок `Range`.
- `GET /RecipientSelectionRules/{id}` — Возвращает правило выбора получателя по идентификатору. · коды: 200, 204 · примеры
  ← path: id:int → RRSRGetResult

## Triggers
- `GET /Triggers` — Возвращает список триггеров. · paginated · коды: 200, 204, 206 · примеры
  ← query: isDeleted?:bool, isEnabled?:bool → map<RTListResult>
  Поддерживает фильтрацию по query-параметрам и ограничение результата через заголовок `Range`.
- `GET /Triggers/{id}` — Возвращает триггер по идентификатору. · коды: 200, 204 · примеры
  ← path: id:int → RTGetResult
- `GET /Triggers/{id}/criticalities` — Возвращает список критичностей для триггера. · paginated · коды: 200, 204, 206 · примеры
  ← path: id:int → IdNameResultOfShort[]
  Поддерживает ограничение результата через заголовок `Range`.

## Webhooks
- `GET /Webhooks` — Возвращает список webhook-ов. · paginated · коды: 200, 204, 206 · примеры
  → map<RWListResult>
  Поддерживает ограничение результата через заголовок `Range`.
- `GET /Webhooks/{id}` — Возвращает детальную информацию о webhook-е по идентификатору. · коды: 200, 204 · примеры
  ← path: id:int → RWGetResult
