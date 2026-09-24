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

### `POST /Criticalities`

## Пример запроса:
```json
[
  {
    "name": "Высокая",
    "color": "#FF0000",
    "isDefault": false,
    "sortOrder": 1,
    "erpID": "ERP-CRIT-001"
  }
]
```
## Пример успешного ответа (201):
```json
[1, 2]
```
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `CriticalityAdd`.

### `PUT /Criticalities`

## Пример запроса:
```json
[
  {
    "id": 1,
    "name": "Высокая",
    "color": "#FF0000",
    "isDefault": false,
    "sortOrder": 1,
    "erpID": "ERP-CRIT-001"
  }
]
```
## Пример успешного ответа (202):
Тело ответа отсутствует.
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `CriticalityUpdate`.

### `DELETE /Criticalities`

## Пример запроса:
```json
[1, 2]
```
## Пример успешного ответа (202):
Тело ответа отсутствует.
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `CriticalityDelete`.

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

### `DELETE /Criticalities/{id}`

## Пример запроса:
`DELETE /Criticalities/1`
            
## Пример успешного ответа (202):
Тело ответа отсутствует.
## Негативные сценарии:
- 409 Conflict: критичность не может быть удалена из-за связанных данных.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `CriticalityDelete`.

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

### `POST /DeadlineRules`

## Пример запроса:
```json
[
  {
    "name": "Стандартное правило закрытия",
    "scheduleRuleID": 5,
    "runtime": 24.0
  }
]
```
## Пример успешного ответа (201):
```json
[
  {
    "id": 101
  }
]
```
## Негативные сценарии:
- 409 Conflict: ошибка валидации или конфликт данных.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `DeadlineRuleAdd`.

### `PUT /DeadlineRules`

## Пример запроса:
```json
[
  {
    "id": 101,
    "name": "Обновленное правило закрытия",
    "scheduleRuleID": 5,
    "runtime": 48.0
  }
]
```
## Пример успешного ответа (202):
Тело ответа отсутствует.
## Негативные сценарии:
- 409 Conflict: ошибка валидации или конфликт данных.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `DeadlineRuleUpdate`.

### `DELETE /DeadlineRules`

## Пример запроса:
```json
[101, 102]
```
## Пример успешного ответа (202):
Тело ответа отсутствует.
## Негативные сценарии:
- 409 Conflict: одно или несколько правил не могут быть удалены.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `DeadlineRuleDelete`.

### `PUT /DeadlineRules/activate`

## Пример запроса:
```json
[101, 102]
```
## Пример успешного ответа (202):
Тело ответа отсутствует.
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `DeadlineRuleActivate`.

### `POST /DeadlineRules/attributes`

## Пример запроса:
```json
[
  {
    "deadlineRuleID": 101,
    "data": [
      {
        "attributeID": 3,
        "attrNumbValue": 10
      }
    ]
  }
]
```
## Пример успешного ответа (201):
```json
[
  {
    "deadlineRuleID": 101,
    "attributeID": 3,
    "attrNumbValue": 10
  }
]
```
## Негативные сценарии:
- 204 NoContent: атрибуты не были добавлены.
- 409 Conflict: ошибка валидации или конфликт данных.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `DeadlineRuleAttributeAdd`.

### `DELETE /DeadlineRules/attributes`

## Пример запроса:
```json
[
  {
    "deadlineRuleID": 101,
    "data": [
      {
        "attributeID": 3,
        "attrNumbValue": 10
      }
    ]
  }
]
```
## Пример успешного ответа (202):
Тело ответа отсутствует.
## Негативные сценарии:
- 409 Conflict: ошибка валидации или конфликт данных.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `DeadlineRuleAttributeDelete`.

### `PUT /DeadlineRules/deactivate`

## Пример запроса:
```json
[101, 102]
```
## Пример успешного ответа (202):
Тело ответа отсутствует.
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `DeadlineRuleDeactivate`.

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

### `DELETE /DeadlineRules/{DeadlineRuleID}`

## Пример запроса:
`DELETE /DeadlineRules/101`
            
## Пример успешного ответа (202):
Тело ответа отсутствует.
## Негативные сценарии:
- 409 Conflict: правило не может быть удалено из-за связанных данных.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `DeadlineRuleDelete`.

### `PUT /DeadlineRules/{DeadlineRuleID}/activate`

## Пример запроса:
`PUT /DeadlineRules/101/activate`
            
## Пример успешного ответа (202):
Тело ответа отсутствует.
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `DeadlineRuleActivate`.

### `PUT /DeadlineRules/{DeadlineRuleID}/deactivate`

## Пример запроса:
`PUT /DeadlineRules/101/deactivate`
            
## Пример успешного ответа (202):
Тело ответа отсутствует.
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `DeadlineRuleDeactivate`.

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

### `POST /DeadlineRules/{deadlineRuleID}/attributes/{attributeID}/attrValues/{attrValue}`

## Пример запроса:
`POST /DeadlineRules/101/attributes/3/attrValues/10`
            
## Пример успешного ответа (201):
```json
[
  {
    "deadlineRuleID": 101,
    "attributeID": 3,
    "attrNumbValue": 10
  }
]
```
## Негативные сценарии:
- 409 Conflict: ошибка валидации или конфликт данных.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `DeadlineRuleAttributeAdd`.

### `DELETE /DeadlineRules/{deadlineRuleID}/attributes/{attributeID}/attrValues/{attrValue}`

## Пример запроса:
`DELETE /DeadlineRules/101/attributes/3/attrValues/10`
            
## Пример успешного ответа (202):
Тело ответа отсутствует.
## Негативные сценарии:
- 409 Conflict: ошибка валидации или конфликт данных.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `DeadlineRuleAttributeDelete`.
