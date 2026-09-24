# ADM — справочник ручек

> **Что здесь:** все ручки сервиса ADM (HubEx ADM APIs): сигнатуры, параметры, права. Типы — schemas/ADM.md.
> **Когда сюда идти:** найти ручку и её вход/выход. Типы — `schemas/ADM.md`; грабли — `notes/ADM.md` (если есть).

Base: `{BASE_URL}/ADM`
> Примеры ответов вынесены в [../examples/ADM.md](../examples/ADM.md).

**Оглавление**

- BanReasons — строки 48–50
- Capabilities — строки 52–54
- DefaultPages — строки 56–58
- GeolocationSettings — строки 60–62
- Invitations — строки 64–78
- PermissionApiTags — строки 80–82
- PermissionExtTags — строки 84–86
- PermissionsApi — строки 88–90
- PermissionsExt — строки 92–94
- PermissionsUi — строки 96–108
- RoleApplications — строки 110–114
- RoleAttachments — строки 116–120
- RolePermissionsApi — строки 122–126
- RolePermissionsExt — строки 128–132
- RolePermissionsUi — строки 134–138
- RoleTaskListQueries — строки 140–144
- RoleTaskPropertiesAccess — строки 146–152
- Roles — строки 154–188
- SystemPermissionUiTags — строки 190–192
- TenantCreationRequests — строки 194–202
- TenantMembers — строки 204–222
- TenantSettings — строки 224–230
- Tenants — строки 232–274
- UserAssetListQueries — строки 276–284
- UserCompanyListQueries — строки 286–294
- UserDisabledNotifications — строки 296–298
- UserDistricts — строки 300–306
- UserOrderBy — строки 308–310
- UserRoles — строки 312–316
- UserTags — строки 318–322
- UserTaskListQueries — строки 324–328
- UserTemplateDistricts — строки 330–334
- UserTemplateRoles — строки 336–340
- UserTemplates — строки 342–358
- UserWarehouses — строки 360–364
- Users — строки 366–493

## BanReasons
- `GET /BanReasons` — Получить список причин блокировки пользователя · коды: 200, 204, 206 · примеры
  → map<RBRListResult>

## Capabilities
- `GET /Capabilities` — Получить список возможностей работы с элементами интерфейса · коды: 200, 204, 206 · примеры
  → map<RCListResult>

## DefaultPages
- `GET /DefaultPages` — Получить список доступных стартовых страниц · коды: 200, 204, 400 · примеры
  ← query: applicationID?:int → AllowedPageResult[]

## GeolocationSettings
- `GET /GeolocationSettings/coordinateAccuracy` — Получить список настроек точности сбора геокоординат · коды: 200, 204 · примеры
  → IdNameDescriptionEntityOfByte[]

## Invitations
- `GET /Invitations` — Получить список всех приглашений тенанта · коды: 200, 204, 206 · примеры
  ← query: userTemplateID?:int → map<RIGetResult>
- `POST /Invitations` — Создать приглашения · коды: 201, 202, 400 · примеры
  ← body: ADMIAddData[] → RIAddResult[]
- `PUT /Invitations` — Обновить приглашения · коды: 202, 400 · примеры
  ← body: ADMIUpdateData[]
- `DELETE /Invitations` — Удалить приглашения · коды: 202, 400 · примеры
  ← body: uuid[]
- `GET /Invitations/{id}` — Получить расширенную информацию о приглашении · коды: 200 · примеры
  ← path: id:uuid → RIGetResult
- `DELETE /Invitations/{id}` — Удалить приглашение · коды: 202 · примеры
  ← path: id:uuid
- `GET /Invitations/{id}/short` — Получить сокращенную информацию о приглашении · коды: 200 · примеры
  ← path: id:uuid → GetShortResult

## PermissionApiTags
- `GET /PermissionApiTags` — Получить список тегов API-полномочий · коды: 200, 204, 206 · примеры
  → map<RPATListResult[]>

## PermissionExtTags
- `GET /PermissionExtTags` — Получить список тегов расширенных полномочий · коды: 200, 204, 206 · примеры
  → map<RPETListResult[]>

## PermissionsApi
- `GET /PermissionsApi` — Получить список API-полномочий · коды: 200, 204, 206 · примеры
  → map<RPAListResult>

## PermissionsExt
- `GET /PermissionsExt` — Получить список расширенных полномочий · коды: 200, 204, 206 · примеры
  → map<RPEListResult>

## PermissionsUi
- `GET /PermissionsUi` — Получить список UI полномочий · коды: 200, 204, 206 · примеры
  → map<RPUGetResult>
