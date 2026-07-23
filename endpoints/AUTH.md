# AUTH — справочник ручек

> **Что здесь:** все ручки сервиса AUTH (Authenticatin and authorization API for HubEx): сигнатуры, параметры, права. Типы — schemas/AUTH.md.
> **Когда сюда идти:** найти ручку и её вход/выход. Типы — `schemas/AUTH.md`; грабли — `notes/AUTH.md` (если есть).

Base: `{BASE_URL}/AUTH`

**Оглавление**

- Accounts — строки 15–39
- Messages — строки 41–50
- Passwords — строки 52–55
- VerificationCodes — строки 57–60

## Accounts
- `GET /Accounts` — Возвращает данные учетной записи по учетным данным · права: AccountGet · коды: 200, 500
  ← query: credential?:str → GetResult
- `HEAD /Accounts` — Проверяет присутствие учетной записи по указанным полномочийм · коды: 200, 404
  ← query: credential?:str
  Выполнение данного метода резрешино от **анонимного пользователя**.
- `POST /Accounts/logout` — Выход из системы. Сетод можно вызывать с просроченным токеном. · коды: 200, 500
  ← body: BaseLogoutData
  Выполнение данного метода резрешино от **анонимного пользователя**.
- `POST /Accounts/register` — Создаёт аккаунт с указанной электронной почтой (если ещё не создан),
блокирует его по причине непройденноё верификации почты и отправляет в Кролика
нотификацию для отправки письма на указанный адрес эл. почты со ссылкой
для верификации. · коды: 200
  ← body: CreateData → AccountAddResultEntity
  Выполнение данного метода резрешино от **анонимного пользователя**.
- `GET /Accounts/this/applications` — Приложения учетной записи · права: AccountClientApplicationList · paginated · коды: 200, 206
  → ApplicationListResult[]
- `PUT /Accounts/this/applications` — Актуализация данных о приложениях текущей учетной записи · коды: 202
  ← body: MergeData
  Для выполнения данного метода пользователь должен быть **Authenticated**.
- `DELETE /Accounts/this/applications` — Отвязка приложения и устройства от текущей учетной записи · коды: 202
  ← body: RemoveData
  Для выполнения данного метода пользователь должен быть **Authenticated**.
- `GET /Accounts/this/notifications` — Список уведомлений из лога · права: NotificationLogList · paginated · коды: 200, 206
  → ListResult[]

## Messages
- `POST /Messages/requestPasswordChange` — Отправляет запрос на изменение пароля на указанный адрес эл почты, для аутентифицированного пользователя - на адрес. эл. почты уч.записи · коды: 200
  ← body: RequestPasswordChangeData → VerificationResult
  Выполнение данного метода резрешино от **анонимного пользователя**.
- `POST /Messages/verifyEmail` — Отправляет письмо проверки почты на указаннаый адрес эл почты (если не был указан, то на адрес уч.записи) · коды: 200
  ← body: VerifyEmailData → VerificationResult
  Выполнение данного метода резрешино от **анонимного пользователя**.
- `POST /Messages/verifyPhone` — Отправляет SMS проверки номера телефона почты на указаннаый телефон, (если не был указан, то на телефон учетной записи) · коды: 200
  ← body: VerifyPhoneData → VerificationResult
  Выполнение данного метода резрешино от **анонимного пользователя**.

## Passwords
- `POST /Passwords/change` — Изменяет пароль учётной записи. · коды: 200
  ← body: PasswordSetData
  Выполнение данного метода резрешино от **анонимного пользователя**.

## VerificationCodes
- `POST /VerificationCodes/check` — Проверяет верификационый код. · коды: 200
  ← body: CheckData → int
  Выполнение данного метода резрешино от **анонимного пользователя**.
