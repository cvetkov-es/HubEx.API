# ADM — справочник ручек

> **Что здесь:** все ручки сервиса ADM (HubEx ADM APIs): сигнатуры, параметры, права. Типы — schemas/ADM.md. Сгенерировано из swagger.
> **Когда сюда идти:** найти ручку и её вход/выход. Типы — `schemas/ADM.md`; грабли — `notes/ADM.md` (если есть).
> **Источник:** swagger сервиса ADM · файл генерируется пайплайном — руками не править.

Base: `{BASE_URL}/ADM`
> Примеры ответов вынесены в [../examples/ADM.md](../examples/ADM.md).

**Оглавление**

- BanReasons — строки 49–51
- Capabilities — строки 53–55
- DefaultPages — строки 57–59
- GeolocationSettings — строки 61–63
- Invitations — строки 65–79
- PermissionApiTags — строки 81–83
- PermissionExtTags — строки 85–87
- PermissionsApi — строки 89–91
- PermissionsExt — строки 93–95
- PermissionsUi — строки 97–109
- RoleApplications — строки 111–115
- RoleAttachments — строки 117–121
- RolePermissionsApi — строки 123–127
- RolePermissionsExt — строки 129–133
- RolePermissionsUi — строки 135–139
- RoleTaskListQueries — строки 141–145
- RoleTaskPropertiesAccess — строки 147–153
- Roles — строки 155–189
- SystemPermissionUiTags — строки 191–193
- TenantCreationRequests — строки 195–203
- TenantMembers — строки 205–223
- TenantSettings — строки 225–231
- Tenants — строки 233–278
- UserAssetListQueries — строки 280–288
- UserCompanyListQueries — строки 290–298
- UserDisabledNotifications — строки 300–302
- UserDistricts — строки 304–310
- UserOrderBy — строки 312–314
- UserRoles — строки 316–320
- UserTags — строки 322–326
- UserTaskListQueries — строки 328–332
- UserTemplateDistricts — строки 334–338
- UserTemplateRoles — строки 340–344
- UserTemplates — строки 346–362
- UserWarehouses — строки 364–368
- Users — строки 370–498

## BanReasons
- `GET /BanReasons` — Получить список причин блокировки пользователя · коды: 200, 204, 206 · примеры
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → map<ResultsBanReasonsListResult>

## Capabilities
- `GET /Capabilities` — Получить список возможностей работы с элементами интерфейса · коды: 200, 204, 206 · примеры
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → map<ResultsCapabilitiesListResult>

## DefaultPages
- `GET /DefaultPages` — Получить список доступных стартовых страниц · коды: 200, 204, 400 · примеры
  ← query: applicationID?:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → ResultsDefaultPagesAllowedPageResult[]

## GeolocationSettings
- `GET /GeolocationSettings/coordinateAccuracy` — Получить список настроек точности сбора геокоординат · коды: 200, 204 · примеры
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → IdNameDescriptionEntityOfByte[]

## Invitations
- `GET /Invitations` · paginated · коды: 200, 204, 206
  ← query: userTemplateID?:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → map<ResultsInvitationsGetResult>
- `POST /Invitations` — Создать приглашения · коды: 201, 202, 400 · примеры
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: ADMInvitationAddData[] → ResultsInvitationsAddResult[]
- `PUT /Invitations` — Обновить приглашения · коды: 202, 400 · примеры
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: ADMInvitationUpdateData[]
- `DELETE /Invitations` — Удалить приглашения · коды: 202, 400 · примеры
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: uuid[]
- `GET /Invitations/{id}` — Получить расширенную информацию о приглашении · коды: 200 · примеры
  ← path: id:uuid; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → ResultsInvitationsGetResult
- `DELETE /Invitations/{id}` — Удалить приглашение · коды: 202 · примеры
  ← path: id:uuid; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb)
- `GET /Invitations/{id}/short` — Получить сокращенную информацию о приглашении · коды: 200 · примеры
  ← path: id:uuid; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → ResultsInvitationsGetShortResult

## PermissionApiTags
- `GET /PermissionApiTags` — Получить список тегов API-полномочий · коды: 200, 204, 206 · примеры
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → map<ResultsPermissionsApiTagListResult[]>

## PermissionExtTags
- `GET /PermissionExtTags` — Получить список тегов расширенных полномочий · коды: 200, 204, 206 · примеры
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → map<ResultsPermissionsExtTagListResult[]>

## PermissionsApi
- `GET /PermissionsApi` — Получить список API-полномочий · коды: 200, 204, 206 · примеры
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → map<ResultsPermissionsApiListResult>

## PermissionsExt
- `GET /PermissionsExt` — Получить список расширенных полномочий · коды: 200, 204, 206 · примеры
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → map<ResultsPermissionsExtListResult>

