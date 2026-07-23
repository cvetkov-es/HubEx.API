# LIC — справочник ручек

> **Что здесь:** только read-ручки (GET/HEAD) сервиса LIC (API for LIC in HubEx): сигнатуры, параметры, права. Типы — schemas/LIC.md.
> **Когда сюда идти:** найти ручку и её вход/выход. Типы — `schemas/LIC.md`; грабли — `notes/LIC.md` (если есть).
> **Линза read-only:** здесь только GET/HEAD. Write-ручки (POST/PUT/PATCH/DELETE) и их типы в API **существуют**, но в эту линзу не входят — не делай из их отсутствия здесь вывода, что их нет в API.

Base: `{BASE_URL}/LIC`

**Оглавление**

- LicenseScanner — строки 13–15

## LicenseScanner
- `GET /LicenseScanner/State` — Проверка состояния сервиса мониторинга лицензий · коды: 200
  → WatcherStateEnum
