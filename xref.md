# HubEx API — кросс-индекс ресурсов

> **Что здесь:** где read-ручка (GET/HEAD) дёргает ресурс во ВСЕХ сервисах (от ресурса) и что можно у сущности (от сущности). Указатели ведут в `endpoints/<SVC>.md`; типы — `schemas/<SVC>.md`.
> **Линза read-only:** здесь только GET/HEAD. Write-ручки (POST/PUT/PATCH/DELETE) и их типы в API **существуют**, но в эту линзу не входят — не делай из их отсутствия здесь вывода, что их нет в API.
## От сущности

### Assets (ES)

- assets [GET]
- assignments [GET]
- attachments [GET]
- attributes [GET]
- checklists [GET]
- contacts [GET]
- districts [GET]
- locations [GET]
- skills [GET]
- tags [GET]
- worktypes [GET]

### AssetSchemas (ES)

- image [GET]
- points [GET]

### AssetTemplates (ES)

- attachments [GET]
- attributes [GET]
- districts [GET]
- skills [GET]
- worktypes [GET]

### AssetTypes (ES)

- worktypes [GET]

### Attachments (COMMON)

- roles [GET]

### CheckLists (WORK)

- items [GET]

### Companies (ES)

- attachment [GET]
- attachments [GET]
- attributes [GET]
- bankaccounts [GET]
- contacts [GET]
- locations [GET]

### DeadlineRules (SLA)

- attributes [GET]

### Issues (WH)

- items [GET]

### LayoutTemplates (UI)

- attributes [GET]
- components [GET]
- tasktypes [GET]

### MailBoxes (MSG)

- errors [GET]
- senders [GET]

### Materials (WH)

- attachment [GET]
- attachments [GET]
- barcodes [GET]

### OrgUnits (ES)

- orgunits [GET]

### Receipts (WH)

- items [GET]

### Roles (ADM)

- applications [GET]
- attachments [GET]
- packages [GET]
- permissionsapi [GET]
- permissionsext [GET]
- permissionsui [GET]

### Schedules (PMP)

- appointments [GET]

### ServiceContract (SC)

- assets [GET]
- attachment [GET]
- attachments [GET]
- attributes [GET]
- contacts [GET]

### Tasks (WORK)

- assignments [GET]
- attachment [GET]
- attachments [GET]
- attributes [GET]
- changes [GET]
- checklists [GET]
- completedworks [GET]
- contacts [GET]
- conversations [GET, HEAD]
- marking-codes [GET]
- materials [GET]
- ratings [GET]
- skills [GET]
- stages [GET]
- tags [GET]
- watchlists [GET]

### TaskStages (TSTG)

- messagetriggers [GET]
- requirements [GET]

### TaskTemplates (WORK)

- assignment [GET]
- excludedassets [GET]
- schedules [GET]

### TaskTypes (WORK)

- districts [GET]
- route [GET]
- worktypes [GET]

### Technicians (PA)

- rating [GET]
- taskratings [GET]
- workschedules [GET]

### Triggers (MSG)

- criticalities [GET]

### Users (ADM)

- assetassignments [GET]
- assetlistqueries [GET]
- attributes [GET]
- companylistqueries [GET]
- defaultpages [GET]
- districts [GET]
- notifications [GET]
- ratings [GET]
- roles [GET]
- skills [GET]
- tags [GET]
- tasklistqueries [GET]
- warehouses [GET]

### Users (PA)

- worktypes [GET]

### UserTemplates (ADM)

- districts [GET]
- roles [GET]

### UserViews (UI)

- applications [GET]

### Warehouses (WH)

- users [GET]

### WorkTypes (WORK)

- checklists [GET]
- tasktypes [GET]
- worktypes [GET]


## От ресурса

### accounts

- [AUTH · GET /Accounts](endpoints/AUTH.md) → AUTH:GetResult
- [AUTH · HEAD /Accounts](endpoints/AUTH.md)

### action

- [TSTG · GET /Action](endpoints/TSTG.md) → TSTG:map<ActionResult>

### applications

- [ADM · GET /Roles/{roleID}/applications](endpoints/ADM.md) → ADM:map<ResultsRoleApplicationListResult>
- [AUTH · GET /Accounts/this/applications](endpoints/AUTH.md) → AUTH:ApplicationListResult[]
- [COMMON · GET /Applications](endpoints/COMMON.md) → COMMON:map<ApplicationResult>
- [UI · GET /UserViews/Users/{userID}/Applications/{applicationID}/{code}](endpoints/UI.md) → UI:TaskViewProjection

### appointments

- [PA · GET /Technicians/{userID}/workSchedules/appointments](endpoints/PA.md) → PA:AppointmentResult[]
- [PMP · GET /ScheduledTasks/appointments](endpoints/PMP.md) → PMP:AppointmentResult<AssetAssignResult>[]
- [PMP · GET /ScheduledTasks/v2/appointments](endpoints/PMP.md) → PMP:AppointmentResult<AssetAssignResultV2>[]
- [PMP · GET /Schedules/appointments/assign](endpoints/PMP.md) → PMP:map<ScheduleAppointmentAssignListResult[]>
- [PMP · GET /Schedules/{scheduleID}/appointments/assign](endpoints/PMP.md) → PMP:map<ScheduleAppointmentAssignListResult[]>
- [PMP · GET /Schedules/{scheduleID}/appointments](endpoints/PMP.md) → PMP:ScheduleAppointments.ListResult[]
- [PMP · HEAD /ScheduledTasks/appointments](endpoints/PMP.md)

### articles

- [NEWS · GET /Articles](endpoints/NEWS.md) → NEWS:map<ListResult>

### asclist

- [ES · GET /AssetSchemas/ascList/{assetID}](endpoints/ES.md) → ES:map<ResultsAssetSchemaSchemaBase>

### asset

- [ES · GET /AssetSchemas/asset/{assetID}](endpoints/ES.md) → ES:ResultsAssetSchemaSchema

### assetassignments

- [ADM · GET /Users/{userID}/assetAssignments](endpoints/ADM.md) → ADM:ResultsUsersAssetAssignmentResult[]
- [PA · GET /AssetAssignments](endpoints/PA.md) → PA:AssetAssignments.ListResult[]

### assetclasses

- [ES · GET /AssetClasses/{id}](endpoints/ES.md) → ES:ResultsAssetClassesAssetClassGetResult
- [ES · GET /AssetClasses](endpoints/ES.md) → ES:map<ResultsAssetClassesAssetClassListResult>

### assetfilter

- [ES · GET /AssetFilter](endpoints/ES.md) → ES:ProjectionsCOMMONFilterListItemProjection[]

### assetlistqueries

- [ADM · GET /Users/this/assetListQueries](endpoints/ADM.md) → ADM:map<ResultsUsersAssetListQueryResult>
- [ADM · GET /Users/{id}/assetListQueries](endpoints/ADM.md) → ADM:map<ResultsUsersAssetListQueryResult>
- [ES · GET /AssetListQueries/{id}](endpoints/ES.md) → ES:map<ResultsAssetListQueriesAssetListQueryResult>
- [ES · GET /AssetListQueries](endpoints/ES.md) → ES:map<ResultsAssetListQueriesAssetListQueryResult>[]

### assetlocations

- [ES · GET /AssetLocations](endpoints/ES.md)

### assetmaintenance

- [REPORT · GET /AssetMaintenance/planned](endpoints/REPORT.md) → REPORT:PlannedMaintenanceResult[]

