# AUTHZ — схемы

> **Что здесь:** определения типов read-ответов (GET/HEAD) сервиса AUTHZ. Ручки, ссылающиеся на них — `endpoints/AUTHZ.md`.
> **Линза read-only:** здесь только GET/HEAD. Write-ручки (POST/PUT/PATCH/DELETE) и их типы в API **существуют**, но в эту линзу не входят — не делай из их отсутствия здесь вывода, что их нет в API.

```
type JwtResultBase { access_token?: str /* JWT-токен для доступа к ресурсам */, expires_in?: int /* Количество секунд, через которой токен будет просрочен */, jwtValidTill?: datetime /* Метка времени в UTC, до которой действует JWT */, refresh_token?: str /* JWT-токен для обновления JWT-токена для доступа к ресурсам */ }
```
