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
- Tenants — строки 128–145
- UserOrderBy — строки 147–149
- UserTemplates — строки 151–159
- Users — строки 161–221

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
- `GET /Invitations/{id}` — Получить расширенную информацию о приглашении · коды: 200 · примеры
  ← path: id:uuid; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → ResultsInvitationsGetResult
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
- `GET /PermissionsUi/{id}` — Получить данные UI полномочия · коды: 200, 204, 206 · примеры
  ← path: id:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → ResultsPermissionsUiGetResult

## RoleTaskPropertiesAccess
- `GET /RoleTaskPropertiesAccess/attributes` · paginated · коды: 200, 204, 206
  ← query: roleID?:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → ResultsRoleTaskAttributeRoleTaskAttributeSettings[]

## Roles
- `GET /Roles` — Получить список ролей тенанта · коды: 200, 204, 206 · примеры
  ← query: isDeleted?:bool; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → map<ResultsRolesGetResult>
- `GET /Roles/{id}` — Получить информацию о роли · коды: 200, 204 · примеры
  ← path: id:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → ResultsRolesGetResult
- `GET /Roles/{roleID}/applications` — Получить список приложений роли · коды: 200, 204, 206 · примеры
  ← path: roleID:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → map<ResultsRoleApplicationListResult>
- `GET /Roles/{roleID}/attachments` — Получить список вложенных файлов роли · коды: 200, 204, 206 · примеры
  ← path: roleID:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → ResultsCommonAttachmentResult[]
- `GET /Roles/{roleID}/packages` — Получить список расширений роли · коды: 200, 204, 206 · примеры
  ← path: roleID:int; query: searchText?:str; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → map<ResultsRolePackagesListResult[]>
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
- `GET /TenantCreationRequests/{id}` — Получить запрос на создание тенанта · коды: 200 · примеры
  ← path: id:str; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → ResultsTenantCreationRequestsGetResult

## TenantMembers
- `GET /TenantMembers` · paginated · коды: 200, 204, 206
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → map<ResultsTenantMembersListResult>
- `GET /TenantMembers/anonymousUser` — Получить анонимного пользователя в текущем тенанте · коды: 200, 204 · примеры
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → ResultsTenantMembersListResult
- `GET /TenantMembers/apiUser` — Получить пользователя API в текущем тенанте · коды: 200, 204 · примеры
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → ResultsTenantMembersListResult
- `GET /TenantMembers/this` — Получить данные текущего члена тенанта · коды: 200 · примеры
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → ResultsTenantMembersGetResult
- `GET /TenantMembers/{tenantMemberID}` — Получить данные члена тенанта · коды: 200, 500 · примеры
  ← path: tenantMemberID:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → ResultsTenantMembersGetResult

## TenantSettings
- `GET /TenantSettings` — Получить настройки тенанта · коды: 200, 204, 500 · примеры
  ← query: tenantMemberId?:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → ResultsTenantSettingsGetResult
- `GET /TenantSettings/plateUrl` — Получить кастомный URL текущего тенанта · коды: 200, 204 · примеры
  ← query: taskTemplateID?:str; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → str

## Tenants
- `GET /Tenants` — Получить список тенантов · коды: 200, 204, 206 · примеры
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → ResultsTenantsListResult[]
- `GET /Tenants/templates` — Получить список шаблонных тенантов · коды: 200, 204, 206 · примеры
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → InterfacesEntitiesITenantEntity[]
- `GET /Tenants/this` — Получить данные текущего тенанта · коды: 200 · примеры
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → ResultsTenantsGetResult
- `GET /Tenants/this/featureFlags` — Получить список флагов функций тенанта · коды: 200, 204 · примеры
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → str[]
- `GET /Tenants/this/licenses` — Получить список лицензий тенанта · коды: 200, 204 · примеры
  ← query: validOn?:datetime; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → ResultsTenantLicenseListTenantLicenseResult
- `GET /Tenants/this/meta` — Получить метаданные тенанта · коды: 200, 204 · примеры
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb)
- `GET /Tenants/this/packages` · paginated · коды: 200, 204, 206
  ← query: resourceID?:int[]; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → ResultsTenantPackagesListResult[]
  Для выполнения данного метода пользователь должен быть **TenantMember**.
- `GET /Tenants/this/variables` — Получить список переменных окружения тенанта · коды: 200, 204, 206 · примеры
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → map<ResultsTenantVariablesListResult>

## UserOrderBy
- `GET /UserOrderBy` — Получить список методов сортировки сотрудников · коды: 200, 204, 206 · примеры
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → map<ResultsUserOrderByListResult>

## UserTemplates
- `GET /UserTemplates` · paginated · коды: 200, 204, 206
  ← query: searchText?:str, isTechnician?:bool, roleID?:int, districtID?:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → map<ResultsUserTemplatesListResult>
- `GET /UserTemplates/{id}` — Получить шаблон пользователя · коды: 200, 204 · примеры
  ← path: id:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → ResultsUserTemplatesGetResult
