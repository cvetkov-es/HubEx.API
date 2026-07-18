# WSP — справочник ручек

> **Что здесь:** только read-ручки (GET/HEAD) сервиса WSP (API for work schedule managing for HubEx): сигнатуры, параметры, права. Типы — schemas/WSP.md. Сгенерировано из swagger.
> **Когда сюда идти:** найти ручку и её вход/выход. Типы — `schemas/WSP.md`; грабли — `notes/WSP.md` (если есть).
> **Источник:** swagger сервиса WSP · файл генерируется пайплайном — руками не править.
> **Линза read-only:** здесь только GET/HEAD. Write-ручки (POST/PUT/PATCH/DELETE) и их типы в API **существуют**, но в эту линзу не входят — не делай из их отсутствия здесь вывода, что их нет в API.

Base: `{BASE_URL}/WSP`

**Оглавление**

- ScheduleRules — строки 15–21
- WorkSchedules — строки 23–27

## ScheduleRules
- `GET /ScheduleRules` — Возвращает список доступных графиков рабочего времени · права: ScheduleRulesList · paginated · коды: 200, 206
  → map<ListResult>
- `GET /ScheduleRules/holiday` — Возвращает График праздничных дней · права: ScheduleRulesList · paginated · коды: 200, 206, 400
  ← query: year?:str → map<datetime[]>
- `GET /ScheduleRules/{id}` — Возвращает ГРВ · права: ScheduleRulesList · paginated · коды: 200, 206
  ← path: id:int → ScheduleRuleDto

## WorkSchedules
- `GET /WorkSchedules` — Возвращает график рабочего времени на заданный период · права: ScheduleRulesList · paginated · коды: 200, 206
  ← query: validTill?:any, validFrom?:any, scheduleRuleID?:any → map<WorkScheduleDailyItemResult>
- `GET /WorkSchedules/daily` — Возвращает график рабочего времени на заданный период по суткам · права: ScheduleRulesList · paginated · коды: 200, 206
  ← query: validTill?:any, validFrom?:any, scheduleRuleID?:any → map<WorkScheduleDailyItemResult[]>
