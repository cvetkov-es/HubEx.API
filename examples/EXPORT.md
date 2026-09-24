# EXPORT — примеры

> **Что здесь:** блоки примеров запросов/ответов ручек сервиса EXPORT, вынесенные из `endpoints/EXPORT.md`. Сигнатуры и типы — там же и в `schemas/EXPORT.md`.

## Assets

### `GET /Assets`

## Пример запроса:
`GET /Assets?searchText=Насос&noData=false`
            
## Пример успешного ответа (200):
Content-Type: `application/vnd.openxmlformats-officedocument.spreadsheetml.sheet`
            
Тело ответа — Excel-файл (.xlsx) с листом «Объекты и оборудование».
В заголовке ответа присутствует `Content-Disposition: attachment`.
            
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `AssetsExport`.

### `GET /Assets/extended`

## Пример запроса:
`GET /Assets/extended?include=Name&include=000001&searchText=Насос`
            
## Пример успешного ответа (200):
Content-Type: `application/vnd.openxmlformats-officedocument.spreadsheetml.sheet`
            
Тело ответа — Excel-файл (.xlsx) с выбранными столбцами объектов и атрибутов.
В заголовке ответа присутствует `Content-Disposition: attachment`.
            
## Негативные сценарии:
- 500 Internal Server Error: не указан ни один столбец для экспорта (`include`).
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `AssetsExport`.

### `GET /Assets/extended/includes`

## Пример запроса:
`GET /Assets/extended/includes?searchText=Название`
            
## Пример успешного ответа (200):
```json
[
  { "code": "Name", "description": "Название" },
  { "code": "000001", "description": "Атрибут объекта" }
]
```
            
## Пример успешного ответа (206):
Тело ответа имеет тот же формат, что и для `200`, но содержит частичный диапазон.
В заголовке ответа присутствует `Content-Range`.
            
## Негативные сценарии:
- 204 NoContent: по заданным фильтрам поля не найдены.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `AssetsExport`.

## Companies

### `GET /Companies`

## Пример запроса:
`GET /Companies?searchText=HubEx&noData=false`
            
## Пример успешного ответа (200):
Content-Type: `application/vnd.openxmlformats-officedocument.spreadsheetml.sheet`
            
Тело ответа — Excel-файл (.xlsx) с листом «Компании».
В заголовке ответа присутствует `Content-Disposition: attachment`.
            
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `CompaniesExport`.

## MaterialConsumption

### `GET /MaterialConsumption`

## Пример запроса:
`GET /MaterialConsumption?searchText=Болт&consumptionPeriodFrom=2026-01-01&consumptionPeriodTill=2026-01-31`
            
## Пример успешного ответа (200):
Content-Type: `application/vnd.openxmlformats-officedocument.spreadsheetml.sheet`
            
Тело ответа — Excel-файл (.xlsx) с листом «Расход материалов».
В заголовке ответа присутствует `Content-Disposition: attachment`.
            
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `MaterialConsumptionList`.

## Materials

### `GET /Materials`

## Пример запроса:
`GET /Materials?searchText=Болт&warehouseID=1&noData=false`
            
## Пример успешного ответа (200):
Content-Type: `application/vnd.openxmlformats-officedocument.spreadsheetml.sheet`
            
Тело ответа — Excel-файл (.xlsx) с листом «Материалы».
В заголовке ответа присутствует `Content-Disposition: attachment`.
            
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `MaterialList`.

### `GET /Materials/v2.0`

## Пример запроса:
`GET /Materials/v2.0?searchText=Болт&warehouseID=1&noData=false`
            
## Пример успешного ответа (200):
Content-Type: `application/vnd.openxmlformats-officedocument.spreadsheetml.sheet`
            
Тело ответа — Excel-файл (.xlsx) с листом «Материалы».
Данные загружаются постранично (до 2000 записей за запрос).
В заголовке ответа присутствует `Content-Disposition: attachment`.
            
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `MaterialList`.

