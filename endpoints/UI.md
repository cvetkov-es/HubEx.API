# UI — справочник ручек

> **Что здесь:** все ручки сервиса UI (API for UI information): сигнатуры, параметры, права. Типы — schemas/UI.md.
> **Когда сюда идти:** найти ручку и её вход/выход. Типы — `schemas/UI.md`; грабли — `notes/UI.md` (если есть).

Base: `{BASE_URL}/UI`
> Примеры ответов вынесены в [../examples/UI.md](../examples/UI.md).

**Оглавление**

- Components — строки 50–52
- Filters — строки 54–58
- LayoutTemplates — строки 60–63
- Пример запроса: — строки 65–66
- Пример успешного ответа (200): — строки 68–78
- Негативные сценарии: — строки 80–86
- Пример запроса: — строки 88–113
- Пример успешного ответа (201): — строки 115–123
- Негативные сценарии: — строки 125–132
- Пример запроса: — строки 134–135
- Пример успешного ответа (200): — строки 137–145
- Негативные сценарии: — строки 147–155
- Пример запроса: — строки 157–158
- Пример успешного ответа (200): — строки 160–168
- Негативные сценарии: — строки 170–178
- Пример запроса: — строки 180–194
- Пример успешного ответа (200): — строки 196–204
- Негативные сценарии: — строки 206–215
- Пример запроса: — строки 217–218
- Пример успешного ответа (200): — строки 220–228
- Негативные сценарии: — строки 230–237
- Пример запроса: — строки 239–240
- Пример успешного ответа (200): — строки 242–252
- Негативные сценарии: — строки 254–261
- Пример запроса: — строки 263–264
- Пример успешного ответа (200): — строки 266–274
- Негативные сценарии: — строки 276–286
- Resources — строки 288–290
- SubsystemView — строки 292–296
- TaskViewTemplate — строки 298–300
- UserViews — строки 302–309
- Пример запроса: — строки 311–321
- Пример успешного ответа (201): — строки 323–323
- Негативные сценарии: — строки 325–332
- Пример запроса: — строки 334–345
- Пример успешного ответа (202): — строки 347–347
- Негативные сценарии: — строки 349–355
- Views — строки 357–361

## Components
- `GET /Components` — Возвращает полный список компонентов · коды: 200, 204, 206 · примеры
  → map<ResultsBaseComponentResult>

## Filters
- `GET /Filters` — Получение списка избранных фильтров пользователя · коды: 200, 204, 206 · примеры
  ← query: applicationID?:int, resource?:str, applicationID?:int, resource?:str → EntitiesUIUserFilterFavouriteEntity[]
- `POST /Filters/{resource}` — Сохранение избранных фильтров пользователя · коды: 202 · примеры
  ← path: resource:str; body: DataUIMergeData[]

## LayoutTemplates
- `GET /LayoutTemplates` — Получить список представлений · коды: 200, 204
  ← query: taskTypeID?:int[], isDefault?:bool, taskTypeID?:int, isDefault?:bool → ApiDtoLayoutTemplateDto[]
  Список возвращается с полным набором атрибутов представления.
            
## Пример запроса:
`GET /LayoutTemplates?taskTypeID=1&taskTypeID=2&isDefault=false`
            
## Пример успешного ответа (200):
```json
[
  {
    "id": 1,
    "isDefault": false,
    "name": "Шаблон для ремонта",
    "columns": [],
    "taskTypes": [1, 2]
  }
]
```
## Негативные сценарии:
- 204 NoContent: шаблоны не найдены по указанным фильтрам.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `TaskTemplateGet`.
- `POST /LayoutTemplates` — Создать представление · коды: 201, 400, 409
  ← body: ApiDtoLayoutTemplateDto → ApiDtoLayoutTemplateDto
  Создаёт представление со всеми связанными свойствами.
            
## Пример запроса:
```json
{
  "isDefault": false,
  "name": "Новый шаблон",
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
  "taskTypes": [1, 2]
}
```
## Пример успешного ответа (201):
```json
{
  "id": 10,
  "isDefault": false,
  "name": "Новый шаблон",
  "columns": [],
  "taskTypes": [1, 2]
}
```
## Негативные сценарии:
- 400 BadRequest: некорректные данные шаблона.
- 409 Conflict: шаблон с такими параметрами уже существует.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `TaskTemplateAdd`.
- `GET /LayoutTemplates/bytype/{id}` — Получить представление по типу заявки · коды: 200, 404
  ← path: id:int → ApiDtoLayoutTemplateDto
  Возвращает первое подходящее представление для типа заявки или дефолтное.
            
