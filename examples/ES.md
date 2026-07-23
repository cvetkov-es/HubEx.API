# ES — примеры

> **Что здесь:** блоки примеров запросов/ответов ручек сервиса ES, вынесенные из `endpoints/ES.md`. Сигнатуры и типы — там же и в `schemas/ES.md`.

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
