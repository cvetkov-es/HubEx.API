# ADM — справочник ручек

> **Что здесь:** только read-ручки (GET/HEAD) сервиса ADM (HubEx ADM APIs): сигнатуры, параметры, права. Типы — schemas/ADM.md. Сгенерировано из swagger.
> **Когда сюда идти:** найти ручку и её вход/выход. Типы — `schemas/ADM.md`; грабли — `notes/ADM.md` (если есть).
> **Источник:** swagger сервиса ADM · файл генерируется пайплайном — руками не править.
> **Линза read-only:** здесь только GET/HEAD. Write-ручки (POST/PUT/PATCH/DELETE) и их типы в API **существуют**, но в эту линзу не входят — не делай из их отсутствия здесь вывода, что их нет в API.

Base: `{BASE_URL}/ADM`
> Примеры ответов вынесены в [../examples/ADM.md](../examples/ADM.md).

**Оглавление**

- BanReasons — строки 34–36
- Capabilities — строки 38–40
- DefaultPages — строки 42–44
- GeolocationSettings — строки 46–48
- Invitations — строки 50–56
- PermissionApiTags — строки 58–60
- PermissionExtTags — строки 62–64
- PermissionsApi — строки 66–68
- PermissionsExt — строки 70–72
- PermissionsUi — строки 74–78
- RoleTaskPropertiesAccess — строки 80–82
- Roles — строки 84–100
- SystemPermissionUiTags — строки 102–104
- TenantCreationRequests — строки 106–108
- TenantMembers — строки 110–120
- TenantSettings — строки 122–126
- Tenants — строки 128–144
- UserOrderBy — строки 146–148
- UserTemplates — строки 150–158
- Users — строки 160–220

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
- `GET /Invitations/{id}` — Получить расширенную информацию о приглашении · коды: 200 · примеры
  ← path: id:uuid → ResultsInvitationsGetResult
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
- `GET /PermissionsUi/{id}` — Получить данные UI полномочия · коды: 200, 204, 206 · примеры
  ← path: id:int → ResultsPermissionsUiGetResult

## RoleTaskPropertiesAccess
- `GET /RoleTaskPropertiesAccess/attributes` · paginated · коды: 200, 204, 206
  ← query: roleID?:int → ResultsRoleTaskAttributeRoleTaskAttributeSettings[]

## Roles
- `GET /Roles` — Получить список ролей тенанта · коды: 200, 204, 206 · примеры
  ← query: isDeleted?:bool → map<ResultsRolesGetResult>
- `GET /Roles/{id}` — Получить информацию о роли · коды: 200, 204 · примеры
  ← path: id:int → ResultsRolesGetResult
- `GET /Roles/{roleID}/applications` — Получить список приложений роли · коды: 200, 204, 206 · примеры
  ← path: roleID:int → map<ResultsRoleApplicationListResult>
- `GET /Roles/{roleID}/attachments` — Получить список вложенных файлов роли · коды: 200, 204, 206 · примеры
  ← path: roleID:int → ResultsCommonAttachmentResult[]
- `GET /Roles/{roleID}/packages` — Получить список расширений роли · коды: 200, 204, 206 · примеры
  ← path: roleID:int; query: searchText?:str → map<ResultsRolePackagesListResult[]>
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
- `GET /TenantCreationRequests/{id}` — Получить запрос на создание тенанта · коды: 200 · примеры
  ← path: id:str → ResultsTenantCreationRequestsGetResult

## TenantMembers
- `GET /TenantMembers` · paginated · коды: 200, 204, 206
  → map<ResultsTenantMembersListResult>
- `GET /TenantMembers/anonymousUser` — Получить анонимного пользователя в текущем тенанте · коды: 200, 204 · примеры
  → ResultsTenantMembersListResult
- `GET /TenantMembers/apiUser` — Получить пользователя API в текущем тенанте · коды: 200, 204 · примеры
  → ResultsTenantMembersListResult
- `GET /TenantMembers/this` — Получить данные текущего члена тенанта · коды: 200 · примеры
  → ResultsTenantMembersGetResult
- `GET /TenantMembers/{tenantMemberID}` — Получить данные члена тенанта · коды: 200, 500 · примеры
  ← path: tenantMemberID:int → ResultsTenantMembersGetResult

## TenantSettings
- `GET /TenantSettings` — Получить настройки тенанта · коды: 200, 204, 500 · примеры
  ← query: tenantMemberId?:int → ResultsTenantSettingsGetResult
- `GET /TenantSettings/plateUrl` — Получить кастомный URL текущего тенанта · коды: 200, 204 · примеры
  ← query: taskTemplateID?:str → str

## Tenants
- `GET /Tenants` — Получить список тенантов · коды: 200, 204, 206 · примеры
  → ResultsTenantsListResult[]
- `GET /Tenants/templates` — Получить список шаблонных тенантов · коды: 200, 204, 206 · примеры
  → InterfacesEntitiesITenantEntity[]
- `GET /Tenants/this` — Получить данные текущего тенанта · коды: 200 · примеры
  → ResultsTenantsGetResult
- `GET /Tenants/this/featureFlags` — Получить список флагов функций тенанта · коды: 200, 204 · примеры
  → str[]
- `GET /Tenants/this/licenses` — Получить список лицензий тенанта · коды: 200, 204 · примеры
  ← query: validOn?:datetime → ResultsTenantLicenseListTenantLicenseResult
- `GET /Tenants/this/meta` — Получить метаданные тенанта · коды: 200, 204 · примеры
- `GET /Tenants/this/packages` · paginated · коды: 200, 204, 206
  ← query: resourceID?:int[] → ResultsTenantPackagesListResult[]
  Для выполнения данного метода пользователь должен быть **TenantMember**.
