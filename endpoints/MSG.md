# MSG — справочник ручек

> **Что здесь:** все ручки сервиса MSG (API for MSG in HubEx): сигнатуры, параметры, права. Типы — schemas/MSG.md. Сгенерировано из swagger.
> **Когда сюда идти:** найти ручку и её вход/выход. Типы — `schemas/MSG.md`; грабли — `notes/MSG.md` (если есть).
> **Источник:** `snapshots/MSG.json` · файл генерируется пайплайном — руками не править.

Base: `{BASE_URL}/MSG`

## ContentTypes
- `GET /ContentTypes` — Метод получения списка типов контента · права: ContentTypeList · paginated
  → ContentTypes.ListResult[]

## CriticalityForTriggers
- `POST /CriticalityForTriggers` — Добавляет или изменяет критичноти для триггера · права: CriticalityForTriggerMerge
  ← body: CriticalityForTrigger.MergeData[]

## MailBoxes
- `GET /MailBoxes` — Возвращает список mailbox-ов · права: MailBoxList · paginated
  → map<MailBox.ListResult>
- `POST /MailBoxes` — Добавить или обновить mailbox · права: MailBoxMerge
  ← body: MailBox.MergeData[] → int[]
- `DELETE /MailBoxes` — Помечает mailbox'ы как удаленные · права: MailBoxDelete
  ← body: int[]
- `PUT /MailBoxes/activate` — Делает mailbox'ы активными · права: MailBoxActivate
  ← body: int[]
- `PUT /MailBoxes/activate/{id}` — Делает mailbox активным · права: MailBoxActivate
  ← path: id:int
- `PUT /MailBoxes/deactivate` — Делает mailbox'ы неактивными · права: MailBoxDeactivate
  ← body: int[]
- `PUT /MailBoxes/deactivate/{id}` — Делает mailbox неактивным · права: MailBoxDeactivate
  ← path: id:int
- `GET /MailBoxes/regexactions` — Метод возвращает список действий, которые необходимо выполнить при неудачном применении 
регулярного выражения для темы или тела email-сообщения · права: RegexNotMatchActionList · paginated
  → map<RegexNotMatchAction.ListResult>
- `GET /MailBoxes/{id}` — Получение детальной информации о mailbox'е по идентификатору · права: MailBoxGet
  ← path: id:int → MailBox.GetResult
- `DELETE /MailBoxes/{id}` — Помечает mailbox как удаленный · права: MailBoxDelete
  ← path: id:int
- `GET /MailBoxes/{id}/errors` — Получение информации об ошибках, возникших при чтении mailbox'ов · права: MailBoxErrorsList · paginated
  ← path: id:int; query: occurredFrom?:any, occurredTill?:any → MailBox.GetResult
- `GET /MailBoxes/{mailBoxID}/senders` — Возвращает список sender'ов mailbox-ов · права: MailBoxSenderList · paginated
  ← path: mailBoxID:int → map<MailBoxSender.ListResult>
- `DELETE /MailBoxes/{mailBoxID}/senders` — Помечает sender'ы mailbox'a как удаленные · права: MailBoxSenderDelete
  ← path: mailBoxID:int; body: int[]
- `DELETE /MailBoxes/{mailBoxID}/senders/{id}` — Помечает sender mailbox'a как удаленный · права: MailBoxSenderDelete
  ← path: mailBoxID:int, id:int
- `GET /MailBoxes/{mailBoxID}/senders/{senderID}` — Получение детальной информации о sender'e mailbox'a по идентификатору · права: MailBoxSenderGet
  ← path: mailBoxID:int, senderID:int → MailBoxSender.GetResult

## MessageTemplates
- `GET /MessageTemplates` — Возвращает список активных шаблонов уведоплений · права: MessageTemplateList · paginated
  ← query: isDeleted?:enum(true, false) → map<MessageTemplates.ListResult>
- `POST /MessageTemplates` — Создает шаблоны уведомлений · права: MessageTemplateAdd
  ← body: MessageTemplate.AddData[] → int[]
- `PUT /MessageTemplates` — Изменяет шаблоны уведомлений · права: MessageTemplateUpdate
  ← body: MessageTemplate.UpdateData[]
- `DELETE /MessageTemplates` — Помечает шаблоны уведомлений, как удаленные · права: MessageTemplateDelete
  ← body: int[]
- `GET /MessageTemplates/{id}` — Возвращает шаблон уведомлений · права: MessageTemplateGet
  ← path: id:int → map<MessageTemplates.GetResult>
- `DELETE /MessageTemplates/{id}` — Помечает шаблон уведомлений, как удаленный · права: MessageTemplateDelete
  ← path: id:int
- `PUT /MessageTemplates/{id}/validate` — Изменяет валидационную информацию в шаблонах уведомлений · права: MessageTemplateValidate
  ← path: id:int

## NavigateTo
- `GET /NavigateTo` — Метод получения списка переходов · права: NavigateToList · paginated
  → NavigateTo.ListResult[]

## Notifications
- `GET /Notifications` — Возвращает список уведомлений пользователя · права: NotificationLogList · paginated
  ← query: includeIsViewed?:bool → map<Notification.ListResult>
- `POST /Notifications` — Отправка запроса на интеграцию с системой · права: ApplicationIntegrationRequest
  ← query: integratedSystemName?:str
