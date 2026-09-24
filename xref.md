# HubEx API — кросс-индекс ресурсов

> **Что здесь:** где ресурс дёргается во ВСЕХ сервисах (от ресурса) и что можно у сущности (от сущности). Указатели ведут в `endpoints/<SVC>.md`; типы — `schemas/<SVC>.md`.
## От сущности

### Assets (ES)

- assets [GET]
- assignments [GET]
- attachments [GET]
- attributes [GET]
- avatar [DELETE, PUT]
- checklists [DELETE, GET, POST]
- contacts [DELETE, GET, POST]
- districts [GET]
- locations [GET]
- skills [GET]
- tags [GET]
- worktypes [GET]

### AssetSchemas (ES)

- image [DELETE, GET, POST]
- points [DELETE, GET, POST]

### AssetTemplates (ES)

- attachments [GET]
- attributes [GET]
- avatar [DELETE, PUT]
- districts [GET]
- skills [GET]
- worktypes [GET]

### AssetTypes (ES)

- worktypes [DELETE, GET, POST]

### Attachments (COMMON)

- roles [GET]

### CheckLists (WORK)

- items [GET]

### Companies (ES)

- attachment [GET]
- attachments [GET]
- attributes [GET, POST]
- bankaccounts [DELETE, GET, POST, PUT]
- contacts [DELETE, GET, POST]
- locations [GET]

### DeadlineRules (SLA)

- attributes [DELETE, GET, POST]

### Issues (WH)

- items [DELETE, GET]

### LayoutTemplates (UI)

- attributes [GET]
- components [GET]
- tasktypes [DELETE, GET, PUT]

### MailBoxes (MSG)

- errors [GET]
- senders [DELETE, GET]

### Materials (WH)

- attachment [DELETE, GET]
- attachments [DELETE, GET, POST]
- barcodes [DELETE, GET]

### OrgUnits (ES)

- orgunits [GET]

### Receipts (WH)

- items [DELETE, GET]

### Roles (ADM)

- applications [GET]
- attachments [GET]
- packages [DELETE, GET, POST, PUT]
- permissionsapi [GET]
- permissionsext [GET]
- permissionsui [GET]

### Schedules (PMP)

- appointments [DELETE, GET, POST]

### ServiceContract (SC)

- assets [DELETE, GET, POST, PUT]
- attachment [GET]
- attachments [DELETE, GET, POST]
- attributes [GET]
- contacts [DELETE, GET, POST, PUT]

### Tasks (WORK)

- assignments [GET]
- attachment [GET]
- attachments [GET]
- attributes [GET]
- changes [GET]
- checklists [DELETE, GET, POST, PUT]
- completedworks [DELETE, GET, POST, PUT]
- contacts [DELETE, GET]
- conversation [POST]
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

- assignment [GET, POST]
- excludedassets [DELETE, GET]
- schedules [GET, POST, PUT]

### TaskTypes (WORK)

- districts [GET]
- route [GET]
- worktypes [DELETE, GET, POST]

### Technicians (PA)

- rating [GET]
- taskratings [GET]
- workschedules [GET]

### Transfers (WH)

- items [DELETE, GET]

### Triggers (MSG)

- criticalities [GET]

### Users (ADM)

- assetassignments [GET]
- assetlistqueries [GET]
- attributes [DELETE, GET, POST, PUT]
- avatar [DELETE, PUT]
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

- worktypes [DELETE, GET, POST]

### UserTemplates (ADM)

- districts [GET]
- roles [GET]

### UserViews (UI)

- applications [GET, POST, PUT]

### Warehouses (WH)

- users [DELETE, GET, POST]

### WorkTypes (WORK)

- checklists [DELETE, GET, POST]
- tasktypes [DELETE, GET, POST]
- worktypes [GET]


## От ресурса

### accesstokens

- [AUTHZ · POST /AccessTokens](endpoints/AUTHZ.md)

### accounts

- [AUTH · GET /Accounts](endpoints/AUTH.md) → AUTH:GetResult
- [AUTH · HEAD /Accounts](endpoints/AUTH.md)
- [AUTH · POST /Accounts/logout](endpoints/AUTH.md)
- [AUTH · POST /Accounts/register](endpoints/AUTH.md)
- [AUTHN · POST /Accounts/login/sso](endpoints/AUTHN.md)
- [AUTHN · POST /Accounts/login](endpoints/AUTHN.md)
- [AUTHN · POST /Accounts/realm](endpoints/AUTHN.md)
- [AUTHN · POST /Accounts/smsLogin](endpoints/AUTHN.md)
- [AUTHN · POST /Accounts/smsSend](endpoints/AUTHN.md)
- [AUTHZ · POST /Accounts/authorize](endpoints/AUTHZ.md)

### action

- [TSTG · GET /Action](endpoints/TSTG.md) → TSTG:map<ActionsResult>

### applications

- [ADM · GET /Roles/{roleID}/applications](endpoints/ADM.md) → ADM:map<RRAListResult>
- [AUTH · DELETE /Accounts/this/applications](endpoints/AUTH.md)
- [AUTH · GET /Accounts/this/applications](endpoints/AUTH.md) → AUTH:ApplicationListResult[]
- [AUTH · PUT /Accounts/this/applications](endpoints/AUTH.md)
- [COMMON · GET /Applications](endpoints/COMMON.md) → COMMON:map<ApplicationResult>
- [UI · GET /UserViews/Users/{userID}/Applications/{applicationID}/{code}](endpoints/UI.md) → UI:ProjectionsUITaskViewProjection
- [UI · POST /UserViews/Users/{userID}/Applications/{applicationID}/{code}](endpoints/UI.md)
- [UI · PUT /UserViews/Users/{userID}/Applications/{applicationID}/{code}/reset](endpoints/UI.md)
- [UI · PUT /UserViews/Users/{userID}/Applications/{applicationID}/{code}](endpoints/UI.md)
- [UI · PUT /Views/Applications/{applicationID}/{code}/reset](endpoints/UI.md)
- [UI · PUT /Views/Applications/{applicationID}/{code}](endpoints/UI.md)

### appointments

- [PA · GET /Technicians/{userID}/workSchedules/appointments](endpoints/PA.md) → PA:AppointmentResult[]
- [PMP · DELETE /Schedules/appointments/assign](endpoints/PMP.md)
- [PMP · GET /ScheduledTasks/appointments](endpoints/PMP.md) → PMP:AppointmentResultOfRSTAssetAssignResult[]
- [PMP · GET /ScheduledTasks/v2/appointments](endpoints/PMP.md) → PMP:AppointmentResultOfAssetAssignResultV2[]
- [PMP · GET /Schedules/appointments/assign](endpoints/PMP.md) → PMP:map<ScheduleAppointmentAssignListResult>
- [PMP · GET /Schedules/{scheduleID}/appointments/assign](endpoints/PMP.md) → PMP:map<ScheduleAppointmentAssignListResult>
- [PMP · GET /Schedules/{scheduleID}/appointments](endpoints/PMP.md) → PMP:RSAListResult[]
- [PMP · HEAD /ScheduledTasks/appointments](endpoints/PMP.md)
- [PMP · POST /Schedules/appointments/assign](endpoints/PMP.md)
- [WORK · POST /TaskTemplates/{taskTemplateId}/schedules/{scheduleId}/appointments](endpoints/WORK.md)

### articles

- [NEWS · GET /Articles](endpoints/NEWS.md) → NEWS:map<ResultsArticlesListResult>
- [NEWS · PUT /Articles](endpoints/NEWS.md)

### asclist

- [ES · GET /AssetSchemas/ascList/{assetID}](endpoints/ES.md) → ES:map<ResultsAssetSchemaSchemaBase>

### asset

- [ES · GET /AssetSchemas/asset/{assetID}](endpoints/ES.md) → ES:ResultsAssetSchemaSchema
- [ES · POST /AssetSchemas/asset/{assetId}](endpoints/ES.md)
- [ES · PUT /AssetSchemas/asset/{assetId}](endpoints/ES.md)
- [PMP · DELETE /Schedules/{scheduleID}/appointments/{appointmentID}/asset/{assetID}](endpoints/PMP.md)
- [PMP · POST /Schedules/{scheduleID}/appointments/{appointmentID}/asset/{assetID}/assign/{userID}](endpoints/PMP.md)

### assetassignments

- [ADM · GET /Users/{userID}/assetAssignments](endpoints/ADM.md) → ADM:AssetAssignmentResult[]
- [PA · DELETE /AssetAssignments](endpoints/PA.md)
- [PA · GET /AssetAssignments](endpoints/PA.md) → PA:RAAListResult[]
- [PA · POST /AssetAssignments](endpoints/PA.md)

### assetattachments

- [ES · DELETE /AssetAttachments](endpoints/ES.md)
- [ES · POST /AssetAttachments/upload/fromBody](endpoints/ES.md)
- [ES · POST /AssetAttachments/upload/fromForm](endpoints/ES.md)
- [ES · POST /AssetAttachments/upload](endpoints/ES.md)
- [ES · POST /AssetAttachments](endpoints/ES.md)

### assetattributes

- [ES · DELETE /AssetAttributes](endpoints/ES.md)
- [ES · POST /AssetAttributes/v2](endpoints/ES.md)
- [ES · POST /AssetAttributes](endpoints/ES.md)
- [ES · PUT /AssetAttributes/v2](endpoints/ES.md)

### assetclasses

- [ES · DELETE /AssetClasses/{id}](endpoints/ES.md)
- [ES · DELETE /AssetClasses](endpoints/ES.md)
- [ES · GET /AssetClasses/{id}](endpoints/ES.md) → ES:ResultsAssetClassesAssetClassGetResult
- [ES · GET /AssetClasses](endpoints/ES.md) → ES:map<ResultsAssetClassesAssetClassListResult>
- [ES · POST /AssetClasses](endpoints/ES.md)
- [ES · PUT /AssetClasses](endpoints/ES.md)

### assetdistricts

- [ES · DELETE /AssetDistricts](endpoints/ES.md)
- [ES · POST /AssetDistricts](endpoints/ES.md)

### assetfilter

- [ES · GET /AssetFilter](endpoints/ES.md) → ES:ProjectionsCOMMONFilterListItemProjection[]
- [ES · PUT /AssetFilter](endpoints/ES.md)

### assetlistqueries

- [ADM · GET /Users/this/assetListQueries](endpoints/ADM.md) → ADM:map<AssetListQueryResult>
- [ADM · GET /Users/{id}/assetListQueries](endpoints/ADM.md) → ADM:map<AssetListQueryResult>
- [ES · DELETE /AssetListQueries/remove](endpoints/ES.md)
- [ES · DELETE /AssetListQueries/{id}/remove](endpoints/ES.md)
- [ES · DELETE /AssetListQueries/{id}](endpoints/ES.md)
- [ES · DELETE /AssetListQueries](endpoints/ES.md)
- [ES · GET /AssetListQueries/{id}](endpoints/ES.md) → ES:ResultsAssetListQueriesAssetListQueryGetResult
- [ES · GET /AssetListQueries](endpoints/ES.md) → ES:map<ResultsAssetListQueriesAssetListQueryResult>
- [ES · POST /AssetListQueries](endpoints/ES.md)
- [ES · PUT /AssetListQueries](endpoints/ES.md)

### assetlocations

- [ES · DELETE /AssetLocations](endpoints/ES.md)
- [ES · GET /AssetLocations](endpoints/ES.md) → ES:map<ResultsAssetsAssetLocationResult>
- [ES · POST /AssetLocations](endpoints/ES.md)
- [ES · PUT /AssetLocations](endpoints/ES.md)

### assetmaintenance

- [REPORT · GET /AssetMaintenance/planned](endpoints/REPORT.md) → REPORT:ResultsAssetMaintenancePlannedMaintenanceResult[]

### assets

- [ES · DELETE /Assets/full](endpoints/ES.md)
- [ES · DELETE /Assets/{assetID}/full](endpoints/ES.md)
- [ES · DELETE /Assets/{assetID}](endpoints/ES.md)
- [ES · DELETE /Assets](endpoints/ES.md)
- [ES · GET /Assets/root](endpoints/ES.md) → ES:map<ResultsAssetsAssetExtResult>
- [ES · GET /Assets/{assetID}](endpoints/ES.md) → ES:ResultsAssetsAssetDetailedInfoResult
- [ES · GET /Assets/{parentAssetID}/assets/all](endpoints/ES.md) → ES:map<ResultsAssetsAssetExtResult>
- [ES · GET /Assets/{parentAssetID}/assets](endpoints/ES.md) → ES:map<ResultsAssetsAssetExtResult>
- [ES · GET /Assets](endpoints/ES.md) → ES:map<ResultsAssetsAssetExtResult>
- [ES · HEAD /Assets](endpoints/ES.md)
- [ES · POST /Assets](endpoints/ES.md)
- [ES · PUT /Assets/restore](endpoints/ES.md)
- [ES · PUT /Assets/{assetID}/publish](endpoints/ES.md)
- [ES · PUT /Assets/{assetID}/unpublish](endpoints/ES.md)
- [ES · PUT /Assets/{assetID}](endpoints/ES.md)
- [ES · PUT /Assets](endpoints/ES.md)
- [EXPORT · GET /Assets](endpoints/EXPORT.md)
- [IMPORT · POST /Assets](endpoints/IMPORT.md)
- [SC · DELETE /ServiceContract/{contractID}/assets/{assetID}](endpoints/SC.md)
- [SC · DELETE /ServiceContract/{contractID}/assets](endpoints/SC.md)
- [SC · GET /ServiceContract/{contractID}/assets](endpoints/SC.md) → SC:map<AssetResultBase>
- [SC · POST /ServiceContract/{contractID}/assets](endpoints/SC.md)
- [SC · PUT /ServiceContract/{contractID}/assets/{assetID}](endpoints/SC.md)

### assetschemas

- [ES · DELETE /AssetSchemas/{schemaId}](endpoints/ES.md)
- [ES · GET /AssetSchemas/list](endpoints/ES.md) → ES:map<ResultsAssetSchemaSchemaBase>
- [ES · GET /AssetSchemas/{schemaId}](endpoints/ES.md) → ES:ResultsAssetSchemaSchema
- [ES · POST /AssetSchemas/{schemaId}/bind](endpoints/ES.md)
- [ES · PUT /AssetSchemas/{schemaId}/unbind](endpoints/ES.md)

