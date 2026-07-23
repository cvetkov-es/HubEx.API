# WSP — схемы

> **Что здесь:** определения типов запросов/ответов сервиса WSP. Ручки, ссылающиеся на них — `endpoints/WSP.md`.

```
type ErrorModel { arguments?: map<str>, code?: str, message?: str, traceIdentifier?: str }
type ListResult { dataFrom?: datetime /* Дата старта графика */, description?: str /* Описание правила */, name?: str /* Название правила */, scheduleTypeID?: int /* Тип графика */ }
type ScheduleCreateDto { considerPublicHolidays?: bool, description?: str, from?: datetime, isDefault?: bool, name?: str, overridings?: ScheduleDto[], rules?: ScheduleDto+Rule[], scheduleTypeID?: int, shortageHoursBeforeHoliday?: int, till?: datetime }
type ScheduleDto { isPublicHoliday?: bool, isWorking?: bool, rules?: ScheduleDto+Rule[] }
type ScheduleDto+Rule { cron?: str, occurrenceDuration?: str, periodicity?: ScheduleDto+Rule+PeriodicityData }
type ScheduleDto+Rule+PeriodicityData { repeatCnt?: int, skip?: str }
type ScheduleExtendDto { considerPublicHolidays?: bool, from?: datetime, overridings?: ScheduleDto[], rules?: ScheduleDto+Rule[], shortageHoursBeforeHoliday?: int, till?: datetime }
type ScheduleOccurrenceDto { duration?: str, isNightShift?: bool, isPublicHoliday?: bool, isWorking?: bool, start?: datetime }
type SchedulePersistDto { overridings?: ScheduleDto[], rules?: ScheduleDto+Rule[] }
type ScheduleRuleDto { description?: str, name?: str, periods?: ScheduleRuleDto+Period[], scheduleTypeID?: int }
type ScheduleRuleDto+Period { from?: datetime, holidayCalendarID?: int, model?: SchedulePersistDto, shortageHoursBeforeHoliday?: int, till?: datetime }
type ScheduleUpdateDto { considerPublicHolidays?: bool, description?: str, from?: datetime, name?: str, overridings?: ScheduleDto[], rules?: ScheduleDto+Rule[], scheduleTypeID?: int, shortageHoursBeforeHoliday?: int, till?: datetime }
type WorkScheduleDailyItemResult { dateWork?: datetime /* Дата работы */, isNightShift?: bool /* Признак ночной смены */, isPublicHoliday?: bool /* Признак праздничного дня */, scheduleRuleID?: int /* Идентификатор правила графика рабочего времени */, timeFrom?: datetime /* Начало работы */, timeTill?: datetime /* Окончание работы */ }
```
