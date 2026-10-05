# WSP — справочник ручек

> **Что здесь:** все ручки сервиса WSP (API for work schedule managing for HubEx): сигнатуры, параметры, права. Типы — schemas/WSP.md.
> **Когда сюда идти:** найти ручку и её вход/выход. Типы — `schemas/WSP.md`; грабли — `notes/WSP.md` (если есть).

Base: `{BASE_URL}/WSP`

**Оглавление**

- ScheduleRules — строки 13–29
- WorkSchedules — строки 31–35

## ScheduleRules
- `GET /ScheduleRules` — Возвращает список доступных графиков рабочего времени · коды: 200
  → map<ListResult>
- `POST /ScheduleRules` — Создаёт ГРВ · коды: 201
  ← body: ScheduleCreateDto → int
- `PUT /ScheduleRules/extend/{id}` — Расширяет ГРВ · коды: 202
  ← path: id:int; body: ScheduleExtendDto
- `GET /ScheduleRules/holiday` — Возвращает График праздничных дней · коды: 200, 400
  ← query: year?:str → map<datetime[]>
- `POST /ScheduleRules/preview` — Возвращает ГРВ для предпросмотра · коды: 201
  ← body: ScheduleExtendDto → ScheduleOccurrenceDto[]
- `GET /ScheduleRules/{id}` — Возвращает ГРВ · коды: 200
  ← path: id:int → ScheduleRuleDto
- `PUT /ScheduleRules/{id}` — Меняет ГРВ · коды: 202
  ← path: id:int; body: ScheduleUpdateDto
- `DELETE /ScheduleRules/{id}` — Удаляет ГРВ · коды: 202
  ← path: id:int

## WorkSchedules
- `GET /WorkSchedules` — Возвращает график рабочего времени на заданный период · коды: 200
  → map<WorkScheduleDailyItemResult>
- `GET /WorkSchedules/daily` — Возвращает график рабочего времени на заданный период по суткам · коды: 200
  → map<WorkScheduleDailyItemResult[]>
