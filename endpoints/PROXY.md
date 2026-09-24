# PROXY — справочник ручек

> **Что здесь:** все ручки сервиса PROXY (API for remote calling 3rd party services.): сигнатуры, параметры, права. Типы — schemas/PROXY.md.
> **Когда сюда идти:** найти ручку и её вход/выход. Типы — `schemas/PROXY.md`; грабли — `notes/PROXY.md` (если есть).

Base: `{BASE_URL}/PROXY`
> Примеры ответов вынесены в [../examples/PROXY.md](../examples/PROXY.md).

**Оглавление**

- Bypass — строки 15–17
- NavigateTo — строки 19–21
- TaskTemplates — строки 23–25

## Bypass
- `POST /Bypass` — Прокидывает запрос на заданный в теле адрес, применяя к нему дополнительные заголовки по имени домена · коды: 200, 400 · примеры
  ← body: PostData → PostResult

## NavigateTo
- `GET /NavigateTo/{appCode}` — Возвращает ссылку на указанное приложение или расширение с одноразовым токеном для авторизации · коды: 200, 400, 500 · примеры
  ← path: appCode:str; query: deepLink?:str → GetResult

## TaskTemplates
- `GET /TaskTemplates/{codeDynamicPart}` — Перенаправляет запрос на электронный паспорт оборудования · коды: 307, 400, 500 · примеры
  ← path: codeDynamicPart:str; header: referer?:str