## PermissionsUi
- `GET /PermissionsUi` — Получить список UI полномочий · коды: 200, 204, 206 · примеры
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → map<ResultsPermissionsUiGetResult>
- `POST /PermissionsUi` — Создать UI полномочия · коды: 201, 400 · примеры
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: ADMPermissionUiAddData[] → int[]
- `PUT /PermissionsUi` — Обновить UI полномочия · коды: 202, 400 · примеры
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: ADMPermissionUiUpdateData[]
- `DELETE /PermissionsUi` — Удалить UI полномочия · коды: 202, 400 · примеры
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: int[]
- `GET /PermissionsUi/{id}` — Получить данные UI полномочия · коды: 200, 204, 206 · примеры
  ← path: id:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → ResultsPermissionsUiGetResult
- `DELETE /PermissionsUi/{id}` — Удалить UI полномочие · коды: 202 · примеры
  ← path: id:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb)

## RoleApplications
- `POST /RoleApplications` — Добавить или обновить приложения для ролей · коды: 201, 400 · примеры
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: RoleApplicationBaseBaseData[] → ResultsRoleApplicationMergeResult[]
- `DELETE /RoleApplications` — Удалить приложения для ролей · коды: 202, 400 · примеры
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: RoleApplicationBaseBaseData[]

## RoleAttachments
- `POST /RoleAttachments` — Добавить роли для доступа к файлам · коды: 201, 400 · примеры
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: ADMRoleAttachmentAddData[] → ResultsRoleAttachmentsPostResult[]
- `DELETE /RoleAttachments` — Удалить доступ ролей к файлам · коды: 202, 400 · примеры
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: ADMRoleAttachmentDeleteData[]

## RolePermissionsApi
- `POST /RolePermissionsApi` — Создать связи роли с API-полномочиями · коды: 201, 400 · примеры
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: ADMRolePermissionApiAddData[] → ResultsRolePermissionsApiPostResult[]
- `DELETE /RolePermissionsApi` — Удалить связи роли с API-полномочиями · коды: 202, 400 · примеры
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: ADMRolePermissionApiDeleteData[]

## RolePermissionsExt
- `POST /RolePermissionsExt` — Создать связи роли с Ext-полномочиями · коды: 201, 400 · примеры
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: ADMRolePermissionExtAddData[] → ResultsRolePermissionsExtPostResult[]
- `DELETE /RolePermissionsExt` — Удалить связи роли с Ext-полномочиями · коды: 202, 400 · примеры
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: ADMRolePermissionExtDeleteData[]

## RolePermissionsUi
- `POST /RolePermissionsUi` — Создать связи роли с UI-полномочиями · коды: 201, 400 · примеры
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: ADMRolePermissionUiAddData[] → ResultsRolePermissionsUiPostResult[]
- `DELETE /RolePermissionsUi` — Удалить связи роли с UI-полномочиями · коды: 202, 400 · примеры
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: ADMRolePermissionUiDeleteData[]

## RoleTaskListQueries
- `POST /RoleTaskListQueries` — Добавить сохраненные запросы заявок для роли · коды: 201, 400 · примеры
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: ADMRoleTaskListQueryAddData[] → ResultsRoleTaskListQueriesPostResult[]
- `DELETE /RoleTaskListQueries` — Удалить сохраненные запросы заявок у роли · коды: 202, 400 · примеры
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: ADMRoleTaskListQueryDeleteData[]

## RoleTaskPropertiesAccess
- `GET /RoleTaskPropertiesAccess/attributes` · paginated · коды: 200, 204, 206
  ← query: roleID?:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → ResultsRoleTaskAttributeRoleTaskAttributeSettings[]
- `POST /RoleTaskPropertiesAccess/attributes` — Добавить настройки доступности атрибутов задач для ролей · коды: 201, 400 · примеры
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: DataADMRoleTaskAttributeDto[]
- `PUT /RoleTaskPropertiesAccess/attributes` — Обновить настройки доступности атрибутов задач для ролей · коды: 202, 400 · примеры
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: DataADMRoleTaskAttributeDto[]

## Roles
- `GET /Roles` — Получить список ролей тенанта · коды: 200, 204, 206 · примеры
  ← query: isDeleted?:bool; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → map<ResultsRolesGetResult>
- `POST /Roles` — Создать роли · коды: 201, 400 · примеры
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: ADMRoleAddData[] → int[]
- `PUT /Roles` — Обновить роли · коды: 202, 400 · примеры
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: ADMRoleUpdateData[]
- `DELETE /Roles` — Удалить роли · коды: 202, 400 · примеры
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: int[]
- `POST /Roles/copy` — Копировать роли · коды: 201, 400 · примеры
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: ADMRoleCopyData[] → int[]
- `GET /Roles/{id}` — Получить информацию о роли · коды: 200, 204 · примеры
  ← path: id:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → ResultsRolesGetResult