### assetsearchsettings

- [ES · DELETE /AssetSearchSettings/tenant](endpoints/ES.md)
- [ES · GET /AssetSearchSettings](endpoints/ES.md) → ES:ProjectionsESAssetSearchFieldSettingsProjection[]
- [ES · POST /AssetSearchSettings/tenant](endpoints/ES.md)

### assetskills

- [ES · DELETE /AssetSkills](endpoints/ES.md)
- [ES · POST /AssetSkills](endpoints/ES.md)

### assettags

- [ES · DELETE /AssetTags](endpoints/ES.md)
- [ES · POST /AssetTags](endpoints/ES.md)

### assettemplateattachments

- [ES · DELETE /AssetTemplateAttachments](endpoints/ES.md)
- [ES · POST /AssetTemplateAttachments/upload/fromBody](endpoints/ES.md)
- [ES · POST /AssetTemplateAttachments/upload/fromForm](endpoints/ES.md)
- [ES · POST /AssetTemplateAttachments/upload](endpoints/ES.md)
- [ES · POST /AssetTemplateAttachments](endpoints/ES.md)

### assettemplateattributes

- [ES · POST /AssetTemplateAttributes](endpoints/ES.md)

### assettemplatedistricts

- [ES · DELETE /AssetTemplateDistricts/{id}](endpoints/ES.md)
- [ES · DELETE /AssetTemplateDistricts](endpoints/ES.md)
- [ES · POST /AssetTemplateDistricts](endpoints/ES.md)

### assettemplates

- [ES · DELETE /AssetTemplates/{id}](endpoints/ES.md)
- [ES · DELETE /AssetTemplates](endpoints/ES.md)
- [ES · GET /AssetTemplates/{id}](endpoints/ES.md) → ES:ResultsAssetTemplatesGetResult
- [ES · GET /AssetTemplates](endpoints/ES.md) → ES:map<ResultsAssetTemplatesListResult>
- [ES · POST /AssetTemplates](endpoints/ES.md)
- [ES · PUT /AssetTemplates](endpoints/ES.md)

### assettemplateskills

- [ES · DELETE /AssetTemplateSkills/{id}](endpoints/ES.md)
- [ES · DELETE /AssetTemplateSkills](endpoints/ES.md)
- [ES · POST /AssetTemplateSkills](endpoints/ES.md)

### assettemplateworktypes

- [ES · DELETE /AssetTemplateWorkTypes/{id}](endpoints/ES.md)
- [ES · DELETE /AssetTemplateWorkTypes](endpoints/ES.md)
- [ES · POST /AssetTemplateWorkTypes](endpoints/ES.md)

### assettypes

- [ES · DELETE /AssetTypes/{id}](endpoints/ES.md)
- [ES · DELETE /AssetTypes](endpoints/ES.md)
- [ES · GET /AssetTypes/{id}](endpoints/ES.md) → ES:ResultsAssetTypesGetResult
- [ES · GET /AssetTypes](endpoints/ES.md) → ES:map<ResultsAssetTypesGetResult>
- [ES · POST /AssetTypes](endpoints/ES.md)
- [ES · PUT /AssetTypes](endpoints/ES.md)

### assetworktypes

- [ES · DELETE /AssetWorkTypes](endpoints/ES.md)
- [ES · POST /AssetWorkTypes](endpoints/ES.md)

### assigneeselectionrules

- [TSTG · DELETE /AssigneeSelectionRules/{id}](endpoints/TSTG.md)
- [TSTG · DELETE /AssigneeSelectionRules](endpoints/TSTG.md)
- [TSTG · GET /AssigneeSelectionRules/{id}](endpoints/TSTG.md) → TSTG:RASRGetResult
- [TSTG · GET /AssigneeSelectionRules](endpoints/TSTG.md) → TSTG:map<RASRListResult>
- [TSTG · POST /AssigneeSelectionRules](endpoints/TSTG.md)
- [TSTG · PUT /AssigneeSelectionRules](endpoints/TSTG.md)

### assignment

- [WORK · GET /TaskTemplates/{id}/assignment](endpoints/WORK.md) → WORK:TaskTemplateAssignmentDetailsProjection
- [WORK · POST /TaskTemplates/{id}/assignment](endpoints/WORK.md)

### assignments

- [ES · GET /Assets/{assetID}/assignments](endpoints/ES.md) → ES:ResultsAssetsAssetAssignmentResult[]
- [WORK · GET /Tasks/{taskID}/assignments](endpoints/WORK.md) → WORK:ListAssignmentHistoryResult

### attach

- [ES · POST /AssetSchemas/{schemaId}/image/attach/{attachmentId}](endpoints/ES.md)

### attachment

- [ES · GET /Companies/{companyID}/attachment/{attachmentID}](endpoints/ES.md) → ES:ResultsCommonGetAttachmentResult
- [SC · GET /ServiceContract/{contractID}/attachment/{attachmentID}](endpoints/SC.md) → SC:RAAttachmentResult
- [WH · DELETE /Materials/{materialID}/attachment/{attachmentID}](endpoints/WH.md)
- [WH · GET /Materials/{materialID}/attachment/{attachmentID}](endpoints/WH.md) → WH:ResultsMaterialAttachmentsMaterialAttachmentResult
- [WORK · DELETE /Tasks/{taskID}/completedWorks/report/attachment/{attachmentID}](endpoints/WORK.md)
- [WORK · GET /Tasks/{taskID}/attachment/{attachmentID}](endpoints/WORK.md) → WORK:GetAttachmentResult
- [WORK · GET /Tasks/{taskID}/completedWorks/report/attachment](endpoints/WORK.md)
- [WORK · POST /Tasks/completedWorks/report/attachment/upload/fromBody](endpoints/WORK.md)
- [WORK · POST /Tasks/completedWorks/report/attachment/upload/fromForm](endpoints/WORK.md)
- [WORK · POST /Tasks/{taskID}/completedWorks/report/attachment/v2/{attachmentID}](endpoints/WORK.md)
- [WORK · POST /Tasks/{taskID}/completedWorks/report/attachment/{attachmentID}](endpoints/WORK.md)

### attachments

- [ADM · GET /Roles/{roleID}/attachments](endpoints/ADM.md) → ADM:RCAttachmentResult[]
- [COMMON · DELETE /Attachments/{attachmentID}](endpoints/COMMON.md)
- [COMMON · DELETE /Attachments](endpoints/COMMON.md)
- [COMMON · GET /Attachments/downloadLink](endpoints/COMMON.md) → COMMON:FSRDownloadLinkResult
- [COMMON · GET /Attachments/{attachmentID}/this](endpoints/COMMON.md) → COMMON:RAGetResult
- [COMMON · GET /Attachments/{attachmentID}](endpoints/COMMON.md)
- [COMMON · GET /Attachments](endpoints/COMMON.md) → COMMON:map<RAListResult>
- [COMMON · POST /Attachments/upload/fromBody](endpoints/COMMON.md)
- [COMMON · POST /Attachments/upload/fromForm](endpoints/COMMON.md)
- [COMMON · POST /Attachments/v2/upload/fromForm](endpoints/COMMON.md)
- [COMMON · POST /Attachments/{attachmentID}/publish](endpoints/COMMON.md)
- [COMMON · POST /Attachments/{attachmentID}/unpublish](endpoints/COMMON.md)
- [ES · GET /AssetTemplates/{assetTemplateID}/attachments/{attachmentID}](endpoints/ES.md)
- [ES · GET /AssetTemplates/{assetTemplateID}/attachments](endpoints/ES.md) → ES:map<ResultsCommonListAttachmentResult>
- [ES · GET /Assets/{assetID}/attachments/{attachmentID}](endpoints/ES.md)
- [ES · GET /Assets/{assetID}/attachments](endpoints/ES.md) → ES:map<ResultsCommonListAttachmentResult>
- [ES · GET /Companies/{companyID}/attachments/{attachmentID}](endpoints/ES.md)
- [ES · GET /Companies/{companyID}/attachments](endpoints/ES.md) → ES:map<ResultsCommonListAttachmentResult>
- [SC · DELETE /ServiceContract/{contractID}/attachments](endpoints/SC.md)
- [SC · GET /ServiceContract/{contractID}/attachments/{attachmentID}](endpoints/SC.md) → SC:ANCRAttachmentResult
- [SC · GET /ServiceContract/{contractID}/attachments](endpoints/SC.md) → SC:map<AttachmentListResult>
- [SC · POST /ServiceContract/{contractID}/attachments/upload/fromBody](endpoints/SC.md)
- [SC · POST /ServiceContract/{contractID}/attachments/upload/fromForm](endpoints/SC.md)
- [SC · POST /ServiceContract/{contractID}/attachments](endpoints/SC.md)
- [SC · POST /ServiceContract/{contractID}/v2/attachments/upload/fromForm](endpoints/SC.md)
- [WH · DELETE /Materials/{materialID}/attachments](endpoints/WH.md)
- [WH · GET /Materials/{materialID}/attachments/{attachmentID}](endpoints/WH.md)
- [WH · GET /Materials/{materialID}/attachments](endpoints/WH.md) → WH:map<ResultsMaterialAttachmentsMaterialAttachmentListResult>
- [WH · POST /Materials/{materialID}/attachments/upload/fromBody](endpoints/WH.md)
- [WH · POST /Materials/{materialID}/attachments/upload/fromForm](endpoints/WH.md)
- [WH · POST /Materials/{materialID}/attachments](endpoints/WH.md)
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

### attributelistofvalues

- [COMMON · POST /AttributeListOfValues](endpoints/COMMON.md)

### attributes

- [ADM · DELETE /Users/attributes](endpoints/ADM.md)
- [ADM · DELETE /Users/{userID}/attributes](endpoints/ADM.md)
- [ADM · GET /RoleTaskPropertiesAccess/attributes](endpoints/ADM.md) → ADM:RoleTaskAttributeSettings[]
- [ADM · GET /Users/attributes](endpoints/ADM.md) → ADM:UserAttributesResult[]
- [ADM · GET /Users/{userID}/attributes](endpoints/ADM.md) → ADM:UserAttributesResult[]
- [ADM · POST /RoleTaskPropertiesAccess/attributes](endpoints/ADM.md)
- [ADM · POST /Users/attributes](endpoints/ADM.md)
- [ADM · POST /Users/{userID}/attributes](endpoints/ADM.md)
- [ADM · PUT /RoleTaskPropertiesAccess/attributes](endpoints/ADM.md)
- [ADM · PUT /Users/attributes](endpoints/ADM.md)
- [ADM · PUT /Users/{userID}/attributes](endpoints/ADM.md)
- [COMMON · DELETE /Attributes/{id}](endpoints/COMMON.md)
- [COMMON · DELETE /Attributes](endpoints/COMMON.md)
- [COMMON · GET /Attributes/{attributeID}/listOfValues](endpoints/COMMON.md) → COMMON:map<str>
- [COMMON · GET /Attributes/{attributeID}](endpoints/COMMON.md) → COMMON:AttributeResultGet
- [COMMON · GET /Attributes](endpoints/COMMON.md) → COMMON:map<AttributeResultList>
- [COMMON · POST /Attributes](endpoints/COMMON.md)
- [COMMON · PUT /Attributes](endpoints/COMMON.md)
- [ES · GET /AssetTemplates/{assetTemplateID}/attributes](endpoints/ES.md) → ES:ResultsAssetTemplatesAssetTemplateAttributeResult[]
- [ES · GET /Assets/attributes](endpoints/ES.md) → ES:ResultsAssetsAssetAttributesExtResult[]
- [ES · GET /Assets/{assetID}/attributes](endpoints/ES.md) → ES:ResultsAssetsAssetAttributeResult[]
- [ES · GET /Companies/{companyID}/attributes](endpoints/ES.md) → ES:ResultsCompanyAttributesCompanyAttributeResult[]
- [ES · POST /Companies/{companyID}/attributes](endpoints/ES.md)
- [SC · GET /ServiceContract/{contractID}/attributes](endpoints/SC.md) → SC:ContractAttributeResult[]
- [SLA · DELETE /DeadlineRules/attributes](endpoints/SLA.md)
- [SLA · GET /Attributes](endpoints/SLA.md) → SLA:map<ResultsAttributesListResult>
- [SLA · GET /DeadlineRules/{deadlineRuleID}/attributes](endpoints/SLA.md) → SLA:map<int[]>
- [SLA · POST /DeadlineRules/attributes](endpoints/SLA.md)
- [UI · GET /LayoutTemplates/{id}/Attributes](endpoints/UI.md) → UI:ApiDtoAttributeDto[]
- [WORK · DELETE /Tasks/completedWorks/attributes](endpoints/WORK.md)
- [WORK · DELETE /Tasks/{taskID}/completedWorks/{completedWorkID}/attributes/{attributeID}](endpoints/WORK.md)
- [WORK · DELETE /Tasks/{taskID}/completedWorks/{completedWorkID}/attributes](endpoints/WORK.md)
- [WORK · GET /Tasks/{taskID}/attributes](endpoints/WORK.md) → WORK:AttributeResult[]
- [WORK · GET /Tasks/{taskID}/completedWorks/attributes](endpoints/WORK.md) → WORK:CompletedWorkAttributeResult[]
- [WORK · GET /Tasks/{taskID}/completedWorks/{completedWorkID}/attributes](endpoints/WORK.md) → WORK:CompletedWorkAttributeResult[]
- [WORK · PUT /Tasks/completedWorks/attributes](endpoints/WORK.md)
- [WORK · PUT /Tasks/{taskID}/completedWorks/{completedWorkID}/attributes](endpoints/WORK.md)

### attributetypes

- [COMMON · GET /AttributeTypes/v2](endpoints/COMMON.md) → COMMON:ExtListResult[]
- [COMMON · GET /AttributeTypes](endpoints/COMMON.md) → COMMON:map<RATListResult>

### attrvalues

