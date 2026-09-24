# LIC — справочник ручек

> **Что здесь:** все ручки сервиса LIC (API for LIC in HubEx): сигнатуры, параметры, права. Типы — schemas/LIC.md.
> **Когда сюда идти:** найти ручку и её вход/выход. Типы — `schemas/LIC.md`; грабли — `notes/LIC.md` (если есть).

Base: `{BASE_URL}/LIC`
> Примеры ответов вынесены в [../examples/LIC.md](../examples/LIC.md).

**Оглавление**

- LicenseScanner — строки 13–17

## LicenseScanner
- `POST /LicenseScanner/Start` — Запуск сервиса периодического мониторинга лицензий · коды: 202 · примеры
- `GET /LicenseScanner/State` — Получение состояния сервиса мониторинга лицензий · коды: 200 · примеры
  → WatcherStateEnum
- `POST /LicenseScanner/Stop` — Остановка сервиса периодического мониторинга лицензий · коды: 202 · примеры
