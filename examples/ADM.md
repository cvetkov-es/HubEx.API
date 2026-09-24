# ADM — примеры

> **Что здесь:** блоки примеров запросов/ответов ручек сервиса ADM, вынесенные из `endpoints/ADM.md`. Сигнатуры и типы — там же и в `schemas/ADM.md`.

## BanReasons

### `GET /BanReasons`

## Пример запроса:

GET /banreasons

## Пример успешного ответа:
```json
{
  "1": {
    "code": "VIOLATION",
    "name": "Нарушение правил",
    "description": "Пользователь нарушил правила использования системы"
  },
  "2": {
    "code": "INACTIVITY",
    "name": "Неактивность",
    "description": "Длительное отсутствие активности"
  }
}
```
            
## Пример успешного ответа (206):
Тело ответа имеет тот же формат, что и для `200`, но содержит частичный диапазон.
## Негативные сценарии:
- 204 NoContent: причины не найдены.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `BanReasonsList`.

## Capabilities

### `GET /Capabilities`

## Пример запроса:

GET /capabilities

## Пример успешного ответа:
```json
{
  "1": {
    "code": "CAPABILITY_1",
    "name": "Возможность 1",
    "weightCoefficient": 1
  },
  "2": {
    "code": "CAPABILITY_2",
    "name": "Возможность 2",
    "weightCoefficient": 2
  }
}
```
            
## Пример успешного ответа (206):
Тело ответа имеет тот же формат, что и для `200`, но содержит частичный диапазон.
## Негативные сценарии:
- 204 NoContent: возможности не найдены.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `CapabilitiesList`.

## DefaultPages

### `GET /DefaultPages`

## Пример запроса:
            
GET /defaultpages?applicationID=3
            
## Пример успешного ответа:
```json
[
  {
    "tenantID": 1,
    "code": "dashboard",
    "version": null,
    "nameRu": "Рабочий стол",
    "resourceID": null,
    "resourceNameRu": null
  },
  {
    "tenantID": 1,
    "code": "custom.package.code",
    "version": "1.0.0",
    "nameRu": "Пакетная стартовая страница",
    "resourceID": 16,
    "resourceNameRu": "Портал"
  }
]
```
            
## Негативные сценарии:
- 204 NoContent: нет доступных страниц.
- 400 BadRequest: некорректный query-параметр `applicationID`.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `DefaultPagesList`.

## GeolocationSettings

### `GET /GeolocationSettings/coordinateAccuracy`

## Пример запроса:

GET /geolocationsettings/coordinateAccuracy

## Пример успешного ответа:
```json
[
  {
    "id": 1,
    "nameRu": "Высокая точность",
    "descriptionRu": "Точность до 5 метров"
  },
  {
    "id": 2,
    "nameRu": "Средняя точность",
    "descriptionRu": "Точность до 50 метров"
  }
]
```
            
## Негативные сценарии:
- 204 NoContent: настройки не найдены.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `CoordinateAccuracyList`.

## Invitations

### `GET /Invitations`

## Пример запроса:

GET /invitations?userTemplateID=1&userTemplateID=2

## Пример успешного ответа:
```json
{
  "123e4567-e89b-12d3-a456-426614174000": {
    "id": "123e4567-e89b-12d3-a456-426614174000",
    "description": "Приглашение для нового сотрудника",
    "validTill": "2025-12-31T23:59:59Z"
  },
  "223e4567-e89b-12d3-a456-426614174001": {
    "id": "223e4567-e89b-12d3-a456-426614174001",
    "description": "Приглашение для менеджера",
    "validTill": "2025-12-31T23:59:59Z"
  }
}
```
            
## Пример успешного ответа (206):
Тело ответа имеет тот же формат, что и для `200`, но содержит частичный диапазон.
## Негативные сценарии:
- 204 NoContent: приглашения не найдены.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `InvitationGet`.

### `POST /Invitations`

## Пример запроса:

POST /invitations

```json
[
  {
    "userTemplateID": 1,
    "description": "Приглашение для нового сотрудника",
    "isPublic": true,
    "isForSupport": false,
    "allowSelfRegistration": true,
    "requiredSelfRegistration": false,
    "validFrom": "2025-01-01T00:00:00Z",
    "validTill": "2025-12-31T23:59:59Z",
    "allowRegisterWithoutVerification": false
  }
]
```

## Пример успешного ответа:
```json
[
  {
    "id": "123e4567-e89b-12d3-a456-426614174000",
    "tenantID": 1
  }
]
```
            
## Негативные сценарии:
- 400 BadRequest: неверные данные тела запроса.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `InvitationAdd`.

### `PUT /Invitations`

## Пример запроса:

PUT /invitations

```json
[
  {
    "id": "123e4567-e89b-12d3-a456-426614174000",
    "description": "Обновленное описание приглашения",
    "isPublic": true,
    "isForSupport": false,
    "allowSelfRegistration": true,
    "requiredSelfRegistration": false,
    "validFrom": "2025-01-01T00:00:00Z",
    "validTill": "2026-12-31T23:59:59Z",
    "allowRegisterWithoutVerification": false
  }
]
```

## Пример успешного ответа:

HTTP 202 Accepted
            
## Негативные сценарии:
- 400 BadRequest: неверные данные тела запроса.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `InvitationUpdate`.

### `DELETE /Invitations`

## Пример запроса:

DELETE /invitations

```json
[
  "123e4567-e89b-12d3-a456-426614174000",
  "223e4567-e89b-12d3-a456-426614174001"
]
```

## Пример успешного ответа:

HTTP 202 Accepted
            
## Негативные сценарии:
- 400 BadRequest: неверные данные тела запроса.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `InvitationDelete`.

### `GET /Invitations/{id}`

## Пример запроса:

GET /invitations/123e4567-e89b-12d3-a456-426614174000

## Пример успешного ответа:
```json
{
  "id": "123e4567-e89b-12d3-a456-426614174000",
  "pinCode": "123456",
  "description": "Приглашение для нового сотрудника",
  "isPublic": true,
  "isForSupport": false,
  "allowSelfRegistration": true,
  "requiredSelfRegistration": false,
  "validFrom": "2025-01-01T00:00:00Z",
  "validTill": "2025-12-31T23:59:59Z",
  "allowRegisterWithoutVerification": false,
  "userTemplate": {
    "id": 1,
    "name": "Шаблон инженера"
  }
}
```
            
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `InvitationGet`.

### `DELETE /Invitations/{id}`

## Пример запроса:

DELETE /invitations/123e4567-e89b-12d3-a456-426614174000

## Пример успешного ответа:

HTTP 202 Accepted
            
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `InvitationDelete`.

### `GET /Invitations/{id}/short`

## Пример запроса:

GET /invitations/123e4567-e89b-12d3-a456-426614174000/short

## Пример успешного ответа:
```json
{
  "id": "123e4567-e89b-12d3-a456-426614174000",
  "description": "Приглашение для нового сотрудника",
  "isPublic": true,
  "allowSelfRegistration": true,
  "requiredSelfRegistration": false,
  "validFrom": "2025-01-01T00:00:00Z",
  "validTill": "2025-12-31T23:59:59Z",
  "allowRegisterWithoutVerification": false,
  "tenant": {
    "id": 1,
    "name": "Компания"
  }
}
```

Этот метод доступен без аутентификации.

## PermissionApiTags

### `GET /PermissionApiTags`

## Пример запроса:

GET /permissionapitags

## Пример успешного ответа:
```json
{
  "1": [
    {
      "permissionApiID": 10,
      "code": "TAG_1",
      "description": "Тег 1"
    },
    {
      "permissionApiID": 11,
      "code": "TAG_2",
      "description": "Тег 2"
    }
  ]
}
```
            
## Пример успешного ответа (206):
Тело ответа имеет тот же формат, что и для `200`, но содержит частичный диапазон.
## Негативные сценарии:
- 204 NoContent: теги не найдены.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `PermissionApiTagList`.

## PermissionExtTags

### `GET /PermissionExtTags`

## Пример запроса:

GET /permissionexttags

## Пример успешного ответа:
```json
{
  "1": [
    {
      "permissionExtID": 10,
      "code": "TAG_1",
      "description": "Тег 1"
    },
    {
      "permissionExtID": 11,
      "code": "TAG_2",
      "description": "Тег 2"
    }
  ]
}
```
            
## Пример успешного ответа (206):
Тело ответа имеет тот же формат, что и для `200`, но содержит частичный диапазон.
## Негативные сценарии:
- 204 NoContent: теги не найдены.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `PermissionExtTagList`.

## PermissionsApi

### `GET /PermissionsApi`

## Пример запроса:

GET /permissionsapi

## Пример успешного ответа:
```json
{
  "1": {
    "code": "USER_GET",
    "description": "Получение информации о пользователе"
  },
  "2": {
    "code": "USER_ADD",
    "description": "Добавление пользователя"
  }
}
```
            
## Пример успешного ответа (206):
Тело ответа имеет тот же формат, что и для `200`, но содержит частичный диапазон.
## Негативные сценарии:
- 204 NoContent: полномочия не найдены.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `PermissionsApiList`.

## PermissionsExt

### `GET /PermissionsExt`

## Пример запроса:

GET /permissionsext

## Пример успешного ответа:
```json
{
  "1": {
    "code": "EXT_FEATURE_1",
    "description": "Расширенное полномочие 1"
  },
  "2": {
    "code": "EXT_FEATURE_2",
    "description": "Расширенное полномочие 2"
  }
}
```
            
## Пример успешного ответа (206):
Тело ответа имеет тот же формат, что и для `200`, но содержит частичный диапазон.
## Негативные сценарии:
- 204 NoContent: полномочия не найдены.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `PermissionsExtList`.

## PermissionsUi

### `GET /PermissionsUi`

## Пример запроса:

GET /permissionsui

## Пример успешного ответа:
```json
{
  "1": {
    "code": "UI_FEATURE_1",
    "description": "UI полномочие 1",
    "isSystem": false
  },
  "2": {
    "code": "UI_FEATURE_2",
    "description": "UI полномочие 2",
    "isSystem": true
  }
}
```

Возвращает только неудаленные полномочия.
            
## Пример успешного ответа (206):
Тело ответа имеет тот же формат, что и для `200`, но содержит частичный диапазон.
## Негативные сценарии:
- 204 NoContent: полномочия не найдены.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `PermissionUiList`.

### `POST /PermissionsUi`

## Пример запроса:

POST /permissionsui

```json
[
  {
    "code": "UI_NEW_FEATURE",
    "description": "Новое UI полномочие",
    "mustBeAssignedToRole": true
  }
]
```

## Пример успешного ответа:
```json
[1]
```
            
## Негативные сценарии:
- 400 BadRequest: неверные данные тела запроса.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `PermissionUiAdd`.

### `PUT /PermissionsUi`

## Пример запроса:

PUT /permissionsui

```json
[
  {
    "id": 1,
    "description": "Обновленное описание",
    "mustBeAssignedToRole": false
  }
]
```

## Пример успешного ответа:

HTTP 202 Accepted
            
## Негативные сценарии:
- 400 BadRequest: неверные данные тела запроса.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `PermissionUiUpdate`.

### `DELETE /PermissionsUi`

## Пример запроса:

DELETE /permissionsui

```json
[1, 2, 3]
```

## Пример успешного ответа:

HTTP 202 Accepted
            
## Негативные сценарии:
- 400 BadRequest: неверные данные тела запроса.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `PermissionUiDelete`.

### `GET /PermissionsUi/{id}`

## Пример запроса:

GET /permissionsui/1

## Пример успешного ответа:
```json
{
  "code": "UI_FEATURE_1",
  "description": "UI полномочие 1",
  "isSystem": false,
  "mustBeAssignedToRole": true,
  "allowReadonlyOnly": false,
  "allowRewritableOnly": false,
  "deleted": null
}
```

Метод возвращает данные, включая помеченные как удаленные.
            
## Негативные сценарии:
- 204 NoContent: полномочие не найдено.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `PermissionUiGet`.

### `DELETE /PermissionsUi/{id}`

## Пример запроса:

DELETE /permissionsui/1

## Пример успешного ответа:

HTTP 202 Accepted
            
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `PermissionUiDelete`.

## RoleApplications

### `POST /RoleApplications`

## Пример запроса:

POST /roleapplications

```json
[
  {
    "roleID": 1,
    "data": [10, 11]
  }
]
```

## Пример успешного ответа:
```json
[
  {
    "tenantID": 1,
    "roleID": 1,
    "applicationID": 10
  },
  {
    "tenantID": 1,
    "roleID": 1,
    "applicationID": 11
  }
]
```
            
## Негативные сценарии:
- 400 BadRequest: неверные данные тела запроса.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `RoleApplicationMerge`.

### `DELETE /RoleApplications`

## Пример запроса:

DELETE /roleapplications

```json
[
  {
    "roleID": 1,
    "data": [10]
  }
]
```

## Пример успешного ответа:

HTTP 202 Accepted
            
## Негативные сценарии:
- 400 BadRequest: неверные данные тела запроса.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `RoleApplicationDelete`.