## Пример запроса:
`GET /LayoutTemplates/bytype/1`
            
## Пример успешного ответа (200):
```json
{
  "id": 3,
  "isDefault": false,
  "name": "Шаблон для типа 1",
  "columns": [],
  "taskTypes": [1]
}
```
## Негативные сценарии:
- 404 NotFound: представление для указанного типа заявки не найдено.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `TaskTemplateGet`.
- `GET /LayoutTemplates/default` — Возвращает шаблон по умолчанию · коды: 200, 409 · примеры
  → ApiDtoLayoutTemplateDto
- `POST /LayoutTemplates/default` — Создаёт шаблон по умолчанию · коды: 200, 409
  → ApiDtoLayoutTemplateDto
  Если шаблон с флагом `IsDefault = true` уже существует, возвращается ошибка `409 Conflict`.
            
## Пример запроса:
`POST /LayoutTemplates/default`
            
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
- 409 Conflict: шаблон по умолчанию уже существует.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `TaskTemplateAdd`.
- `GET /LayoutTemplates/{id}` — Получить конкретное представление · коды: 200, 404 · примеры
  ← path: id:int → ApiDtoLayoutTemplateDto
- `PUT /LayoutTemplates/{id}` — Обновить представление и все связанные сущности · коды: 200, 400, 404
  ← path: id:int; body: ApiDtoLayoutTemplateDto → ApiDtoLayoutTemplateDto
  Пересоздаёт представление полностью.
            
## Пример запроса:
`PUT /LayoutTemplates/5`
            
```json
{
  "isDefault": false,
  "name": "Обновленный шаблон",
  "columns": [
    {
      "index": 0,
      "blocks": []
    }
  ],
  "taskTypes": [1]
}
```
## Пример успешного ответа (200):
```json
{
  "id": 5,
  "isDefault": false,
  "name": "Обновленный шаблон",
  "columns": [],
  "taskTypes": [1]
}
```
## Негативные сценарии:
- 400 BadRequest: некорректные данные шаблона.
- 404 NotFound: шаблон с указанным `id` не найден.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `TaskTemplateUpdate`.
- `DELETE /LayoutTemplates/{id}` — Удалить представление и все связные сущности · коды: 202, 400, 404 · примеры
  ← path: id:int
- `GET /LayoutTemplates/{id}/Attributes` — Полный список доступных атрибутов системы с указанием использования в шаблоне · коды: 200, 204, 404
  ← path: id:int → ApiDtoAttributeDto[]
  Возвращает полный список доступных дополнительных полей с указанием того, были ли они перемещены пользователем в данном шаблоне.
            
## Пример запроса:
`GET /LayoutTemplates/5/Attributes`
            
## Пример успешного ответа (200):
```json
[
  {
    "id": 10,
    "name": "Приоритет",
    "isInUse": false
  }
]
```
## Негативные сценарии:
- 204 NoContent: атрибуты не найдены.
- 404 NotFound: шаблон с указанным `id` не найден.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `TaskTemplateGet`.
- `GET /LayoutTemplates/{id}/Components` — Полный список доступных компонентов системы с указанием использования в шаблоне · коды: 200, 204, 404
  ← path: id:int → ApiDtoComponentDto[]
  Возвращает полный список доступных полей системы с указанием того, были ли они перемещены пользователем в данном шаблоне.
            
## Пример запроса:
`GET /LayoutTemplates/5/Components`
            
## Пример успешного ответа (200):
```json
[
  {
    "id": 1,
    "code": "TaskDescription",
    "description": "Описание заявки",
    "isRequired": true,
    "isInUse": true
  }
]
```
## Негативные сценарии:
- 204 NoContent: компоненты не найдены.
- 404 NotFound: шаблон с указанным `id` не найден.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `TaskTemplateGet`.
- `PUT /LayoutTemplates/{id}/reset` — Сбрасывает настройки шаблона к состоянию шаблона по умолчанию · коды: 200, 404, 409
  ← path: id:int → ApiDtoLayoutTemplateDto
  NB: при этом шаблон не становится дефолтным для тенанта.
            
## Пример запроса:
`PUT /LayoutTemplates/5/reset`
            
