# UI — справочник ручек

> **Что здесь:** только read-ручки (GET/HEAD) сервиса UI (API for UI information): сигнатуры, параметры, права. Типы — schemas/UI.md.
> **Когда сюда идти:** найти ручку и её вход/выход. Типы — `schemas/UI.md`; грабли — `notes/UI.md` (если есть).
> **Линза read-only:** здесь только GET/HEAD. Write-ручки (POST/PUT/PATCH/DELETE) и их типы в API **существуют**, но в эту линзу не входят — не делай из их отсутствия здесь вывода, что их нет в API.

Base: `{BASE_URL}/UI`
> Примеры ответов вынесены в [../examples/UI.md](../examples/UI.md).

**Оглавление**

- Components — строки 32–34
- Filters — строки 36–38
- LayoutTemplates — строки 40–43
- Пример запроса: — строки 45–46
- Пример успешного ответа (200): — строки 48–58
- Негативные сценарии: — строки 60–66
- Пример запроса: — строки 68–69
- Пример успешного ответа (200): — строки 71–79
- Негативные сценарии: — строки 81–91
- Пример запроса: — строки 93–94
- Пример успешного ответа (200): — строки 96–104
- Негативные сценарии: — строки 106–113
- Пример запроса: — строки 115–116
- Пример успешного ответа (200): — строки 118–128
- Негативные сценарии: — строки 130–136
- Resources — строки 138–140
- SubsystemView — строки 142–146
- TaskViewTemplate — строки 148–150
- UserViews — строки 152–156

## Components
- `GET /Components` — Возвращает полный список компонентов · коды: 200, 204, 206 · примеры
  → map<ResultsBaseComponentResult>

## Filters
- `GET /Filters` — Получение списка избранных фильтров пользователя · коды: 200, 204, 206 · примеры
  ← query: applicationID?:int, resource?:str, applicationID?:int, resource?:str → EntitiesUIUserFilterFavouriteEntity[]

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
- `GET /LayoutTemplates/{id}` — Получить конкретное представление · коды: 200, 404 · примеры
  ← path: id:int → ApiDtoLayoutTemplateDto
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
- `GET /LayoutTemplates/{id}/taskTypes` — Получить список типов задач представления · коды: 200, 204, 404 · примеры
  ← path: id:int → ApiDtoLayoutTaskTypeDto[]

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