## RoleAttachments

### `POST /RoleAttachments`

## Пример запроса:

POST /roleattachments

```json
[
  {
    "roleID": 1,
    "attachmentID": 10
  },
  {
    "roleID": 1,
    "attachmentID": 11
  }
]
```

## Пример успешного ответа:
```json
[
  {
    "roleID": 1,
    "attachmentID": 10
  },
  {
    "roleID": 1,
    "attachmentID": 11
  }
]
```
            
## Негативные сценарии:
- 400 BadRequest: неверные данные тела запроса.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `RoleAttachmentAdd`.

### `DELETE /RoleAttachments`

## Пример запроса:

DELETE /roleattachments

```json
[
  {
    "roleID": 1,
    "attachmentID": 10
  }
]
```

## Пример успешного ответа:

HTTP 202 Accepted
            
## Негативные сценарии:
- 400 BadRequest: неверные данные тела запроса.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `RoleAttachmentDelete`.

## RolePermissionsApi

### `POST /RolePermissionsApi`

## Пример запроса:

POST /rolepermissionsapi

```json
[
  {
    "roleID": 1,
    "data": [10, 11]
  }
]
```

## Пример успешного ответа:
```json
[
  {
    "roleID": 1,
    "permissionApiID": 10
  },
  {
    "roleID": 1,
    "permissionApiID": 11
  }
]
```
            
## Негативные сценарии:
- 400 BadRequest: неверные данные тела запроса.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `RolePermissionApiAdd`.

### `DELETE /RolePermissionsApi`

## Пример запроса:

DELETE /rolepermissionsapi

```json
[
  {
    "roleID": 1,
    "data": [10]
  }
]
```

## Пример успешного ответа:

HTTP 202 Accepted
            
## Негативные сценарии:
- 400 BadRequest: неверные данные тела запроса.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `RolePermissionApiDelete`.

## RolePermissionsExt

### `POST /RolePermissionsExt`

## Пример запроса:

POST /rolepermissionsext

```json
[
  {
    "roleID": 1,
    "data": [10, 11]
  }
]
```

## Пример успешного ответа:
```json
[
  {
    "roleID": 1,
    "permissionExtID": 10
  },
  {
    "roleID": 1,
    "permissionExtID": 11
  }
]
```
            
## Негативные сценарии:
- 400 BadRequest: неверные данные тела запроса.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `RolePermissionExtAdd`.

### `DELETE /RolePermissionsExt`

## Пример запроса:

DELETE /rolepermissionsext

```json
[
  {
    "roleID": 1,
    "data": [10]
  }
]
```

## Пример успешного ответа:

HTTP 202 Accepted
            
## Негативные сценарии:
- 400 BadRequest: неверные данные тела запроса.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `RolePermissionExtDelete`.

## RolePermissionsUi

### `POST /RolePermissionsUi`

## Пример запроса:

POST /rolepermissionsui

```json
[
  {
    "roleID": 1,
    "capabilityID": 1,
    "data": [10, 11]
  }
]
```

## Пример успешного ответа:
```json
[
  {
    "roleID": 1,
    "permissionUiID": 10
  },
  {
    "roleID": 1,
    "permissionUiID": 11
  }
]
```
            
## Негативные сценарии:
- 400 BadRequest: неверные данные тела запроса.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `RolePermissionUiAdd`.

### `DELETE /RolePermissionsUi`

## Пример запроса:

DELETE /rolepermissionsui

```json
[
  {
    "roleID": 1,
    "capabilityID": 1,
    "data": [10]
  }
]
```

## Пример успешного ответа:

HTTP 202 Accepted
            
## Негативные сценарии:
- 400 BadRequest: неверные данные тела запроса.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `RolePermissionUiDelete`.

## RoleTaskListQueries

### `POST /RoleTaskListQueries`

## Пример запроса:

POST /roletasklistqueries

```json
[
  {
    "roleID": 1,
    "taskListQueryID": 10
  },
  {
    "roleID": 1,
    "taskListQueryID": 11
  }
]
```

## Пример успешного ответа:
```json
[
  {
    "roleID": 1,
    "taskListQueryID": 10
  },
  {
    "roleID": 1,
    "taskListQueryID": 11
  }
]
```
            
## Негативные сценарии:
- 400 BadRequest: неверные данные тела запроса.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `RoleTaskListQueryAdd`.

### `DELETE /RoleTaskListQueries`

## Пример запроса:

DELETE /roletasklistqueries

```json
[
  {
    "roleID": 1,
    "taskListQueryID": 10
  }
]
```

## Пример успешного ответа:

HTTP 202 Accepted
            
## Негативные сценарии:
- 400 BadRequest: неверные данные тела запроса.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `RoleTaskListQueryDelete`.

## RoleTaskPropertiesAccess

### `GET /RoleTaskPropertiesAccess/attributes`

## Пример запроса:

GET /roletaskpropertiesaccess/attributes?roleID=1&roleID=2

## Пример успешного ответа:
```json
[
  {
    "roleID": 1,
    "attributeID": 10,
    "isAccessable": true,
    "isDefault": false
  },
  {
    "roleID": 1,
    "attributeID": 11,
    "isAccessable": false,
    "isDefault": true
  }
]
```
            
## Пример успешного ответа (206):
Тело ответа имеет тот же формат, что и для `200`, но содержит частичный диапазон.
            
## Негативные сценарии:
- 204 NoContent: по заданным фильтрам записи не найдены.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `RoleTaskAttributeAccessList`.

### `POST /RoleTaskPropertiesAccess/attributes`

## Пример запроса:

POST /roletaskpropertiesaccess/attributes

```json
[
  {
    "roleID": 1,
    "attributeID": 10,
    "isAccessable": true
  }
]
```

## Пример успешного ответа:

HTTP 201 Created
            
## Негативные сценарии:
- 400 BadRequest: неверные данные тела запроса.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `RoleTaskAttributeAccessAdd`.

### `PUT /RoleTaskPropertiesAccess/attributes`

## Пример запроса:

PUT /roletaskpropertiesaccess/attributes

```json
[
  {
    "roleID": 1,
    "attributeID": 10,
    "isAccessable": false
  }
]
```

## Пример успешного ответа:

HTTP 202 Accepted
            
## Негативные сценарии:
- 400 BadRequest: неверные данные тела запроса.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `RoleTaskAttributeAccessUpdate`.

## Roles

### `GET /Roles`

## Пример запроса:

GET /roles?isDeleted=false

## Пример успешного ответа:
```json
[
  {
    "id": 1,
    "name": "Администратор",
    "description": "Роль администратора системы",
    "deleted": null,
    "systemRoles": [
      {
        "id": 1,
        "name": "Системный администратор"
      }
    ]
  },
  {
    "id": 2,
    "name": "Менеджер",
    "description": "Роль менеджера",
    "deleted": null,
    "systemRoles": []
  }
]
```
            
## Пример успешного ответа (206):
Тело ответа имеет тот же формат, что и для `200`, но содержит частичный диапазон.
## Негативные сценарии:
- 204 NoContent: роли не найдены.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `RoleList`.

### `POST /Roles`

## Пример запроса:

POST /roles

```json
[
  {
    "name": "Новая роль",
    "description": "Описание новой роли"
  }
]
```

## Пример успешного ответа:
```json
[1, 2]
```
            
## Негативные сценарии:
- 400 BadRequest: неверные данные тела запроса.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `RoleAdd`.

### `PUT /Roles`

## Пример запроса:

PUT /roles

```json
[
  {
    "id": 1,
    "name": "Обновленное название",
    "description": "Обновленное описание"
  }
]
```

## Пример успешного ответа:

HTTP 202 Accepted
            
## Негативные сценарии:
- 400 BadRequest: неверные данные тела запроса.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `RoleUpdate`.

### `DELETE /Roles`

## Пример запроса:

DELETE /roles

```json
[1, 2, 3]
```

## Пример успешного ответа:

HTTP 202 Accepted
            
## Негативные сценарии:
- 400 BadRequest: неверные данные тела запроса.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `RoleDelete`.

### `POST /Roles/copy`

## Пример запроса:

POST /roles/copy

```json
[
  {
    "copiedRoleID": 1,
    "name": "Копия роли администратора"
  }
]
```

## Пример успешного ответа:
```json
[3]
```
            
## Негативные сценарии:
- 400 BadRequest: неверные данные тела запроса.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `RoleAdd`.

### `GET /Roles/{id}`

## Пример запроса:

GET /roles/1

## Пример успешного ответа:
```json
{
  "id": 1,
  "name": "Администратор",
  "description": "Роль администратора системы",
  "deleted": null,
  "systemRoles": [
    {
      "id": 1,
      "name": "Системный администратор"
    }
  ]
}
```
            
## Негативные сценарии:
- 204 NoContent: роль не найдена или удалена.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `RoleGet`.

### `DELETE /Roles/{id}`

## Пример запроса:

DELETE /roles/1

## Пример успешного ответа:

HTTP 202 Accepted
            
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `RoleDelete`.

### `GET /Roles/{roleID}/applications`

## Пример запроса:

GET /roles/1/applications

## Пример успешного ответа:
```json
{
  "1": {
    "applicationCode": "WEB",
    "applicationName": "Веб-приложение"
  },
  "2": {
    "applicationCode": "MOBILE",
    "applicationName": "Мобильное приложение"
  }
}
```
            
## Пример успешного ответа (206):
Тело ответа имеет тот же формат, что и для `200`, но содержит частичный диапазон.
## Негативные сценарии:
- 204 NoContent: приложения не найдены.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `RoleApplicationList`.

### `GET /Roles/{roleID}/attachments`

## Пример запроса:

GET /roles/1/attachments

## Пример успешного ответа:
```json
[
  {
    "fileName": "document.pdf",
    "description": "Документация",
    "isUploaded": true,
    "publicUrl": "https://example.com/files/document.pdf",
    "contentType": "application/pdf"
  }
]
```
            
## Пример успешного ответа (206):
Тело ответа имеет тот же формат, что и для `200`, но содержит частичный диапазон.
## Негативные сценарии:
- 204 NoContent: файлы не найдены.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `RoleAttachmentsList`.

### `GET /Roles/{roleID}/packages`

## Пример запроса:

GET /roles/1/packages?searchText=модуль

## Пример успешного ответа:
```json
{
  "1": [
    {
      "packageID": "pkg-10",
      "packageVersion": "1.0.0",
      "packageName": "Модуль отчетности",
      "isEnabled": true,
      "resource": {
        "id": 1,
        "code": "WEB",
        "name": "Web интерфейс"
      }
    }
  ]
}
```
            
## Пример успешного ответа (206):
Тело ответа имеет тот же формат, что и для `200`, но содержит частичный диапазон.
## Негативные сценарии:
- 204 NoContent: расширения не найдены.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `RolePackageList`.

### `POST /Roles/{roleID}/packages`

## Пример запроса:

POST /roles/1/packages

```json
[
  {
    "packageID": "pkg-10",
    "packageVersion": "1.0.0",
    "isEnabled": true
  }
]
```

## Пример успешного ответа:
```json
[
  {
    "roleID": 1,
    "id": 5,
    "packageID": "pkg-10",
    "packageVersion": "1.0.0"
  }
]
```
            
## Негативные сценарии:
- 400 BadRequest: неверные данные тела запроса.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `RolePackageAdd`.

### `DELETE /Roles/{roleID}/packages`

## Пример запроса:

DELETE /roles/1/packages

```json
[1, 2, 3]
```

## Пример успешного ответа:

HTTP 202 Accepted
            
## Негативные сценарии:
- 400 BadRequest: неверные данные тела запроса.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `RolePackageDelete`.

### `PUT /Roles/{roleID}/packages/activate`

## Пример запроса:

PUT /roles/1/packages/activate

```json
[1, 2, 3]
```

## Пример успешного ответа:

HTTP 202 Accepted
            
## Негативные сценарии:
- 400 BadRequest: неверные данные тела запроса.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `RolePackageActivate`.

### `PUT /Roles/{roleID}/packages/deactivate`

## Пример запроса:

PUT /roles/1/packages/deactivate

```json
[1, 2, 3]
```

## Пример успешного ответа:

HTTP 202 Accepted
            
## Негативные сценарии:
- 400 BadRequest: неверные данные тела запроса.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `RolePackageDeactivate`.

### `GET /Roles/{roleID}/permissionsApi`

## Пример запроса:

GET /roles/1/permissionsApi?isCheckedPermission=true

## Пример успешного ответа:
```json
{
  "1": [
    {
      "permissionApiID": 1,
      "code": "USER_VIEW",
      "description": "Просмотр пользователей",
      "isChecked": true,
      "systemTag": {
        "id": 1,
        "name": "Управление пользователями"
      }
    }
  ]
}
```
            
## Пример успешного ответа (206):
Тело ответа имеет тот же формат, что и для `200`, но содержит частичный диапазон.
## Негативные сценарии:
- 204 NoContent: полномочия не найдены.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `RolePermissionApiList`.

### `GET /Roles/{roleID}/permissionsExt`

## Пример запроса:

GET /roles/1/permissionsExt?isCheckedPermission=true

