# ES — справочник ручек

> **Что здесь:** только read-ручки (GET/HEAD) сервиса ES (API for managing enterprise structure in HubEx): сигнатуры, параметры, права. Типы — schemas/ES.md.
> **Когда сюда идти:** найти ручку и её вход/выход. Типы — `schemas/ES.md`; грабли — `notes/ES.md` (если есть).
> **Линза read-only:** здесь только GET/HEAD. Write-ручки (POST/PUT/PATCH/DELETE) и их типы в API **существуют**, но в эту линзу не входят — не делай из их отсутствия здесь вывода, что их нет в API.

Base: `{BASE_URL}/ES`
> Примеры ответов вынесены в [../examples/ES.md](../examples/ES.md).

**Оглавление**

- AssetClasses — строки 33–37
- AssetFilter — строки 39–41
- AssetListQueries — строки 43–47
- AssetLocations — строки 49–51
- AssetSchemas — строки 53–67
- AssetSearchSettings — строки 69–71
- AssetTemplates — строки 73–89
- AssetTypes — строки 91–97
- Assets — строки 99–110
- Негативные сценарии: — строки 112–146
- Негативные сценарии: — строки 148–156
- Негативные сценарии: — строки 158–161
- Companies — строки 163–187
- CompanyListQueries — строки 189–193
- CompanyLocations — строки 195–197
- CompanyRegistrationTypes — строки 199–201
- Districts — строки 203–207
- Locations — строки 209–215
- OrgUnits — строки 217–223
- PreferredTechnicians — строки 225–227

## AssetClasses
- `GET /AssetClasses` — Возвращает список классов объектов · коды: 200, 204, 206 · примеры
  → map<ResultsAssetClassesAssetClassListResult>
- `GET /AssetClasses/{id}` — Возвращает класс объекта · коды: 200, 204 · примеры
  ← path: id:int → ResultsAssetClassesAssetClassGetResult

## AssetFilter
- `GET /AssetFilter` — Возвращает список доступных фильтров для пользователя, запросившего данные · коды: 200, 204 · примеры
  ← query: selectedOnly?:bool → ProjectionsCOMMONFilterListItemProjection[]

## AssetListQueries
- `GET /AssetListQueries` — Возвращает список сохранённых запросов, доступных в тенанте · коды: 200, 204, 206 · примеры
  → map<ResultsAssetListQueriesAssetListQueryResult>
- `GET /AssetListQueries/{id}` — Возвращает сохранённый запрос · коды: 200, 204 · примеры
  ← path: id:int → ResultsAssetListQueriesAssetListQueryGetResult

## AssetLocations
- `GET /AssetLocations` — Возвращает список локаций объекта · коды: 200, 204, 206, 409 · примеры
  ← query: assetID?:int, onDate?:datetime → map<ResultsAssetsAssetLocationResult>

## AssetSchemas
- `GET /AssetSchemas/ascList/{assetID}` — Возвращает список существующих план-схем для текущего объекта и всех доступных объектов вверх по дереву · коды: 200, 204 · примеры
  ← path: assetID:int → map<ResultsAssetSchemaSchemaBase>
- `GET /AssetSchemas/asset/{assetID}` — Возвращает план-схему, привязанную к объекту, или ближайшую по дереву сверху · коды: 200, 204 · примеры
  ← path: assetID:int → ResultsAssetSchemaSchema
- `GET /AssetSchemas/list` — Возвращает полный список схем тенанта · коды: 200, 204 · примеры
  → map<ResultsAssetSchemaSchemaBase>
- `GET /AssetSchemas/{schemaId}` — Возвращает план-схему по её уникальному идентификатору · коды: 200, 404 · примеры
  ← path: schemaId:int → ResultsAssetSchemaSchema
- `GET /AssetSchemas/{schemaId}/image` — Получает информацию об изображении, привязанном к план-схеме · коды: 200, 400, 404 · примеры
  ← path: schemaId:int; query: thumbnailSize?:int → ResultsAssetSchemaSchemaImage
- `GET /AssetSchemas/{schemaId}/image/download` — Возвращает временный redirect на ссылку для скачивания изображения план-схемы · коды: 303, 400, 404 · примеры
  ← path: schemaId:int; query: thumbnailSize?:int, noRedirect?:bool