### assets

- [ES · GET /Assets/root](endpoints/ES.md) → ES:map<ResultsAssetsAssetExtResult>
- [ES · GET /Assets/{assetID}](endpoints/ES.md) → ES:ResultsAssetsAssetDetailedInfoResult
- [ES · GET /Assets/{parentAssetID}/assets/all](endpoints/ES.md) → ES:map<ResultsAssetsAssetExtResult>
- [ES · GET /Assets/{parentAssetID}/assets](endpoints/ES.md) → ES:map<ResultsAssetsAssetExtResult>
- [ES · GET /Assets](endpoints/ES.md) → ES:map<ResultsAssetsAssetExtResult>
- [ES · HEAD /Assets](endpoints/ES.md)
- [EXPORT · GET /Assets](endpoints/EXPORT.md)
- [SC · GET /ServiceContract/{contractID}/assets](endpoints/SC.md) → SC:map<AssetResultBase>

### assetschemas

- [ES · GET /AssetSchemas/list](endpoints/ES.md) → ES:map<ResultsAssetSchemaSchemaBase>
- [ES · GET /AssetSchemas/{schemaID}](endpoints/ES.md) → ES:ResultsAssetSchemaSchema

### assetsearchsettings

- [ES · GET /AssetSearchSettings](endpoints/ES.md) → ES:ProjectionsESAssetSearchFieldSettingsProjection[]

### assettemplates

- [ES · GET /AssetTemplates/{id}](endpoints/ES.md) → ES:ResultsAssetTemplatesGetResult
- [ES · GET /AssetTemplates](endpoints/ES.md) → ES:map<ResultsAssetTemplatesListResult>

### assettypes

- [ES · GET /AssetTypes/{id}](endpoints/ES.md)
- [ES · GET /AssetTypes](endpoints/ES.md) → ES:map<ResultsAssetTypesGetResult>

### assigneeselectionrules

- [TSTG · GET /AssigneeSelectionRules/{id}](endpoints/TSTG.md) → TSTG:AssigneeSelectionRule.GetResult
- [TSTG · GET /AssigneeSelectionRules](endpoints/TSTG.md) → TSTG:map<AssigneeSelectionRule.ListResult>

### assignment

- [WORK · GET /TaskTemplates/{id}/assignment](endpoints/WORK.md) → WORK:TaskTemplateAssignmentDetailsProjection

### assignments

- [ES · GET /Assets/{assetID}/assignments](endpoints/ES.md) → ES:ResultsAssetsAssetAssignmentResult[]
- [WORK · GET /Tasks/{taskID}/assignments](endpoints/WORK.md) → WORK:ListAssignmentHistoryResult

### attachment

- [ES · GET /Companies/{companyID}/attachment/{attachmentID}](endpoints/ES.md) → ES:ResultsCommonGetAttachmentResult
- [SC · GET /ServiceContract/{contractID}/attachment/{attachmentID}](endpoints/SC.md) → SC:AttachmentResult
- [WH · GET /Materials/{materialID}/attachment/{attachmentID}](endpoints/WH.md) → WH:MaterialAttachmentResult
- [WORK · GET /Tasks/{taskID}/attachment/{attachmentID}](endpoints/WORK.md) → WORK:GetAttachmentResult
- [WORK · GET /Tasks/{taskID}/completedWorks/report/attachment](endpoints/WORK.md)

### attachments

- [ADM · GET /Roles/{roleID}/attachments](endpoints/ADM.md) → ADM:ResultsCommonAttachmentResult[]
- [COMMON · GET /Attachments/downloadLink](endpoints/COMMON.md) → COMMON:DownloadLinkResult
- [COMMON · GET /Attachments/{attachmentID}/this](endpoints/COMMON.md) → COMMON:Attachments.GetResult
- [COMMON · GET /Attachments/{attachmentID}](endpoints/COMMON.md)
- [COMMON · GET /Attachments](endpoints/COMMON.md) → COMMON:map<Attachments.ListResult>
- [ES · GET /AssetTemplates/{assetTemplateID}/attachments/{attachmentID}](endpoints/ES.md)
- [ES · GET /AssetTemplates/{assetTemplateID}/attachments](endpoints/ES.md) → ES:map<ResultsCommonListAttachmentResult>
- [ES · GET /Assets/{assetID}/attachments/{attachmentID}](endpoints/ES.md)
- [ES · GET /Assets/{assetID}/attachments](endpoints/ES.md) → ES:map<ResultsCommonListAttachmentResult>
- [ES · GET /Companies/{CompanyID}/attachments/{attachmentID}](endpoints/ES.md)
- [ES · GET /Companies/{companyID}/attachments](endpoints/ES.md) → ES:map<ResultsCommonListAttachmentResult>
- [SC · GET /ServiceContract/{contractID}/attachments/{attachmentID}](endpoints/SC.md)
- [SC · GET /ServiceContract/{contractID}/attachments](endpoints/SC.md) → SC:map<AttachmentListResult>
- [WH · GET /Materials/{materialID}/attachments/{attachmentID}](endpoints/WH.md)
- [WH · GET /Materials/{materialID}/attachments](endpoints/WH.md) → WH:map<MaterialAttachmentListResult>
- [WORK · GET /Tasks/{taskID}/attachments/{attachmentID}](endpoints/WORK.md)
- [WORK · GET /Tasks/{taskID}/attachments](endpoints/WORK.md) → WORK:map<Common.ListAttachmentResult>
- [WORK · GET /Tasks/{taskID}/checkLists/{taskCheckListID}/results/attachments](endpoints/WORK.md) → WORK:map<Common.ListAttachmentResult>
- [WORK · GET /Tasks/{taskID}/checkLists/{taskCheckListID}/results/{taskCheckListResultID}/attachments/{attachmentID}](endpoints/WORK.md)
- [WORK · GET /Tasks/{taskID}/checkLists/{taskCheckListID}/results/{taskCheckListResultID}/attachments](endpoints/WORK.md) → WORK:map<Common.ListAttachmentResult>
- [WORK · GET /Tasks/{taskID}/completedWorks/attachments](endpoints/WORK.md) → WORK:ListAttachmentForCompletedWorkResult[]
- [WORK · GET /Tasks/{taskID}/completedWorks/{completedWorkID}/attachments/{attachmentID}](endpoints/WORK.md)
- [WORK · GET /Tasks/{taskID}/completedWorks/{completedWorkID}/attachments](endpoints/WORK.md) → WORK:ListAttachmentForCompletedWorkResult[]
- [WORK · GET /Tasks/{taskID}/completedWorks/{completedWorkID}/attributes/attachments](endpoints/WORK.md) → WORK:map<CompletedWorkAttributeAttachment.ListAttachmentResult[]>
- [WORK · GET /Tasks/{taskID}/completedWorks/{completedWorkID}/attributes/{attributeID}/attachments](endpoints/WORK.md) → WORK:map<CompletedWorkAttributeAttachment.ListAttachmentResult[]>
- [WORK · GET /Tasks/{taskID}/conversations/{taskConversationID}/attachments/{attachmentID}](endpoints/WORK.md)

### attributes

