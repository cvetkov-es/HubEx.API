# Вход для Claude Code

Это автономный справочник API HubEx для ИИ-агентов. **Перед задачей прочитай [README.md](README.md).**

Критичное, дублируется намеренно:
- Ручка API → [overview.md](overview.md) (какой сервис) → `endpoints/<SVC>.md` (сигнатура) → `schemas/<SVC>.md` (точные типы) → `notes/<SVC>.md` (грабли).
- `endpoints/**`, `schemas/**`, `snapshots/**`, `llms*.txt` руками не правь — их ведёт пайплайн (`python3 tools/api_cli.py update`).
- Нашёл особенность, которой нет в swagger, — запиши в `notes/<SVC>.md`; противоречить `snapshots/` нельзя.
- Не выдумывай ручки: нет в `endpoints/` — нет в API.
- `snapshots/*.json` целиком не читай (до 1.2 МБ) — только grep/точечная вырезка.
- `tools/`, `cli/` — git-сабмодули; для обновления/живого доступа: `git submodule update --init <путь>`.
- Живая запись в тенант — только dry-run → явное подтверждение человека (`cli/hubex_cli.py api write ... --confirm`).
