# entity-map.md — связка бизнес-сущностей с ручками API

> **Что здесь:** связка бизнес-сущностей с ручками API (таблицы БД — домен HubEx.DB, здесь их нет).
> **Когда сюда идти:** первым делом в любой задаче про данные — узнать, какой сервис и какая таблица отвечают за сущность.
> **Источник:** сущности продукта + справочники ручек (`endpoints/`) · **Обновлено:** 2026-07-02

Первые 15 сущностей — наиболее используемые (см. «Наиболее используемые API.txt»). Остальные 12 — ниже, под разделителем.

## Заявка (Ticket)
- **API:** [WORK](endpoints/WORK.md) — CRUD заявок, стадии, назначения. Ключевые ручки: `GET /Tasks`, `POST /Tasks`, `GET /Tasks/{taskID}`, `PATCH /Tasks/{taskID}`, `POST /TaskStagingHistory`
- ⚠ Тип заявки неизменяем после создания — смена только через копирование заявки с нужным типом и удаление старой.

## Тип заявки (TicketType)
- **API:** [WORK](endpoints/WORK.md) — справочник типов, маршруты стадий. Ключевые ручки: `GET /TaskTypes`, `POST /TaskTypes`, `PUT /TaskTypes`, `GET /TaskTypes/{taskTypeID}/route`
- ⚠ Номер заявки формируется по шаблону из Типа (номер меняем, тип — нет).

## Объект/Оборудование (Object)
- **API:** [ES](endpoints/ES.md) — CRUD активов, иерархия, атрибуты, публикация. Ключевые ручки: `GET /Assets`, `POST /Assets`, `GET /Assets/{assetID}`, `PUT /Assets/{assetID}`, `PUT /Assets/{assetID}/publish`
- ⚠ Родительский объект образует неограниченную иерархию; мобильное оборудование синхронизирует адрес с Заявкой.

## Компания (Company)
- **API:** [ES](endpoints/ES.md) — CRUD компаний, банк.реквизиты, контакты. Ключевые ручки: `GET /Companies`, `POST /Companies`, `GET /Companies/{id}`, `GET /Companies/{companyID}/bankAccounts`
- ⚠ ERP ID используется для интеграций с 1С/Битрикс.

## Сотрудник (Employee)
- **API:** [ADM](endpoints/ADM.md) — CRUD пользователей, роли, участки. Ключевые ручки: `GET /Users`, `POST /Users`, `GET /Users/{id}`, `PUT /Users/{id}`, `POST /UserRoles`
- ⚠ Soft delete асимметричен: заблокированного можно восстановить (`PUT /Users/{userID}/restore`), удалённого — нет.

## Выполненная работа (WorkCompletion)
- **API:** [WORK](endpoints/WORK.md) — добавление/обновление работ, материалы, техники. Ключевые ручки: `POST /CompletedWorks`, `PUT /CompletedWorks`, `POST /Tasks/completedWorks/materials`, `POST /Tasks/completedWorks/technicians`
- ⚠ Несколько Выполненных работ на одну Заявку; расчёт стоимости зависит от Вида работ и материалов.
- ⚠ Ставка исполнителя кратна 1 часу — округление вверх при расчёте стоимости (1ч35мин → 2ч × ставка).

## Вид работ (WorkType)
- **API:** [WORK](endpoints/WORK.md) — справочник видов работ, привязка к типам заявок и чек-листам. Ключевые ручки: `GET /WorkTypes`, `POST /WorkTypes`, `PUT /WorkTypes/{id}/publish`, `GET /WorkTypes/{workTypeID}/checkLists`
- ⚠ Список Видов работ в Заявке ограничен теми, что привязаны к выбранному Объекту (`GET /Assets/{assetID}/workTypes`).

