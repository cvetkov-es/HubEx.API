# TSTG — схемы

> **Что здесь:** определения типов запросов/ответов сервиса TSTG. Ручки, ссылающиеся на них — `endpoints/TSTG.md`.

```
type ActionsResult { code?: str /* Код в системе */, name?: str /* Имя действия */ }
type AttributeResult { id?: int /* Идентификатор атрибута */, name?: str /* Наименование атрибута */, type?: AttributeTypeResult }
type AttributeTypeResult { code?: str /* Код типа атрибута */, name?: str /* Наименование типа атрибута */ }
type AvailabilityAttributeResult { attribute?: AttributeResult, availability?: AvailabilityResult }
type AvailabilityComponentResult { availability?: AvailabilityResult, component?: ComponentResult }
type AvailabilityListResult { attributes?: AvailabilityAttributeResult[] /* Информация о атрибутах */, components?: AvailabilityComponentResult[] /* Информация о компонентах */ }
type AvailabilityResult { capabilityID?: int /* Идентификатор возможности */, roleID?: int /* Идентификатор роли */, taskStageID?: int /* Идентификатор стадии */, taskTypes?: int[] /* Идентификатор типа заявки */ }
type BranchResult { color?: str /* Цвет ветки жизненного цикла */, isExclusiveMode?: bool /* Флаг эксклюзивности */, nameRu?: str /* Название */ }
type ComponentResult { code?: str /* Код компонента */, description?: str /* Описание компонента */, id?: int /* Идентификатор компонента */ }
type ErrorModel { arguments?: map<str>, code?: str, message?: str, traceIdentifier?: str }
type IdNameDescriptionResultOfShort { description?: str, id?: int, name?: str }
type IdNameResultOfByte { id?: int, name?: str }
type IdNameResultOfInt { id?: int, name?: str }
type IdNameResultOfShort { id?: int, name?: str }
type MSGTTSMergeData { data?: int[], triggerID: int }
type OverrideListResult { description?: str /* Описание */, fromTaskStage?: IdNameResultOfShort, isPositiveResult?: bool /* Результат перехода */, name?: str /* Название */, role?: IdNameResultOfShort, taskTypeID?: int /* Идентификатор типа заявки */, toTaskStage?: IdNameResultOfShort }
type RASRGetResult { assetResponsibilityRatio?: float /* Коэффициент учета отв. по объекту */, customerRatio?: float /* Коэффициент учета заказчика */, deleted?: datetime /* TenantMemberID, который проставил флаг "удалено" */, districtRatio?: float /* Коэффициент учета района */, id?: int /* Идентификатор правила */, managerRatio?: float /* Коэффициент учета руководителя */, name?: str /* Название правила */, oftenAssignedRatio?: float /* Коэффициент учета того, как часто назначается на объект */, optionalSkillRatio?: float /* Коэффициент опциональных навыков */, preffereableRatio?: float /* Коэффициент учета предпочтительного инженера */, requiredSkillRatio?: float /* Коэффициент обязательных навыков */, workScheduleRatio?: float /* Коэффициент учета расписания */, workTypeRatio?: float /* Коэффициент учета видов работ */ }
type RASRListResult { assetResponsibilityRatio?: float /* Коэффициент учета отв. по объекту */, customerRatio?: float /* Коэффициент учета заказчика */, districtRatio?: float /* Коэффициент учета района */, managerRatio?: float /* Коэффициент учета руководителя */, name?: str /* Название правила */, oftenAssignedRatio?: float /* Коэффициент учета того, как часто назначается на объект */, optionalSkillRatio?: float /* Коэффициент опциональных навыков */, preffereableRatio?: float /* Коэффициент учета предпочтительного инженера */, requiredSkillRatio?: float /* Коэффициент обязательных навыков */, workScheduleRatio?: float /* Коэффициент учета расписания */, workTypeRatio?: float /* Коэффициент учета видов работ */ }
type RequirementMergeData { argumentsJson?: str, id: int }
type RRListResult { code?: str /* Код требования */, description?: str /* Описание требования */, name?: str /* Название требования */ }
type RTSGetResult { action?: IdNameResultOfByte, assignToRole?: IdNameResultOfInt, assignToUser?: IdNameResultOfInt, assigneeSelectionRule?: IdNameResultOfByte, color?: str /* Цвет стадии заявки */, deleted?: datetime /* Признак удаления элемента */, description?: str, id?: int, isShowTechnicianOnMap?: bool /* Признак видимости сотрудника на карте */, messageTriggerCount?: int /* Количество триггеров уведомлений, связанных со стадией */, messageTriggers?: IdNameResultOfShort[] /* Триггеры сообщений */, name?: str, requirements?: IdNameResultOfShort[] /* Требования */, taskViewTemplate?: IdNameResultOfByte }
type RTSListResult { action?: IdNameResultOfByte, assignToRole?: IdNameResultOfInt, assignToUser?: IdNameResultOfInt, assigneeSelectionRule?: IdNameResultOfByte, color?: str /* Цвет стадии заявки */, deleted?: datetime /* Признак удаления элемента */, description?: str, id?: int, isShowTechnicianOnMap?: bool /* Признак видимости сотрудника на карте */, messageTriggerCount?: int /* Количество триггеров уведомлений, связанных со стадией */, name?: str, taskViewTemplate?: IdNameResultOfByte }
type RTSLListResult { branch?: IdNameResultOfByte, description?: str /* Описание */, fromTaskStage?: IdNameResultOfShort, isPositiveResult?: bool /* Результат перехода */, name?: str /* Название */, permissionUiID?: int /* Идентификатор связанного с переходом UI-полномочия */, roles?: IdNameDescriptionResultOfShort[], sortOrder?: int /* Номер для сортировки */, taskStatus?: IdNameResultOfByte, taskTypeID?: int /* Идентификатор типа заявки */, timeoutSeconds?: int /* Количество секунд до автоматического перехода */, timeoutToDeadlineSeconds?: int /* Количество секунд до дедлайна при автоматическом переходе в зависимости от него */, toTaskStage?: IdNameResultOfShort }
type TaskStageRequirementResult { requirementID?: int /* Идентификатор требования */, requirementName?: str /* Имя требования */, taskStageID?: int /* Идентификатор стадии заявки */ }
type TemplateMergeData { taskStageID: int, taskTypeID: int, taskViewTemplateID: int }
type TSCBBaseData { capabilityID?: int, id: int, permissionUiID?: int, roleID: int }
type TSTGASRAddData { assetResponsibilityRatio?: float, customerRatio?: float, districtRatio?: float, managerRatio?: float, name: str, oftenAssignedRatio?: float, optionalSkillRatio?: float, preffereableRatio?: float, requiredSkillRatio?: float, workScheduleRatio?: float, workTypeRatio?: float }
type TSTGASRUpdateData { assetResponsibilityRatio?: float, customerRatio?: float, districtRatio?: float, id: int, managerRatio?: float, name: str, oftenAssignedRatio?: float, optionalSkillRatio?: float, preffereableRatio?: float, requiredSkillRatio?: float, workScheduleRatio?: float, workTypeRatio?: float }
type TSTGTSAddData { actionID?: int, assignToRoleID?: int, assignToUserID?: int, assigneeSelectionRuleID?: int, color: str, description?: str, isShowTechnicianOnMap?: bool, name: str, taskViewTemplateID: int }
type TSTGTSCMergeData { attributes?: TSCBBaseData[], components?: TSCBBaseData[], taskStageID?: int, taskTypeID?: int }
type TSTGTSCopyData { description?: str, name?: str, sourceID?: int }
type TSTGTSLAddData { applyTaskStatusID?: int, branchID: int, description?: str, fromTaskStageID: int, isPositiveResult?: bool, name?: str, roles?: int[], sortOrder?: int, taskTypeID: int, timeoutSeconds?: int, timeoutToDeadlineSeconds?: int, toTaskStageID: int }
type TSTGTSLCopyData { sourceTaskTypeID: int, targetTaskTypeID: int }
type TSTGTSLDeleteData { fromTaskStageID: int, taskTypeID: int, toTaskStageID: int }
type TSTGTSLOAddData { description?: str, fromTaskStageID: int, isPositiveResult?: bool, name?: str, roles: int[], taskTypeID: int, toTaskStageID: int }
type TSTGTSLODeleteData { fromTaskStageID: int, roles: int[], taskTypeID: int, toTaskStageID: int }
type TSTGTSLOUpdateData { description?: str, fromTaskStageID: int, isPositiveResult?: bool, name?: str, roles: int[], taskTypeID: int, toTaskStageID: int }
type TSTGTSLSortData { fromTaskStageID: int, sortOrder: int, taskTypeID: int, toTaskStageID: int }
type TSTGTSLUpdateData { applyTaskStatusID?: int, branchID: int, description?: str, fromTaskStageID: int, isPositiveResult?: bool, name?: str, roles?: int[], sortOrder?: int, taskTypeID: int, timeoutSeconds?: int, timeoutToDeadlineSeconds?: int, toTaskStageID: int }
type TSTGTSMTMergeData { messageTriggers?: int[] }
type TSTGTSRMergeData { data: RequirementMergeData[], taskStageID: int }
type TSTGTSUpdateData { actionID?: int, assignToRoleID?: int, assignToUserID?: int, assigneeSelectionRuleID?: int, color: str, description?: str, id?: int, isShowTechnicianOnMap?: bool, name: str, taskViewTemplateID: int }
```
