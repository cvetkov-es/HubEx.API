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
- Tenants — строки 232–275
- UserAssetListQueries — строки 277–285
- UserCompanyListQueries — строки 287–295
- UserDisabledNotifications — строки 297–299
- UserDistricts — строки 301–307
- UserOrderBy — строки 309–311
- UserRoles — строки 313–317
- UserTags — строки 319–323
- UserTaskListQueries — строки 325–329
- UserTemplateDistricts — строки 331–335
- UserTemplateRoles — строки 337–341
- UserTemplates — строки 343–359
- UserWarehouses — строки 361–365
- Users — строки 367–494

## BanReasons
- `GET /BanReasons` — Получить список причин блокировки пользователя · коды: 200, 204, 206 · примеры
  → map<ResultsBanReasonsListResult>

## Capabilities
- `GET /Capabilities` — Получить список возможностей работы с элементами интерфейса · коды: 200, 204, 206 · примеры
  → map<ResultsCapabilitiesListResult>

## DefaultPages
- `GET /DefaultPages` — Получить список доступных стартовых страниц · коды: 200, 204, 400 · примеры
  ← query: applicationID?:int → ResultsDefaultPagesAllowedPageResult[]

## GeolocationSettings
- `GET /GeolocationSettings/coordinateAccuracy` — Получить список настроек точности сбора геокоординат · коды: 200, 204 · примеры
  → IdNameDescriptionEntityOfByte[]

## Invitations
- `GET /Invitations` · paginated · коды: 200, 204, 206
  ← query: userTemplateID?:int → map<ResultsInvitationsGetResult>
- `POST /Invitations` — Создать приглашения · коды: 201, 202, 400 · примеры
  ← body: ADMInvitationAddData[] → ResultsInvitationsAddResult[]
- `PUT /Invitations` — Обновить приглашения · коды: 202, 400 · примеры
  ← body: ADMInvitationUpdateData[]
- `DELETE /Invitations` — Удалить приглашения · коды: 202, 400 · примеры
  ← body: uuid[]
- `GET /Invitations/{id}` — Получить расширенную информацию о приглашении · коды: 200 · примеры
  ← path: id:uuid → ResultsInvitationsGetResult
- `DELETE /Invitations/{id}` — Удалить приглашение · коды: 202 · примеры
  ← path: id:uuid
- `GET /Invitations/{id}/short` — Получить сокращенную информацию о приглашении · коды: 200 · примеры
  ← path: id:uuid → ResultsInvitationsGetShortResult

## PermissionApiTags
- `GET /PermissionApiTags` — Получить список тегов API-полномочий · коды: 200, 204, 206 · примеры
  → map<ResultsPermissionsApiTagListResult[]>

## PermissionExtTags
- `GET /PermissionExtTags` — Получить список тегов расширенных полномочий · коды: 200, 204, 206 · примеры
  → map<ResultsPermissionsExtTagListResult[]>

## PermissionsApi
- `GET /PermissionsApi` — Получить список API-полномочий · коды: 200, 204, 206 · примеры
  → map<ResultsPermissionsApiListResult>

## PermissionsExt
- `GET /PermissionsExt` — Получить список расширенных полномочий · коды: 200, 204, 206 · примеры
  → map<ResultsPermissionsExtListResult>

## PermissionsUi
- `GET /PermissionsUi` — Получить список UI полномочий · коды: 200, 204, 206 · примеры
  → map<ResultsPermissionsUiGetResult>
- `POST /PermissionsUi` — Создать UI полномочия · коды: 201, 400 · примеры
  ← body: ADMPermissionUiAddData[] → int[]
- `PUT /PermissionsUi` — Обновить UI полномочия · коды: 202, 400 · примеры
  ← body: ADMPermissionUiUpdateData[]
- `DELETE /PermissionsUi` — Удалить UI полномочия · коды: 202, 400 · примеры
  ← body: int[]
- `GET /PermissionsUi/{id}` — Получить данные UI полномочия · коды: 200, 204, 206 · примеры
  ← path: id:int → ResultsPermissionsUiGetResult
- `DELETE /PermissionsUi/{id}` — Удалить UI полномочие · коды: 202 · примеры
  ← path: id:int

## RoleApplications
- `POST /RoleApplications` — Добавить или обновить приложения для ролей · коды: 201, 400 · примеры
  ← body: RoleApplicationBaseBaseData[] → ResultsRoleApplicationMergeResult[]
- `DELETE /RoleApplications` — Удалить приложения для ролей · коды: 202, 400 · примеры
  ← body: RoleApplicationBaseBaseData[]

## RoleAttachments
- `POST /RoleAttachments` — Добавить роли для доступа к файлам · коды: 201, 400 · примеры
  ← body: ADMRoleAttachmentAddData[] → ResultsRoleAttachmentsPostResult[]