## Стадия заявки (TicketStage)
- **API:** [TSTG](endpoints/TSTG.md) — стадии, переходы, требования. Ключевые ручки: `GET /TaskStages`, `POST /TaskStages`, `GET /TaskStages/{id}`, `GET /TaskStageLinks`
- ⚠ Требования стадии — «Назначен исполнитель» / «Обработаны чек-листы»; автопереход настраивается флагом + временем.

## Материал (Material)
- **API:** [WH](endpoints/WH.md) — CRUD материалов, штрихкоды, привязка к складу. Ключевые ручки: `GET /Materials`, `POST /Materials`, `GET /Materials/{id}`, `GET /Materials/{materialID}/barcodes`
- ⚠ Стоимость и Ед.измерения материала участвуют в расчёте Акта через `CompletedWorkMaterial`.

## Склад (Warehouse)
- **API:** [WH](endpoints/WH.md) — CRUD складов, привязка сотрудников. Ключевые ручки: `GET /Warehouses`, `POST /Warehouses`, `GET /Warehouses/{id}`, `POST /Warehouses/{id}/users`
- нет значимых граблей в entities.md.

## Критичность (Criticality)
- **API:** [SLA](endpoints/SLA.md) — справочник критичностей. Ключевые ручки: `GET /Criticalities`, `POST /Criticalities`, `PUT /Criticalities`, `GET /Criticalities/{id}`
- нет значимых граблей в entities.md.

## Чек-лист (Checklist)
- **API:** [WORK](endpoints/WORK.md) — CRUD чек-листов, пункты, привязка к объектам/видам работ. Ключевые ручки: `GET /CheckLists`, `POST /CheckLists`, `GET /CheckLists/{checkListID}/items`, `POST /CheckLists/{checkListID}/assign`
- ⚠ Привязка к Объекту и/или Виду работ — оба канала автоматически добавляют чек-лист в Заявку.

## Роль (Role)
- **API:** [ADM](endpoints/ADM.md) — CRUD ролей, права. Ключевые ручки: `GET /Roles`, `POST /Roles`, `GET /Roles/{roleID}/permissionsUi`, `POST /RolePermissionsUi`
- ⚠ Доступ к полям заявки настраивается по матрице Роль × Стадия (R/RW/скрыто) через `RoleTaskPropertiesAccess`.

## Договор (Contract)
- **API:** [SC](endpoints/SC.md) — CRUD договоров, привязка объектов. Ключевые ручки: `GET /ServiceContract`, `POST /ServiceContract`, `GET /ServiceContract/{contractID}`, `POST /ServiceContract/{contractID}/assets`
- ⚠ В Заявке Договор доступен только после выбора Объекта; при просрочке — предупреждение.

## Акт выполненных работ (CompletionAct)
- **API:** [WORK](endpoints/WORK.md) — печатная форма акта, подпись, вложение. Ключевые ручки: `PUT /Tasks/{taskID}/complete`, `GET /Tasks/{taskID}/completedWorks/report/attachment`, `POST /Tasks/completedWorks/report/attachment/upload/fromForm`
- ⚠ Сумма Акта = стоимость видов работ + ставка×часы + материалы; печать содержит банк.реквизиты исполнителя и QR-код оплаты.
- ⚠ Ставка исполнителя кратна 1 часу — округление вверх при расчёте стоимости (1ч35мин → 2ч × ставка).

---

## Тип оборудования (ObjectType)
- **API:** [ES](endpoints/ES.md) — справочник типов активов. Ключевые ручки: `GET /AssetTypes`, `POST /AssetTypes`, `PUT /AssetTypes`, `GET /AssetTypes/{id}/workTypes`
- нет значимых граблей в entities.md.

## Заказчик (Customer)
- **API:** [ADM](endpoints/ADM.md) — использует общий CRUD пользователей + смена роли. Ключевые ручки: `GET /Users ?isCustomer:bool`, `POST /Users/changeToCustomer`, `POST /Users/changeToStaff`
- ⚠ Заказчик не может менять стадии сам — ходит по ветке ЖЦ «Для заказчика».