- `GET /AssetSchemas/{schemaId}/points` — Возвращает полный список точек-заданий, размещённых на план-схеме · коды: 200, 204 · примеры
  ← path: schemaId:int; query: taskID?:int, assetID?:int → ResultsAssetSchemaSchemaTask[]

## AssetSearchSettings
- `GET /AssetSearchSettings` — Получение списка полей поиска объекта для текущего пользователя · коды: 200, 204 · примеры
  → ProjectionsESAssetSearchFieldSettingsProjection[]

## AssetTemplates
- `GET /AssetTemplates` — Возвращает список шаблонов объектов · коды: 200, 204, 206 · примеры
  ← query: searchText?:str, assetClassID?:int, assetTypeID?:int → map<ResultsAssetTemplatesListResult>
- `GET /AssetTemplates/{assetTemplateID}/attachments` — Возвращает список файлов, вложенных в шаблон объекта · коды: 200, 204, 206, 400 · примеры
  ← path: assetTemplateID:int; query: thumbnailSize?:int → map<ResultsCommonListAttachmentResult>
- `GET /AssetTemplates/{assetTemplateID}/attachments/{attachmentID}` — Возвращает TemporaryRedirect на временную ссылку для скачивания файла · коды: 307, 400, 404 · примеры
  ← path: assetTemplateID:int, attachmentID:int; query: thumbnailSize?:int, noRedirect?:bool
- `GET /AssetTemplates/{assetTemplateID}/attributes` — Возвращает список пользовательских полей шаблона объекта · коды: 200, 204, 206, 400 · примеры
  ← path: assetTemplateID:int → ResultsAssetTemplatesAssetTemplateAttributeResult[]
- `GET /AssetTemplates/{assetTemplateID}/districts` — Возвращает список участков шаблона объекта · коды: 200, 204, 206, 400 · примеры
  ← path: assetTemplateID:int → map<ResultsCommonAssetDistrictResult>
- `GET /AssetTemplates/{assetTemplateID}/skills` — Возвращает список навыков шаблона объекта · коды: 200, 204, 206, 400 · примеры
  ← path: assetTemplateID:int → ResultsAssetTemplatesAssetTemplateSkillResult[]
- `GET /AssetTemplates/{assetTemplateID}/workTypes` — Возвращает список видов работ шаблона объекта · коды: 200, 204, 206, 400 · примеры
  ← path: assetTemplateID:int → ResultsAssetTemplatesAssetTemplateWorkTypeResult[]
- `GET /AssetTemplates/{id}` — Возвращает шаблон объекта · коды: 200, 204 · примеры
  ← path: id:int → ResultsAssetTemplatesGetResult

## AssetTypes
- `GET /AssetTypes` — Возвращает список типов объектов · коды: 200, 204, 206 · примеры
  → map<ResultsAssetTypesGetResult>
- `GET /AssetTypes/{id}` — Возвращает тип объекта · коды: 200, 204, 400, 404, 409 · примеры
  ← path: id:int → ResultsAssetTypesGetResult
- `GET /AssetTypes/{id}/workTypes` — Возвращает список видов работ, привязанных к типу объекта · коды: 200, 204, 206 · примеры
  ← path: id:int; query: isPublished?:bool → map<str>

## Assets
- `GET /Assets` — Возвращает справочник объектов, доступных пользователю · коды: 200, 204, 206, 400 · примеры
  ← query: includePath?:bool, includeTaskActuality?:bool, searchText?:str, needForAllowedTasks?:bool, parentID?:int, assetID?:int, responsiblePerson?:int, districtID?:int, workTypeID?:int, skillID?:int, companyID?:int, taskTypeID?:int, tag?:str, name?:str, isMobile?:bool, isAssigned?:bool, hasSchema?:bool, isDeleted?:bool, isPublished?:bool, warrantyFrom?:datetime, warrantyTill?:datetime, checkListID?:int, startWithAssetID?:int, assetTypeID?:int, assetClassID?:int, erpID?:str, contactID?:int, attributeValues?:str, contractID?:int → map<ResultsAssetsAssetExtResult>
