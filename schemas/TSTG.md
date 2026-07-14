# TSTG — схемы

> **Что здесь:** определения типов запросов/ответов сервиса TSTG. Ручки, ссылающиеся на них — `endpoints/TSTG.md`.
> **Источник:** `snapshots/TSTG.json` · файл генерируется пайплайном — руками не править.

```
type ActionResult map
type AssigneeSelectionRule.AddData { name: str, requiredSkillRatio?: float, optionalSkillRatio?: float, workTypeRatio?: float, preffereableRatio?: float, managerRatio?: float, assetResponsibilityRatio?: float, customerRatio?: float, districtRatio?: float, oftenAssignedRatio?: float, workScheduleRatio?: float }
type AssigneeSelectionRule.GetResult { name?: str /* Название правила */, requiredSkillRatio?: float /* Коэффициент обязательных навыков */, optionalSkillRatio?: float /* Коэффициент опциональных навыков */, workTypeRatio?: float /* Коэффициент учета видов работ */, preffereableRatio?: float /* Коэффициент учета предпочтительного инженера */, managerRatio?: float /* Коэффициент  учета руководителя */, assetResponsibilityRatio?: float /* Коэффициент учета отв. по объекту */, customerRatio?: float /* Коэффициент учета заказчика */, districtRatio?: float /* Коэффициент учета заказчика */, oftenAssignedRatio?: float /* Коэффициент учета того, как часто назначается на объект */, workScheduleRatio?: float /* Коэффициент учета расписания */, id?: int /* Идентификатор правила */, deleted?: datetime /* TenantMemberID, который проставил флаг "удалено" */ }
type AssigneeSelectionRule.ListResult { name?: str /* Название правила */, requiredSkillRatio?: float /* Коэффициент обязательных навыков */, optionalSkillRatio?: float /* Коэффициент опциональных навыков */, workTypeRatio?: float /* Коэффициент учета видов работ */, preffereableRatio?: float /* Коэффициент учета предпочтительного инженера */, managerRatio?: float /* Коэффициент  учета руководителя */, assetResponsibilityRatio?: float /* Коэффициент учета отв. по объекту */, customerRatio?: float /* Коэффициент учета заказчика */, districtRatio?: float /* Коэффициент учета заказчика */, oftenAssignedRatio?: float /* Коэффициент учета того, как часто назначается на объект */, workScheduleRatio?: float /* Коэффициент учета расписания */ }
type AssigneeSelectionRule.UpdateData { name: str, requiredSkillRatio?: float, optionalSkillRatio?: float, workTypeRatio?: float, preffereableRatio?: float, managerRatio?: float, assetResponsibilityRatio?: float, customerRatio?: float, districtRatio?: float, oftenAssignedRatio?: float, workScheduleRatio?: float, id: int }
type AttributeResult { id?: int /* Идентификатор атрибута */, name?: str /* Наименование атрибута */, type?: AttributeTypeResult }
type AttributeTypeResult { code?: str /* Код типа атрибута */, name?: str /* Наименование типа атрибута */ }
type AvailabilityAttributeResult { attribute?: AttributeResult, availability?: AvailabilityResult }
type AvailabilityComponentResult { component?: ComponentResult, availability?: AvailabilityResult }
type AvailabilityListResult { components?: AvailabilityComponentResult[] /* Информация о компонентах */, attributes?: AvailabilityAttributeResult[] /* Информация о атрибутах */ }
type AvailabilityResult { taskStageID?: int /* Идентификатор стадии */, taskTypes?: int[] /* Идентификатор типа заявки */, roleID?: int /* Идентификатор роли */, capabilityID?: int /* Идентификатор возможности */ }
type BaseData { id: int, roleID: int, capabilityID?: int, permissionUiID?: int }
type BranchResult { nameRu?: str /* ;
            Название */, isExclusiveMode?: bool /* Флаг эксклюзивности */, color?: str /* Цвет ветки жизненного цикла */ }
type ComponentResult { id?: int /* Идентификатор компонента */, code?: str /* Код компонента */, description?: str /* Описание компонента */ }
type ErrorModel { traceIdentifier?: str, code?: str, message?: str, arguments?: map<str> }
type IdNameDescriptionResult<Int16> { id?: int, name?: str, description?: str }
type IdNameResult<Byte> { id?: int, name?: str }
type IdNameResult<Int16> { id?: int, name?: str }
type IdNameResult<Int32> { id?: int, name?: str }
type OverrideListResult { taskTypeID?: int /* Идентификатор типа заявки */, fromTaskStage?: IdNameResult<Int16>, toTaskStage?: IdNameResult<Int16>, name?: str /* Название */, description?: str /* Описание */, isPositiveResult?: bool /* Результат перехода */, role?: IdNameResult<Int16> }
type RequirementMergeData { id: int, argumentsJson?: str }
type Requirements.ListResult { code?: str /* Код требования */, name?: str /* Название тербования */, description?: str /* Описание требования */ }
type SortData { taskTypeID: int, fromTaskStageID: int, toTaskStageID: int, sortOrder: int }
type TaskStage.AddData { color: str, taskViewTemplateID: int, name: str, description?: str, actionID?: int, assigneeSelectionRuleID?: int, assignToUserID?: int, assignToRoleID?: int, isShowTechnicianOnMap?: bool }
type TaskStage.CopyData { sourceID?: int, name?: str, description?: str }
type TaskStage.UpdateData { color: str, taskViewTemplateID: int, name: str, description?: str, actionID?: int, assigneeSelectionRuleID?: int, assignToUserID?: int, assignToRoleID?: int, isShowTechnicianOnMap?: bool, id?: int }
type TaskStageComponent.MergeData { taskStageID?: int, taskTypeID?: int, components?: BaseData[], attributes?: BaseData[] }
type TaskStageLink.AddData { taskTypeID: int, fromTaskStageID: int, toTaskStageID: int, name?: str, description?: str, isPositiveResult?: bool, timeoutSeconds?: int, timeoutToDeadlineSeconds?: int, branchID: int, applyTaskStatusID?: int, roles?: int[], sortOrder?: int }
type TaskStageLink.CopyData { sourceTaskTypeID: int, targetTaskTypeID: int }
type TaskStageLink.DeleteData { taskTypeID: int, fromTaskStageID: int, toTaskStageID: int }
type TaskStageLink.UpdateData { taskTypeID: int, fromTaskStageID: int, toTaskStageID: int, name?: str, description?: str, isPositiveResult?: bool, timeoutSeconds?: int, timeoutToDeadlineSeconds?: int, branchID: int, applyTaskStatusID?: int, roles?: int[], sortOrder?: int }
type TaskStageLinkOverride.AddData { taskTypeID: int, fromTaskStageID: int, toTaskStageID: int, roles: int[], name?: str, description?: str, isPositiveResult?: bool }
type TaskStageLinkOverride.DeleteData { taskTypeID: int, fromTaskStageID: int, toTaskStageID: int, roles: int[] }
type TaskStageLinkOverride.UpdateData { taskTypeID: int, fromTaskStageID: int, toTaskStageID: int, roles: int[], name?: str, description?: str, isPositiveResult?: bool }
type TaskStageLinks.ListResult { taskTypeID?: int /* Идентификатор типа заявки */, fromTaskStage?: IdNameResult<Int16>, toTaskStage?: IdNameResult<Int16>, taskStatus?: IdNameResult<Byte>, branch?: IdNameResult<Byte>, name?: str /* Название */, description?: str /* Описание */, isPositiveResult?: bool /* Результат перехода */, permissionUiID?: int /* Идентификатор связанного с переходом UI-полномочия */, sortOrder?: int /* Номер для сортировки */, timeoutSeconds?: int /* Количество секунд до автоматического перехода */, timeoutToDeadlineSeconds?: int /* Количество секунд до делайна при автоматического переходе в зависимости от него */, roles?: IdNameDescriptionResult<Int16>[] }
type TaskStageMessageTrigger.MergeData { messageTriggers?: int[] }
type TaskStageRequirement.MergeData { data: RequirementMergeData[], taskStageID: int }
type TaskStageRequirementResult { taskStageID?: int /* Идентифкатор стадии заявки */, requirementID?: int /* Идентификатор требования */, requirementName?: str /* Имя требования */ }
type TaskStages.GetResult { id?: int, name?: str, description?: str, color?: str /* Цвет стадии заявки */, messageTriggerCount?: int /* Количество триггеров уведомлений, связанных со стадией */, taskViewTemplate?: IdNameResult<Byte>, action?: IdNameResult<Byte>, assigneeSelectionRule?: IdNameResult<Byte>, assignToUser?: IdNameResult<Int32>, assignToRole?: IdNameResult<Int32>, isShowTechnicianOnMap?: bool /* Признак видимости сотрудника на карте */, deleted?: datetime /* Признак удаления элемента */, requirements?: IdNameResult<Int16>[] /* Требования */, messageTriggers?: IdNameResult<Int16>[] /* Триггеры сообщений */ }
type TaskStages.ListResult { id?: int, name?: str, description?: str, color?: str /* Цвет стадии заявки */, messageTriggerCount?: int /* Количество триггеров уведомлений, связанных со стадией */, taskViewTemplate?: IdNameResult<Byte>, action?: IdNameResult<Byte>, assigneeSelectionRule?: IdNameResult<Byte>, assignToUser?: IdNameResult<Int32>, assignToRole?: IdNameResult<Int32>, isShowTechnicianOnMap?: bool /* Признак видимости сотрудника на карте */, deleted?: datetime /* Признак удаления элемента */ }
type TemplateMergeData { taskStageID: int, taskTypeID: int, taskViewTemplateID: int }
type TriggerTaskStage.MergeData { triggerID: int, data?: int[] }
```
