# REPORT — примеры

> **Что здесь:** блоки примеров запросов/ответов ручек сервиса REPORT, вынесенные из `endpoints/REPORT.md`. Сигнатуры и типы — там же и в `schemas/REPORT.md`.

## AssetMaintenance

### `GET /AssetMaintenance/planned`

## Пример запроса:
`GET /AssetMaintenance/planned?validFrom=2026-01-01&validTill=2026-12-31`
            
## Пример успешного ответа (200):
```json
[
  {
    "taskTemplateID": 10,
    "appointment": "2026-03-15T09:00:00Z",
    "normalWorkingHours": 2,
    "normalWorkingMinutes": 120,
    "workType": { "id": 5, "name": "ТО оборудования" },
    "asset": { "id": 100, "name": "Насосная станция №1" }
  }
]
```
## Негативные сценарии:
- 204 NoContent: данные не найдены.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `PreventiveAssetMaintenanceList`.

## CompletionTime

### `GET /CompletionTime`

## Пример запроса:
`GET /CompletionTime?groupByPeriod=Month&creationFrom=2026-01-01&creationTill=2026-12-31`
            
## Пример успешного ответа (200):
```json
[
  {
    "period": { "from": "2026-01-01T00:00:00Z", "till": "2026-01-31T23:59:59Z" },
    "completionTime": { "totalMinutes": 4800, "averageMinutes": 120 }
  }
]
```
## Негативные сценарии:
- 204 NoContent: данные по заданным фильтрам не найдены.
- 206 PartialContent: частичный ответ при использовании Range-заголовка.
- 400 BadRequest: не указан или некорректен параметр groupByPeriod.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав TaskListCompletionTime.

## PowerBICustomReports

### `GET /PowerBICustomReports`

## Пример запроса:
`GET /PowerBICustomReports`
            
## Пример успешного ответа (200):
```json
{
  "1": {
    "name": "Отчет по заявкам",
    "reportID": "a1b2c3d4-e5f6-7890-abcd-ef1234567890",
    "reportType": "PowerBI"
  }
}
```
## Негативные сценарии:
- 204 NoContent: отчеты не найдены.
- 206 PartialContent: частичный ответ при использовании Range-заголовка.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `PowerBICustomReportList`.

## ReactionTime

### `GET /ReactionTime`

## Пример запроса:
`GET /ReactionTime?groupByPeriod=Week&creationFrom=2026-01-01&creationTill=2026-03-31`
            
## Пример успешного ответа (200):
```json
[
  {
    "period": { "from": "2026-01-01T00:00:00Z", "till": "2026-01-07T23:59:59Z" },
    "reactionTime": { "totalMinutes": 360, "averageMinutes": 45 }
  }
]
```
## Негативные сценарии:
- 204 NoContent: данные по заданным фильтрам не найдены.
- 206 PartialContent: частичный ответ при использовании Range-заголовка.
- 400 BadRequest: не указан или некорректен параметр groupByPeriod.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав TaskListReactionTime.

## TasksByAssets

### `GET /TasksByAssets`

## Пример запроса:
`GET /TasksByAssets?searchText=ремонт&assetID=10&isClosed=false`
            
## Пример успешного ответа (200):
```json
[
  {
    "asset": { "id": 10, "name": "Насосная станция" },
    "activeTasksCount": 5,
    "outdatedTasksCount": 1,
    "undefinedTasksCount": 0,
    "total": 6
  }
]
```
## Негативные сценарии:
- 204 NoContent: данные по заданным фильтрам не найдены.
- 206 PartialContent: частичный ответ при использовании Range-заголовка.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав TaskListGroupByAssets.

## TasksByAssignees

### `GET /TasksByAssignees`

## Пример запроса:
`GET /TasksByAssignees?searchText=12345&assignedTo=15`
            
## Пример успешного ответа (200):
```json
[
  {
    "assignee": { "id": 15, "lastName": "Иванов", "firstName": "Иван" },
    "activeTasksCount": 3,
    "outdatedTasksCount": 0,
    "undefinedTasksCount": 0,
    "total": 3
  }
]
```
## Негативные сценарии:
- 204 NoContent: данные по заданным фильтрам не найдены.
- 206 PartialContent: частичный ответ при использовании Range-заголовка.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав TaskListGroupByAssignees.

## TasksByCompanies

### `GET /TasksByCompanies`

## Пример запроса:
`GET /TasksByCompanies?searchText=обслуживание&companyID=3`
            
## Пример успешного ответа (200):
```json
[
  {
    "company": { "id": 3, "name": "ООО Ремонт" },
    "activeTasksCount": 8,
    "outdatedTasksCount": 2,
    "undefinedTasksCount": 0,
    "total": 10
  }
]
```
## Негативные сценарии:
- 204 NoContent: данные по заданным фильтрам не найдены.
- 206 PartialContent: частичный ответ при использовании Range-заголовка.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав TaskListGroupByCompanies.

## TasksByStages

### `GET /TasksByStages`

## Пример запроса:
`GET /TasksByStages?taskStageID=2&isCompleted=false`
            
## Пример успешного ответа (200):
```json
[
  {
    "taskStage": { "id": 2, "name": "В работе", "color": "#FFA500" },
    "activeTasksCount": 12,
    "outdatedTasksCount": 1,
    "undefinedTasksCount": 0,
    "total": 13
  }
]
```
## Негативные сценарии:
- 204 NoContent: данные по заданным фильтрам не найдены.
- 206 PartialContent: частичный ответ при использовании Range-заголовка.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав TaskListGroupByStages.

## TasksByWorkTypes

### `GET /TasksByWorkTypes`

## Пример запроса:
`GET /TasksByWorkTypes?searchText=ТО&workTypeID=5`
            
## Пример успешного ответа (200):
```json
[
  {
    "workType": { "id": 5, "name": "Техническое обслуживание" },
    "activeTasksCount": 7,
    "outdatedTasksCount": 0,
    "undefinedTasksCount": 0,
    "total": 7
  }
]
```
## Негативные сценарии:
- 204 NoContent: данные по заданным фильтрам не найдены.
- 206 PartialContent: частичный ответ при использовании Range-заголовка.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав TaskListGroupByWorkTypes.

## WorkingTime

### `GET /WorkingTime`

## Пример запроса:
`GET /WorkingTime?groupByPeriod=Day&assignedTo=15&creationFrom=2026-08-01`
            
## Пример успешного ответа (200):
```json
[
  {
    "period": { "from": "2026-08-01T00:00:00Z", "till": "2026-08-01T23:59:59Z" },
    "workingTime": { "totalMinutes": 960, "averageMinutes": 80 }
  }
]
```
## Негативные сценарии:
- 204 NoContent: данные по заданным фильтрам не найдены.
- 206 PartialContent: частичный ответ при использовании Range-заголовка.
- 400 BadRequest: не указан или некорректен параметр groupByPeriod.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав TaskListWorkingTime.
