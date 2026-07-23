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
    "weightCoefficient": 1.0
  },
  "2": {
    "code": "CAPABILITY_2",
    "name": "Возможность 2",
    "weightCoefficient": 1.5
  }
}
```

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

## GeolocationSettings

### `GET /GeolocationSettings/coordinateAccuracy`

## Пример запроса:

GET /geolocationsettings/coordinateAccuracy

## Пример успешного ответа:
```json
[
  {
    "id": 1,
    "name": "Высокая точность",
    "description": "Точность до 5 метров"
  },
  {
    "id": 2,
    "name": "Средняя точность",
    "description": "Точность до 50 метров"
  }
]
```

## Invitations

### `POST /Invitations`

## Пример запроса:

POST /invitations

```json
[
  {
    "userTemplateID": 1,
    "description": "Приглашение для нового сотрудника",
    "validTill": "2025-12-31T23:59:59Z",
    "isPublic": true,
    "allowSelfRegistration": true
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

### `PUT /Invitations`

## Пример запроса:

PUT /invitations

```json
[
  {
    "id": "123e4567-e89b-12d3-a456-426614174000",
    "description": "Обновленное описание приглашения",
    "validTill": "2026-12-31T23:59:59Z"
  }
]
```

## Пример успешного ответа:

HTTP 202 Accepted

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

### `GET /Invitations/{id}`

## Пример запроса:

GET /invitations/123e4567-e89b-12d3-a456-426614174000

## Пример успешного ответа:
```json
{
  "id": "123e4567-e89b-12d3-a456-426614174000",
  "pinCode": "123456",
  "description": "Приглашение для нового сотрудника",
  "isForSupport": false,
  "userTemplate": {
    "id": 1,
    "name": "Шаблон инженера"
  },
  "validTill": "2025-12-31T23:59:59Z"
}
```

### `DELETE /Invitations/{id}`

## Пример запроса:

DELETE /invitations/123e4567-e89b-12d3-a456-426614174000

## Пример успешного ответа:

HTTP 202 Accepted

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
  "tenant": {
    "id": 1,
    "name": "Компания"
  },
  "validTill": "2025-12-31T23:59:59Z"
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

### `DELETE /PermissionsUi`

## Пример запроса:

DELETE /permissionsui

```json
[1, 2, 3]
```

## Пример успешного ответа:

HTTP 202 Accepted

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
  "deleted": false
}
```

Метод возвращает данные, включая помеченные как удаленные.

### `DELETE /PermissionsUi/{id}`

## Пример запроса:

DELETE /permissionsui/1

## Пример успешного ответа:

HTTP 202 Accepted

## RoleApplications

### `POST /RoleApplications`

## Пример запроса:

POST /roleapplications

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

### `DELETE /RoleApplications`

## Пример запроса:

DELETE /roleapplications

```json
[
  {
    "tenantID": 1,
    "roleID": 1,
    "applicationID": 10
  }
]
```

## Пример успешного ответа:

HTTP 202 Accepted

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

## RolePermissionsApi

### `POST /RolePermissionsApi`

## Пример запроса:

POST /rolepermissionsapi

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

### `DELETE /RolePermissionsApi`

## Пример запроса:

DELETE /rolepermissionsapi

```json
[
  {
    "roleID": 1,
    "permissionApiID": 10
  }
]
```

## Пример успешного ответа:

HTTP 202 Accepted

## RolePermissionsExt

### `POST /RolePermissionsExt`

## Пример запроса:

POST /rolepermissionsext

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

### `DELETE /RolePermissionsExt`

## Пример запроса:

DELETE /rolepermissionsext

```json
[
  {
    "roleID": 1,
    "permissionExtID": 10
  }
]
```

## Пример успешного ответа:

HTTP 202 Accepted

## RolePermissionsUi

### `POST /RolePermissionsUi`

## Пример запроса:

POST /rolepermissionsui

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

### `DELETE /RolePermissionsUi`

## Пример запроса:

DELETE /rolepermissionsui

```json
[
  {
    "roleID": 1,
    "permissionUiID": 10
  }
]
```

## Пример успешного ответа:

HTTP 202 Accepted

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

## RoleTaskPropertiesAccess

### `POST /RoleTaskPropertiesAccess/attributes`

## Пример запроса:

POST /roletaskpropertiesaccess/attributes

```json
[
  {
    "roleID": 1,
    "attributeID": 10,
    "isAccessable": true,
    "isDefault": false
  }
]
```

## Пример успешного ответа:

HTTP 201 Created

### `PUT /RoleTaskPropertiesAccess/attributes`

## Пример запроса:

PUT /roletaskpropertiesaccess/attributes

```json
[
  {
    "roleID": 1,
    "attributeID": 10,
    "isAccessable": false,
    "isDefault": true
  }
]
```

## Пример успешного ответа:

HTTP 202 Accepted

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
    "deleted": false
  },
  {
    "id": 2,
    "name": "Менеджер",
    "description": "Роль менеджера",
    "deleted": false
  }
]
```

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

### `DELETE /Roles`

## Пример запроса:

DELETE /roles

```json
[1, 2, 3]
```

## Пример успешного ответа:

HTTP 202 Accepted

### `POST /Roles/copy`

## Пример запроса:

POST /roles/copy

```json
[
  {
    "sourceRoleID": 1,
    "name": "Копия роли администратора"
  }
]
```

## Пример успешного ответа:
```json
[3]
```

### `GET /Roles/{id}`

## Пример запроса:

GET /roles/1

## Пример успешного ответа:
```json
{
  "id": 1,
  "name": "Администратор",
  "description": "Роль администратора системы",
  "deleted": false,
  "permissions": [
    "USER_VIEW",
    "USER_EDIT",
    "ROLE_MANAGE"
  ]
}
```

### `DELETE /Roles/{id}`

## Пример запроса:

DELETE /roles/1

## Пример успешного ответа:

HTTP 202 Accepted

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

### `GET /Roles/{roleID}/attachments`

## Пример запроса:

GET /roles/1/attachments

## Пример успешного ответа:
```json
{
  "1": {
    "fileName": "document.pdf",
    "description": "Документация",
    "isUploaded": true,
    "publicUrl": "https://example.com/files/document.pdf",
    "mimeType": "application/pdf",
    "size": 1024000,
    "created": "2024-01-01T00:00:00Z"
  }
}
```

### `GET /Roles/{roleID}/packages`

## Пример запроса:

GET /roles/1/packages?searchText=модуль

## Пример успешного ответа:
```json
{
  "1": {
    "id": 1,
    "packageID": 10,
    "packageVersion": "1.0.0",
    "packageName": "Модуль отчетности",
    "isEnabled": true,
    "resource": {
      "url": "https://example.com/resource"
    }
  }
}
```

### `POST /Roles/{roleID}/packages`

## Пример запроса:

POST /roles/1/packages

```json
[
  {
    "packageID": 10,
    "packageVersion": "1.0.0"
  }
]
```

## Пример успешного ответа:
```json
[
  {
    "roleID": 1,
    "id": 5,
    "packageID": 10,
    "packageVersion": "1.0.0"
  }
]
```

### `DELETE /Roles/{roleID}/packages`

## Пример запроса:

DELETE /roles/1/packages

```json
[1, 2, 3]
```

## Пример успешного ответа:

HTTP 202 Accepted

### `PUT /Roles/{roleID}/packages/activate`

## Пример запроса:

PUT /roles/1/packages/activate

```json
[1, 2, 3]
```

## Пример успешного ответа:

HTTP 202 Accepted

### `PUT /Roles/{roleID}/packages/deactivate`

## Пример запроса:

PUT /roles/1/packages/deactivate

```json
[1, 2, 3]
```

## Пример успешного ответа:

HTTP 202 Accepted

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
        "code": "USERS",
        "description": "Управление пользователями"
      }
    }
  ]
}
```

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
        "code": "TASKS",
        "description": "Управление заявками"
      }
    }
  ]
}
```

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
        "code": "USERS",
        "description": "Управление пользователями"
      }
    }
  ]
}
```

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

## TenantCreationRequests

### `POST /TenantCreationRequests`

## Пример запроса:

POST /tenantcreationrequests

```json
{
  "name": "Новая компания",
  "uriName": "new-company",
  "fullName": "ООО Новая компания",
  "email": "admin@newcompany.com"
}
```

## Пример успешного ответа:
```json
{
  "id": "abc123"
}
```

### `GET /TenantCreationRequests/{id}`

## Пример запроса:

GET /tenantcreationrequests/abc123

## Пример успешного ответа:
```json
{
  "id": "abc123",
  "approved": false,
  "processed": false,
  "created": "2024-01-15T10:00:00Z",
  "rejected": false,
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

### `PUT /TenantCreationRequests/{id}/reject`

## Пример запроса:

PUT /tenantcreationrequests/abc123/reject

```json
{
  "rejectionReason": "Недостаточно информации для создания тенанта"
}
```

## Пример успешного ответа:

HTTP 202 Accepted

Доступно только для кросс-тенантных администраторов.

## TenantMembers

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

### `DELETE /TenantMembers`

## Пример запроса:

DELETE /tenantmembers

```json
[123, 124, 125]
```

## Пример успешного ответа:

HTTP 202 Accepted

### `GET /TenantMembers/anonymousUser`

## Пример запроса:

GET /tenantmembers/anonymousUser

## Пример успешного ответа:
```json
{
  "id": 123,
  "accountID": 456,
  "userID": 789,
  "description": "Анонимный пользователь"
}
```

### `GET /TenantMembers/apiUser`

## Пример запроса:

GET /tenantmembers/apiUser

## Пример успешного ответа:
```json
{
  "id": 123,
  "accountID": 456,
  "userID": 789,
  "description": "API пользователь"
}
```

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

### `GET /TenantMembers/{tenantMemberID}`

## Пример запроса:

GET /tenantmembers/123

## Пример успешного ответа:
```json
{
  "id": 123,
  "accountID": 456,
  "userID": 789,
  "description": "Основной член тенанта",
  "validTill": "2025-12-31T23:59:59Z",
  "account": {
    "id": 456,
    "email": "user@example.com",
    "login": "user"
  },
  "user": {
    "id": 789,
    "firstName": "Иван",
    "lastName": "Петров"
  }
}
```

## Пример ошибки:
```json
[
  {
    "traceIdentifier": "0HMV3B6Q3K2Q1:00000001",
    "code": "TENANT_MEMBER_NOT_FOUND", 
    "message": "Член тенанта с ID 999 не найден"
  }
]
```

### `DELETE /TenantMembers/{tenantMemberID}`

## Пример запроса:

DELETE /tenantmembers/123

## Пример успешного ответа:

HTTP 202 Accepted

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
    "shortName": "RUB"
  },
  "defaultTimezoneID": 1,
  "defaultMailBoxID": 1,
  "realm": "example"
}
```

## Пример ошибки:
```json
[
  {
    "traceIdentifier": "0HMV3B6Q3K2Q1:00000001",
    "code": "SETTINGS_ERROR", 
    "message": "Ошибка при получении настроек"
  }
]
```

### `GET /TenantSettings/plateUrl`

## Пример запроса:

GET /tenantsettings/this/plateUrl?taskTemplateID=123

## Пример успешного ответа:
```json
"https://plate.hubex.ru"
```

### `PUT /TenantSettings/plateUrl`

## Пример запроса:

PUT /tenantsettings/this/plateUrl?plateUrl=https://client-domain.ru

### NULL
Если параметр `plateUrl` не передали, будет сохранен `NULL`.

## Пример успешного ответа:

HTTP 202 Accepted

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
    "banned": null,
    "owner": {
      "tenantMemberID": 1,
      "userID": 123
    },
    "accounts": [
      {
        "id": 456,
        "email": "user@example.com"
      }
    ]
  }
]
```

