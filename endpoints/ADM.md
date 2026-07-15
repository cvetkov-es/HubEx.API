# ADM — справочник ручек

> **Что здесь:** все ручки сервиса ADM (HubEx ADM APIs): сигнатуры, параметры, права. Типы — schemas/ADM.md. Сгенерировано из swagger.
> **Когда сюда идти:** найти ручку и её вход/выход. Типы — `schemas/ADM.md`; грабли — `notes/ADM.md` (если есть).
> **Источник:** swagger сервиса ADM · файл генерируется пайплайном — руками не править.

Base: `{BASE_URL}/ADM`

## BanReasons
- `GET /BanReasons` — Получить список причин блокировки пользователя · коды: 200, 204, 206
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → map<ResultsBanReasonsListResult>
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
- `GET /Capabilities` — Получить список возможностей работы с элементами интерфейса · коды: 200, 204, 206
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → map<ResultsCapabilitiesListResult>
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
- `GET /DefaultPages` — Получить список доступных стартовых страниц · коды: 200, 204, 400
  ← query: applicationID?:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → ResultsDefaultPagesAllowedPageResult[]
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
- `GET /GeolocationSettings/coordinateAccuracy` — Получить список настроек точности сбора геокоординат · коды: 200, 204
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → IdNameDescriptionEntityOfByte[]
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
- `GET /Invitations` · paginated · коды: 200, 204, 206
  ← query: userTemplateID?:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → map<ResultsInvitationsGetResult>
- `POST /Invitations` — Создать приглашения · коды: 201, 202, 400
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: ADMInvitationAddData[] → ResultsInvitationsAddResult[]
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
- `PUT /Invitations` — Обновить приглашения · коды: 202, 400
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: ADMInvitationUpdateData[]
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
- `DELETE /Invitations` — Удалить приглашения · коды: 202, 400
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: uuid[]
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
- `GET /Invitations/{id}` — Получить расширенную информацию о приглашении · коды: 200
  ← path: id:uuid; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → ResultsInvitationsGetResult
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
- `DELETE /Invitations/{id}` — Удалить приглашение · коды: 202
  ← path: id:uuid; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb)
  ## Пример запроса:

DELETE /invitations/123e4567-e89b-12d3-a456-426614174000

## Пример успешного ответа:

HTTP 202 Accepted
- `GET /Invitations/{id}/short` — Получить сокращенную информацию о приглашении · коды: 200
  ← path: id:uuid; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → ResultsInvitationsGetShortResult
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
- `GET /PermissionApiTags` — Получить список тегов API-полномочий · коды: 200, 204, 206
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → map<ResultsPermissionsApiTagListResult[]>
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
- `GET /PermissionExtTags` — Получить список тегов расширенных полномочий · коды: 200, 204, 206
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → map<ResultsPermissionsExtTagListResult[]>
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
- `GET /PermissionsApi` — Получить список API-полномочий · коды: 200, 204, 206
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → map<ResultsPermissionsApiListResult>
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
- `GET /PermissionsExt` — Получить список расширенных полномочий · коды: 200, 204, 206
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → map<ResultsPermissionsExtListResult>

## PermissionsUi
- `GET /PermissionsUi` — Получить список UI полномочий · коды: 200, 204, 206
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → map<ResultsPermissionsUiGetResult>
- `POST /PermissionsUi` — Создать UI полномочия · коды: 201, 400
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: ADMPermissionUiAddData[] → int[]
- `PUT /PermissionsUi` — Обновить UI полномочия · коды: 202, 400
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: ADMPermissionUiUpdateData[]
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
- `DELETE /PermissionsUi` — Удалить UI полномочия · коды: 202, 400
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: int[]
  ## Пример запроса:

DELETE /permissionsui

```json
[1, 2, 3]
```

## Пример успешного ответа:

HTTP 202 Accepted
- `GET /PermissionsUi/{id}` — Получить данные UI полномочия · коды: 200, 204, 206
  ← path: id:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → ResultsPermissionsUiGetResult
- `DELETE /PermissionsUi/{id}` — Удалить UI полномочие · коды: 202
  ← path: id:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb)
  ## Пример запроса:

DELETE /permissionsui/1

## Пример успешного ответа:

HTTP 202 Accepted