- `POST /PermissionsUi` — Создать UI полномочия · коды: 201, 400 · примеры
  ← body: ADMPUAddData[] → int[]
- `PUT /PermissionsUi` — Обновить UI полномочия · коды: 202, 400 · примеры
  ← body: ADMPUUpdateData[]
- `DELETE /PermissionsUi` — Удалить UI полномочия · коды: 202, 400 · примеры
  ← body: int[]
- `GET /PermissionsUi/{id}` — Получить данные UI полномочия · коды: 200, 204 · примеры
  ← path: id:int → RPUGetResult
- `DELETE /PermissionsUi/{id}` — Удалить UI полномочие · коды: 202 · примеры
  ← path: id:int

## RoleApplications
- `POST /RoleApplications` — Добавить или обновить приложения для ролей · коды: 201, 400 · примеры
  ← body: ApiBaseData[] → RRAMergeResult[]
- `DELETE /RoleApplications` — Удалить приложения для ролей · коды: 202, 400 · примеры
  ← body: ApiBaseData[]

## RoleAttachments
- `POST /RoleAttachments` — Добавить роли для доступа к файлам · коды: 201, 400 · примеры
  ← body: ADMRAAddData[] → RRAPostResult[]
- `DELETE /RoleAttachments` — Удалить доступ ролей к файлам · коды: 202, 400 · примеры
  ← body: ADMRADeleteData[]

## RolePermissionsApi
- `POST /RolePermissionsApi` — Создать связи роли с API-полномочиями · коды: 201, 400 · примеры
  ← body: ADMRPAAddData[] → RRPAPostResult[]
- `DELETE /RolePermissionsApi` — Удалить связи роли с API-полномочиями · коды: 202, 400 · примеры
  ← body: ADMRPADeleteData[]

## RolePermissionsExt
- `POST /RolePermissionsExt` — Создать связи роли с Ext-полномочиями · коды: 201, 400 · примеры
  ← body: ADMRPEAddData[] → RRPEPostResult[]
- `DELETE /RolePermissionsExt` — Удалить связи роли с Ext-полномочиями · коды: 202, 400 · примеры
  ← body: ADMRPEDeleteData[]

## RolePermissionsUi
- `POST /RolePermissionsUi` — Создать связи роли с UI-полномочиями · коды: 201, 400 · примеры
  ← body: ADMRPUAddData[] → RRPUPostResult[]
- `DELETE /RolePermissionsUi` — Удалить связи роли с UI-полномочиями · коды: 202, 400 · примеры
  ← body: ADMRPUDeleteData[]

## RoleTaskListQueries
- `POST /RoleTaskListQueries` — Добавить сохраненные запросы заявок для роли · коды: 201, 400 · примеры
  ← body: ADMRTLQAddData[] → RRTLQPostResult[]
- `DELETE /RoleTaskListQueries` — Удалить сохраненные запросы заявок у роли · коды: 202, 400 · примеры
  ← body: ADMRTLQDeleteData[]

## RoleTaskPropertiesAccess
- `GET /RoleTaskPropertiesAccess/attributes` — Получить настройки доступности атрибутов задач для ролей · коды: 200, 204, 206 · примеры
  ← query: roleID?:int → RoleTaskAttributeSettings[]
- `POST /RoleTaskPropertiesAccess/attributes` — Добавить настройки доступности атрибутов задач для ролей · коды: 201, 400 · примеры
  ← body: RoleTaskAttributeDto[]
- `PUT /RoleTaskPropertiesAccess/attributes` — Обновить настройки доступности атрибутов задач для ролей · коды: 202, 400 · примеры
  ← body: RoleTaskAttributeDto[]

## Roles
- `GET /Roles` — Получить список ролей тенанта · коды: 200, 204, 206 · примеры
  ← query: isDeleted?:bool → RRGetResult[]
- `POST /Roles` — Создать роли · коды: 201, 400 · примеры
  ← body: ADMRAddData[] → int[]
- `PUT /Roles` — Обновить роли · коды: 202, 400 · примеры
  ← body: ADMRUpdateData[]
- `DELETE /Roles` — Удалить роли · коды: 202, 400 · примеры
  ← body: int[]
- `POST /Roles/copy` — Копировать роли · коды: 201, 400 · примеры
  ← body: ADMRCopyData[] → int[]
- `GET /Roles/{id}` — Получить информацию о роли · коды: 200, 204 · примеры
  ← path: id:int → RRGetResult
- `DELETE /Roles/{id}` — Удалить роль · коды: 202 · примеры
  ← path: id:int
- `GET /Roles/{roleID}/applications` — Получить список приложений роли · коды: 200, 204, 206 · примеры
  ← path: roleID:int → map<RRAListResult>