- [SLA · DELETE /DeadlineRules/{deadlineRuleID}/attributes/{attributeID}/attrValues/{attrValue}](endpoints/SLA.md)
- [SLA · POST /DeadlineRules/{deadlineRuleID}/attributes/{attributeID}/attrValues/{attrValue}](endpoints/SLA.md)

### availability

- [TSTG · GET /TaskStageComponents/availability](endpoints/TSTG.md) → TSTG:AvailabilityListResult

### avatar

- [ADM · DELETE /Users/avatar](endpoints/ADM.md)
- [ADM · DELETE /Users/this/avatar](endpoints/ADM.md)
- [ADM · DELETE /Users/{id}/avatar](endpoints/ADM.md)
- [ADM · PUT /Users/this/avatar/upload/fromBody](endpoints/ADM.md)
- [ADM · PUT /Users/this/avatar/upload/fromForm](endpoints/ADM.md)
- [ADM · PUT /Users/{id}/avatar/upload/fromBody](endpoints/ADM.md)
- [ADM · PUT /Users/{id}/avatar/upload/fromForm](endpoints/ADM.md)
- [ES · DELETE /AssetTemplates/avatar](endpoints/ES.md)
- [ES · DELETE /AssetTemplates/{id}/avatar](endpoints/ES.md)
- [ES · DELETE /Assets/avatar](endpoints/ES.md)
- [ES · DELETE /Assets/{id}/avatar](endpoints/ES.md)
- [ES · PUT /AssetTemplates/{id}/avatar/upload/fromBody](endpoints/ES.md)
- [ES · PUT /AssetTemplates/{id}/avatar/upload/fromForm](endpoints/ES.md)
- [ES · PUT /Assets/{id}/avatar/upload/fromBody](endpoints/ES.md)
- [ES · PUT /Assets/{id}/avatar/upload/fromForm](endpoints/ES.md)

### bankaccounts

- [ES · DELETE /Companies/{companyID}/bankAccounts/{bankAccountID}](endpoints/ES.md)
- [ES · DELETE /Companies/{companyID}/bankAccounts](endpoints/ES.md)
- [ES · GET /Companies/{companyID}/bankAccounts](endpoints/ES.md) → ES:map<ResultsCompanyBankAccountsListResult>
- [ES · POST /Companies/{companyID}/bankAccounts](endpoints/ES.md)
- [ES · PUT /Companies/{companyID}/bankAccounts](endpoints/ES.md)

### banks

- [COMMON · GET /Banks/{bankId}](endpoints/COMMON.md) → COMMON:BankResult
- [COMMON · GET /Banks](endpoints/COMMON.md) → COMMON:map<BankResult>

### banreasons

- [ADM · GET /BanReasons](endpoints/ADM.md) → ADM:map<RBRListResult>

### barcodes

- [WH · DELETE /Materials/barcodes](endpoints/WH.md)
- [WH · DELETE /Materials/{materialID}/barcodes/{barcodeID}](endpoints/WH.md)
- [WH · GET /Materials/{materialID}/barcodes](endpoints/WH.md) → WH:map<ResultsMaterialBarcodesListResult[]>
- [WH · POST /Materials/barcodes](endpoints/WH.md)
- [WH · PUT /Materials/barcodes](endpoints/WH.md)

### barcodetypes

- [WH · GET /BarcodeTypes](endpoints/WH.md) → WH:map<ResultsBarcodeTypesListResult>

### branches

- [TSTG · GET /Branches](endpoints/TSTG.md) → TSTG:map<BranchResult>

### bypass

- [PROXY · POST /Bypass](endpoints/PROXY.md)

### bytype

- [UI · GET /LayoutTemplates/bytype/{id}](endpoints/UI.md) → UI:ApiDtoLayoutTemplateDto

### capabilities

- [ADM · GET /Capabilities](endpoints/ADM.md) → ADM:map<RCListResult>

### changes

- [WORK · GET /Tasks/{taskID}/changes](endpoints/WORK.md) → WORK:HistoryResult[]

### checklistitems

- [WORK · DELETE /CheckListItems](endpoints/WORK.md)
- [WORK · POST /CheckListItems](endpoints/WORK.md)

### checklists

- [ES · DELETE /Assets/{assetID}/checkLists/{checkListID}](endpoints/ES.md)
- [ES · DELETE /Assets/{assetID}/checkLists](endpoints/ES.md)
- [ES · GET /Assets/{assetID}/checkLists](endpoints/ES.md) → ES:map<ResultsAssetCheckListsGetResult[]>
- [ES · POST /Assets/{assetID}/checkLists/{checkListID}](endpoints/ES.md)
- [ES · POST /Assets/{assetID}/checkLists](endpoints/ES.md)
- [WORK · DELETE /CheckLists/{checkListID}/assign](endpoints/WORK.md)
- [WORK · DELETE /CheckLists/{id}](endpoints/WORK.md)
- [WORK · DELETE /CheckLists](endpoints/WORK.md)
- [WORK · DELETE /Tasks/{taskID}/checkLists/{taskCheckListID}](endpoints/WORK.md)
- [WORK · DELETE /Tasks/{taskID}/checkLists](endpoints/WORK.md)
- [WORK · DELETE /WorkTypes/{workTypeID}/checkLists/{checkListID}](endpoints/WORK.md)
- [WORK · DELETE /WorkTypes/{workTypeID}/checkLists](endpoints/WORK.md)
- [WORK · GET /CheckLists/{id}](endpoints/WORK.md) → WORK:map<CheckLists.GetResult>
- [WORK · GET /CheckLists](endpoints/WORK.md) → WORK:map<CheckLists.ListResult>
- [WORK · GET /Tasks/{taskID}/checkLists](endpoints/WORK.md) → WORK:map<TaskCheckListResult>
- [WORK · GET /WorkTypes/{workTypeID}/checkLists](endpoints/WORK.md) → WORK:map<CheckLists.GetResult[]>
- [WORK · POST /CheckLists/{checkListID}/assign](endpoints/WORK.md)
- [WORK · POST /CheckLists](endpoints/WORK.md)
- [WORK · POST /Tasks/{taskID}/checkLists/{taskCheckListID}/upload/fromForm](endpoints/WORK.md)
- [WORK · POST /Tasks/{taskID}/checkLists/{taskCheckListID}](endpoints/WORK.md)
- [WORK · POST /Tasks/{taskID}/checkLists](endpoints/WORK.md)
- [WORK · POST /WorkTypes/{workTypeID}/checkLists/{checkListID}](endpoints/WORK.md)
- [WORK · POST /WorkTypes/{workTypeID}/checkLists](endpoints/WORK.md)
- [WORK · PUT /CheckLists](endpoints/WORK.md)

### companies

- [ES · DELETE /Companies/{id}](endpoints/ES.md)
- [ES · DELETE /Companies](endpoints/ES.md)
- [ES · GET /Companies/{id}](endpoints/ES.md) → ES:ResultsCompaniesGetResult
- [ES · GET /Companies](endpoints/ES.md) → ES:map<ResultsCompaniesListResult>
- [ES · HEAD /Companies](endpoints/ES.md)
- [ES · POST /Companies](endpoints/ES.md)
- [ES · PUT /Companies/restore](endpoints/ES.md)
- [ES · PUT /Companies](endpoints/ES.md)
- [EXPORT · GET /Companies](endpoints/EXPORT.md)
- [IMPORT · POST /Companies](endpoints/IMPORT.md)

### companyattachments

- [ES · DELETE /CompanyAttachments](endpoints/ES.md)
- [ES · POST /CompanyAttachments/upload/fromBody](endpoints/ES.md)
- [ES · POST /CompanyAttachments/upload/fromForm](endpoints/ES.md)
- [ES · POST /CompanyAttachments](endpoints/ES.md)

### companycontacts

- [ES · DELETE /CompanyContacts](endpoints/ES.md)
- [ES · POST /CompanyContacts](endpoints/ES.md)

### companylistqueries

- [ADM · GET /Users/this/companyListQueries](endpoints/ADM.md) → ADM:map<CompanyListQueryResult>
- [ADM · GET /Users/{id}/companyListQueries](endpoints/ADM.md) → ADM:map<CompanyListQueryResult>
- [ES · DELETE /CompanyListQueries/remove](endpoints/ES.md)
- [ES · DELETE /CompanyListQueries/{id}/remove](endpoints/ES.md)
- [ES · DELETE /CompanyListQueries/{id}](endpoints/ES.md)
- [ES · DELETE /CompanyListQueries](endpoints/ES.md)
- [ES · GET /CompanyListQueries/{id}](endpoints/ES.md) → ES:ResultsCompanyListQueriesCompanyListQueryGetResult
- [ES · GET /CompanyListQueries](endpoints/ES.md) → ES:map<ResultsCompanyListQueriesCompanyListQueryResult>
- [ES · POST /CompanyListQueries](endpoints/ES.md)
- [ES · PUT /CompanyListQueries](endpoints/ES.md)

### companylocations

- [ES · DELETE /CompanyLocations](endpoints/ES.md)
- [ES · GET /CompanyLocations](endpoints/ES.md) → ES:map<ResultsCompaniesCompanyLocationResult>
- [ES · POST /CompanyLocations](endpoints/ES.md)
- [ES · PUT /CompanyLocations](endpoints/ES.md)

### companyregistrationtypes

- [ES · GET /CompanyRegistrationTypes](endpoints/ES.md) → ES:map<ResultsCompanyRegistrationTypesListResult>

### completedworkattachments

- [WORK · DELETE /CompletedWorkAttachments](endpoints/WORK.md)
- [WORK · POST /CompletedWorkAttachments/upload/fromBody](endpoints/WORK.md)
- [WORK · POST /CompletedWorkAttachments/upload/fromForm](endpoints/WORK.md)
- [WORK · POST /CompletedWorkAttachments](endpoints/WORK.md)

### completedworks

- [WORK · DELETE /CompletedWorks](endpoints/WORK.md)
- [WORK · GET /Tasks/{taskID}/completedWorks/materialsWithCodes](endpoints/WORK.md) → WORK:map<CompletedWorkMaterialResult>
- [WORK · GET /Tasks/{taskID}/completedWorks/{id}](endpoints/WORK.md) → WORK:CompletedWorkResult[]
- [WORK · GET /Tasks/{taskID}/completedWorks](endpoints/WORK.md) → WORK:CompletedWorkResult[]
- [WORK · POST /CompletedWorks](endpoints/WORK.md)
- [WORK · POST /Tasks/{taskID}/completedWorks/{completedWorkID}/upload/fromForm](endpoints/WORK.md)
- [WORK · PUT /CompletedWorks](endpoints/WORK.md)

### completiontime

- [REPORT · GET /CompletionTime](endpoints/REPORT.md) → REPORT:ResultsCompletionTimeCompletionTimeResult[]

### components

- [UI · GET /Components](endpoints/UI.md) → UI:map<ResultsBaseComponentResult>
- [UI · GET /LayoutTemplates/{id}/Components](endpoints/UI.md) → UI:ApiDtoComponentDto[]

### contacts

- [COMMON · DELETE /Contacts/{id}](endpoints/COMMON.md)
- [COMMON · DELETE /Contacts](endpoints/COMMON.md)
- [COMMON · GET /Contacts/{contactID}](endpoints/COMMON.md) → COMMON:RCGetResult
- [COMMON · GET /Contacts](endpoints/COMMON.md) → COMMON:map<RContactsListResult>
- [COMMON · POST /Contacts](endpoints/COMMON.md)
- [COMMON · PUT /Contacts](endpoints/COMMON.md)
- [ES · DELETE /Assets/contacts](endpoints/ES.md)
- [ES · DELETE /Assets/{assetID}/contacts/{contactID}](endpoints/ES.md)
- [ES · DELETE /Companies/contacts](endpoints/ES.md)
- [ES · DELETE /Companies/{companyID}/contacts/{contactID}](endpoints/ES.md)
- [ES · GET /Assets/{assetID}/contacts/{contactID}](endpoints/ES.md) → ES:ResultsAssetContactsGetResult
- [ES · GET /Assets/{assetID}/contacts](endpoints/ES.md) → ES:map<ResultsAssetContactsListResult>
- [ES · GET /Companies/{companyID}/contacts/{contactID}](endpoints/ES.md) → ES:ResultsCompanyContactsGetResult
- [ES · GET /Companies/{companyID}/contacts](endpoints/ES.md) → ES:map<ResultsCompanyContactsListResult>
- [ES · POST /Assets/contacts](endpoints/ES.md)
- [ES · POST /Assets/{assetID}/contacts/{contactID}](endpoints/ES.md)
- [ES · POST /Companies/contacts](endpoints/ES.md)
- [ES · POST /Companies/{companyID}/contacts/{contactID}](endpoints/ES.md)
- [SC · DELETE /ServiceContract/{contractID}/contacts/{contactID}](endpoints/SC.md)
- [SC · DELETE /ServiceContract/{contractID}/contacts](endpoints/SC.md)
- [SC · GET /ServiceContract/{contractID}/contacts](endpoints/SC.md) → SC:map<ContactResultBase>
- [SC · POST /ServiceContract/{contractID}/contacts](endpoints/SC.md)
- [SC · PUT /ServiceContract/{contractID}/contacts/{contactID}](endpoints/SC.md)
- [WORK · DELETE /Tasks/{taskID}/contacts/{contactID}](endpoints/WORK.md)
- [WORK · GET /Tasks/{taskID}/contacts/{contactID}](endpoints/WORK.md) → WORK:TaskContacts.GetResult
- [WORK · GET /Tasks/{taskID}/contacts](endpoints/WORK.md) → WORK:map<TaskContacts.ListResult>

### content

- [COMMON · GET /Attachments/content/{container}/{filePath}](endpoints/COMMON.md)

### contenttypes

- [MSG · GET /ContentTypes](endpoints/MSG.md) → MSG:map<RCTListResult>

### contractattributes

- [SC · POST /ContractAttributes](endpoints/SC.md)

### conversation

- [WORK · POST /Tasks/{taskID}/conversation/upload/fromForm](endpoints/WORK.md)
- [WORK · POST /Tasks/{taskID}/conversation](endpoints/WORK.md)

### conversations