- `DELETE /RoleAttachments` — Удалить доступ ролей к файлам · коды: 202, 400 · примеры
  ← body: ADMRoleAttachmentDeleteData[]

## RolePermissionsApi
- `POST /RolePermissionsApi` — Создать связи роли с API-полномочиями · коды: 201, 400 · примеры
  ← body: ADMRolePermissionApiAddData[] → ResultsRolePermissionsApiPostResult[]
- `DELETE /RolePermissionsApi` — Удалить связи роли с API-полномочиями · коды: 202, 400 · примеры
  ← body: ADMRolePermissionApiDeleteData[]

## RolePermissionsExt
- `POST /RolePermissionsExt` — Создать связи роли с Ext-полномочиями · коды: 201, 400 · примеры
  ← body: ADMRolePermissionExtAddData[] → ResultsRolePermissionsExtPostResult[]
- `DELETE /RolePermissionsExt` — Удалить связи роли с Ext-полномочиями · коды: 202, 400 · примеры
  ← body: ADMRolePermissionExtDeleteData[]

## RolePermissionsUi
- `POST /RolePermissionsUi` — Создать связи роли с UI-полномочиями · коды: 201, 400 · примеры
  ← body: ADMRolePermissionUiAddData[] → ResultsRolePermissionsUiPostResult[]
- `DELETE /RolePermissionsUi` — Удалить связи роли с UI-полномочиями · коды: 202, 400 · примеры
  ← body: ADMRolePermissionUiDeleteData[]

## RoleTaskListQueries
- `POST /RoleTaskListQueries` — Добавить сохраненные запросы заявок для роли · коды: 201, 400 · примеры
  ← body: ADMRoleTaskListQueryAddData[] → ResultsRoleTaskListQueriesPostResult[]
- `DELETE /RoleTaskListQueries` — Удалить сохраненные запросы заявок у роли · коды: 202, 400 · примеры
  ← body: ADMRoleTaskListQueryDeleteData[]

## RoleTaskPropertiesAccess
- `GET /RoleTaskPropertiesAccess/attributes` · paginated · коды: 200, 204, 206
  ← query: roleID?:int → ResultsRoleTaskAttributeRoleTaskAttributeSettings[]
- `POST /RoleTaskPropertiesAccess/attributes` — Добавить настройки доступности атрибутов задач для ролей · коды: 201, 400 · примеры
  ← body: DataADMRoleTaskAttributeDto[]
- `PUT /RoleTaskPropertiesAccess/attributes` — Обновить настройки доступности атрибутов задач для ролей · коды: 202, 400 · примеры
  ← body: DataADMRoleTaskAttributeDto[]

## Roles
- `GET /Roles` — Получить список ролей тенанта · коды: 200, 204, 206 · примеры
  ← query: isDeleted?:bool → map<ResultsRolesGetResult>
- `POST /Roles` — Создать роли · коды: 201, 400 · примеры
  ← body: ADMRoleAddData[] → int[]
- `PUT /Roles` — Обновить роли · коды: 202, 400 · примеры
  ← body: ADMRoleUpdateData[]
- `DELETE /Roles` — Удалить роли · коды: 202, 400 · примеры
  ← body: int[]
- `POST /Roles/copy` — Копировать роли · коды: 201, 400 · примеры
  ← body: ADMRoleCopyData[] → int[]
- `GET /Roles/{id}` — Получить информацию о роли · коды: 200, 204 · примеры
  ← path: id:int → ResultsRolesGetResult
- `DELETE /Roles/{id}` — Удалить роль · коды: 202 · примеры
  ← path: id:int
- `GET /Roles/{roleID}/applications` — Получить список приложений роли · коды: 200, 204, 206 · примеры
  ← path: roleID:int → map<ResultsRoleApplicationListResult>
- `GET /Roles/{roleID}/attachments` — Получить список вложенных файлов роли · коды: 200, 204, 206 · примеры
  ← path: roleID:int → ResultsCommonAttachmentResult[]
- `GET /Roles/{roleID}/packages` — Получить список расширений роли · коды: 200, 204, 206 · примеры
  ← path: roleID:int; query: searchText?:str → map<ResultsRolePackagesListResult[]>
- `POST /Roles/{roleID}/packages` — Добавить расширения к роли · коды: 201, 400 · примеры
  ← path: roleID:int; body: ADMRolePackageAddData[] → ResultsRolePackagesPostResult[]
- `DELETE /Roles/{roleID}/packages` — Удалить расширения роли · коды: 202, 400 · примеры
  ← path: roleID:int; body: int[]
- `PUT /Roles/{roleID}/packages/activate` — Активировать расширения роли · коды: 202, 400 · примеры
  ← path: roleID:int; body: int[]