- `GET /Roles/{roleID}/attachments` — Получить список вложенных файлов роли · коды: 200, 204, 206 · примеры
  ← path: roleID:int → RCAttachmentResult[]
- `GET /Roles/{roleID}/packages` — Получить список расширений роли · коды: 200, 204, 206 · примеры
  ← path: roleID:int; query: searchText?:str → map<RRPListResult[]>
- `POST /Roles/{roleID}/packages` — Добавить расширения к роли · коды: 201, 400 · примеры
  ← path: roleID:int; body: ADMRPAddData[] → RRPPostResult[]
- `DELETE /Roles/{roleID}/packages` — Удалить расширения роли · коды: 202, 400 · примеры
  ← path: roleID:int; body: int[]
- `PUT /Roles/{roleID}/packages/activate` — Активировать расширения роли · коды: 202, 400 · примеры
  ← path: roleID:int; body: int[]
- `PUT /Roles/{roleID}/packages/deactivate` — Деактивировать расширения роли · коды: 202, 400 · примеры
  ← path: roleID:int; body: int[]
- `GET /Roles/{roleID}/permissionsApi` — Получить список API-полномочий роли · коды: 200, 204, 206 · примеры
  ← path: roleID:int; query: systemTagID?:str, isCheckedPermission?:bool → map<RRPAListResult[]>
- `GET /Roles/{roleID}/permissionsExt` — Получить список Ext-полномочий роли · коды: 200, 204, 206 · примеры
  ← path: roleID:int; query: systemTagID?:str, isCheckedPermission?:bool → map<RRPEListResult[]>
- `GET /Roles/{roleID}/permissionsUi` — Получить список UI-полномочий роли · коды: 200, 204, 206 · примеры
  ← path: roleID:int; query: systemTagID?:int, isCheckedPermission?:bool, isSystemPermission?:bool → map<RRPUListResult[]>

## SystemPermissionUiTags
- `GET /SystemPermissionUiTags` — Получить список тегов системных UI-полномочий · коды: 200, 204, 206 · примеры
  → map<RPUTListResult[]>

## TenantCreationRequests
- `POST /TenantCreationRequests` — Создать запрос на создание тенанта · коды: 201, 400 · примеры
  ← body: ADMTCRAddData → RTCRPostResult
- `GET /TenantCreationRequests/{id}` — Получить запрос на создание тенанта · коды: 200 · примеры
  ← path: id:str → RTCRGetResult
- `PUT /TenantCreationRequests/{id}/approve` — Утвердить запрос на создание тенанта · коды: 202, 400 · примеры
  ← path: id:str
- `PUT /TenantCreationRequests/{id}/reject` — Отклонить запрос на создание тенанта · коды: 202, 400 · примеры
  ← path: id:str; body: RejectData

## TenantMembers
- `GET /TenantMembers` — Получить список членов тенанта · коды: 200, 204, 206 · примеры
  → map<RTMListResult>
- `POST /TenantMembers` — Создать члена тенанта · коды: 201, 400 · примеры
  ← body: ADMTMAddData[] → int[]
- `PUT /TenantMembers` — Обновить данные члена тенанта · коды: 202, 400 · примеры
  ← body: ADMTMUpdateData[]
- `DELETE /TenantMembers` — Удалить членов тенанта · коды: 202, 400 · примеры
  ← body: int[]
- `GET /TenantMembers/anonymousUser` — Получить анонимного пользователя в текущем тенанте · коды: 200, 204 · примеры
  → RTMListResult
- `GET /TenantMembers/apiUser` — Получить пользователя API в текущем тенанте · коды: 200, 204 · примеры
  → RTMListResult
- `GET /TenantMembers/this` — Получить данные текущего члена тенанта · коды: 200 · примеры
  → RTMGetResult
- `GET /TenantMembers/{tenantMemberID}` — Получить данные члена тенанта · коды: 200 · примеры
  ← path: tenantMemberID:int → RTMGetResult
- `DELETE /TenantMembers/{tenantMemberID}` — Удалить члена тенанта · коды: 202 · примеры
  ← path: tenantMemberID:int

## TenantSettings
- `GET /TenantSettings` — Получить настройки тенанта · коды: 200, 204 · примеры
  ← query: tenantMemberId?:int → RTSGetResult
- `GET /TenantSettings/plateUrl` — Получить кастомный URL текущего тенанта · коды: 200, 204 · примеры
  ← query: taskTemplateID?:str → str
- `PUT /TenantSettings/plateUrl` — Обновить кастомный URL текущего тенанта · коды: 202 · примеры
  ← query: plateUrl?:str