- [WORK · GET /Tasks/{taskID}/conversations/{taskConversationID}](endpoints/WORK.md) → WORK:TaskMessage
- [WORK · GET /Tasks/{taskID}/conversations](endpoints/WORK.md) → WORK:TaskMessage[]
- [WORK · HEAD /Tasks/{taskID}/conversations](endpoints/WORK.md)

### countries

- [COMMON · GET /Countries](endpoints/COMMON.md) → COMMON:map<RCountriesListResult>

### criticalities

- [MSG · GET /Triggers/{id}/criticalities](endpoints/MSG.md) → MSG:IdNameResultOfShort[]
- [SLA · DELETE /Criticalities/{id}](endpoints/SLA.md)
- [SLA · DELETE /Criticalities](endpoints/SLA.md)
- [SLA · GET /Criticalities/{id}](endpoints/SLA.md) → SLA:ResultsCriticalitiesGetResult
- [SLA · GET /Criticalities](endpoints/SLA.md) → SLA:map<ResultsCriticalitiesGetResult>
- [SLA · POST /Criticalities](endpoints/SLA.md)
- [SLA · PUT /Criticalities](endpoints/SLA.md)

### criticalityfortriggers

- [MSG · POST /CriticalityForTriggers](endpoints/MSG.md)

### currencies

- [COMMON · GET /Currencies](endpoints/COMMON.md) → COMMON:map<RCurrenciesListResult>

### dadata

- [ES · GET /Companies/dadata/find](endpoints/ES.md) → ES:ESCompanyAddData

### deadlinerules

- [SLA · DELETE /DeadlineRules/{DeadlineRuleID}](endpoints/SLA.md)
- [SLA · DELETE /DeadlineRules](endpoints/SLA.md)
- [SLA · GET /DeadlineRules/{DeadlineRuleID}](endpoints/SLA.md) → SLA:ResultsDeadlineRulesGetResult
- [SLA · GET /DeadlineRules](endpoints/SLA.md) → SLA:map<ResultsDeadlineRulesListResult>
- [SLA · POST /DeadlineRules](endpoints/SLA.md)
- [SLA · PUT /DeadlineRules/activate](endpoints/SLA.md)
- [SLA · PUT /DeadlineRules/deactivate](endpoints/SLA.md)
- [SLA · PUT /DeadlineRules/{DeadlineRuleID}/activate](endpoints/SLA.md)
- [SLA · PUT /DeadlineRules/{DeadlineRuleID}/deactivate](endpoints/SLA.md)
- [SLA · PUT /DeadlineRules](endpoints/SLA.md)

### defaultpages

- [ADM · DELETE /Users/defaultPages](endpoints/ADM.md)
- [ADM · GET /DefaultPages](endpoints/ADM.md) → ADM:AllowedPageResult[]
- [ADM · GET /Users/{userID}/defaultPages](endpoints/ADM.md) → ADM:RUDPGetResult
- [ADM · POST /Users/defaultPages](endpoints/ADM.md)
- [ADM · PUT /Users/defaultPages](endpoints/ADM.md)

### delivery

- [WORK · GET /Tasks/{taskID}/conversations/{taskConversationID}/delivery](endpoints/WORK.md) → WORK:ListConversationDeliveryResult[]

### districts

- [ADM · GET /UserTemplates/{id}/districts](endpoints/ADM.md) → ADM:IdNameResultOfShort[]
- [ADM · GET /Users/{id}/districts](endpoints/ADM.md) → ADM:map<ListDistrictResult>
- [ES · DELETE /Districts/{id}](endpoints/ES.md)
- [ES · DELETE /Districts](endpoints/ES.md)
- [ES · GET /AssetTemplates/{assetTemplateID}/districts](endpoints/ES.md) → ES:map<ResultsCommonAssetDistrictResult>
- [ES · GET /Assets/{assetID}/districts](endpoints/ES.md) → ES:map<ResultsCommonAssetDistrictResult>
- [ES · GET /Districts/{id}](endpoints/ES.md) → ES:ResultsDistrictsDistrictResult
- [ES · GET /Districts](endpoints/ES.md) → ES:ResultsDistrictsDistrictListForTenantMemberResult[]
- [ES · POST /Districts](endpoints/ES.md)
- [ES · PUT /Districts/parentAndReorder](endpoints/ES.md)
- [ES · PUT /Districts](endpoints/ES.md)
- [WORK · GET /TaskTypes/{id}/districts](endpoints/WORK.md) → WORK:map<TaskTypeDistrictList>

### documents

- [WH · GET /Documents](endpoints/WH.md) → WH:ResultsDocumentsDocumentResult[]

### documentstatuses

- [WH · GET /DocumentStatuses](endpoints/WH.md) → WH:map<ResultsDocumentStatusesListResult>

### documenttypes

- [WH · GET /DocumentTypes](endpoints/WH.md) → WH:map<ResultsDocumentTypesListResult>

### employment

- [PA · DELETE /Employment](endpoints/PA.md)
- [PA · GET /Employment/{userID}](endpoints/PA.md) → PA:EmploymentGetResult[]
- [PA · POST /Employment](endpoints/PA.md)
- [PA · PUT /Employment](endpoints/PA.md)

### end

- [PA · PUT /Users/onshift/end/{userID}](endpoints/PA.md)

### errors

- [MSG · GET /MailBoxes/{id}/errors](endpoints/MSG.md) → MSG:MailBoxErrorsEntity[]

### events

- [COMMON · GET /Events](endpoints/COMMON.md) → COMMON:map<REListResult>

### excludedassets

- [WORK · DELETE /TaskTemplates/{taskTemplateID}/excludedAssets/{assetID}](endpoints/WORK.md)
- [WORK · GET /TaskTemplates/{tasktTemplateID}/excludedAssets](endpoints/WORK.md) → WORK:map<TaskTemplateExcludedAssetResult>

### extend

- [WSP · PUT /ScheduleRules/extend/{id}](endpoints/WSP.md)

### extended

- [EXPORT · GET /Assets/extended/includes](endpoints/EXPORT.md) → EXPORT:FieldResult[]
- [EXPORT · GET /Assets/extended](endpoints/EXPORT.md)
- [EXPORT · GET /Tasks/extended/V2](endpoints/EXPORT.md)
- [EXPORT · GET /Tasks/extended/includes](endpoints/EXPORT.md) → EXPORT:FieldResult[]
- [EXPORT · GET /Tasks/extended](endpoints/EXPORT.md)

### fields

- [MSG · GET /Notifications/fields](endpoints/MSG.md) → MSG:map<str>

### filters

- [UI · GET /Filters](endpoints/UI.md) → UI:EntitiesUIUserFilterFavouriteEntity[]
- [UI · POST /Filters/{resource}](endpoints/UI.md)

### frequencytypes

- [PMP · GET /FrequencyTypes](endpoints/PMP.md) → PMP:map<IdCodeNameResultOfByte>

### geolocationsettings

- [ADM · GET /GeolocationSettings/coordinateAccuracy](endpoints/ADM.md) → ADM:IdNameDescriptionEntityOfByte[]

### geotrackingmodes

- [PA · GET /GeoTrackingModes](endpoints/PA.md) → PA:map<RGTMListResult>

### groupby

- [WORK · GET /Tasks/groupBy/geoHash](endpoints/WORK.md) → WORK:TaskGroupByResult<ClusterResult>[]

### image

- [ES · DELETE /AssetSchemas/{schemaId}/image](endpoints/ES.md)
- [ES · GET /AssetSchemas/{schemaId}/image/download](endpoints/ES.md)
- [ES · GET /AssetSchemas/{schemaId}/image](endpoints/ES.md) → ES:ResultsAssetSchemaSchemaImage
- [ES · POST /AssetSchemas/{schemaId}/image/upload](endpoints/ES.md)

### inventories

- [WH · DELETE /Inventories/{id}](endpoints/WH.md)
- [WH · DELETE /Inventories](endpoints/WH.md)
- [WH · GET /Inventories/actual](endpoints/WH.md) → WH:ResultsInventoriesListResult
- [WH · GET /Inventories](endpoints/WH.md) → WH:map<ResultsInventoriesListResult>
- [WH · POST /Inventories](endpoints/WH.md)
- [WH · PUT /Inventories](endpoints/WH.md)

### invitations

- [ADM · DELETE /Invitations/{id}](endpoints/ADM.md)
- [ADM · DELETE /Invitations](endpoints/ADM.md)
- [ADM · GET /Invitations/{id}/short](endpoints/ADM.md) → ADM:GetShortResult
- [ADM · GET /Invitations/{id}](endpoints/ADM.md) → ADM:RIGetResult
- [ADM · GET /Invitations](endpoints/ADM.md) → ADM:map<RIGetResult>
- [ADM · POST /Invitations](endpoints/ADM.md)
- [ADM · PUT /Invitations](endpoints/ADM.md)

### issues

- [WH · DELETE /Issues/{id}](endpoints/WH.md)
- [WH · DELETE /Issues](endpoints/WH.md)
- [WH · GET /Issues/{id}](endpoints/WH.md) → WH:ResultsIssuesIssueResult
- [WH · GET /Issues](endpoints/WH.md) → WH:map<ResultsIssuesIssueResult>
- [WH · HEAD /Issues](endpoints/WH.md)
- [WH · POST /Issues](endpoints/WH.md)
- [WH · PUT /Issues/post](endpoints/WH.md)
- [WH · PUT /Issues/restore](endpoints/WH.md)
- [WH · PUT /Issues/unpost](endpoints/WH.md)
- [WH · PUT /Issues/{id}/post](endpoints/WH.md)
- [WH · PUT /Issues/{id}/restore](endpoints/WH.md)
- [WH · PUT /Issues/{id}/unpost](endpoints/WH.md)
- [WH · PUT /Issues](endpoints/WH.md)

### items

- [WH · DELETE /Issues/items](endpoints/WH.md)
- [WH · DELETE /Issues/{issueID}/items/{materialID}](endpoints/WH.md)
- [WH · DELETE /Receipts/items](endpoints/WH.md)
- [WH · DELETE /Receipts/{receiptID}/items/{materialID}](endpoints/WH.md)
- [WH · DELETE /Transfers/items](endpoints/WH.md)
- [WH · DELETE /Transfers/{transferID}/items/{materialID}](endpoints/WH.md)
- [WH · GET /Issues/{issueID}/items](endpoints/WH.md) → WH:ResultsIssueItemsListResult[]
- [WH · GET /Receipts/{receiptID}/items](endpoints/WH.md) → WH:ResultsReceiptItemsListResult[]
- [WH · GET /Transfers/{transferID}/items](endpoints/WH.md) → WH:ResultsTransferItemsListResult[]
- [WH · POST /Issues/items](endpoints/WH.md)
- [WH · POST /Receipts/items](endpoints/WH.md)
- [WH · POST /Transfers/items](endpoints/WH.md)
- [WORK · GET /CheckLists/{checkListID}/items](endpoints/WORK.md) → WORK:map<CheckListItemResult>

### layouttemplates

- [UI · DELETE /LayoutTemplates/{id}](endpoints/UI.md)
- [UI · GET /LayoutTemplates/default](endpoints/UI.md) → UI:ApiDtoLayoutTemplateDto
- [UI · GET /LayoutTemplates/{id}](endpoints/UI.md) → UI:ApiDtoLayoutTemplateDto
- [UI · GET /LayoutTemplates](endpoints/UI.md) → UI:ApiDtoLayoutTemplateDto[]
- [UI · POST /LayoutTemplates/default](endpoints/UI.md)
- [UI · POST /LayoutTemplates](endpoints/UI.md)
- [UI · PUT /LayoutTemplates/{id}/reset](endpoints/UI.md)
- [UI · PUT /LayoutTemplates/{id}](endpoints/UI.md)

### licenses

- [ADM · DELETE /Tenants/this/licenses/{id}](endpoints/ADM.md)
- [ADM · DELETE /Tenants/this/licenses](endpoints/ADM.md)
- [ADM · GET /Tenants/this/licenses](endpoints/ADM.md) → ADM:ListTenantLicenseResult[]
- [ADM · POST /Tenants/this/licenses/renewal](endpoints/ADM.md)
- [ADM · POST /Tenants/this/licenses](endpoints/ADM.md)
- [ADM · PUT /Tenants/licenses](endpoints/ADM.md)

### licensescanner

- [LIC · GET /LicenseScanner/State](endpoints/LIC.md) → LIC:WatcherStateEnum
- [LIC · POST /LicenseScanner/Start](endpoints/LIC.md)
- [LIC · POST /LicenseScanner/Stop](endpoints/LIC.md)

### locations

- [CM · POST /Clients/locations](endpoints/CM.md)
- [ES · DELETE /Locations/remove](endpoints/ES.md)
- [ES · DELETE /Locations/{id}/remove](endpoints/ES.md)
- [ES · DELETE /Locations/{id}](endpoints/ES.md)
- [ES · DELETE /Locations](endpoints/ES.md)
- [ES · GET /Assets/{assetID}/locations/actual](endpoints/ES.md) → ES:ResultsCommonLocationResult
- [ES · GET /Companies/{companyID}/locations/actual](endpoints/ES.md) → ES:ResultsCommonLocationResult
- [ES · GET /Locations/{id}](endpoints/ES.md) → ES:ResultsLocationsLocationGetResult
- [ES · GET /Locations](endpoints/ES.md) → ES:map<ResultsCommonLocationResult>
- [ES · HEAD /Locations](endpoints/ES.md)
- [ES · POST /Locations](endpoints/ES.md)
- [ES · PUT /Locations](endpoints/ES.md)

### mailboxes

- [MSG · DELETE /MailBoxes/{id}](endpoints/MSG.md)
- [MSG · DELETE /MailBoxes](endpoints/MSG.md)
- [MSG · GET /MailBoxes/regexactions](endpoints/MSG.md) → MSG:map<RRNMAListResult>
- [MSG · GET /MailBoxes/{id}](endpoints/MSG.md) → MSG:RMBGetResult
- [MSG · GET /MailBoxes](endpoints/MSG.md) → MSG:map<RMBListResult>
- [MSG · POST /MailBoxes](endpoints/MSG.md)
- [MSG · PUT /MailBoxes/activate/{id}](endpoints/MSG.md)
- [MSG · PUT /MailBoxes/activate](endpoints/MSG.md)
- [MSG · PUT /MailBoxes/deactivate/{id}](endpoints/MSG.md)
- [MSG · PUT /MailBoxes/deactivate](endpoints/MSG.md)

