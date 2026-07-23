# TSTG — схемы

> **Что здесь:** определения типов запросов/ответов сервиса TSTG. Ручки, ссылающиеся на них — `endpoints/TSTG.md`.

```
type ActionResult map
type AssigneeSelectionRule.AddData { assetResponsibilityRatio?: float, customerRatio?: float, districtRatio?: float, managerRatio?: float, name: str, oftenAssignedRatio?: float, optionalSkillRatio?: float, preffereableRatio?: float, requiredSkillRatio?: float, workScheduleRatio?: float, workTypeRatio?: float }
type AssigneeSelectionRule.GetResult { assetResponsibilityRatio?: float /* Коэффициент учета отв. по объекту */, customerRatio?: float /* Коэффициент учета заказчика */, deleted?: datetime /* TenantMemberID, который проставил флаг "удалено" */, districtRatio?: float /* Коэффициент учета заказчика */, id?: int /* Идентификатор правила */, managerRatio?: float /* Коэффициент  учета руководителя */, name?: str /* Название правила */, oftenAssignedRatio?: float /* Коэффициент учета того, как часто назначается на объект */, optionalSkillRatio?: float /* Коэффициент опциональных навыков */, preffereableRatio?: float /* Коэффициент учета предпочтительного инженера */, requiredSkillRatio?: float /* Коэффициент обязательных навыков */, workScheduleRatio?: float /* Коэффициент учета расписания */, workTypeRatio?: float /* Коэффициент учета видов работ */ }
type AssigneeSelectionRule.ListResult { assetResponsibilityRatio?: float /* Коэффициент учета отв. по объекту */, customerRatio?: float /* Коэффициент учета заказчика */, districtRatio?: float /* Коэффициент учета заказчика */, managerRatio?: float /* Коэффициент  учета руководителя */, name?: str /* Название правила */, oftenAssignedRatio?: float /* Коэффициент учета того, как часто назначается на объект */, optionalSkillRatio?: float /* Коэффициент опциональных навыков */, preffereableRatio?: float /* Коэффициент учета предпочтительного инженера */, requiredSkillRatio?: float /* Коэффициент обязательных навыков */, workScheduleRatio?: float /* Коэффициент учета расписания */, workTypeRatio?: float /* Коэффициент учета видов работ */ }
type AssigneeSelectionRule.UpdateData { assetResponsibilityRatio?: float, customerRatio?: float, districtRatio?: float, id: int, managerRatio?: float, name: str, oftenAssignedRatio?: float, optionalSkillRatio?: float, preffereableRatio?: float, requiredSkillRatio?: float, workScheduleRatio?: float, workTypeRatio?: float }
type AttributeResult { id?: int /* Идентификатор атрибута */, name?: str /* Наименование атрибута */, type?: AttributeTypeResult }
type AttributeTypeResult { code?: str /* Код типа атрибута */, name?: str /* Наименование типа атрибута */ }
type AvailabilityAttributeResult { attribute?: AttributeResult, availability?: AvailabilityResult }
type AvailabilityComponentResult { availability?: AvailabilityResult, component?: ComponentResult }
type AvailabilityListResult { attributes?: AvailabilityAttributeResult[] /* Информация о атрибутах */, components?: AvailabilityComponentResult[] /* Информация о компонентах */ }
type AvailabilityResult { capabilityID?: int /* Идентификатор возможности */, roleID?: int /* Идентификатор роли */, taskStageID?: int /* Идентификатор стадии */, taskTypes?: int[] /* Идентификатор типа заявки */ }
type BaseData { capabilityID?: int, id: int, permissionUiID?: int, roleID: int }
type BranchResult { color?: str /* Цвет ветки жизненного цикла */, isExclusiveMode?: bool /* Флаг эксклюзивности */, nameRu?: str /* ;
            Название */ }
type ComponentResult { code?: str /* Код компонента */, description?: str /* Описание компонента */, id?: int /* Идентификатор компонента */ }
type ErrorModel { arguments?: map<str>, code?: str, message?: str, traceIdentifier?: str }
type IdNameDescriptionResult<Int16> { description?: str, id?: int, name?: str }
type IdNameResult<Byte> { id?: int, name?: str }
type IdNameResult<Int16> { id?: int, name?: str }
type IdNameResult<Int32> { id?: int, name?: str }
type OverrideListResult { description?: str /* Описание */, fromTaskStage?: IdNameResult<Int16>, isPositiveResult?: bool /* Результат перехода */, name?: str /* Название */, role?: IdNameResult<Int16>, taskTypeID?: int /* Идентификатор типа заявки */, toTaskStage?: IdNameResult<Int16> }
type RequirementMergeData { argumentsJson?: str, id: int }
type Requirements.ListResult { code?: str /* Код требования */, description?: str /* Описание требования */, name?: str /* Название тербования */ }
type SortData { fromTaskStageID: int, sortOrder: int, taskTypeID: int, toTaskStageID: int }
type TaskStage.AddData { actionID?: int, assignToRoleID?: int, assignToUserID?: int, assigneeSelectionRuleID?: int, color: str, description?: str, isShowTechnicianOnMap?: bool, name: str, taskViewTemplateID: int }
type TaskStage.CopyData { description?: str, name?: str, sourceID?: int }
type TaskStage.UpdateData { actionID?: int, assignToRoleID?: int, assignToUserID?: int, assigneeSelectionRuleID?: int, color: str, description?: str, id?: int, isShowTechnicianOnMap?: bool, name: str, taskViewTemplateID: int }
type TaskStageComponent.MergeData { attributes?: BaseData[], components?: BaseData[], taskStageID?: int, taskTypeID?: int }
type TaskStageLink.AddData { applyTaskStatusID?: int, branchID: int, description?: str, fromTaskStageID: int, isPositiveResult?: bool, name?: str, roles?: int[], sortOrder?: int, taskTypeID: int, timeoutSeconds?: int, timeoutToDeadlineSeconds?: int, toTaskStageID: int }
type TaskStageLink.CopyData { sourceTaskTypeID: int, targetTaskTypeID: int }
type TaskStageLink.DeleteData { fromTaskStageID: int, taskTypeID: int, toTaskStageID: int }
type TaskStageLink.UpdateData { applyTaskStatusID?: int, branchID: int, description?: str, fromTaskStageID: int, isPositiveResult?: bool, name?: str, roles?: int[], sortOrder?: int, taskTypeID: int, timeoutSeconds?: int, timeoutToDeadlineSeconds?: int, toTaskStageID: int }
type TaskStageLinkOverride.AddData { description?: str, fromTaskStageID: int, isPositiveResult?: bool, name?: str, roles: int[], taskTypeID: int, toTaskStageID: int }
type TaskStageLinkOverride.DeleteData { fromTaskStageID: int, roles: int[], taskTypeID: int, toTaskStageID: int }
type TaskStageLinkOverride.UpdateData { description?: str, fromTaskStageID: int, isPositiveResult?: bool, name?: str, roles: int[], taskTypeID: int, toTaskStageID: int }
type TaskStageLinks.ListResult { branch?: IdNameResult<Byte>, description?: str /* Описание */, fromTaskStage?: IdNameResult<Int16>, isPositiveResult?: bool /* Результат перехода */, name?: str /* Название */, permissionUiID?: int /* Идентификатор связанного с переходом UI-полномочия */, roles?: IdNameDescriptionResult<Int16>[], sortOrder?: int /* Номер для сортировки */, taskStatus?: IdNameResult<Byte>, taskTypeID?: int /* Идентификатор типа заявки */, timeoutSeconds?: int /* Количество секунд до автоматического перехода */, timeoutToDeadlineSeconds?: int /* Количество секунд до делайна при автоматического переходе в зависимости от него */, toTaskStage?: IdNameResult<Int16> }
type TaskStageMessageTrigger.MergeData { messageTriggers?: int[] }
type TaskStageRequirement.MergeData { data: RequirementMergeData[], taskStageID: int }
type TaskStageRequirementResult { requirementID?: int /* Идентификатор требования */, requirementName?: str /* Имя требования */, taskStageID?: int /* Идентифкатор стадии заявки */ }
type TaskStages.GetResult { action?: IdNameResult<Byte>, assignToRole?: IdNameResult<Int32>, assignToUser?: IdNameResult<Int32>, assigneeSelectionRule?: IdNameResult<Byte>, color?: str /* Цвет стадии заявки */, deleted?: datetime /* Признак удаления элемента */, description?: str, id?: int, isShowTechnicianOnMap?: bool /* Признак видимости сотрудника на карте */, messageTriggerCount?: int /* Количество триггеров уведомлений, связанных со стадией */, messageTriggers?: IdNameResult<Int16>[] /* Триггеры сообщений */, name?: str, requirements?: IdNameResult<Int16>[] /* Требования */, taskViewTemplate?: IdNameResult<Byte> }
type TaskStages.ListResult { action?: IdNameResult<Byte>, assignToRole?: IdNameResult<Int32>, assignToUser?: IdNameResult<Int32>, assigneeSelectionRule?: IdNameResult<Byte>, color?: str /* Цвет стадии заявки */, deleted?: datetime /* Признак удаления элемента */, description?: str, id?: int, isShowTechnicianOnMap?: bool /* Признак видимости сотрудника на карте */, messageTriggerCount?: int /* Количество триггеров уведомлений, связанных со стадией */, name?: str, taskViewTemplate?: IdNameResult<Byte> }
type TemplateMergeData { taskStageID: int, taskTypeID: int, taskViewTemplateID: int }
type TriggerTaskStage.MergeData { data?: int[], triggerID: int }
```