### `PUT /Tenants/licenses`

## Пример запроса:

PUT /tenants/licenses

```json
{
  "id": 1,
  "dateFrom": "2024-01-01T00:00:00Z",
  "dateTill": "2025-12-31T23:59:59Z",
  "payment": {
    "payer": "ООО Обновленная компания",
    "tin": "1234567890"
  }
}
```

## Пример успешного ответа:

HTTP 202 Accepted

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
    "accountID": 456
  }
}
```

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

### `GET /Tenants/this/licenses`

## Пример запроса:

GET /tenants/this/licenses?validOn=2024-01-15T00:00:00Z

## Пример успешного ответа:
```json
[
  {
    "id": 1,
    "license": {
      "code": "BASIC",
      "name": "Базовая лицензия"
    },
    "type": {
      "id": 1,
      "name": "Техническая"
    },
    "dateFrom": "2024-01-01T00:00:00Z",
    "dateTill": "2024-12-31T23:59:59Z",
    "status": {
      "id": 1,
      "name": "Активна"
    },
    "total": {
      "techniciansCount": 10,
      "companiesCount": 5
    },
    "remaining": {
      "techniciansCount": 8,
      "companiesCount": 3
    }
  }
]
```

### `POST /Tenants/this/licenses`

## Пример запроса:

POST /tenants/this/licenses

```json
{
  "licenseID": 1,
  "dateFrom": "2024-01-01T00:00:00Z",
  "dateTill": "2024-12-31T23:59:59Z",
  "payment": {
    "payer": "ООО Компания",
    "tin": "1234567890",
    "email": "payment@example.com"
  }
}
```

## Пример успешного ответа:

HTTP 201 Created

### `DELETE /Tenants/this/licenses`

## Пример запроса:

DELETE /tenants/this/licenses

```json
[1, 2, 3]
```

## Пример успешного ответа:

HTTP 202 Accepted

### `POST /Tenants/this/licenses/renewal`

## Пример запроса:

POST /tenants/this/licenses/renewal

## Пример успешного ответа:

HTTP 200 OK

## Пример ошибки:
```json
[
  {
    "traceIdentifier": "0HMV3B6Q3K2Q1:00000001",
    "code": "LICENSE_RENEWAL_ERROR", 
    "message": "Ошибка при отправке запроса на продление"
  }
]
```

### `DELETE /Tenants/this/licenses/{id}`

## Пример запроса:

DELETE /tenants/this/licenses/1

## Пример успешного ответа:

HTTP 202 Accepted

### `GET /Tenants/this/meta`

## Пример запроса:

GET /tenants/this/meta

## Пример успешного ответа:
```json
{
  "version": "1.0.0",
  "features": ["feature1", "feature2"],
  "settings": {
    "theme": "dark",
    "language": "ru"
  }
}
```

### `POST /Tenants/this/packages`

## Пример запроса:

POST /tenants/this/packages

```json
{
  "packageID": 1,
  "packageVersion": "1.0.0"
}
```

## Пример успешного ответа:
```json
[
  {
    "id": 1,
    "package": {
      "packageID": 1,
      "packageVersion": "1.0.0",
      "packageName": "Расширение отчетности"
    }
  }
]
```

### `PATCH /Tenants/this/packages`

## Пример запроса:

PATCH /tenants/this/packages

```json
{
  "packageID": 1,
  "packageVersion": "1.0.0",
  "newPackageVersion": "1.1.0"
}
```

## Пример успешного ответа:

HTTP 202 Accepted

### `DELETE /Tenants/this/packages`

## Пример запроса:

DELETE /tenants/this/packages

```json
{
  "packageID": 1,
  "packageVersion": "1.0.0"
}
```

## Пример успешного ответа:

HTTP 202 Accepted

### `POST /Tenants/this/packages/tenant`

## Пример запроса:

POST /tenants/this/packages/tenant

```json
{
  "packageID": 1,
  "packageVersion": "1.0.0"
}
```

## Пример успешного ответа:
```json
[
  {
    "id": 1,
    "package": {
      "packageID": 1,
      "packageVersion": "1.0.0",
      "packageName": "Расширение отчетности"
    }
  }
]
```

### `DELETE /Tenants/this/packages/tenant`

## Пример запроса:

DELETE /tenants/this/packages/tenant

```json
{
  "packageID": 1,
  "packageVersion": "1.0.0"
}
```

## Пример успешного ответа:

HTTP 202 Accepted

### `GET /Tenants/this/variables`

## Пример запроса:

GET /tenants/this/variables

## Пример успешного ответа:
```json
{
  "API_URL": {
    "name": "API_URL",
    "value": "https://api.example.com",
    "description": "URL API сервиса"
  },
  "DB_CONNECTION": {
    "name": "DB_CONNECTION",
    "value": "Server=localhost;Database=HubEx",
    "description": "Строка подключения к БД"
  }
}
```

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

### `DELETE /Tenants/this/variables`

## Пример запроса:

DELETE /tenants/this/variables

```json
["API_URL", "DB_CONNECTION"]
```

## Пример успешного ответа:

HTTP 202 Accepted

### `DELETE /Tenants/this/variables/{name}`

## Пример запроса:

DELETE /tenants/this/variables/API_URL

## Пример успешного ответа:

HTTP 202 Accepted

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

### `DELETE /UserAssetListQueries/{userID}`

## Пример запроса:

DELETE /userassetlistqueries/123

```json
[10, 11]
```

## Пример успешного ответа:

HTTP 202 Accepted

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

## Пример ошибки:
```json
[
  {
    "traceIdentifier": "0HMV3B6Q3K2Q1:00000001",
    "code": "NOTIFICATION_UPDATE_ERROR", 
    "message": "Ошибка при изменении настроек уведомлений"
  }
]
```

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
      "isPrimary": true
    },
    {
      "districtID": 2,
      "isPrimary": false
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

## Пример ошибки:
```json
[
  {
    "traceIdentifier": "0HMV3B6Q3K2Q1:00000001",
    "code": "DISTRICT_ADD_ERROR", 
    "message": "Ошибка при добавлении участков"
  }
]
```

### `PUT /UserDistricts`

## Пример запроса:

PUT /userdistricts

```json
{
  "userID": 123,
  "data": [
    {
      "districtID": 1,
      "isPrimary": false
    }
  ]
}
```

## Пример успешного ответа:

HTTP 202 Accepted

## Пример ошибки:
```json
[
  {
    "traceIdentifier": "0HMV3B6Q3K2Q1:00000001",
    "code": "DISTRICT_UPDATE_ERROR", 
    "message": "Ошибка при обновлении участков"
  }
]
```

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

## Пример ошибки:
```json
[
  {
    "traceIdentifier": "0HMV3B6Q3K2Q1:00000001",
    "code": "DISTRICT_DELETE_ERROR", 
    "message": "Ошибка при удалении участков"
  }
]
```

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

## Пример ошибки:
```json
[
  {
    "traceIdentifier": "0HMV3B6Q3K2Q1:00000001",
    "code": "ROLE_ADD_ERROR", 
    "message": "Ошибка при добавлении ролей"
  }
]
```

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

## Пример ошибки:
```json
[
  {
    "traceIdentifier": "0HMV3B6Q3K2Q1:00000001",
    "code": "ROLE_DELETE_ERROR", 
    "message": "Ошибка при удалении ролей"
  }
]
```

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
    "tags": "VIP"
  },
  {
    "userID": 123,
    "tags": "Менеджер"
  }
]
```

