# UI — примеры

> **Что здесь:** блоки примеров запросов/ответов ручек сервиса UI, вынесенные из `endpoints/UI.md`. Сигнатуры и типы — там же и в `schemas/UI.md`.

## Components

### `GET /Components`

## Пример запроса:
`GET /Components`
            
## Пример успешного ответа (200):
```json
{
  "1": {
    "code": "TaskDescription",
    "description": "Описание заявки"
  }
}
```
## Пример успешного ответа (206):
Тело ответа имеет тот же формат, что и для `200`, но содержит частичный диапазон.
## Негативные сценарии:
- 204 NoContent: компоненты не найдены.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `ComponentsList`.

## Filters

### `GET /Filters`

## Пример запроса:
`GET /Filters?applicationID=1&resource=Tasks`
            
## Пример успешного ответа (200):
```json
[
  {
    "applicationID": 1,
    "resource": "Tasks",
    "sortOrder": 1
  }
]
```
## Пример успешного ответа (206):
Тело ответа имеет тот же формат, что и для `200`, но содержит частичный диапазон.
## Негативные сценарии:
- 204 NoContent: избранные фильтры не найдены.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `UserFilterFavouriteList`.

## LayoutTemplates

### `GET /LayoutTemplates/default`

## Пример запроса:
`GET /LayoutTemplates/default`
            
## Пример успешного ответа (200):
```json
{
  "id": 1,
  "isDefault": true,
  "name": "Шаблон по умолчанию",
  "columns": [],
  "taskTypes": []
}
```
## Негативные сценарии:
- 409 Conflict: шаблон по умолчанию не найден или возник конфликт при получении.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `TaskTemplateGet`.

### `GET /LayoutTemplates/{id}`

## Пример запроса:
`GET /LayoutTemplates/5`
            
## Пример успешного ответа (200):
```json
{
  "id": 5,
  "isDefault": false,
  "name": "Пользовательский шаблон",
  "columns": [
    {
      "index": 0,
      "blocks": [
        {
          "index": 0,
          "name": "Основная информация",
          "fields": [
            {
              "index": 0,
              "label": "Описание",
              "type": "Component",
              "code": "TaskDescription"
            }
          ]
        }
      ]
    }
  ],
  "taskTypes": [1]
}
```
## Негативные сценарии:
- 404 NotFound: шаблон с указанным `id` не найден.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `TaskTemplateGet`.

### `GET /LayoutTemplates/{id}/taskTypes`

## Пример запроса:
`GET /LayoutTemplates/5/taskTypes`
            
## Пример успешного ответа (200):
```json
[
  {
    "id": 1,
    "name": "Ремонт"
  },
  {
    "id": 2,
    "name": "Обслуживание"
  }
]
```
## Негативные сценарии:
- 204 NoContent: типы задач для шаблона не найдены.
- 404 NotFound: шаблон с указанным `id` не найден.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `TaskTemplateGet`.

## Resources

### `GET /Resources`

## Пример запроса:
`GET /Resources`
            
## Пример успешного ответа (200):
```json
{
  "1": {
    "id": 1,
    "code": "Tasks",
    "name": "Заявки"
  }
}
```
## Пример успешного ответа (206):
Тело ответа имеет тот же формат, что и для `200`, но содержит частичный диапазон.
## Негативные сценарии:
- 204 NoContent: ресурсы не найдены.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `ResourcesList`.

## SubsystemView

### `GET /SubsystemView`

## Пример запроса:
`GET /SubsystemView`
            
## Пример успешного ответа (200):
```json
[
  {
    "subsystemID": 5,
    "viewCode": "TaskList",
    "description": "Список заявок"
  }
]
```
## Негативные сценарии:
- 204 NoContent: формы подсистемы не найдены.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав для просмотра форм подсистемы.
- 500 InternalServerError: внутренняя ошибка сервера.

### `GET /SubsystemView/{subsystemID}`

## Пример запроса:
`GET /SubsystemView/5`
            
## Пример успешного ответа (200):
```json
[
  {
    "subsystemID": 5,
    "viewCode": "TaskList",
    "description": "Список заявок"
  }
]
```
## Негативные сценарии:
- 204 NoContent: формы подсистемы не найдены.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав для просмотра форм подсистемы.
- 404 NotFound: подсистема не найдена.
- 500 InternalServerError: внутренняя ошибка сервера.

## TaskViewTemplate

### `GET /TaskViewTemplate`

## Пример запроса:
`GET /TaskViewTemplate`
            
## Пример успешного ответа (200):
```json
{
  "1": {
    "name": "Стандартная форма",
    "code": "DefaultTaskView",
    "isDefault": true
  }
}
```
## Пример успешного ответа (206):
Тело ответа имеет тот же формат, что и для `200`, но содержит частичный диапазон.
## Негативные сценарии:
- 204 NoContent: шаблоны не найдены.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `TaskViewTemplateList`.

## UserViews

### `GET /UserViews/Users/{id}`

## Пример запроса:
`GET /UserViews/Users/100`
            
## Пример успешного ответа (200):
```json
[
  {
    "userID": 100,
    "applicationID": 1,
    "code": "taskList",
    "data": "{ \"columns\": [] }"
  }
]
```
## Негативные сценарии:
- 204 NoContent: шаблоны пользователя не найдены.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `UserViewRead`.
- 404 NotFound: пользователь не найден.
- 500 InternalServerError: внутренняя ошибка сервера.

### `GET /UserViews/Users/{userID}/Applications/{applicationID}/{code}`

## Пример запроса:
`GET /UserViews/Users/100/Applications/1/taskList`
            
## Пример успешного ответа (200):
```json
{
  "userID": 100,
  "applicationID": 1,
  "code": "taskList",
  "data": "{ \"columns\": [ { \"field\": \"number\", \"width\": 120 } ] }"
}
```
## Негативные сценарии:
- 204 NoContent: шаблон не найден.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `UserViewRead`.
- 404 NotFound: пользователь, приложение или форма не найдены.
- 500 InternalServerError: внутренняя ошибка сервера.
