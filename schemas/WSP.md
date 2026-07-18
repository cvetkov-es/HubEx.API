# WSP — схемы

> **Что здесь:** определения типов read-ответов (GET/HEAD) сервиса WSP. Ручки, ссылающиеся на них — `endpoints/WSP.md`.
> **Источник:** swagger сервиса WSP · файл генерируется пайплайном — руками не править.
> **Линза read-only:** здесь только GET/HEAD. Write-ручки (POST/PUT/PATCH/DELETE) и их типы в API **существуют**, но в эту линзу не входят — не делай из их отсутствия здесь вывода, что их нет в API.

```
type ErrorModel { arguments?: map<str>, code?: str, message?: str, traceIdentifier?: str }
type ListResult { dataFrom?: datetime /* Дата старта графика */, description?: str /* Описание правила */, name?: str /* Название правила */, scheduleTypeID?: int /* Тип графика */ }
type ScheduleDto { isPublicHoliday?: bool, isWorking?: bool, rules?: ScheduleDto+Rule[] }
type ScheduleDto+Rule { cron?: str, occurrenceDuration?: str, periodicity?: ScheduleDto+Rule+PeriodicityData }
type ScheduleDto+Rule+PeriodicityData { repeatCnt?: int, skip?: str }
type SchedulePersistDto { overridings?: ScheduleDto[], rules?: ScheduleDto+Rule[] }
type ScheduleRuleDto { description?: str, name?: str, periods?: ScheduleRuleDto+Period[], scheduleTypeID?: int }
type ScheduleRuleDto+Period { from?: datetime, holidayCalendarID?: int, model?: SchedulePersistDto, shortageHoursBeforeHoliday?: int, till?: datetime }
type WorkScheduleDailyItemResult { dateWork?: datetime /* Дата работы */, isNightShift?: bool /* Признак ночной смены */, isPublicHoliday?: bool /* Признак праздничного дня */, scheduleRuleID?: int /* Идентификатор правила графика рабочего времени */, timeFrom?: datetime /* Начало работы */, timeTill?: datetime /* Окончание работы */ }
```