## Пример ошибки:
```json
[
  {
    "traceIdentifier": "0HMV3B6Q3K2Q1:00000001",
    "code": "TAG_CONFLICT", 
    "message": "Тег уже существует для пользователя"
  }
]
```

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

## UserTaskListQueries

### `POST /UserTaskListQueries`

## Пример запроса:

POST /usertasklistqueries

```json
[
  {
    "userID": 123,
    "taskListQueryID": 10
  },
  {
    "userID": 123,
    "taskListQueryID": 11
  }
]
```

## Пример успешного ответа:
```json
[
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

### `DELETE /UserTaskListQueries`

## Пример запроса:

DELETE /usertasklistqueries

```json
[
  {
    "userID": 123,
    "taskListQueryID": 10
  }
]
```

## Пример успешного ответа:

HTTP 202 Accepted

## UserTemplateDistricts

### `POST /UserTemplateDistricts`

## Пример запроса:

POST /usertemplatedistricts

```json
[
  {
    "id": 1,
    "data": [10, 11]
  },
  {
    "id": 2,
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

## Пример ошибки:
```json
[
  {
    "traceIdentifier": "0HMV3B6Q3K2Q1:00000001",
    "code": "DISTRICT_ADD_ERROR", 
    "message": "Ошибка при добавлении участков к шаблону"
  }
]
```

### `DELETE /UserTemplateDistricts/remove`

## Пример запроса:

DELETE /usertemplatedistricts/remove

```json
[
  {
    "id": 1,
    "data": [10, 11]
  }
]
```

## Пример успешного ответа:

HTTP 202 Accepted

## Пример ошибки:
```json
[
  {
    "traceIdentifier": "0HMV3B6Q3K2Q1:00000001",
    "code": "DISTRICT_REMOVE_ERROR", 
    "message": "Ошибка при удалении участков из шаблона"
  }
]
```

## UserTemplateRoles

### `POST /UserTemplateRoles`

## Пример запроса:

POST /usertemplateroles

```json
[
  {
    "id": 1,
    "data": [10, 11]
  },
  {
    "id": 2,
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

## Пример ошибки:
```json
[
  {
    "traceIdentifier": "0HMV3B6Q3K2Q1:00000001",
    "code": "ROLE_ADD_ERROR", 
    "message": "Ошибка при добавлении ролей к шаблону"
  }
]
```

### `DELETE /UserTemplateRoles/remove`

## Пример запроса:

DELETE /usertemplateroles/remove

```json
[
  {
    "id": 1,
    "data": [10, 11]
  }
]
```

## Пример успешного ответа:

HTTP 202 Accepted

## Пример ошибки:
```json
[
  {
    "traceIdentifier": "0HMV3B6Q3K2Q1:00000001",
    "code": "ROLE_REMOVE_ERROR", 
    "message": "Ошибка при удалении ролей из шаблона"
  }
]
```

## UserTemplates

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

## Пример ошибки:
```json
[
  {
    "traceIdentifier": "0HMV3B6Q3K2Q1:00000001",
    "code": "TEMPLATE_CONFLICT", 
    "message": "Конфликт при обновлении шаблона"
  }
]
```

### `DELETE /UserTemplates`

## Пример запроса:

DELETE /usertemplates

```json
[1, 2, 3]
```

## Пример успешного ответа:

HTTP 202 Accepted

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

### `DELETE /UserTemplates/{id}`

## Пример запроса:

DELETE /usertemplates/1

## Пример успешного ответа:

HTTP 202 Accepted

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

## UserWarehouses

### `POST /UserWarehouses`

## Пример запроса:

POST /userwarehouses

```json
[
  {
    "userID": 123,
    "warehouseID": 1
  },
  {
    "userID": 123,
    "warehouseID": 2
  }
]
```

## Пример успешного ответа:
```json
{
  "123": [1, 2]
}
```

## Пример ошибки:
```json
[
  {
    "traceIdentifier": "0HMV3B6Q3K2Q1:00000001",
    "code": "WAREHOUSE_ADD_ERROR", 
    "message": "Ошибка при добавлении складов"
  }
]
```

⚠️ **Устаревший метод**: Используйте POST /WH/WarehouseUser/s

### `DELETE /UserWarehouses`

## Пример запроса:

DELETE /userwarehouses

```json
[
  {
    "userID": 123,
    "warehouseID": 1
  }
]
```

## Пример успешного ответа:

HTTP 202 Accepted

## Пример ошибки:
```json
[
  {
    "traceIdentifier": "0HMV3B6Q3K2Q1:00000001",
    "code": "WAREHOUSE_DELETE_ERROR", 
    "message": "Ошибка при удалении складов"
  }
]
```

⚠️ **Устаревший метод**: Используйте DELETE /WH/WarehouseUser/

## Users

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
  "mobilePhone": null,
  "workPhone": null,
  "isTechnician": true,
  "isTeam": false,
  "isCustomer": true,
  "mobilityID": 1,
  "geotrackingModeID": 1,
  "isBanned": false,
  "banReasonID": null,
  "banTill": null,
  "isEmailVerified": false,
  "isMobilePhoneVerified": false,
  "companyID": 2,
  "rate": 1500.00,
  "rateCurrencyID": 1
}
```

## Пример успешного ответа:
```json
{
  "userID": 123,
  "accountID": 456,
  "tenantMemberID": 789
}
```

## Пример ошибки:
```json
[
  {
    "traceIdentifier": "0HMV3B6Q3K2Q1:00000001",
    "code": "USER_ALREADY_EXISTS", 
    "message": "Пользователь с таким email уже существует"
  }
]
```

### `DELETE /Users`

## Пример запроса:

DELETE /users

```json
[123, 456, 789]
```

## Пример успешного ответа:

HTTP 202 Accepted

## Пример ошибки:
```json
[
  {
    "traceIdentifier": "0HMV3B6Q3K2Q1:00000001",
    "code": "USER_HAS_ACTIVE_TASKS", 
    "message": "Невозможно удалить пользователя с ID 123, у которого есть активные заявки"
  }
]
```

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
  "mobilePhone": null,
  "workPhone": null,
  "isTechnician": true,
  "isTeam": false,
  "isCustomer": true,
  "mobilityID": 1,
  "geotrackingModeID": 1,
  "isBanned": false,
  "banReasonID": null,
  "banTill": null,
  "isEmailVerified": false,
  "isMobilePhoneVerified": false,
  "companyID": 2,
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
    "code": "USER_ALREADY_EXISTS", 
    "message": "Пользователь с таким email уже существует"
  }
]
```

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

### `POST /Users/changeToCustomer`

## Пример запроса:

POST /users/changeToCustomer

```json
[123, 456, 789]
```

## Пример успешного ответа:

HTTP 202 Accepted

## Пример ошибки:
```json
{
  "traceIdentifier": "0HMV3B6Q3K2Q1:00000001",
  "code": "USER_NOT_FOUND", 
  "message": "Пользователь с ID 999 не найден"
}
```

### `POST /Users/changeToStaff`

## Пример запроса:

POST /users/changeToStaff

```json
[123, 456, 789]
```

## Пример успешного ответа:

HTTP 202 Accepted

## Пример ошибки:
```json
{
  "traceIdentifier": "0HMV3B6Q3K2Q1:00000001",
  "code": "USER_NOT_FOUND", 
  "message": "Пользователь с ID 999 не найден"
}
```

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

### `DELETE /Users/defaultPages`

## Пример запроса:

DELETE /users/defaultPages

```json
[123, 124, 125]
```

## Пример успешного ответа:

HTTP 202 Accepted

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
      "company": "ООО Пример",
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

### `POST /Users/registration`

## Пример запроса:

POST /users/registration

```json
{
  "invitationID": "abc123",
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

## Пример ошибки:
```json
[
  {
    "traceIdentifier": "0HMV3B6Q3K2Q1:00000001",
    "code": "INVITATION_INVALID", 
    "message": "Приглашение недействительно или истекло"
  }
]
```

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

### `PUT /Users/restore`

## Пример запроса:

PUT /users/restore

```json
[123, 456, 789]
```

## Пример успешного ответа:

HTTP 202 Accepted

## Пример ошибки:
```json
[
  {
    "traceIdentifier": "0HMV3B6Q3K2Q1:00000001",
    "code": "USER_ALREADY_RESTORED", 
    "message": "Пользователь с ID 123 уже восстановлен"
  }
]
```

### `GET /Users/this/assetListQueries`

## Пример запроса:

GET /users/this/assetListQueries

## Пример успешного ответа:
```json
{
  "1": {
    "id": 1,
    "name": "Мои объекты",
    "isDefault": true,
    "isFavorite": false
  }
}
```

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
      "company": "ООО Пример",
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

### `GET /Users/this/taskListQueries`

## Пример запроса:

GET /users/this/taskListQueries

## Пример успешного ответа:
```json
{
  "1": {
    "id": 1,
    "name": "Мои заявки",
    "isDefault": true,
    "isFavorite": false
  }
}
```

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

## Пример ошибки:
```json
{
  "traceIdentifier": "0HMV3B6Q3K2Q1:00000001",
  "code": "USER_NOT_FOUND", 
  "message": "Пользователь с ID 999 не найден"
}
```

### `GET /Users/{id}/assetListQueries`

## Пример запроса:

GET /users/123/assetListQueries

## Пример успешного ответа:
```json
{
  "1": {
    "id": 1,
    "name": "Мои объекты",
    "isDefault": true,
    "isFavorite": false
  }
}
```

### `GET /Users/{id}/districts`

## Пример запроса:

GET /users/123/districts

## Пример успешного ответа:
```json
{
  "1": {
    "id": 1,
    "name": "Центральный район",
    "parentID": null
  },
  "2": {
    "id": 2,
    "name": "Северный район",
    "parentID": 1
  }
}
```

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
      "company": "ООО Пример",
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

### `GET /Users/{id}/taskListQueries`

## Пример запроса:

GET /users/123/taskListQueries

## Пример успешного ответа:
```json
{
  "1": {
    "id": 1,
    "name": "Мои заявки",
    "isDefault": true,
    "isFavorite": false
  }
}
```

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

### `DELETE /Users/{userID}`

## Пример запроса:

DELETE /users/123

## Пример успешного ответа:

HTTP 202 Accepted

## Пример ошибки:
```json
[
  {
    "traceIdentifier": "0HMV3B6Q3K2Q1:00000001",
    "code": "USER_HAS_ACTIVE_TASKS", 
    "message": "Невозможно удалить пользователя, у которого есть активные заявки"
  }
]
```

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
      "dateFrom": "2024-01-01T00:00:00Z",
      "dateTill": "2024-12-31T23:59:59Z"
    },
    "notes": "Основной объект"
  }
]
```

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

### `DELETE /Users/{userID}/attributes`

## Пример запроса:

DELETE /users/123/attributes

```json
[1, 2, 3]
```

## Пример успешного ответа:

HTTP 202 Accepted

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

### `POST /Users/{userID}/geolocation`

## Пример запроса:

POST /users/123/geolocation?coordinateAccuracyID=1

## Пример успешного ответа:

HTTP 201 Created

### `PUT /Users/{userID}/geolocation`

## Пример запроса:

PUT /users/123/geolocation?coordinateAccuracyID=2

## Пример успешного ответа:

HTTP 202 Accepted

### `PUT /Users/{userID}/resendinvitation`

## Пример запроса:

PUT /users/123/resendinvitation

## Пример успешного ответа:

HTTP 202 Accepted

## Пример ошибки:
```json
{
  "traceIdentifier": "0HMV3B6Q3K2Q1:00000001",
  "code": "USER_NOT_FOUND", 
  "message": "Пользователь не найден"
}
```

### `PUT /Users/{userID}/restore`

## Пример запроса:

PUT /users/123/restore

## Пример успешного ответа:

HTTP 202 Accepted

## Пример ошибки:
```json
[
  {
    "traceIdentifier": "0HMV3B6Q3K2Q1:00000001",
    "code": "USER_ALREADY_RESTORED", 
    "message": "Пользователь с ID 123 уже восстановлен"
  }
]
```

### `GET /Users/{userID}/skills`

## Пример запроса:

GET /users/123/skills

## Пример успешного ответа:
```json
{
  "1": {
    "skillID": 1,
    "dateFrom": "2024-01-01T00:00:00Z",
    "dateTill": "2024-12-31T23:59:59Z"
  },
  "2": {
    "skillID": 2,
    "dateFrom": "2024-01-01T00:00:00Z",
    "dateTill": null
  }
}
```

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