### marking-codes

- [WORK · DELETE /Tasks/{taskId}/completedWorks/marking-codes](endpoints/WORK.md)
- [WORK · DELETE /Tasks/{taskId}/completedWorks/{completedWorkID}/materials/marking-codes](endpoints/WORK.md)
- [WORK · DELETE /Tasks/{taskId}/completedWorks/{completedWorkID}/materials/{materialID}/marking-codes](endpoints/WORK.md)
- [WORK · GET /Tasks/{taskId}/completedWorks/{completedWorkID}/marking-codes](endpoints/WORK.md) → WORK:MarkingCodesListResult
- [WORK · GET /Tasks/{taskId}/completedWorks/{completedWorkID}/materials/{materialID}/marking-codes](endpoints/WORK.md) → WORK:MarkingCodesListResult
- [WORK · GET /Tasks/{taskId}/marking-codes](endpoints/WORK.md) → WORK:MarkingCodesListResult
- [WORK · POST /Tasks/{taskId}/completedWorks/{completedWorkID}/materials/marking-codes](endpoints/WORK.md)
- [WORK · POST /Tasks/{taskId}/completedWorks/{completedWorkID}/materials/{materialID}/marking-codes](endpoints/WORK.md)
- [WORK · PUT /Tasks/{taskId}/completedWorks/{completedWorkID}/materials/marking-codes](endpoints/WORK.md)
- [WORK · PUT /Tasks/{taskId}/completedWorks/{completedWorkID}/materials/{materialID}/marking-codes](endpoints/WORK.md)

### materialconsumption

- [EXPORT · GET /MaterialConsumption](endpoints/EXPORT.md)

### materialconsumptions

- [WH · GET /MaterialConsumptions](endpoints/WH.md) → WH:map<ResultsMaterialConsumptionsMaterialInventoryResult>

### materials

- [EXPORT · GET /Materials/v2.0](endpoints/EXPORT.md)
- [EXPORT · GET /Materials](endpoints/EXPORT.md)
- [IMPORT · POST /Materials/v2.0](endpoints/IMPORT.md)
- [IMPORT · POST /Materials](endpoints/IMPORT.md)
- [WH · DELETE /Materials/{id}](endpoints/WH.md)
- [WH · DELETE /Materials](endpoints/WH.md)
- [WH · GET /Materials/v2](endpoints/WH.md) → WH:map<ResultsMaterialsMaterialListResult>
- [WH · GET /Materials/{id}](endpoints/WH.md) → WH:ResultsMaterialsMaterialResult
- [WH · GET /Materials/{required}](endpoints/WH.md) → WH:ResultsMaterialsListRequiredResult[]
- [WH · GET /Materials](endpoints/WH.md) → WH:ResultsMaterialsListResult[]
- [WH · HEAD /Materials](endpoints/WH.md) → WH:map<ResultsMaterialsMaterialListResult>
- [WH · POST /Materials](endpoints/WH.md)
- [WH · PUT /Materials/restore](endpoints/WH.md)
- [WH · PUT /Materials/{id}/restore](endpoints/WH.md)
- [WH · PUT /Materials](endpoints/WH.md)
- [WORK · DELETE /Tasks/completedWorks/materials](endpoints/WORK.md)
- [WORK · DELETE /Tasks/{taskID}/completedWorks/{completedWorkID}/materials](endpoints/WORK.md)
- [WORK · GET /Tasks/{taskID}/completedWorks/materials](endpoints/WORK.md) → WORK:map<CompletedWorkMaterialResult>
- [WORK · GET /Tasks/{taskID}/completedWorks/{completedWorkID}/materials](endpoints/WORK.md) → WORK:CompletedWorkMaterialResult
- [WORK · GET /Tasks/{taskID}/materials](endpoints/WORK.md) → WORK:map<TaskMaterials.ListResult>
- [WORK · POST /Tasks/completedWorks/materials](endpoints/WORK.md)
- [WORK · PUT /Tasks/completedWorks/materials](endpoints/WORK.md)

### measurementunits

- [COMMON · GET /MeasurementUnits](endpoints/COMMON.md) → COMMON:map<MeasurementUnitResult>

### messages

- [AUTH · POST /Messages/requestPasswordChange](endpoints/AUTH.md)
- [AUTH · POST /Messages/verifyEmail](endpoints/AUTH.md)
- [AUTH · POST /Messages/verifyPhone](endpoints/AUTH.md)

### messagetemplates

- [MSG · DELETE /MessageTemplates/{id}](endpoints/MSG.md)
- [MSG · DELETE /MessageTemplates](endpoints/MSG.md)
- [MSG · GET /MessageTemplates/{id}](endpoints/MSG.md) → MSG:RMTGetResult
- [MSG · GET /MessageTemplates](endpoints/MSG.md) → MSG:map<RMTListResult>
- [MSG · POST /MessageTemplates](endpoints/MSG.md)
- [MSG · PUT /MessageTemplates/{id}/validate](endpoints/MSG.md)
- [MSG · PUT /MessageTemplates](endpoints/MSG.md)

### messagetriggers

- [TSTG · GET /TaskStages/{id}/messageTriggers](endpoints/TSTG.md) → TSTG:IdNameResultOfShort[]

### mobilities

- [PA · GET /Mobilities](endpoints/PA.md) → PA:map<RMListResult>

### moblities

- [PA · GET /Moblities](endpoints/PA.md) → PA:map<RMListResult>

### navigateto

- [MSG · GET /NavigateTo](endpoints/MSG.md) → MSG:map<RNTListResult>
- [PROXY · GET /NavigateTo/{appCode}](endpoints/PROXY.md) → PROXY:GetResult

### new

- [WORK · GET /Tasks/new/meta](endpoints/WORK.md) → WORK:map<TaskTypeFormMetadataResult>

### notifications

- [ADM · GET /Users/this/notifications](endpoints/ADM.md) → ADM:RUDNListResult
- [ADM · GET /Users/{id}/notifications](endpoints/ADM.md) → ADM:RUDNListResult
- [AUTH · GET /Accounts/this/notifications](endpoints/AUTH.md) → AUTH:ListResult[]
- [MSG · GET /Notifications](endpoints/MSG.md) → MSG:map<RNListResult>
- [MSG · HEAD /Notifications](endpoints/MSG.md)
- [MSG · POST /Notifications](endpoints/MSG.md)
- [MSG · PUT /Notifications/all](endpoints/MSG.md)
- [MSG · PUT /Notifications](endpoints/MSG.md)

### numbersequences

- [WH · GET /NumberSequences/{documentTypeId}](endpoints/WH.md) → WH:ResultsNumberSequencesNumberSequenceResult
- [WH · GET /NumberSequences](endpoints/WH.md) → WH:ResultsNumberSequencesNumberSequenceResult[]
- [WH · POST /NumberSequences](endpoints/WH.md)
- [WH · PUT /NumberSequences](endpoints/WH.md)

### onshift

- [PA · DELETE /Users/onshift/{userID}](endpoints/PA.md)
- [PA · GET /Users/onshift/status](endpoints/PA.md) → PA:WorkShiftScheduleUserStatusResult[]
- [PA · POST /Users/onshift/{userID}](endpoints/PA.md)
- [PA · PUT /Users/onshift/start/{userID}](endpoints/PA.md)

### operationtypes

- [WH · DELETE /OperationTypes/{id}](endpoints/WH.md)
- [WH · DELETE /OperationTypes](endpoints/WH.md)
- [WH · GET /OperationTypes/{id}](endpoints/WH.md) → WH:ResultsOperationTypesOperationTypeResult
- [WH · GET /OperationTypes](endpoints/WH.md) → WH:map<ResultsOperationTypesOperationTypeResult>
- [WH · POST /OperationTypes](endpoints/WH.md)
- [WH · PUT /OperationTypes](endpoints/WH.md)

### orgunits

- [ES · GET /OrgUnits/root](endpoints/ES.md) → ES:map<ResultsOrgUnitsOrgUnitListResult>
- [ES · GET /OrgUnits/{id}/orgunits](endpoints/ES.md) → ES:map<ResultsOrgUnitsOrgUnitListResult>
- [ES · GET /OrgUnits](endpoints/ES.md) → ES:map<ResultsOrgUnitsOrgUnitListResult>

### overridings

- [TSTG · DELETE /TaskStageLinks/overridings](endpoints/TSTG.md)
- [TSTG · GET /TaskStageLinks/overridings](endpoints/TSTG.md) → TSTG:OverrideListResult[]
- [TSTG · POST /TaskStageLinks/overridings](endpoints/TSTG.md)
- [TSTG · PUT /TaskStageLinks/overridings](endpoints/TSTG.md)

### packages

- [ADM · DELETE /Roles/{roleID}/packages](endpoints/ADM.md)
- [ADM · DELETE /Tenants/this/packages/tenant](endpoints/ADM.md)
- [ADM · DELETE /Tenants/this/packages](endpoints/ADM.md)
- [ADM · GET /Roles/{roleID}/packages](endpoints/ADM.md) → ADM:map<RRPListResult[]>
- [ADM · GET /Tenants/this/packages](endpoints/ADM.md) → ADM:RTPListResult[]
- [ADM · PATCH /Tenants/this/packages](endpoints/ADM.md)
- [ADM · POST /Roles/{roleID}/packages](endpoints/ADM.md)
- [ADM · POST /Tenants/this/packages/tenant](endpoints/ADM.md)
- [ADM · POST /Tenants/this/packages](endpoints/ADM.md)
- [ADM · PUT /Roles/{roleID}/packages/activate](endpoints/ADM.md)
- [ADM · PUT /Roles/{roleID}/packages/deactivate](endpoints/ADM.md)

### passwords

- [AUTH · POST /Passwords/change](endpoints/AUTH.md)
- [AUTHN · POST /Passwords/set](endpoints/AUTHN.md)

### permissionapitags

- [ADM · GET /PermissionApiTags](endpoints/ADM.md) → ADM:map<RPATListResult[]>

### permissionexttags

- [ADM · GET /PermissionExtTags](endpoints/ADM.md) → ADM:map<RPETListResult[]>

### permissions

- [ADM · GET /Users/this/permissions/ext](endpoints/ADM.md) → ADM:map<str>
- [ADM · GET /Users/this/permissions/ui](endpoints/ADM.md) → ADM:map<str>

### permissionsapi

- [ADM · GET /PermissionsApi](endpoints/ADM.md) → ADM:map<RPAListResult>
- [ADM · GET /Roles/{roleID}/permissionsApi](endpoints/ADM.md) → ADM:map<RRPAListResult[]>

### permissionsext

- [ADM · GET /PermissionsExt](endpoints/ADM.md) → ADM:map<RPEListResult>
- [ADM · GET /Roles/{roleID}/permissionsExt](endpoints/ADM.md) → ADM:map<RRPEListResult[]>

### permissionsui

- [ADM · DELETE /PermissionsUi/{id}](endpoints/ADM.md)
- [ADM · DELETE /PermissionsUi](endpoints/ADM.md)
- [ADM · GET /PermissionsUi/{id}](endpoints/ADM.md) → ADM:RPUGetResult
- [ADM · GET /PermissionsUi](endpoints/ADM.md) → ADM:map<RPUGetResult>
- [ADM · GET /Roles/{roleID}/permissionsUi](endpoints/ADM.md) → ADM:map<RRPUListResult[]>
- [ADM · POST /PermissionsUi](endpoints/ADM.md)
- [ADM · PUT /PermissionsUi](endpoints/ADM.md)

### points

- [ES · DELETE /AssetSchemas/{schemaId}/points](endpoints/ES.md)
- [ES · GET /AssetSchemas/{schemaId}/points](endpoints/ES.md) → ES:ResultsAssetSchemaSchemaTask[]
- [ES · POST /AssetSchemas/{schemaId}/points](endpoints/ES.md)

### powerbicustomreports

- [REPORT · GET /PowerBICustomReports](endpoints/REPORT.md) → REPORT:map<ResultsPowerBICustomReportsCustomReportList>

### powerbireports

- [COMMON · GET /PowerBIReports/{id}](endpoints/COMMON.md) → COMMON:PowerBIReportResult
- [COMMON · GET /PowerBIReports](endpoints/COMMON.md) → COMMON:PowerBIReportResult[]

### preferredtechnicians

- [ES · GET /PreferredTechnicians](endpoints/ES.md) → ES:ResultsPreferredTechniciansPreferredTechniciansResult
- [ES · POST /PreferredTechnicians](endpoints/ES.md)

### protocols

- [MSG · GET /Protocols](endpoints/MSG.md) → MSG:map<RProtocolsListResult>

### providers

- [MSG · GET /Providers](endpoints/MSG.md) → MSG:map<RProvidersListResult>

### rating

- [PA · GET /Technicians/{userID}/rating](endpoints/PA.md) → PA:TechnicianRatingResult

### ratingcriteria

- [PA · DELETE /RatingCriteria/{id}](endpoints/PA.md)
- [PA · DELETE /RatingCriteria](endpoints/PA.md)
- [PA · GET /RatingCriteria/{id}](endpoints/PA.md) → PA:RRCGetResult
- [PA · GET /RatingCriteria](endpoints/PA.md) → PA:map<RRCListResult>
- [PA · POST /RatingCriteria](endpoints/PA.md)
- [PA · PUT /RatingCriteria](endpoints/PA.md)

### ratings

- [ADM · GET /Users/{UserID}/ratings](endpoints/ADM.md) → ADM:RatingTechnicianResult
- [WORK · GET /Tasks/{taskID}/ratings/avg](endpoints/WORK.md) → WORK:RatingResult[]
- [WORK · GET /Tasks/{taskID}/ratings](endpoints/WORK.md) → WORK:RatingResult[]

### reactiontime

- [REPORT · GET /ReactionTime](endpoints/REPORT.md) → REPORT:ResultsReactionTimeReactionTimeResult[]

### read

- [WORK · PUT /TaskConversationDeliveries/read/All](endpoints/WORK.md)
- [WORK · PUT /TaskConversationDeliveries/read](endpoints/WORK.md)

