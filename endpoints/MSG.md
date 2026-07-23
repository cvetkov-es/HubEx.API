# MSG — справочник ручек

> **Что здесь:** только read-ручки (GET/HEAD) сервиса MSG (API for MSG in HubEx): сигнатуры, параметры, права. Типы — schemas/MSG.md.
> **Когда сюда идти:** найти ручку и её вход/выход. Типы — `schemas/MSG.md`; грабли — `notes/MSG.md` (если есть).
> **Линза read-only:** здесь только GET/HEAD. Write-ручки (POST/PUT/PATCH/DELETE) и их типы в API **существуют**, но в эту линзу не входят — не делай из их отсутствия здесь вывода, что их нет в API.

Base: `{BASE_URL}/MSG`

**Оглавление**

- ContentTypes — строки 22–24
- MailBoxes — строки 26–39
- MessageTemplates — строки 41–45
- NavigateTo — строки 47–49
- Notifications — строки 51–57
- Protocols — строки 59–61
- Providers — строки 63–65
- RecipientSelectionRules — строки 67–73
- Triggers — строки 75–81
- Webhooks — строки 83–87

## ContentTypes
- `GET /ContentTypes` — Метод получения списка типов контента · права: ContentTypeList · paginated · коды: 200, 206
  → ContentTypes.ListResult[]

## MailBoxes
- `GET /MailBoxes` — Возвращает список mailbox-ов · права: MailBoxList · paginated · коды: 200, 206
  → map<MailBox.ListResult>
- `GET /MailBoxes/regexactions` — Метод возвращает список действий, которые необходимо выполнить при неудачном применении 
регулярного выражения для темы или тела email-сообщения · права: RegexNotMatchActionList · paginated · коды: 200, 206
  → map<RegexNotMatchAction.ListResult>
- `GET /MailBoxes/{id}` — Получение детальной информации о mailbox'е по идентификатору · права: MailBoxGet · коды: 200
  ← path: id:int → MailBox.GetResult
- `GET /MailBoxes/{id}/errors` — Получение информации об ошибках, возникших при чтении mailbox'ов · права: MailBoxErrorsList · paginated · коды: 200, 206
  ← path: id:int; query: occurredFrom?:any, occurredTill?:any → MailBox.GetResult
- `GET /MailBoxes/{mailBoxID}/senders` — Возвращает список sender'ов mailbox-ов · права: MailBoxSenderList · paginated · коды: 200, 206
  ← path: mailBoxID:int → map<MailBoxSender.ListResult>
- `GET /MailBoxes/{mailBoxID}/senders/{senderID}` — Получение детальной информации о sender'e mailbox'a по идентификатору · права: MailBoxSenderGet · коды: 200
  ← path: mailBoxID:int, senderID:int → MailBoxSender.GetResult

## MessageTemplates
- `GET /MessageTemplates` — Возвращает список активных шаблонов уведоплений · права: MessageTemplateList · paginated · коды: 200, 206
  ← query: isDeleted?:enum(true, false) → map<MessageTemplates.ListResult>
- `GET /MessageTemplates/{id}` — Возвращает шаблон уведомлений · права: MessageTemplateGet · коды: 200
  ← path: id:int → map<MessageTemplates.GetResult>

## NavigateTo
- `GET /NavigateTo` — Метод получения списка переходов · права: NavigateToList · paginated · коды: 200, 206
  → NavigateTo.ListResult[]

## Notifications
- `GET /Notifications` — Возвращает список уведомлений пользователя · права: NotificationLogList · paginated · коды: 200, 206
  ← query: includeIsViewed?:bool → map<Notification.ListResult>
- `HEAD /Notifications` — Возвращает заголовок запроса списка уведомлений пользователя с количеством данных · права: NotificationLogList · коды: 200
  ← query: includeIsViewed?:bool
- `GET /Notifications/fields` — Получение списка полей, используемых для уведомлений · права: NotificationFieldsList · paginated · коды: 200, 206
  → map<str>

## Protocols
- `GET /Protocols` — Возвращает список протоколов · права: ProtocolList · paginated · коды: 200, 206
  → map<Protocols.ListResult>

## Providers
- `GET /Providers` — Метод получения списка провайдеров · права: ProviderList · paginated · коды: 200, 206
  → Providers.ListResult[]

## RecipientSelectionRules
- `GET /RecipientSelectionRules` — Возвращает список правил выбора получателя · права: RecipientSelectionRuleList · paginated · коды: 200, 206
  ← query: isDeleted?:enum(true, false), triggerID?:any → map<RecipientSelectionRules.ListResult>
- `GET /RecipientSelectionRules/recipients` — Возвращает список получателей уведомлений · права: RecipientList · paginated · коды: 200, 206
  ← query: isHidden?:enum(true, false) → RecipientListResult[]
- `GET /RecipientSelectionRules/{id}` — Возвращает правило выбора получателя · права: RecipientSelectionRuleGet · коды: 200
  ← path: id:int → map<RecipientSelectionRules.GetResult>

## Triggers
- `GET /Triggers` — Возвращает список активных триггеров · права: TriggerList · paginated · коды: 200, 206
  ← query: isDeleted?:enum(true, false), isEnabled?:enum(true, false) → map<Triggers.ListResult>
- `GET /Triggers/{id}` — Возвращает триггер · права: TriggerGet · коды: 200
  ← path: id:int → map<Triggers.GetResult>
- `GET /Triggers/{id}/criticalities` — Метод получения списка критичностей для триггера · права: CriticalityForTriggerList · paginated · коды: 200, 206
  ← path: id:int → Triggers.ListResult[]

## Webhooks
- `GET /Webhooks` — Возвращает список webhook-ов · права: WebhookList · paginated · коды: 200, 206
  → map<Webhook.ListResult>
- `GET /Webhooks/{id}` — Получение детальной информации о webhook'е по идентификатору · права: WebhookGet · коды: 200
  ← path: id:int → Webhook.GetResult
