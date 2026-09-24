# LIC — примеры

> **Что здесь:** блоки примеров запросов/ответов ручек сервиса LIC, вынесенные из `endpoints/LIC.md`. Сигнатуры и типы — там же и в `schemas/LIC.md`.

## LicenseScanner

### `GET /LicenseScanner/State`

## Пример запроса:
`GET /LicenseScanner/State`
            
## Пример успешного ответа (200):
```json
1
```
Возможные значения HubEx.Actor.LIC.Watcher.Interfaces.WatcherStateEnum:
- `0` (`Stopped`) — сервис мониторинга не работает. Это же значение возвращается, если актор недоступен.
- `1` (`Started`) — сервис мониторинга запущен.
            
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: доступ запрещён.