## Пример успешного ответа:
```json
{
  "1": [
    {
      "permissionExtID": 1,
      "code": "TASK_ASSIGN",
      "description": "Назначение заявок",
      "isChecked": true,
      "systemTag": {
        "id": 1,
        "name": "Управление заявками"
      }
    }
  ]
}
```
            
## Пример успешного ответа (206):
Тело ответа имеет тот же формат, что и для `200`, но содержит частичный диапазон.
## Негативные сценарии:
- 204 NoContent: полномочия не найдены.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `RolePermissionExtList`.

### `GET /Roles/{roleID}/permissionsUi`

## Пример запроса:

GET /roles/1/permissionsUi?isCheckedPermission=true

## Пример успешного ответа:
```json
{
  "1": [
    {
      "permissionUiID": 1,
      "capabilityID": 1,
      "code": "USER_VIEW",
      "description": "Просмотр пользователей",
      "isChecked": true,
      "isSystem": false,
      "systemTag": {
        "id": 1,
        "name": "Управление пользователями"
      }
    }
  ]
}
```
            
## Пример успешного ответа (206):
Тело ответа имеет тот же формат, что и для `200`, но содержит частичный диапазон.
## Негативные сценарии:
- 204 NoContent: полномочия не найдены.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `RolePermissionUiList`.

## SystemPermissionUiTags

### `GET /SystemPermissionUiTags`

## Пример запроса:

GET /systempermissionuitags

## Пример успешного ответа:
```json
{
  "1": [
    {
      "permissionUiID": 10,
      "code": "TAG_1",
      "description": "Тег 1"
    },
    {
      "permissionUiID": 11,
      "code": "TAG_2",
      "description": "Тег 2"
    }
  ]
}
```
            
## Пример успешного ответа (206):
Тело ответа имеет тот же формат, что и для `200`, но содержит частичный диапазон.
## Негативные сценарии:
- 204 NoContent: теги не найдены.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `SystemPermissionUiTagList`.

## TenantCreationRequests

### `POST /TenantCreationRequests`

## Пример запроса:

POST /tenantcreationrequests

```json
{
  "accountID": 456,
  "tenantName": "Новая компания",
  "tenantUriName": "new-company"
}
```

## Пример успешного ответа:
```json
{
  "id": "abc123"
}
```
            
## Негативные сценарии:
- 400 BadRequest: неверные данные тела запроса.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав доступа.

### `GET /TenantCreationRequests/{id}`

## Пример запроса:

GET /tenantcreationrequests/abc123

## Пример успешного ответа:
```json
{
  "id": "abc123",
  "approved": null,
  "processed": null,
  "created": "2024-01-15T10:00:00Z",
  "rejected": null,
  "rejectionReason": null,
  "tenant": null
}
```

Этот метод доступен без аутентификации.

### `PUT /TenantCreationRequests/{id}/approve`

## Пример запроса:

PUT /tenantcreationrequests/abc123/approve

## Пример успешного ответа:

HTTP 202 Accepted

Доступно только для кросс-тенантных администраторов.
            
## Негативные сценарии:
- 400 BadRequest: некорректный идентификатор запроса.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав доступа.

### `PUT /TenantCreationRequests/{id}/reject`

## Пример запроса:

PUT /tenantcreationrequests/abc123/reject

```json
{
  "id": "abc123",
  "reason": "Недостаточно информации для создания тенанта"
}
```

## Пример успешного ответа:

HTTP 202 Accepted

Доступно только для кросс-тенантных администраторов.
            
## Негативные сценарии:
- 400 BadRequest: пустое или отсутствующее тело запроса (`data`).
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав доступа.

## TenantMembers

### `GET /TenantMembers`

## Пример запроса:

GET /tenantmembers?userID=789&accountID=456

## Пример успешного ответа:
```json
{
  "123": {
    "id": 123,
    "description": "Основной член тенанта",
    "validTill": "2025-12-31T23:59:59Z",
    "account": {
      "id": 456,
      "email": "user@example.com",
      "mobilePhone": "+79991234567",
      "login": "username",
      "ban": null
    },
    "user": {
      "id": 789,
      "firstName": "Иван",
      "middleName": "Петрович",
      "lastName": "Иванов",
      "ban": null
    },
    "tokens": null
  },
  "124": {
    "id": 124,
    "description": "Дополнительный член тенанта",
    "validTill": "2025-12-31T23:59:59Z",
    "account": {
      "id": 457,
      "email": "user2@example.com",
      "mobilePhone": "+79991234568",
      "login": "username2",
      "ban": null
    },
    "user": {
      "id": 790,
      "firstName": "Пётр",
      "middleName": null,
      "lastName": "Петров",
      "ban": null
    },
    "tokens": null
  }
}
```

Если фильтр не указан, возвращается список пользователей, с которыми ассоциирована учетная запись текущего члена тенанта.
            
## Пример успешного ответа (206):
Тело ответа имеет тот же формат, что и для `200`, но содержит частичный диапазон.
## Негативные сценарии:
- 204 NoContent: члены не найдены.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `TenantMemberList`.

### `POST /TenantMembers`

## Пример запроса:

POST /tenantmembers

```json
[
  {
    "accountID": 456,
    "userID": 789,
    "description": "Новый член тенанта",
    "validTill": "2025-12-31T23:59:59Z"
  }
]
```

## Пример успешного ответа:
```json
[123]
```
            
## Негативные сценарии:
- 400 BadRequest: неверные данные тела запроса.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `TenantMemberAdd`.

### `PUT /TenantMembers`

## Пример запроса:

PUT /tenantmembers

```json
[
  {
    "id": 123,
    "description": "Обновленное описание",
    "validTill": "2026-12-31T23:59:59Z"
  }
]
```

## Пример успешного ответа:

HTTP 202 Accepted
            
## Негативные сценарии:
- 400 BadRequest: неверные данные тела запроса.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `TenantMemberUpdate`.

### `DELETE /TenantMembers`

## Пример запроса:

DELETE /tenantmembers

```json
[123, 124, 125]
```

## Пример успешного ответа:

HTTP 202 Accepted
            
## Негативные сценарии:
- 400 BadRequest: неверные данные тела запроса.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `TenantMemberDelete`.

### `GET /TenantMembers/anonymousUser`

## Пример запроса:

GET /tenantmembers/anonymousUser

## Пример успешного ответа:
```json
{
  "id": 123,
  "description": "Анонимный пользователь",
  "validTill": "2025-12-31T23:59:59Z",
  "account": {
    "id": 456,
    "email": "anonymous@example.com",
    "mobilePhone": null,
    "login": "anonymous",
    "ban": null
  },
  "user": {
    "id": 789,
    "firstName": "Anonymous",
    "middleName": null,
    "lastName": "User",
    "ban": null
  },
  "tokens": null
}
```
            
## Негативные сценарии:
- 204 NoContent: анонимный пользователь не найден.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `TenantMemberGet`.

### `GET /TenantMembers/apiUser`

## Пример запроса:

GET /tenantmembers/apiUser

## Пример успешного ответа:
```json
{
  "id": 123,
  "description": "API пользователь",
  "validTill": "2025-12-31T23:59:59Z",
  "account": {
    "id": 456,
    "email": "api@example.com",
    "mobilePhone": "+79991234567",
    "login": "apiuser",
    "ban": null
  },
  "user": {
    "id": 789,
    "firstName": "API",
    "middleName": null,
    "lastName": "User",
    "ban": null
  },
  "tokens": null
}
```
            
## Негативные сценарии:
- 204 NoContent: API пользователь не найден.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `TenantMemberGet`.

### `GET /TenantMembers/this`

## Пример запроса:

GET /tenantmembers/this

## Пример успешного ответа:
```json
{
  "id": 123,
  "accountID": 456,
  "userID": 789,
  "description": "Основной член тенанта",
  "validTill": "2025-12-31T23:59:59Z"
}
```
            
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `TenantMemberGet`.

### `GET /TenantMembers/{tenantMemberID}`

## Пример запроса:

GET /tenantmembers/123

## Пример успешного ответа:
```json
{
  "id": 123,
  "accountID": 456,
  "userID": 789,
  "validTill": "2025-12-31T23:59:59Z",
  "description": "Основной член тенанта"
}
```
            
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `TenantMemberGet`.

### `DELETE /TenantMembers/{tenantMemberID}`

## Пример запроса:

DELETE /tenantmembers/123

## Пример успешного ответа:

HTTP 202 Accepted
            
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `TenantMemberDelete`.

## TenantSettings

### `GET /TenantSettings`

## Пример запроса:

GET /tenantsettings?tenantMemberId=123

## Пример успешного ответа:
```json
{
  "geoDataRetentionMonths": 12,
  "supportEmail": "support@example.com",
  "supportPhone": "+7 (999) 123-45-67",
  "storageApiUrl": "https://storage.example.com/api",
  "storageUrl": "https://storage.example.com",
  "defaultCurrency": {
    "id": 1,
    "shortName": "RUB",
    "asciiCode": "RUB"
  },
  "defaultTimezoneID": 1,
  "defaultMailBoxID": 1,
  "storageProviderID": 1,
  "realm": "example",
  "managerFullName": "Иванов Иван",
  "managerPhone": "+79998887766",
  "managerEmail": "manager@hubex.ru"
}
```
            
## Негативные сценарии:
- 204 NoContent: настройки тенанта не найдены.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав доступа.

### `GET /TenantSettings/plateUrl`

## Пример запроса:

GET /tenantsettings/this/plateUrl?taskTemplateID=123

## Пример успешного ответа:
```json
"https://plate.hubex.ru"
```
            
## Негативные сценарии:
- 204 NoContent: кастомный URL не найден.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `TenantPlateUrlGet`.

### `PUT /TenantSettings/plateUrl`

## Пример запроса:

PUT /tenantsettings/this/plateUrl?plateUrl=https://client-domain.ru

### NULL
Если параметр `plateUrl` не передали, будет сохранен `NULL`.

## Пример успешного ответа:

HTTP 202 Accepted
            
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `TenantCustomPlateUrlUpdate`.

## Tenants

### `GET /Tenants`

## Пример запроса:

GET /tenants

## Пример успешного ответа:
```json
[
  {
    "id": 1,
    "name": "Моя компания",
    "uriName": "my-company",
    "fullName": "ООО Моя компания",
    "banned": null,
    "owner": {
      "id": 1,
      "accountID": 456,
      "description": "Владелец тенанта",
      "firstName": "Иван",
      "lastName": "Иванов",
      "middleName": "Петрович"
    },
    "tenantMembers": [
      {
        "id": 1,
        "accountID": 456,
        "description": "Владелец тенанта",
        "firstName": "Иван",
        "lastName": "Иванов",
        "middleName": "Петрович"
      }
    ],
    "isCurrent": true
  }
]
```
            
## Пример успешного ответа (206):
Тело ответа имеет тот же формат, что и для `200`, но содержит частичный диапазон.
## Негативные сценарии:
- 204 NoContent: тенанты не найдены.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `TenantsList`.

### `PUT /Tenants/licenses`

## Пример запроса:

PUT /tenants/licenses

```json
{
  "licenseID": 1,
  "dateFrom": "2024-01-01T00:00:00Z",
  "dateTill": "2025-12-31T23:59:59Z"
}
```

## Пример успешного ответа:

HTTP 202 Accepted
            
## Негативные сценарии:
- 400 BadRequest: неверные данные тела запроса.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `TenantLicenseUpdate`.

### `GET /Tenants/templates`

## Пример запроса:

GET /tenants/templates

## Пример успешного ответа:
```json
[
  {
    "id": 1,
    "name": "Шаблонный тенант",
    "uriName": "template-tenant"
  }
]
```
            
## Пример успешного ответа (206):
Тело ответа имеет тот же формат, что и для `200`, но содержит частичный диапазон.
## Негативные сценарии:
- 204 NoContent: шаблонные тенанты не найдены.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав доступа.

### `GET /Tenants/this`

## Пример запроса:

GET /tenants/this

## Пример успешного ответа:
```json
{
  "id": 1,
  "name": "Моя компания",
  "uriName": "my-company",
  "fullName": "ООО Моя компания",
  "owner": {
    "tenantMemberID": 1,
    "userID": 123,
    "accountID": 456,
    "firstName": "Иван",
    "lastName": "Иванов",
    "middleName": "Петрович",
    "mobilePhone": "+79991234567",
    "email": "owner@example.com"
  },
  "paymentInfo": {
    "payer": "ООО Моя компания",
    "tin": "1234567890",
    "iec": "123456789",
    "lawAddress": "г. Москва, ул. Примерная, д. 1",
    "postAddress": "г. Москва, ул. Примерная, д. 1",
    "phone": "+74951234567",
    "email": "accounting@example.com",
    "contactPerson": "Иванов Иван Петрович",
    "bic": "044525225",
    "bankName": "ПАО Сбербанк",
    "correspondingAccount": "30101810400000000225",
    "checkingAccount": "40702810100000000001"
  }
}
```
            
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `TenantGet`.

### `GET /Tenants/this/featureFlags`

