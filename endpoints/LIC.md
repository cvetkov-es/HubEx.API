# LIC — справочник ручек

> **Что здесь:** все ручки сервиса LIC (API for LIC in HubEx): сигнатуры, параметры, права. Типы — schemas/LIC.md. Сгенерировано из swagger.
> **Когда сюда идти:** найти ручку и её вход/выход. Типы — `schemas/LIC.md`; грабли — `notes/LIC.md` (если есть).
> **Источник:** swagger сервиса LIC · файл генерируется пайплайном — руками не править.

Base: `{BASE_URL}/LIC`

## LicenseScanner
- `POST /LicenseScanner/Start` — Запускает сервис периодического мониторинга · права: LicenseServiceMonitorManagement · коды: 202
- `GET /LicenseScanner/State` — Проверка состояния сервиса мониторинга лицензий · коды: 200
  → WatcherStateEnum
- `POST /LicenseScanner/Stop` — Останавливает сервис периодического мониторинга · права: LicenseServiceMonitorManagement · коды: 202