## Tenants
- `GET /Tenants` — Получить список тенантов · коды: 200, 204, 206 · примеры
  → RTListResult[]
- `PUT /Tenants/licenses` — Обновить лицензию тенанта · коды: 202, 400 · примеры
  ← body: ADMTLUpdateData
- `GET /Tenants/templates` — Получить список шаблонных тенантов · коды: 200, 204, 206 · примеры
  → ITenantEntity[]
- `GET /Tenants/this` — Получить данные текущего тенанта · коды: 200 · примеры
  → RTGetResult
- `GET /Tenants/this/featureFlags` — Получить список флагов функций тенанта · коды: 200, 204 · примеры
  → str[]
- `GET /Tenants/this/licenses` — Получить список лицензий тенанта · коды: 200, 204 · примеры
  ← query: validOn?:datetime → ListTenantLicenseResult[]
- `POST /Tenants/this/licenses` — Добавить лицензию для тенанта · коды: 201, 400 · примеры
  ← body: ADMTLAddData
- `DELETE /Tenants/this/licenses` — Удалить лицензии тенанта · коды: 202, 400 · примеры
  ← body: int[]
- `POST /Tenants/this/licenses/renewal` — Отправить запрос на продление лицензии · коды: 200 · примеры
- `DELETE /Tenants/this/licenses/{id}` — Удалить лицензию тенанта · коды: 202 · примеры
  ← path: id:int
- `GET /Tenants/this/meta` — Получить метаданные тенанта · коды: 200, 204 · примеры
- `GET /Tenants/this/packages` — Получить список расширений тенанта · коды: 200, 204, 206 · примеры
  ← query: resourceID?:int[] → RTPListResult[]
- `POST /Tenants/this/packages` — Добавить расширение (только для кросс-тенантных администраторов) · коды: 200, 204, 400 · примеры
  ← body: ADDONPAddData → RTPListResult[]
- `PATCH /Tenants/this/packages` — Обновить расширение (только для кросс-тенантных администраторов) · коды: 202, 400 · примеры
  ← body: ADDONPUpdateData
- `DELETE /Tenants/this/packages` — Удалить расширение (только для кросс-тенантных администраторов) · коды: 202, 400 · примеры
  ← body: PackageIdentifier
- `POST /Tenants/this/packages/tenant` — Добавить расширение для тенанта · коды: 200, 204, 400 · примеры
  ← body: AddTenantPackageData → RTPListResult[]
- `DELETE /Tenants/this/packages/tenant` — Удалить расширение для тенанта · коды: 202, 400 · примеры
  ← body: PackageIdentifier
- `GET /Tenants/this/variables` — Получить список переменных окружения тенанта · коды: 200, 204, 206 · примеры
  → map<RTVListResult>
- `POST /Tenants/this/variables` — Добавить переменные окружения тенанта · коды: 201, 400 · примеры
  ← body: ADMTVAddData[]
- `PUT /Tenants/this/variables` — Обновить переменные окружения тенанта · коды: 202, 400 · примеры
  ← body: ADMTVUpdateData[]
- `DELETE /Tenants/this/variables` — Удалить переменные окружения тенанта · коды: 202, 400 · примеры
  ← body: str[]
- `DELETE /Tenants/this/variables/{name}` — Удалить переменную окружения тенанта · коды: 202 · примеры
  ← path: name:str

## UserAssetListQueries
- `POST /UserAssetListQueries` — Добавить сохраненные запросы объектов пользователям · коды: 201, 400 · примеры
  ← body: ADMUALQAddData[] → RUALQPostResult[]
- `DELETE /UserAssetListQueries` — Удалить сохраненные запросы объектов у пользователей · коды: 202, 400 · примеры
  ← body: ADMUALQDeleteData[]
- `POST /UserAssetListQueries/{userID}` — Добавить сохраненные запросы объектов пользователю · коды: 201, 400 · примеры
  ← path: userID:int; body: int[] → RUALQPostResult[]
- `DELETE /UserAssetListQueries/{userID}` — Удалить сохраненные запросы объектов у пользователя · коды: 202, 400 · примеры
  ← path: userID:int; body: int[]

## UserCompanyListQueries
- `POST /UserCompanyListQueries` — Добавляет сохраненные запросы пользователям · коды: 201, 400 · примеры
  ← body: ADMUCLQAddData[] → RUCLQPostResult[]
- `DELETE /UserCompanyListQueries` — Помечает как удалённые сохраненные запросы для пользователей · коды: 202, 400 · примеры
  ← body: ADMUCLQDeleteData[]
