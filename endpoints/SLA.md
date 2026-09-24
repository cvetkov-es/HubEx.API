# SLA — справочник ручек

> **Что здесь:** все ручки сервиса SLA (API for SLA in HubEx): сигнатуры, параметры, права. Типы — schemas/SLA.md.
> **Когда сюда идти:** найти ручку и её вход/выход. Типы — `schemas/SLA.md`; грабли — `notes/SLA.md` (если есть).

Base: `{BASE_URL}/SLA`
> Примеры ответов вынесены в [../examples/SLA.md](../examples/SLA.md).

**Оглавление**

- Attributes — строки 15–17
- Criticalities — строки 19–31
- DeadlineRules — строки 33–63

## Attributes
- `GET /Attributes` — Получение списка атрибутов SLA · коды: 200, 204 · примеры
  → map<ResultsAttributesListResult>

## Criticalities
- `GET /Criticalities` — Получение списка критичностей · коды: 200, 204 · примеры
  ← query: contractID?:int[], workTypeID?:int[] → map<ResultsCriticalitiesGetResult>
- `POST /Criticalities` — Создание критичностей · коды: 201 · примеры
  ← body: SLACriticalityAddData[] → int[]
- `PUT /Criticalities` — Изменение критичностей · коды: 202 · примеры
  ← body: SLACriticalityUpdateData[]
- `DELETE /Criticalities` — Удаление критичностей · коды: 202 · примеры
  ← body: int[]
- `GET /Criticalities/{id}` — Получение критичности · коды: 200, 204 · примеры
  ← path: id:int → ResultsCriticalitiesGetResult
- `DELETE /Criticalities/{id}` — Удаление критичности · коды: 202, 409 · примеры
  ← path: id:int

## DeadlineRules
- `GET /DeadlineRules` — Получение списка правил планового закрытия заявки · коды: 200, 204, 206 · примеры
  → map<ResultsDeadlineRulesListResult>
- `POST /DeadlineRules` — Создание правил планового закрытия заявки · коды: 201, 409 · примеры
  ← body: SLADeadlineRuleDeadlineRuleAddData[] → ResultsDeadlineRulesPostResult[]
- `PUT /DeadlineRules` — Обновление правил планового закрытия заявки · коды: 202, 409 · примеры
  ← body: SLADeadlineRuleDeadlineRuleUpdateData[]
- `DELETE /DeadlineRules` — Удаление правил планового закрытия заявки · коды: 202, 409 · примеры
  ← body: int[]
- `PUT /DeadlineRules/activate` — Активация правил планового закрытия заявки · коды: 202 · примеры
  ← body: int[]
- `POST /DeadlineRules/attributes` — Добавление атрибутов к правилам планового закрытия заявки · коды: 201, 204, 409 · примеры
  ← body: DeadlineRuleActionDataOfDeadlineRuleAttributeData[] → ResultsDeadlineRuleAttributesDeadlineRuleAttributeResult[]
- `DELETE /DeadlineRules/attributes` — Удаление атрибутов у правил планового закрытия заявки · коды: 202, 409 · примеры
  ← body: DeadlineRuleActionDataOfDeadlineRuleAttributeData[]
- `PUT /DeadlineRules/deactivate` — Деактивация правил планового закрытия заявки · коды: 202 · примеры
  ← body: int[]
- `GET /DeadlineRules/{DeadlineRuleID}` — Получение правила планового закрытия заявки · коды: 200, 204, 400 · примеры
  ← path: DeadlineRuleID:int → ResultsDeadlineRulesGetResult
- `DELETE /DeadlineRules/{DeadlineRuleID}` — Удаление правила планового закрытия заявки · коды: 202, 409 · примеры
  ← path: DeadlineRuleID:int
- `PUT /DeadlineRules/{DeadlineRuleID}/activate` — Активация правила планового закрытия заявки · коды: 202 · примеры
  ← path: DeadlineRuleID:int
- `PUT /DeadlineRules/{DeadlineRuleID}/deactivate` — Деактивация правила планового закрытия заявки · коды: 202 · примеры
  ← path: DeadlineRuleID:int
- `GET /DeadlineRules/{deadlineRuleID}/attributes` — Получение атрибутов правила планового закрытия заявки · коды: 200, 204, 400 · примеры
  ← path: deadlineRuleID:int → map<int[]>
- `POST /DeadlineRules/{deadlineRuleID}/attributes/{attributeID}/attrValues/{attrValue}` — Добавление атрибута к правилу планового закрытия заявки · коды: 201, 409 · примеры
  ← path: deadlineRuleID:int, attributeID:int, attrValue:int → ResultsDeadlineRuleAttributesDeadlineRuleAttributeResult[]
- `DELETE /DeadlineRules/{deadlineRuleID}/attributes/{attributeID}/attrValues/{attrValue}` — Удаление атрибута у правила планового закрытия заявки · коды: 202, 409 · примеры
  ← path: deadlineRuleID:int, attributeID:int, attrValue:int
