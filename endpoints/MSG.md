# MSG — справочник ручек

> **Что здесь:** все ручки сервиса MSG (API for MSG in HubEx): сигнатуры, параметры, права. Типы — schemas/MSG.md.
> **Когда сюда идти:** найти ручку и её вход/выход. Типы — `schemas/MSG.md`; грабли — `notes/MSG.md` (если есть).

Base: `{BASE_URL}/MSG`

**Оглавление**

- ContentTypes — строки 23–25
- CriticalityForTriggers — строки 27–29
- MailBoxes — строки 31–62
- MessageTemplates — строки 64–78
- NavigateTo — строки 80–82
- Notifications — строки 84–95
- Protocols — строки 97–99
- Providers — строки 101–103
- RecipientSelectionRules — строки 105–119
- TriggerRecipientSelectionRules — строки 121–123
- Triggers — строки 125–147
- Webhooks — строки 149–167

## ContentTypes
- `GET /ContentTypes` — Метод получения списка типов контента · права: ContentTypeList · paginated · коды: 200, 206
  → ContentTypes.ListResult[]

## CriticalityForTriggers
- `POST /CriticalityForTriggers` — Добавляет или изменяет критичноти для триггера · права: CriticalityForTriggerMerge · коды: 202
  ← body: CriticalityForTrigger.MergeData[]

## MailBoxes
- `GET /MailBoxes` — Возвращает список mailbox-ов · права: MailBoxList · paginated · коды: 200, 206
  → map<MailBox.ListResult>
- `POST /MailBoxes` — Добавить или обновить mailbox · права: MailBoxMerge · коды: 201
  ← body: MailBox.MergeData[] → int[]
- `DELETE /MailBoxes` — Помечает mailbox'ы как удаленные · права: MailBoxDelete · коды: 202
  ← body: int[]
- `PUT /MailBoxes/activate` — Делает mailbox'ы активными · права: MailBoxActivate · коды: 202
  ← body: int[]
- `PUT /MailBoxes/activate/{id}` — Делает mailbox активным · права: MailBoxActivate · коды: 202
  ← path: id:int
- `PUT /MailBoxes/deactivate` — Делает mailbox'ы неактивными · права: MailBoxDeactivate · коды: 202
  ← body: int[]
- `PUT /MailBoxes/deactivate/{id}` — Делает mailbox неактивным · права: MailBoxDeactivate · коды: 202
  ← path: id:int
- `GET /MailBoxes/regexactions` — Метод возвращает список действий, которые необходимо выполнить при неудачном применении 
регулярного выражения для темы или тела email-сообщения · права: RegexNotMatchActionList · paginated · коды: 200, 206
  → map<RegexNotMatchAction.ListResult>
- `GET /MailBoxes/{id}` — Получение детальной информации о mailbox'е по идентификатору · права: MailBoxGet · коды: 200
  ← path: id:int → MailBox.GetResult
- `DELETE /MailBoxes/{id}` — Помечает mailbox как удаленный · права: MailBoxDelete · коды: 202
  ← path: id:int
- `GET /MailBoxes/{id}/errors` — Получение информации об ошибках, возникших при чтении mailbox'ов · права: MailBoxErrorsList · paginated · коды: 200, 206
  ← path: id:int; query: occurredFrom?:any, occurredTill?:any → MailBox.GetResult
- `GET /MailBoxes/{mailBoxID}/senders` — Возвращает список sender'ов mailbox-ов · права: MailBoxSenderList · paginated · коды: 200, 206
  ← path: mailBoxID:int → map<MailBoxSender.ListResult>
- `DELETE /MailBoxes/{mailBoxID}/senders` — Помечает sender'ы mailbox'a как удаленные · права: MailBoxSenderDelete · коды: 202
  ← path: mailBoxID:int; body: int[]
- `DELETE /MailBoxes/{mailBoxID}/senders/{id}` — Помечает sender mailbox'a как удаленный · права: MailBoxSenderDelete · коды: 202
  ← path: mailBoxID:int, id:int
- `GET /MailBoxes/{mailBoxID}/senders/{senderID}` — Получение детальной информации о sender'e mailbox'a по идентификатору · права: MailBoxSenderGet · коды: 200
  ← path: mailBoxID:int, senderID:int → MailBoxSender.GetResult

## MessageTemplates
- `GET /MessageTemplates` — Возвращает список активных шаблонов уведоплений · права: MessageTemplateList · paginated · коды: 200, 206
  ← query: isDeleted?:enum(true, false) → map<MessageTemplates.ListResult>
- `POST /MessageTemplates` — Создает шаблоны уведомлений · права: MessageTemplateAdd · коды: 201
  ← body: MessageTemplate.AddData[] → int[]
- `PUT /MessageTemplates` — Изменяет шаблоны уведомлений · права: MessageTemplateUpdate · коды: 202
  ← body: MessageTemplate.UpdateData[]
- `DELETE /MessageTemplates` — Помечает шаблоны уведомлений, как удаленные · права: MessageTemplateDelete · коды: 202
  ← body: int[]
- `GET /MessageTemplates/{id}` — Возвращает шаблон уведомлений · права: MessageTemplateGet · коды: 200
  ← path: id:int → map<MessageTemplates.GetResult>
- `DELETE /MessageTemplates/{id}` — Помечает шаблон уведомлений, как удаленный · права: MessageTemplateDelete · коды: 202, 409
  ← path: id:int
- `PUT /MessageTemplates/{id}/validate` — Изменяет валидационную информацию в шаблонах уведомлений · права: MessageTemplateValidate · коды: 202
  ← path: id:int