- `DELETE /Roles/{id}` — Удалить роль · коды: 202 · примеры
  ← path: id:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb)
- `GET /Roles/{roleID}/applications` — Получить список приложений роли · коды: 200, 204, 206 · примеры
  ← path: roleID:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → map<ResultsRoleApplicationListResult>
- `GET /Roles/{roleID}/attachments` — Получить список вложенных файлов роли · коды: 200, 204, 206 · примеры
  ← path: roleID:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → ResultsCommonAttachmentResult[]
- `GET /Roles/{roleID}/packages` — Получить список расширений роли · коды: 200, 204, 206 · примеры
  ← path: roleID:int; query: searchText?:str; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → map<ResultsRolePackagesListResult[]>
- `POST /Roles/{roleID}/packages` — Добавить расширения к роли · коды: 201, 400 · примеры
  ← path: roleID:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: ADMRolePackageAddData[] → ResultsRolePackagesPostResult[]
- `DELETE /Roles/{roleID}/packages` — Удалить расширения роли · коды: 202, 400 · примеры
  ← path: roleID:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: int[]
- `PUT /Roles/{roleID}/packages/activate` — Активировать расширения роли · коды: 202, 400 · примеры
  ← path: roleID:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: int[]
- `PUT /Roles/{roleID}/packages/deactivate` — Деактивировать расширения роли · коды: 202, 400 · примеры
  ← path: roleID:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: int[]
- `GET /Roles/{roleID}/permissionsApi` — Получить список API-полномочий роли · коды: 200, 204, 206 · примеры
  ← path: roleID:int; query: systemTagID?:str, isCheckedPermission?:bool; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → map<ResultsRolePermissionsApiListResult[]>
- `GET /Roles/{roleID}/permissionsExt` — Получить список Ext-полномочий роли · коды: 200, 204, 206 · примеры
  ← path: roleID:int; query: systemTagID?:str, isCheckedPermission?:bool; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → map<ResultsRolePermissionsExtListResult[]>
- `GET /Roles/{roleID}/permissionsUi` — Получить список UI-полномочий роли · коды: 200, 204, 206 · примеры
  ← path: roleID:int; query: systemTagID?:int, isCheckedPermission?:bool, isSystemPermission?:bool; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → map<ResultsRolePermissionsUiListResult[]>

## SystemPermissionUiTags
- `GET /SystemPermissionUiTags` — Получить список тегов системных UI-полномочий · коды: 200, 204, 206 · примеры
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → map<ResultsPermissionsUiTagListResult[]>

## TenantCreationRequests
- `POST /TenantCreationRequests` — Создать запрос на создание тенанта · коды: 201, 400 · примеры
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: ADMTenantCreationRequestAddData → ResultsTenantCreationRequestsPostResult
- `GET /TenantCreationRequests/{id}` — Получить запрос на создание тенанта · коды: 200 · примеры
  ← path: id:str; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → ResultsTenantCreationRequestsGetResult
- `PUT /TenantCreationRequests/{id}/approve` — Утвердить запрос на создание тенанта · коды: 202, 400 · примеры
  ← path: id:str; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb)
- `PUT /TenantCreationRequests/{id}/reject` — Отклонить запрос на создание тенанта · коды: 202, 400 · примеры
  ← path: id:str; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: ADMTenantCreationRequestRejectData

## TenantMembers
- `GET /TenantMembers` · paginated · коды: 200, 204, 206
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → map<ResultsTenantMembersListResult>
- `POST /TenantMembers` — Создать члена тенанта · коды: 201, 400 · примеры
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: ADMTenantMemberAddData[] → int[]
- `PUT /TenantMembers` — Обновить данные члена тенанта · коды: 202, 400 · примеры
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: ADMTenantMemberUpdateData[]
- `DELETE /TenantMembers` — Удалить членов тенанта · коды: 202, 400 · примеры
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: int[]
- `GET /TenantMembers/anonymousUser` — Получить анонимного пользователя в текущем тенанте · коды: 200, 204 · примеры
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → ResultsTenantMembersListResult
- `GET /TenantMembers/apiUser` — Получить пользователя API в текущем тенанте · коды: 200, 204 · примеры
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → ResultsTenantMembersListResult
- `GET /TenantMembers/this` — Получить данные текущего члена тенанта · коды: 200 · примеры
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → ResultsTenantMembersGetResult
- `GET /TenantMembers/{tenantMemberID}` — Получить данные члена тенанта · коды: 200, 500 · примеры
  ← path: tenantMemberID:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → ResultsTenantMembersGetResult
- `DELETE /TenantMembers/{tenantMemberID}` — Удалить члена тенанта · коды: 202 · примеры
  ← path: tenantMemberID:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb)