## Tasks

### `GET /Tasks`

## Пример запроса:
`GET /Tasks?searchText=Насос`
            
## Пример успешного ответа (200):
Content-Type: `application/vnd.openxmlformats-officedocument.spreadsheetml.sheet`
            
Тело ответа — Excel-файл (.xlsx) с листом «Заявки».
В заголовке ответа присутствует `Content-Disposition: attachment`.
            
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `TasksExport`.

### `GET /Tasks/extended`

## Пример запроса:
`GET /Tasks/extended?include=TaskNumber&include=000001&searchText=Насос`
            
## Пример успешного ответа (200):
Content-Type: `application/vnd.openxmlformats-officedocument.spreadsheetml.sheet`
            
Тело ответа — Excel-файл (.xlsx) с выбранными столбцами заявок, атрибутов и дополнительных листов.
В заголовке ответа присутствует `Content-Disposition: attachment`.
            
## Негативные сценарии:
- 500 Internal Server Error: не указан ни один столбец для экспорта (`include`).
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `TasksExport`.

### `GET /Tasks/extended/V2`

## Пример запроса:
`GET /Tasks/extended/V2?include=TaskNumber&include=000001&searchText=Насос`
            
## Пример успешного ответа (200):
Content-Type: `application/vnd.openxmlformats-officedocument.spreadsheetml.sheet`
            
Тело ответа — Excel-файл (.xlsx) с выбранными столбцами заявок, атрибутов и дополнительных листов.
Данные загружаются постранично (до 2000 записей за запрос).
В заголовке ответа присутствует `Content-Disposition: attachment`.
            
## Негативные сценарии:
- 500 Internal Server Error: не указан ни один столбец для экспорта (`include`).
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `TasksExport`.

### `GET /Tasks/extended/includes`

## Пример запроса:
`GET /Tasks/extended/includes?searchText=Номер`
            
## Пример успешного ответа (200):
```json
[
  { "code": "TaskNumber", "description": "Номер заявки" },
  { "code": "CompletedWorks", "description": "Выполненные работы" },
  { "code": "000001", "description": "Атрибут заявки" }
]
```
            
## Пример успешного ответа (206):
Тело ответа имеет тот же формат, что и для `200`, но содержит частичный диапазон.
В заголовке ответа присутствует `Content-Range`.
            
## Негативные сценарии:
- 204 NoContent: по заданным фильтрам поля не найдены.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `TasksExport`.

### `GET /Tasks/noData`

## Пример запроса:
`GET /Tasks/noData`
            
## Пример успешного ответа (200):
Content-Type: `application/vnd.openxmlformats-officedocument.spreadsheetml.sheet`
            
Тело ответа — Excel-файл (.xlsx) с пустым шаблоном для импорта заявок (лист «Заявки») и справочниками.
В заголовке ответа присутствует `Content-Disposition: attachment`.
            
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `TasksExport`.

### `GET /Tasks/v2.0`

## Пример запроса:
`GET /Tasks/v2.0?searchText=Насос`
            
## Пример успешного ответа (200):
Content-Type: `application/vnd.openxmlformats-officedocument.spreadsheetml.sheet`
            
Тело ответа — Excel-файл (.xlsx) с листом «Заявки».
Данные загружаются постранично (до 2000 записей за запрос).
В заголовке ответа присутствует `Content-Disposition: attachment`.
            
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `TasksExport`.

## Users

### `GET /Users`

## Пример запроса:
`GET /Users?searchText=Иванов&noData=false`
            
## Пример успешного ответа (200):
Content-Type: `application/vnd.openxmlformats-officedocument.spreadsheetml.sheet`
            
Тело ответа — Excel-файл (.xlsx) с листом «Пользователи».
В заголовке ответа присутствует `Content-Disposition: attachment`.
            
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `UsersExport`.
