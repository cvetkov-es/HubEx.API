# TSTG — примеры

> **Что здесь:** блоки примеров запросов/ответов ручек сервиса TSTG, вынесенные из `endpoints/TSTG.md`. Сигнатуры и типы — там же и в `schemas/TSTG.md`.

## TaskStageLinks

### `GET /TaskStageLinks`

## Пример запроса:
`GET /TaskStageLinks?taskTypeID=1&taskStageFromID=2&userID=500&roleID=101`
            
## Пример успешного ответа (200):
```json
[
  {
    "taskTypeID": 1,
    "fromTaskStage": { "id": 2, "name": "Назначена" },
    "toTaskStage": { "id": 3, "name": "В работе" },
    "taskStatus": { "id": 5, "name": "Принята" },
    "branch": { "id": 1, "name": "Основная ветка" },
    "name": "Принять",
    "description": "Принять заявку",
    "isPositiveResult": true,
    "permissionUiID": 10,
    "sortOrder": 1,
    "timeoutSeconds": null,
    "timeoutToDeadlineSeconds": null,
    "roles": [
      { "id": 101, "name": "Инженер", "description": "Роль инженера" }
    ]
  }
]
```
## Негативные сценарии:
- 204 NoContent: переходы по заданным фильтрам не найдены.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `TaskStageLinkList`.

### `POST /TaskStageLinks`

## Пример запроса:
`POST /TaskStageLinks`
            
```json
[
  {
    "taskTypeID": 1,
    "fromTaskStageID": 2,
    "toTaskStageID": 3,
    "name": "Принять",
    "description": "Принять заявку",
    "applyTaskStatusID": 5,
    "branchID": 1,
    "permissionUiID": 10,
    "isPositiveResult": true,
    "timeoutSeconds": null,
    "timeoutToDeadlineSeconds": null,
    "roles": [101]
  }
]
```
## Негативные сценарии:
- 400 BadRequest: некорректный формат данных.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `TaskStageLinkAdd`.

### `PUT /TaskStageLinks`

## Пример запроса:
`PUT /TaskStageLinks`
            
```json
[
  {
    "taskTypeID": 1,
    "fromTaskStageID": 2,
    "toTaskStageID": 3,
    "name": "Принять (обновлено)",
    "description": "Обновленное описание",
    "applyTaskStatusID": 5,
    "branchID": 1,
    "permissionUiID": 10,
    "isPositiveResult": true,
    "timeoutSeconds": 300,
    "timeoutToDeadlineSeconds": null,
    "roles": [101, 102]
  }
]
```
## Негативные сценарии:
- 400 BadRequest: некорректный формат данных.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `TaskStageLinkUpdate`.

### `DELETE /TaskStageLinks`

## Пример запроса:
`DELETE /TaskStageLinks`
            
```json
[
  { "taskTypeID": 1, "fromTaskStageID": 2, "toTaskStageID": 3 }
]
```
## Негативные сценарии:
- 400 BadRequest: некорректный формат данных удаления.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `TaskStageLinkDelete`.

### `POST /TaskStageLinks/copy`

## Пример запроса:
`POST /TaskStageLinks/copy`
            
```json
[
  { "sourceTaskTypeID": 1, "targetTaskTypeID": 2 }
]
```
## Негативные сценарии:
- 400 BadRequest: некорректный формат данных копирования.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `TaskStageLinkAdd`.

### `POST /TaskStageLinks/reorder`

## Пример запроса:
`POST /TaskStageLinks/reorder`
            
```json
[
  { "taskTypeID": 1, "fromTaskStageID": 2, "toTaskStageID": 3, "sortOrder": 1 },
  { "taskTypeID": 1, "fromTaskStageID": 2, "toTaskStageID": 5, "sortOrder": 2 }
]
```
## Негативные сценарии:
- 400 BadRequest: некорректный формат данных сортировки.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `TaskStageLinkReorder`.
