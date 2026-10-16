# AUTH — справочник ручек

> **Что здесь:** все ручки сервиса AUTH (Authentication and authorization API for HubEx): сигнатуры, параметры, права. Типы — schemas/AUTH.md.
> **Когда сюда идти:** найти ручку и её вход/выход. Типы — `schemas/AUTH.md`; грабли — `notes/AUTH.md` (если есть).

Base: `{BASE_URL}/AUTH`
> Примеры ответов вынесены в [../examples/AUTH.md](../examples/AUTH.md).

**Оглавление**

- Accounts — строки 16–36
- Messages — строки 38–44
- Passwords — строки 46–48
- VerificationCodes — строки 50–53

## Accounts
- `GET /Accounts` — Возвращает данные учетной записи по учетным данным · коды: 200, 204 · примеры
  ← query: credential?:str → GetResult
- `HEAD /Accounts` — Проверяет присутствие учетной записи по указанным полномочиям · коды: 200, 404, 409 · примеры
  ← query: credential?:str
- `POST /Accounts/logout` — Выход из системы. Метод можно вызывать с просроченным токеном. · коды: 200, 409 · примеры
  ← body: BaseLogoutData
- `POST /Accounts/register` — Создаёт аккаунт с указанной электронной почтой (если ещё не создан),
блокирует его по причине непройденной верификации почты и отправляет
нотификацию для отправки письма или SMS со ссылкой для верификации. · коды: 200, 202, 409 · примеры
  ← body: CreateData → AccountAddResultEntity
- `GET /Accounts/this/applications` — Приложения учетной записи · paginated · коды: 200, 204, 206 · примеры
  → ApplicationListResult[]
  Поддерживает ограничение результата через query-параметры `offset` и `fetch`.
- `PUT /Accounts/this/applications` — Актуализация данных о приложениях текущей учетной записи · коды: 202 · примеры
  ← body: AUTHACAMergeData
- `DELETE /Accounts/this/applications` — Отвязка приложения и устройства от текущей учетной записи · коды: 202 · примеры
  ← body: AUTHACARemoveData
- `GET /Accounts/this/notifications` — Список уведомлений из лога · paginated · коды: 200, 204, 206 · примеры
  → ListResult[]
  Поддерживает ограничение результата через query-параметры `offset` и `fetch`.

## Messages
- `POST /Messages/requestPasswordChange` — Отправляет запрос на изменение пароля на указанный адрес эл. почты; для аутентифицированного пользователя — на адрес эл. почты уч.записи · коды: 202, 409 · примеры
  ← body: RequestPasswordChangeData → VerificationResult
- `POST /Messages/verifyEmail` — Отправляет письмо проверки почты на указанный адрес эл. почты (если не был указан, то на адрес уч.записи) · коды: 202, 204, 409 · примеры
  ← body: VerifyEmailData → VerificationResult
- `POST /Messages/verifyPhone` — Отправляет SMS проверки номера телефона на указанный телефон (если не был указан, то на телефон учетной записи) · коды: 202, 204, 409 · примеры
  ← body: VerifyPhoneData → VerificationResult

## Passwords
- `POST /Passwords/change` — Изменяет пароль учётной записи. · коды: 202, 409 · примеры
  ← body: PasswordSetData

## VerificationCodes
- `POST /VerificationCodes/check` — Проверяет верификационный код. · коды: 200, 409 · примеры
  ← body: CheckData → CheckResult
  Заголовок `Authorization` **не обязателен**. Для проверки по SMS достаточно тела запроса с `code` и `mobilePhone`.