- [ADM · GET /RoleTaskPropertiesAccess/attributes](endpoints/ADM.md) → ADM:ResultsRoleTaskAttributeRoleTaskAttributeSettings[]
- [ADM · GET /Users/attributes](endpoints/ADM.md) → ADM:ResultsUserAttributeUserAttributesResult[]
- [ADM · GET /Users/{userID}/attributes](endpoints/ADM.md) → ADM:ResultsUserAttributeUserAttributesResult[]
- [COMMON · GET /Attributes/{attributeID}/listOfValues](endpoints/COMMON.md) → COMMON:map<str>
- [COMMON · GET /Attributes/{attributeID}](endpoints/COMMON.md) → COMMON:AttributeResultGet
- [COMMON · GET /Attributes](endpoints/COMMON.md) → COMMON:map<AttributeResultList>
- [ES · GET /AssetTemplates/{assetTemplateID}/attributes](endpoints/ES.md) → ES:ResultsAssetTemplatesAssetTemplateAttributeResult[]
- [ES · GET /Assets/attributes](endpoints/ES.md) → ES:ResultsAssetsAssetAttributesExtResult[]
- [ES · GET /Assets/{assetID}/attributes](endpoints/ES.md) → ES:ResultsAssetsAssetAttributeResult[]
- [ES · GET /Companies/{companyID}/attributes](endpoints/ES.md) → ES:ResultsCompanyAttributesCompanyAttributeResult[]
- [SC · GET /ServiceContract/{contractID}/attributes](endpoints/SC.md) → SC:ContractAttributeResult[]
- [SLA · GET /Attributes](endpoints/SLA.md) → SLA:map<Attributes.ListResult>
- [SLA · GET /DeadlineRules/{deadlineRuleID}/attributes](endpoints/SLA.md) → SLA:map<int[]>
- [UI · GET /LayoutTemplates/{id}/Attributes](endpoints/UI.md) → UI:AttributeDto[]
- [WORK · GET /Tasks/{taskID}/attributes](endpoints/WORK.md) → WORK:AttributeResult[]
- [WORK · GET /Tasks/{taskID}/completedWorks/attributes](endpoints/WORK.md) → WORK:CompletedWorkAttributeResult[]
- [WORK · GET /Tasks/{taskID}/completedWorks/{completedWorkID}/attributes](endpoints/WORK.md) → WORK:CompletedWorkAttributeResult[]

### attributetypes

- [COMMON · GET /AttributeTypes/v2](endpoints/COMMON.md) → COMMON:ExtListResult[]
- [COMMON · GET /AttributeTypes](endpoints/COMMON.md) → COMMON:map<AttributeTypes.ListResult>

### availability

- [TSTG · GET /TaskStageComponents/availability](endpoints/TSTG.md) → TSTG:AvailabilityListResult

### bankaccounts

- [ES · GET /Companies/{companyID}/bankAccounts](endpoints/ES.md) → ES:map<ResultsCompanyBankAccountsListResult>

### banks

- [COMMON · GET /Banks/{bankId}](endpoints/COMMON.md) → COMMON:BankResult
- [COMMON · GET /Banks](endpoints/COMMON.md) → COMMON:map<BankResult>

### banreasons

- [ADM · GET /BanReasons](endpoints/ADM.md) → ADM:map<ResultsBanReasonsListResult>

### barcodes

- [WH · GET /Materials/{materialID}/barcodes](endpoints/WH.md) → WH:map<MaterialBarcodes.ListResult[]>

### barcodetypes

- [WH · GET /BarcodeTypes](endpoints/WH.md) → WH:map<BarcodeTypes.ListResult>

### branches

- [TSTG · GET /Branches](endpoints/TSTG.md) → TSTG:map<BranchResult>

### bytype

- [UI · GET /LayoutTemplates/bytype/{id}](endpoints/UI.md) → UI:LayoutTemplateDto

### capabilities

- [ADM · GET /Capabilities](endpoints/ADM.md) → ADM:map<ResultsCapabilitiesListResult>

### changes

- [WORK · GET /Tasks/{taskID}/changes](endpoints/WORK.md) → WORK:HistoryResult[]

### checklists

- [ES · GET /Assets/{assetID}/checkLists](endpoints/ES.md) → ES:map<ResultsAssetCheckListsGetResult[]>
- [WORK · GET /CheckLists/{id}](endpoints/WORK.md) → WORK:map<CheckLists.GetResult>
- [WORK · GET /CheckLists](endpoints/WORK.md) → WORK:map<CheckLists.ListResult>
- [WORK · GET /Tasks/{taskID}/checkLists](endpoints/WORK.md) → WORK:map<TaskCheckListResult>
- [WORK · GET /WorkTypes/{workTypeID}/checkLists](endpoints/WORK.md) → WORK:map<CheckLists.GetResult[]>

### companies

- [ES · GET /Companies/{id}](endpoints/ES.md) → ES:ResultsCompaniesGetResult
- [ES · GET /Companies](endpoints/ES.md) → ES:map<ResultsCompaniesListResult>
- [ES · HEAD /Companies](endpoints/ES.md)
- [EXPORT · GET /Companies](endpoints/EXPORT.md)

### companylistqueries

- [ADM · GET /Users/this/companyListQueries](endpoints/ADM.md) → ADM:map<ResultsUsersCompanyListQueryResult>
- [ADM · GET /Users/{id}/companyListQueries](endpoints/ADM.md) → ADM:map<ResultsUsersCompanyListQueryResult>
- [ES · GET /CompanyListQueries/{id}](endpoints/ES.md) → ES:ResultsCompanyListQueriesCompanyListQueryGetResult
- [ES · GET /CompanyListQueries](endpoints/ES.md) → ES:map<ResultsCompanyListQueriesCompanyListQueryResult>

### companylocations

- [ES · GET /CompanyLocations](endpoints/ES.md)

### companyregistrationtypes

- [ES · GET /CompanyRegistrationTypes](endpoints/ES.md) → ES:map<ResultsCompanyRegistrationTypesListResult>

### completedworks

- [WORK · GET /Tasks/{taskID}/completedWorks/materialsWithCodes](endpoints/WORK.md) → WORK:map<CompletedWorkMaterialResult>
- [WORK · GET /Tasks/{taskID}/completedWorks/{id}](endpoints/WORK.md) → WORK:CompletedWorkResult[]
- [WORK · GET /Tasks/{taskID}/completedWorks](endpoints/WORK.md) → WORK:CompletedWorkResult[]

### completiontime

- [REPORT · GET /CompletionTime](endpoints/REPORT.md) → REPORT:TaskListGroupByAssigneesResult[]

### components

- [UI · GET /Components](endpoints/UI.md) → UI:map<ComponentResult>
- [UI · GET /LayoutTemplates/{id}/Components](endpoints/UI.md) → UI:ComponentDto[]

### contacts

- [COMMON · GET /Contacts/{contactID}](endpoints/COMMON.md) → COMMON:Contacts.GetResult
- [COMMON · GET /Contacts](endpoints/COMMON.md) → COMMON:map<Contacts.ListResult>
- [ES · GET /Assets/{assetID}/contacts/{contactID}](endpoints/ES.md) → ES:ResultsAssetContactsGetResult
- [ES · GET /Assets/{assetID}/contacts](endpoints/ES.md) → ES:ResultsAssetContactsListResult[]
- [ES · GET /Companies/{companyID}/contacts/{contactID}](endpoints/ES.md) → ES:ResultsCompanyContactsGetResult
- [ES · GET /Companies/{companyID}/contacts](endpoints/ES.md) → ES:map<ResultsCompanyContactsListResult>
- [SC · GET /ServiceContract/{contractID}/contacts](endpoints/SC.md) → SC:map<ContactResultBase>
- [WORK · GET /Tasks/{taskID}/contacts/{contactID}](endpoints/WORK.md) → WORK:TaskContacts.GetResult
- [WORK · GET /Tasks/{taskID}/contacts](endpoints/WORK.md) → WORK:map<TaskContacts.ListResult>