- `HEAD /Assets` — Возвращает заголовок запроса с количеством объектов, удовлетворяющих фильтру · коды: 200, 206 · примеры
  ← query: checkListID?:int, parentID?:int, assetID?:int, responsiblePerson?:int, districtID?:int, workTypeID?:int, skillID?:int, companyID?:int, taskTypeID?:int, tag?:str, name?:str, isMobile?:bool, isAssigned?:bool, hasSchema?:bool, isDeleted?:bool, isPublished?:bool, warrantyFrom?:datetime, warrantyTill?:datetime, startWithAssetID?:int, assetTypeID?:int, assetClassID?:int, erpID?:str, contactID?:int, attributeValues?:str, contractID?:int
- `GET /Assets/attributes` — Возвращает список атрибутов по объектам · коды: 200, 204, 206 · примеры
  ← query: assetID?:int, attributeID?:int → ResultsAssetsAssetAttributesExtResult[]
- `GET /Assets/root` — Возращает справочник корневых объектов, доступных пользователю. · коды: 200, 204, 206
  ← query: checkListID?:int, assetID?:int, responsiblePerson?:int, districtID?:int, workTypeID?:int, skillID?:int, companyID?:int, taskTypeID?:int, tag?:str, name?:str, isMobile?:bool, isAssigned?:bool, hasSchema?:bool, isDeleted?:bool, isPublished?:bool, warrantyFrom?:datetime, warrantyTill?:datetime, assetTypeID?:int, assetClassID?:int, erpID?:str, contactID?:int → map<ResultsAssetsAssetExtResult>
  Доступность объекта определяется по пересечанию участков пользователя и объека, наличию полномочия
AllDistricts или AllAssets. Корневой объект - объект не имеющий объекта более высого уровня среди 
доступных пользователю.
            
## Негативные сценарии:
- 204 NoContent: объекты не найдены.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `AssetsList`.
- `GET /Assets/{assetID}` — Детальная информация по объекту · коды: 200, 204 · примеры
  ← path: assetID:int → ResultsAssetsAssetDetailedInfoResult
- `GET /Assets/{assetID}/assignments` — Возвращает список назначений объекта для пользователей · коды: 200, 204, 206, 404 · примеры
  ← path: assetID:int; query: userID?:int, validOn?:datetime → ResultsAssetsAssetAssignmentResult[]
- `GET /Assets/{assetID}/attachments` — Возвращает список файлов, вложенных в объект · коды: 200, 204, 206, 400 · примеры
  ← path: assetID:int; query: thumbnailSize?:int → map<ResultsCommonListAttachmentResult>
- `GET /Assets/{assetID}/attachments/{attachmentID}` — Возвращает TemporaryRedirect на временную ссылку для скачивания файла · коды: 307, 400, 404 · примеры
  ← path: assetID:int, attachmentID:int; query: thumbnailSize?:int, noRedirect?:bool
- `GET /Assets/{assetID}/attributes` — Возвращает список пользовательских полей объекта · коды: 200, 204, 206, 400 · примеры
  ← path: assetID:int → ResultsAssetsAssetAttributeResult[]
- `GET /Assets/{assetID}/checkLists` — Возвращает список чек-листов объекта · коды: 200, 204, 206 · примеры
  ← path: assetID:int → map<ResultsAssetCheckListsGetResult[]>
- `GET /Assets/{assetID}/contacts` — Возвращает список действующих контактов объекта · коды: 200, 204, 206, 400 · примеры
  ← path: assetID:int; query: searchText?:str → map<ResultsAssetContactsListResult>
- `GET /Assets/{assetID}/contacts/{contactID}` — Возвращает контакт объекта · коды: 200, 204 · примеры
  ← path: assetID:int, contactID:int → ResultsAssetContactsGetResult
- `GET /Assets/{assetID}/districts` — Возвращает список участков объекта · коды: 200, 204, 206, 400 · примеры
  ← path: assetID:int → map<ResultsCommonAssetDistrictResult>
- `GET /Assets/{assetID}/locations/actual` — Возвращает текущее местоположение объекта · коды: 200, 204, 206 · примеры
  ← path: assetID:int → ResultsCommonLocationResult
- `GET /Assets/{assetID}/skills` — Возвращает список навыков объекта · коды: 200, 204, 206 · примеры
  ← path: assetID:int → map<ResultsAssetSkillsAssetSkillResult>
