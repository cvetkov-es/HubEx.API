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