### content

- [COMMON · GET /Attachments/content/{container}/{filePath}](endpoints/COMMON.md)

### contenttypes

- [MSG · GET /ContentTypes](endpoints/MSG.md) → MSG:ContentTypes.ListResult[]

### conversations

- [WORK · GET /Tasks/{taskID}/conversations/{taskConversationID}](endpoints/WORK.md) → WORK:TaskMessage
- [WORK · GET /Tasks/{taskID}/conversations](endpoints/WORK.md) → WORK:TaskMessage[]
- [WORK · HEAD /Tasks/{taskID}/conversations](endpoints/WORK.md)

### countries

- [COMMON · GET /Countries](endpoints/COMMON.md) → COMMON:map<Countries.ListResult>

### criticalities

- [MSG · GET /Triggers/{id}/criticalities](endpoints/MSG.md) → MSG:Triggers.ListResult[]
- [SLA · GET /Criticalities/{id}](endpoints/SLA.md) → SLA:Criticalities.GetResult
- [SLA · GET /Criticalities](endpoints/SLA.md) → SLA:map<Criticalities.GetResult>

### currencies

- [COMMON · GET /Currencies](endpoints/COMMON.md) → COMMON:map<Currencies.ListResult>

### dadata

- [ES · GET /Companies/dadata/find](endpoints/ES.md) → ES:ESCompanyAddData

### deadlinerules

- [SLA · GET /DeadlineRules/{DeadlineRuleID}](endpoints/SLA.md) → SLA:DeadlineRules.GetResult
- [SLA · GET /DeadlineRules](endpoints/SLA.md) → SLA:map<DeadlineRules.ListResult>

### defaultpages

- [ADM · GET /DefaultPages](endpoints/ADM.md) → ADM:ResultsDefaultPagesAllowedPageResult[]
- [ADM · GET /Users/{userID}/defaultPages](endpoints/ADM.md) → ADM:ResultsUserDefaultPagesGetResult

### delivery

- [WORK · GET /Tasks/{taskID}/conversations/{taskConversationID}/delivery](endpoints/WORK.md) → WORK:ListConversationDeliveryResult[]

### districts

- [ADM · GET /UserTemplates/{id}/districts](endpoints/ADM.md) → ADM:IdNameResultOfShort[]
- [ADM · GET /Users/{id}/districts](endpoints/ADM.md) → ADM:map<IdNameResultOfShort>
- [ES · GET /AssetTemplates/{assetTemplateID}/districts](endpoints/ES.md) → ES:int[]
- [ES · GET /Assets/{assetID}/districts](endpoints/ES.md) → ES:ResultsCommonAssetDistrictResult[]
- [ES · GET /Districts/{id}](endpoints/ES.md) → ES:ResultsDistrictsDistrictResult
- [ES · GET /Districts](endpoints/ES.md) → ES:ResultsDistrictsDistrictListForTenantMemberResult[]
- [WORK · GET /TaskTypes/{id}/districts](endpoints/WORK.md) → WORK:map<TaskTypeDistrictList>

### documentstatuses

- [WH · GET /DocumentStatuses](endpoints/WH.md) → WH:map<DocumentStatuses.ListResult>

### documenttypes

- [WH · GET /DocumentTypes](endpoints/WH.md) → WH:map<DocumentTypes.ListResult>

### employment

- [PA · GET /Employment/{userID}](endpoints/PA.md) → PA:EmploymentGetResult[]

### errors

- [MSG · GET /MailBoxes/{id}/errors](endpoints/MSG.md) → MSG:MailBox.GetResult

### events

- [COMMON · GET /Events](endpoints/COMMON.md) → COMMON:Events.ListResult[]

### excludedassets

- [WORK · GET /TaskTemplates/{tasktTemplateID}/excludedAssets](endpoints/WORK.md) → WORK:map<TaskTemplateExcludedAssetResult>

### extended

- [EXPORT · GET /Assets/extended/includes](endpoints/EXPORT.md) → EXPORT:FieldResult[]
- [EXPORT · GET /Assets/extended](endpoints/EXPORT.md)
- [EXPORT · GET /Tasks/extended/V2](endpoints/EXPORT.md)
- [EXPORT · GET /Tasks/extended/includes](endpoints/EXPORT.md) → EXPORT:FieldResult[]
- [EXPORT · GET /Tasks/extended](endpoints/EXPORT.md)

### fields

- [MSG · GET /Notifications/fields](endpoints/MSG.md) → MSG:map<str>

### filters

- [UI · GET /Filters](endpoints/UI.md) → UI:UserFilterFavouriteEntity[]

### frequencytypes

- [PMP · GET /FrequencyTypes](endpoints/PMP.md) → PMP:map<IdCodeNameResult<Byte>>[]

### geolocationsettings

- [ADM · GET /GeolocationSettings/coordinateAccuracy](endpoints/ADM.md) → ADM:IdNameDescriptionEntityOfByte[]

### geotrackingmodes

- [PA · GET /GeoTrackingModes](endpoints/PA.md) → PA:map<GeoTrackingModes.ListResult>

### groupby

- [WORK · GET /Tasks/groupBy/geoHash](endpoints/WORK.md) → WORK:TaskGroupByResult<ClusterResult>[]

### image

- [ES · GET /AssetSchemas/{schemaId}/image/download](endpoints/ES.md)
- [ES · GET /AssetSchemas/{schemaId}/image](endpoints/ES.md) → ES:ResultsAssetSchemaSchemaImage

### inventories

- [WH · GET /Inventories/actual](endpoints/WH.md) → WH:Inventories.ListResult
- [WH · GET /Inventories](endpoints/WH.md) → WH:map<Inventories.ListResult>

### invitations

- [ADM · GET /Invitations/{id}/short](endpoints/ADM.md) → ADM:ResultsInvitationsGetShortResult
- [ADM · GET /Invitations/{id}](endpoints/ADM.md) → ADM:ResultsInvitationsGetResult
- [ADM · GET /Invitations](endpoints/ADM.md) → ADM:map<ResultsInvitationsGetResult>

### issues

- [WH · GET /Issues/{id}](endpoints/WH.md) → WH:IssueResult
- [WH · GET /Issues](endpoints/WH.md) → WH:map<IssueResult>
- [WH · HEAD /Issues](endpoints/WH.md) → WH:map<IssueResult>

### items

- [WH · GET /Issues/{issueID}/items](endpoints/WH.md) → WH:IssueItems.ListResult[]
- [WH · GET /Receipts/{receiptID}/items](endpoints/WH.md) → WH:ReceiptItems.ListResult[]
- [WORK · GET /CheckLists/{checkListID}/items](endpoints/WORK.md) → WORK:map<CheckListItemResult>

### layouttemplates

- [UI · GET /LayoutTemplates/default](endpoints/UI.md) → UI:LayoutTemplateDto
- [UI · GET /LayoutTemplates/{id}](endpoints/UI.md) → UI:LayoutTemplateDto
- [UI · GET /LayoutTemplates](endpoints/UI.md) → UI:LayoutTemplateDto[]

### licenses

- [ADM · GET /Tenants/this/licenses](endpoints/ADM.md) → ADM:ResultsTenantLicenseListTenantLicenseResult

