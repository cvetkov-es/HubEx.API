# CM — схемы

> **Что здесь:** определения типов запросов/ответов сервиса CM. Ручки, ссылающиеся на них — `endpoints/CM.md`.

```
type DataClientsCoordinateData { accuracy?: float /* Точность определения координат, метры */, altitude?: float /* Высота над уровнем моря, метры */, bearing?: float /* Азимут (направление движения), градусы */, latitude?: float /* Широта */, longitude?: float /* Долгота */, speed?: float /* Скорость движения, м/с */ }
type DataClientsPostData { accuracy?: float /* Точность определения координат, метры */, altitude?: float /* Высота над уровнем моря, метры */, bearing?: float /* Азимут (направление движения), градусы */, clientTimestamp?: datetime /* Дата и время события в UTC */, coordinate?: str /* Координаты в формате "широта:долгота" */, coords?: DataClientsCoordinateData, speed?: float /* Скорость движения, м/с */, timestamp?: datetime }
type ExceptionHandlingModelsErrorModel { arguments?: map<str>, code?: str, message?: str, traceIdentifier?: str }
type ResultsClientsLocationPostResult { clientId?: str /* Уникальный идентификатор клиента (устройства) */, clientOffset?: int /* Смещение часового пояса клиента в минутах от UTC */ }
```
