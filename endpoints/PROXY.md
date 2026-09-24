# PROXY — справочник ручек

> **Что здесь:** только read-ручки (GET/HEAD) сервиса PROXY (API for remote calling 3rd party services.): сигнатуры, параметры, права. Типы — schemas/PROXY.md.
> **Когда сюда идти:** найти ручку и её вход/выход. Типы — `schemas/PROXY.md`; грабли — `notes/PROXY.md` (если есть).
> **Линза read-only:** здесь только GET/HEAD. Write-ручки (POST/PUT/PATCH/DELETE) и их типы в API **существуют**, но в эту линзу не входят — не делай из их отсутствия здесь вывода, что их нет в API.

Base: `{BASE_URL}/PROXY`
> Примеры ответов вынесены в [../examples/PROXY.md](../examples/PROXY.md).

**Оглавление**

- NavigateTo — строки 15–17
- TaskTemplates — строки 19–21

## NavigateTo
- `GET /NavigateTo/{appCode}` — Возвращает ссылку на указанное приложение или расширение с одноразовым токеном для авторизации · коды: 200, 400, 500 · примеры
  ← path: appCode:str; query: deepLink?:str → GetResult

## TaskTemplates
- `GET /TaskTemplates/{codeDynamicPart}` — Перенаправляет запрос на электронный паспорт оборудования · коды: 307, 400, 500 · примеры
  ← path: codeDynamicPart:str; header: referer?:str