### licensescanner

- [LIC · GET /LicenseScanner/State](endpoints/LIC.md) → LIC:WatcherStateEnum

### locations

- [ES · GET /Assets/{assetID}/locations/actual](endpoints/ES.md) → ES:ResultsCommonLocationResult
- [ES · GET /Companies/{companyID}/locations/actual](endpoints/ES.md) → ES:ResultsCommonLocationResult
- [ES · GET /Locations/{id}](endpoints/ES.md) → ES:map<ResultsLocationsLocationGetResult>
- [ES · GET /Locations](endpoints/ES.md) → ES:map<ResultsCommonLocationResult>
- [ES · HEAD /Locations](endpoints/ES.md)

### mailboxes

- [MSG · GET /MailBoxes/regexactions](endpoints/MSG.md) → MSG:map<RegexNotMatchAction.ListResult>
- [MSG · GET /MailBoxes/{id}](endpoints/MSG.md) → MSG:MailBox.GetResult
- [MSG · GET /MailBoxes](endpoints/MSG.md) → MSG:map<MailBox.ListResult>

### marking-codes

- [WORK · GET /Tasks/{taskId}/completedWorks/{completedWorkID}/marking-codes](endpoints/WORK.md) → WORK:MarkingCodesListResult
- [WORK · GET /Tasks/{taskId}/completedWorks/{completedWorkID}/materials/{materialID}/marking-codes](endpoints/WORK.md) → WORK:MarkingCodesListResult
- [WORK · GET /Tasks/{taskId}/marking-codes](endpoints/WORK.md) → WORK:MarkingCodesListResult

### materialconsumption

- [EXPORT · GET /MaterialConsumption](endpoints/EXPORT.md)

### materialconsumptions

- [WH · GET /MaterialConsumptions](endpoints/WH.md) → WH:map<MaterialInventoryResult>

### materials

- [EXPORT · GET /Materials/v2.0](endpoints/EXPORT.md)
- [EXPORT · GET /Materials](endpoints/EXPORT.md)
- [WH · GET /Materials/v2](endpoints/WH.md) → WH:map<MaterialListResult>
- [WH · GET /Materials/{id}](endpoints/WH.md) → WH:MaterialResult
- [WH · GET /Materials/{required}](endpoints/WH.md) → WH:ListRequiredResult[]
- [WH · GET /Materials](endpoints/WH.md) → WH:Materials.ListResult[]
- [WH · HEAD /Materials](endpoints/WH.md) → WH:map<MaterialListResult>
- [WORK · GET /Tasks/{taskID}/completedWorks/materials](endpoints/WORK.md) → WORK:map<CompletedWorkMaterialResult>
- [WORK · GET /Tasks/{taskID}/completedWorks/{completedWorkID}/materials](endpoints/WORK.md) → WORK:CompletedWorkMaterialResult
- [WORK · GET /Tasks/{taskID}/materials](endpoints/WORK.md) → WORK:map<TaskMaterials.ListResult>

### measurementunits

- [COMMON · GET /MeasurementUnits](endpoints/COMMON.md) → COMMON:map<MeasurementUnitResult>

### messagetemplates

- [MSG · GET /MessageTemplates/{id}](endpoints/MSG.md) → MSG:map<MessageTemplates.GetResult>
- [MSG · GET /MessageTemplates](endpoints/MSG.md) → MSG:map<MessageTemplates.ListResult>

### messagetriggers

- [TSTG · GET /TaskStages/{id}/messageTriggers](endpoints/TSTG.md) → TSTG:IdNameResult<Int16>[]

### moblities

- [PA · GET /Moblities](endpoints/PA.md) → PA:map<Mobilities.ListResult>

### navigateto

- [MSG · GET /NavigateTo](endpoints/MSG.md) → MSG:NavigateTo.ListResult[]
- [PROXY · GET /NavigateTo/{appCode}](endpoints/PROXY.md) → PROXY:GetResult

### new

- [WORK · GET /Tasks/new/meta](endpoints/WORK.md) → WORK:map<TaskTypeFormMetadataResult>

### notifications

- [ADM · GET /Users/this/notifications](endpoints/ADM.md) → ADM:ResultsUserDisabledNotificationsListResult
- [ADM · GET /Users/{id}/notifications](endpoints/ADM.md) → ADM:ResultsUserDisabledNotificationsListResult
- [AUTH · GET /Accounts/this/notifications](endpoints/AUTH.md) → AUTH:ListResult[]
- [MSG · GET /Notifications](endpoints/MSG.md) → MSG:map<Notification.ListResult>
- [MSG · HEAD /Notifications](endpoints/MSG.md)

### numbersequences

- [WH · GET /NumberSequences/{documentTypeId}](endpoints/WH.md) → WH:NumberSequenceResult
- [WH · GET /NumberSequences](endpoints/WH.md) → WH:NumberSequenceResult[]

### onshift

- [PA · GET /Users/onshift/status](endpoints/PA.md) → PA:WorkShiftScheduleUserStatusResult[]

### operationtypes

- [WH · GET /OperationTypes/{id}](endpoints/WH.md) → WH:OperationTypeResult
- [WH · GET /OperationTypes](endpoints/WH.md) → WH:map<OperationTypeResult>

### orgunits

- [ES · GET /OrgUnits/root](endpoints/ES.md)
- [ES · GET /OrgUnits/{id}/orgunits](endpoints/ES.md)
- [ES · GET /OrgUnits](endpoints/ES.md)

### overridings

- [TSTG · GET /TaskStageLinks/overridings](endpoints/TSTG.md) → TSTG:OverrideListResult[]

### packages

- [ADM · GET /Roles/{roleID}/packages](endpoints/ADM.md) → ADM:map<ResultsRolePackagesListResult[]>
- [ADM · GET /Tenants/this/packages](endpoints/ADM.md) → ADM:ResultsTenantPackagesListResult[]

### permissionapitags

- [ADM · GET /PermissionApiTags](endpoints/ADM.md) → ADM:map<ResultsPermissionsApiTagListResult[]>

### permissionexttags

- [ADM · GET /PermissionExtTags](endpoints/ADM.md) → ADM:map<ResultsPermissionsExtTagListResult[]>

### permissions

- [ADM · GET /Users/this/permissions/ext](endpoints/ADM.md) → ADM:map<str>
- [ADM · GET /Users/this/permissions/ui](endpoints/ADM.md) → ADM:map<str>

### permissionsapi

- [ADM · GET /PermissionsApi](endpoints/ADM.md) → ADM:map<ResultsPermissionsApiListResult>
- [ADM · GET /Roles/{roleID}/permissionsApi](endpoints/ADM.md) → ADM:map<ResultsRolePermissionsApiListResult[]>

### permissionsext

- [ADM · GET /PermissionsExt](endpoints/ADM.md) → ADM:map<ResultsPermissionsExtListResult>
- [ADM · GET /Roles/{roleID}/permissionsExt](endpoints/ADM.md) → ADM:map<ResultsRolePermissionsExtListResult[]>

### permissionsui

- [ADM · GET /PermissionsUi/{id}](endpoints/ADM.md) → ADM:ResultsPermissionsUiGetResult
- [ADM · GET /PermissionsUi](endpoints/ADM.md) → ADM:map<ResultsPermissionsUiGetResult>
- [ADM · GET /Roles/{roleID}/permissionsUi](endpoints/ADM.md) → ADM:map<ResultsRolePermissionsUiListResult[]>