- `GET /UserTemplates/{id}/districts` — Получить список участков шаблона пользователя · коды: 200, 204, 206 · примеры
  ← path: id:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → IdNameResultOfShort[]
- `GET /UserTemplates/{id}/roles` — Получить список ролей шаблона пользователя · коды: 200, 204, 206 · примеры
  ← path: id:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → IdNameResultOfShort[]

## Users
- `GET /Users` — Возвращает список пользователей · paginated · коды: 200, 206
  ← query: searchText?:str, includeTaskActuality?:bool, includeDistricts?:bool, needForAllowedTasks?:bool, orgUnitID?:int, districtID?:int, userID?:int, workTypeID?:int, skillID?:int, tag?:str, isDeleted?:bool, isCustomer?:bool, isTeam?:bool, isTechnician?:bool, isBanned?:bool, isOnShift?:bool, firstName?:str, lastName?:str, middleName?:str, position?:str, userTypeID?:int, companyID?:int, orderBy?:int, sortDirection?:int, erpID?:str, roleID?:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → map<ResultsUsersUserResult>
- `HEAD /Users` — Возвращает заголовок запроса пользователей с количеством данных, удовлетворяющих фильтру · коды: 200
  ← query: orgUnitID?:int, districtID?:int, userID?:int, workTypeID?:int, skillID?:int, tag?:str, isDeleted?:bool, isCustomer?:bool, isTeam?:bool, isTechnician?:bool, firstName?:str, lastName?:str, middleName?:str, position?:str, userTypeID?:int, erpID?:str; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb)
- `GET /Users/attributes` — Получить список атрибутов пользователей · коды: 200, 204, 206 · примеры
  ← query: attributeID?:int, userID?:int, IsRelevantForCustomer?:bool, IsRelevantForTechnician?:bool; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → ResultsUserAttributeUserAttributesResult[]
- `GET /Users/geolocation` — Получить список настроек точности сбора геокоординат для пользователей · коды: 200, 204, 206 · примеры
  ← query: userID?:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → ResultsCoordinateAccuracyUserGeolocationSettings[]
- `GET /Users/profile` — Получить профиль пользователя · коды: 200, 404 · примеры
  ← query: tenantMemberId?:int, userId?:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → ResultsUsersUserProfileResult
- `GET /Users/relevance` — Возвращает список пользователей по их релевантности к заявке · paginated · коды: 200, 206
  ← query: searchText?:str, includeTaskActuality?:bool, includeDistricts?:bool, assetID?:int, districtID?:int, workTypeID?:int, skillID?:int, levelOnShift?:bool, dateOnShift?:datetime, userTypeID?:int, isDeleted?:bool, isCustomer?:bool, isTechnician?:bool, isBanned?:bool; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → map<ResultsUsersUserResult>
- `GET /Users/short` — Возвращает список пользователей с усеченным набором полей (для справочников и ниспадающих списков) · paginated · коды: 200, 206
  ← query: searchText?:str, orgUnitID?:int, districtID?:int, userID?:int, workTypeID?:int, skillID?:int, tag?:str, isDeleted?:bool, isCustomer?:bool, isTeam?:bool, isTechnician?:bool, isBanned?:bool, firstName?:str, lastName?:str, middleName?:str, position?:str, userTypeID?:int, erpID?:str, roleID?:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → map<ResultsUsersUserShortResult>
- `GET /Users/this/assetListQueries` — Получить список сохраненных запросов по объектам текущего пользователя · коды: 200, 204, 206 · примеры
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → map<ResultsUsersAssetListQueryResult>
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
- `GET /Users/{id}/assetListQueries` — Получить список сохраненных запросов по объектам пользователя · коды: 200, 204, 206 · примеры
  ← path: id:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → map<ResultsUsersAssetListQueryResult>
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
- `GET /Users/{userID}/assetAssignments` — Получить список объектов, назначенных пользователю · коды: 200, 204, 206 · примеры
  ← path: userID:int; query: assetID?:int, validOn?:datetime; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → ResultsUsersAssetAssignmentResult[]
- `GET /Users/{userID}/attributes` — Получить атрибуты пользователя · коды: 200, 204, 206 · примеры
  ← path: userID:int; query: attributeID?:int, IsRelevantForCustomer?:bool, IsRelevantForTechnician?:bool; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → ResultsUserAttributeUserAttributesResult[]
- `GET /Users/{userID}/defaultPages` — Получить текущие стартовые страницы пользователя · коды: 200, 204, 400 · примеры
  ← path: userID:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → ResultsUserDefaultPagesGetResult
- `GET /Users/{userID}/skills` — Получить список навыков пользователя · коды: 200, 204, 206, 500 · примеры
  ← path: userID:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → map<ResultsSkillsSkillResult>
- `GET /Users/{userID}/tags` — Получить список тегов пользователя · коды: 200, 204, 206 · примеры
  ← path: userID:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → str[]