- `GET /Assets/{assetID}/tags` — Возвращает список активных тегов объекта · коды: 200, 204, 206, 400 · примеры
  ← path: assetID:int → str[]
- `GET /Assets/{assetID}/workTypes` — Возвращает список доступных по объекту видов работ · коды: 200, 204, 206 · примеры
  ← path: assetID:int → map<ResultsAssetsAssetWorkTypeResult>
- `GET /Assets/{parentAssetID}/assets` — Возращает справочник дочерних объектов (один уровень иерархии), 
доступных пользователю. · коды: 200, 204, 206
  ← path: parentAssetID:int; query: searchText?:str, checkListID?:int, assetID?:int, responsiblePerson?:int, districtID?:int, workTypeID?:int, skillID?:int, companyID?:int, taskTypeID?:int, tag?:str, name?:str, isMobile?:bool, isAssigned?:bool, hasSchema?:bool, isDeleted?:bool, isPublished?:bool, warrantyFrom?:datetime, warrantyTill?:datetime, assetTypeID?:int, assetClassID?:int, erpID?:str, contactID?:int → map<ResultsAssetsAssetExtResult>
  Доступность объекта определяется по пересечанию участков пользователя и объека, наличию полномочия
AllDistricts или AllAssets.
            
## Негативные сценарии:
- 204 NoContent: объекты не найдены.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `AssetsList`.
- `GET /Assets/{parentAssetID}/assets/all` — Возращает справочник всех дочерних объектов (вниз по иерархии до самого нижнего уровня), 
доступных пользователю. · коды: 200, 204, 206
  ← path: parentAssetID:int; query: checkListID?:int, assetID?:int, responsiblePerson?:int, districtID?:int, workTypeID?:int, skillID?:int, companyID?:int, taskTypeID?:int, tag?:str, name?:str, isMobile?:bool, isAssigned?:bool, hasSchema?:bool, isDeleted?:bool, isPublished?:bool, warrantyFrom?:datetime, warrantyTill?:datetime, assetTypeID?:int, assetClassID?:int, erpID?:str, contactID?:int → map<ResultsAssetsAssetExtResult>
  Доступность объекта определяется по пересечанию участков пользователя и объека, наличию полномочия
AllDistricts или AllAssets.
            
## Негативные сценарии:
- 204 NoContent: объекты не найдены.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `AssetsList`.

## Companies
- `GET /Companies` — Возвращает список доступных пользователю компаний · коды: 200, 204, 206 · примеры
  ← query: searchText?:str, isDeleted?:bool, taskTypeID?:int, companyID?:int, companyRegistrationTypeID?:int, isEmployer?:bool, isContractorHolder?:bool, isOurCompany?:bool, isVATTaxpayer?:bool → map<ResultsCompaniesListResult>
- `HEAD /Companies` — Возвращает заголовок запроса доступных пользователю компаний с количеством данных, удовлетворяющих фильтру · коды: 200, 206 · примеры
  ← query: searchText?:str, isDeleted?:bool, taskTypeID?:int, companyID?:int, companyRegistrationTypeID?:int, isEmployer?:bool, isContractorHolder?:bool, isOurCompany?:bool, isVATTaxpayer?:bool
- `GET /Companies/dadata/find` — Поиск информации о компании по ИНН через DaData · коды: 200, 204 · примеры
  ← query: inn?:str → ESCompanyAddData
- `GET /Companies/{companyID}/attachment/{attachmentID}` — Возвращает прикреплённый файл компании · коды: 200, 204, 400, 500 · примеры
  ← path: companyID:int, attachmentID:int; query: thumbnailSize?:int → ResultsCommonGetAttachmentResult
- `GET /Companies/{companyID}/attachments` — Возвращает список файлов, вложенных в компанию · коды: 200, 204, 206, 400 · примеры
  ← path: companyID:int; query: thumbnailSize?:int → map<ResultsCommonListAttachmentResult>
- `GET /Companies/{companyID}/attachments/{attachmentID}` — Возвращает TemporaryRedirect на временную ссылку для скачивания файла · коды: 307, 400, 404 · примеры
  ← path: companyID:int, attachmentID:int; query: thumbnailSize?:int, noRedirect?:bool