## RoleApplications
- `POST /RoleApplications` — Добавить или обновить приложения для ролей · коды: 201, 400
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: RoleApplicationBaseBaseData[] → ResultsRoleApplicationMergeResult[]
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
- `DELETE /RoleApplications` — Удалить приложения для ролей · коды: 202, 400
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: RoleApplicationBaseBaseData[]
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
- `POST /RoleAttachments` — Добавить роли для доступа к файлам · коды: 201, 400
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: ADMRoleAttachmentAddData[] → ResultsRoleAttachmentsPostResult[]
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
- `DELETE /RoleAttachments` — Удалить доступ ролей к файлам · коды: 202, 400
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: ADMRoleAttachmentDeleteData[]
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
- `POST /RolePermissionsApi` — Создать связи роли с API-полномочиями · коды: 201, 400
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: ADMRolePermissionApiAddData[] → ResultsRolePermissionsApiPostResult[]
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
- `DELETE /RolePermissionsApi` — Удалить связи роли с API-полномочиями · коды: 202, 400
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: ADMRolePermissionApiDeleteData[]
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
- `POST /RolePermissionsExt` — Создать связи роли с Ext-полномочиями · коды: 201, 400
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: ADMRolePermissionExtAddData[] → ResultsRolePermissionsExtPostResult[]
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
- `DELETE /RolePermissionsExt` — Удалить связи роли с Ext-полномочиями · коды: 202, 400
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: ADMRolePermissionExtDeleteData[]
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
- `POST /RolePermissionsUi` — Создать связи роли с UI-полномочиями · коды: 201, 400
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: ADMRolePermissionUiAddData[] → ResultsRolePermissionsUiPostResult[]
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
- `DELETE /RolePermissionsUi` — Удалить связи роли с UI-полномочиями · коды: 202, 400
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: ADMRolePermissionUiDeleteData[]
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
- `POST /RoleTaskListQueries` — Добавить сохраненные запросы заявок для роли · коды: 201, 400
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: ADMRoleTaskListQueryAddData[] → ResultsRoleTaskListQueriesPostResult[]
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
- `DELETE /RoleTaskListQueries` — Удалить сохраненные запросы заявок у роли · коды: 202, 400
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: ADMRoleTaskListQueryDeleteData[]
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
- `GET /RoleTaskPropertiesAccess/attributes` · paginated · коды: 200, 204, 206
  ← query: roleID?:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → ResultsRoleTaskAttributeRoleTaskAttributeSettings[]
- `POST /RoleTaskPropertiesAccess/attributes` — Добавить настройки доступности атрибутов задач для ролей · коды: 201, 400
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: DataADMRoleTaskAttributeDto[]
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
- `PUT /RoleTaskPropertiesAccess/attributes` — Обновить настройки доступности атрибутов задач для ролей · коды: 202, 400
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: DataADMRoleTaskAttributeDto[]
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
- `GET /Roles` — Получить список ролей тенанта · коды: 200, 204, 206
  ← query: isDeleted?:bool; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → map<ResultsRolesGetResult>
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
- `POST /Roles` — Создать роли · коды: 201, 400
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: ADMRoleAddData[] → int[]
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
- `PUT /Roles` — Обновить роли · коды: 202, 400
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: ADMRoleUpdateData[]
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
- `DELETE /Roles` — Удалить роли · коды: 202, 400
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: int[]
  ## Пример запроса:

DELETE /roles

```json
[1, 2, 3]
```

## Пример успешного ответа:

HTTP 202 Accepted
- `POST /Roles/copy` — Копировать роли · коды: 201, 400
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: ADMRoleCopyData[] → int[]
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
- `GET /Roles/{id}` — Получить информацию о роли · коды: 200, 204
  ← path: id:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → ResultsRolesGetResult
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
- `DELETE /Roles/{id}` — Удалить роль · коды: 202
  ← path: id:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb)
  ## Пример запроса:

DELETE /roles/1

## Пример успешного ответа:

HTTP 202 Accepted
- `GET /Roles/{roleID}/applications` — Получить список приложений роли · коды: 200, 204, 206
  ← path: roleID:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → map<ResultsRoleApplicationListResult>
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
- `GET /Roles/{roleID}/attachments` — Получить список вложенных файлов роли · коды: 200, 204, 206
  ← path: roleID:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → ResultsCommonAttachmentResult[]
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
- `GET /Roles/{roleID}/packages` — Получить список расширений роли · коды: 200, 204, 206
  ← path: roleID:int; query: searchText?:str; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → map<ResultsRolePackagesListResult[]>
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
- `POST /Roles/{roleID}/packages` — Добавить расширения к роли · коды: 201, 400
  ← path: roleID:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: ADMRolePackageAddData[] → ResultsRolePackagesPostResult[]
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
- `DELETE /Roles/{roleID}/packages` — Удалить расширения роли · коды: 202, 400
  ← path: roleID:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: int[]
  ## Пример запроса:

DELETE /roles/1/packages

```json
[1, 2, 3]
```

## Пример успешного ответа:

HTTP 202 Accepted
- `PUT /Roles/{roleID}/packages/activate` — Активировать расширения роли · коды: 202, 400
  ← path: roleID:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: int[]
  ## Пример запроса:

PUT /roles/1/packages/activate

```json
[1, 2, 3]
```

## Пример успешного ответа:

HTTP 202 Accepted
- `PUT /Roles/{roleID}/packages/deactivate` — Деактивировать расширения роли · коды: 202, 400
  ← path: roleID:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: int[]
  ## Пример запроса:

PUT /roles/1/packages/deactivate

```json
[1, 2, 3]
```

## Пример успешного ответа:

HTTP 202 Accepted
- `GET /Roles/{roleID}/permissionsApi` — Получить список API-полномочий роли · коды: 200, 204, 206
  ← path: roleID:int; query: systemTagID?:str, isCheckedPermission?:bool; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → map<ResultsRolePermissionsApiListResult[]>
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
- `GET /Roles/{roleID}/permissionsExt` — Получить список Ext-полномочий роли · коды: 200, 204, 206
  ← path: roleID:int; query: systemTagID?:str, isCheckedPermission?:bool; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → map<ResultsRolePermissionsExtListResult[]>
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
- `GET /Roles/{roleID}/permissionsUi` — Получить список UI-полномочий роли · коды: 200, 204, 206
  ← path: roleID:int; query: systemTagID?:int, isCheckedPermission?:bool, isSystemPermission?:bool; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → map<ResultsRolePermissionsUiListResult[]>
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
- `GET /SystemPermissionUiTags` — Получить список тегов системных UI-полномочий · коды: 200, 204, 206
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → map<ResultsPermissionsUiTagListResult[]>
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
- `POST /TenantCreationRequests` — Создать запрос на создание тенанта · коды: 201, 400
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: ADMTenantCreationRequestAddData → ResultsTenantCreationRequestsPostResult
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
- `GET /TenantCreationRequests/{id}` — Получить запрос на создание тенанта · коды: 200
  ← path: id:str; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → ResultsTenantCreationRequestsGetResult
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
- `PUT /TenantCreationRequests/{id}/approve` — Утвердить запрос на создание тенанта · коды: 202, 400
  ← path: id:str; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb)
  ## Пример запроса:

PUT /tenantcreationrequests/abc123/approve

## Пример успешного ответа:

HTTP 202 Accepted

Доступно только для кросс-тенантных администраторов.
- `PUT /TenantCreationRequests/{id}/reject` — Отклонить запрос на создание тенанта · коды: 202, 400
  ← path: id:str; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: ADMTenantCreationRequestRejectData
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
- `GET /TenantMembers` · paginated · коды: 200, 204, 206
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → map<ResultsTenantMembersListResult>
- `POST /TenantMembers` — Создать члена тенанта · коды: 201, 400
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: ADMTenantMemberAddData[] → int[]
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
- `PUT /TenantMembers` — Обновить данные члена тенанта · коды: 202, 400
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: ADMTenantMemberUpdateData[]
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
- `DELETE /TenantMembers` — Удалить членов тенанта · коды: 202, 400
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: int[]
  ## Пример запроса:

DELETE /tenantmembers

```json
[123, 124, 125]
```

## Пример успешного ответа:

HTTP 202 Accepted
- `GET /TenantMembers/anonymousUser` — Получить анонимного пользователя в текущем тенанте · коды: 200, 204
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → ResultsTenantMembersListResult
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
- `GET /TenantMembers/apiUser` — Получить пользователя API в текущем тенанте · коды: 200, 204
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → ResultsTenantMembersListResult
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
- `GET /TenantMembers/this` — Получить данные текущего члена тенанта · коды: 200
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → ResultsTenantMembersGetResult
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
- `GET /TenantMembers/{tenantMemberID}` — Получить данные члена тенанта · коды: 200, 500
  ← path: tenantMemberID:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → ResultsTenantMembersGetResult
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
- `DELETE /TenantMembers/{tenantMemberID}` — Удалить члена тенанта · коды: 202
  ← path: tenantMemberID:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb)
  ## Пример запроса:

DELETE /tenantmembers/123

## Пример успешного ответа:

HTTP 202 Accepted

## TenantSettings
- `GET /TenantSettings` — Получить настройки тенанта · коды: 200, 204, 500
  ← query: tenantMemberId?:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → ResultsTenantSettingsGetResult
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
- `GET /TenantSettings/plateUrl` — Получить кастомный URL текущего тенанта · коды: 200, 204
  ← query: taskTemplateID?:str; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → str
  ## Пример запроса:

GET /tenantsettings/this/plateUrl?taskTemplateID=123

## Пример успешного ответа:
```json
"https://plate.hubex.ru"
```
- `PUT /TenantSettings/plateUrl` — Обновить кастомный URL текущего тенанта · коды: 202
  ← query: plateUrl?:str; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb)
  ## Пример запроса:

PUT /tenantsettings/this/plateUrl?plateUrl=https://client-domain.ru

### NULL
Если параметр `plateUrl` не передали, будет сохранен `NULL`.

## Пример успешного ответа:

HTTP 202 Accepted