- `GET /Tenants/this/variables` — Получить список переменных окружения тенанта · коды: 200, 204, 206 · примеры
  → map<ResultsTenantVariablesListResult>

## UserOrderBy
- `GET /UserOrderBy` — Получить список методов сортировки сотрудников · коды: 200, 204, 206 · примеры
  → map<ResultsUserOrderByListResult>

## UserTemplates
- `GET /UserTemplates` · paginated · коды: 200, 204, 206
  ← query: searchText?:str, isTechnician?:bool, roleID?:int, districtID?:int → map<ResultsUserTemplatesListResult>
- `GET /UserTemplates/{id}` — Получить шаблон пользователя · коды: 200, 204 · примеры
  ← path: id:int → ResultsUserTemplatesGetResult
- `GET /UserTemplates/{id}/districts` — Получить список участков шаблона пользователя · коды: 200, 204, 206 · примеры
  ← path: id:int → IdNameResultOfShort[]
- `GET /UserTemplates/{id}/roles` — Получить список ролей шаблона пользователя · коды: 200, 204, 206 · примеры
  ← path: id:int → IdNameResultOfShort[]

## Users
- `GET /Users` — Возвращает список пользователей · paginated · коды: 200, 206
  ← query: searchText?:str, includeTaskActuality?:bool, includeDistricts?:bool, needForAllowedTasks?:bool, orgUnitID?:int, districtID?:int, userID?:int, workTypeID?:int, skillID?:int, tag?:str, isDeleted?:bool, isCustomer?:bool, isTeam?:bool, isTechnician?:bool, isBanned?:bool, isOnShift?:bool, firstName?:str, lastName?:str, middleName?:str, position?:str, userTypeID?:int, companyID?:int, orderBy?:int, sortDirection?:int, erpID?:str, roleID?:int → map<ResultsUsersUserResult>
- `HEAD /Users` — Возвращает заголовок запроса пользователей с количеством данных, удовлетворяющих фильтру · коды: 200
  ← query: orgUnitID?:int, districtID?:int, userID?:int, workTypeID?:int, skillID?:int, tag?:str, isDeleted?:bool, isCustomer?:bool, isTeam?:bool, isTechnician?:bool, firstName?:str, lastName?:str, middleName?:str, position?:str, userTypeID?:int, erpID?:str
- `GET /Users/attributes` — Получить список атрибутов пользователей · коды: 200, 204, 206 · примеры
  ← query: attributeID?:int, userID?:int, IsRelevantForCustomer?:bool, IsRelevantForTechnician?:bool → ResultsUserAttributeUserAttributesResult[]
- `GET /Users/geolocation` — Получить список настроек точности сбора геокоординат для пользователей · коды: 200, 204, 206 · примеры
  ← query: userID?:int → ResultsCoordinateAccuracyUserGeolocationSettings[]
- `GET /Users/profile` — Получить профиль пользователя · коды: 200, 404 · примеры
  ← query: tenantMemberId?:int, userId?:int → ResultsUsersUserProfileResult
- `GET /Users/relevance` — Возвращает список пользователей по их релевантности к заявке · paginated · коды: 200, 206
  ← query: searchText?:str, includeTaskActuality?:bool, includeDistricts?:bool, assetID?:int, districtID?:int, workTypeID?:int, skillID?:int, levelOnShift?:bool, dateOnShift?:datetime, userTypeID?:int, isDeleted?:bool, isCustomer?:bool, isTechnician?:bool, isBanned?:bool → map<ResultsUsersUserResult>
- `GET /Users/short` — Возвращает список пользователей с усеченным набором полей (для справочников и ниспадающих списков) · paginated · коды: 200, 206
  ← query: searchText?:str, orgUnitID?:int, districtID?:int, userID?:int, workTypeID?:int, skillID?:int, tag?:str, isDeleted?:bool, isCustomer?:bool, isTeam?:bool, isTechnician?:bool, isBanned?:bool, firstName?:str, lastName?:str, middleName?:str, position?:str, userTypeID?:int, erpID?:str, roleID?:int → map<ResultsUsersUserShortResult>
- `GET /Users/this/assetListQueries` — Получить список сохраненных запросов по объектам текущего пользователя · коды: 200, 204, 206 · примеры
  → map<ResultsUsersAssetListQueryResult>
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
- `GET /Users/{id}/assetListQueries` — Получить список сохраненных запросов по объектам пользователя · коды: 200, 204, 206 · примеры
  ← path: id:int → map<ResultsUsersAssetListQueryResult>
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
- `GET /Users/{userID}/assetAssignments` — Получить список объектов, назначенных пользователю · коды: 200, 204, 206 · примеры
  ← path: userID:int; query: assetID?:int, validOn?:datetime → ResultsUsersAssetAssignmentResult[]
- `GET /Users/{userID}/attributes` — Получить атрибуты пользователя · коды: 200, 204, 206 · примеры
  ← path: userID:int; query: attributeID?:int, IsRelevantForCustomer?:bool, IsRelevantForTechnician?:bool → ResultsUserAttributeUserAttributesResult[]
- `GET /Users/{userID}/defaultPages` — Получить текущие стартовые страницы пользователя · коды: 200, 204, 400 · примеры
  ← path: userID:int → ResultsUserDefaultPagesGetResult
- `GET /Users/{userID}/skills` — Получить список навыков пользователя · коды: 200, 204, 206, 500 · примеры
  ← path: userID:int → map<ResultsSkillsSkillResult>
- `GET /Users/{userID}/tags` — Получить список тегов пользователя · коды: 200, 204, 206 · примеры
  ← path: userID:int → str[]