### points

- [ES · GET /AssetSchemas/{schemaID}/points](endpoints/ES.md) → ES:ResultsAssetSchemaSchemaTask[]

### powerbicustomreports

- [REPORT · GET /PowerBICustomReports](endpoints/REPORT.md) → REPORT:map<CustomReportList>

### powerbireports

- [COMMON · GET /PowerBIReports/{id}](endpoints/COMMON.md) → COMMON:PowerBIReportResult
- [COMMON · GET /PowerBIReports](endpoints/COMMON.md) → COMMON:PowerBIReportResult[]

### preferredtechnicians

- [ES · GET /PreferredTechnicians](endpoints/ES.md) → ES:ResultsAssetsAssetDetailedInfoResult

### protocols

- [MSG · GET /Protocols](endpoints/MSG.md) → MSG:map<Protocols.ListResult>

### providers

- [MSG · GET /Providers](endpoints/MSG.md) → MSG:Providers.ListResult[]

### rating

- [PA · GET /Technicians/{userID}/rating](endpoints/PA.md) → PA:TechnicianRatingResult[]

### ratingcriteria

- [PA · GET /RatingCriteria/{id}](endpoints/PA.md) → PA:RatingCriteria.GetResult
- [PA · GET /RatingCriteria](endpoints/PA.md) → PA:map<RatingCriteria.ListResult>

### ratings

- [ADM · GET /Users/{UserID}/ratings](endpoints/ADM.md) → ADM:ResultsUsersRatingTechnicianResult
- [WORK · GET /Tasks/{taskID}/ratings/avg](endpoints/WORK.md) → WORK:RatingResult[]
- [WORK · GET /Tasks/{taskID}/ratings](endpoints/WORK.md) → WORK:RatingResult[]

### reactiontime

- [REPORT · GET /ReactionTime](endpoints/REPORT.md) → REPORT:TaskListGroupByAssigneesResult[]

### receipts

- [WH · GET /Receipts/{id}](endpoints/WH.md) → WH:ReceiptResult
- [WH · GET /Receipts](endpoints/WH.md) → WH:map<ReceiptResult>
- [WH · HEAD /Receipts](endpoints/WH.md) → WH:map<ReceiptResult>

### recipients

- [MSG · GET /RecipientSelectionRules/recipients](endpoints/MSG.md) → MSG:RecipientListResult[]

### recipientselectionrules

- [MSG · GET /RecipientSelectionRules/{id}](endpoints/MSG.md) → MSG:map<RecipientSelectionRules.GetResult>
- [MSG · GET /RecipientSelectionRules](endpoints/MSG.md) → MSG:map<RecipientSelectionRules.ListResult>

### refreshtokens

- [AUTHZ · GET /RefreshTokens](endpoints/AUTHZ.md) → AUTHZ:JwtResultBase

### requestmethods

- [WORK · GET /RequestMethods](endpoints/WORK.md) → WORK:map<RequestMethods.ListResult>

### requirements

- [TSTG · GET /Requirements/requirements](endpoints/TSTG.md) → TSTG:Requirements.ListResult[]
- [TSTG · GET /TaskStages/{id}/requirements](endpoints/TSTG.md) → TSTG:TaskStageRequirementResult

### resources

- [UI · GET /Resources](endpoints/UI.md) → UI:map<TaskViewTemplateResult>

### results

- [WORK · GET /Tasks/{taskID}/checkLists/{taskCheckListID}/results/v2](endpoints/WORK.md) → WORK:map<TaskCheckListResultV2Result>
- [WORK · GET /Tasks/{taskID}/checkLists/{taskCheckListID}/results](endpoints/WORK.md) → WORK:map<TaskCheckListResultResult>

### roles

- [ADM · GET /Roles/{id}](endpoints/ADM.md) → ADM:ResultsRolesGetResult
- [ADM · GET /Roles](endpoints/ADM.md) → ADM:map<ResultsRolesGetResult>
- [ADM · GET /UserTemplates/{id}/roles](endpoints/ADM.md) → ADM:IdNameResultOfShort[]
- [ADM · GET /Users/{id}/roles](endpoints/ADM.md) → ADM:map<IdNameResultOfShort>
- [COMMON · GET /Attachments/{attachmentID}/roles](endpoints/COMMON.md) → COMMON:map<str>

### route

- [WORK · GET /TaskTypes/{taskTypeID}/route](endpoints/WORK.md) → WORK:RouteResult

### scheduledtasks

- [PMP · GET /ScheduledTasks/count](endpoints/PMP.md) → PMP:map<ListCountResult[]>
- [PMP · GET /ScheduledTasks/v2/count](endpoints/PMP.md) → PMP:map<CountResult[]>
- [PMP · GET /ScheduledTasks](endpoints/PMP.md) → PMP:map<ScheduledTasks.ListResult>
- [PMP · HEAD /ScheduledTasks](endpoints/PMP.md)

### schedulerules

- [WSP · GET /ScheduleRules/holiday](endpoints/WSP.md) → WSP:map<datetime[]>
- [WSP · GET /ScheduleRules/{id}](endpoints/WSP.md) → WSP:ScheduleRuleDto
- [WSP · GET /ScheduleRules](endpoints/WSP.md) → WSP:map<ListResult>

### schedules

- [PA · GET /Users/onshift/schedules](endpoints/PA.md) → PA:map<WorkShiftScheduleDailyItemResult[]>
- [PMP · GET /Schedules/{id}](endpoints/PMP.md) → PMP:GetResult
- [PMP · GET /Schedules](endpoints/PMP.md) → PMP:map<GetResult>[]
- [WORK · GET /TaskTemplates/{id}/schedules](endpoints/WORK.md) → WORK:GetSchedulesResult[]

### senders

- [MSG · GET /MailBoxes/{mailBoxID}/senders/{senderID}](endpoints/MSG.md) → MSG:MailBoxSender.GetResult
- [MSG · GET /MailBoxes/{mailBoxID}/senders](endpoints/MSG.md) → MSG:map<MailBoxSender.ListResult>

### servicecontract

- [SC · GET /ServiceContract/{contractID}](endpoints/SC.md) → SC:ContractGetResult
- [SC · GET /ServiceContract](endpoints/SC.md) → SC:map<ContractListResult>
- [SC · HEAD /ServiceContract](endpoints/SC.md)

### sexes

- [PA · GET /Sexes](endpoints/PA.md) → PA:map<NameResult>

### skills

- [ADM · GET /Users/{userID}/skills](endpoints/ADM.md) → ADM:map<ResultsSkillsSkillResult>
- [ES · GET /AssetTemplates/{assetTemplateID}/skills](endpoints/ES.md) → ES:int[]
- [ES · GET /Assets/{assetID}/skills](endpoints/ES.md) → ES:map<ResultsAssetSkillsAssetSkillResult>
- [PA · GET /Skills/{id}](endpoints/PA.md) → PA:Skills.GetResult
- [PA · GET /Skills](endpoints/PA.md) → PA:map<Skills.ListResult>
- [WORK · GET /Tasks/{taskID}/skills](endpoints/WORK.md) → WORK:map<TaskSkillResult>

### stages

- [WORK · GET /Tasks/stages/next](endpoints/WORK.md) → WORK:map<ListStagesResult>
- [WORK · GET /Tasks/{taskID}/stages/next](endpoints/WORK.md) → WORK:map<ListStagesResult>
- [WORK · GET /Tasks/{taskID}/stages](endpoints/WORK.md) → WORK:ListStagingHistoryResult

