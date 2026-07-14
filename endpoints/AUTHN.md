# AUTHN — справочник ручек

> **Что здесь:** все ручки сервиса AUTHN (Authenticatin and authorization API for HubEx): сигнатуры, параметры, права. Типы — schemas/AUTHN.md. Сгенерировано из swagger.
> **Когда сюда идти:** найти ручку и её вход/выход. Типы — `schemas/AUTHN.md`; грабли — `notes/AUTHN.md` (если есть).
> **Источник:** `snapshots/AUTHN.json` · файл генерируется пайплайном — руками не править.

Base: `{BASE_URL}/AUTHN`

## Accounts
- `POST /Accounts/login` — Аутентификация учетной записи по мобильному телефону, адресу электронной почты или логину и паролю через Basic-авторизацию
  → AuthenticationResult
  Выполнение данного метода резрешино от **анонимного пользователя**.
- `POST /Accounts/login/sso` — Аутентификация учетной записи по sso
  → AuthenticationResult
  Выполнение данного метода резрешино от **анонимного пользователя**.
- `POST /Accounts/realm` — Возвращает данные о реалмах аккаунта по адресу электронной почты или домену
  ← body: CredentialData → AccountRealmResult[]
  Выполнение данного метода резрешино от **анонимного пользователя**.
- `POST /Accounts/smsLogin` — Проверка СМС кода
  ← body: AuthSmsDto → AuthenticationResult
  Выполнение данного метода резрешино от **анонимного пользователя**.
- `POST /Accounts/smsSend` — Генерация кода для авторизации через СМС
  ← body: PhoneDto → OtpGenerateResult
  Выполнение данного метода резрешино от **анонимного пользователя**.

## Passwords
- `POST /Passwords/set` — Устанавливает пароль для вновь созданной учётной записи.
  ← body: SetData
  Выполнение данного метода резрешино от **анонимного пользователя**.