## Пример успешного ответа (200):
```json
{
  "id": 5,
  "isDefault": false,
  "name": "Пользовательский шаблон",
  "columns": [],
  "taskTypes": [1, 2]
}
```
## Негативные сценарии:
- 404 NotFound: шаблон с указанным `id` не найден.
- 409 Conflict: сброс невозможен из-за конфликта данных.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `TaskTemplateUpdate`.
- `GET /LayoutTemplates/{id}/taskTypes` — Получить список типов задач представления · коды: 200, 204, 404 · примеры
  ← path: id:int → ApiDtoLayoutTaskTypeDto[]
- `PUT /LayoutTemplates/{id}/taskTypes` — Сопоставить список типов задач представления · коды: 202, 400, 404 · примеры
  ← path: id:int; body: int[]
- `DELETE /LayoutTemplates/{id}/taskTypes` — Отвязать типы задач от шаблона · коды: 202, 400, 404 · примеры
  ← path: id:int; body: int[]

## Resources
- `GET /Resources` — Возвращает список ресурсов · коды: 200, 204, 206 · примеры
  → map<IdCodeNameResultOfByte>

## SubsystemView
- `GET /SubsystemView` — Получение списка форм всех подсистем · коды: 200, 204, 500 · примеры
  → ProjectionsUISubsystemViewProjection[]
- `GET /SubsystemView/{subsystemID}` — Получение списка форм подсистемы по идентификатору · коды: 200, 204, 404, 500 · примеры
  ← path: subsystemID:int → ProjectionsUISubsystemViewProjection[]

## TaskViewTemplate
- `GET /TaskViewTemplate` — Получение списка шаблонов формы заявки · коды: 200, 204, 206 · примеры
  → map<ResultsTaskViewTemplatesTaskViewTemplateResult>

## UserViews
- `GET /UserViews/Users/{id}` — Получение списка шаблонов пользователя · коды: 200, 204, 404, 500 · примеры
  ← path: id:int → ProjectionsUITaskViewProjection[]
- `GET /UserViews/Users/{userID}/Applications/{applicationID}/{code}` — Получение шаблона пользователя · коды: 200, 204, 404, 500 · примеры
  ← path: userID:int, applicationID:int, code:str → ProjectionsUITaskViewProjection
- `POST /UserViews/Users/{userID}/Applications/{applicationID}/{code}` — Добавление индивидуального шаблона пользователя · коды: 201, 404, 500
  ← path: userID:int, applicationID:int, code:str; body: map<JsonLinqJToken>
  Тело запроса передается как JSON-объект (`JObject`) с произвольной структурой шаблона представления.
            
## Пример запроса:
`POST /UserViews/Users/100/Applications/1/taskList`
            
```json
{
  "columns": [
    { "field": "number", "width": 120, "visible": true },
    { "field": "status", "width": 100, "visible": true }
  ],
  "sort": { "field": "number", "direction": "desc" }
}
```
## Пример успешного ответа (201):
Тело ответа отсутствует.
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `UserViewWrite`.
- 404 NotFound: пользователь, приложение или форма не найдены.
- 500 InternalServerError: внутренняя ошибка сервера.
- `PUT /UserViews/Users/{userID}/Applications/{applicationID}/{code}` — Изменение индивидуального шаблона пользователя · коды: 202, 404, 500
  ← path: userID:int, applicationID:int, code:str; body: map<JsonLinqJToken>
  Тело запроса передается как JSON-объект (`JObject`) с произвольной структурой шаблона представления.
            
## Пример запроса:
`PUT /UserViews/Users/100/Applications/1/taskList`
            
```json
{
  "columns": [
    { "field": "number", "width": 150, "visible": true },
    { "field": "status", "width": 100, "visible": true },
    { "field": "created", "width": 180, "visible": false }
  ],
  "sort": { "field": "created", "direction": "asc" }
}
```
## Пример успешного ответа (202):
Тело ответа отсутствует.
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `UserViewWrite`.
- 404 NotFound: пользователь, приложение или форма не найдены.
- 500 InternalServerError: внутренняя ошибка сервера.
- `PUT /UserViews/Users/{userID}/Applications/{applicationID}/{code}/reset` — Сброс индивидуального шаблона пользователя · коды: 202, 404, 500 · примеры
  ← path: userID:int, applicationID:int, code:str

## Views
- `PUT /Views/Applications/{applicationID}/{code}` — Изменение дефолтного шаблона · коды: 202, 404, 500 · примеры
  ← path: applicationID:int, code:str; body: map<JsonLinqJToken>
- `PUT /Views/Applications/{applicationID}/{code}/reset` — Сброс дефолтного шаблона · коды: 202, 404, 500 · примеры
  ← path: applicationID:int, code:str
