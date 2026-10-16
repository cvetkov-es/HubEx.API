# AUTHN — справочник ручек

> **Что здесь:** все ручки сервиса AUTHN (Authentication and authorization API for HubEx): сигнатуры, параметры, права. Типы — schemas/AUTHN.md.
> **Когда сюда идти:** найти ручку и её вход/выход. Типы — `schemas/AUTHN.md`; грабли — `notes/AUTHN.md` (если есть).

Base: `{BASE_URL}/AUTHN`
> Примеры ответов вынесены в [../examples/AUTHN.md](../examples/AUTHN.md).

**Оглавление**

- Accounts — строки 14–25
- Passwords — строки 27–29

## Accounts
- `POST /Accounts/login` — Аутентифицирует учётную запись по логину, e-mail или телефону и паролю. · коды: 200, 409 · примеры
  → AuthenticationResult
- `POST /Accounts/login/sso` — Аутентифицирует учётную запись через SSO (Keycloak). · коды: 200, 409 · примеры
  ← header: X-Realm-ID:str → AuthenticationResult
- `POST /Accounts/realm` — Возвращает реалмы SSO для аккаунта по e-mail или домену. · paginated · коды: 200, 204, 206, 400 · примеры
  ← body: CredentialData → AccountRealmResult[]
  Поддерживает ограничение результата через заголовок `Range` (например, `Range: items=1-50`).
- `POST /Accounts/smsLogin` — Проверяет SMS-код и выполняет вход. · коды: 200, 400, 404 · примеры
  ← body: AuthSmsDto → AuthenticationResult
- `POST /Accounts/smsSend` — Отправляет SMS с кодом для входа. · коды: 200, 400, 404, 429 · примеры
  ← body: PhoneDto

## Passwords
- `POST /Passwords/set` — Устанавливает пароль для учётной записи. · коды: 202, 400 · примеры
  ← body: SetData → JwtResultBase
