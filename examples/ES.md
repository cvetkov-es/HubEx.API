# ES — примеры

> **Что здесь:** блоки примеров запросов/ответов ручек сервиса ES, вынесенные из `endpoints/ES.md`. Сигнатуры и типы — там же и в `schemas/ES.md`.

## AssetAttributes

### `POST /AssetAttributes`

## Пример запроса:
`POST /AssetAttributes`
            
```json
[
  {
    "assetID": 101,
    "data": [
      {
        "attributeID": 2,
        "value": "Значение атрибута",
        "isPublic": true,
        "sortOrder": 1
      }
    ]
  }
]
```
            
## Пример успешного ответа (202):
Пустое тело ответа.
            
## Негативные сценарии:
- 400 BadRequest: некорректный формат запроса или отсутствуют обязательные поля.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `AssetAttributeMerge`.

### `DELETE /AssetAttributes`

## Пример запроса:
`DELETE /AssetAttributes`
            
```json
[
  {
    "assetID": 101,
    "data": [
      {
        "attributeID": 2
      }
    ]
  }
]
```
            
## Пример успешного ответа (202):
```json
[
  {
    "tenantID": 105,
    "assetID": 101,
    "attributeID": 2,
    "error": "InvalidDataFormat@AlreadyActive"
  }
]
```
Пустой массив — если все строки запроса обработаны успешно.
            
## Негативные сценарии:
- 400 BadRequest: некорректный формат запроса или отсутствуют обязательные поля.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `AssetAttributeDelete`.
            
Удаляются только явно переданные пары AssetID+AttributeID.
Непереданные атрибуты объекта не затрагиваются.

### `POST /AssetAttributes/v2`

## Пример запроса:
`POST /AssetAttributes/v2`
            
```json
[
  {
    "assetID": 101,
    "data": [
      {
        "attributeID": 2,
        "value": "Новый атрибут",
        "isPublic": true,
        "sortOrder": 1
      }
    ]
  }
]
```
            
## Пример успешного ответа (202):
```json
[
  {
    "tenantID": 105,
    "assetID": 101,
    "attributeID": 2,
    "error": "InvalidDataFormat@AlreadyActive"
  }
]
```
Пустой массив — если все строки запроса обработаны успешно.
            
## Негативные сценарии:
- 400 BadRequest: некорректный формат запроса или отсутствуют обязательные поля.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `AssetAttributeAdd`.
            
Добавляются только явно переданные атрибуты.
Пустое значение не создает запись значения атрибута.
При отсутствии `SortOrder` значение по умолчанию обрабатывается на стороне backend.

### `PUT /AssetAttributes/v2`

## Пример запроса:
`PUT /AssetAttributes/v2`
            
```json
[
  {
    "assetID": 101,
    "data": [
      {
        "attributeID": 2,
        "value": "Обновленное значение",
        "isPublic": false
      }
    ]
  }
]
```
            
## Пример успешного ответа (202):
```json
[
  {
    "tenantID": 105,
    "assetID": 101,
    "attributeID": 2,
    "error": "InvalidDataFormat@AlreadyActive"
  }
]
```
Пустой массив — если все строки запроса обработаны успешно.
            
## Негативные сценарии:
- 400 BadRequest: некорректный формат запроса или отсутствуют обязательные поля.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `AssetAttributeUpdate`.
            
Обновляются только явно переданные атрибуты.
Если для атрибута передать пустое значение, его значение будет удалено.
При отсутствии `SortOrder` значение по умолчанию обрабатывается на стороне backend.

## AssetSearchSettings

### `GET /AssetSearchSettings`

## Пример запроса:
`GET /AssetSearchSettings`
            
## Пример успешного ответа (200), пользователь ещё не сохранял выбор:
```json
[
  {
    "searchFieldID": 1,
    "entityCode": "Asset",
    "fieldCode": "Name",
    "descriptionRu": "Название",
    "isSelected": true,
    "isSelectedByUser": false
  },
  {
    "searchFieldID": 2,
    "entityCode": "Asset",
    "fieldCode": "SerialNumber",
    "descriptionRu": "Серийный номер",
    "isSelected": true,
    "isSelectedByUser": false
  }
]
```
## Пример ответа после сохранения выбора (только SerialNumber):
```json
[
  {
    "searchFieldID": 1,
    "entityCode": "Asset",
    "fieldCode": "Name",
    "descriptionRu": "Название",
    "isSelected": false,
    "isSelectedByUser": false
  },
  {
    "searchFieldID": 2,
    "entityCode": "Asset",
    "fieldCode": "SerialNumber",
    "descriptionRu": "Серийный номер",
    "isSelected": true,
    "isSelectedByUser": true
  }
]
```
`fieldCode` — технический код поля; `descriptionRu` — подпись для UI.
`isSelected` — итоговое состояние чекбокса (при отсутствии сохранённых настроек все доступные поля `true`).
`isSelectedByUser` — поле сохранено в `TenantMemberSearchField`; при первом сохранении у всех строк `false` — отправлять `POST /tenantMember` с отмеченными id.
## Негативные сценарии:
- 204 NoContent: для пользователя нет доступных полей поиска.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `AssetSearchFieldListForTenantMember`.

### `POST /AssetSearchSettings/tenant`

## Пример запроса:
`POST /AssetSearchSettings/tenant`
            
```json
[1,2,3]
```
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `AssetTenantSearchSettingsAdd`.

### `DELETE /AssetSearchSettings/tenant`

## Пример запроса:
`DELETE /AssetSearchSettings/tenant`
            
```json
[2,3]
```
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `AssetTenantSearchSettingsDelete`.

### `POST /AssetSearchSettings/tenantMember`

## Пример запроса:
`POST /AssetSearchSettings/tenantMember`
            
```json
[1,2]
```
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `AssetTenantMemberSearchSettingsAdd`.
- 409 Conflict: поле поиска скрыто для компании (`SearchFieldNotAllowedForTenant`).

### `DELETE /AssetSearchSettings/tenantMember`

## Пример запроса:
`DELETE /AssetSearchSettings/tenantMember`
            
```json
[2]
```
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `AssetTenantMemberSearchSettingsDelete`.
- 409 Conflict: поле поиска скрыто для компании (`SearchFieldNotAllowedForTenant`).