## TenantSettings
- `GET /TenantSettings` — Получить настройки тенанта · коды: 200, 204, 500 · примеры
  ← query: tenantMemberId?:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → ResultsTenantSettingsGetResult
- `GET /TenantSettings/plateUrl` — Получить кастомный URL текущего тенанта · коды: 200, 204 · примеры
  ← query: taskTemplateID?:str; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → str
- `PUT /TenantSettings/plateUrl` — Обновить кастомный URL текущего тенанта · коды: 202 · примеры
  ← query: plateUrl?:str; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb)

## Tenants
- `GET /Tenants` — Получить список тенантов · коды: 200, 204, 206 · примеры
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → ResultsTenantsListResult[]
- `PUT /Tenants/licenses` — Обновить лицензию тенанта · коды: 202, 400 · примеры
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: ADMTenantLicenseUpdateData
- `GET /Tenants/templates` — Получить список шаблонных тенантов · коды: 200, 204, 206 · примеры
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → InterfacesEntitiesITenantEntity[]
- `GET /Tenants/this` — Получить данные текущего тенанта · коды: 200 · примеры
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → ResultsTenantsGetResult
- `GET /Tenants/this/featureFlags` — Получить список флагов функций тенанта · коды: 200, 204 · примеры
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → str[]
- `GET /Tenants/this/licenses` — Получить список лицензий тенанта · коды: 200, 204 · примеры
  ← query: validOn?:datetime; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → ResultsTenantLicenseListTenantLicenseResult
- `POST /Tenants/this/licenses` — Добавить лицензию для тенанта · коды: 201, 400 · примеры
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: ADMTenantLicenseAddData
- `DELETE /Tenants/this/licenses` — Удалить лицензии тенанта · коды: 202, 400 · примеры
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: int[]
- `POST /Tenants/this/licenses/renewal` — Отправить запрос на продление лицензии · коды: 200, 500 · примеры
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb)
- `DELETE /Tenants/this/licenses/{id}` — Удалить лицензию тенанта · коды: 202 · примеры
  ← path: id:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb)
- `GET /Tenants/this/meta` — Получить метаданные тенанта · коды: 200, 204 · примеры
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb)
- `GET /Tenants/this/packages` · paginated · коды: 200, 204, 206
  ← query: resourceID?:int[]; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → ResultsTenantPackagesListResult[]
  Для выполнения данного метода пользователь должен быть **TenantMember**.
- `POST /Tenants/this/packages` — Добавить расширение (только для кросс-тенантных администраторов) · коды: 200, 204, 206, 400 · примеры
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: ADDONPackageAddData → ResultsTenantPackagesListResult[]
- `PATCH /Tenants/this/packages` — Обновить расширение (только для кросс-тенантных администраторов) · коды: 202, 400 · примеры
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: ADDONPackageUpdateData
- `DELETE /Tenants/this/packages` — Удалить расширение (только для кросс-тенантных администраторов) · коды: 202, 400 · примеры
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: ADDONPackagePackageIdentifier
- `POST /Tenants/this/packages/tenant` — Добавить расширение для тенанта · коды: 200, 204, 206, 400 · примеры
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: ADDONPackageAddTenantPackageData → ResultsTenantPackagesListResult[]
- `DELETE /Tenants/this/packages/tenant` — Удалить расширение для тенанта · коды: 202, 400 · примеры
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: ADDONPackagePackageIdentifier
- `GET /Tenants/this/variables` — Получить список переменных окружения тенанта · коды: 200, 204, 206 · примеры
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → map<ResultsTenantVariablesListResult>
- `POST /Tenants/this/variables` — Добавить переменные окружения тенанта · коды: 201, 400 · примеры
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: ADMTenantVariableAddData[]
- `PUT /Tenants/this/variables` — Обновить переменные окружения тенанта · коды: 202, 400 · примеры
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: ADMTenantVariableUpdateData[]
- `DELETE /Tenants/this/variables` — Удалить переменные окружения тенанта · коды: 202, 400 · примеры
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: str[]
- `DELETE /Tenants/this/variables/{name}` — Удалить переменную окружения тенанта · коды: 202 · примеры
  ← path: name:str; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb)

## UserAssetListQueries
- `POST /UserAssetListQueries` — Добавить сохраненные запросы объектов пользователям · коды: 201, 400 · примеры
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: ADMUserAssetListQueryAddData[] → ResultsUserAssetListQueriesPostResult[]
- `DELETE /UserAssetListQueries` — Удалить сохраненные запросы объектов у пользователей · коды: 202, 400 · примеры
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: ADMUserAssetListQueryDeleteData[]
- `POST /UserAssetListQueries/{userID}` — Добавить сохраненные запросы объектов пользователю · коды: 201, 400 · примеры
  ← path: userID:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: int[] → ResultsUserAssetListQueriesPostResult[]
