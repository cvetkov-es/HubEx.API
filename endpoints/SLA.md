# SLA — справочник ручек

> **Что здесь:** все ручки сервиса SLA (API for SLA in HubEx): сигнатуры, параметры, права. Типы — schemas/SLA.md. Сгенерировано из swagger.
> **Когда сюда идти:** найти ручку и её вход/выход. Типы — `schemas/SLA.md`; грабли — `notes/SLA.md` (если есть).
> **Источник:** `snapshots/SLA.json` · файл генерируется пайплайном — руками не править.

Base: `{BASE_URL}/SLA`

## Attributes
- `GET /Attributes` — Возвращает полный список атрибутов  SLA · права: AttributeSLAList
  → map<Attributes.ListResult>

## Criticalities
- `GET /Criticalities` — Возвращает полный список критичностей · права: CriticalitiesList
  ← query: contractID?:int[], workTypeID?:int[] → map<Criticalities.GetResult>
- `POST /Criticalities` — Создает критичности · права: CriticalityAdd
  ← body: AddData[] → int[]
- `PUT /Criticalities` — Изменяет критичности · права: CriticalityUpdate
  ← body: UpdateData[]
- `DELETE /Criticalities` — Помечает критичности, как удаленные · права: CriticalityDelete
  ← body: int[]
- `GET /Criticalities/{id}` — Возвращает критичность · права: CriticalityGet
  ← path: id:int → Criticalities.GetResult
- `DELETE /Criticalities/{id}` — Помечает критичность как удаленную · права: CriticalityDelete
  ← path: id:int

## DeadlineRules
- `GET /DeadlineRules` — Возвращает полный список правил планового закрытия заявки · права: DeadlineRuleList · paginated
  → map<DeadlineRules.ListResult>
- `POST /DeadlineRules` — Создает правила планового закрытия заявки · права: DeadlineRuleAdd
  ← body: DeadlineRuleAddData[] → PostResult
- `PUT /DeadlineRules` — Обновляет правила планового закрытия заявки · права: DeadlineRuleUpdate
  ← body: DeadlineRuleUpdateData[]
- `DELETE /DeadlineRules` — Помечает правила планового закрытия заявки как удаленные · права: DeadlineRuleDelete
  ← body: int[]
- `PUT /DeadlineRules/activate` — Делает правила планового закрытия заявки активными · права: DeadlineRuleActivate
  ← body: int[]
- `POST /DeadlineRules/attributes` — Добавляет атрибуты к правилу планового закрытия заявки · права: DeadlineRuleAttributeAdd
  ← body: DeadlineRuleActionData<DeadlineRuleAttributeData>[] → DeadlineRuleAttributeResult
- `DELETE /DeadlineRules/attributes` — Удаляет атрибуты у правила планового закрытия заявки · права: DeadlineRuleAttributeDelete
  ← body: DeadlineRuleActionData<DeadlineRuleAttributeData>[]
- `PUT /DeadlineRules/deactivate` — Делает правила планового закрытия заявки неактивными · права: DeadlineRuleDeactivate
  ← body: int[]
- `GET /DeadlineRules/{DeadlineRuleID}` — Детальная информация по правилу планового закрытия заявки · права: DeadlineRuleGet
  ← path: DeadlineRuleID:int → DeadlineRules.GetResult
- `DELETE /DeadlineRules/{DeadlineRuleID}` — Помечает правило планового закрытия заявки как удаленное · права: DeadlineRuleDelete
  ← path: DeadlineRuleID:int
- `PUT /DeadlineRules/{DeadlineRuleID}/activate` — Делает правило планового закрытия заявки активным · права: DeadlineRuleActivate
  ← path: DeadlineRuleID:int
- `PUT /DeadlineRules/{DeadlineRuleID}/deactivate` — Делает правило планового закрытия заявки неактивным · права: DeadlineRuleDeactivate
  ← path: DeadlineRuleID:int
- `GET /DeadlineRules/{deadlineRuleID}/attributes` — Возвращает список действующих атрибутов для правила планового закрытия заявки · права: DeadlineRuleAttributeList
  ← path: deadlineRuleID:int → map<int[]>
- `POST /DeadlineRules/{deadlineRuleID}/attributes/{attributeID}/attrValues/{attrValue}` — Добавляет атрибут к правилу планового закрытия заявки · права: DeadlineRuleAttributeAdd
  ← path: deadlineRuleID:int, attributeID:int, attrValue:int → map<int[]>
- `DELETE /DeadlineRules/{deadlineRuleID}/attributes/{attributeID}/attrValues/{attrValue}` — Удаляет атрибут у правила планового закрытия заявки · права: DeadlineRuleAttributeDelete
  ← path: deadlineRuleID:int, attributeID:int, attrValue:int
