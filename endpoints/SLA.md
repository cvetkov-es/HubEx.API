# SLA — справочник ручек

> **Что здесь:** только read-ручки (GET/HEAD) сервиса SLA (API for SLA in HubEx): сигнатуры, параметры, права. Типы — schemas/SLA.md.
> **Когда сюда идти:** найти ручку и её вход/выход. Типы — `schemas/SLA.md`; грабли — `notes/SLA.md` (если есть).
> **Линза read-only:** здесь только GET/HEAD. Write-ручки (POST/PUT/PATCH/DELETE) и их типы в API **существуют**, но в эту линзу не входят — не делай из их отсутствия здесь вывода, что их нет в API.

Base: `{BASE_URL}/SLA`

**Оглавление**

- Attributes — строки 15–17
- Criticalities — строки 19–23
- DeadlineRules — строки 25–31

## Attributes
- `GET /Attributes` — Возвращает полный список атрибутов  SLA · права: AttributeSLAList · коды: 200
  → map<Attributes.ListResult>

## Criticalities
- `GET /Criticalities` — Возвращает полный список критичностей · права: CriticalitiesList · коды: 200, 500
  ← query: contractID?:int[], workTypeID?:int[] → map<Criticalities.GetResult>
- `GET /Criticalities/{id}` — Возвращает критичность · права: CriticalityGet · коды: 200
  ← path: id:int → Criticalities.GetResult

## DeadlineRules
- `GET /DeadlineRules` — Возвращает полный список правил планового закрытия заявки · права: DeadlineRuleList · paginated · коды: 200, 206, 500
  → map<DeadlineRules.ListResult>
- `GET /DeadlineRules/{DeadlineRuleID}` — Детальная информация по правилу планового закрытия заявки · права: DeadlineRuleGet · коды: 200, 400
  ← path: DeadlineRuleID:int → DeadlineRules.GetResult
- `GET /DeadlineRules/{deadlineRuleID}/attributes` — Возвращает список действующих атрибутов для правила планового закрытия заявки · права: DeadlineRuleAttributeList · коды: 200, 400
  ← path: deadlineRuleID:int → map<int[]>