## Пример запроса:

GET /tenants/this/featureFlags

## Пример успешного ответа:
```json
[
  "FEATURE_NEW_UI",
  "FEATURE_ADVANCED_REPORTS",
  "FEATURE_MOBILE_APP"
]
```
            
## Негативные сценарии:
- 204 NoContent: флаги не найдены.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `FeatureFlagsForTenantList`.

### `GET /Tenants/this/licenses`

## Пример запроса:

GET /tenants/this/licenses?validOn=2024-01-15T00:00:00Z

## Пример успешного ответа:
```json
[
  {
    "license": {
      "id": 1,
      "name": "Базовая лицензия",
      "description": "Базовая лицензия тенанта",
      "code": "BASIC"
    },
    "type": {
      "id": 1,
      "name": "Техническая"
    },
    "dateTill": "2024-12-31T23:59:59Z",
    "dateFrom": "2024-01-01T00:00:00Z",
    "trialPeriodDays": 30,
    "remainig": {
      "techniciansCount": 8,
      "companiesCount": 3,
      "publicTaskTemplatesCount": 10
    },
    "total": {
      "techniciansCount": 10,
      "companiesCount": 5,
      "publicTaskTemplatesCount": 20
    },
    "status": {
      "id": 1,
      "name": "Активна"
    }
  }
]
```
            
## Негативные сценарии:
- 204 NoContent: по заданным фильтрам записи не найдены.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `TenantLicenseList`.

### `POST /Tenants/this/licenses`

## Пример запроса:

POST /tenants/this/licenses

```json
{
  "licenseID": 1,
  "dateFrom": "2024-01-01T00:00:00Z",
  "dateTill": "2024-12-31T23:59:59Z",
  "paymentInfo": {
    "payer": "ООО Компания",
    "tin": "1234567890",
    "iec": "123456789",
    "lawAddress": "г. Москва, ул. Примерная, д. 1",
    "postAddress": "г. Москва, ул. Примерная, д. 1",
    "contactPerson": "Иванов Иван Иванович",
    "bic": "044525225",
    "bankName": "ПАО Сбербанк",
    "correspondingAccount": "30101810400000000225",
    "checkingAccount": "40702810100000000001"
  }
}
```

## Пример успешного ответа:

HTTP 201 Created
            
## Негативные сценарии:
- 400 BadRequest: неверные данные тела запроса.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `TenantLicenseAdd`.

### `DELETE /Tenants/this/licenses`

## Пример запроса:

DELETE /tenants/this/licenses

```json
[1, 2, 3]
```

## Пример успешного ответа:

HTTP 202 Accepted
            
## Негативные сценарии:
- 400 BadRequest: неверные данные тела запроса.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `TenantLicenseDelete`.

### `POST /Tenants/this/licenses/renewal`

## Пример запроса:

POST /tenants/this/licenses/renewal

## Пример успешного ответа:

HTTP 200 OK
            
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав доступа.

### `DELETE /Tenants/this/licenses/{id}`

## Пример запроса:

DELETE /tenants/this/licenses/1

## Пример успешного ответа:

HTTP 202 Accepted
            
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `TenantLicenseDelete`.

### `GET /Tenants/this/meta`

## Пример запроса:

GET /tenants/this/meta

## Пример успешного ответа:

HTTP 200 OK

Тело — JSON метаданных тенанта (`DataJson`). Фиксированной схемы ответа нет.
            
## Негативные сценарии:
- 204 NoContent: метаданные не найдены.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав доступа.

### `GET /Tenants/this/packages`

## Пример запроса:

GET /tenants/this/packages?resourceID=1&resourceID=2

## Пример успешного ответа:
```json
[
  {
    "resource": {
      "id": 1,
      "name": "Web интерфейс"
    },
    "package": {
      "id": "pkg-1",
      "name": "Расширение отчетности",
      "version": "1.0.0",
      "iconUrl": "https://example.com/icon.png",
      "isAddAuthorizeParameters": false
    }
  }
]
```
            
## Пример успешного ответа (206):
Тело ответа имеет тот же формат, что и для `200`, но содержит частичный диапазон.
## Негативные сценарии:
- 204 NoContent: расширения не найдены.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав доступа.

### `POST /Tenants/this/packages`

## Пример запроса:

POST /tenants/this/packages

```json
{
  "name": "Расширение отчетности",
  "iconUrl": "https://example.com/icon.png",
  "addonUrl": "https://example.com/addon",
  "resourceID": 1,
  "isMobile": false
}
```

## Пример успешного ответа:
```json
[
  {
    "resource": {
      "id": 1,
      "name": "Web интерфейс"
    },
    "package": {
      "id": "pkg-1",
      "name": "Расширение отчетности",
      "version": "1.0.0",
      "iconUrl": "https://example.com/icon.png",
      "isAddAuthorizeParameters": false
    }
  }
]
```
            
## Негативные сценарии:
- 400 BadRequest: пустое или отсутствующее тело запроса (`data`).
- 204 NoContent: расширение не найдено.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав доступа.

### `PATCH /Tenants/this/packages`

## Пример запроса:

PATCH /tenants/this/packages

```json
{
  "addonID": "pkg-1",
  "version": "1.0.0",
  "name": "Расширение отчетности"
}
```

## Пример успешного ответа:

HTTP 202 Accepted
            
## Негативные сценарии:
- 400 BadRequest: пустое или отсутствующее тело запроса (`data`).
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав доступа.

### `DELETE /Tenants/this/packages`

## Пример запроса:

DELETE /tenants/this/packages

```json
{
  "addonID": "pkg-1",
  "version": "1.0.0"
}
```

## Пример успешного ответа:

HTTP 202 Accepted
            
## Негативные сценарии:
- 400 BadRequest: пустое или отсутствующее тело запроса (`data`).
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав доступа.

### `POST /Tenants/this/packages/tenant`

## Пример запроса:

POST /tenants/this/packages/tenant

```json
{
  "addonID": "pkg-1",
  "version": "1.0.0"
}
```

## Пример успешного ответа:
```json
[
  {
    "resource": {
      "id": 1,
      "name": "Web интерфейс"
    },
    "package": {
      "id": "pkg-1",
      "name": "Расширение отчетности",
      "version": "1.0.0",
      "iconUrl": "https://example.com/icon.png",
      "isAddAuthorizeParameters": false
    }
  }
]
```
            
## Негативные сценарии:
- 400 BadRequest: пустое или отсутствующее тело запроса (`data`).
- 204 NoContent: расширение не найдено.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав доступа.

### `DELETE /Tenants/this/packages/tenant`

## Пример запроса:

DELETE /tenants/this/packages/tenant

```json
{
  "addonID": "pkg-1",
  "version": "1.0.0"
}
```

## Пример успешного ответа:

HTTP 202 Accepted
            
## Негативные сценарии:
- 400 BadRequest: пустое или отсутствующее тело запроса (`data`).
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав доступа.

### `GET /Tenants/this/variables`

## Пример запроса:

GET /tenants/this/variables

## Пример успешного ответа:
```json
{
  "API_URL": {
    "value": "https://api.example.com",
    "description": "URL API сервиса"
  },
  "DB_CONNECTION": {
    "value": "Server=localhost;Database=HubEx",
    "description": "Строка подключения к БД"
  }
}
```
            
## Пример успешного ответа (206):
Тело ответа имеет тот же формат, что и для `200`, но содержит частичный диапазон.
## Негативные сценарии:
- 204 NoContent: переменные не найдены.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `TenantVariableList`.

### `POST /Tenants/this/variables`

## Пример запроса:

POST /tenants/this/variables

```json
[
  {
    "name": "API_URL",
    "value": "https://api.example.com",
    "description": "URL API сервиса"
  },
  {
    "name": "DB_CONNECTION",
    "value": "Server=localhost;Database=HubEx",
    "description": "Строка подключения к БД"
  }
]
```

## Пример успешного ответа:

HTTP 201 Created
            
## Негативные сценарии:
- 400 BadRequest: неверные данные тела запроса.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `TenantVariableAdd`.

### `PUT /Tenants/this/variables`

## Пример запроса:

PUT /tenants/this/variables

```json
[
  {
    "name": "API_URL",
    "value": "https://new-api.example.com",
    "description": "Обновленный URL API сервиса"
  }
]
```

## Пример успешного ответа:

HTTP 202 Accepted
            
## Негативные сценарии:
- 400 BadRequest: неверные данные тела запроса.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `TenantVariableUpdate`.

### `DELETE /Tenants/this/variables`

## Пример запроса:

DELETE /tenants/this/variables

```json
["API_URL", "DB_CONNECTION"]
```

## Пример успешного ответа:

HTTP 202 Accepted
            
## Негативные сценарии:
- 400 BadRequest: неверные данные тела запроса.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `TenantVariableDelete`.

### `DELETE /Tenants/this/variables/{name}`

## Пример запроса:

DELETE /tenants/this/variables/API_URL

## Пример успешного ответа:

HTTP 202 Accepted
            
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `TenantVariableDelete`.

## UserAssetListQueries

### `POST /UserAssetListQueries`

## Пример запроса:

POST /userassetlistqueries

```json
[
  {
    "userID": 123,
    "data": [10, 11]
  },
  {
    "userID": 124,
    "data": [10]
  }
]
```

## Пример успешного ответа:
```json
[
  {
    "assetListQueryID": 10,
    "userID": 123
  },
  {
    "assetListQueryID": 11,
    "userID": 123
  },
  {
    "assetListQueryID": 10,
    "userID": 124
  }
]
```
            
## Негативные сценарии:
- 400 BadRequest: неверные данные тела запроса.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `UserAssetListQueryAdd`.

### `DELETE /UserAssetListQueries`

## Пример запроса:

DELETE /userassetlistqueries

```json
[
  {
    "userID": 123,
    "data": [10, 11]
  }
]
```

## Пример успешного ответа:

HTTP 202 Accepted
            
## Негативные сценарии:
- 400 BadRequest: неверные данные тела запроса.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `UserAssetListQueryDelete`.

### `POST /UserAssetListQueries/{userID}`

## Пример запроса:

POST /userassetlistqueries/123

```json
[10, 11, 12]
```

## Пример успешного ответа:
```json
[
  {
    "assetListQueryID": 10,
    "userID": 123
  },
  {
    "assetListQueryID": 11,
    "userID": 123
  },
  {
    "assetListQueryID": 12,
    "userID": 123
  }
]
```
            
## Негативные сценарии:
- 400 BadRequest: неверные данные тела запроса.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `UserAssetListQueryAdd`.

### `DELETE /UserAssetListQueries/{userID}`

## Пример запроса:

DELETE /userassetlistqueries/123

```json
[10, 11]
```

## Пример успешного ответа:

HTTP 202 Accepted
            
## Негативные сценарии:
- 400 BadRequest: неверные данные тела запроса.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `UserAssetListQueryDelete`.

## UserCompanyListQueries

### `POST /UserCompanyListQueries`

## Пример запроса:

POST /usercompanylistqueries

```json
[
  {
    "userID": 123,
    "data": [10, 11]
  },
  {
    "userID": 124,
    "data": [10]
  }
]
```

## Пример успешного ответа:
```json
[
  {
    "companyListQueryID": 10,
    "userID": 123
  },
  {
    "companyListQueryID": 11,
    "userID": 123
  },
  {
    "companyListQueryID": 10,
    "userID": 124
  }
]
```
            
## Негативные сценарии:
- 400 BadRequest: неверные данные тела запроса.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `UserCompanyListQueryAdd`.

### `DELETE /UserCompanyListQueries`

## Пример запроса:

DELETE /usercompanylistqueries

```json
[
  {
    "userID": 123,
    "data": [10, 11]
  }
]
```

## Пример успешного ответа:

HTTP 202 Accepted
            
## Негативные сценарии:
- 400 BadRequest: неверные данные тела запроса.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `UserCompanyListQueryDelete`.

### `POST /UserCompanyListQueries/{userID}`

## Пример запроса:

POST /usercompanylistqueries/123

```json
[10, 11, 12]
```

## Пример успешного ответа:
```json
[
  {
    "companyListQueryID": 10,
    "userID": 123
  },
  {
    "companyListQueryID": 11,
    "userID": 123
  },
  {
    "companyListQueryID": 12,
    "userID": 123
  }
]
```
            
## Негативные сценарии:
- 400 BadRequest: неверные данные тела запроса.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `UserCompanyListQueryAdd`.

### `DELETE /UserCompanyListQueries/{userID}`

## Пример запроса:

DELETE /usercompanylistqueries/123

```json
[10, 11]
```

## Пример успешного ответа:

HTTP 202 Accepted
            
## Негативные сценарии:
- 400 BadRequest: неверные данные тела запроса.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `UserCompanyListQueryDelete`.

## UserDisabledNotifications

### `POST /UserDisabledNotifications`

## Пример запроса:

POST /userdisablednotifications

```json
{
  "userID": 123,
  "data": [
    {
      "providerID": 1,
      "isOn": false
    },
    {
      "providerID": 2,
      "isOn": true
    }
  ]
}
```

