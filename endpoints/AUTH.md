# AUTH — справочник ручек

> **Что здесь:** только read-ручки (GET/HEAD) сервиса AUTH (Authenticatin and authorization API for HubEx): сигнатуры, параметры, права. Типы — schemas/AUTH.md. Сгенерировано из swagger.
> **Когда сюда идти:** найти ручку и её вход/выход. Типы — `schemas/AUTH.md`; грабли — `notes/AUTH.md` (если есть).
> **Источник:** swagger сервиса AUTH · файл генерируется пайплайном — руками не править.
> **Линза read-only:** здесь только GET/HEAD. Write-ручки (POST/PUT/PATCH/DELETE) и их типы в API **существуют**, но в эту линзу не входят — не делай из их отсутствия здесь вывода, что их нет в API.

Base: `{BASE_URL}/AUTH`

**Оглавление**

- Accounts — строки 14–23

## Accounts
- `GET /Accounts` — Возвращает данные учетной записи по учетным данным · права: AccountGet · коды: 200, 500
  ← query: credential?:str → GetResult
- `HEAD /Accounts` — Проверяет присутствие учетной записи по указанным полномочийм · коды: 200, 404
  ← query: credential?:str
  Выполнение данного метода резрешино от **анонимного пользователя**.
- `GET /Accounts/this/applications` — Приложения учетной записи · права: AccountClientApplicationList · paginated · коды: 200, 206
  → ApplicationListResult[]
- `GET /Accounts/this/notifications` — Список уведомлений из лога · права: NotificationLogList · paginated · коды: 200, 206
  → ListResult[]
