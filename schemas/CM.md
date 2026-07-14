# CM — схемы

> **Что здесь:** определения типов запросов/ответов сервиса CM. Ручки, ссылающиеся на них — `endpoints/CM.md`.
> **Источник:** `snapshots/CM.json` · файл генерируется пайплайном — руками не править.

```
type CoordinateData { altitude?: float /* Высота */, bearing?: float /* Азимут */, accuracy?: float /* Точность */, speed?: float /* Скорость */, latitude?: float /* Широта */, longitude?: float /* Долгота */ }
type PostData { coordinate?: str /* Координаты в формате "широта:долгота" */, clientTimestamp?: datetime /* Дата события UTC */, timestamp?: datetime /* Дата события UTC */, altitude?: float /* Высота */, bearing?: float /* Азимут */, accuracy?: float /* Точность */, speed?: float /* Скорость */, coords?: CoordinateData }
```
