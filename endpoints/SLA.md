# SLA — справочник ручек

> **Что здесь:** все ручки сервиса SLA (API for SLA in HubEx): сигнатуры, параметры, права. Типы — schemas/SLA.md.
> **Когда сюда идти:** найти ручку и её вход/выход. Типы — `schemas/SLA.md`; грабли — `notes/SLA.md` (если есть).

Base: `{BASE_URL}/SLA`

**Оглавление**

- Attributes — строки 14–16
- Criticalities — строки 18–30
- DeadlineRules — строки 32–62

## Attributes
- `GET /Attributes` — Возвращает полный список атрибутов  SLA · права: AttributeSLAList · коды: 200
  → map<Attributes.ListResult>

## Criticalities
- `GET /Criticalities` — Возвращает полный список критичностей · права: CriticalitiesList · коды: 200, 500
  ← query: contractID?:int[], workTypeID?:int[] → map<Criticalities.GetResult>
- `POST /Criticalities` — Создает критичности · права: CriticalityAdd · коды: 201
  ← body: AddData[] → int[]
- `PUT /Criticalities` — Изменяет критичности · права: CriticalityUpdate · коды: 202
  ← body: UpdateData[]
- `DELETE /Criticalities` — Помечает критичности, как удаленные · права: CriticalityDelete · коды: 202
  ← body: int[]
- `GET /Criticalities/{id}` — Возвращает критичность · права: CriticalityGet · коды: 200
  ← path: id:int → Criticalities.GetResult
- `DELETE /Criticalities/{id}` — Помечает критичность как удаленную · права: CriticalityDelete · коды: 202, 409
  ← path: id:int

## DeadlineRules
- `GET /DeadlineRules` — Возвращает полный список правил планового закрытия заявки · права: DeadlineRuleList · paginated · коды: 200, 206, 500
  → map<DeadlineRules.ListResult>
- `POST /DeadlineRules` — Создает правила планового закрытия заявки · права: DeadlineRuleAdd · коды: 201, 409
  ← body: DeadlineRuleAddData[] → PostResult
- `PUT /DeadlineRules` — Обновляет правила планового закрытия заявки · права: DeadlineRuleUpdate · коды: 202, 409
  ← body: DeadlineRuleUpdateData[]
- `DELETE /DeadlineRules` — Помечает правила планового закрытия заявки как удаленные · права: DeadlineRuleDelete · коды: 202, 409
  ← body: int[]
- `PUT /DeadlineRules/activate` — Делает правила планового закрытия заявки активными · права: DeadlineRuleActivate · коды: 202
  ← body: int[]
- `POST /DeadlineRules/attributes` — Добавляет атрибуты к правилу планового закрытия заявки · права: DeadlineRuleAttributeAdd · коды: 201, 409
  ← body: DeadlineRuleActionData<DeadlineRuleAttributeData>[] → DeadlineRuleAttributeResult
- `DELETE /DeadlineRules/attributes` — Удаляет атрибуты у правила планового закрытия заявки · права: DeadlineRuleAttributeDelete · коды: 202, 409
  ← body: DeadlineRuleActionData<DeadlineRuleAttributeData>[]
- `PUT /DeadlineRules/deactivate` — Делает правила планового закрытия заявки неактивными · права: DeadlineRuleDeactivate · коды: 202
  ← body: int[]
- `GET /DeadlineRules/{DeadlineRuleID}` — Детальная информация по правилу планового закрытия заявки · права: DeadlineRuleGet · коды: 200, 400
  ← path: DeadlineRuleID:int → DeadlineRules.GetResult
- `DELETE /DeadlineRules/{DeadlineRuleID}` — Помечает правило планового закрытия заявки как удаленное · права: DeadlineRuleDelete · коды: 202, 409
  ← path: DeadlineRuleID:int
- `PUT /DeadlineRules/{DeadlineRuleID}/activate` — Делает правило планового закрытия заявки активным · права: DeadlineRuleActivate · коды: 202
  ← path: DeadlineRuleID:int
- `PUT /DeadlineRules/{DeadlineRuleID}/deactivate` — Делает правило планового закрытия заявки неактивным · права: DeadlineRuleDeactivate · коды: 202
  ← path: DeadlineRuleID:int
- `GET /DeadlineRules/{deadlineRuleID}/attributes` — Возвращает список действующих атрибутов для правила планового закрытия заявки · права: DeadlineRuleAttributeList · коды: 200, 400
  ← path: deadlineRuleID:int → map<int[]>
- `POST /DeadlineRules/{deadlineRuleID}/attributes/{attributeID}/attrValues/{attrValue}` — Добавляет атрибут к правилу планового закрытия заявки · права: DeadlineRuleAttributeAdd · коды: 201, 409
  ← path: deadlineRuleID:int, attributeID:int, attrValue:int → map<int[]>
- `DELETE /DeadlineRules/{deadlineRuleID}/attributes/{attributeID}/attrValues/{attrValue}` — Удаляет атрибут у правила планового закрытия заявки · права: DeadlineRuleAttributeDelete · коды: 202, 409
  ← path: deadlineRuleID:int, attributeID:int, attrValue:int