- `GET /Companies/{companyID}/attributes` — Возвращает список пользовательских атрибутов компании · коды: 200, 204, 206, 400 · примеры
  ← path: companyID:int → ResultsCompanyAttributesCompanyAttributeResult[]
- `GET /Companies/{companyID}/bankAccounts` — Возвращает список банковских счетов компании · коды: 200, 204, 206, 400 · примеры
  ← path: companyID:int; query: searchText?:str → map<ResultsCompanyBankAccountsListResult>
- `GET /Companies/{companyID}/contacts` — Возвращает список контактов компании · коды: 200, 204, 206, 400 · примеры
  ← path: companyID:int; query: searchText?:str → map<ResultsCompanyContactsListResult>
- `GET /Companies/{companyID}/contacts/{contactID}` — Возвращает контакт компании · коды: 200, 204 · примеры
  ← path: companyID:int, contactID:int → ResultsCompanyContactsGetResult
- `GET /Companies/{companyID}/locations/actual` — Возвращает текущее местоположение компании · коды: 200, 204, 206 · примеры
  ← path: companyID:int → ResultsCommonLocationResult
- `GET /Companies/{id}` — Возвращает доступную пользователю компанию по идентификатору · коды: 200, 204 · примеры
  ← path: id:int → ResultsCompaniesGetResult

## CompanyListQueries
- `GET /CompanyListQueries` — Возвращает список сохранённых запросов, доступных в тенанте · коды: 200, 204, 206 · примеры
  → map<ResultsCompanyListQueriesCompanyListQueryResult>
- `GET /CompanyListQueries/{id}` — Возвращает сохранённый запрос · коды: 200, 204 · примеры
  ← path: id:int → ResultsCompanyListQueriesCompanyListQueryGetResult

## CompanyLocations
- `GET /CompanyLocations` — Возвращает список локаций компании · коды: 200, 204, 206, 409 · примеры
  ← query: companyID?:int, onDate?:datetime → map<ResultsCompaniesCompanyLocationResult>

## CompanyRegistrationTypes
- `GET /CompanyRegistrationTypes` — Возвращает список видов регистрации компании · коды: 200, 204 · примеры
  → map<ResultsCompanyRegistrationTypesListResult>

## Districts
- `GET /Districts` — Возвращает список доступных пользователю участков · коды: 200, 204, 206 · примеры
  ← query: includePath?:bool, parentID?:int, districtID?:int, assetID?:int, userID?:int, taskTypeID?:int → ResultsDistrictsDistrictListForTenantMemberResult[]
- `GET /Districts/{id}` — Возвращает доступный пользователю участок по идентификатору · коды: 200, 204 · примеры
  ← path: id:int → ResultsDistrictsDistrictResult

## Locations
- `GET /Locations` — Возвращает список локаций · коды: 200, 204, 206 · примеры
  ← query: searchText?:str, searchFor?:str, radius?:float, pointCenter?:str, pointNorthEast?:str, pointSouthWest?:str → map<ResultsCommonLocationResult>
- `HEAD /Locations` — Возвращает количество локаций · коды: 200, 206 · примеры
  ← query: searchFor?:str
- `GET /Locations/{id}` — Возвращает локацию с областью · коды: 200, 204 · примеры
  ← path: id:int → ResultsLocationsLocationGetResult

## OrgUnits
- `GET /OrgUnits` — Возвращает справочник активных организационных единиц, доступных пользователю · коды: 200, 204, 206 · примеры
  ← query: companyID?:int[] → map<ResultsOrgUnitsOrgUnitListResult>
- `GET /OrgUnits/root` — Возвращает справочник активных корневых организационных единиц, доступных пользователю · коды: 200, 204, 206 · примеры
  ← query: companyID?:int[] → map<ResultsOrgUnitsOrgUnitListResult>
- `GET /OrgUnits/{id}/orgunits` — Возвращает дочерние организационные единицы для указанного родителя · коды: 200, 204, 206, 400 · примеры
  ← path: id:int; query: companyID?:int[] → map<ResultsOrgUnitsOrgUnitListResult>

## PreferredTechnicians
- `GET /PreferredTechnicians` — Список предпочтительных исполнителей для объекта(ов) · коды: 200, 204 · примеры
  ← query: assetID?:int, userID?:int → ResultsPreferredTechniciansPreferredTechniciansResult