### receipts

- [WH · DELETE /Receipts/{id}](endpoints/WH.md)
- [WH · DELETE /Receipts](endpoints/WH.md)
- [WH · GET /Receipts/{id}](endpoints/WH.md) → WH:ResultsReceiptsReceiptResult
- [WH · GET /Receipts](endpoints/WH.md) → WH:map<ResultsReceiptsReceiptResult>
- [WH · HEAD /Receipts](endpoints/WH.md)
- [WH · POST /Receipts](endpoints/WH.md)
- [WH · PUT /Receipts/post](endpoints/WH.md)
- [WH · PUT /Receipts/restore](endpoints/WH.md)
- [WH · PUT /Receipts/unpost](endpoints/WH.md)
- [WH · PUT /Receipts/{id}/post](endpoints/WH.md)
- [WH · PUT /Receipts/{id}/restore](endpoints/WH.md)
- [WH · PUT /Receipts/{id}/unpost](endpoints/WH.md)
- [WH · PUT /Receipts](endpoints/WH.md)

### recipients

- [MSG · GET /RecipientSelectionRules/recipients](endpoints/MSG.md) → MSG:map<RecipientListResult>

### recipientselectionrules

- [MSG · DELETE /RecipientSelectionRules/{id}](endpoints/MSG.md)
- [MSG · DELETE /RecipientSelectionRules](endpoints/MSG.md)
- [MSG · GET /RecipientSelectionRules/{id}](endpoints/MSG.md) → MSG:RRSRGetResult
- [MSG · GET /RecipientSelectionRules](endpoints/MSG.md) → MSG:map<RRSRListResult>
- [MSG · POST /RecipientSelectionRules](endpoints/MSG.md)
- [MSG · PUT /RecipientSelectionRules](endpoints/MSG.md)

### refreshtokens

- [AUTHZ · GET /RefreshTokens](endpoints/AUTHZ.md) → AUTHZ:JwtResultBase
- [AUTHZ · POST /RefreshTokens](endpoints/AUTHZ.md)

### registration

- [ADM · POST /Users/registration/verify](endpoints/ADM.md)
- [ADM · POST /Users/registration](endpoints/ADM.md)

### requestmethods

- [WORK · GET /RequestMethods](endpoints/WORK.md) → WORK:map<RequestMethods.ListResult>

### requirements

- [TSTG · GET /Requirements/requirements](endpoints/TSTG.md) → TSTG:map<RRListResult>
- [TSTG · GET /TaskStages/{id}/requirements](endpoints/TSTG.md) → TSTG:TaskStageRequirementResult[]

### resources

- [UI · GET /Resources](endpoints/UI.md) → UI:map<IdCodeNameResultOfByte>

### results

- [WORK · DELETE /Tasks/{taskID}/checkLists/{taskCheckListID}/results](endpoints/WORK.md)
- [WORK · GET /Tasks/{taskID}/checkLists/{taskCheckListID}/results/v2](endpoints/WORK.md) → WORK:map<TaskCheckListResultV2Result>
- [WORK · GET /Tasks/{taskID}/checkLists/{taskCheckListID}/results](endpoints/WORK.md) → WORK:map<TaskCheckListResultResult>
- [WORK · PUT /Tasks/{taskID}/checkLists/{taskCheckListID}/results/v2](endpoints/WORK.md)
- [WORK · PUT /Tasks/{taskID}/checkLists/{taskCheckListID}/results](endpoints/WORK.md)

### roleapplications

- [ADM · DELETE /RoleApplications](endpoints/ADM.md)
- [ADM · POST /RoleApplications](endpoints/ADM.md)

### roleattachments

- [ADM · DELETE /RoleAttachments](endpoints/ADM.md)
- [ADM · POST /RoleAttachments](endpoints/ADM.md)

### rolepermissionsapi

- [ADM · DELETE /RolePermissionsApi](endpoints/ADM.md)
- [ADM · POST /RolePermissionsApi](endpoints/ADM.md)

### rolepermissionsext

- [ADM · DELETE /RolePermissionsExt](endpoints/ADM.md)
- [ADM · POST /RolePermissionsExt](endpoints/ADM.md)

### rolepermissionsui

- [ADM · DELETE /RolePermissionsUi](endpoints/ADM.md)
- [ADM · POST /RolePermissionsUi](endpoints/ADM.md)

### roles

- [ADM · DELETE /Roles/{id}](endpoints/ADM.md)
- [ADM · DELETE /Roles](endpoints/ADM.md)
- [ADM · GET /Roles/{id}](endpoints/ADM.md) → ADM:RRGetResult
- [ADM · GET /Roles](endpoints/ADM.md) → ADM:RRGetResult[]
- [ADM · GET /UserTemplates/{id}/roles](endpoints/ADM.md) → ADM:IdNameResultOfShort[]
- [ADM · GET /Users/{id}/roles](endpoints/ADM.md) → ADM:map<IdNameResultOfShort[]>
- [ADM · POST /Roles/copy](endpoints/ADM.md)
- [ADM · POST /Roles](endpoints/ADM.md)
- [ADM · PUT /Roles](endpoints/ADM.md)
- [COMMON · GET /Attachments/{attachmentID}/roles](endpoints/COMMON.md) → COMMON:map<str>

### roletasklistqueries

- [ADM · DELETE /RoleTaskListQueries](endpoints/ADM.md)
- [ADM · POST /RoleTaskListQueries](endpoints/ADM.md)

### route

- [WORK · GET /TaskTypes/{taskTypeID}/route](endpoints/WORK.md) → WORK:RouteResult

### scheduledtasks

- [PMP · GET /ScheduledTasks/count](endpoints/PMP.md) → PMP:map<ListCountResult[]>
- [PMP · GET /ScheduledTasks/v2/count](endpoints/PMP.md) → PMP:map<CountResult[]>
- [PMP · GET /ScheduledTasks](endpoints/PMP.md) → PMP:map<RSTListResult>
- [PMP · HEAD /ScheduledTasks](endpoints/PMP.md)

### schedulerules

- [WSP · DELETE /ScheduleRules/{id}](endpoints/WSP.md)
- [WSP · GET /ScheduleRules/holiday](endpoints/WSP.md) → WSP:map<datetime[]>
- [WSP · GET /ScheduleRules/{id}](endpoints/WSP.md) → WSP:ScheduleRuleDto
- [WSP · GET /ScheduleRules](endpoints/WSP.md) → WSP:map<ListResult>
- [WSP · POST /ScheduleRules/preview](endpoints/WSP.md)
- [WSP · POST /ScheduleRules](endpoints/WSP.md)
- [WSP · PUT /ScheduleRules/{id}](endpoints/WSP.md)

### schedules

- [PA · GET /Users/onshift/schedules](endpoints/PA.md) → PA:map<WorkShiftScheduleDailyItemResult[]>
- [PMP · DELETE /Schedules/{id}](endpoints/PMP.md)
- [PMP · DELETE /Schedules](endpoints/PMP.md)
- [PMP · GET /Schedules/{id}](endpoints/PMP.md) → PMP:GetResult
- [PMP · GET /Schedules](endpoints/PMP.md) → PMP:map<RSRListResult>
- [PMP · POST /Schedules](endpoints/PMP.md)
- [WORK · GET /TaskTemplates/{id}/schedules](endpoints/WORK.md) → WORK:GetSchedulesResult[]
- [WORK · POST /TaskTemplates/{id}/schedules](endpoints/WORK.md)
- [WORK · PUT /TaskTemplates/{taskTemplateId}/schedules/{scheduleId}/activate](endpoints/WORK.md)
- [WORK · PUT /TaskTemplates/{taskTemplateId}/schedules/{scheduleId}/deactivate](endpoints/WORK.md)

### senders

- [MSG · DELETE /MailBoxes/{mailBoxID}/senders/{id}](endpoints/MSG.md)
- [MSG · DELETE /MailBoxes/{mailBoxID}/senders](endpoints/MSG.md)
- [MSG · GET /MailBoxes/{mailBoxID}/senders/{senderID}](endpoints/MSG.md) → MSG:RMBSGetResult
- [MSG · GET /MailBoxes/{mailBoxID}/senders](endpoints/MSG.md) → MSG:map<RMBSListResult>

### servicecontract

- [SC · DELETE /ServiceContract/{id}](endpoints/SC.md)
- [SC · DELETE /ServiceContract](endpoints/SC.md)
- [SC · GET /ServiceContract/{contractID}](endpoints/SC.md) → SC:ContractGetResult
- [SC · GET /ServiceContract](endpoints/SC.md) → SC:map<ContractListResult>
- [SC · HEAD /ServiceContract](endpoints/SC.md)
- [SC · POST /ServiceContract](endpoints/SC.md)
- [SC · PUT /ServiceContract](endpoints/SC.md)

### servicetokens

- [AUTHZ · DELETE /ServiceTokens](endpoints/AUTHZ.md)
- [AUTHZ · POST /ServiceTokens](endpoints/AUTHZ.md)

### sexes

- [PA · GET /Sexes](endpoints/PA.md) → PA:map<NameResult>

### skills

- [ADM · GET /Users/{userID}/skills](endpoints/ADM.md) → ADM:map<SkillResult>
- [ES · GET /AssetTemplates/{assetTemplateID}/skills](endpoints/ES.md) → ES:ResultsAssetTemplatesAssetTemplateSkillResult[]
- [ES · GET /Assets/{assetID}/skills](endpoints/ES.md) → ES:map<ResultsAssetSkillsAssetSkillResult>
- [PA · DELETE /Skills/{id}](endpoints/PA.md)
- [PA · DELETE /Skills](endpoints/PA.md)
- [PA · GET /Skills/{id}](endpoints/PA.md) → PA:RSGetResult
- [PA · GET /Skills](endpoints/PA.md) → PA:map<RSListResult>
- [PA · POST /Skills](endpoints/PA.md)
- [PA · PUT /Skills](endpoints/PA.md)
- [WORK · GET /Tasks/{taskID}/skills](endpoints/WORK.md) → WORK:map<TaskSkillResult>

### stages

- [WORK · GET /Tasks/stages/next](endpoints/WORK.md) → WORK:map<ListStagesResult>
- [WORK · GET /Tasks/{taskID}/stages/next](endpoints/WORK.md) → WORK:map<ListStagesResult>
- [WORK · GET /Tasks/{taskID}/stages](endpoints/WORK.md) → WORK:ListStagingHistoryResult

### subsystemview

- [UI · GET /SubsystemView/{subsystemID}](endpoints/UI.md) → UI:ProjectionsUISubsystemViewProjection[]
- [UI · GET /SubsystemView](endpoints/UI.md) → UI:ProjectionsUISubsystemViewProjection[]

### systempermissionuitags

- [ADM · GET /SystemPermissionUiTags](endpoints/ADM.md) → ADM:map<RPUTListResult[]>

### systemtags

- [COMMON · GET /SystemTags](endpoints/COMMON.md) → COMMON:IdNameResultOfShort[]

### tags

- [ADM · GET /Users/{userID}/tags](endpoints/ADM.md) → ADM:str[]
- [COMMON · GET /Tags](endpoints/COMMON.md) → COMMON:str[]
- [ES · GET /Assets/{assetID}/tags](endpoints/ES.md) → ES:str[]
- [WORK · GET /Tasks/{taskID}/tags](endpoints/WORK.md) → WORK:str[]

### taskactualities

- [WORK · DELETE /TaskActualities/{id}](endpoints/WORK.md)
- [WORK · DELETE /TaskActualities](endpoints/WORK.md)
- [WORK · GET /TaskActualities/{id}](endpoints/WORK.md) → WORK:TaskActualities.ListResult
- [WORK · GET /TaskActualities](endpoints/WORK.md) → WORK:map<TaskActualities.ListResult>
- [WORK · POST /TaskActualities](endpoints/WORK.md)
- [WORK · PUT /TaskActualities](endpoints/WORK.md)

### taskassignmenthistory

- [WORK · POST /TaskAssignmentHistory](endpoints/WORK.md)

### taskattachments

- [WORK · DELETE /TaskAttachments](endpoints/WORK.md)
- [WORK · POST /TaskAttachments/upload/fromBody](endpoints/WORK.md)
- [WORK · POST /TaskAttachments/upload/fromForm](endpoints/WORK.md)
- [WORK · POST /TaskAttachments](endpoints/WORK.md)

### taskattributes

- [WORK · GET /TaskAttributes](endpoints/WORK.md) → WORK:TaskAttributesResult[]
- [WORK · POST /TaskAttributes](endpoints/WORK.md)

### taskcontacts

- [WORK · DELETE /TaskContacts](endpoints/WORK.md)
- [WORK · POST /TaskContacts](endpoints/WORK.md)

### taskconversations

- [WORK · DELETE /TaskConversations/remove](endpoints/WORK.md)
- [WORK · DELETE /TaskConversations](endpoints/WORK.md)
- [WORK · GET /TaskConversations](endpoints/WORK.md) → WORK:TaskMessageLast[]
- [WORK · HEAD /TaskConversations](endpoints/WORK.md)

### taskfilter

- [WORK · GET /TaskFilter](endpoints/WORK.md) → WORK:FilterListItemProjection[]
- [WORK · PUT /TaskFilter](endpoints/WORK.md)

### tasklistqueries

- [ADM · GET /Users/this/taskListQueries](endpoints/ADM.md) → ADM:map<TaskListQueryResult>
- [ADM · GET /Users/{id}/taskListQueries](endpoints/ADM.md) → ADM:map<TaskListQueryResult>
- [WORK · DELETE /TaskListQueries/remove](endpoints/WORK.md)
- [WORK · DELETE /TaskListQueries/{id}/remove](endpoints/WORK.md)
- [WORK · DELETE /TaskListQueries/{id}](endpoints/WORK.md)
- [WORK · DELETE /TaskListQueries](endpoints/WORK.md)
- [WORK · GET /TaskListQueries/{id}](endpoints/WORK.md) → WORK:map<TaskListQueryResult>
- [WORK · GET /TaskListQueries](endpoints/WORK.md) → WORK:map<TaskListQueryResult>
- [WORK · POST /TaskListQueries](endpoints/WORK.md)
- [WORK · PUT /TaskListQueries](endpoints/WORK.md)