- `DELETE /UserAssetListQueries/{userID}` — Удалить сохраненные запросы объектов у пользователя · коды: 202, 400 · примеры
  ← path: userID:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: int[]

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
- `POST /UserDisabledNotifications` — Изменить настройки уведомлений пользователя · коды: 202, 204, 400, 500 · примеры
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: DataUserDisabledNotificationsPostData → ResultsUserDisabledNotificationsMergeResult[]

## UserDistricts
- `POST /UserDistricts` — Добавить участки пользователю · коды: 201, 400, 500 · примеры
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: OperationDataOfAddData
- `PUT /UserDistricts` — Обновить участки у пользователя · коды: 202, 400, 500 · примеры
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: OperationDataOfUpdateData
- `DELETE /UserDistricts` — Удалить участки у пользователя · коды: 202, 400, 500 · примеры
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: OperationDataOfShort

## UserOrderBy
- `GET /UserOrderBy` — Получить список методов сортировки сотрудников · коды: 200, 204, 206 · примеры
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → map<ResultsUserOrderByListResult>

## UserRoles
- `POST /UserRoles` — Добавить роли пользователю · коды: 201, 400, 500 · примеры
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: DataUserRolesPostData[]
- `DELETE /UserRoles` — Удалить роли у пользователя · коды: 202, 400, 500 · примеры
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: DataUserRolesDeleteData[]

## UserTags
- `POST /UserTags` — Добавить теги пользователю · коды: 201, 400, 409 · примеры
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: DataUserTagsPostData[] → ResultsUserTagAddResult[]
- `DELETE /UserTags` — Удалить теги пользователя · коды: 202, 400 · примеры
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: DataUserTagsDeleteData[]

## UserTaskListQueries
- `POST /UserTaskListQueries` — Добавить сохраненные запросы заявок пользователям · коды: 201, 400 · примеры
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: ADMUserTaskListQueryAddData[] → ResultsUserTaskListQueriesPostResult[]
- `DELETE /UserTaskListQueries` — Удалить сохраненные запросы заявок у пользователей · коды: 202, 400 · примеры
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: ADMUserTaskListQueryDeleteData[]

## UserTemplateDistricts
- `POST /UserTemplateDistricts` — Добавить участки к шаблону пользователя · коды: 201, 400, 500 · примеры
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: ActionDataOfShort[]
- `DELETE /UserTemplateDistricts/remove` — Удалить участки из шаблона пользователя · коды: 202, 400, 500 · примеры
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: ActionDataOfShort[]

## UserTemplateRoles
- `POST /UserTemplateRoles` — Добавить роли к шаблону пользователя · коды: 201, 400, 500 · примеры
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: ActionDataOfShort[]
- `DELETE /UserTemplateRoles/remove` — Удалить роли из шаблона пользователя · коды: 202, 400, 500 · примеры
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: ActionDataOfShort[]

## UserTemplates
- `GET /UserTemplates` · paginated · коды: 200, 204, 206
  ← query: searchText?:str, isTechnician?:bool, roleID?:int, districtID?:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → map<ResultsUserTemplatesListResult>
- `POST /UserTemplates` — Создать шаблон пользователя · коды: 201, 400 · примеры
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: ADMUserTemplateAddData[] → int[]
- `PUT /UserTemplates` — Обновить шаблон пользователя · коды: 202, 400, 409 · примеры
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: ADMUserTemplateUpdateData[]
- `DELETE /UserTemplates` — Удалить шаблоны пользователя · коды: 202, 400 · примеры
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: int[]
- `GET /UserTemplates/{id}` — Получить шаблон пользователя · коды: 200, 204 · примеры
  ← path: id:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → ResultsUserTemplatesGetResult
- `DELETE /UserTemplates/{id}` — Удалить шаблон пользователя · коды: 202 · примеры
  ← path: id:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb)
- `GET /UserTemplates/{id}/districts` — Получить список участков шаблона пользователя · коды: 200, 204, 206 · примеры
  ← path: id:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → IdNameResultOfShort[]
- `GET /UserTemplates/{id}/roles` — Получить список ролей шаблона пользователя · коды: 200, 204, 206 · примеры
  ← path: id:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → IdNameResultOfShort[]

## UserWarehouses
- `POST /UserWarehouses` — Добавить склады пользователю · коды: 201, 400, 500 · примеры
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: WHWarehouseUserUserWarehousesData[]
- `DELETE /UserWarehouses` — Удалить склады у пользователя · коды: 202, 400, 500 · примеры
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: WHWarehouseUserUserWarehousesData[]