- `POST /UserCompanyListQueries/{userID}` — Добавляет сохраненные запросы пользователю · коды: 201, 400 · примеры
  ← path: userID:int; body: int[] → RUCLQPostResult[]
- `DELETE /UserCompanyListQueries/{userID}` — Помечает как удалённые сохраненные запросы для пользователя · коды: 202, 400 · примеры
  ← path: userID:int; body: int[]

## UserDisabledNotifications
- `POST /UserDisabledNotifications` — Изменить настройки уведомлений пользователя · коды: 202, 204, 400 · примеры
  ← body: DUDNPostData → RUDNMergeResult[]

## UserDistricts
- `POST /UserDistricts` — Добавить участки пользователю · коды: 201, 400 · примеры
  ← body: OperationDataOfADMUDAddData
- `PUT /UserDistricts` — Обновить участки у пользователя · коды: 202, 400 · примеры
  ← body: OperationDataOfADMUDUpdateData
- `DELETE /UserDistricts` — Удалить участки у пользователя · коды: 202, 400 · примеры
  ← body: OperationDataOfShort

## UserOrderBy
- `GET /UserOrderBy` — Получить список методов сортировки сотрудников · коды: 200, 204, 206 · примеры
  → map<RUOBListResult>

## UserRoles
- `POST /UserRoles` — Добавить роли пользователю · коды: 201, 400 · примеры
  ← body: DURPostData[]
- `DELETE /UserRoles` — Удалить роли у пользователя · коды: 202, 400 · примеры
  ← body: DURDeleteData[]

## UserTags
- `POST /UserTags` — Добавить теги пользователю · коды: 201, 400, 409 · примеры
  ← body: DUTPostData[] → RUTAddResult[]
- `DELETE /UserTags` — Удалить теги пользователя · коды: 202, 400 · примеры
  ← body: DUTDeleteData[]

## UserTaskListQueries
- `POST /UserTaskListQueries` — Добавить сохраненные запросы заявок пользователям · коды: 201, 400 · примеры
  ← body: ADMUTLQAddData[] → RUTLQPostResult[]
- `DELETE /UserTaskListQueries` — Удалить сохраненные запросы заявок у пользователей · коды: 202, 400 · примеры
  ← body: ADMUTLQDeleteData[]

## UserTemplateDistricts
- `POST /UserTemplateDistricts` — Добавить участки к шаблону пользователя · коды: 201, 400 · примеры
  ← body: ADMCActionDataOfShort[]
- `DELETE /UserTemplateDistricts/remove` — Удалить участки из шаблона пользователя · коды: 202, 400 · примеры
  ← body: ADMCActionDataOfShort[]

## UserTemplateRoles
- `POST /UserTemplateRoles` — Добавить роли к шаблону пользователя · коды: 201, 400 · примеры
  ← body: ADMCActionDataOfShort[]
- `DELETE /UserTemplateRoles/remove` — Удалить роли из шаблона пользователя · коды: 202, 400 · примеры
  ← body: ADMCActionDataOfShort[]

## UserTemplates
- `GET /UserTemplates` — Получить список шаблонов пользователя · коды: 200, 204, 206 · примеры
  ← query: searchText?:str, isTechnician?:bool, roleID?:int, districtID?:int → map<RUTListResult>
- `POST /UserTemplates` — Создать шаблон пользователя · коды: 201, 400 · примеры
  ← body: ADMUserTemplateAddData[] → int[]
- `PUT /UserTemplates` — Обновить шаблон пользователя · коды: 202, 400, 409 · примеры
  ← body: ADMUTUpdateData[]
- `DELETE /UserTemplates` — Удалить шаблоны пользователя · коды: 202, 400 · примеры
  ← body: int[]
- `GET /UserTemplates/{id}` — Получить шаблон пользователя · коды: 200, 204 · примеры
  ← path: id:int → RUTGetResult
- `DELETE /UserTemplates/{id}` — Удалить шаблон пользователя · коды: 202 · примеры
  ← path: id:int
- `GET /UserTemplates/{id}/districts` — Получить список участков шаблона пользователя · коды: 200, 204, 206 · примеры
  ← path: id:int → IdNameResultOfShort[]
- `GET /UserTemplates/{id}/roles` — Получить список ролей шаблона пользователя · коды: 200, 204, 206 · примеры
  ← path: id:int → IdNameResultOfShort[]

## UserWarehouses
- `POST /UserWarehouses` — Добавить склады пользователю · коды: 201, 400 · примеры
  ← body: UserWarehousesData[]
- `DELETE /UserWarehouses` — Удалить склады у пользователя · коды: 202, 400 · примеры
  ← body: UserWarehousesData[]

