# Вход для агентов

Это автономный справочник API HubEx для ИИ-агентов. **Перед задачей прочитай [README.md](README.md).**

Критичное, дублируется намеренно:
- Ручка API → [overview.md](overview.md) (какой сервис) → `endpoints/<SVC>.md` (сигнатура) → `schemas/<SVC>.md` (точные типы) → `notes/<SVC>.md` (грабли).
- Сущность/связь без известной ручки → [xref.md](xref.md) (кросс-индекс ресурсов, генерируется) → `endpoints/<SVC>.md` (оглавление → секция) → `schemas/<SVC>.md` → `notes/<SVC>.md`; [entity-map.md](entity-map.md) — тот же манёвр по бизнес-семантике, рукописный.
- `endpoints/**`, `schemas/**`, `examples/**`, `xref.md` руками не правь — их ведёт пайплайн (`python3 tools/api_cli.py update`). llms.txt в репо нет — это экспорт в `dist/` (`export-llms`), операция мейнтейнера.
- Нашёл особенность, которой нет в swagger, — запиши в `notes/<SVC>.md`; не противоречь наблюдаемому поведению API (не `endpoints/`/`schemas/` буквально — генератор часть swagger вычищает осознанно: `Authorization`/`Range`/`offset`/`fetch`, `401`/`403`, описания параметров, `example`).
- Не выдумывай ручки: нет в `endpoints/` — нет в API; но нет параметра/кода/заголовка в `endpoints/` ещё не значит, что его нет в swagger — сверяйся напрямую.
- `tools/`, `cli/` — git-сабмодули; для обновления/живого доступа: `git submodule update --init <путь>`.
- Живая запись в тенант — только dry-run → явное подтверждение человека (`cli/hubex_cli.py api write ... --confirm`).