## Tenants
- `GET /Tenants` — Получить список тенантов · коды: 200, 204, 206
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → ResultsTenantsListResult[]
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
- `PUT /Tenants/licenses` — Обновить лицензию тенанта · коды: 202, 400
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: ADMTenantLicenseUpdateData
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
- `GET /Tenants/templates` — Получить список шаблонных тенантов · коды: 200, 204, 206
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → InterfacesEntitiesITenantEntity[]
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
- `GET /Tenants/this` — Получить данные текущего тенанта · коды: 200
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → ResultsTenantsGetResult
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
- `GET /Tenants/this/featureFlags` — Получить список флагов функций тенанта · коды: 200, 204
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → str[]
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
- `GET /Tenants/this/licenses` — Получить список лицензий тенанта · коды: 200, 204
  ← query: validOn?:datetime; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → ResultsTenantLicenseListTenantLicenseResult
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
- `POST /Tenants/this/licenses` — Добавить лицензию для тенанта · коды: 201, 400
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: ADMTenantLicenseAddData
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
- `DELETE /Tenants/this/licenses` — Удалить лицензии тенанта · коды: 202, 400
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: int[]
  ## Пример запроса:

DELETE /tenants/this/licenses

```json
[1, 2, 3]
```

## Пример успешного ответа:

HTTP 202 Accepted
- `POST /Tenants/this/licenses/renewal` — Отправить запрос на продление лицензии · коды: 200, 500
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb)
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
- `DELETE /Tenants/this/licenses/{id}` — Удалить лицензию тенанта · коды: 202
  ← path: id:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb)
  ## Пример запроса:

DELETE /tenants/this/licenses/1

## Пример успешного ответа:

HTTP 202 Accepted
- `GET /Tenants/this/meta` — Получить метаданные тенанта · коды: 200, 204
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb)
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
- `GET /Tenants/this/packages` · paginated · коды: 200, 204, 206
  ← query: resourceID?:int[]; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → ResultsTenantPackagesListResult[]
  Для выполнения данного метода пользователь должен быть **TenantMember**.
- `POST /Tenants/this/packages` — Добавить расширение (только для кросс-тенантных администраторов) · коды: 200, 204, 206, 400
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: ADDONPackageAddData → ResultsTenantPackagesListResult[]
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
- `PATCH /Tenants/this/packages` — Обновить расширение (только для кросс-тенантных администраторов) · коды: 202, 400
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: ADDONPackageUpdateData
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
- `DELETE /Tenants/this/packages` — Удалить расширение (только для кросс-тенантных администраторов) · коды: 202, 400
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: ADDONPackagePackageIdentifier
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
- `POST /Tenants/this/packages/tenant` — Добавить расширение для тенанта · коды: 200, 204, 206, 400
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: ADDONPackageAddTenantPackageData → ResultsTenantPackagesListResult[]
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
- `DELETE /Tenants/this/packages/tenant` — Удалить расширение для тенанта · коды: 202, 400
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: ADDONPackagePackageIdentifier
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
- `GET /Tenants/this/variables` — Получить список переменных окружения тенанта · коды: 200, 204, 206
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → map<ResultsTenantVariablesListResult>
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
- `POST /Tenants/this/variables` — Добавить переменные окружения тенанта · коды: 201, 400
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: ADMTenantVariableAddData[]
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
- `PUT /Tenants/this/variables` — Обновить переменные окружения тенанта · коды: 202, 400
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: ADMTenantVariableUpdateData[]
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
- `DELETE /Tenants/this/variables` — Удалить переменные окружения тенанта · коды: 202, 400
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: str[]
  ## Пример запроса:

DELETE /tenants/this/variables

```json
["API_URL", "DB_CONNECTION"]
```

## Пример успешного ответа:

HTTP 202 Accepted
- `DELETE /Tenants/this/variables/{name}` — Удалить переменную окружения тенанта · коды: 202
  ← path: name:str; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb)
  ## Пример запроса:

DELETE /tenants/this/variables/API_URL

## Пример успешного ответа:

HTTP 202 Accepted

## UserAssetListQueries
- `POST /UserAssetListQueries` — Добавить сохраненные запросы объектов пользователям · коды: 201, 400
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: ADMUserAssetListQueryAddData[] → ResultsUserAssetListQueriesPostResult[]
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
- `DELETE /UserAssetListQueries` — Удалить сохраненные запросы объектов у пользователей · коды: 202, 400
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: ADMUserAssetListQueryDeleteData[]
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
- `POST /UserAssetListQueries/{userID}` — Добавить сохраненные запросы объектов пользователю · коды: 201, 400
  ← path: userID:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: int[] → ResultsUserAssetListQueriesPostResult[]
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
- `DELETE /UserAssetListQueries/{userID}` — Удалить сохраненные запросы объектов у пользователя · коды: 202, 400
  ← path: userID:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: int[]
  ## Пример запроса:

DELETE /userassetlistqueries/123

```json
[10, 11]
```

## Пример успешного ответа:

HTTP 202 Accepted

## UserCompanyListQueries
- `POST /UserCompanyListQueries` — Добавляет сохраненные запросы пользователям · коды: 201
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: ADMUserCompanyListQueryAddData[] → ResultsUserCompanyListQueriesPostResult[]
- `DELETE /UserCompanyListQueries` — Помечает как удалённые сохраненные запросы для пользователей · коды: 202
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: ADMUserCompanyListQueryDeleteData[]
- `POST /UserCompanyListQueries/{userID}` — Добавляет сохраненные запросы пользователю · коды: 201
  ← path: userID:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: int[] → ResultsUserCompanyListQueriesPostResult[]