- `PUT /Roles/{roleID}/packages/deactivate` — Деактивировать расширения роли · коды: 202, 400 · примеры
  ← path: roleID:int; body: int[]
- `GET /Roles/{roleID}/permissionsApi` — Получить список API-полномочий роли · коды: 200, 204, 206 · примеры
  ← path: roleID:int; query: systemTagID?:str, isCheckedPermission?:bool → map<ResultsRolePermissionsApiListResult[]>
- `GET /Roles/{roleID}/permissionsExt` — Получить список Ext-полномочий роли · коды: 200, 204, 206 · примеры
  ← path: roleID:int; query: systemTagID?:str, isCheckedPermission?:bool → map<ResultsRolePermissionsExtListResult[]>
- `GET /Roles/{roleID}/permissionsUi` — Получить список UI-полномочий роли · коды: 200, 204, 206 · примеры
  ← path: roleID:int; query: systemTagID?:int, isCheckedPermission?:bool, isSystemPermission?:bool → map<ResultsRolePermissionsUiListResult[]>

## SystemPermissionUiTags
- `GET /SystemPermissionUiTags` — Получить список тегов системных UI-полномочий · коды: 200, 204, 206 · примеры
  → map<ResultsPermissionsUiTagListResult[]>

## TenantCreationRequests
- `POST /TenantCreationRequests` — Создать запрос на создание тенанта · коды: 201, 400 · примеры
  ← body: ADMTenantCreationRequestAddData → ResultsTenantCreationRequestsPostResult
- `GET /TenantCreationRequests/{id}` — Получить запрос на создание тенанта · коды: 200 · примеры
  ← path: id:str → ResultsTenantCreationRequestsGetResult
- `PUT /TenantCreationRequests/{id}/approve` — Утвердить запрос на создание тенанта · коды: 202, 400 · примеры
  ← path: id:str
- `PUT /TenantCreationRequests/{id}/reject` — Отклонить запрос на создание тенанта · коды: 202, 400 · примеры
  ← path: id:str; body: ADMTenantCreationRequestRejectData

## TenantMembers
- `GET /TenantMembers` · paginated · коды: 200, 204, 206
  → map<ResultsTenantMembersListResult>
- `POST /TenantMembers` — Создать члена тенанта · коды: 201, 400 · примеры
  ← body: ADMTenantMemberAddData[] → int[]
- `PUT /TenantMembers` — Обновить данные члена тенанта · коды: 202, 400 · примеры
  ← body: ADMTenantMemberUpdateData[]
- `DELETE /TenantMembers` — Удалить членов тенанта · коды: 202, 400 · примеры
  ← body: int[]
- `GET /TenantMembers/anonymousUser` — Получить анонимного пользователя в текущем тенанте · коды: 200, 204 · примеры
  → ResultsTenantMembersListResult
- `GET /TenantMembers/apiUser` — Получить пользователя API в текущем тенанте · коды: 200, 204 · примеры
  → ResultsTenantMembersListResult
- `GET /TenantMembers/this` — Получить данные текущего члена тенанта · коды: 200 · примеры
  → ResultsTenantMembersGetResult
- `GET /TenantMembers/{tenantMemberID}` — Получить данные члена тенанта · коды: 200, 500 · примеры
  ← path: tenantMemberID:int → ResultsTenantMembersGetResult
- `DELETE /TenantMembers/{tenantMemberID}` — Удалить члена тенанта · коды: 202 · примеры
  ← path: tenantMemberID:int

## TenantSettings
- `GET /TenantSettings` — Получить настройки тенанта · коды: 200, 204, 500 · примеры
  ← query: tenantMemberId?:int → ResultsTenantSettingsGetResult
- `GET /TenantSettings/plateUrl` — Получить кастомный URL текущего тенанта · коды: 200, 204 · примеры
  ← query: taskTemplateID?:str → str
- `PUT /TenantSettings/plateUrl` — Обновить кастомный URL текущего тенанта · коды: 202 · примеры
  ← query: plateUrl?:str

## Tenants
- `GET /Tenants` — Получить список тенантов · коды: 200, 204, 206 · примеры
  → ResultsTenantsListResult[]
- `PUT /Tenants/licenses` — Обновить лицензию тенанта · коды: 202, 400 · примеры
  ← body: ADMTenantLicenseUpdateData
- `GET /Tenants/templates` — Получить список шаблонных тенантов · коды: 200, 204, 206 · примеры
  → InterfacesEntitiesITenantEntity[]
- `GET /Tenants/this` — Получить данные текущего тенанта · коды: 200 · примеры
  → ResultsTenantsGetResult
- `GET /Tenants/this/featureFlags` — Получить список флагов функций тенанта · коды: 200, 204 · примеры
  → str[]
