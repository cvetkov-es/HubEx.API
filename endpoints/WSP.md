# WSP — справочник ручек

> **Что здесь:** все ручки сервиса WSP (API for work schedule managing for HubEx): сигнатуры, параметры, права. Типы — schemas/WSP.md.
> **Когда сюда идти:** найти ручку и её вход/выход. Типы — `schemas/WSP.md`; грабли — `notes/WSP.md` (если есть).

Base: `{BASE_URL}/WSP`

**Оглавление**

- ScheduleRules — строки 13–29
- WorkSchedules — строки 31–35

## ScheduleRules
- `GET /ScheduleRules` — Возвращает список доступных графиков рабочего времени · права: ScheduleRulesList · paginated · коды: 200, 206
  → map<ListResult>
- `POST /ScheduleRules` — Создаёт ГРВ · права: ScheduleRulesList · paginated · коды: 201, 206
  ← body: ScheduleCreateDto → int
- `PUT /ScheduleRules/extend/{id}` — Расширяет ГРВ · права: ScheduleRulesList · paginated · коды: 202, 206
  ← path: id:int; body: ScheduleExtendDto
- `GET /ScheduleRules/holiday` — Возвращает График праздничных дней · права: ScheduleRulesList · paginated · коды: 200, 206, 400
  ← query: year?:str → map<datetime[]>
- `POST /ScheduleRules/preview` — Возвращает ГРВ для предпросмотра · права: ScheduleRulesList · paginated · коды: 201, 206
  ← body: ScheduleExtendDto → ScheduleOccurrenceDto[]
- `GET /ScheduleRules/{id}` — Возвращает ГРВ · права: ScheduleRulesList · paginated · коды: 200, 206
  ← path: id:int → ScheduleRuleDto
- `PUT /ScheduleRules/{id}` — Меняет ГРВ · права: ScheduleRulesList · paginated · коды: 202, 206
  ← path: id:int; body: ScheduleUpdateDto
- `DELETE /ScheduleRules/{id}` — Удаляет ГРВ · права: ScheduleRulesList · paginated · коды: 202, 206
  ← path: id:int

## WorkSchedules
- `GET /WorkSchedules` — Возвращает график рабочего времени на заданный период · права: ScheduleRulesList · paginated · коды: 200, 206
  ← query: validTill?:any, validFrom?:any, scheduleRuleID?:any → map<WorkScheduleDailyItemResult>
- `GET /WorkSchedules/daily` — Возвращает график рабочего времени на заданный период по суткам · права: ScheduleRulesList · paginated · коды: 200, 206
  ← query: validTill?:any, validFrom?:any, scheduleRuleID?:any → map<WorkScheduleDailyItemResult[]>