## NavigateTo
- `GET /NavigateTo` — Метод получения списка переходов · права: NavigateToList · paginated · коды: 200, 206
  → NavigateTo.ListResult[]

## Notifications
- `GET /Notifications` — Возвращает список уведомлений пользователя · права: NotificationLogList · paginated · коды: 200, 206
  ← query: includeIsViewed?:bool → map<Notification.ListResult>
- `POST /Notifications` — Отправка запроса на интеграцию с системой · права: ApplicationIntegrationRequest · коды: 202
  ← query: integratedSystemName?:str
- `PUT /Notifications` — Установка признака просмотра уведомления · права: NotificationLogList · коды: 202
  ← body: SetViewedData
- `HEAD /Notifications` — Возвращает заголовок запроса списка уведомлений пользователя с количеством данных · права: NotificationLogList · коды: 200
  ← query: includeIsViewed?:bool
- `PUT /Notifications/all` — Установка признака просмотра всех уведомлений пользователя · права: NotificationLogList · коды: 202
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
- `POST /RecipientSelectionRules` — Создает правила выбора получателя · права: RecipientSelectionRuleAdd · коды: 201
  ← body: RecipientSelectionRule.AddData[] → int[]
- `PUT /RecipientSelectionRules` — Изменяет правила выбора получателя · права: RecipientSelectionRuleUpdate · коды: 202
  ← body: RecipientSelectionRule.UpdateData[]
- `DELETE /RecipientSelectionRules` — Помечает правила выбора получателя, как удаленные · права: RecipientSelectionRuleDelete · коды: 202
  ← body: int[]
- `GET /RecipientSelectionRules/recipients` — Возвращает список получателей уведомлений · права: RecipientList · paginated · коды: 200, 206
  ← query: isHidden?:enum(true, false) → RecipientListResult[]
- `GET /RecipientSelectionRules/{id}` — Возвращает правило выбора получателя · права: RecipientSelectionRuleGet · коды: 200
  ← path: id:int → map<RecipientSelectionRules.GetResult>
- `DELETE /RecipientSelectionRules/{id}` — Помечает правило выбора получателя, как удаленное · права: RecipientSelectionRuleDelete · коды: 202, 409
  ← path: id:int

## TriggerRecipientSelectionRules
- `POST /TriggerRecipientSelectionRules` — Добавляет или изменяет правила выбора получателя для триггера · права: TriggerRecipientSelectionRuleMerge · коды: 202
  ← body: TriggerRecipientSelectionRule.MergeData[]

## Triggers
- `GET /Triggers` — Возвращает список активных триггеров · права: TriggerList · paginated · коды: 200, 206
  ← query: isDeleted?:enum(true, false), isEnabled?:enum(true, false) → map<Triggers.ListResult>
- `POST /Triggers` — Создает триггеры · права: TriggerAdd · коды: 201
  ← body: Trigger.AddData[] → int[]
- `PUT /Triggers` — Изменяет триггеры · права: TriggerUpdate · коды: 202
  ← body: Trigger.UpdateData[]
- `DELETE /Triggers` — Помечает триггеры, как удаленные · права: TriggerDelete · коды: 202
  ← body: int[]
- `PUT /Triggers/activate` — Делает триггеры активными · права: TriggerUpdate · коды: 202
  ← body: int[]
- `PUT /Triggers/deactivate` — Делает триггеры неактивными · права: TriggerUpdate · коды: 202
  ← body: int[]
- `GET /Triggers/{id}` — Возвращает триггер · права: TriggerGet · коды: 200
  ← path: id:int → map<Triggers.GetResult>
- `DELETE /Triggers/{id}` — Помечает триггер, как удаленный · права: TriggerDelete · коды: 202, 409
  ← path: id:int
- `GET /Triggers/{id}/criticalities` — Метод получения списка критичностей для триггера · права: CriticalityForTriggerList · paginated · коды: 200, 206
  ← path: id:int → Triggers.ListResult[]
- `PUT /Triggers/{triggerID}/activate` — Делает триггер активным · права: TriggerUpdate · коды: 202
  ← path: triggerID:int
- `PUT /Triggers/{triggerID}/deactivate` — Делает триггер неактивным · права: TriggerUpdate · коды: 202
  ← path: triggerID:int

## Webhooks
- `GET /Webhooks` — Возвращает список webhook-ов · права: WebhookList · paginated · коды: 200, 206
  → map<Webhook.ListResult>
- `POST /Webhooks` — Добавить или обновить webhook · права: WebhookMerge · коды: 201
  ← body: Webhook.MergeData[] → int[]
- `DELETE /Webhooks` — Помечает webhookи, как удаленные · права: WebhookDelete · коды: 202
  ← body: int[]
- `PUT /Webhooks/activate` — Делает webhook-и, активными · права: WebhookActivate · коды: 202
  ← body: int[]
- `PUT /Webhooks/activate/{id}` — Делает webhook, активным · права: WebhookActivate · коды: 202
  ← path: id:int
- `PUT /Webhooks/deactivate` — Делает webhook-и, неактивными · права: WebhookDeactivate · коды: 202
  ← body: int[]
- `PUT /Webhooks/deactivate/{id}` — Делает webhook, неактивным · права: WebhookDeactivate · коды: 202
  ← path: id:int
- `GET /Webhooks/{id}` — Получение детальной информации о webhook'е по идентификатору · права: WebhookGet · коды: 200
  ← path: id:int → Webhook.GetResult
- `DELETE /Webhooks/{id}` — Помечает webhook, как удаленный · права: WebhookDelete · коды: 202
  ← path: id:int
