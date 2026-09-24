# NEWS — примеры

> **Что здесь:** блоки примеров запросов/ответов ручек сервиса NEWS, вынесенные из `endpoints/NEWS.md`. Сигнатуры и типы — там же и в `schemas/NEWS.md`.

## Articles

### `GET /Articles`

## Пример запроса:
`GET /Articles?isRead=false&isPublished=true`
            
## Пример успешного ответа (200):
```json
{
  "1": {
    "id": 1,
    "title": "Обновление системы",
    "text": "Текст новости",
    "footer": "Команда HubEx"
  }
}
```
## Негативные сценарии:
- 204 NoContent: новости не найдены.
- 206 PartialContent: частичный ответ при использовании Range-заголовка.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав ArticleListForTenantMember.