- `GET /Tenants/this/licenses` — Получить список лицензий тенанта · коды: 200, 204 · примеры
  ← query: validOn?:datetime → ResultsTenantLicenseListTenantLicenseResult
- `POST /Tenants/this/licenses` — Добавить лицензию для тенанта · коды: 201, 400 · примеры
  ← body: ADMTenantLicenseAddData
- `DELETE /Tenants/this/licenses` — Удалить лицензии тенанта · коды: 202, 400 · примеры
  ← body: int[]
- `POST /Tenants/this/licenses/renewal` — Отправить запрос на продление лицензии · коды: 200, 500 · примеры
- `DELETE /Tenants/this/licenses/{id}` — Удалить лицензию тенанта · коды: 202 · примеры
  ← path: id:int
- `GET /Tenants/this/meta` — Получить метаданные тенанта · коды: 200, 204 · примеры
- `GET /Tenants/this/packages` · paginated · коды: 200, 204, 206
  ← query: resourceID?:int[] → ResultsTenantPackagesListResult[]
  Для выполнения данного метода пользователь должен быть **TenantMember**.
- `POST /Tenants/this/packages` — Добавить расширение (только для кросс-тенантных администраторов) · коды: 200, 204, 206, 400 · примеры
  ← body: ADDONPackageAddData → ResultsTenantPackagesListResult[]
- `PATCH /Tenants/this/packages` — Обновить расширение (только для кросс-тенантных администраторов) · коды: 202, 400 · примеры
  ← body: ADDONPackageUpdateData
- `DELETE /Tenants/this/packages` — Удалить расширение (только для кросс-тенантных администраторов) · коды: 202, 400 · примеры
  ← body: ADDONPackagePackageIdentifier
- `POST /Tenants/this/packages/tenant` — Добавить расширение для тенанта · коды: 200, 204, 206, 400 · примеры
  ← body: ADDONPackageAddTenantPackageData → ResultsTenantPackagesListResult[]
- `DELETE /Tenants/this/packages/tenant` — Удалить расширение для тенанта · коды: 202, 400 · примеры
  ← body: ADDONPackagePackageIdentifier
- `GET /Tenants/this/variables` — Получить список переменных окружения тенанта · коды: 200, 204, 206 · примеры
  → map<ResultsTenantVariablesListResult>
- `POST /Tenants/this/variables` — Добавить переменные окружения тенанта · коды: 201, 400 · примеры
  ← body: ADMTenantVariableAddData[]
- `PUT /Tenants/this/variables` — Обновить переменные окружения тенанта · коды: 202, 400 · примеры
  ← body: ADMTenantVariableUpdateData[]
- `DELETE /Tenants/this/variables` — Удалить переменные окружения тенанта · коды: 202, 400 · примеры
  ← body: str[]
- `DELETE /Tenants/this/variables/{name}` — Удалить переменную окружения тенанта · коды: 202 · примеры
  ← path: name:str

## UserAssetListQueries
- `POST /UserAssetListQueries` — Добавить сохраненные запросы объектов пользователям · коды: 201, 400 · примеры
  ← body: ADMUserAssetListQueryAddData[] → ResultsUserAssetListQueriesPostResult[]
- `DELETE /UserAssetListQueries` — Удалить сохраненные запросы объектов у пользователей · коды: 202, 400 · примеры
  ← body: ADMUserAssetListQueryDeleteData[]
- `POST /UserAssetListQueries/{userID}` — Добавить сохраненные запросы объектов пользователю · коды: 201, 400 · примеры
  ← path: userID:int; body: int[] → ResultsUserAssetListQueriesPostResult[]
- `DELETE /UserAssetListQueries/{userID}` — Удалить сохраненные запросы объектов у пользователя · коды: 202, 400 · примеры
  ← path: userID:int; body: int[]

## UserCompanyListQueries
- `POST /UserCompanyListQueries` — Добавляет сохраненные запросы пользователям · коды: 201
  ← body: ADMUserCompanyListQueryAddData[] → ResultsUserCompanyListQueriesPostResult[]
- `DELETE /UserCompanyListQueries` — Помечает как удалённые сохраненные запросы для пользователей · коды: 202
  ← body: ADMUserCompanyListQueryDeleteData[]
- `POST /UserCompanyListQueries/{userID}` — Добавляет сохраненные запросы пользователю · коды: 201
  ← path: userID:int; body: int[] → ResultsUserCompanyListQueriesPostResult[]
- `DELETE /UserCompanyListQueries/{userID}` — Помечает как удалённые сохраненные запросы для пользователя · коды: 202
  ← path: userID:int; body: int[]

## UserDisabledNotifications
- `POST /UserDisabledNotifications` — Изменить настройки уведомлений пользователя · коды: 202, 204, 400, 500 · примеры
  ← body: DataUserDisabledNotificationsPostData → ResultsUserDisabledNotificationsMergeResult[]