- `DELETE /UserCompanyListQueries/{userID}` — Помечает как удалённые сохраненные запросы для пользователя · коды: 202
  ← path: userID:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: int[]

## UserDisabledNotifications
- `POST /UserDisabledNotifications` — Изменить настройки уведомлений пользователя · коды: 202, 204, 400, 500
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: DataUserDisabledNotificationsPostData → ResultsUserDisabledNotificationsMergeResult[]
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
- `POST /UserDistricts` — Добавить участки пользователю · коды: 201, 400, 500
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: OperationDataOfAddData
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
- `PUT /UserDistricts` — Обновить участки у пользователя · коды: 202, 400, 500
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: OperationDataOfUpdateData
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
- `DELETE /UserDistricts` — Удалить участки у пользователя · коды: 202, 400, 500
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: OperationDataOfShort
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
- `GET /UserOrderBy` — Получить список методов сортировки сотрудников · коды: 200, 204, 206
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → map<ResultsUserOrderByListResult>
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
- `POST /UserRoles` — Добавить роли пользователю · коды: 201, 400, 500
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: DataUserRolesPostData[]
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
- `DELETE /UserRoles` — Удалить роли у пользователя · коды: 202, 400, 500
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: DataUserRolesDeleteData[]
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
- `POST /UserTags` — Добавить теги пользователю · коды: 201, 400, 409
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: DataUserTagsPostData[] → ResultsUserTagAddResult[]
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
- `DELETE /UserTags` — Удалить теги пользователя · коды: 202, 400
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: DataUserTagsDeleteData[]
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
- `POST /UserTaskListQueries` — Добавить сохраненные запросы заявок пользователям · коды: 201, 400
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: ADMUserTaskListQueryAddData[] → ResultsUserTaskListQueriesPostResult[]
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
- `DELETE /UserTaskListQueries` — Удалить сохраненные запросы заявок у пользователей · коды: 202, 400
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: ADMUserTaskListQueryDeleteData[]
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
- `POST /UserTemplateDistricts` — Добавить участки к шаблону пользователя · коды: 201, 400, 500
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: ActionDataOfShort[]
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
- `DELETE /UserTemplateDistricts/remove` — Удалить участки из шаблона пользователя · коды: 202, 400, 500
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: ActionDataOfShort[]
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
- `POST /UserTemplateRoles` — Добавить роли к шаблону пользователя · коды: 201, 400, 500
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: ActionDataOfShort[]
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
- `DELETE /UserTemplateRoles/remove` — Удалить роли из шаблона пользователя · коды: 202, 400, 500
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: ActionDataOfShort[]
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
- `GET /UserTemplates` · paginated · коды: 200, 204, 206
  ← query: searchText?:str, isTechnician?:bool, roleID?:int, districtID?:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → map<ResultsUserTemplatesListResult>
- `POST /UserTemplates` — Создать шаблон пользователя · коды: 201, 400
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: ADMUserTemplateAddData[] → int[]
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
- `PUT /UserTemplates` — Обновить шаблон пользователя · коды: 202, 400, 409
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: ADMUserTemplateUpdateData[]
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
- `DELETE /UserTemplates` — Удалить шаблоны пользователя · коды: 202, 400
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: int[]
  ## Пример запроса:

DELETE /usertemplates

```json
[1, 2, 3]
```

## Пример успешного ответа:

HTTP 202 Accepted
- `GET /UserTemplates/{id}` — Получить шаблон пользователя · коды: 200, 204
  ← path: id:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → ResultsUserTemplatesGetResult
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
- `DELETE /UserTemplates/{id}` — Удалить шаблон пользователя · коды: 202
  ← path: id:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb)
  ## Пример запроса:

DELETE /usertemplates/1

## Пример успешного ответа:

HTTP 202 Accepted
- `GET /UserTemplates/{id}/districts` — Получить список участков шаблона пользователя · коды: 200, 204, 206
  ← path: id:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → IdNameResultOfShort[]
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
- `GET /UserTemplates/{id}/roles` — Получить список ролей шаблона пользователя · коды: 200, 204, 206
  ← path: id:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → IdNameResultOfShort[]
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
- `POST /UserWarehouses` — Добавить склады пользователю · коды: 201, 400, 500
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: WHWarehouseUserUserWarehousesData[]
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
- `DELETE /UserWarehouses` — Удалить склады у пользователя · коды: 202, 400, 500
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: WHWarehouseUserUserWarehousesData[]
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
- `GET /Users` — Возвращает список пользователей · paginated · коды: 200, 206
  ← query: searchText?:str, includeTaskActuality?:bool, includeDistricts?:bool, needForAllowedTasks?:bool, orgUnitID?:int, districtID?:int, userID?:int, workTypeID?:int, skillID?:int, tag?:str, isDeleted?:bool, isCustomer?:bool, isTeam?:bool, isTechnician?:bool, isBanned?:bool, isOnShift?:bool, firstName?:str, lastName?:str, middleName?:str, position?:str, userTypeID?:int, companyID?:int, orderBy?:int, sortDirection?:int, erpID?:str, roleID?:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → map<ResultsUsersUserResult>