### taskmaterials

- [WORK · DELETE /TaskMaterials](endpoints/WORK.md)
- [WORK · POST /TaskMaterials](endpoints/WORK.md)
- [WORK · PUT /TaskMaterials/takeOff](endpoints/WORK.md)
- [WORK · PUT /TaskMaterials/takeOn](endpoints/WORK.md)
- [WORK · PUT /TaskMaterials](endpoints/WORK.md)

### taskorderby

- [WORK · GET /TaskOrderBy](endpoints/WORK.md) → WORK:map<TaskOrderBy.ListResult>

### taskratings

- [PA · GET /Technicians/{userID}/taskRatings](endpoints/PA.md) → PA:TaskRatingResult[]
- [WORK · POST /TaskRatings](endpoints/WORK.md)

### tasks

- [EXPORT · GET /Tasks/noData](endpoints/EXPORT.md)
- [EXPORT · GET /Tasks/v2.0](endpoints/EXPORT.md)
- [EXPORT · GET /Tasks](endpoints/EXPORT.md)
- [IMPORT · POST /Tasks](endpoints/IMPORT.md)
- [WORK · DELETE /Tasks/{taskID}/autoStaginging](endpoints/WORK.md)
- [WORK · DELETE /Tasks/{taskID}](endpoints/WORK.md)
- [WORK · DELETE /Tasks](endpoints/WORK.md)
- [WORK · GET /Tasks/changeTypes](endpoints/WORK.md) → WORK:ChangeTypeResult[]
- [WORK · GET /Tasks/count](endpoints/WORK.md) → WORK:map<ListCountResult>
- [WORK · GET /Tasks/short](endpoints/WORK.md) → WORK:map<ListShortResult>
- [WORK · GET /Tasks/{taskID}/checkCompanyCodeUsed](endpoints/WORK.md) → WORK:bool
- [WORK · GET /Tasks/{taskID}/meta](endpoints/WORK.md) → WORK:TaskTypeFormMetadataResult
- [WORK · GET /Tasks/{taskID}](endpoints/WORK.md) → WORK:DetailedInfoResult
- [WORK · GET /Tasks](endpoints/WORK.md) → WORK:map<Tasks.ListResult>
- [WORK · HEAD /Tasks](endpoints/WORK.md)
- [WORK · PATCH /Tasks/{taskID}](endpoints/WORK.md)
- [WORK · POST /Tasks/{taskID}/autoStaginging](endpoints/WORK.md)
- [WORK · POST /Tasks](endpoints/WORK.md)
- [WORK · PUT /Tasks/restore](endpoints/WORK.md)
- [WORK · PUT /Tasks/{taskID}/complete](endpoints/WORK.md)
- [WORK · PUT /Tasks/{taskID}](endpoints/WORK.md)

### tasksbyassets

- [REPORT · GET /TasksByAssets](endpoints/REPORT.md) → REPORT:ResultsTaskListGroupByAssetsTasksListGroupByAssetsResult[]

### tasksbyassignees

- [REPORT · GET /TasksByAssignees](endpoints/REPORT.md) → REPORT:ResultsTaskListGroupByAssigneesTaskListGroupByAssigneesResult[]

### tasksbycompanies

- [REPORT · GET /TasksByCompanies](endpoints/REPORT.md) → REPORT:ResultsTaskListGroupByCompaniesTaskListGroupByCompaniesResult[]

### tasksbystages

- [REPORT · GET /TasksByStages](endpoints/REPORT.md) → REPORT:ResultsTaskListGroupByStagesTaskListGroupByStagesResult[]

### tasksbyworktypes

- [REPORT · GET /TasksByWorkTypes](endpoints/REPORT.md) → REPORT:ResultsTaskListGroupByWorkTypesTaskListGroupByWorkTypesResult[]

### taskschedules

- [PA · GET /Technicians/taskSchedules](endpoints/PA.md) → PA:ScheduleTaskResult[]

### taskskills

- [WORK · DELETE /TaskSkills](endpoints/WORK.md)
- [WORK · POST /TaskSkills](endpoints/WORK.md)

### taskstagecomponents

- [TSTG · POST /TaskStageComponents](endpoints/TSTG.md)

### taskstagelinks

- [TSTG · DELETE /TaskStageLinks](endpoints/TSTG.md)
- [TSTG · GET /TaskStageLinks](endpoints/TSTG.md) → TSTG:RTSLListResult[]
- [TSTG · POST /TaskStageLinks/copy](endpoints/TSTG.md)
- [TSTG · POST /TaskStageLinks/reorder](endpoints/TSTG.md)
- [TSTG · POST /TaskStageLinks](endpoints/TSTG.md)
- [TSTG · PUT /TaskStageLinks](endpoints/TSTG.md)

### taskstagemessagetriggers

- [TSTG · POST /TaskStageMessageTriggers](endpoints/TSTG.md)

### taskstagerequirements

- [TSTG · POST /TaskStageRequirements](endpoints/TSTG.md)

### taskstages

- [TSTG · DELETE /TaskStages/{id}](endpoints/TSTG.md)
- [TSTG · DELETE /TaskStages](endpoints/TSTG.md)
- [TSTG · GET /TaskStages/{id}](endpoints/TSTG.md) → TSTG:RTSGetResult
- [TSTG · GET /TaskStages](endpoints/TSTG.md) → TSTG:map<RTSListResult>
- [TSTG · HEAD /TaskStages](endpoints/TSTG.md)
- [TSTG · POST /TaskStages/copy](endpoints/TSTG.md)
- [TSTG · POST /TaskStages/{id}/assign](endpoints/TSTG.md)
- [TSTG · POST /TaskStages](endpoints/TSTG.md)
- [TSTG · PUT /TaskStages](endpoints/TSTG.md)

### taskstaginghistory

- [WORK · POST /TaskStagingHistory/batch](endpoints/WORK.md)
- [WORK · POST /TaskStagingHistory/multiple](endpoints/WORK.md)
- [WORK · POST /TaskStagingHistory](endpoints/WORK.md)

### taskstatuses

- [WORK · DELETE /TaskStatuses/{id}](endpoints/WORK.md)
- [WORK · DELETE /TaskStatuses](endpoints/WORK.md)
- [WORK · GET /TaskStatuses/{id}](endpoints/WORK.md) → WORK:TaskStatuses.ListResult
- [WORK · GET /TaskStatuses](endpoints/WORK.md) → WORK:map<TaskStatuses.ListResult>
- [WORK · POST /TaskStatuses](endpoints/WORK.md)
- [WORK · PUT /TaskStatuses](endpoints/WORK.md)

### tasktags

- [WORK · DELETE /TaskTags](endpoints/WORK.md)
- [WORK · POST /TaskTags](endpoints/WORK.md)

### tasktemplateexcludedassets

- [WORK · DELETE /TaskTemplateExcludedAssets](endpoints/WORK.md)
- [WORK · POST /TaskTemplateExcludedAssets](endpoints/WORK.md)

### tasktemplates

- [PROXY · GET /TaskTemplates/{codeDynamicPart}](endpoints/PROXY.md)
- [WORK · DELETE /TaskTemplates](endpoints/WORK.md)
- [WORK · GET /TaskTemplates/download](endpoints/WORK.md)
- [WORK · GET /TaskTemplates/{id}/download](endpoints/WORK.md)
- [WORK · GET /TaskTemplates/{id}/public](endpoints/WORK.md) → WORK:GetPublicResult
- [WORK · GET /TaskTemplates/{id}](endpoints/WORK.md) → WORK:TaskTemplates.GetResult
- [WORK · GET /TaskTemplates](endpoints/WORK.md) → WORK:map<TaskTemplates.ListResult>
- [WORK · HEAD /TaskTemplates](endpoints/WORK.md)
- [WORK · POST /TaskTemplates](endpoints/WORK.md)
- [WORK · PUT /TaskTemplates/{id}/publish](endpoints/WORK.md)
- [WORK · PUT /TaskTemplates/{id}/unpublish](endpoints/WORK.md)
- [WORK · PUT /TaskTemplates](endpoints/WORK.md)

### tasktypedistrict

- [WORK · PUT /TaskTypeDistrict](endpoints/WORK.md)

### tasktyperoutes

- [WORK · DELETE /TaskTypeRoutes/{id}](endpoints/WORK.md)
- [WORK · DELETE /TaskTypeRoutes](endpoints/WORK.md)
- [WORK · POST /TaskTypeRoutes](endpoints/WORK.md)
- [WORK · PUT /TaskTypeRoutes](endpoints/WORK.md)

### tasktypes

- [UI · DELETE /LayoutTemplates/{id}/taskTypes](endpoints/UI.md)
- [UI · GET /LayoutTemplates/{id}/taskTypes](endpoints/UI.md) → UI:ApiDtoLayoutTaskTypeDto[]
- [UI · PUT /LayoutTemplates/{id}/taskTypes](endpoints/UI.md)
- [WORK · DELETE /TaskTypes/{id}](endpoints/WORK.md)
- [WORK · DELETE /TaskTypes](endpoints/WORK.md)
- [WORK · DELETE /WorkTypes/{id}/taskTypes](endpoints/WORK.md)
- [WORK · GET /TaskTypes/{id}](endpoints/WORK.md) → WORK:TaskTypes.ListResult
- [WORK · GET /TaskTypes](endpoints/WORK.md) → WORK:map<TaskTypes.ListResult>
- [WORK · GET /WorkTypes/{id}/taskTypes](endpoints/WORK.md) → WORK:IdNameEntity<Byte>[]
- [WORK · POST /TaskTypes](endpoints/WORK.md)
- [WORK · POST /WorkTypes/{id}/taskTypes](endpoints/WORK.md)
- [WORK · PUT /TaskTypes](endpoints/WORK.md)
- [WORK · PUT /TemplateQuickResponse/taskTypes](endpoints/WORK.md)

### taskviewtemplate

- [UI · GET /TaskViewTemplate](endpoints/UI.md) → UI:map<ResultsTaskViewTemplatesTaskViewTemplateResult>

### taskwatchlists

- [WORK · DELETE /TaskWatchLists](endpoints/WORK.md)
- [WORK · POST /TaskWatchLists](endpoints/WORK.md)

### technicians

- [WORK · DELETE /Tasks/completedWorks/technicians](endpoints/WORK.md)
- [WORK · DELETE /Tasks/{taskID}/completedWorks/{completedWorkID}/technicians](endpoints/WORK.md)
- [WORK · GET /Tasks/{taskID}/completedWorks/technicians](endpoints/WORK.md) → WORK:CompletedWorkTechnicianResult
- [WORK · GET /Tasks/{taskID}/completedWorks/{completedWorkID}/technicians](endpoints/WORK.md) → WORK:CompletedWorkTechnicianResult
- [WORK · POST /Tasks/completedWorks/technicians](endpoints/WORK.md)
- [WORK · PUT /Tasks/completedWorks/technicians](endpoints/WORK.md)

### templatequickresponse

- [WORK · DELETE /TemplateQuickResponse](endpoints/WORK.md)
- [WORK · GET /TemplateQuickResponse/{id}](endpoints/WORK.md) → WORK:TemplateQuickResponse.GetResult
- [WORK · GET /TemplateQuickResponse](endpoints/WORK.md) → WORK:map<TemplateQuickResponse.ListResult>
- [WORK · POST /TemplateQuickResponse](endpoints/WORK.md)
- [WORK · PUT /TemplateQuickResponse](endpoints/WORK.md)

### templates

- [ADM · GET /Tenants/templates](endpoints/ADM.md) → ADM:ITenantEntity[]
- [TSTG · POST /TaskStageComponents/templates](endpoints/TSTG.md)

### tenantcreationrequests

- [ADM · GET /TenantCreationRequests/{id}](endpoints/ADM.md) → ADM:RTCRGetResult
- [ADM · POST /TenantCreationRequests](endpoints/ADM.md)
- [ADM · PUT /TenantCreationRequests/{id}/approve](endpoints/ADM.md)
- [ADM · PUT /TenantCreationRequests/{id}/reject](endpoints/ADM.md)

### tenantmember

- [ES · DELETE /AssetSearchSettings/tenantMember](endpoints/ES.md)
- [ES · POST /AssetSearchSettings/tenantMember](endpoints/ES.md)

### tenantmembers

- [ADM · DELETE /TenantMembers/{tenantMemberID}](endpoints/ADM.md)
- [ADM · DELETE /TenantMembers](endpoints/ADM.md)
- [ADM · GET /TenantMembers/anonymousUser](endpoints/ADM.md) → ADM:RTMListResult
- [ADM · GET /TenantMembers/apiUser](endpoints/ADM.md) → ADM:RTMListResult
- [ADM · GET /TenantMembers/this](endpoints/ADM.md) → ADM:RTMGetResult
- [ADM · GET /TenantMembers/{tenantMemberID}](endpoints/ADM.md) → ADM:RTMGetResult
- [ADM · GET /TenantMembers](endpoints/ADM.md) → ADM:map<RTMListResult>
- [ADM · POST /TenantMembers](endpoints/ADM.md)
- [ADM · PUT /TenantMembers](endpoints/ADM.md)

### tenants

- [ADM · GET /Tenants/this/featureFlags](endpoints/ADM.md) → ADM:str[]
- [ADM · GET /Tenants/this/meta](endpoints/ADM.md)
- [ADM · GET /Tenants/this](endpoints/ADM.md) → ADM:RTGetResult
- [ADM · GET /Tenants](endpoints/ADM.md) → ADM:RTListResult[]

### tenantsettings

- [ADM · GET /TenantSettings/plateUrl](endpoints/ADM.md) → ADM:str
- [ADM · GET /TenantSettings](endpoints/ADM.md) → ADM:RTSGetResult
- [ADM · PUT /TenantSettings/plateUrl](endpoints/ADM.md)
- [PA · GET /TenantSettings](endpoints/PA.md) → PA:RTSGetResult

### timezones

- [COMMON · GET /Timezones/info](endpoints/COMMON.md) → COMMON:TimezoneGetResult
- [COMMON · GET /Timezones](endpoints/COMMON.md) → COMMON:map<RTListResult>

### tokens