## UserDistricts
- `POST /UserDistricts` — Добавить участки пользователю · коды: 201, 400, 500 · примеры
  ← body: OperationDataOfAddData
- `PUT /UserDistricts` — Обновить участки у пользователя · коды: 202, 400, 500 · примеры
  ← body: OperationDataOfUpdateData
- `DELETE /UserDistricts` — Удалить участки у пользователя · коды: 202, 400, 500 · примеры
  ← body: OperationDataOfShort

## UserOrderBy
- `GET /UserOrderBy` — Получить список методов сортировки сотрудников · коды: 200, 204, 206 · примеры
  → map<ResultsUserOrderByListResult>

## UserRoles
- `POST /UserRoles` — Добавить роли пользователю · коды: 201, 400, 500 · примеры
  ← body: DataUserRolesPostData[]
- `DELETE /UserRoles` — Удалить роли у пользователя · коды: 202, 400, 500 · примеры
  ← body: DataUserRolesDeleteData[]

## UserTags
- `POST /UserTags` — Добавить теги пользователю · коды: 201, 400, 409 · примеры
  ← body: DataUserTagsPostData[] → ResultsUserTagAddResult[]
- `DELETE /UserTags` — Удалить теги пользователя · коды: 202, 400 · примеры
  ← body: DataUserTagsDeleteData[]

## UserTaskListQueries
- `POST /UserTaskListQueries` — Добавить сохраненные запросы заявок пользователям · коды: 201, 400 · примеры
  ← body: ADMUserTaskListQueryAddData[] → ResultsUserTaskListQueriesPostResult[]
- `DELETE /UserTaskListQueries` — Удалить сохраненные запросы заявок у пользователей · коды: 202, 400 · примеры
  ← body: ADMUserTaskListQueryDeleteData[]

## UserTemplateDistricts
- `POST /UserTemplateDistricts` — Добавить участки к шаблону пользователя · коды: 201, 400, 500 · примеры
  ← body: ActionDataOfShort[]
- `DELETE /UserTemplateDistricts/remove` — Удалить участки из шаблона пользователя · коды: 202, 400, 500 · примеры
  ← body: ActionDataOfShort[]

## UserTemplateRoles
- `POST /UserTemplateRoles` — Добавить роли к шаблону пользователя · коды: 201, 400, 500 · примеры
  ← body: ActionDataOfShort[]
- `DELETE /UserTemplateRoles/remove` — Удалить роли из шаблона пользователя · коды: 202, 400, 500 · примеры
  ← body: ActionDataOfShort[]

## UserTemplates
- `GET /UserTemplates` · paginated · коды: 200, 204, 206
  ← query: searchText?:str, isTechnician?:bool, roleID?:int, districtID?:int → map<ResultsUserTemplatesListResult>
- `POST /UserTemplates` — Создать шаблон пользователя · коды: 201, 400 · примеры
  ← body: ADMUserTemplateAddData[] → int[]
- `PUT /UserTemplates` — Обновить шаблон пользователя · коды: 202, 400, 409 · примеры
  ← body: ADMUserTemplateUpdateData[]
- `DELETE /UserTemplates` — Удалить шаблоны пользователя · коды: 202, 400 · примеры
  ← body: int[]
- `GET /UserTemplates/{id}` — Получить шаблон пользователя · коды: 200, 204 · примеры
  ← path: id:int → ResultsUserTemplatesGetResult
- `DELETE /UserTemplates/{id}` — Удалить шаблон пользователя · коды: 202 · примеры
  ← path: id:int
- `GET /UserTemplates/{id}/districts` — Получить список участков шаблона пользователя · коды: 200, 204, 206 · примеры
  ← path: id:int → IdNameResultOfShort[]
- `GET /UserTemplates/{id}/roles` — Получить список ролей шаблона пользователя · коды: 200, 204, 206 · примеры
  ← path: id:int → IdNameResultOfShort[]

## UserWarehouses
- `POST /UserWarehouses` — Добавить склады пользователю · коды: 201, 400, 500 · примеры
  ← body: WHWarehouseUserUserWarehousesData[]
- `DELETE /UserWarehouses` — Удалить склады у пользователя · коды: 202, 400, 500 · примеры
  ← body: WHWarehouseUserUserWarehousesData[]

## Users
- `GET /Users` — Возвращает список пользователей · paginated · коды: 200, 206
  ← query: searchText?:str, includeTaskActuality?:bool, includeDistricts?:bool, needForAllowedTasks?:bool, orgUnitID?:int, districtID?:int, userID?:int, workTypeID?:int, skillID?:int, tag?:str, isDeleted?:bool, isCustomer?:bool, isTeam?:bool, isTechnician?:bool, isBanned?:bool, isOnShift?:bool, firstName?:str, lastName?:str, middleName?:str, position?:str, userTypeID?:int, companyID?:int, orderBy?:int, sortDirection?:int, erpID?:str, roleID?:int → map<ResultsUsersUserResult>