## Users
- `GET /Users` — Возвращает список пользователей · paginated · коды: 200, 206
  ← query: searchText?:str, includeTaskActuality?:bool, includeDistricts?:bool, needForAllowedTasks?:bool, orgUnitID?:int, districtID?:int, userID?:int, workTypeID?:int, skillID?:int, tag?:str, isDeleted?:bool, isCustomer?:bool, isTeam?:bool, isTechnician?:bool, isBanned?:bool, isOnShift?:bool, firstName?:str, lastName?:str, middleName?:str, position?:str, userTypeID?:int, companyID?:int, orderBy?:int, sortDirection?:int, erpID?:str, roleID?:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → map<ResultsUsersUserResult>
- `POST /Users` — Добавить нового пользователя · коды: 201, 400, 409 · примеры
  ← query: skipAccountVerification?:bool, skipAccountVerification?:bool; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: ADMUserAddData → ProjectionsADMUserAddProjection
- `DELETE /Users` — Удалить нескольких пользователей · коды: 202, 409 · примеры
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: int[]
- `HEAD /Users` — Возвращает заголовок запроса пользователей с количеством данных, удовлетворяющих фильтру · коды: 200
  ← query: orgUnitID?:int, districtID?:int, userID?:int, workTypeID?:int, skillID?:int, tag?:str, isDeleted?:bool, isCustomer?:bool, isTeam?:bool, isTechnician?:bool, firstName?:str, lastName?:str, middleName?:str, position?:str, userTypeID?:int, erpID?:str; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb)
- `POST /Users/addbyintegration` — Добавить нового пользователя через интеграцию · коды: 200, 400, 409 · примеры
  ← query: skipAccountVerification?:bool, skipAccountVerification?:bool; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: ADMUserAddData → ProjectionsADMUserRoleAddProjection[]
- `POST /Users/anonymous` — Создать анонимного пользователя в тенанте · коды: 201 · примеры
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → DataUsersServiceUserResult
- `POST /Users/api` — Создать API-пользователя в тенанте · коды: 201 · примеры
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → DataUsersServiceUserResult
- `GET /Users/attributes` — Получить список атрибутов пользователей · коды: 200, 204, 206 · примеры
  ← query: attributeID?:int, userID?:int, IsRelevantForCustomer?:bool, IsRelevantForTechnician?:bool; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → ResultsUserAttributeUserAttributesResult[]
- `POST /Users/attributes` — Создать атрибуты для пользователей · коды: 201, 400 · примеры
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: UserActionDataOfAttributeData[]
- `PUT /Users/attributes` — Обновить атрибуты пользователей · коды: 202, 400 · примеры
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: UserActionDataOfAttributeData[]
- `DELETE /Users/attributes` — Удалить атрибуты пользователей · коды: 202, 400 · примеры
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: UserActionDataOfShort[]
- `DELETE /Users/avatar` — Удаляет аватку для указанного списка пользователей. · коды: 202
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: int[]
- `POST /Users/changeToCustomer` — Изменить тип пользователя на заказчика · коды: 202, 400 · примеры
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: int[]
- `POST /Users/changeToStaff` — Изменить тип пользователя на сотрудника · коды: 202, 400 · примеры
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: int[]
- `POST /Users/defaultPages` — Добавить стартовые страницы пользователей · коды: 201, 400, 409 · примеры
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: ADMUserDefaultPagesUserStartPageDto[]
- `PUT /Users/defaultPages` — Изменить стартовые страницы пользователей · коды: 202, 400, 404 · примеры
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: ADMUserDefaultPagesUserStartPageDto[]
- `DELETE /Users/defaultPages` — Сбросить стартовые страницы у пользователей · коды: 202, 400 · примеры
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: int[]
- `GET /Users/geolocation` — Получить список настроек точности сбора геокоординат для пользователей · коды: 200, 204, 206 · примеры
  ← query: userID?:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → ResultsCoordinateAccuracyUserGeolocationSettings[]
- `POST /Users/geolocation` — Добавить настройки точности сбора геокоординат для пользователей · коды: 201, 400 · примеры
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: DataADMUserGeolocationDto[]
- `PUT /Users/geolocation` — Обновить настройки точности сбора геокоординат для пользователей · коды: 202, 400 · примеры
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: DataADMUserGeolocationDto[]
- `GET /Users/profile` — Получить профиль пользователя · коды: 200, 404 · примеры
  ← query: tenantMemberId?:int, userId?:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → ResultsUsersUserProfileResult
- `POST /Users/registration` — Саморегистрация пользователя по приглашению · коды: 201, 202, 409 · примеры
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: DataUsersRegisterData → ResultsUsersSelfRegisterResult
- `POST /Users/registration/verify` — Подтвердить регистрацию пользователя · коды: 202 · примеры
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: DataUsersRegistrationVerifyData → ResultsUsersSelfRegisterResult
- `GET /Users/relevance` — Возвращает список пользователей по их релевантности к заявке · paginated · коды: 200, 206
  ← query: searchText?:str, includeTaskActuality?:bool, includeDistricts?:bool, assetID?:int, districtID?:int, workTypeID?:int, skillID?:int, levelOnShift?:bool, dateOnShift?:datetime, userTypeID?:int, isDeleted?:bool, isCustomer?:bool, isTechnician?:bool, isBanned?:bool; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → map<ResultsUsersUserResult>
