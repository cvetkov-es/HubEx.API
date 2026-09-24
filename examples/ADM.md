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
