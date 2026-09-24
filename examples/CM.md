# CM — примеры

> **Что здесь:** блоки примеров запросов/ответов ручек сервиса CM, вынесенные из `endpoints/CM.md`. Сигнатуры и типы — там же и в `schemas/CM.md`.

## Clients

### `POST /Clients/locations`

## Пример запроса:
`POST /Clients/locations`
            
Заголовки:
- `X-CLIENT-IDENTIFIER` — уникальный идентификатор клиента (устройства), обязателен.
- `X-Client-Utc-Offset` — смещение часового пояса клиента в минутах от UTC, необязателен (по умолчанию `0`).
- `X-Application-ID` — идентификатор приложения-источника запроса (enum 1..6), необязателен.
            
```json
[
  {
    "coordinate": "55.75:37.62",
    "clientTimestamp": "2026-08-17T08:30:00Z",
    "altitude": 150.5,
    "bearing": 90.0,
    "accuracy": 10.0,
    "speed": 5.2
  }
]
```
            
Альтернативный формат координат через объект `coords`:
```json
[
  {
    "coords": {
      "latitude": 55.75,
      "longitude": 37.62,
      "altitude": 150.5,
      "accuracy": 10.0,
      "speed": 5.2,
      "bearing": 90.0
    },
    "timestamp": "2026-08-17T08:30:00Z"
  }
]
```
            
## Пример успешного ответа (200):
```json
{
  "clientId": "device-uuid-12345",
  "clientOffset": 180
}
```
            
## Негативные сценарии:
- 404 Not Found: не передан обязательный заголовок `X-CLIENT-IDENTIFIER`.
- 409 Conflict: пустое или отсутствующее тело запроса.
- 409 Conflict: отсутствуют или некорректны координаты (`coordinate` / `coords`).
- 409 Conflict: `clientTimestamp` раньше 2018-10-01.