- `POST /Users` — Добавить нового пользователя · коды: 201, 400, 409
  ← query: skipAccountVerification?:bool, skipAccountVerification?:bool; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: ADMUserAddData → ProjectionsADMUserAddProjection
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
- `DELETE /Users` — Удалить нескольких пользователей · коды: 202, 409
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: int[]
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
- `HEAD /Users` — Возвращает заголовок запроса пользователей с количеством данных, удовлетворяющих фильтру · коды: 200
  ← query: orgUnitID?:int, districtID?:int, userID?:int, workTypeID?:int, skillID?:int, tag?:str, isDeleted?:bool, isCustomer?:bool, isTeam?:bool, isTechnician?:bool, firstName?:str, lastName?:str, middleName?:str, position?:str, userTypeID?:int, erpID?:str; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb)
- `POST /Users/addbyintegration` — Добавить нового пользователя через интеграцию · коды: 200, 400, 409
  ← query: skipAccountVerification?:bool, skipAccountVerification?:bool; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: ADMUserAddData → ProjectionsADMUserRoleAddProjection[]
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
- `POST /Users/anonymous` — Создать анонимного пользователя в тенанте · коды: 201
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → DataUsersServiceUserResult
  ## Пример запроса:

POST /users/anonymous

## Пример успешного ответа:
```json
{
  "userID": 123,
  "tenantMemberID": 456
}
```
- `POST /Users/api` — Создать API-пользователя в тенанте · коды: 201
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → DataUsersServiceUserResult
  ## Пример запроса:

POST /users/api

## Пример успешного ответа:
```json
{
  "userID": 123,
  "tenantMemberID": 456
}
```
- `GET /Users/attributes` — Получить список атрибутов пользователей · коды: 200, 204, 206
  ← query: attributeID?:int, userID?:int, IsRelevantForCustomer?:bool, IsRelevantForTechnician?:bool; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → ResultsUserAttributeUserAttributesResult[]
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
- `POST /Users/attributes` — Создать атрибуты для пользователей · коды: 201, 400
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: UserActionDataOfAttributeData[]
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
- `PUT /Users/attributes` — Обновить атрибуты пользователей · коды: 202, 400
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: UserActionDataOfAttributeData[]
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
- `DELETE /Users/attributes` — Удалить атрибуты пользователей · коды: 202, 400
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: UserActionDataOfShort[]
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
- `DELETE /Users/avatar` — Удаляет аватку для указанного списка пользователей. · коды: 202
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: int[]
- `POST /Users/changeToCustomer` — Изменить тип пользователя на заказчика · коды: 202, 400
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: int[]
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
- `POST /Users/changeToStaff` — Изменить тип пользователя на сотрудника · коды: 202, 400
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: int[]
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
- `POST /Users/defaultPages` — Добавить стартовые страницы пользователей · коды: 201, 400, 409
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: ADMUserDefaultPagesUserStartPageDto[]
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
- `PUT /Users/defaultPages` — Изменить стартовые страницы пользователей · коды: 202, 400, 404
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: ADMUserDefaultPagesUserStartPageDto[]
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
- `DELETE /Users/defaultPages` — Сбросить стартовые страницы у пользователей · коды: 202, 400
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: int[]
  ## Пример запроса:

DELETE /users/defaultPages

```json
[123, 124, 125]
```

## Пример успешного ответа:

HTTP 202 Accepted
- `GET /Users/geolocation` — Получить список настроек точности сбора геокоординат для пользователей · коды: 200, 204, 206
  ← query: userID?:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → ResultsCoordinateAccuracyUserGeolocationSettings[]
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
- `POST /Users/geolocation` — Добавить настройки точности сбора геокоординат для пользователей · коды: 201, 400
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: DataADMUserGeolocationDto[]
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
- `PUT /Users/geolocation` — Обновить настройки точности сбора геокоординат для пользователей · коды: 202, 400
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: DataADMUserGeolocationDto[]
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
- `GET /Users/profile` — Получить профиль пользователя · коды: 200, 404
  ← query: tenantMemberId?:int, userId?:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → ResultsUsersUserProfileResult
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
- `POST /Users/registration` — Саморегистрация пользователя по приглашению · коды: 201, 202, 409
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: DataUsersRegisterData → ResultsUsersSelfRegisterResult
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
- `POST /Users/registration/verify` — Подтвердить регистрацию пользователя · коды: 202
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: DataUsersRegistrationVerifyData → ResultsUsersSelfRegisterResult
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
- `GET /Users/relevance` — Возвращает список пользователей по их релевантности к заявке · paginated · коды: 200, 206
  ← query: searchText?:str, includeTaskActuality?:bool, includeDistricts?:bool, assetID?:int, districtID?:int, workTypeID?:int, skillID?:int, levelOnShift?:bool, dateOnShift?:datetime, userTypeID?:int, isDeleted?:bool, isCustomer?:bool, isTechnician?:bool, isBanned?:bool; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → map<ResultsUsersUserResult>
