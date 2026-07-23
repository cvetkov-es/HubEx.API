# CM — схемы

> **Что здесь:** определения типов запросов/ответов сервиса CM. Ручки, ссылающиеся на них — `endpoints/CM.md`.

```
type CoordinateData { accuracy?: float /* Точность */, altitude?: float /* Высота */, bearing?: float /* Азимут */, latitude?: float /* Широта */, longitude?: float /* Долгота */, speed?: float /* Скорость */ }
type PostData { accuracy?: float /* Точность */, altitude?: float /* Высота */, bearing?: float /* Азимут */, clientTimestamp?: datetime /* Дата события UTC */, coordinate?: str /* Координаты в формате "широта:долгота" */, coords?: CoordinateData, speed?: float /* Скорость */, timestamp?: datetime /* Дата события UTC */ }
```
