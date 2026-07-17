# PROXY — справочник ручек

> **Что здесь:** все ручки сервиса PROXY (API for remote calling 3rd party services.): сигнатуры, параметры, права. Типы — schemas/PROXY.md. Сгенерировано из swagger.
> **Когда сюда идти:** найти ручку и её вход/выход. Типы — `schemas/PROXY.md`; грабли — `notes/PROXY.md` (если есть).
> **Источник:** swagger сервиса PROXY · файл генерируется пайплайном — руками не править.

Base: `{BASE_URL}/PROXY`

**Оглавление**

- Bypass — строки 15–18
- NavigateTo — строки 20–23
- TaskTemplates — строки 25–28

## Bypass
- `POST /Bypass` · коды: 200
  ← body: PostData → PostResult
  Для выполнения данного метода пользователь должен быть **TenantMember**.

## NavigateTo
- `GET /NavigateTo/{appCode}` · коды: 200
  ← path: appCode:str; query: deepLink?:str → GetResult
  Для выполнения данного метода пользователь должен быть **TenantMember**.

## TaskTemplates
- `GET /TaskTemplates/{codeDynamicPart}` · коды: 307
  ← path: codeDynamicPart:str; header: referer?:str
  Выполнение данного метода резрешино от **анонимного пользователя**.
