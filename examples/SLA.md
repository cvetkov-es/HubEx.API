# SLA — примеры

> **Что здесь:** блоки примеров запросов/ответов ручек сервиса SLA, вынесенные из `endpoints/SLA.md`. Сигнатуры и типы — там же и в `schemas/SLA.md`.

## Attributes

### `GET /Attributes`

## Пример запроса:
`GET /Attributes`
            
## Пример успешного ответа (200):
```json
{
  "1": {
    "name": "Тип заявки"
  },
  "2": {
    "name": "Регион"
  }
}
```
## Негативные сценарии:
- 204 NoContent: атрибуты не найдены.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `AttributeSLAList`.

## Criticalities

### `GET /Criticalities`

## Пример запроса:
`GET /Criticalities?contractID=10&workTypeID=5`
            
## Пример успешного ответа (200):
```json
{
  "1": {
    "name": "Высокая",
    "color": "#FF0000",
    "isDefault": false,
    "sortOrder": 1,
    "erpID": "ERP-CRIT-001"
  }
}
```
## Негативные сценарии:
- 204 NoContent: критичности не найдены.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `CriticalitiesList`.

### `GET /Criticalities/{id}`

## Пример запроса:
`GET /Criticalities/1`
            
## Пример успешного ответа (200):
```json
{
  "name": "Высокая",
  "color": "#FF0000",
  "isDefault": false,
  "sortOrder": 1,
  "erpID": "ERP-CRIT-001"
}
```
## Негативные сценарии:
- 204 NoContent: критичность с указанным `id` не найдена.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `CriticalityGet`.

## DeadlineRules

### `GET /DeadlineRules`

## Пример запроса:
`GET /DeadlineRules`
            
## Пример успешного ответа (200):
```json
{
  "101": {
    "id": 101,
    "name": "Стандартное правило закрытия",
    "scheduleRuleID": 5,
    "isActive": true,
    "runtime": 24.0
  }
}
```
## Пример успешного ответа (206):
Тело ответа имеет тот же формат, что и для `200`, но содержит частичный диапазон.
## Негативные сценарии:
- 204 NoContent: правила не найдены.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `DeadlineRuleList`.

### `GET /DeadlineRules/{DeadlineRuleID}`

## Пример запроса:
`GET /DeadlineRules/101`
            
## Пример успешного ответа (200):
```json
{
  "id": 101,
  "name": "Стандартное правило закрытия",
  "scheduleRuleID": 5,
  "isActive": true,
  "runtime": 24.0
}
```
## Негативные сценарии:
- 204 NoContent: правило с указанным `DeadlineRuleID` не найдено.
- 400 BadRequest: некорректный идентификатор правила.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `DeadlineRuleGet`.

### `GET /DeadlineRules/{deadlineRuleID}/attributes`

## Пример запроса:
`GET /DeadlineRules/101/attributes`
            
## Пример успешного ответа (200):
```json
{
  "3": [10, 20],
  "5": [15]
}
```
## Негативные сценарии:
- 204 NoContent: атрибуты для указанного правила не найдены.
- 400 BadRequest: некорректный идентификатор правила.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `DeadlineRuleAttributeList`.