- `PUT /Users/restore` — Восстановить нескольких пользователей из удаленных · коды: 202, 409 · примеры
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: int[]
- `GET /Users/short` — Возвращает список пользователей с усеченным набором полей (для справочников и ниспадающих списков) · paginated · коды: 200, 206
  ← query: searchText?:str, orgUnitID?:int, districtID?:int, userID?:int, workTypeID?:int, skillID?:int, tag?:str, isDeleted?:bool, isCustomer?:bool, isTeam?:bool, isTechnician?:bool, isBanned?:bool, firstName?:str, lastName?:str, middleName?:str, position?:str, userTypeID?:int, erpID?:str, roleID?:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → map<ResultsUsersUserShortResult>
- `GET /Users/this/assetListQueries` — Получить список сохраненных запросов по объектам текущего пользователя · коды: 200, 204, 206 · примеры
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → map<ResultsUsersAssetListQueryResult>
- `DELETE /Users/this/avatar` — Удаляет аватку текущего пользователя. · коды: 202
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb)
- `PUT /Users/this/avatar/upload/fromBody` — Загружает изображение JPG не менее 128x128 используемое в качестве аватарки текущего пользователя. Данные будут получены из тела запроса (base64). · коды: 202
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: DataAttachmentsFromBodyUploadData → ResultsUsersUserProfileResult
- `PUT /Users/this/avatar/upload/fromForm` — Загружает изображение JPG не менее 128x128 используемое в качестве аватарки для текущего пользователя. Данные будут получены из формы. · коды: 202
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: { ContentLength?: int, ContentStream.CanRead?: bool, ContentStream.CanSeek?: bool, ContentStream.CanTimeout?: bool, ContentStream.CanWrite?: bool, ContentStream.Capacity?: int, ContentStream.Length?: int, ContentStream.Position?: int, ContentStream.ReadTimeout?: int, ContentStream.WriteTimeout?: int, ContentType?: str, Coordinate?: str, Description?: str, File: file, FileName?: str, IsIgnorePossibleDuplication?: bool, IsPublic?: bool, Md5Hash?: str, Roles?: int[], Uid?: uuid } → ResultsUsersUserProfileResult
- `GET /Users/this/companyListQueries` — Возвращает список запросов по компаниям, доступных текущему пользователю · коды: 200
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → map<ResultsUsersCompanyListQueryResult>
- `GET /Users/this/geolocation` — Получить настройку точности сбора геокоординат текущего пользователя · коды: 200, 206 · примеры
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → ResultsCoordinateAccuracyUserGeolocationSettings
- `GET /Users/this/notifications` — Получить список настроек уведомлений текущего пользователя · коды: 200, 204, 206 · примеры
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → ResultsUserDisabledNotificationsListResult
- `GET /Users/this/permissions/ext` — Получить список расширенных полномочий текущего пользователя · коды: 200, 204, 206 · примеры
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → map<str>
- `GET /Users/this/permissions/ui` — Получить список UI полномочий текущего пользователя · коды: 200, 204, 206 · примеры
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → map<str>
- `GET /Users/this/profile` — Получить профиль текущего пользователя · коды: 200 · примеры
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → ResultsUsersUserProfileResult
- `GET /Users/this/taskListQueries` — Получить список сохраненных запросов по заявкам текущего пользователя · коды: 200, 204, 206 · примеры
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → map<ResultsUsersTaskListQueryResult>
- `GET /Users/{UserID}/ratings` — Получить рейтинг инженера · коды: 200, 204, 206 · примеры
  ← path: userID:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → ResultsUsersRatingTechnicianResult
- `GET /Users/{id}` — Получить детальную информацию о пользователе · коды: 200, 400, 404 · примеры
  ← path: id:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → ResultsUsersDetailedInfoResult
- `PUT /Users/{id}` — Обновить данные пользователя · коды: 202, 400, 404 · примеры
  ← path: id:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: ADMUserUpdateData
- `GET /Users/{id}/assetListQueries` — Получить список сохраненных запросов по объектам пользователя · коды: 200, 204, 206 · примеры
  ← path: id:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → map<ResultsUsersAssetListQueryResult>
- `DELETE /Users/{id}/avatar` — Удаляет аватку указаного пользователя. · коды: 202
  ← path: id:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb)
- `PUT /Users/{id}/avatar/upload/fromBody` — Загружает изображение JPG не менее 256x256 используемое в качестве аватарки для указанного пользователя. Данные будут получены из тела запроса (base64). · коды: 202
  ← path: id:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: DataAttachmentsFromBodyUploadData → ResultsUsersUserProfileResult
