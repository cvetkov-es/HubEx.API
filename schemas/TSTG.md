# TSTG — схемы

> **Что здесь:** определения типов read-ответов (GET/HEAD) сервиса TSTG. Ручки, ссылающиеся на них — `endpoints/TSTG.md`.
> **Линза read-only:** здесь только GET/HEAD. Write-ручки (POST/PUT/PATCH/DELETE) и их типы в API **существуют**, но в эту линзу не входят — не делай из их отсутствия здесь вывода, что их нет в API.

```
type ActionResult map
type AssigneeSelectionRule.GetResult { assetResponsibilityRatio?: float /* Коэффициент учета отв. по объекту */, customerRatio?: float /* Коэффициент учета заказчика */, deleted?: datetime /* TenantMemberID, который проставил флаг "удалено" */, districtRatio?: float /* Коэффициент учета заказчика */, id?: int /* Идентификатор правила */, managerRatio?: float /* Коэффициент  учета руководителя */, name?: str /* Название правила */, oftenAssignedRatio?: float /* Коэффициент учета того, как часто назначается на объект */, optionalSkillRatio?: float /* Коэффициент опциональных навыков */, preffereableRatio?: float /* Коэффициент учета предпочтительного инженера */, requiredSkillRatio?: float /* Коэффициент обязательных навыков */, workScheduleRatio?: float /* Коэффициент учета расписания */, workTypeRatio?: float /* Коэффициент учета видов работ */ }
type AssigneeSelectionRule.ListResult { assetResponsibilityRatio?: float /* Коэффициент учета отв. по объекту */, customerRatio?: float /* Коэффициент учета заказчика */, districtRatio?: float /* Коэффициент учета заказчика */, managerRatio?: float /* Коэффициент  учета руководителя */, name?: str /* Название правила */, oftenAssignedRatio?: float /* Коэффициент учета того, как часто назначается на объект */, optionalSkillRatio?: float /* Коэффициент опциональных навыков */, preffereableRatio?: float /* Коэффициент учета предпочтительного инженера */, requiredSkillRatio?: float /* Коэффициент обязательных навыков */, workScheduleRatio?: float /* Коэффициент учета расписания */, workTypeRatio?: float /* Коэффициент учета видов работ */ }
type AttributeResult { id?: int /* Идентификатор атрибута */, name?: str /* Наименование атрибута */, type?: AttributeTypeResult }
type AttributeTypeResult { code?: str /* Код типа атрибута */, name?: str /* Наименование типа атрибута */ }
type AvailabilityAttributeResult { attribute?: AttributeResult, availability?: AvailabilityResult }
type AvailabilityComponentResult { availability?: AvailabilityResult, component?: ComponentResult }
type AvailabilityListResult { attributes?: AvailabilityAttributeResult[] /* Информация о атрибутах */, components?: AvailabilityComponentResult[] /* Информация о компонентах */ }
type AvailabilityResult { capabilityID?: int /* Идентификатор возможности */, roleID?: int /* Идентификатор роли */, taskStageID?: int /* Идентификатор стадии */, taskTypes?: int[] /* Идентификатор типа заявки */ }
type BranchResult { color?: str /* Цвет ветки жизненного цикла */, isExclusiveMode?: bool /* Флаг эксклюзивности */, nameRu?: str /* ;
            Название */ }
type ComponentResult { code?: str /* Код компонента */, description?: str /* Описание компонента */, id?: int /* Идентификатор компонента */ }
type IdNameDescriptionResult<Int16> { description?: str, id?: int, name?: str }
type IdNameResult<Byte> { id?: int, name?: str }
type IdNameResult<Int16> { id?: int, name?: str }
type IdNameResult<Int32> { id?: int, name?: str }
type OverrideListResult { description?: str /* Описание */, fromTaskStage?: IdNameResult<Int16>, isPositiveResult?: bool /* Результат перехода */, name?: str /* Название */, role?: IdNameResult<Int16>, taskTypeID?: int /* Идентификатор типа заявки */, toTaskStage?: IdNameResult<Int16> }
type Requirements.ListResult { code?: str /* Код требования */, description?: str /* Описание требования */, name?: str /* Название тербования */ }
type TaskStageLinks.ListResult { branch?: IdNameResult<Byte>, description?: str /* Описание */, fromTaskStage?: IdNameResult<Int16>, isPositiveResult?: bool /* Результат перехода */, name?: str /* Название */, permissionUiID?: int /* Идентификатор связанного с переходом UI-полномочия */, roles?: IdNameDescriptionResult<Int16>[], sortOrder?: int /* Номер для сортировки */, taskStatus?: IdNameResult<Byte>, taskTypeID?: int /* Идентификатор типа заявки */, timeoutSeconds?: int /* Количество секунд до автоматического перехода */, timeoutToDeadlineSeconds?: int /* Количество секунд до делайна при автоматического переходе в зависимости от него */, toTaskStage?: IdNameResult<Int16> }
type TaskStageRequirementResult { requirementID?: int /* Идентификатор требования */, requirementName?: str /* Имя требования */, taskStageID?: int /* Идентифкатор стадии заявки */ }
type TaskStages.GetResult { action?: IdNameResult<Byte>, assignToRole?: IdNameResult<Int32>, assignToUser?: IdNameResult<Int32>, assigneeSelectionRule?: IdNameResult<Byte>, color?: str /* Цвет стадии заявки */, deleted?: datetime /* Признак удаления элемента */, description?: str, id?: int, isShowTechnicianOnMap?: bool /* Признак видимости сотрудника на карте */, messageTriggerCount?: int /* Количество триггеров уведомлений, связанных со стадией */, messageTriggers?: IdNameResult<Int16>[] /* Триггеры сообщений */, name?: str, requirements?: IdNameResult<Int16>[] /* Требования */, taskViewTemplate?: IdNameResult<Byte> }
type TaskStages.ListResult { action?: IdNameResult<Byte>, assignToRole?: IdNameResult<Int32>, assignToUser?: IdNameResult<Int32>, assigneeSelectionRule?: IdNameResult<Byte>, color?: str /* Цвет стадии заявки */, deleted?: datetime /* Признак удаления элемента */, description?: str, id?: int, isShowTechnicianOnMap?: bool /* Признак видимости сотрудника на карте */, messageTriggerCount?: int /* Количество триггеров уведомлений, связанных со стадией */, name?: str, taskViewTemplate?: IdNameResult<Byte> }
```