### subsystemview

- [UI · GET /SubsystemView/{subsystemID}](endpoints/UI.md) → UI:SubsystemViewProjection[]
- [UI · GET /SubsystemView](endpoints/UI.md) → UI:SubsystemViewProjection[]

### systempermissionuitags

- [ADM · GET /SystemPermissionUiTags](endpoints/ADM.md) → ADM:map<ResultsPermissionsUiTagListResult[]>

### systemtags

- [COMMON · GET /SystemTags](endpoints/COMMON.md) → COMMON:IdNameResult<Int16>[]

### tags

- [ADM · GET /Users/{userID}/tags](endpoints/ADM.md) → ADM:str[]
- [COMMON · GET /Tags](endpoints/COMMON.md) → COMMON:str[]
- [ES · GET /Assets/{assetID}/tags](endpoints/ES.md) → ES:str[]
- [WORK · GET /Tasks/{taskID}/tags](endpoints/WORK.md) → WORK:str[]

### taskactualities

- [WORK · GET /TaskActualities/{id}](endpoints/WORK.md) → WORK:TaskActualities.ListResult
- [WORK · GET /TaskActualities](endpoints/WORK.md) → WORK:map<TaskActualities.ListResult>

### taskattributes

- [WORK · GET /TaskAttributes](endpoints/WORK.md) → WORK:TaskAttributesResult[]

### taskconversations

- [WORK · GET /TaskConversations](endpoints/WORK.md) → WORK:TaskMessageLast[]
- [WORK · HEAD /TaskConversations](endpoints/WORK.md)

### taskfilter

- [WORK · GET /TaskFilter](endpoints/WORK.md) → WORK:FilterListItemProjection[]

### tasklistqueries

- [ADM · GET /Users/this/taskListQueries](endpoints/ADM.md) → ADM:map<ResultsUsersTaskListQueryResult>
- [ADM · GET /Users/{id}/taskListQueries](endpoints/ADM.md) → ADM:map<ResultsUsersTaskListQueryResult>
- [WORK · GET /TaskListQueries/{id}](endpoints/WORK.md) → WORK:map<TaskListQueryResult>
- [WORK · GET /TaskListQueries](endpoints/WORK.md) → WORK:map<TaskListQueryResult>

### taskorderby

- [WORK · GET /TaskOrderBy](endpoints/WORK.md) → WORK:map<TaskOrderBy.ListResult>

### taskratings

- [PA · GET /Technicians/{userID}/taskRatings](endpoints/PA.md) → PA:TechnicianRatingResult[]

### tasks

- [EXPORT · GET /Tasks/noData](endpoints/EXPORT.md)
- [EXPORT · GET /Tasks/v2.0](endpoints/EXPORT.md)
- [EXPORT · GET /Tasks](endpoints/EXPORT.md)
- [WORK · GET /Tasks/changeTypes](endpoints/WORK.md) → WORK:ChangeTypeResult[]
- [WORK · GET /Tasks/count](endpoints/WORK.md) → WORK:map<ListCountResult>
- [WORK · GET /Tasks/short](endpoints/WORK.md) → WORK:map<ListShortResult>
- [WORK · GET /Tasks/{taskID}/checkCompanyCodeUsed](endpoints/WORK.md) → WORK:bool
- [WORK · GET /Tasks/{taskID}/meta](endpoints/WORK.md) → WORK:TaskTypeFormMetadataResult
- [WORK · GET /Tasks/{taskID}](endpoints/WORK.md) → WORK:DetailedInfoResult
- [WORK · GET /Tasks](endpoints/WORK.md) → WORK:map<Tasks.ListResult>
- [WORK · HEAD /Tasks](endpoints/WORK.md)

### tasksbyassets

- [REPORT · GET /TasksByAssets](endpoints/REPORT.md) → REPORT:TaskListGroupByAssigneesResult[]

### tasksbyassignees

- [REPORT · GET /TasksByAssignees](endpoints/REPORT.md) → REPORT:TaskListGroupByAssigneesResult[]

### tasksbycompanies

- [REPORT · GET /TasksByCompanies](endpoints/REPORT.md) → REPORT:TaskListGroupByCompaniesResult[]

### tasksbystages

- [REPORT · GET /TasksByStages](endpoints/REPORT.md) → REPORT:TaskListGroupByStagesResult[]

### tasksbyworktypes

- [REPORT · GET /TasksByWorkTypes](endpoints/REPORT.md) → REPORT:TaskListGroupByWorkTypesResult[]

### taskschedules

- [PA · GET /Technicians/taskSchedules](endpoints/PA.md) → PA:ScheduleTaskResult[]

### taskstagelinks

- [TSTG · GET /TaskStageLinks](endpoints/TSTG.md) → TSTG:TaskStageLinks.ListResult[]

### taskstages

- [TSTG · GET /TaskStages/{id}](endpoints/TSTG.md) → TSTG:TaskStages.GetResult
- [TSTG · GET /TaskStages](endpoints/TSTG.md) → TSTG:TaskStages.ListResult[]
- [TSTG · HEAD /TaskStages](endpoints/TSTG.md)

### taskstatuses

- [WORK · GET /TaskStatuses/{id}](endpoints/WORK.md) → WORK:TaskStatuses.ListResult
- [WORK · GET /TaskStatuses](endpoints/WORK.md) → WORK:map<TaskStatuses.ListResult>

### tasktemplates

- [PROXY · GET /TaskTemplates/{codeDynamicPart}](endpoints/PROXY.md)
- [WORK · GET /TaskTemplates/download](endpoints/WORK.md)
- [WORK · GET /TaskTemplates/{id}/download](endpoints/WORK.md)
- [WORK · GET /TaskTemplates/{id}/public](endpoints/WORK.md) → WORK:GetPublicResult
- [WORK · GET /TaskTemplates/{id}](endpoints/WORK.md) → WORK:TaskTemplates.GetResult
- [WORK · GET /TaskTemplates](endpoints/WORK.md) → WORK:map<TaskTemplates.ListResult>
- [WORK · HEAD /TaskTemplates](endpoints/WORK.md)

### tasktypes

- [UI · GET /LayoutTemplates/{id}/taskTypes](endpoints/UI.md) → UI:LayoutTaskTypeDto[]
- [WORK · GET /TaskTypes/{id}](endpoints/WORK.md) → WORK:TaskTypes.ListResult
- [WORK · GET /TaskTypes](endpoints/WORK.md) → WORK:map<TaskTypes.ListResult>
- [WORK · GET /WorkTypes/{id}/taskTypes](endpoints/WORK.md) → WORK:IdNameEntity<Byte>[]

### taskviewtemplate

- [UI · GET /TaskViewTemplate](endpoints/UI.md) → UI:map<TaskViewTemplateResult>

### technicians

- [WORK · GET /Tasks/{taskID}/completedWorks/technicians](endpoints/WORK.md) → WORK:CompletedWorkTechnicianResult
- [WORK · GET /Tasks/{taskID}/completedWorks/{completedWorkID}/technicians](endpoints/WORK.md) → WORK:CompletedWorkTechnicianResult

### templatequickresponse

- [WORK · GET /TemplateQuickResponse/{id}](endpoints/WORK.md) → WORK:TemplateQuickResponse.GetResult
- [WORK · GET /TemplateQuickResponse](endpoints/WORK.md) → WORK:map<TemplateQuickResponse.ListResult>