- `PUT /Users/{id}/avatar/upload/fromForm` — Загружает изображение JPG не менее 256x256 используемое в качестве аватарки для указанного пользователя. Данные будут получены из формы. · коды: 202
  ← path: id:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: { ContentLength?: int, ContentStream.CanRead?: bool, ContentStream.CanSeek?: bool, ContentStream.CanTimeout?: bool, ContentStream.CanWrite?: bool, ContentStream.Capacity?: int, ContentStream.Length?: int, ContentStream.Position?: int, ContentStream.ReadTimeout?: int, ContentStream.WriteTimeout?: int, ContentType?: str, Coordinate?: str, Description?: str, File: file, FileName?: str, IsIgnorePossibleDuplication?: bool, IsPublic?: bool, Md5Hash?: str, Roles?: int[], Uid?: uuid } → ResultsUsersUserProfileResult
- `GET /Users/{id}/companyListQueries` — Возвращает список запросов по компаниям, доступных пользователю · коды: 200
  ← path: id:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → map<ResultsUsersCompanyListQueryResult>
- `GET /Users/{id}/districts` — Получить список участков пользователя · коды: 200, 204, 206 · примеры
  ← path: id:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → map<IdNameResultOfShort>
- `GET /Users/{id}/notifications` — Получить список настроек уведомлений пользователя · коды: 200, 204, 206 · примеры
  ← path: id:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → ResultsUserDisabledNotificationsListResult
- `GET /Users/{id}/profile` — Получить профиль пользователя · коды: 200, 404 · примеры
  ← path: id:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → ResultsUsersUserProfileResult
- `GET /Users/{id}/roles` — Получить список ролей пользователя · коды: 200, 204, 206 · примеры
  ← path: id:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → map<IdNameResultOfShort>
- `GET /Users/{id}/taskListQueries` — Получить список сохраненных запросов по заявкам пользователя · коды: 200, 204, 206 · примеры
  ← path: id:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → map<ResultsUsersTaskListQueryResult>
- `GET /Users/{id}/warehouses` — Получить список складов пользователя · коды: 200, 204, 206 · примеры
  ← path: id:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → map<IdNameErpIDResultOfShort>
- `DELETE /Users/{userID}` — Удалить пользователя · коды: 202, 409 · примеры
  ← path: userID:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb)
- `GET /Users/{userID}/assetAssignments` — Получить список объектов, назначенных пользователю · коды: 200, 204, 206 · примеры
  ← path: userID:int; query: assetID?:int, validOn?:datetime; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → ResultsUsersAssetAssignmentResult[]
- `GET /Users/{userID}/attributes` — Получить атрибуты пользователя · коды: 200, 204, 206 · примеры
  ← path: userID:int; query: attributeID?:int, IsRelevantForCustomer?:bool, IsRelevantForTechnician?:bool; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → ResultsUserAttributeUserAttributesResult[]
- `POST /Users/{userID}/attributes` — Создать атрибуты пользователя · коды: 201, 400 · примеры
  ← path: userID:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: ADMUserAttributeAttributeData[]
- `PUT /Users/{userID}/attributes` — Обновить атрибуты пользователя · коды: 202, 400 · примеры
  ← path: userID:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: ADMUserAttributeAttributeData[]
- `DELETE /Users/{userID}/attributes` — Удалить атрибуты пользователя · коды: 202, 400 · примеры
  ← path: userID:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: int[]
- `GET /Users/{userID}/defaultPages` — Получить текущие стартовые страницы пользователя · коды: 200, 204, 400 · примеры
  ← path: userID:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → ResultsUserDefaultPagesGetResult
- `POST /Users/{userID}/geolocation` — Добавить настройку точности сбора геокоординат для пользователя · коды: 201, 400 · примеры
  ← path: userID:int; query: coordinateAccuracyID?:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb)
- `PUT /Users/{userID}/geolocation` — Обновить настройку точности сбора геокоординат для пользователя · коды: 202, 400 · примеры
  ← path: userID:int; query: coordinateAccuracyID?:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb)
- `PUT /Users/{userID}/resendinvitation` — Повторно отправить приглашение пользователю · коды: 202, 204 · примеры
  ← path: userID:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb)
- `PUT /Users/{userID}/restore` — Восстановить пользователя из удаленных · коды: 202, 409 · примеры
  ← path: userID:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb)
- `GET /Users/{userID}/skills` — Получить список навыков пользователя · коды: 200, 204, 206, 500 · примеры
  ← path: userID:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → map<ResultsSkillsSkillResult>
- `GET /Users/{userID}/tags` — Получить список тегов пользователя · коды: 200, 204, 206 · примеры
  ← path: userID:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → str[]