## Статус заявки (TicketStatus)
- **API:** [WORK](endpoints/WORK.md) — справочник статусов (отображение стадии для заказчика). Ключевые ручки: `GET /TaskStatuses`, `POST /TaskStatuses`, `PUT /TaskStatuses`
- нет значимых граблей в entities.md.

## Жизненный цикл (Lifecycle)
- **API:** [TSTG](endpoints/TSTG.md) — ветки и маршруты переходов между стадиями. Ключевые ручки: `GET /Branches`, `GET /TaskStageLinks`, `POST /TaskStageLinks`, `POST /TaskStageLinks/copy`
- ⚠ Две ветки ЖЦ: для сотрудников и для заказчика — обычно с разным набором стадий.

## Участок (Place)
- **API:** [ES](endpoints/ES.md) — районы/участки, привязка объектов. Ключевые ручки: `GET /Districts`, `POST /Districts`, `PUT /Districts`, `POST /AssetDistricts`
- ⚠ Разграничивает доступ через Роли — участок сотрудника/заказчика фильтрует видимые заявки и объекты.

## Навык (Skill)
- **API:** [PA](endpoints/PA.md) — справочник навыков, привязка к сотрудникам. Ключевые ручки: `GET /Skills`, `POST /Skills`, `POST /UserSkills`, `DELETE /UserSkills`
- ⚠ Навык используется для автоназначения исполнителя (связка Объект ↔ Сотрудник).

## Контактное лицо (Contact)
- **API:** [COMMON](endpoints/COMMON.md) — CRUD контактов, привязка к компании/объекту через ES/SC. Ключевые ручки: `GET /Contacts`, `POST /Contacts`, `PUT /Contacts`, `GET /Contacts/{contactID}`
- нет значимых граблей в entities.md.

## Инициатор заявки (Requester)
- **API:** [WORK](endpoints/WORK.md) — заявка хранит инициатора как пользователя (см. `requestedByUserID` в `TaskAddData`). Ключевые ручки: `GET /Tasks ?requestedBy:any`, `GET /Users/{id}` ([ADM](endpoints/ADM.md))
- ⚠ Инициатор проставляется автоматически для зарегистрированных пользователей.

## Дополнительное поле (CustomField)
- **API:** [COMMON](endpoints/COMMON.md) — справочник атрибутов и их значений. Ключевые ручки: `GET /Attributes`, `POST /Attributes`, `PUT /Attributes`, `GET /Attributes/{attributeID}/listOfValues`
- ⚠ Тип Дополнительного поля нельзя изменить после создания.

## Шаблон заявки (TicketTemplate)
- **API:** [WORK](endpoints/WORK.md) — CRUD шаблонов, публикация, QR. Ключевые ручки: `GET /TaskTemplates`, `POST /TaskTemplates`, `PUT /TaskTemplates/{id}/publish`, `GET /TaskTemplates/{id}/public`
- нет значимых граблей в entities.md.

## Плановая заявка (PlannedTicket)
- **API:** [PMP](endpoints/PMP.md) — расписания и автосоздание заявок. Ключевые ручки: `GET /ScheduledTasks`, `GET /Schedules`, `POST /Schedules`, `GET /Schedules/{scheduleID}/appointments`
- ⚠ Плановая заявка = Шаблон + период повторения + Объект; создаётся автоматически по расписанию.

## График работы (Schedule)
- **API:** [WSP](endpoints/WSP.md) — правила смен, рабочие расписания. Ключевые ручки: `GET /ScheduleRules`, `POST /ScheduleRules`, `GET /WorkSchedules`, `PUT /ScheduleRules/extend/{id}`
- ⚠ Учитывается при автоназначении исполнителя («на смене» — посменный режим).

Все 27 сущностей из `product/entities.md` покрыты выше: 15 самых частых (по «Наиболее используемые API.txt») — в первом блоке, остальные 12 — во втором, под разделителем.
