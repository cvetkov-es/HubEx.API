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

## TenantMembers

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
  "realm": "example",
  "managerFullName": "Иванов Иван",
  "managerPhone": "+79998887766",
  "managerEmail": "manager@hubex.ru"
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

## UserTemplates

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

## Users

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