## Пример успешного ответа:
```json
[
  {
    "providerID": 1,
    "isOn": false
  },
  {
    "providerID": 2,
    "isOn": true
  }
]
```
            
## Негативные сценарии:
- 400 BadRequest: пустое или отсутствующее тело запроса (`data`).
- 204 NoContent: настройки не найдены.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав доступа.

## UserDistricts

### `POST /UserDistricts`

## Пример запроса:

POST /userdistricts

```json
{
  "userID": 123,
  "data": [
    {
      "districtID": 1,
      "scheduleRuleID": 10
    },
    {
      "districtID": 2,
      "scheduleRuleID": 11
    }
  ]
}
```

## Пример успешного ответа:
```json
{
  "123": [1, 2]
}
```
            
## Негативные сценарии:
- 400 BadRequest: пустое или отсутствующее тело запроса (`data`).
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `UserDistrictAdd`.

### `PUT /UserDistricts`

## Пример запроса:

PUT /userdistricts

```json
{
  "userID": 123,
  "data": [
    {
      "districtID": 1,
      "scheduleRuleID": 10
    }
  ]
}
```

## Пример успешного ответа:

HTTP 202 Accepted
            
## Негативные сценарии:
- 400 BadRequest: пустое или отсутствующее тело запроса (`data`).
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `UserDistrictUpdate`.

### `DELETE /UserDistricts`

## Пример запроса:

DELETE /userdistricts

```json
{
  "userID": 123,
  "data": [1, 2, 3]
}
```

## Пример успешного ответа:

HTTP 202 Accepted
            
## Негативные сценарии:
- 400 BadRequest: пустое или отсутствующее тело запроса (`data`).
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `UserDistrictDelete`.

## UserOrderBy

### `GET /UserOrderBy`

## Пример запроса:

GET /userorderby

## Пример успешного ответа:
```json
{
  "1": {
    "name": "По имени",
    "code": "BY_NAME"
  },
  "2": {
    "name": "По дате регистрации",
    "code": "BY_REGISTRATION_DATE"
  }
}
```
            
## Пример успешного ответа (206):
Тело ответа имеет тот же формат, что и для `200`, но содержит частичный диапазон.
## Негативные сценарии:
- 204 NoContent: методы сортировки не найдены.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `UserOrderByList`.

## UserRoles

### `POST /UserRoles`

## Пример запроса:

POST /userroles

```json
[
  {
    "userID": 123,
    "roleIDs": [1, 2]
  },
  {
    "userID": 124,
    "roleIDs": [1]
  }
]
```

## Пример успешного ответа:
```json
{
  "123": [1, 2],
  "124": [1]
}
```
            
## Негативные сценарии:
- 400 BadRequest: пустое или отсутствующее тело запроса (`data`).
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `UserRoleAdd`.

### `DELETE /UserRoles`

## Пример запроса:

DELETE /userroles

```json
[
  {
    "userID": 123,
    "roleIDs": [1, 2]
  }
]
```

## Пример успешного ответа:

HTTP 202 Accepted
            
## Негативные сценарии:
- 400 BadRequest: пустое или отсутствующее тело запроса (`data`).
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `UserRoleDelete`.

## UserTags

### `POST /UserTags`

## Пример запроса:

POST /usertags

```json
[
  {
    "userID": 123,
    "tags": ["VIP", "Менеджер"]
  }
]
```

## Пример успешного ответа:
```json
[
  {
    "userID": 123,
    "tag": "VIP"
  },
  {
    "userID": 123,
    "tag": "Менеджер"
  }
]
```
            
## Негативные сценарии:
- 400 BadRequest: неверные данные тела запроса.
- 409 Conflict: бизнес-конфликт при добавлении тегов.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `UserTagAdd`.

### `DELETE /UserTags`

## Пример запроса:

DELETE /usertags

```json
[
  {
    "userID": 123,
    "tags": ["VIP"]
  }
]
```

## Пример успешного ответа:

HTTP 202 Accepted
            
## Негативные сценарии:
- 400 BadRequest: неверные данные тела запроса.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `UserTagRemove`.

## UserTaskListQueries

### `POST /UserTaskListQueries`

## Пример запроса:

POST /usertasklistqueries

```json
[
  {
    "userID": 616,
    "data": [94]
  },
  {
    "userID": 123,
    "data": [10, 11]
  }
]
```

## Пример успешного ответа:
```json
[
  {
    "taskListQueryID": 94,
    "userID": 616
  },
  {
    "taskListQueryID": 10,
    "userID": 123
  },
  {
    "taskListQueryID": 11,
    "userID": 123
  }
]
```
            
## Негативные сценарии:
- 400 BadRequest: неверные данные тела запроса.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `UserTaskListQueryAdd`.

### `DELETE /UserTaskListQueries`

## Пример запроса:

DELETE /usertasklistqueries

```json
[
  {
    "userID": 616,
    "data": [94]
  }
]
```

## Пример успешного ответа:

HTTP 202 Accepted
            
## Негативные сценарии:
- 400 BadRequest: неверные данные тела запроса.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `UserTaskListQueryDelete`.

## UserTemplateDistricts

### `POST /UserTemplateDistricts`

## Пример запроса:

POST /usertemplatedistricts

```json
[
  {
    "userTemplateID": 1,
    "data": [10, 11]
  },
  {
    "userTemplateID": 2,
    "data": [10]
  }
]
```

## Пример успешного ответа:
```json
{
  "1": [10, 11],
  "2": [10]
}
```
            
## Негативные сценарии:
- 400 BadRequest: неверные данные тела запроса.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `UserTemplateDistrictAdd`.

### `DELETE /UserTemplateDistricts/remove`

## Пример запроса:

DELETE /usertemplatedistricts/remove

```json
[
  {
    "userTemplateID": 1,
    "data": [10, 11]
  }
]
```

## Пример успешного ответа:

HTTP 202 Accepted
            
## Негативные сценарии:
- 400 BadRequest: неверные данные тела запроса.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `UserTemplateDistrictRemove`.

## UserTemplateRoles

### `POST /UserTemplateRoles`

## Пример запроса:

POST /usertemplateroles

```json
[
  {
    "userTemplateID": 1,
    "data": [10, 11]
  },
  {
    "userTemplateID": 2,
    "data": [10]
  }
]
```

## Пример успешного ответа:
```json
{
  "1": [10, 11],
  "2": [10]
}
```
            
## Негативные сценарии:
- 400 BadRequest: неверные данные тела запроса.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `UserTemplateRoleAdd`.

### `DELETE /UserTemplateRoles/remove`

## Пример запроса:

DELETE /usertemplateroles/remove

```json
[
  {
    "userTemplateID": 1,
    "data": [10, 11]
  }
]
```

## Пример успешного ответа:

HTTP 202 Accepted
            
## Негативные сценарии:
- 400 BadRequest: неверные данные тела запроса.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `UserTemplateRoleRemove`.

## UserTemplates

### `GET /UserTemplates`

## Пример запроса:

GET /usertemplates?searchText=инженер&isTechnician=true&roleID=1&districtID=2

## Пример успешного ответа:
```json
{
  "1": {
    "id": 1,
    "name": "Шаблон инженера",
    "description": "Шаблон для инженеров",
    "isTechnician": true,
    "isTeam": false,
    "isCustomer": false,
    "defaultLocationID": 10,
    "mobilityID": 1,
    "geoTrackingModeID": 1,
    "roles": [
      {
        "id": 1,
        "name": "Инженер"
      }
    ],
    "districts": [
      {
        "id": 2,
        "name": "Участок 2"
      }
    ]
  }
}
```
            
## Пример успешного ответа (206):
Тело ответа имеет тот же формат, что и для `200`, но содержит частичный диапазон.
## Негативные сценарии:
- 204 NoContent: шаблоны не найдены.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `UserTemplateList`.

### `POST /UserTemplates`

## Пример запроса:

POST /usertemplates

```json
[
  {
    "name": "Новый шаблон инженера",
    "description": "Описание шаблона",
    "isTechnician": true,
    "defaultLocationID": 10
  }
]
```

## Пример успешного ответа:
```json
[1]
```
            
## Негативные сценарии:
- 400 BadRequest: неверные данные тела запроса.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `UserTemplateAdd`.

### `PUT /UserTemplates`

## Пример запроса:

PUT /usertemplates

```json
[
  {
    "id": 1,
    "name": "Обновленное название",
    "description": "Обновленное описание",
    "defaultLocationID": 11
  }
]
```

## Пример успешного ответа:

HTTP 202 Accepted
            
## Негативные сценарии:
- 400 BadRequest: неверные данные тела запроса.
- 409 Conflict: бизнес-конфликт при обновлении шаблона.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `UserTemplateUpdate`.

### `DELETE /UserTemplates`

## Пример запроса:

DELETE /usertemplates

```json
[1, 2, 3]
```

## Пример успешного ответа:

HTTP 202 Accepted
            
## Негативные сценарии:
- 400 BadRequest: неверные данные тела запроса.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `UserTemplateDelete`.

### `GET /UserTemplates/{id}`

## Пример запроса:

GET /usertemplates/1

## Пример успешного ответа:
```json
{
  "id": 1,
  "name": "Шаблон инженера",
  "description": "Шаблон для инженеров",
  "isTechnician": true,
  "isTeam": false,
  "isCustomer": false,
  "defaultLocation": {
    "id": 10,
    "address": "Москва, ул. Примерная, 1"
  },
  "mobility": {
    "id": 1,
    "name": "Мобильный"
  },
  "geoTrackingMode": {
    "id": 1,
    "name": "Автоматический"
  }
}
```
            
## Негативные сценарии:
- 204 NoContent: шаблон не найден.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `UserTemplateGet`.

### `DELETE /UserTemplates/{id}`

## Пример запроса:

DELETE /usertemplates/1

## Пример успешного ответа:

HTTP 202 Accepted
            
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `UserTemplateDelete`.

### `GET /UserTemplates/{id}/districts`

## Пример запроса:

GET /usertemplates/1/districts

## Пример успешного ответа:
```json
[
  {
    "id": 1,
    "name": "Центральный участок"
  },
  {
    "id": 2,
    "name": "Северный участок"
  }
]
```
            
## Пример успешного ответа (206):
Тело ответа имеет тот же формат, что и для `200`, но содержит частичный диапазон.
## Негативные сценарии:
- 204 NoContent: участки не найдены.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `UserTemplateDistrictList`.

### `GET /UserTemplates/{id}/roles`

## Пример запроса:

GET /usertemplates/1/roles

## Пример успешного ответа:
```json
[
  {
    "id": 1,
    "name": "Инженер"
  },
  {
    "id": 2,
    "name": "Менеджер"
  }
]
```
            
## Пример успешного ответа (206):
Тело ответа имеет тот же формат, что и для `200`, но содержит частичный диапазон.
## Негативные сценарии:
- 204 NoContent: роли не найдены.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `UserTemplateRoleList`.

## UserWarehouses

### `POST /UserWarehouses`

## Пример запроса:

POST /userwarehouses

```json
[
  {
    "userID": 123,
    "warehouseIDs": [1, 2]
  }
]
```

## Пример успешного ответа:
```json
{
  "123": [1, 2]
}
```

⚠️ **Устаревший метод**: Используйте POST /WH/WarehouseUser/s
            
## Негативные сценарии:
- 400 BadRequest: пустое или отсутствующее тело запроса (`data`).
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `UserWarehouseAdd`.

### `DELETE /UserWarehouses`

## Пример запроса:

DELETE /userwarehouses

```json
[
  {
    "userID": 123,
    "warehouseIDs": [1]
  }
]
```

## Пример успешного ответа:

HTTP 202 Accepted

⚠️ **Устаревший метод**: Используйте DELETE /WH/WarehouseUser/
            
## Негативные сценарии:
- 400 BadRequest: пустое или отсутствующее тело запроса (`data`).
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `UserWarehouseDelete`.

## Users

### `GET /Users`

## Пример запроса:
            
GET /users?searchText=Иван&includeDistricts=true&includeTaskActuality=false
            
## Пример успешного ответа:
```json
{
  "123": {
    "userID": 123,
    "firstName": "Иван",
    "lastName": "Иванов",
    "employments": [],
    "districts": [],
    "sortOrder": 1
  }
}
```
            
## Пример успешного ответа (206):
Тело ответа имеет тот же формат, что и для `200`, но содержит частичный диапазон.
            
## Негативные сценарии:
- 204 NoContent: по заданным фильтрам записи не найдены.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `UsersList`.

### `POST /Users`

## Пример запроса:

POST /users?skipAccountVerification=false

```json
{
  "firstName": "Иван",
  "middleName": "Николаевич",
  "lastName": "Реван",
  "sexID": 1,
  "email": "japose9395@combcub.com",
  "mobilePhone": "+79991234567",
  "workPhone": null,
  "accountDomainLogin": "DOMAIN\\username",
  "isTechnician": true,
  "isTeam": false,
  "isCustomer": true,
  "mobilityID": 1,
  "geotrackingModeID": 1,
  "banReasonID": null,
  "banTill": null,
  "isEmailVerified": false,
  "isMobilePhoneVerified": false,
  "rate": 1500.00,
  "rateCurrencyID": 1
}
```

