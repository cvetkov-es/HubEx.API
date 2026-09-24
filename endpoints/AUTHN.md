# AUTHN — справочник ручек

> **Что здесь:** все ручки сервиса AUTHN (Authentication and authorization API for HubEx): сигнатуры, параметры, права. Типы — schemas/AUTHN.md.
> **Когда сюда идти:** найти ручку и её вход/выход. Типы — `schemas/AUTHN.md`; грабли — `notes/AUTHN.md` (если есть).

Base: `{BASE_URL}/AUTHN`
> Примеры ответов вынесены в [../examples/AUTHN.md](../examples/AUTHN.md).

**Оглавление**

- Accounts — строки 18–25
- Пример запроса: — строки 27–32
- Пример успешного ответа (200): — строки 34–43
- Пример успешного ответа (206): — строки 45–46
- Негативные сценарии: — строки 48–54
- Passwords — строки 56–58

## Accounts
- `POST /Accounts/login` — Аутентифицирует учётную запись по логину, e-mail или телефону и паролю. · коды: 200, 409 · примеры
  → AuthenticationResult
- `POST /Accounts/login/sso` — Аутентифицирует учётную запись через SSO (Keycloak). · коды: 200, 409 · примеры
  ← header: X-Realm-ID:str → AuthenticationResult
- `POST /Accounts/realm` — Возвращает реалмы SSO для аккаунта по e-mail или домену. · коды: 200, 204, 206, 400
  ← body: CredentialData → AccountRealmResult[]
  Поддерживает ограничение результата через заголовок `Range` (например, `Range: items=1-50`).
            
## Пример запроса:
```json
{
  "credential": "user@company.com"
}
```
            
## Пример успешного ответа (200):
```json
[
  {
    "tenantID": 10,
    "tenantName": "Demo Tenant",
    "realm": "demo"
  }
]
```
            
## Пример успешного ответа (206):
Тело ответа имеет тот же формат, что и для `200`, но содержит только часть диапазона. Заголовок `Content-Range` указывает общее количество.
            
## Негативные сценарии:
- 400 Bad Request — не указан credential.
- 204 No Content — реалмы для указанного credential не найдены.
- `POST /Accounts/smsLogin` — Проверяет SMS-код и выполняет вход. · коды: 200, 400, 404 · примеры
  ← body: AuthSmsDto → AuthenticationResult
- `POST /Accounts/smsSend` — Отправляет SMS с кодом для входа. · коды: 200, 400, 404, 429 · примеры
  ← body: PhoneDto

## Passwords
- `POST /Passwords/set` — Устанавливает пароль для учётной записи. · коды: 202, 400 · примеры
  ← body: SetData → JwtResultBase