- [AUTHZ · POST /Tokens/renew](endpoints/AUTHZ.md)

### transfers

- [WH · DELETE /Transfers/{id}](endpoints/WH.md)
- [WH · DELETE /Transfers](endpoints/WH.md)
- [WH · GET /Transfers/{id}](endpoints/WH.md) → WH:ResultsTransfersTransferResult
- [WH · GET /Transfers](endpoints/WH.md) → WH:map<ResultsTransfersTransferResult>
- [WH · HEAD /Transfers](endpoints/WH.md)
- [WH · POST /Transfers](endpoints/WH.md)
- [WH · PUT /Transfers/post](endpoints/WH.md)
- [WH · PUT /Transfers/restore](endpoints/WH.md)
- [WH · PUT /Transfers/unpost](endpoints/WH.md)
- [WH · PUT /Transfers/{id}/post](endpoints/WH.md)
- [WH · PUT /Transfers/{id}/restore](endpoints/WH.md)
- [WH · PUT /Transfers/{id}/unpost](endpoints/WH.md)
- [WH · PUT /Transfers](endpoints/WH.md)

### triggerrecipientselectionrules

- [MSG · POST /TriggerRecipientSelectionRules](endpoints/MSG.md)

### triggers

- [MSG · DELETE /Triggers/{id}](endpoints/MSG.md)
- [MSG · DELETE /Triggers](endpoints/MSG.md)
- [MSG · GET /Triggers/{id}](endpoints/MSG.md) → MSG:RTGetResult
- [MSG · GET /Triggers](endpoints/MSG.md) → MSG:map<RTListResult>
- [MSG · POST /Triggers](endpoints/MSG.md)
- [MSG · PUT /Triggers/activate](endpoints/MSG.md)
- [MSG · PUT /Triggers/deactivate](endpoints/MSG.md)
- [MSG · PUT /Triggers/{triggerID}/activate](endpoints/MSG.md)
- [MSG · PUT /Triggers/{triggerID}/deactivate](endpoints/MSG.md)
- [MSG · PUT /Triggers](endpoints/MSG.md)

### userassetlistqueries

- [ADM · DELETE /UserAssetListQueries/{userID}](endpoints/ADM.md)
- [ADM · DELETE /UserAssetListQueries](endpoints/ADM.md)
- [ADM · POST /UserAssetListQueries/{userID}](endpoints/ADM.md)
- [ADM · POST /UserAssetListQueries](endpoints/ADM.md)

### usercompanylistqueries

- [ADM · DELETE /UserCompanyListQueries/{userID}](endpoints/ADM.md)
- [ADM · DELETE /UserCompanyListQueries](endpoints/ADM.md)
- [ADM · POST /UserCompanyListQueries/{userID}](endpoints/ADM.md)
- [ADM · POST /UserCompanyListQueries](endpoints/ADM.md)

### userdisablednotifications

- [ADM · POST /UserDisabledNotifications](endpoints/ADM.md)

### userdistricts

- [ADM · DELETE /UserDistricts](endpoints/ADM.md)
- [ADM · POST /UserDistricts](endpoints/ADM.md)
- [ADM · PUT /UserDistricts](endpoints/ADM.md)

### usergroups

- [PA · GET /UserGroups](endpoints/PA.md) → PA:map<UserGroupResult>

### userorderby

- [ADM · GET /UserOrderBy](endpoints/ADM.md) → ADM:map<RUOBListResult>

### userroles

- [ADM · DELETE /UserRoles](endpoints/ADM.md)
- [ADM · POST /UserRoles](endpoints/ADM.md)

### users

- [ADM · DELETE /Users/{userID}](endpoints/ADM.md)
- [ADM · DELETE /Users](endpoints/ADM.md)
- [ADM · GET /Users/geolocation](endpoints/ADM.md) → ADM:UserGeolocationSettings[]
- [ADM · GET /Users/profile](endpoints/ADM.md) → ADM:UserProfileResult
- [ADM · GET /Users/relevance](endpoints/ADM.md) → ADM:map<RUUserResult>
- [ADM · GET /Users/short](endpoints/ADM.md) → ADM:map<UserShortResult>
- [ADM · GET /Users/this/geolocation](endpoints/ADM.md) → ADM:UserGeolocationSettings
- [ADM · GET /Users/this/profile](endpoints/ADM.md) → ADM:UserProfileResult
- [ADM · GET /Users/{id}/profile](endpoints/ADM.md) → ADM:UserProfileResult
- [ADM · GET /Users/{id}](endpoints/ADM.md) → ADM:DetailedInfoResult
- [ADM · GET /Users](endpoints/ADM.md) → ADM:map<RUUserResult>
- [ADM · HEAD /Users](endpoints/ADM.md)
- [ADM · POST /Users/addbyintegration](endpoints/ADM.md)
- [ADM · POST /Users/anonymous](endpoints/ADM.md)
- [ADM · POST /Users/api](endpoints/ADM.md)
- [ADM · POST /Users/changeToCustomer](endpoints/ADM.md)
- [ADM · POST /Users/changeToStaff](endpoints/ADM.md)
- [ADM · POST /Users/geolocation](endpoints/ADM.md)
- [ADM · POST /Users/{userID}/geolocation](endpoints/ADM.md)
- [ADM · POST /Users](endpoints/ADM.md)
- [ADM · PUT /Users/geolocation](endpoints/ADM.md)
- [ADM · PUT /Users/restore](endpoints/ADM.md)
- [ADM · PUT /Users/{id}](endpoints/ADM.md)
- [ADM · PUT /Users/{userID}/geolocation](endpoints/ADM.md)
- [ADM · PUT /Users/{userID}/resendinvitation](endpoints/ADM.md)
- [ADM · PUT /Users/{userID}/restore](endpoints/ADM.md)
- [EXPORT · GET /Users](endpoints/EXPORT.md)
- [IMPORT · POST /Users](endpoints/IMPORT.md)
- [UI · GET /UserViews/Users/{id}](endpoints/UI.md) → UI:ProjectionsUITaskViewProjection[]
- [WH · DELETE /Warehouses/users](endpoints/WH.md)
- [WH · DELETE /Warehouses/{id}/users](endpoints/WH.md)
- [WH · GET /Warehouses/{id}/users](endpoints/WH.md) → WH:ResultsWarehouseUsersWarehouseUserListResult[]
- [WH · POST /Warehouses/users](endpoints/WH.md)
- [WH · POST /Warehouses/{id}/users](endpoints/WH.md)

### userskills

- [PA · DELETE /UserSkills](endpoints/PA.md)
- [PA · POST /UserSkills](endpoints/PA.md)
- [PA · PUT /UserSkills](endpoints/PA.md)

### usertags

- [ADM · DELETE /UserTags](endpoints/ADM.md)
- [ADM · POST /UserTags](endpoints/ADM.md)

### usertaskfavourites

- [WORK · DELETE /UserTaskFavourites](endpoints/WORK.md)
- [WORK · POST /UserTaskFavourites](endpoints/WORK.md)

### usertasklistqueries

- [ADM · DELETE /UserTaskListQueries](endpoints/ADM.md)
- [ADM · POST /UserTaskListQueries](endpoints/ADM.md)

### usertemplatedistricts

- [ADM · DELETE /UserTemplateDistricts/remove](endpoints/ADM.md)
- [ADM · POST /UserTemplateDistricts](endpoints/ADM.md)

### usertemplateroles

- [ADM · DELETE /UserTemplateRoles/remove](endpoints/ADM.md)
- [ADM · POST /UserTemplateRoles](endpoints/ADM.md)

### usertemplates

- [ADM · DELETE /UserTemplates/{id}](endpoints/ADM.md)
- [ADM · DELETE /UserTemplates](endpoints/ADM.md)
- [ADM · GET /UserTemplates/{id}](endpoints/ADM.md) → ADM:RUTGetResult
- [ADM · GET /UserTemplates](endpoints/ADM.md) → ADM:map<RUTListResult>
- [ADM · POST /UserTemplates](endpoints/ADM.md)
- [ADM · PUT /UserTemplates](endpoints/ADM.md)

### userwarehouses

- [ADM · DELETE /UserWarehouses](endpoints/ADM.md)
- [ADM · POST /UserWarehouses](endpoints/ADM.md)
- [WH · DELETE /UserWarehouses/{id}](endpoints/WH.md)
- [WH · DELETE /UserWarehouses](endpoints/WH.md)
- [WH · GET /UserWarehouses/{id}](endpoints/WH.md) → WH:ResultsWarehouseUsersUserWarehouseListResult[]
- [WH · POST /UserWarehouses/{id}](endpoints/WH.md)
- [WH · POST /UserWarehouses](endpoints/WH.md)

### variables

- [ADM · DELETE /Tenants/this/variables/{name}](endpoints/ADM.md)
- [ADM · DELETE /Tenants/this/variables](endpoints/ADM.md)
- [ADM · GET /Tenants/this/variables](endpoints/ADM.md) → ADM:map<RTVListResult>
- [ADM · POST /Tenants/this/variables](endpoints/ADM.md)
- [ADM · PUT /Tenants/this/variables](endpoints/ADM.md)

### verificationcodes

- [AUTH · POST /VerificationCodes/check](endpoints/AUTH.md)

### warehouses

- [ADM · GET /Users/{id}/warehouses](endpoints/ADM.md) → ADM:IdNameErpIDResultOfShort[]
- [WH · DELETE /Warehouses/{id}](endpoints/WH.md)
- [WH · DELETE /Warehouses](endpoints/WH.md)
- [WH · GET /Warehouses/V2](endpoints/WH.md) → WH:map<ResultsWarehousesListResult>
- [WH · GET /Warehouses/short](endpoints/WH.md) → WH:map<ResultsWarehousesListShortResult>
- [WH · GET /Warehouses/{id}](endpoints/WH.md) → WH:ResultsWarehousesGetResult
- [WH · GET /Warehouses](endpoints/WH.md) → WH:map<ResultsWarehousesListShortResult>
- [WH · HEAD /Warehouses](endpoints/WH.md) → WH:map<ResultsWarehousesListResult>
- [WH · POST /Warehouses](endpoints/WH.md)
- [WH · PUT /Warehouses/restore](endpoints/WH.md)
- [WH · PUT /Warehouses/{id}/restore](endpoints/WH.md)
- [WH · PUT /Warehouses](endpoints/WH.md)

### watchlists

- [WORK · GET /Tasks/{taskID}/watchLists](endpoints/WORK.md) → WORK:TaskWatchLists.ListResult[]

### webhooks

- [MSG · DELETE /Webhooks/{id}](endpoints/MSG.md)
- [MSG · DELETE /Webhooks](endpoints/MSG.md)
- [MSG · GET /Webhooks/{id}](endpoints/MSG.md) → MSG:RWGetResult
- [MSG · GET /Webhooks](endpoints/MSG.md) → MSG:map<RWListResult>
- [MSG · POST /Webhooks](endpoints/MSG.md)
- [MSG · PUT /Webhooks/activate/{id}](endpoints/MSG.md)
- [MSG · PUT /Webhooks/activate](endpoints/MSG.md)
- [MSG · PUT /Webhooks/deactivate/{id}](endpoints/MSG.md)
- [MSG · PUT /Webhooks/deactivate](endpoints/MSG.md)

### workingtime

- [REPORT · GET /WorkingTime](endpoints/REPORT.md) → REPORT:ResultsWorkingTimeWorkingTimeResult[]

### workschedules

- [PA · GET /Technicians/{userID}/workSchedules](endpoints/PA.md) → PA:map<WorkScheduleResult>
- [WSP · GET /WorkSchedules/daily](endpoints/WSP.md) → WSP:map<WorkScheduleDailyItemResult[]>
- [WSP · GET /WorkSchedules](endpoints/WSP.md) → WSP:map<WorkScheduleDailyItemResult>

### worktypes

- [ES · DELETE /AssetTypes/{id}/workTypes](endpoints/ES.md)
- [ES · GET /AssetTemplates/{assetTemplateID}/workTypes](endpoints/ES.md) → ES:ResultsAssetTemplatesAssetTemplateWorkTypeResult[]
- [ES · GET /AssetTypes/{id}/workTypes](endpoints/ES.md) → ES:map<str>
- [ES · GET /Assets/{assetID}/workTypes](endpoints/ES.md) → ES:map<ResultsAssetsAssetWorkTypeResult>
- [ES · POST /AssetTypes/{id}/workTypes](endpoints/ES.md)
- [PA · DELETE /Users/{userID}/workTypes](endpoints/PA.md)
- [PA · GET /Users/{userID}/workTypes](endpoints/PA.md) → PA:map<WorkTypesListResult[]>
- [PA · POST /Users/{userID}/workTypes](endpoints/PA.md)
- [WORK · DELETE /TaskTypes/{id}/workTypes](endpoints/WORK.md)
- [WORK · DELETE /WorkTypes/{id}](endpoints/WORK.md)
- [WORK · DELETE /WorkTypes](endpoints/WORK.md)
- [WORK · GET /TaskTypes/{id}/workTypes](endpoints/WORK.md) → WORK:IdNameEntity<Int16>[]
- [WORK · GET /WorkTypes/{id}](endpoints/WORK.md) → WORK:WorkTypes.GetResult
- [WORK · GET /WorkTypes/{parentWorkTypeID}/workTypes/all](endpoints/WORK.md) → WORK:map<WorkTypes.ListResult>
- [WORK · GET /WorkTypes/{parentWorkTypeID}/workTypes](endpoints/WORK.md) → WORK:map<WorkTypes.ListResult>
- [WORK · GET /WorkTypes](endpoints/WORK.md) → WORK:map<WorkTypes.ListResult>
- [WORK · POST /TaskTypes/{id}/workTypes](endpoints/WORK.md)
- [WORK · POST /WorkTypes](endpoints/WORK.md)
- [WORK · PUT /WorkTypes/publish](endpoints/WORK.md)
- [WORK · PUT /WorkTypes/unpublish](endpoints/WORK.md)
- [WORK · PUT /WorkTypes/{id}/publish](endpoints/WORK.md)
- [WORK · PUT /WorkTypes/{id}/unpublish](endpoints/WORK.md)
- [WORK · PUT /WorkTypes](endpoints/WORK.md)