## Users
- `GET /Users` — Возвращает список пользователей · коды: 200, 204, 206 · примеры
  ← query: searchText?:str, includeTaskActuality?:bool, includeDistricts?:bool, needForAllowedTasks?:bool, orgUnitID?:int, districtID?:int, userID?:int, workTypeID?:int, skillID?:int, tag?:str, isDeleted?:bool, isCustomer?:bool, isTeam?:bool, isTechnician?:bool, isBanned?:bool, isOnShift?:bool, firstName?:str, lastName?:str, middleName?:str, position?:str, userTypeID?:int, companyID?:int, orderBy?:int, sortDirection?:int, erpID?:str, roleID?:int → map<RUUserResult>
- `POST /Users` — Добавить нового пользователя · коды: 201, 400, 409 · примеры
  ← query: skipAccountVerification?:bool; body: ADMUAddData → UserAddProjection
- `DELETE /Users` — Удалить нескольких пользователей · коды: 202, 409 · примеры
  ← body: int[]
- `HEAD /Users` — Возвращает заголовок запроса пользователей с количеством данных, удовлетворяющих фильтру · коды: 200 · примеры
  ← query: orgUnitID?:int, districtID?:int, userID?:int, workTypeID?:int, skillID?:int, tag?:str, isDeleted?:bool, isCustomer?:bool, isTeam?:bool, isTechnician?:bool, firstName?:str, lastName?:str, middleName?:str, position?:str, userTypeID?:int, erpID?:str
- `POST /Users/addbyintegration` — Добавить нового пользователя через интеграцию · коды: 200, 400, 409 · примеры
  ← query: skipAccountVerification?:bool; body: ADMUAddData → UserRoleAddProjection[]
- `POST /Users/anonymous` — Создать анонимного пользователя в тенанте · коды: 201 · примеры
  → ServiceUserResult
- `POST /Users/api` — Создать API-пользователя в тенанте · коды: 201 · примеры
  → ServiceUserResult
- `GET /Users/attributes` — Получить список атрибутов пользователей · коды: 200, 204, 206 · примеры
  ← query: attributeID?:int, userID?:int, IsRelevantForCustomer?:bool, IsRelevantForTechnician?:bool → UserAttributesResult[]
- `POST /Users/attributes` — Создать атрибуты для пользователей · коды: 201, 400 · примеры
  ← body: UserActionDataOfADMUAAttributeData[]
- `PUT /Users/attributes` — Обновить атрибуты пользователей · коды: 202, 400 · примеры
  ← body: UserActionDataOfADMUAAttributeData[]
- `DELETE /Users/attributes` — Удалить атрибуты пользователей · коды: 202, 400 · примеры
  ← body: UserActionDataOfShort[]
- `DELETE /Users/avatar` — Удалить аватары указанных пользователей · коды: 202 · примеры
  ← body: int[]
- `POST /Users/changeToCustomer` — Изменить тип пользователя на заказчика · коды: 202, 400 · примеры
  ← body: int[]
- `POST /Users/changeToStaff` — Изменить тип пользователя на сотрудника · коды: 202, 400 · примеры
  ← body: int[]
- `POST /Users/defaultPages` — Добавить стартовые страницы пользователей · коды: 201, 400, 409 · примеры
  ← body: UserStartPageDto[]
- `PUT /Users/defaultPages` — Изменить стартовые страницы пользователей · коды: 202, 400, 404, 409 · примеры
  ← body: UserStartPageDto[]
- `DELETE /Users/defaultPages` — Сбросить стартовые страницы у пользователей · коды: 202, 400 · примеры
  ← body: int[]
- `GET /Users/geolocation` — Получить список настроек точности сбора геокоординат для пользователей · коды: 200, 204, 206 · примеры
  ← query: userID?:int → UserGeolocationSettings[]
- `POST /Users/geolocation` — Добавить настройки точности сбора геокоординат для пользователей · коды: 201, 400 · примеры
  ← body: UserGeolocationDto[]
- `PUT /Users/geolocation` — Обновить настройки точности сбора геокоординат для пользователей · коды: 202, 400 · примеры
  ← body: UserGeolocationDto[]
- `GET /Users/profile` — Получить профиль пользователя · коды: 200, 404 · примеры
  ← query: tenantMemberId?:int, userId?:int → UserProfileResult
- `POST /Users/registration` — Саморегистрация пользователя по приглашению · коды: 201, 202, 204, 400, 409 · примеры
  ← body: DURegisterData → SelfRegisterResult