- `POST /Users` — Добавить нового пользователя · коды: 201, 400, 409 · примеры
  ← query: skipAccountVerification?:bool, skipAccountVerification?:bool; body: ADMUserAddData → ProjectionsADMUserAddProjection
- `DELETE /Users` — Удалить нескольких пользователей · коды: 202, 409 · примеры
  ← body: int[]
- `HEAD /Users` — Возвращает заголовок запроса пользователей с количеством данных, удовлетворяющих фильтру · коды: 200
  ← query: orgUnitID?:int, districtID?:int, userID?:int, workTypeID?:int, skillID?:int, tag?:str, isDeleted?:bool, isCustomer?:bool, isTeam?:bool, isTechnician?:bool, firstName?:str, lastName?:str, middleName?:str, position?:str, userTypeID?:int, erpID?:str
- `POST /Users/addbyintegration` — Добавить нового пользователя через интеграцию · коды: 200, 400, 409 · примеры
  ← query: skipAccountVerification?:bool, skipAccountVerification?:bool; body: ADMUserAddData → ProjectionsADMUserRoleAddProjection[]
- `POST /Users/anonymous` — Создать анонимного пользователя в тенанте · коды: 201 · примеры
  → DataUsersServiceUserResult
- `POST /Users/api` — Создать API-пользователя в тенанте · коды: 201 · примеры
  → DataUsersServiceUserResult
- `GET /Users/attributes` — Получить список атрибутов пользователей · коды: 200, 204, 206 · примеры
  ← query: attributeID?:int, userID?:int, IsRelevantForCustomer?:bool, IsRelevantForTechnician?:bool → ResultsUserAttributeUserAttributesResult[]
- `POST /Users/attributes` — Создать атрибуты для пользователей · коды: 201, 400 · примеры
  ← body: UserActionDataOfAttributeData[]
- `PUT /Users/attributes` — Обновить атрибуты пользователей · коды: 202, 400 · примеры
  ← body: UserActionDataOfAttributeData[]
- `DELETE /Users/attributes` — Удалить атрибуты пользователей · коды: 202, 400 · примеры
  ← body: UserActionDataOfShort[]
- `DELETE /Users/avatar` — Удаляет аватку для указанного списка пользователей. · коды: 202
  ← body: int[]
- `POST /Users/changeToCustomer` — Изменить тип пользователя на заказчика · коды: 202, 400 · примеры
  ← body: int[]
- `POST /Users/changeToStaff` — Изменить тип пользователя на сотрудника · коды: 202, 400 · примеры
  ← body: int[]
- `POST /Users/defaultPages` — Добавить стартовые страницы пользователей · коды: 201, 400, 409 · примеры
  ← body: ADMUserDefaultPagesUserStartPageDto[]
- `PUT /Users/defaultPages` — Изменить стартовые страницы пользователей · коды: 202, 400, 404 · примеры
  ← body: ADMUserDefaultPagesUserStartPageDto[]
- `DELETE /Users/defaultPages` — Сбросить стартовые страницы у пользователей · коды: 202, 400 · примеры
  ← body: int[]
- `GET /Users/geolocation` — Получить список настроек точности сбора геокоординат для пользователей · коды: 200, 204, 206 · примеры
  ← query: userID?:int → ResultsCoordinateAccuracyUserGeolocationSettings[]
- `POST /Users/geolocation` — Добавить настройки точности сбора геокоординат для пользователей · коды: 201, 400 · примеры
  ← body: DataADMUserGeolocationDto[]
- `PUT /Users/geolocation` — Обновить настройки точности сбора геокоординат для пользователей · коды: 202, 400 · примеры
  ← body: DataADMUserGeolocationDto[]
- `GET /Users/profile` — Получить профиль пользователя · коды: 200, 404 · примеры
  ← query: tenantMemberId?:int, userId?:int → ResultsUsersUserProfileResult
- `POST /Users/registration` — Саморегистрация пользователя по приглашению · коды: 201, 202, 409 · примеры
  ← body: DataUsersRegisterData → ResultsUsersSelfRegisterResult
- `POST /Users/registration/verify` — Подтвердить регистрацию пользователя · коды: 202 · примеры
  ← body: DataUsersRegistrationVerifyData → ResultsUsersSelfRegisterResult
