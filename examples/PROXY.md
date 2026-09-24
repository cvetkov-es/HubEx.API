# PROXY — примеры

> **Что здесь:** блоки примеров запросов/ответов ручек сервиса PROXY, вынесенные из `endpoints/PROXY.md`. Сигнатуры и типы — там же и в `schemas/PROXY.md`.

## Bypass

### `POST /Bypass`

## Пример запроса:
`POST /Bypass`
            
```json
{
  "url": "https://api.example.com/v1/items",
  "method": "POST",
  "headers": [
    { "key": "Content-Type", "value": "application/json" },
    { "key": "Authorization", "value": "Bearer <token>" }
  ],
  "body": "eyJuYW1lIjoiZGVtbyJ9"
}
```
            
## Пример успешного ответа (200):
```json
{
  "headers": {
    "content-type": ["application/json; charset=utf-8"]
  },
  "content": "eyJpZCI6MTIzfQ==",
  "statusCode": 200
}
```
Поле `content` содержит тело ответа, закодированное в Base64.
            
## Негативные сценарии:
- 400 BadRequest: некорректные входные данные, неподдерживаемый метод, отсутствует Content-Type при передаче тела запроса или ошибка выполнения внешнего запроса.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: пользователь аутентифицирован, но не соответствует политике `TENANT_MEMBER`.

## NavigateTo

### `GET /NavigateTo/{appCode}`

## Пример запроса:
`GET /NavigateTo/MainWeb?deepLink=/tasks/123`
            
Параметр запроса OpenAPI: только `deepLink` (query). Дополнительные query-параметры запроса,
кроме `deepLink`, при наличии переносятся в итоговый URL в теле ответа.
            
## Пример успешного ответа (200):
```json
{
  "url": "https://app.hubex.ru/tenant-name/tasks/123?oneTimeLoginToken=abc123&tenantID=1&tenantUrlName=tenant-name"
}
```
Поля `oneTimeLoginToken`, `tenantID` и `tenantUrlName` не являются параметрами этого API:
сервис добавляет их в строку `url` ответа, когда для целевого приложения включена одноразовая авторизация.
            
## Негативные сценарии:
- 400 BadRequest: некорректный `deepLink` или для найденного `appCode` не удалось сформировать URL приложения.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: пользователь аутентифицирован, но не соответствует политике `TENANT_MEMBER`.
- 500 InternalServerError: неизвестный пакетный `appCode` (пакет не найден) — в текущей реализации возможен сбой до проверки URL.

## TaskTemplates

### `GET /TaskTemplates/{codeDynamicPart}`

## Пример запроса:
`GET /TaskTemplates/abc123`
            
Заголовки:
- Referer: https://example.com/tasktemplates/abc123
            
## Пример успешного ответа (307):
HTTP 307 Temporary Redirect
            
Заголовок ответа:
- Location: https://plate.hubex.ru/assets/<taskTemplateID>
            
## Негативные сценарии:
- 400 BadRequest: не указана динамическая часть кода, заголовок Referer отсутствует или не совпадает с `codeDynamicPart`.
- 500 InternalServerError: либо не настроен URL сервиса паспортов.