## Пример успешного ответа:
```json
{
  "id": 456,
  "userID": 123,
  "tenantMemberID": 789,
  "tenantID": 1,
  "isNewAccount": true,
  "isPasswordDefined": false,
  "verificationRequestValidTill": "2024-01-15T10:15:00Z"
}
```

## Пример ошибки:
```json
[
  {
    "traceIdentifier": "0HMV3B6Q3K2Q1:00000001",
    "code": "UserAccountAlreadyExists",
    "message": "Пользователь с таким email, телефоном или domain login уже существует"
  }
]
```
            
## Негативные сценарии:
- 400 BadRequest: пустое или отсутствующее тело запроса (`data`).
- 409 Conflict: не пройдена валидация `AddData` (`firstName`/`lastName`, `sexID`; для техника — `mobilityID`/`geotrackingModeID`; нужен email, телефон или domain login) (`InvalidDataException` / `InvalidEmailException` / `ParameterOutOfRangeException`).
- 409 Conflict: некорректный `mobilePhone` (`InvalidPhoneException`).
- 409 Conflict: учетная запись с таким email, телефоном или domain login уже существует (`UserAccountAlreadyExists`).
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `UserAdd`.

### `DELETE /Users`

## Пример запроса:

DELETE /users

```json
[123, 456, 789]
```

## Пример успешного ответа:

HTTP 202 Accepted
            
## Негативные сценарии:
- 409 Conflict: бизнес-конфликт при удалении одного или нескольких пользователей.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `UserDelete`.

### `HEAD /Users`

## Пример запроса:
            
HEAD /users?isDeleted=false
            
## Пример успешного ответа:
            
HTTP 200 OK
            
Заголовок ответа:
```
Content-Range: items 0-0/42
```
            
Тело ответа пустое.
            
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `UsersList`.

### `POST /Users/addbyintegration`

## Пример запроса:

POST /users/addbyintegration?skipAccountVerification=false

```json
{
  "firstName": "Иван",
  "middleName": "Николаевич",
  "lastName": "Реван",
  "sexID": 1,
  "email": "japose9395@combcub.com",
  "mobilePhone": "+79991234567",
  "workPhone": null,
  "accountDomainLogin": "DOMAIN\\username",
  "isTechnician": true,
  "isTeam": false,
  "isCustomer": true,
  "mobilityID": 1,
  "geotrackingModeID": 1,
  "banReasonID": null,
  "banTill": null,
  "isEmailVerified": false,
  "isMobilePhoneVerified": false,
  "rate": 1500.00,
  "rateCurrencyID": 1
}
```

## Пример успешного ответа:
```json
[
  {
    "userID": 123,
    "roleID": 1
  }
]
```

## Пример ошибки:
```json
[
  {
    "traceIdentifier": "0HMV3B6Q3K2Q1:00000001",
    "code": "UserAccountAlreadyExists",
    "message": "Пользователь с таким email, телефоном или domain login уже существует"
  }
]
```
            
## Негативные сценарии:
- 400 BadRequest: пустое или отсутствующее тело запроса (`data`).
- 409 Conflict: не пройдена валидация `AddData` (`firstName`/`lastName`, `sexID`; для техника — `mobilityID`/`geotrackingModeID`; нужен email, телефон или domain login) (`InvalidDataException` / `InvalidEmailException` / `ParameterOutOfRangeException`).
- 409 Conflict: некорректный `mobilePhone` (`InvalidPhoneException`).
- 409 Conflict: учетная запись с таким email, телефоном или domain login уже существует (`UserAccountAlreadyExists`).
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `UserAddWithSystemRoleByIntegration`.

### `POST /Users/anonymous`

## Пример запроса:

POST /users/anonymous

## Пример успешного ответа:
```json
{
  "userID": 123,
  "tenantMemberID": 456
}
```
            
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `UserAddAnonymous`.

### `POST /Users/api`

## Пример запроса:

POST /users/api

## Пример успешного ответа:
```json
{
  "userID": 123,
  "tenantMemberID": 456
}
```
            
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `UserAddApi`.

### `GET /Users/attributes`

## Пример запроса:

GET /users/attributes?userID=123&attributeID=1

## Пример успешного ответа:
```json
[
  {
    "tenantID": 1,
    "userID": 123,
    "attributeID": 1,
    "attributeName": "Специализация",
    "value": "Электрика",
    "domain": {
      "id": 1,
      "name": "Технические навыки",
      "code": "TECH_SKILLS"
    }
  }
]
```
            
## Пример успешного ответа (206):
Тело ответа имеет тот же формат, что и для `200`, но содержит частичный диапазон.
            
## Негативные сценарии:
- 204 NoContent: по заданным фильтрам записи не найдены.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `UserAttributeList`.

### `POST /Users/attributes`

## Пример запроса:

POST /users/attributes

```json
[
  {
    "userID": 123,
    "data": {
      "attributeID": 1,
      "value": "Электрика"
    }
  }
]
```

## Пример успешного ответа:

HTTP 201 Created
            
## Негативные сценарии:
- 400 BadRequest: неверные данные тела запроса.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `UserAttributeAdd`.

### `PUT /Users/attributes`

## Пример запроса:

PUT /users/attributes

```json
[
  {
    "userID": 123,
    "data": {
      "attributeID": 1,
      "value": "Сантехника"
    }
  }
]
```

## Пример успешного ответа:

HTTP 202 Accepted
            
## Негативные сценарии:
- 400 BadRequest: неверные данные тела запроса.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `UserAttributeUpdate`.

### `DELETE /Users/attributes`

## Пример запроса:

DELETE /users/attributes

```json
[
  {
    "userID": 123,
    "data": 1
  }
]
```

## Пример успешного ответа:

HTTP 202 Accepted
            
## Негативные сценарии:
- 400 BadRequest: неверные данные тела запроса.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `UserAttributeDelete`.

### `DELETE /Users/avatar`

## Пример запроса:
            
DELETE /users/avatar
            
```json
[123, 124]
```
            
## Пример успешного ответа:
            
HTTP 202 Accepted
            
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `UserProfileAvatarDelete`.

### `POST /Users/changeToCustomer`

## Пример запроса:

POST /users/changeToCustomer

```json
[123, 456, 789]
```

## Пример успешного ответа:

HTTP 202 Accepted
            
## Негативные сценарии:
- 400 BadRequest: неверные данные тела запроса.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `UserChangeTypeToCustomer`.

### `POST /Users/changeToStaff`

## Пример запроса:

POST /users/changeToStaff

```json
[123, 456, 789]
```

## Пример успешного ответа:

HTTP 202 Accepted
            
## Негативные сценарии:
- 400 BadRequest: неверные данные тела запроса.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `UserChangeTypeToStaff`.

### `POST /Users/defaultPages`

## Пример запроса:

POST /users/defaultPages

```json
[
  {
    "userID": 1,
    "webPage": "dashboard",
    "mobilePage": "tasks"
  },
  {
    "userID": 2,
    "webPage": "workorders",
    "mobilePage": null
  }
]
```

## Успешный ответ

HTTP 201 Created, без тела.
            
## Негативные сценарии:
- 409 Conflict: null-элемент или не заданы `webPage` и `mobilePage` (`ParameterOutOfRangeException`).
- 409 Conflict: у всех переданных пользователей настройки стартовых страниц уже существуют.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `UserDefaultPagesAdd`.

### `PUT /Users/defaultPages`

## Пример запроса:
            
PUT /users/defaultPages
            
```json
[
  {
    "userID": 123,
    "webPage": "dashboard",
    "mobilePage": "tasks"
  },
  {
    "userID": 124,
    "webPage": "workorders",
    "mobilePage": null
  }
]
```
            
## Успешный ответ
            
HTTP 202 Accepted, без тела.
            
## Негативные сценарии:
- 409 Conflict: null-элемент или не заданы `webPage` и `mobilePage` (`ParameterOutOfRangeException`).
- 400 BadRequest: ошибка обновления настроек для всех переданных пользователей.
- 404 NotFound: ни для одного из переданных пользователей не найдены настройки стартовых страниц.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `UserDefaultPagesUpdate`.

### `DELETE /Users/defaultPages`

## Пример запроса:

DELETE /users/defaultPages

```json
[123, 124, 125]
```

## Пример успешного ответа:

HTTP 202 Accepted
            
## Негативные сценарии:
- 400 BadRequest: неверные данные тела запроса.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `UserDefaultPagesDelete`.

### `GET /Users/geolocation`

## Пример запроса:

GET /users/geolocation?userID=123

## Пример успешного ответа:
```json
[
  {
    "tenantID": 1,
    "userID": 123,
    "coordinateAccuracy": {
      "id": 1,
      "isDefault": true
    }
  }
]
```
            
## Пример успешного ответа (206):
Тело ответа имеет тот же формат, что и для `200`, но содержит частичный диапазон.
            
## Негативные сценарии:
- 204 NoContent: по заданным фильтрам записи не найдены.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `UserGeolocationList`.

### `POST /Users/geolocation`

## Пример запроса:

POST /users/geolocation

```json
[
  {
    "userID": 123,
    "coordinateAccuracyID": 1
  }
]
```

## Пример успешного ответа:

HTTP 201 Created
            
## Негативные сценарии:
- 400 BadRequest: неверные данные тела запроса.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `UserGeolocationBatchAdd`.

### `PUT /Users/geolocation`

## Пример запроса:

PUT /users/geolocation

```json
[
  {
    "userID": 123,
    "coordinateAccuracyID": 2
  }
]
```

## Пример успешного ответа:

HTTP 202 Accepted
            
## Негативные сценарии:
- 400 BadRequest: неверные данные тела запроса.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `UserGeolocationBatchUpdate`.

### `GET /Users/profile`

## Пример запроса:

GET /users/profile?tenantMemberId=1&userId=123

## Пример успешного ответа:
```json
{
  "userID": 123,
  "firstName": "Иван",
  "middleName": "Петрович",
  "lastName": "Иванов",
  "email": "ivan.ivanov@example.com",
  "mobilePhone": "+79991234567",
  "workPhone": "+74951234567",
  "isEmailVerified": true,
  "isMobilePhoneVerified": true,
  "isTechnician": true,
  "isTeam": false,
  "isCustomer": false,
  "avatarUrl": "https://storage.example.com/avatars/user123.jpg",
  "isDelegationOn": false,
  "averageRating": 4.5,
  "sex": {
    "id": 1,
    "name": "Мужской"
  },
  "employments": [
    {
      "company": {
        "id": 1,
        "name": "ООО Пример"
      },
      "position": "Инженер",
      "scheduleRuleID": 1,
      "dateFrom": "2024-01-01T00:00:00Z",
      "dateTill": "2024-12-31T23:59:59Z"
    }
  ],
  "geoTrackingMode": {
    "id": 1,
    "name": "Автоматический"
  }
}
```

## Пример ошибки:
```json
{
  "traceIdentifier": "0HMV3B6Q3K2Q1:00000001",
  "code": "USER_NOT_FOUND", 
  "message": "Пользователь не найден"
}
```
            
## Негативные сценарии:
- 404 NotFound: пользователь не найден.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `UserGet`.

### `POST /Users/registration`

## Пример запроса:

POST /users/registration

```json
{
  "invitationID": "123e4567-e89b-12d3-a456-426614174000",
  "firstName": "Иван",
  "middleName": "Петрович",
  "lastName": "Иванов",
  "email": "ivan.ivanov@example.com",
  "mobilePhone": "+79991234567",
  "accountDomainLogin": "DOMAIN\\username"
}
```

## Пример успешного ответа:
```json
{
  "accountID": 456,
  "tenantID": 1,
  "userID": 123,
  "verificationCodeRepeatTimeout": 60
}
```
            
## Негативные сценарии:
- 400 BadRequest: пустое или отсутствующее тело запроса (`data`).
- 409 Conflict: не заданы обязательные `invitationID`/`firstName`/`lastName` или превышена длина строковых полей (`InvalidDataException`).
- 409 Conflict: не передан ни `email`, ни `mobilePhone`, ни `accountDomainLogin` (`InvalidDataException`).
- 204 NoContent: регистрация по приглашению не выполнена.
- 409 Conflict: приглашение недействительно или бизнес-конфликт при регистрации.

### `POST /Users/registration/verify`

## Пример запроса:

POST /users/registration/verify

```json
{
  "tenantID": 1,
  "accountID": 456
}
```

## Пример успешного ответа:
```json
{
  "accountID": 456,
  "tenantID": 1,
  "userID": null,
  "verificationCodeRepeatTimeout": 60
}
```
            
## Негативные сценарии:
- 400 BadRequest: пустое или отсутствующее тело запроса (`data`).
- 409 Conflict: не пройдена валидация `tenantID`/`accountID` (`InvalidDataException` / `ParameterOutOfRangeException`).

### `GET /Users/relevance`

## Пример запроса:
            
GET /users/relevance?searchText=Иван&assetID=100&includeDistricts=true
            