- `GET /Users/relevance` — Возвращает список пользователей по их релевантности к заявке · paginated · коды: 200, 206
  ← query: searchText?:str, includeTaskActuality?:bool, includeDistricts?:bool, assetID?:int, districtID?:int, workTypeID?:int, skillID?:int, levelOnShift?:bool, dateOnShift?:datetime, userTypeID?:int, isDeleted?:bool, isCustomer?:bool, isTechnician?:bool, isBanned?:bool → map<ResultsUsersUserResult>
- `PUT /Users/restore` — Восстановить нескольких пользователей из удаленных · коды: 202, 409 · примеры
  ← body: int[]
- `GET /Users/short` — Возвращает список пользователей с усеченным набором полей (для справочников и ниспадающих списков) · paginated · коды: 200, 206
  ← query: searchText?:str, orgUnitID?:int, districtID?:int, userID?:int, workTypeID?:int, skillID?:int, tag?:str, isDeleted?:bool, isCustomer?:bool, isTeam?:bool, isTechnician?:bool, isBanned?:bool, firstName?:str, lastName?:str, middleName?:str, position?:str, userTypeID?:int, erpID?:str, roleID?:int → map<ResultsUsersUserShortResult>
- `GET /Users/this/assetListQueries` — Получить список сохраненных запросов по объектам текущего пользователя · коды: 200, 204, 206 · примеры
  → map<ResultsUsersAssetListQueryResult>
- `DELETE /Users/this/avatar` — Удаляет аватку текущего пользователя. · коды: 202
- `PUT /Users/this/avatar/upload/fromBody` — Загружает изображение JPG не менее 128x128 используемое в качестве аватарки текущего пользователя. Данные будут получены из тела запроса (base64). · коды: 202
  ← body: DataAttachmentsFromBodyUploadData → ResultsUsersUserProfileResult
- `PUT /Users/this/avatar/upload/fromForm` — Загружает изображение JPG не менее 128x128 используемое в качестве аватарки для текущего пользователя. Данные будут получены из формы. · коды: 202
  ← body: { ContentLength?: int, ContentStream.CanRead?: bool, ContentStream.CanSeek?: bool, ContentStream.CanTimeout?: bool, ContentStream.CanWrite?: bool, ContentStream.Capacity?: int, ContentStream.Length?: int, ContentStream.Position?: int, ContentStream.ReadTimeout?: int, ContentStream.WriteTimeout?: int, ContentType?: str, Coordinate?: str, Description?: str, File: file, FileName?: str, IsIgnorePossibleDuplication?: bool, IsPublic?: bool, Md5Hash?: str, Roles?: int[], Uid?: uuid } → ResultsUsersUserProfileResult
- `GET /Users/this/companyListQueries` — Возвращает список запросов по компаниям, доступных текущему пользователю · коды: 200
  → map<ResultsUsersCompanyListQueryResult>
- `GET /Users/this/geolocation` — Получить настройку точности сбора геокоординат текущего пользователя · коды: 200, 206 · примеры
  → ResultsCoordinateAccuracyUserGeolocationSettings
- `GET /Users/this/notifications` — Получить список настроек уведомлений текущего пользователя · коды: 200, 204, 206 · примеры
  → ResultsUserDisabledNotificationsListResult
- `GET /Users/this/permissions/ext` — Получить список расширенных полномочий текущего пользователя · коды: 200, 204, 206 · примеры
  → map<str>
- `GET /Users/this/permissions/ui` — Получить список UI полномочий текущего пользователя · коды: 200, 204, 206 · примеры
  → map<str>
- `GET /Users/this/profile` — Получить профиль текущего пользователя · коды: 200 · примеры
  → ResultsUsersUserProfileResult
- `GET /Users/this/taskListQueries` — Получить список сохраненных запросов по заявкам текущего пользователя · коды: 200, 204, 206 · примеры
  → map<ResultsUsersTaskListQueryResult>
- `GET /Users/{UserID}/ratings` — Получить рейтинг инженера · коды: 200, 204, 206 · примеры
  ← path: userID:int → ResultsUsersRatingTechnicianResult
- `GET /Users/{id}` — Получить детальную информацию о пользователе · коды: 200, 400, 404 · примеры
  ← path: id:int → ResultsUsersDetailedInfoResult
- `PUT /Users/{id}` — Обновить данные пользователя · коды: 202, 400, 404 · примеры
  ← path: id:int; body: ADMUserUpdateData
- `GET /Users/{id}/assetListQueries` — Получить список сохраненных запросов по объектам пользователя · коды: 200, 204, 206 · примеры
  ← path: id:int → map<ResultsUsersAssetListQueryResult>
- `DELETE /Users/{id}/avatar` — Удаляет аватку указаного пользователя. · коды: 202
  ← path: id:int
- `PUT /Users/{id}/avatar/upload/fromBody` — Загружает изображение JPG не менее 256x256 используемое в качестве аватарки для указанного пользователя. Данные будут получены из тела запроса (base64). · коды: 202
  ← path: id:int; body: DataAttachmentsFromBodyUploadData → ResultsUsersUserProfileResult