- `POST /Users/registration/verify` — Подтвердить регистрацию пользователя · коды: 202, 400, 409 · примеры
  ← body: RegistrationVerifyData → SelfRegisterResult
- `GET /Users/relevance` — Возвращает список пользователей по их релевантности к заявке · коды: 200, 204, 206 · примеры
  ← query: searchText?:str, includeTaskActuality?:bool, includeDistricts?:bool, assetID?:int, districtID?:int, workTypeID?:int, skillID?:int, levelOnShift?:bool, dateOnShift?:datetime, userTypeID?:int, isDeleted?:bool, isCustomer?:bool, isTechnician?:bool, isBanned?:bool → map<RUUserResult>
- `PUT /Users/restore` — Восстановить нескольких пользователей из удаленных · коды: 202, 409 · примеры
  ← body: int[]
- `GET /Users/short` — Возвращает список пользователей с усеченным набором полей (для справочников и ниспадающих списков) · коды: 200, 204, 206 · примеры
  ← query: searchText?:str, orgUnitID?:int, districtID?:int, userID?:int, workTypeID?:int, skillID?:int, tag?:str, isDeleted?:bool, isCustomer?:bool, isTeam?:bool, isTechnician?:bool, isBanned?:bool, firstName?:str, lastName?:str, middleName?:str, position?:str, userTypeID?:int, erpID?:str, roleID?:int → map<UserShortResult>
- `GET /Users/this/assetListQueries` — Получить список сохраненных запросов по объектам текущего пользователя · коды: 200, 204, 206 · примеры
  → map<AssetListQueryResult>
- `DELETE /Users/this/avatar` — Удалить аватар текущего пользователя · коды: 202 · примеры
- `PUT /Users/this/avatar/upload/fromBody` — Загрузить аватар текущего пользователя из тела запроса · коды: 200, 400, 409 · примеры
  ← body: FromBodyUploadData → UploadAttachmentResult
- `PUT /Users/this/avatar/upload/fromForm` — Загрузить аватар текущего пользователя из формы · коды: 200, 400, 409 · примеры
  ← body: { ContentLength?: int, ContentStream.CanRead?: bool, ContentStream.CanSeek?: bool, ContentStream.CanTimeout?: bool, ContentStream.CanWrite?: bool, ContentStream.Capacity?: int, ContentStream.Length?: int, ContentStream.Position?: int, ContentStream.ReadTimeout?: int, ContentStream.WriteTimeout?: int, ContentType?: str, Coordinate?: str, Description?: str, File: file, FileName?: str, IsIgnorePossibleDuplication?: bool, IsPublic?: bool, Md5Hash?: str, Roles?: int[], Uid?: uuid } → UploadAttachmentResult
- `GET /Users/this/companyListQueries` — Получить список сохраненных запросов по компаниям текущего пользователя · коды: 200, 204, 206 · примеры
  → map<CompanyListQueryResult>
- `GET /Users/this/geolocation` — Получить настройку точности сбора геокоординат текущего пользователя · коды: 200 · примеры
  → UserGeolocationSettings
- `GET /Users/this/notifications` — Получить список настроек уведомлений текущего пользователя · коды: 200, 204, 206 · примеры
  → RUDNListResult
- `GET /Users/this/permissions/ext` — Получить список расширенных полномочий текущего пользователя · коды: 200, 204, 206 · примеры
  → map<str>
- `GET /Users/this/permissions/ui` — Получить список UI полномочий текущего пользователя · коды: 200, 204, 206 · примеры
  → map<str>
- `GET /Users/this/profile` — Получить профиль текущего пользователя · коды: 200 · примеры
  → UserProfileResult
- `GET /Users/this/taskListQueries` — Получить список сохраненных запросов по заявкам текущего пользователя · коды: 200, 204, 206 · примеры
  → map<TaskListQueryResult>
- `GET /Users/{UserID}/ratings` — Получить рейтинг инженера · коды: 200, 204, 206 · примеры
  ← path: userID:int → RatingTechnicianResult
- `GET /Users/{id}` — Получить детальную информацию о пользователе · коды: 200, 400, 404 · примеры
  ← path: id:int → DetailedInfoResult
- `PUT /Users/{id}` — Обновить данные пользователя · коды: 202, 400, 404 · примеры
  ← path: id:int; body: ADMUUpdateData
- `GET /Users/{id}/assetListQueries` — Получить список сохраненных запросов по объектам пользователя · коды: 200, 204, 206 · примеры
  ← path: id:int → map<AssetListQueryResult>
- `DELETE /Users/{id}/avatar` — Удалить аватар указанного пользователя · коды: 202 · примеры
  ← path: id:int