## Пример успешного ответа:
```json
{
  "123": {
    "userID": 123,
    "firstName": "Иван",
    "lastName": "Иванов",
    "relevance": {
      "total": 85
    }
  }
}
```
            
## Пример успешного ответа (206):
Тело ответа имеет тот же формат, что и для `200`, но содержит частичный диапазон.
            
## Негативные сценарии:
- 204 NoContent: по заданным фильтрам записи не найдены.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `UsersList`.

### `PUT /Users/restore`

## Пример запроса:

PUT /users/restore

```json
[123, 456, 789]
```

## Пример успешного ответа:

HTTP 202 Accepted
            
## Негативные сценарии:
- 409 Conflict: бизнес-конфликт при восстановлении одного или нескольких пользователей.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `UserRestore`.

### `GET /Users/short`

## Пример запроса:
            
GET /users/short?searchText=Иван
            
## Пример успешного ответа:
```json
{
  "123": {
    "userID": 123,
    "firstName": "Иван",
    "lastName": "Иванов",
    "employments": [],
    "sortOrder": 1
  }
}
```
            
## Пример успешного ответа (206):
Тело ответа имеет тот же формат, что и для `200`, но содержит частичный диапазон.
            
## Негативные сценарии:
- 204 NoContent: по заданным фильтрам записи не найдены.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `UsersListShort`.

### `GET /Users/this/assetListQueries`

## Пример запроса:

GET /users/this/assetListQueries

## Пример успешного ответа:
```json
{
  "1": {
    "name": "Мои объекты",
    "filter": {
      "flags": {
        "isDeleted": false
      }
    },
    "searchText": "Офис",
    "queryString": "?searchText=Офис&range=1-10",
    "sort": {
      "orderBy": 1,
      "direction": 2
    },
    "range": {
      "offset": 0,
      "fetch": 10
    }
  }
}
```
            
## Пример успешного ответа (206):
Тело ответа имеет тот же формат, что и для `200`, но содержит частичный диапазон.
            
## Негативные сценарии:
- 204 NoContent: сохраненные запросы по объектам текущего пользователя не найдены.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `AssetListQueryList`.

### `DELETE /Users/this/avatar`

## Пример запроса:
            
DELETE /users/this/avatar
            
## Пример успешного ответа:
            
HTTP 202 Accepted
            
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `UserProfileAvatarDelete`.

### `PUT /Users/this/avatar/upload/fromBody`

## Пример запроса:
            
PUT /users/this/avatar/upload/fromBody
            
```json
{
  "fileName": "avatar.jpg",
  "contentType": "image/jpeg",
  "file": "base64-encoded-content"
}
```
            
## Пример успешного ответа:
```json
{
  "attachmentID": 456,
  "publicUrl": "https://storage.example.com/avatars/user123.jpg",
  "size": 102400
}
```
            
## Негативные сценарии:
- 400 BadRequest: пустое или отсутствующее тело запроса (`data`).
- 409 Conflict: не пройдена валидация данных вложения (`InvalidDataException`).
- 409 Conflict: значение `userID` вне допустимого диапазона (`ParameterOutOfRangeException`).
- 409 Conflict: недопустимый `Content-Type` изображения (`InvalidContentTypeException`).
- 400 BadRequest: ошибка загрузки файла в хранилище.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `UserProfileAvatarUpload`.

### `PUT /Users/this/avatar/upload/fromForm`

## Пример запроса:
            
PUT /users/this/avatar/upload/fromForm
            
Форма multipart/form-data с полем файла изображения JPG не менее 128x128.
            
## Пример успешного ответа:
```json
{
  "attachmentID": 456,
  "publicUrl": "https://storage.example.com/avatars/user123.jpg",
  "size": 102400
}
```
            
## Негативные сценарии:
- 400 BadRequest: пустое или отсутствующее тело запроса (`data`).
- 409 Conflict: не пройдена валидация данных вложения (`InvalidDataException`).
- 409 Conflict: значение `userID` вне допустимого диапазона (`ParameterOutOfRangeException`).
- 409 Conflict: недопустимый `Content-Type` изображения (`InvalidContentTypeException`).
- 400 BadRequest: ошибка загрузки файла в хранилище.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `UserProfileAvatarUpload`.

### `GET /Users/this/companyListQueries`

## Пример запроса:
            
GET /users/this/companyListQueries
            
## Пример успешного ответа:
```json
{
  "10": {
    "name": "Мои компании",
    "filter": {
      "flags": {
        "isDeleted": false
      }
    },
    "searchText": "",
    "queryString": "?isDeleted=false",
    "sort": {
      "orderBy": 1,
      "direction": 2
    }
  }
}
```
            
## Пример успешного ответа (206):
Тело ответа имеет тот же формат, что и для `200`, но содержит частичный диапазон.
            
## Негативные сценарии:
- 204 NoContent: сохраненные запросы по компаниям текущего пользователя не найдены.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `CompanyListQueryList`.

### `GET /Users/this/geolocation`

## Пример запроса:

GET /users/this/geolocation

## Пример успешного ответа:
```json
{
  "tenantID": 1,
  "userID": 123,
  "coordinateAccuracy": {
    "id": 1,
    "parametersJson": "{\"accuracy\": 10}",
    "isDefault": true
  }
}
```
            
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `UserGeolocationGet`.

### `GET /Users/this/notifications`

## Пример запроса:

GET /users/this/notifications

## Пример успешного ответа:
```json
{
  "email": "user@example.com",
  "mobilePhone": "+79991234567",
  "providers": [
    {
      "id": 1,
      "code": "EMAIL",
      "name": "Email",
      "isOn": true,
      "isAvailableForUser": true
    }
  ]
}
```
            
## Пример успешного ответа (206):
Тело ответа имеет тот же формат, что и для `200`, но содержит частичный диапазон.
            
## Негативные сценарии:
- 204 NoContent: настройки уведомлений текущего пользователя не найдены.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.

### `GET /Users/this/permissions/ext`

## Пример запроса:

GET /users/this/permissions/ext

## Пример успешного ответа:
```json
{
  "1": "TASK_ASSIGN",
  "2": "USER_MANAGE",
  "3": "REPORT_VIEW"
}
```
            
## Пример успешного ответа (206):
Тело ответа имеет тот же формат, что и для `200`, но содержит частичный диапазон.
            
## Негативные сценарии:
- 204 NoContent: расширенные полномочия текущего пользователя не найдены.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав доступа.

### `GET /Users/this/permissions/ui`

## Пример запроса:

GET /users/this/permissions/ui

## Пример успешного ответа:
```json
{
  "USER_VIEW": "READ",
  "USER_EDIT": "WRITE",
  "TASK_CREATE": "READ"
}
```
            
## Пример успешного ответа (206):
Тело ответа имеет тот же формат, что и для `200`, но содержит частичный диапазон.
            
## Негативные сценарии:
- 204 NoContent: UI-полномочия текущего пользователя не найдены.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав доступа.

### `GET /Users/this/profile`

## Пример запроса:

GET /users/this/profile

## Пример успешного ответа:
```json
{
  "userID": 123,
  "firstName": "Иван",
  "middleName": "Петрович",
  "lastName": "Иванов",
  "email": "ivan.ivanov@example.com",
  "mobilePhone": "+79991234567",
  "workPhone": "+74951234567",
  "isEmailVerified": true,
  "isMobilePhoneVerified": true,
  "isTechnician": true,
  "isTeam": false,
  "isCustomer": false,
  "avatarUrl": "https://storage.example.com/avatars/user123.jpg",
  "isDelegationOn": false,
  "averageRating": 4.5,
  "sex": {
    "id": 1,
    "name": "Мужской"
  },
  "employments": [
    {
      "company": {
        "id": 1,
        "name": "ООО Пример"
      },
      "position": "Инженер",
      "scheduleRuleID": 1,
      "dateFrom": "2024-01-01T00:00:00Z",
      "dateTill": "2024-12-31T23:59:59Z"
    }
  ],
  "geoTrackingMode": {
    "id": 1,
    "name": "Автоматический"
  }
}
```
            
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `UserGet`.

### `GET /Users/this/taskListQueries`

## Пример запроса:

GET /users/this/taskListQueries

## Пример успешного ответа:
```json
{
  "87": {
    "name": "Мои заявки",
    "filter": {
      "taskFlags": {
        "isClosed": false
      },
      "districts": [592],
      "workTypes": [6],
      "flags": {
        "isDeleted": false
      }
    },
    "searchText": "",
    "queryString": "?districtID=592&workTypeID=6&isDeleted=false&isClosed=false&orderBy=1&sortDirection=2",
    "isUserQuery": true,
    "sort": {
      "orderBy": 1,
      "direction": 2
    }
  }
}
```
            
## Пример успешного ответа (206):
Тело ответа имеет тот же формат, что и для `200`, но содержит частичный диапазон.
            
## Негативные сценарии:
- 204 NoContent: сохраненные запросы по заявкам текущего пользователя не найдены.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `TaskListQueryList`.

### `GET /Users/{UserID}/ratings`

## Пример запроса:

GET /users/123/ratings

## Пример успешного ответа:
```json
{
  "technicianID": 123,
  "averageRating": 4.5,
  "maxMark": 5,
  "ratingCriterias": [
    {
      "id": 1,
      "name": "Качество работы",
      "averageRating": 4.8,
      "rating": [
        {
          "markNumber": 5,
          "countOfTotal": 10,
          "direction": 1
        }
      ]
    }
  ]
}
```
            
## Пример успешного ответа (206):
Тело ответа имеет тот же формат, что и для `200`, но содержит частичный диапазон.
            
## Негативные сценарии:
- 204 NoContent: рейтинги инженера не найдены.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `TaskTechnicianRatingListByTechnicianForTenantMember`.

### `GET /Users/{id}`

## Пример запроса:

GET /users/123

## Пример успешного ответа:
```json
{
  "firstName": "Иван",
  "middleName": "Петрович",
  "lastName": "Иванов",
  "email": "ivan.ivanov@example.com",
  "mobilePhone": "+79991234567",
  "workPhone": "+74951234567",
  "isEmailVerified": true,
  "isMobilePhoneVerified": true,
  "isTechnician": true,
  "isTeam": false,
  "isCustomer": false,
  "avatarUrl": "https://storage.example.com/avatars/user123.jpg",
  "teamUserID": null,
  "lastSeen": "2024-01-15T14:30:00Z",
  "rate": 1500.50,
  "accountDomainLogin": "DOMAIN\\username",
  "ban": null,
  "defaultLocation": {
    "id": 1,
    "address": "г. Москва, ул. Примерная, д. 1",
    "coordinate": "55.7558, 37.6173"
  },
  "actualLocation": {
    "coordinate": "55.7558, 37.6173",
    "actuality": "2024-01-15T14:30:00Z"
  },
  "mobility": {
    "id": 1,
    "name": "Мобильный"
  },
  "geoTrackingMode": {
    "id": 1,
    "name": "Автоматический"
  },
  "rating": {
    "total": 4.5,
    "totalTrendDirection": 1,
    "timestamp": "2024-01-15T14:30:00Z"
  },
  "flags": {
    "IsAllowedNestedDistricts": true
  },
  "sex": {
    "id": 1,
    "name": "Мужской"
  },
  "rateCurrency": {
    "id": 1,
    "shortName": "RUB",
    "asciiCode": "RUB"
  }
}
```

## Пример ошибки:
```json
{
  "traceIdentifier": "0HMV3B6Q3K2Q1:00000001",
  "code": "USER_NOT_FOUND", 
  "message": "Пользователь с ID 999 не найден"
}
```
            
## Негативные сценарии:
- 404 NotFound: пользователь с указанным `id` не найден.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `UserGet`.

### `PUT /Users/{id}`

## Пример запроса:

PUT /users/3

```json
{
  "firstName": "Anonymous",
  "middleName": "",
  "lastName": "",
  "sexID": 3,
  "email": "",
  "mobilePhone": "",
  "workPhone": "",
  "isTechnician": null,
  "mobilityID": null,
  "geotrackingModeID": null,
  "rate": null,
  "rateCurrencyID": null
}
```

## Пример успешного ответа:

HTTP 202 Accepted
            
## Негативные сценарии:
- 400 BadRequest: пустое или отсутствующее тело запроса (`data`).
- 409 Conflict: некорректный `mobilePhone` (`InvalidPhoneException`).
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `UserUpdate`.

### `GET /Users/{id}/assetListQueries`

## Пример запроса:

GET /users/123/assetListQueries

## Пример успешного ответа:
```json
{
  "1": {
    "name": "Мои объекты",
    "filter": {
      "flags": {
        "isDeleted": false
      }
    },
    "searchText": "Офис",
    "queryString": "?searchText=Офис&range=1-10",
    "sort": {
      "orderBy": 1,
      "direction": 2
    },
    "range": {
      "offset": 0,
      "fetch": 10
    }
  }
}
```
            
## Пример успешного ответа (206):
Тело ответа имеет тот же формат, что и для `200`, но содержит частичный диапазон.
            
## Негативные сценарии:
- 204 NoContent: сохраненные запросы по объектам пользователя не найдены.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `AssetListQueryList`.