- `PUT /Users/{id}/avatar/upload/fromForm` — Загружает изображение JPG не менее 256x256 используемое в качестве аватарки для указанного пользователя. Данные будут получены из формы. · коды: 202
  ← path: id:int; body: { ContentLength?: int, ContentStream.CanRead?: bool, ContentStream.CanSeek?: bool, ContentStream.CanTimeout?: bool, ContentStream.CanWrite?: bool, ContentStream.Capacity?: int, ContentStream.Length?: int, ContentStream.Position?: int, ContentStream.ReadTimeout?: int, ContentStream.WriteTimeout?: int, ContentType?: str, Coordinate?: str, Description?: str, File: file, FileName?: str, IsIgnorePossibleDuplication?: bool, IsPublic?: bool, Md5Hash?: str, Roles?: int[], Uid?: uuid } → ResultsUsersUserProfileResult
- `GET /Users/{id}/companyListQueries` — Возвращает список запросов по компаниям, доступных пользователю · коды: 200
  ← path: id:int → map<ResultsUsersCompanyListQueryResult>
- `GET /Users/{id}/districts` — Получить список участков пользователя · коды: 200, 204, 206 · примеры
  ← path: id:int → map<IdNameResultOfShort>
- `GET /Users/{id}/notifications` — Получить список настроек уведомлений пользователя · коды: 200, 204, 206 · примеры
  ← path: id:int → ResultsUserDisabledNotificationsListResult
- `GET /Users/{id}/profile` — Получить профиль пользователя · коды: 200, 404 · примеры
  ← path: id:int → ResultsUsersUserProfileResult
- `GET /Users/{id}/roles` — Получить список ролей пользователя · коды: 200, 204, 206 · примеры
  ← path: id:int → map<IdNameResultOfShort>
- `GET /Users/{id}/taskListQueries` — Получить список сохраненных запросов по заявкам пользователя · коды: 200, 204, 206 · примеры
  ← path: id:int → map<ResultsUsersTaskListQueryResult>
- `GET /Users/{id}/warehouses` — Получить список складов пользователя · коды: 200, 204, 206 · примеры
  ← path: id:int → map<IdNameErpIDResultOfShort>
- `DELETE /Users/{userID}` — Удалить пользователя · коды: 202, 409 · примеры
  ← path: userID:int
- `GET /Users/{userID}/assetAssignments` — Получить список объектов, назначенных пользователю · коды: 200, 204, 206 · примеры
  ← path: userID:int; query: assetID?:int, validOn?:datetime → ResultsUsersAssetAssignmentResult[]
- `GET /Users/{userID}/attributes` — Получить атрибуты пользователя · коды: 200, 204, 206 · примеры
  ← path: userID:int; query: attributeID?:int, IsRelevantForCustomer?:bool, IsRelevantForTechnician?:bool → ResultsUserAttributeUserAttributesResult[]
- `POST /Users/{userID}/attributes` — Создать атрибуты пользователя · коды: 201, 400 · примеры
  ← path: userID:int; body: ADMUserAttributeAttributeData[]
- `PUT /Users/{userID}/attributes` — Обновить атрибуты пользователя · коды: 202, 400 · примеры
  ← path: userID:int; body: ADMUserAttributeAttributeData[]
- `DELETE /Users/{userID}/attributes` — Удалить атрибуты пользователя · коды: 202, 400 · примеры
  ← path: userID:int; body: int[]
- `GET /Users/{userID}/defaultPages` — Получить текущие стартовые страницы пользователя · коды: 200, 204, 400 · примеры
  ← path: userID:int → ResultsUserDefaultPagesGetResult
- `POST /Users/{userID}/geolocation` — Добавить настройку точности сбора геокоординат для пользователя · коды: 201, 400 · примеры
  ← path: userID:int; query: coordinateAccuracyID?:int
- `PUT /Users/{userID}/geolocation` — Обновить настройку точности сбора геокоординат для пользователя · коды: 202, 400 · примеры
  ← path: userID:int; query: coordinateAccuracyID?:int
- `PUT /Users/{userID}/resendinvitation` — Повторно отправить приглашение пользователю · коды: 202, 204 · примеры
  ← path: userID:int
- `PUT /Users/{userID}/restore` — Восстановить пользователя из удаленных · коды: 202, 409 · примеры
  ← path: userID:int
- `GET /Users/{userID}/skills` — Получить список навыков пользователя · коды: 200, 204, 206, 500 · примеры
  ← path: userID:int → map<ResultsSkillsSkillResult>
- `GET /Users/{userID}/tags` — Получить список тегов пользователя · коды: 200, 204, 206 · примеры
  ← path: userID:int → str[]
