# WSP — схемы

> **Что здесь:** определения типов запросов/ответов сервиса WSP. Ручки, ссылающиеся на них — `endpoints/WSP.md`.
> **Источник:** `snapshots/WSP.json` · файл генерируется пайплайном — руками не править.

```
type ErrorModel { traceIdentifier?: str, code?: str, message?: str, arguments?: map<str> }
type ListResult { name?: str /* Название правила */, description?: str /* Описание правила */, scheduleTypeID?: int /* Тип графика */, dataFrom?: datetime /* Дата старта графика */ }
type ScheduleCreateDto { from?: datetime, till?: datetime, considerPublicHolidays?: bool, shortageHoursBeforeHoliday?: int, rules?: ScheduleDto+Rule[], overridings?: ScheduleDto[], name?: str, description?: str, isDefault?: bool, scheduleTypeID?: int }
type ScheduleDto { rules?: ScheduleDto+Rule[], isWorking?: bool, isPublicHoliday?: bool }
type ScheduleDto+Rule { cron?: str, occurrenceDuration?: str, periodicity?: ScheduleDto+Rule+PeriodicityData }
type ScheduleDto+Rule+PeriodicityData { repeatCnt?: int, skip?: str }
type ScheduleExtendDto { from?: datetime, till?: datetime, considerPublicHolidays?: bool, shortageHoursBeforeHoliday?: int, rules?: ScheduleDto+Rule[], overridings?: ScheduleDto[] }
type ScheduleOccurrenceDto { start?: datetime, duration?: str, isWorking?: bool, isNightShift?: bool, isPublicHoliday?: bool }
type SchedulePersistDto { rules?: ScheduleDto+Rule[], overridings?: ScheduleDto[] }
type ScheduleRuleDto { name?: str, description?: str, scheduleTypeID?: int, periods?: ScheduleRuleDto+Period[] }
type ScheduleRuleDto+Period { from?: datetime, till?: datetime, holidayCalendarID?: int, shortageHoursBeforeHoliday?: int, model?: SchedulePersistDto }
type ScheduleUpdateDto { from?: datetime, till?: datetime, considerPublicHolidays?: bool, shortageHoursBeforeHoliday?: int, rules?: ScheduleDto+Rule[], overridings?: ScheduleDto[], name?: str, description?: str, scheduleTypeID?: int }
type WorkScheduleDailyItemResult { scheduleRuleID?: int /* Идентификатор правила графика рабочего времени */, timeFrom?: datetime /* Начало работы */, timeTill?: datetime /* Окончание работы */, isPublicHoliday?: bool /* Признак праздничного дня */, isNightShift?: bool /* Признак ночной смены */, dateWork?: datetime /* Дата работы */ }
```