### templates

- [ADM · GET /Tenants/templates](endpoints/ADM.md) → ADM:InterfacesEntitiesITenantEntity[]

### tenantcreationrequests

- [ADM · GET /TenantCreationRequests/{id}](endpoints/ADM.md) → ADM:ResultsTenantCreationRequestsGetResult

### tenantmembers

- [ADM · GET /TenantMembers/anonymousUser](endpoints/ADM.md) → ADM:ResultsTenantMembersListResult
- [ADM · GET /TenantMembers/apiUser](endpoints/ADM.md) → ADM:ResultsTenantMembersListResult
- [ADM · GET /TenantMembers/this](endpoints/ADM.md) → ADM:ResultsTenantMembersGetResult
- [ADM · GET /TenantMembers/{tenantMemberID}](endpoints/ADM.md) → ADM:ResultsTenantMembersGetResult
- [ADM · GET /TenantMembers](endpoints/ADM.md) → ADM:map<ResultsTenantMembersListResult>

### tenants

- [ADM · GET /Tenants/this/featureFlags](endpoints/ADM.md) → ADM:str[]
- [ADM · GET /Tenants/this/meta](endpoints/ADM.md)
- [ADM · GET /Tenants/this](endpoints/ADM.md) → ADM:ResultsTenantsGetResult
- [ADM · GET /Tenants](endpoints/ADM.md) → ADM:ResultsTenantsListResult[]

### tenantsettings

- [ADM · GET /TenantSettings/plateUrl](endpoints/ADM.md) → ADM:str
- [ADM · GET /TenantSettings](endpoints/ADM.md) → ADM:ResultsTenantSettingsGetResult
- [PA · GET /TenantSettings](endpoints/PA.md) → PA:TenantSettings.GetResult

### timezones

- [COMMON · GET /Timezones/info](endpoints/COMMON.md) → COMMON:TimezoneGetResult
- [COMMON · GET /Timezones](endpoints/COMMON.md) → COMMON:map<Timezones.ListResult>

### triggers

- [MSG · GET /Triggers/{id}](endpoints/MSG.md) → MSG:map<Triggers.GetResult>
- [MSG · GET /Triggers](endpoints/MSG.md) → MSG:map<Triggers.ListResult>

### usergroups

- [PA · GET /UserGroups](endpoints/PA.md) → PA:map<UserGroupResult>

### userorderby

- [ADM · GET /UserOrderBy](endpoints/ADM.md) → ADM:map<ResultsUserOrderByListResult>

### users

- [ADM · GET /Users/geolocation](endpoints/ADM.md) → ADM:ResultsCoordinateAccuracyUserGeolocationSettings[]
- [ADM · GET /Users/profile](endpoints/ADM.md) → ADM:ResultsUsersUserProfileResult
- [ADM · GET /Users/relevance](endpoints/ADM.md) → ADM:map<ResultsUsersUserResult>
- [ADM · GET /Users/short](endpoints/ADM.md) → ADM:map<ResultsUsersUserShortResult>
- [ADM · GET /Users/this/geolocation](endpoints/ADM.md) → ADM:ResultsCoordinateAccuracyUserGeolocationSettings
- [ADM · GET /Users/this/profile](endpoints/ADM.md) → ADM:ResultsUsersUserProfileResult
- [ADM · GET /Users/{id}/profile](endpoints/ADM.md) → ADM:ResultsUsersUserProfileResult
- [ADM · GET /Users/{id}](endpoints/ADM.md) → ADM:ResultsUsersDetailedInfoResult
- [ADM · GET /Users](endpoints/ADM.md) → ADM:map<ResultsUsersUserResult>
- [ADM · HEAD /Users](endpoints/ADM.md)
- [EXPORT · GET /Users](endpoints/EXPORT.md)
- [UI · GET /UserViews/Users/{id}](endpoints/UI.md) → UI:TaskViewProjection[]
- [WH · GET /Warehouses/{id}/users](endpoints/WH.md) → WH:WarehouseUserListResult[]

### usertemplates

- [ADM · GET /UserTemplates/{id}](endpoints/ADM.md) → ADM:ResultsUserTemplatesGetResult
- [ADM · GET /UserTemplates](endpoints/ADM.md) → ADM:map<ResultsUserTemplatesListResult>

### userwarehouses

- [WH · GET /UserWarehouses/{id}](endpoints/WH.md) → WH:UserWarehouseListResult[]

### variables

- [ADM · GET /Tenants/this/variables](endpoints/ADM.md) → ADM:map<ResultsTenantVariablesListResult>

### warehouses

- [ADM · GET /Users/{id}/warehouses](endpoints/ADM.md) → ADM:map<IdNameErpIDResultOfShort>
- [WH · GET /Warehouses/V2](endpoints/WH.md) → WH:map<Warehouses.ListResult>
- [WH · GET /Warehouses/short](endpoints/WH.md) → WH:map<ListShortResult>
- [WH · GET /Warehouses/{id}](endpoints/WH.md) → WH:GetResult
- [WH · GET /Warehouses](endpoints/WH.md) → WH:map<ListShortResult>
- [WH · HEAD /Warehouses](endpoints/WH.md) → WH:map<Warehouses.ListResult>

### watchlists

- [WORK · GET /Tasks/{taskID}/watchLists](endpoints/WORK.md) → WORK:TaskWatchLists.ListResult[]

### webhooks

- [MSG · GET /Webhooks/{id}](endpoints/MSG.md) → MSG:Webhook.GetResult
- [MSG · GET /Webhooks](endpoints/MSG.md) → MSG:map<Webhook.ListResult>

### workingtime

- [REPORT · GET /WorkingTime](endpoints/REPORT.md) → REPORT:TaskListGroupByAssigneesResult[]

### workschedules

- [PA · GET /Technicians/{userID}/workSchedules](endpoints/PA.md) → PA:WorkScheduleResult[]
- [WSP · GET /WorkSchedules/daily](endpoints/WSP.md) → WSP:map<WorkScheduleDailyItemResult[]>
- [WSP · GET /WorkSchedules](endpoints/WSP.md) → WSP:map<WorkScheduleDailyItemResult>

### worktypes

- [ES · GET /AssetTemplates/{assetTemplateID}/workTypes](endpoints/ES.md) → ES:int[]
- [ES · GET /AssetTypes/{id}/workTypes](endpoints/ES.md) → ES:IdNameEntityOfShort[]
- [ES · GET /Assets/{assetID}/workTypes](endpoints/ES.md) → ES:map<ResultsAssetsAssetWorkTypeResult>
- [PA · GET /Users/{userID}/workTypes](endpoints/PA.md) → PA:map<WorkTypesListResult>
- [WORK · GET /TaskTypes/{id}/workTypes](endpoints/WORK.md) → WORK:IdNameEntity<Int16>[]
- [WORK · GET /WorkTypes/{id}](endpoints/WORK.md) → WORK:WorkTypes.GetResult
- [WORK · GET /WorkTypes/{parentWorkTypeID}/workTypes/all](endpoints/WORK.md) → WORK:map<WorkTypes.ListResult>
- [WORK · GET /WorkTypes/{parentWorkTypeID}/workTypes](endpoints/WORK.md) → WORK:map<WorkTypes.ListResult>
- [WORK · GET /WorkTypes](endpoints/WORK.md) → WORK:map<WorkTypes.ListResult>