- `PUT /Users/restore` — Восстановить нескольких пользователей из удаленных · коды: 202, 409
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: int[]
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
- `GET /Users/short` — Возвращает список пользователей с усеченным набором полей (для справочников и ниспадающих списков) · paginated · коды: 200, 206
  ← query: searchText?:str, orgUnitID?:int, districtID?:int, userID?:int, workTypeID?:int, skillID?:int, tag?:str, isDeleted?:bool, isCustomer?:bool, isTeam?:bool, isTechnician?:bool, isBanned?:bool, firstName?:str, lastName?:str, middleName?:str, position?:str, userTypeID?:int, erpID?:str, roleID?:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → map<ResultsUsersUserShortResult>
- `GET /Users/this/assetListQueries` — Получить список сохраненных запросов по объектам текущего пользователя · коды: 200, 204, 206
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → map<ResultsUsersAssetListQueryResult>
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
- `DELETE /Users/this/avatar` — Удаляет аватку текущего пользователя. · коды: 202
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb)
- `PUT /Users/this/avatar/upload/fromBody` — Загружает изображение JPG не менее 128x128 используемое в качестве аватарки текущего пользователя. Данные будут получены из тела запроса (base64). · коды: 202
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: DataAttachmentsFromBodyUploadData → ResultsUsersUserProfileResult
- `PUT /Users/this/avatar/upload/fromForm` — Загружает изображение JPG не менее 128x128 используемое в качестве аватарки для текущего пользователя. Данные будут получены из формы. · коды: 202
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: { ContentLength?: int, ContentStream.CanRead?: bool, ContentStream.CanSeek?: bool, ContentStream.CanTimeout?: bool, ContentStream.CanWrite?: bool, ContentStream.Capacity?: int, ContentStream.Length?: int, ContentStream.Position?: int, ContentStream.ReadTimeout?: int, ContentStream.WriteTimeout?: int, ContentType?: str, Coordinate?: str, Description?: str, File: file, FileName?: str, IsIgnorePossibleDuplication?: bool, IsPublic?: bool, Md5Hash?: str, Roles?: int[], Uid?: uuid } → ResultsUsersUserProfileResult
- `GET /Users/this/companyListQueries` — Возвращает список запросов по компаниям, доступных текущему пользователю · коды: 200
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → map<ResultsUsersCompanyListQueryResult>
- `GET /Users/this/geolocation` — Получить настройку точности сбора геокоординат текущего пользователя · коды: 200, 206
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → ResultsCoordinateAccuracyUserGeolocationSettings
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
- `GET /Users/this/notifications` — Получить список настроек уведомлений текущего пользователя · коды: 200, 204, 206
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → ResultsUserDisabledNotificationsListResult
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
- `GET /Users/this/permissions/ext` — Получить список расширенных полномочий текущего пользователя · коды: 200, 204, 206
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → map<str>
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
- `GET /Users/this/permissions/ui` — Получить список UI полномочий текущего пользователя · коды: 200, 204, 206
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → map<str>
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
- `GET /Users/this/profile` — Получить профиль текущего пользователя · коды: 200
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → ResultsUsersUserProfileResult
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
- `GET /Users/this/taskListQueries` — Получить список сохраненных запросов по заявкам текущего пользователя · коды: 200, 204, 206
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → map<ResultsUsersTaskListQueryResult>
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
- `GET /Users/{UserID}/ratings` — Получить рейтинг инженера · коды: 200, 204, 206
  ← path: userID:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → ResultsUsersRatingTechnicianResult
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
- `GET /Users/{id}` — Получить детальную информацию о пользователе · коды: 200, 400, 404
  ← path: id:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → ResultsUsersDetailedInfoResult
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
- `PUT /Users/{id}` — Обновить данные пользователя · коды: 202, 400, 404
  ← path: id:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: ADMUserUpdateData
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
- `GET /Users/{id}/assetListQueries` — Получить список сохраненных запросов по объектам пользователя · коды: 200, 204, 206
  ← path: id:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → map<ResultsUsersAssetListQueryResult>
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
- `DELETE /Users/{id}/avatar` — Удаляет аватку указаного пользователя. · коды: 202
  ← path: id:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb)
- `PUT /Users/{id}/avatar/upload/fromBody` — Загружает изображение JPG не менее 256x256 используемое в качестве аватарки для указанного пользователя. Данные будут получены из тела запроса (base64). · коды: 202
  ← path: id:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: DataAttachmentsFromBodyUploadData → ResultsUsersUserProfileResult