- `PUT /Notifications` — Установка признака просмотра уведомления · права: NotificationLogList
  ← body: SetViewedData
- `HEAD /Notifications` — Возвращает заголовок запроса списка уведомлений пользователя с количеством данных · права: NotificationLogList
  ← query: includeIsViewed?:bool
- `PUT /Notifications/all` — Установка признака просмотра всех уведомлений пользователя · права: NotificationLogList
- `GET /Notifications/fields` — Получение списка полей, используемых для уведомлений · права: NotificationFieldsList · paginated
  → map<str>

## Protocols
- `GET /Protocols` — Возвращает список протоколов · права: ProtocolList · paginated
  → map<Protocols.ListResult>

## Providers
- `GET /Providers` — Метод получения списка провайдеров · права: ProviderList · paginated
  → Providers.ListResult[]

## RecipientSelectionRules
- `GET /RecipientSelectionRules` — Возвращает список правил выбора получателя · права: RecipientSelectionRuleList · paginated
  ← query: isDeleted?:enum(true, false), triggerID?:any → map<RecipientSelectionRules.ListResult>
- `POST /RecipientSelectionRules` — Создает правила выбора получателя · права: RecipientSelectionRuleAdd
  ← body: RecipientSelectionRule.AddData[] → int[]
- `PUT /RecipientSelectionRules` — Изменяет правила выбора получателя · права: RecipientSelectionRuleUpdate
  ← body: RecipientSelectionRule.UpdateData[]
- `DELETE /RecipientSelectionRules` — Помечает правила выбора получателя, как удаленные · права: RecipientSelectionRuleDelete
  ← body: int[]
- `GET /RecipientSelectionRules/recipients` — Возвращает список получателей уведомлений · права: RecipientList · paginated
  ← query: isHidden?:enum(true, false) → RecipientListResult[]
- `GET /RecipientSelectionRules/{id}` — Возвращает правило выбора получателя · права: RecipientSelectionRuleGet
  ← path: id:int → map<RecipientSelectionRules.GetResult>
- `DELETE /RecipientSelectionRules/{id}` — Помечает правило выбора получателя, как удаленное · права: RecipientSelectionRuleDelete
  ← path: id:int

## TriggerRecipientSelectionRules
- `POST /TriggerRecipientSelectionRules` — Добавляет или изменяет правила выбора получателя для триггера · права: TriggerRecipientSelectionRuleMerge
  ← body: TriggerRecipientSelectionRule.MergeData[]

## Triggers
- `GET /Triggers` — Возвращает список активных триггеров · права: TriggerList · paginated
  ← query: isDeleted?:enum(true, false), isEnabled?:enum(true, false) → map<Triggers.ListResult>
- `POST /Triggers` — Создает триггеры · права: TriggerAdd
  ← body: Trigger.AddData[] → int[]
- `PUT /Triggers` — Изменяет триггеры · права: TriggerUpdate
  ← body: Trigger.UpdateData[]
- `DELETE /Triggers` — Помечает триггеры, как удаленные · права: TriggerDelete
  ← body: int[]
- `PUT /Triggers/activate` — Делает триггеры активными · права: TriggerUpdate
  ← body: int[]
- `PUT /Triggers/deactivate` — Делает триггеры неактивными · права: TriggerUpdate
  ← body: int[]
- `GET /Triggers/{id}` — Возвращает триггер · права: TriggerGet
  ← path: id:int → map<Triggers.GetResult>
- `DELETE /Triggers/{id}` — Помечает триггер, как удаленный · права: TriggerDelete
  ← path: id:int
- `GET /Triggers/{id}/criticalities` — Метод получения списка критичностей для триггера · права: CriticalityForTriggerList · paginated
  ← path: id:int → Triggers.ListResult[]
- `PUT /Triggers/{triggerID}/activate` — Делает триггер активным · права: TriggerUpdate
  ← path: triggerID:int
- `PUT /Triggers/{triggerID}/deactivate` — Делает триггер неактивным · права: TriggerUpdate
  ← path: triggerID:int

## Webhooks
- `GET /Webhooks` — Возвращает список webhook-ов · права: WebhookList · paginated
  → map<Webhook.ListResult>
- `POST /Webhooks` — Добавить или обновить webhook · права: WebhookMerge
  ← body: Webhook.MergeData[] → int[]
- `DELETE /Webhooks` — Помечает webhookи, как удаленные · права: WebhookDelete
  ← body: int[]
- `PUT /Webhooks/activate` — Делает webhook-и, активными · права: WebhookActivate
  ← body: int[]
- `PUT /Webhooks/activate/{id}` — Делает webhook, активным · права: WebhookActivate
  ← path: id:int
- `PUT /Webhooks/deactivate` — Делает webhook-и, неактивными · права: WebhookDeactivate
  ← body: int[]
- `PUT /Webhooks/deactivate/{id}` — Делает webhook, неактивным · права: WebhookDeactivate
  ← path: id:int
- `GET /Webhooks/{id}` — Получение детальной информации о webhook'е по идентификатору · права: WebhookGet
  ← path: id:int → Webhook.GetResult
- `DELETE /Webhooks/{id}` — Помечает webhook, как удаленный · права: WebhookDelete
  ← path: id:int
