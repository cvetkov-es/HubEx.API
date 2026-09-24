# IMPORT — примеры

> **Что здесь:** блоки примеров запросов/ответов ручек сервиса IMPORT, вынесенные из `endpoints/IMPORT.md`. Сигнатуры и типы — там же и в `schemas/IMPORT.md`.

## Assets

### `POST /Assets`

## Пример запроса:
`POST /Assets`
            
Content-Type: `multipart/form-data`
            
Поле формы: `File` — Excel-файл (.xlsx) с листом, имя которого зависит от `Accept-Language`
(ru: `Объекты и оборудование`, en: `Assets`).
            
## Пример успешного ответа (202):
Тело ответа отсутствует. Импорт объектов принят в обработку.
            
## Пример ошибки валидации файла (409):
Возвращается Excel-файл с теми же данными и комментариями в ячейках с ошибками.
В заголовке ответа присутствует `X-Application-Errors: InvalidData`.
            
## Пример ошибки (409):
```json
[
  {
    "traceIdentifier": "00-abc123",
    "code": "InvalidData",
    "message": "Загружен неверный файл"
  }
]
```
## Негативные сценарии:
- 409 Conflict: в файле есть ошибки валидации строк/ячеек — возвращается Excel с комментариями
  (`Content-Type: application/vnd.openxmlformats-officedocument.spreadsheetml.sheet`,
  заголовок `X-Application-Errors: InvalidData`).
- 409 Conflict: отсутствует лист с ожидаемым именем (`WrongFile`) или лист пустой (`EmptyFile`).
  Имя листа зависит от `Accept-Language` (ru: `Объекты и оборудование`, en: `Assets`).
- 409 Conflict: файл создан в неподдерживаемом приложении (например, MyOffice) — `UnsupportedFileFormat`.
- Отсутствует обязательное поле формы `File` или тело запроса некорректно —
  обрабатывается model binding / global exception handling (не 409 Conflict).
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `AssetsImport`.

## Companies

### `POST /Companies`

## Пример запроса:
`POST /Companies`
            
Content-Type: `multipart/form-data`
            
Поле формы: `File` — Excel-файл (.xlsx) с листом, имя которого зависит от `Accept-Language`
(ru: `Компании`, en: `Companies`).
            
## Пример успешного ответа (202):
Тело ответа отсутствует. Импорт компаний принят в обработку.
            
## Пример ошибки валидации файла (409):
Возвращается Excel-файл с теми же данными и комментариями в ячейках с ошибками.
В заголовке ответа присутствует `X-Application-Errors: InvalidData`.
            
## Пример ошибки (409):
```json
[
  {
    "traceIdentifier": "00-abc123",
    "code": "InvalidData",
    "message": "Загружен неверный файл"
  }
]
```
## Негативные сценарии:
- 409 Conflict: в файле есть ошибки валидации строк/ячеек — возвращается Excel с комментариями
  (`Content-Type: application/vnd.openxmlformats-officedocument.spreadsheetml.sheet`,
  заголовок `X-Application-Errors: InvalidData`).
- 409 Conflict: отсутствует лист с ожидаемым именем (`WrongFile`) или лист пустой (`EmptyFile`).
  Имя листа зависит от `Accept-Language` (ru: `Компании`, en: `Companies`).
- 409 Conflict: файл создан в неподдерживаемом приложении (например, MyOffice) — `UnsupportedFileFormat`.
- Отсутствует обязательное поле формы `File` или тело запроса некорректно —
  обрабатывается model binding / global exception handling (не 409 Conflict).
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `CompaniesImport`.

## Materials

### `POST /Materials`

## Пример запроса:
`POST /Materials`
            
Content-Type: `multipart/form-data`
            
Поле формы: `File` — Excel-файл (.xlsx) с листом, имя которого зависит от `Accept-Language`
(ru: `Материалы`, en: `Materials`).
            
## Пример успешного ответа (202):
Тело ответа отсутствует. Импорт материалов принят в обработку.
            
## Пример ошибки валидации файла (409):
Возвращается Excel-файл с теми же данными и комментариями в ячейках с ошибками.
В заголовке ответа присутствует `X-Application-Errors: InvalidData`.
            
## Пример ошибки (409):
```json
[
  {
    "traceIdentifier": "00-abc123",
    "code": "InvalidData",
    "message": "Загружен неверный файл"
  }
]
```
## Негативные сценарии:
- 409 Conflict: в файле есть ошибки валидации строк/ячеек — возвращается Excel с комментариями
  (`Content-Type: application/vnd.openxmlformats-officedocument.spreadsheetml.sheet`,
  заголовок `X-Application-Errors: InvalidData`).
- 409 Conflict: отсутствует лист с ожидаемым именем (`WrongFile`) или лист пустой (`EmptyFile`).
  Имя листа зависит от `Accept-Language` (ru: `Материалы`, en: `Materials`).
- 409 Conflict: файл создан в неподдерживаемом приложении (например, MyOffice) — `UnsupportedFileFormat`.
- Отсутствует обязательное поле формы `File` или тело запроса некорректно —
  обрабатывается model binding / global exception handling (не 409 Conflict).
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `MaterialImport`.