- `PUT /Users/{id}/avatar/upload/fromForm` — Загружает изображение JPG не менее 256x256 используемое в качестве аватарки для указанного пользователя. Данные будут получены из формы. · коды: 202
  ← path: id:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: { ContentLength?: int, ContentStream.CanRead?: bool, ContentStream.CanSeek?: bool, ContentStream.CanTimeout?: bool, ContentStream.CanWrite?: bool, ContentStream.Capacity?: int, ContentStream.Length?: int, ContentStream.Position?: int, ContentStream.ReadTimeout?: int, ContentStream.WriteTimeout?: int, ContentType?: str, Coordinate?: str, Description?: str, File: file, FileName?: str, IsIgnorePossibleDuplication?: bool, IsPublic?: bool, Md5Hash?: str, Roles?: int[], Uid?: uuid } → ResultsUsersUserProfileResult
- `GET /Users/{id}/companyListQueries` — Возвращает список запросов по компаниям, доступных пользователю · коды: 200
  ← path: id:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → map<ResultsUsersCompanyListQueryResult>
- `GET /Users/{id}/districts` — Получить список участков пользователя · коды: 200, 204, 206
  ← path: id:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → map<IdNameResultOfShort>
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
- `GET /Users/{id}/notifications` — Получить список настроек уведомлений пользователя · коды: 200, 204, 206
  ← path: id:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → ResultsUserDisabledNotificationsListResult
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
- `GET /Users/{id}/profile` — Получить профиль пользователя · коды: 200, 404
  ← path: id:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → ResultsUsersUserProfileResult
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
- `GET /Users/{id}/roles` — Получить список ролей пользователя · коды: 200, 204, 206
  ← path: id:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → map<IdNameResultOfShort>
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
- `GET /Users/{id}/taskListQueries` — Получить список сохраненных запросов по заявкам пользователя · коды: 200, 204, 206
  ← path: id:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → map<ResultsUsersTaskListQueryResult>
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
- `GET /Users/{id}/warehouses` — Получить список складов пользователя · коды: 200, 204, 206
  ← path: id:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → map<IdNameErpIDResultOfShort>
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
- `DELETE /Users/{userID}` — Удалить пользователя · коды: 202, 409
  ← path: userID:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb)
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
- `GET /Users/{userID}/assetAssignments` — Получить список объектов, назначенных пользователю · коды: 200, 204, 206
  ← path: userID:int; query: assetID?:int, validOn?:datetime; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → ResultsUsersAssetAssignmentResult[]
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
- `GET /Users/{userID}/attributes` — Получить атрибуты пользователя · коды: 200, 204, 206
  ← path: userID:int; query: attributeID?:int, IsRelevantForCustomer?:bool, IsRelevantForTechnician?:bool; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → ResultsUserAttributeUserAttributesResult[]
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
- `POST /Users/{userID}/attributes` — Создать атрибуты пользователя · коды: 201, 400
  ← path: userID:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: ADMUserAttributeAttributeData[]
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
- `PUT /Users/{userID}/attributes` — Обновить атрибуты пользователя · коды: 202, 400
  ← path: userID:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: ADMUserAttributeAttributeData[]
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
- `DELETE /Users/{userID}/attributes` — Удалить атрибуты пользователя · коды: 202, 400
  ← path: userID:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: int[]
  ## Пример запроса:

DELETE /users/123/attributes

```json
[1, 2, 3]
```

## Пример успешного ответа:

HTTP 202 Accepted
- `GET /Users/{userID}/defaultPages` — Получить текущие стартовые страницы пользователя · коды: 200, 204, 400
  ← path: userID:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → ResultsUserDefaultPagesGetResult
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
- `POST /Users/{userID}/geolocation` — Добавить настройку точности сбора геокоординат для пользователя · коды: 201, 400
  ← path: userID:int; query: coordinateAccuracyID?:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb)
  ## Пример запроса:

POST /users/123/geolocation?coordinateAccuracyID=1

## Пример успешного ответа:

HTTP 201 Created
- `PUT /Users/{userID}/geolocation` — Обновить настройку точности сбора геокоординат для пользователя · коды: 202, 400
  ← path: userID:int; query: coordinateAccuracyID?:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb)
  ## Пример запроса:

PUT /users/123/geolocation?coordinateAccuracyID=2

## Пример успешного ответа:

HTTP 202 Accepted
- `PUT /Users/{userID}/resendinvitation` — Повторно отправить приглашение пользователю · коды: 202, 204
  ← path: userID:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb)
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
- `PUT /Users/{userID}/restore` — Восстановить пользователя из удаленных · коды: 202, 409
  ← path: userID:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb)
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
- `GET /Users/{userID}/skills` — Получить список навыков пользователя · коды: 200, 204, 206, 500
  ← path: userID:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → map<ResultsSkillsSkillResult>
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
- `GET /Users/{userID}/tags` — Получить список тегов пользователя · коды: 200, 204, 206
  ← path: userID:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → str[]
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