### `DELETE /Users/{id}/avatar`

## Пример запроса:
            
DELETE /users/123/avatar
            
## Пример успешного ответа:
            
HTTP 202 Accepted
            
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `UserProfileAvatarDelete`.

### `PUT /Users/{id}/avatar/upload/fromBody`

## Пример запроса:
            
PUT /users/123/avatar/upload/fromBody
            
```json
{
  "fileName": "avatar.jpg",
  "contentType": "image/jpeg",
  "file": "base64-encoded-content"
}
```
            
## Пример успешного ответа:
```json
{
  "attachmentID": 456,
  "publicUrl": "https://storage.example.com/avatars/user123.jpg",
  "size": 102400
}
```
            
## Негативные сценарии:
- 400 BadRequest: пустое или отсутствующее тело запроса (`data`).
- 409 Conflict: не пройдена валидация данных вложения (`InvalidDataException`).
- 409 Conflict: значение `userID` вне допустимого диапазона (`ParameterOutOfRangeException`).
- 409 Conflict: недопустимый `Content-Type` изображения (`InvalidContentTypeException`).
- 400 BadRequest: ошибка загрузки файла в хранилище.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `UserProfileAvatarUpload`.

### `PUT /Users/{id}/avatar/upload/fromForm`

## Пример запроса:
            
PUT /users/123/avatar/upload/fromForm
            
Форма multipart/form-data с полем файла изображения JPG не менее 256x256.
            
## Пример успешного ответа:
```json
{
  "attachmentID": 456,
  "publicUrl": "https://storage.example.com/avatars/user123.jpg",
  "size": 102400
}
```
            
## Негативные сценарии:
- 400 BadRequest: пустое или отсутствующее тело запроса (`data`).
- 409 Conflict: не пройдена валидация данных вложения (`InvalidDataException`).
- 409 Conflict: значение `userID` вне допустимого диапазона (`ParameterOutOfRangeException`).
- 409 Conflict: недопустимый `Content-Type` изображения (`InvalidContentTypeException`).
- 400 BadRequest: ошибка загрузки файла в хранилище.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `UserProfileAvatarUpload`.

### `GET /Users/{id}/companyListQueries`

## Пример запроса:
            
GET /users/123/companyListQueries
            
## Пример успешного ответа:
```json
{
  "10": {
    "name": "Мои компании",
    "filter": {
      "flags": {
        "isDeleted": false
      }
    },
    "searchText": "",
    "queryString": "?isDeleted=false",
    "sort": {
      "orderBy": 1,
      "direction": 2
    }
  }
}
```
            
## Пример успешного ответа (206):
Тело ответа имеет тот же формат, что и для `200`, но содержит частичный диапазон.
            
## Негативные сценарии:
- 204 NoContent: сохраненные запросы по компаниям пользователя не найдены.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `CompanyListQueryList`.

### `GET /Users/{id}/districts`

## Пример запроса:

GET /users/123/districts

## Пример успешного ответа:
```json
{
  "1": {
    "parentID": null,
    "name": "Центральный район"
  },
  "2": {
    "parentID": 1,
    "name": "Северный район"
  }
}
```
            
## Пример успешного ответа (206):
Тело ответа имеет тот же формат, что и для `200`, но содержит частичный диапазон.
            
## Негативные сценарии:
- 204 NoContent: участки пользователя не найдены.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `UserDistrictList`.

### `GET /Users/{id}/notifications`

## Пример запроса:

GET /users/123/notifications

## Пример успешного ответа:
```json
{
  "email": "user@example.com",
  "mobilePhone": "+79991234567",
  "providers": [
    {
      "id": 1,
      "code": "EMAIL",
      "name": "Email",
      "isOn": true,
      "isAvailableForUser": true
    }
  ]
}
```
            
## Пример успешного ответа (206):
Тело ответа имеет тот же формат, что и для `200`, но содержит частичный диапазон.
            
## Негативные сценарии:
- 204 NoContent: настройки уведомлений пользователя не найдены.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.

### `GET /Users/{id}/profile`

## Пример запроса:

GET /users/123/profile

## Пример успешного ответа:
```json
{
  "userID": 123,
  "firstName": "Иван",
  "middleName": "Петрович",
  "lastName": "Иванов",
  "email": "ivan.ivanov@example.com",
  "mobilePhone": "+79991234567",
  "workPhone": "+74951234567",
  "isEmailVerified": true,
  "isMobilePhoneVerified": true,
  "isTechnician": true,
  "isTeam": false,
  "isCustomer": false,
  "avatarUrl": "https://storage.example.com/avatars/user123.jpg",
  "isDelegationOn": false,
  "averageRating": 4.5,
  "sex": {
    "id": 1,
    "name": "Мужской"
  },
  "employments": [
    {
      "company": {
        "id": 1,
        "name": "ООО Пример"
      },
      "position": "Инженер",
      "scheduleRuleID": 1,
      "dateFrom": "2024-01-01T00:00:00Z",
      "dateTill": "2024-12-31T23:59:59Z"
    }
  ],
  "geoTrackingMode": {
    "id": 1,
    "name": "Автоматический"
  }
}
```

## Пример ошибки:
```json
{
  "traceIdentifier": "0HMV3B6Q3K2Q1:00000001",
  "code": "USER_NOT_FOUND", 
  "message": "Пользователь не найден"
}
```
            
## Негативные сценарии:
- 404 NotFound: пользователь с указанным `id` не найден.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `UserGet`.

### `GET /Users/{id}/roles`

## Пример запроса:

GET /users/123/roles

## Пример успешного ответа:
```json
{
  "123": [
    {
      "id": 1,
      "name": "Администратор"
    },
    {
      "id": 2,
      "name": "Менеджер"
    }
  ]
}
```
            
## Пример успешного ответа (206):
Тело ответа имеет тот же формат, что и для `200`, но содержит частичный диапазон.
            
## Негативные сценарии:
- 204 NoContent: роли пользователя не найдены.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `UserRoleList`.

### `GET /Users/{id}/taskListQueries`

## Пример запроса:

GET /users/123/taskListQueries

## Пример успешного ответа:
```json
{
  "87": {
    "name": "Мои заявки",
    "filter": {
      "taskFlags": {
        "isClosed": false
      },
      "districts": [592],
      "workTypes": [6],
      "flags": {
        "isDeleted": false
      }
    },
    "searchText": "",
    "queryString": "?districtID=592&workTypeID=6&isDeleted=false&isClosed=false&orderBy=1&sortDirection=2",
    "isUserQuery": true,
    "sort": {
      "orderBy": 1,
      "direction": 2
    }
  }
}
```
            
## Пример успешного ответа (206):
Тело ответа имеет тот же формат, что и для `200`, но содержит частичный диапазон.
            
## Негативные сценарии:
- 204 NoContent: сохраненные запросы по заявкам пользователя не найдены.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `TaskListQueryList`.

### `GET /Users/{id}/warehouses`

## Пример запроса:

GET /users/123/warehouses

## Пример успешного ответа:
```json
[
  {
    "id": 1,
    "name": "Склад №1",
    "erpID": "WH001"
  },
  {
    "id": 2,
    "name": "Склад №2",
    "erpID": "WH002"
  }
]
```
            
## Пример успешного ответа (206):
Тело ответа имеет тот же формат, что и для `200`, но содержит частичный диапазон.
            
## Негативные сценарии:
- 204 NoContent: склады пользователя не найдены.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `UserWarehouseList`.

### `DELETE /Users/{userID}`

## Пример запроса:

DELETE /users/123

## Пример успешного ответа:

HTTP 202 Accepted
            
## Негативные сценарии:
- 409 Conflict: бизнес-конфликт при удалении пользователя.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `UserDelete`.

### `GET /Users/{userID}/assetAssignments`

## Пример запроса:

GET /users/123/assetAssignments?validOn=2024-01-15T00:00:00Z

## Пример успешного ответа:
```json
[
  {
    "asset": {
      "id": 1,
      "name": "Объект №1"
    },
    "validityPeriod": {
      "from": "2024-01-01T00:00:00Z",
      "till": "2024-12-31T23:59:59Z"
    },
    "notes": "Основной объект"
  }
]
```
            
## Пример успешного ответа (206):
Тело ответа имеет тот же формат, что и для `200`, но содержит частичный диапазон.
            
## Негативные сценарии:
- 204 NoContent: назначения объектов для указанного пользователя не найдены.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `AssetAssignmentList`.

### `GET /Users/{userID}/attributes`

## Пример запроса:

GET /users/123/attributes?attributeID=1

## Пример успешного ответа:
```json
[
  {
    "tenantID": 1,
    "userID": 123,
    "attributeID": 1,
    "attributeName": "Специализация",
    "value": "Электрика",
    "domain": {
      "id": 1,
      "name": "Технические навыки",
      "code": "TECH_SKILLS"
    }
  }
]
```
            
## Пример успешного ответа (206):
Тело ответа имеет тот же формат, что и для `200`, но содержит частичный диапазон.
            
## Негативные сценарии:
- 204 NoContent: атрибуты указанного пользователя не найдены.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `UserAttributeList`.

### `POST /Users/{userID}/attributes`

## Пример запроса:

POST /users/123/attributes

```json
[
  {
    "attributeID": 1,
    "value": "Электрика"
  }
]
```

## Пример успешного ответа:

HTTP 201 Created
            
## Негативные сценарии:
- 400 BadRequest: неверные данные тела запроса.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `UserAttributeAdd`.

### `PUT /Users/{userID}/attributes`

## Пример запроса:

PUT /users/123/attributes

```json
[
  {
    "attributeID": 1,
    "value": "Сантехника"
  }
]
```

## Пример успешного ответа:

HTTP 202 Accepted
            
## Негативные сценарии:
- 400 BadRequest: неверные данные тела запроса.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `UserAttributeUpdate`.

### `DELETE /Users/{userID}/attributes`

## Пример запроса:

DELETE /users/123/attributes

```json
[1, 2, 3]
```

## Пример успешного ответа:

HTTP 202 Accepted
            
## Негативные сценарии:
- 400 BadRequest: неверные данные тела запроса.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `UserAttributeDelete`.

### `GET /Users/{userID}/defaultPages`

## Пример запроса:

GET /users/123/defaultPages

## Пример успешного ответа:
```json
{
  "tenantID": 1,
  "userID": 123,
  "webPage": "dashboard",
  "mobilePage": "tasks",
  "webPageNameRu": "Дашборд",
  "mobilePageNameRu": "Задачи"
}
```
            
## Негативные сценарии:
- 204 NoContent: настройки стартовых страниц пользователя не найдены.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `UserDefaultPagesGet`.

### `POST /Users/{userID}/geolocation`

## Пример запроса:

POST /users/123/geolocation?coordinateAccuracyID=1

## Пример успешного ответа:

HTTP 201 Created
            
## Негативные сценарии:
- 400 BadRequest: некорректный `userID` или `coordinateAccuracyID`.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `UserGeolocationAdd`.

### `PUT /Users/{userID}/geolocation`

## Пример запроса:

PUT /users/123/geolocation?coordinateAccuracyID=2

## Пример успешного ответа:

HTTP 202 Accepted
            
## Негативные сценарии:
- 400 BadRequest: некорректный `userID` или `coordinateAccuracyID`.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `UserGeolocationUpdate`.

### `PUT /Users/{userID}/resendinvitation`

## Пример запроса:

PUT /users/123/resendinvitation

## Пример успешного ответа:

HTTP 202 Accepted
            
## Негативные сценарии:
- 204 NoContent: для указанного пользователя не найден член тенанта.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `UserAdd`.

### `PUT /Users/{userID}/restore`

## Пример запроса:

PUT /users/123/restore

## Пример успешного ответа:

HTTP 202 Accepted
            
## Негативные сценарии:
- 409 Conflict: бизнес-конфликт при восстановлении пользователя.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `UserRestore`.

### `GET /Users/{userID}/skills`

## Пример запроса:

GET /users/123/skills

## Пример успешного ответа:
```json
{
  "1": {
    "id": 1,
    "name": "Электрика",
    "dateFrom": "2024-01-01T00:00:00Z",
    "dateTill": "2024-12-31T23:59:59Z"
  },
  "2": {
    "id": 2,
    "name": "Сантехника",
    "dateFrom": "2024-01-01T00:00:00Z",
    "dateTill": "2024-12-31T23:59:59Z"
  }
}
```
            
## Пример успешного ответа (206):
Тело ответа имеет тот же формат, что и для `200`, но содержит частичный диапазон.
            
## Негативные сценарии:
- 204 NoContent: навыки пользователя не найдены.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `UserSkillList`.

### `GET /Users/{userID}/tags`

## Пример запроса:

GET /users/123/tags

## Пример успешного ответа:
```json
[
  "Срочно",
  "VIP",
  "Важный клиент"
]
```
            
## Пример успешного ответа (206):
Тело ответа имеет тот же формат, что и для `200`, но содержит частичный диапазон.
            
## Негативные сценарии:
- 204 NoContent: теги пользователя не найдены.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `UserTagsList`.
