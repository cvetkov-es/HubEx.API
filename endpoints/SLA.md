# SLA — справочник ручек

> **Что здесь:** только read-ручки (GET/HEAD) сервиса SLA (API for SLA in HubEx): сигнатуры, параметры, права. Типы — schemas/SLA.md.
> **Когда сюда идти:** найти ручку и её вход/выход. Типы — `schemas/SLA.md`; грабли — `notes/SLA.md` (если есть).
> **Линза read-only:** здесь только GET/HEAD. Write-ручки (POST/PUT/PATCH/DELETE) и их типы в API **существуют**, но в эту линзу не входят — не делай из их отсутствия здесь вывода, что их нет в API.

Base: `{BASE_URL}/SLA`
> Примеры ответов вынесены в [../examples/SLA.md](../examples/SLA.md).

**Оглавление**

- Attributes — строки 16–18
- Criticalities — строки 20–24
- DeadlineRules — строки 26–32

## Attributes
- `GET /Attributes` — Получение списка атрибутов SLA · коды: 200, 204 · примеры
  → map<ResultsAttributesListResult>

## Criticalities
- `GET /Criticalities` — Получение списка критичностей · коды: 200, 204 · примеры
  ← query: contractID?:int[], workTypeID?:int[] → map<ResultsCriticalitiesGetResult>
- `GET /Criticalities/{id}` — Получение критичности · коды: 200, 204 · примеры
  ← path: id:int → ResultsCriticalitiesGetResult

## DeadlineRules
- `GET /DeadlineRules` — Получение списка правил планового закрытия заявки · коды: 200, 204, 206 · примеры
  → map<ResultsDeadlineRulesListResult>
- `GET /DeadlineRules/{DeadlineRuleID}` — Получение правила планового закрытия заявки · коды: 200, 204, 400 · примеры
  ← path: DeadlineRuleID:int → ResultsDeadlineRulesGetResult
- `GET /DeadlineRules/{deadlineRuleID}/attributes` — Получение атрибутов правила планового закрытия заявки · коды: 200, 204, 400 · примеры
  ← path: deadlineRuleID:int → map<int[]>