- `PUT /Users/{id}/avatar/upload/fromBody` — Загрузить аватар пользователя из тела запроса · коды: 200, 400, 409 · примеры
  ← path: id:int; body: FromBodyUploadData → UploadAttachmentResult
- `PUT /Users/{id}/avatar/upload/fromForm` — Загрузить аватар пользователя из формы · коды: 200, 400, 409 · примеры
  ← path: id:int; body: { ContentLength?: int, ContentStream.CanRead?: bool, ContentStream.CanSeek?: bool, ContentStream.CanTimeout?: bool, ContentStream.CanWrite?: bool, ContentStream.Capacity?: int, ContentStream.Length?: int, ContentStream.Position?: int, ContentStream.ReadTimeout?: int, ContentStream.WriteTimeout?: int, ContentType?: str, Coordinate?: str, Description?: str, File: file, FileName?: str, IsIgnorePossibleDuplication?: bool, IsPublic?: bool, Md5Hash?: str, Roles?: int[], Uid?: uuid } → UploadAttachmentResult
- `GET /Users/{id}/companyListQueries` — Получить список сохраненных запросов по компаниям пользователя · коды: 200, 204, 206 · примеры
  ← path: id:int → map<CompanyListQueryResult>
- `GET /Users/{id}/districts` — Получить список участков пользователя · коды: 200, 204, 206 · примеры
  ← path: id:int → map<ListDistrictResult>
- `GET /Users/{id}/notifications` — Получить список настроек уведомлений пользователя · коды: 200, 204, 206 · примеры
  ← path: id:int → RUDNListResult
- `GET /Users/{id}/profile` — Получить профиль пользователя · коды: 200, 404 · примеры
  ← path: id:int → UserProfileResult
- `GET /Users/{id}/roles` — Получить список ролей пользователя · коды: 200, 204, 206 · примеры
  ← path: id:int → map<IdNameResultOfShort[]>
- `GET /Users/{id}/taskListQueries` — Получить список сохраненных запросов по заявкам пользователя · коды: 200, 204, 206 · примеры
  ← path: id:int → map<TaskListQueryResult>
- `GET /Users/{id}/warehouses` — Получить список складов пользователя · коды: 200, 204, 206 · примеры
  ← path: id:int → IdNameErpIDResultOfShort[]
- `DELETE /Users/{userID}` — Удалить пользователя · коды: 202, 409 · примеры
  ← path: userID:int
- `GET /Users/{userID}/assetAssignments` — Получить список объектов, назначенных пользователю · коды: 200, 204, 206 · примеры
  ← path: userID:int; query: assetID?:int, validOn?:datetime → AssetAssignmentResult[]
- `GET /Users/{userID}/attributes` — Получить атрибуты пользователя · коды: 200, 204, 206 · примеры
  ← path: userID:int; query: attributeID?:int, IsRelevantForCustomer?:bool, IsRelevantForTechnician?:bool → UserAttributesResult[]
- `POST /Users/{userID}/attributes` — Создать атрибуты пользователя · коды: 201, 400 · примеры
  ← path: userID:int; body: ADMUAAttributeData[]
- `PUT /Users/{userID}/attributes` — Обновить атрибуты пользователя · коды: 202, 400 · примеры
  ← path: userID:int; body: ADMUAAttributeData[]
- `DELETE /Users/{userID}/attributes` — Удалить атрибуты пользователя · коды: 202, 400 · примеры
  ← path: userID:int; body: int[]
- `GET /Users/{userID}/defaultPages` — Получить текущие стартовые страницы пользователя · коды: 200, 204, 400 · примеры
  ← path: userID:int → RUDPGetResult
- `POST /Users/{userID}/geolocation` — Добавить настройку точности сбора геокоординат для пользователя · коды: 201, 400 · примеры
  ← path: userID:int; query: coordinateAccuracyID?:int
- `PUT /Users/{userID}/geolocation` — Обновить настройку точности сбора геокоординат для пользователя · коды: 202, 400 · примеры
  ← path: userID:int; query: coordinateAccuracyID?:int
- `PUT /Users/{userID}/resendinvitation` — Повторно отправить приглашение пользователю · коды: 202, 204 · примеры
  ← path: userID:int
- `PUT /Users/{userID}/restore` — Восстановить пользователя из удаленных · коды: 202, 409 · примеры
  ← path: userID:int
- `GET /Users/{userID}/skills` — Получить список навыков пользователя · коды: 200, 204, 206 · примеры
  ← path: userID:int → map<SkillResult>
- `GET /Users/{userID}/tags` — Получить список тегов пользователя · коды: 200, 204, 206 · примеры
  ← path: userID:int → str[]