### `POST /Materials/v2.0`

## Пример запроса:
`POST /Materials/v2.0`
            
Content-Type: `multipart/form-data`
            
Поле формы: `File` — Excel-файл (.xlsx) с листом, имя которого зависит от `Accept-Language`
(ru: `Материалы`, en: `Materials`).
            
Перед записью строки группируются по `MaterialErpID` (для каждого ERP ID сохраняется последняя запись).
            
## Пример успешного ответа (202):
Тело ответа отсутствует. Импорт материалов принят в обработку.
            
## Пример ошибки валидации файла (409):
Возвращается Excel-файл с теми же данными и комментариями в ячейках с ошибками.
В заголовке ответа присутствует `X-Application-Errors: InvalidData`.
            
## Пример ошибки (409):
```json
[
  {
    "traceIdentifier": "00-abc123",
    "code": "InvalidData",
    "message": "Загружен неверный файл"
  }
]
```
## Негативные сценарии:
- 409 Conflict: в файле есть ошибки валидации строк/ячеек — возвращается Excel с комментариями
  (`Content-Type: application/vnd.openxmlformats-officedocument.spreadsheetml.sheet`,
  заголовок `X-Application-Errors: InvalidData`).
- 409 Conflict: отсутствует лист с ожидаемым именем (`WrongFile`) или лист пустой (`EmptyFile`).
  Имя листа зависит от `Accept-Language` (ru: `Материалы`, en: `Materials`).
- 409 Conflict: файл создан в неподдерживаемом приложении (например, MyOffice) — `UnsupportedFileFormat`.
- Отсутствует обязательное поле формы `File` или тело запроса некорректно —
  обрабатывается model binding / global exception handling (не 409 Conflict).
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `MaterialImport`.

## Tasks

### `POST /Tasks`

## Пример запроса:
`POST /Tasks`
            
Content-Type: `multipart/form-data`
            
Поле формы: `File` — Excel-файл (.xlsx) с листом, имя которого зависит от `Accept-Language`
(ru: `Заявки`, en: `Tasks`).
            
## Пример успешного ответа (202):
Тело ответа отсутствует. Импорт заявок принят в обработку.
После импорта асинхронно отправляются уведомления и запросы на перевод по стадиям.
            
## Пример ошибки валидации файла (409):
Возвращается Excel-файл с теми же данными и комментариями в ячейках с ошибками.
В заголовке ответа присутствует `X-Application-Errors: InvalidData`.
            
## Пример ошибки (409):
```json
[
  {
    "traceIdentifier": "00-abc123",
    "code": "InvalidData",
    "message": "Загружен неверный файл"
  }
]
```
## Негативные сценарии:
- 409 Conflict: в файле есть ошибки валидации строк/ячеек — возвращается Excel с комментариями
  (`Content-Type: application/vnd.openxmlformats-officedocument.spreadsheetml.sheet`,
  заголовок `X-Application-Errors: InvalidData`).
- 409 Conflict: отсутствует лист с ожидаемым именем (`WrongFile`) или лист пустой (`EmptyFile`).
  Имя листа зависит от `Accept-Language` (ru: `Заявки`, en: `Tasks`).
- 409 Conflict: файл создан в неподдерживаемом приложении (например, MyOffice) — `UnsupportedFileFormat`.
- Отсутствует обязательное поле формы `File` или тело запроса некорректно —
  обрабатывается model binding / global exception handling (не 409 Conflict).
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `TaskImport`.

## Users

### `POST /Users`

## Пример запроса:
`POST /Users`
            
Content-Type: `multipart/form-data`
            
Поле формы: `File` — Excel-файл (.xlsx) с листом, имя которого зависит от `Accept-Language`
(ru: `Пользователи`, en: `Users`).
            
## Пример успешного ответа (202):
Тело ответа отсутствует. Импорт пользователей принят в обработку.
После импорта отправляются приглашения на верификацию аккаунта.
            
## Пример ошибки валидации файла (409):
Возвращается Excel-файл с теми же данными и комментариями в ячейках с ошибками.
В заголовке ответа присутствует `X-Application-Errors: InvalidData`.
            
## Пример ошибки (409):
```json
[
  {
    "traceIdentifier": "00-abc123",
    "code": "InvalidData",
    "message": "Загружен неверный файл"
  }
]
```
## Негативные сценарии:
- 409 Conflict: в файле есть ошибки валидации строк/ячеек — возвращается Excel с комментариями
  (`Content-Type: application/vnd.openxmlformats-officedocument.spreadsheetml.sheet`,
  заголовок `X-Application-Errors: InvalidData`).
- 409 Conflict: отсутствует лист с ожидаемым именем (`WrongFile`) или лист пустой (`EmptyFile`).
  Имя листа зависит от `Accept-Language` (ru: `Пользователи`, en: `Users`).
- 409 Conflict: файл создан в неподдерживаемом приложении (например, MyOffice) — `UnsupportedFileFormat`.
- Отсутствует обязательное поле формы `File` или тело запроса некорректно —
  обрабатывается model binding / global exception handling (не 409 Conflict).
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `UserImport`.
