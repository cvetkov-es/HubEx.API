# PROXY — справочник ручек

> **Что здесь:** только read-ручки (GET/HEAD) сервиса PROXY (API for remote calling 3rd party services.): сигнатуры, параметры, права. Типы — schemas/PROXY.md.
> **Когда сюда идти:** найти ручку и её вход/выход. Типы — `schemas/PROXY.md`; грабли — `notes/PROXY.md` (если есть).
> **Линза read-only:** здесь только GET/HEAD. Write-ручки (POST/PUT/PATCH/DELETE) и их типы в API **существуют**, но в эту линзу не входят — не делай из их отсутствия здесь вывода, что их нет в API.

Base: `{BASE_URL}/PROXY`

**Оглавление**

- NavigateTo — строки 14–17
- TaskTemplates — строки 19–22

## NavigateTo
- `GET /NavigateTo/{appCode}` · коды: 200
  ← path: appCode:str; query: deepLink?:str → GetResult
  Для выполнения данного метода пользователь должен быть **TenantMember**.

## TaskTemplates
- `GET /TaskTemplates/{codeDynamicPart}` · коды: 307
  ← path: codeDynamicPart:str; header: referer?:str
  Выполнение данного метода резрешино от **анонимного пользователя**.
