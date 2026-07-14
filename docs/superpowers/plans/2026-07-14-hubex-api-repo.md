# HubEx.API — доменный репозиторий API — Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Создать три репозитория — `HubEx.API` (контент для ИИ-агентов: справочники ручек + снапшоты + llms.txt), `HubEx.API.Pipeline` (пайплайн обновления, сабмодуль `tools/`), `HubEx.API.CLI` (живой доступ, сабмодуль `cli/`) — с детерминированным генератором `endpoints/` и пилотом формата перед раскаткой.

**Architecture:** Пайплайн копирует api-модули из монорепы `HubEx.AI-2.0/tools/update/` и дорабатывает: снапшоты/выходы пишутся в корень суперпроекта (`snapshots/`, `endpoints/`, `notes/`, `llms.txt`), резолюция корня — `Path(__file__).resolve().parents[2]` (как у HubEx.Wiki). Новые чистые модули: `endpoints_gen` (swagger → компактный md-справочник), `llms_txt` (индекс + склейка), `notes_patch` (точечная правка заметок моделью). Спека: `docs/superpowers/specs/2026-07-14-hubex-api-repo-design.md`.

**Tech Stack:** Python 3.10, pytest, requests, git submodules, gh CLI.

## Global Constraints

- **Монорепа `HubEx.AI-2.0` не меняется** — из неё только читаем/копируем.
- **Host-agnostic:** URL сабмодулей в `.gitmodules` — только относительные (`../HubEx.API.Pipeline.git`, `../HubEx.API.CLI.git`).
- **Все репо — под `cvetkov-es`** (рядом, иначе относительный URL не резолвится).
- **Генерируемые файлы (`endpoints/`, `snapshots/`, `llms.txt`, `llms-full.txt`) — без штампа даты**; дату даёт git-история.
- **`endpoints_gen` — детерминированный, без модели.** Модель — только в `notes_patch` (`--recompress`) и точечная правка запрещает полную регенерацию.
- **Пилот (Task 11) — human-gated:** массовый засев `endpoints/` только после одобрения формата мейнтейнером.
- **Human-gated шаги** (создание GitHub-репо, любой `push`) — только после подтверждения пользователя.
- **Коммиты:** русский, conventional commits, последняя строка `Co-Authored-By: Claude Fable 5 <noreply@anthropic.com>`.
- **git-идентичность** каждого нового репо: `git config user.name "cvetkov-es" && git config user.email "95337410+cvetkov-es@users.noreply.github.com"`.
- Тесты: офлайн-прогон `python3 -m pytest -m "not live" -q` должен быть зелёным в конце каждой задачи.
- Пути: контент `/home/cvetkov_es/development/HubEx.API`; пайплайн `/home/cvetkov_es/development/HubEx.API.Pipeline`; CLI `/home/cvetkov_es/development/HubEx.API.CLI`; монорепа `/home/cvetkov_es/development/HubEx.AI-2.0`.

---

## File Structure

**HubEx.API.Pipeline** (разрабатывается отдельно, подключается сабмодулем `tools/`):
- `api_cli.py` — CLI: `update [--service SVC ...] [--report-file PATH] [--recompress]` (новый файл).
- `update/__init__.py`, `update/api_manifest.py`, `update/api_fetch.py`, `update/api_diff.py`, `update/swagger_slice.py`, `update/model_client.py`, `update/recompress_guard.py` — копии из монорепы, без изменений.
- `update/snapshot_store.py` — переработка: `snapshots/<SVC>.json` в корне суперпроекта.
- `update/endpoints_gen.py` — **новый**: swagger → `endpoints/<SVC>.md` + проверка полноты.
- `update/llms_txt.py` — **новый**: `llms.txt` + `llms-full.txt`.
- `update/notes_patch.py` — **новый**: точечная правка `notes/<SVC>.md` моделью + guard.
- `update/prompts/notes-patch.md` — **новый**: фикс-промпт.
- `update/pipeline.py` — переработка: снапшот + endpoints + llms; `--recompress` → notes_patch.
- `update/report.py` — копия с правкой путей в подсказках.
- `lint/check_links.py` — копия с упрощением исключений.
- `tests/` — копии тестов копируемых модулей + новые тесты новых модулей.
- `conftest.py`, `pytest.ini`, `requirements.txt`, `README.md`, `.gitignore`, `docs/superpowers/` (спека+план переезжают сюда).

**HubEx.API.CLI** (сабмодуль `cli/`):
- `hubex_cli.py` — копия из монорепы **без** групп `db` и `update`.
- `hubex_core/` — `__init__.py`, `api.py`, `auth.py`, `config.py`, `safety.py`, `tenants.py` (**без** `db.py`).
- `tenant_base_url_overrides.yaml`, `tenant_notes.yaml`, `SAFETY.md`, `tests/`, `conftest.py`, `pytest.ini`, `requirements.txt`, `README.md`, `.gitignore`.

**HubEx.API** (контент):
- `README.md`, `CLAUDE.md`, `AGENTS.md` — роутер (новые).
- `overview.md`, `entity-map.md` — перенос из `knowledge/api/` с правками.
- `notes/WORK.md` — засев заметок (единственный сервис с ⚠-граблями в монорепе).
- `endpoints/`, `snapshots/`, `llms.txt`, `llms-full.txt` — засеваются пайплайном (Task 18).
- `.gitmodules`, `tools/`, `cli/` — сабмодули; `.gitignore`.

---

### Task 1: Каркас HubEx.API.Pipeline + перенос неизменных модулей

**Files:**
- Create: `/home/cvetkov_es/development/HubEx.API.Pipeline/` (git-репо)
- Copy: `update/{__init__,api_manifest,api_fetch,api_diff,swagger_slice,model_client,recompress_guard}.py`, их тесты и фикстуры, `conftest.py`
- Create: `pytest.ini`, `.gitignore`, `requirements.txt`
- Move: `docs/superpowers/` из `/home/cvetkov_es/development/HubEx.API/`

**Interfaces:**
- Produces: пакет `update` с функциями `api_manifest.fetch_manifest()`, `api_fetch.fetch_swagger(url)`, `api_fetch.normalize(swagger) -> str`, `api_diff.diff_swagger(old, new) -> changeset`, `api_diff.is_empty(cs)`, `api_diff._operations(swagger) -> {"METHOD /path": op}`, `api_diff._schemas(swagger) -> dict`, `recompress_guard.find_phantoms(md, swagger) -> list[str]`, `model_client.run_model(prompt) -> str`.

- [ ] **Step 1: Создать репозиторий и скопировать модули**

```bash
MONO=/home/cvetkov_es/development/HubEx.AI-2.0/tools
P=/home/cvetkov_es/development/HubEx.API.Pipeline
mkdir -p $P/update/prompts $P/tests/fixtures $P/lint
cd $P && git init -b main
git config user.name "cvetkov-es" && git config user.email "95337410+cvetkov-es@users.noreply.github.com"
cp $MONO/update/__init__.py $MONO/update/api_manifest.py $MONO/update/api_fetch.py \
   $MONO/update/api_diff.py $MONO/update/swagger_slice.py $MONO/update/model_client.py \
   $MONO/update/recompress_guard.py $P/update/
cp $MONO/conftest.py $P/
cp $MONO/tests/test_update_api_diff.py $MONO/tests/test_update_api_fetch.py \
   $MONO/tests/test_update_api_manifest.py $MONO/tests/test_update_model_client.py \
   $MONO/tests/test_update_swagger_slice.py $MONO/tests/test_update_recompress_guard.py $P/tests/
cp $MONO/tests/fixtures/doc_index.html $P/tests/fixtures/
```
Expected: файлы на месте, `git status` показывает untracked.

- [ ] **Step 2: Создать pytest.ini, .gitignore, requirements.txt**

`pytest.ini`:
```ini
[pytest]
testpaths = tests
markers =
    live: требует сети к api.hubex.ru / doc.hubex.ru (пропускается офлайн: -m "not live")
```
`.gitignore`:
```gitignore
__pycache__/
*.pyc
.pytest_cache/
```
`requirements.txt` (db-зависимости монорепы не нужны):
```
requests>=2.28
pytest>=7.0
```

- [ ] **Step 3: Прогнать офлайн-тесты**

```bash
cd /home/cvetkov_es/development/HubEx.API.Pipeline && python3 -m pytest -m "not live" -q
```
Expected: все PASS (тесты копируемых модулей самодостаточны: фикстуры + tmp_path). Если тест импортирует выброшенный модуль (`api_draft`, `recompress`) — этот тест сюда не копировался; проверить список Step 1.

- [ ] **Step 4: Перенести docs/superpowers из контент-репо (спека+план живут в пайплайне)**

```bash
cp -r /home/cvetkov_es/development/HubEx.API/docs /home/cvetkov_es/development/HubEx.API.Pipeline/
```
(Удаление из контент-репо — Task 13.)

- [ ] **Step 5: Commit**

```bash
cd /home/cvetkov_es/development/HubEx.API.Pipeline
git add -A
git commit -m "feat: каркас пайплайна — перенос api-модулей из монорепы HubEx.AI-2.0" \
  -m "api_manifest/api_fetch/api_diff/swagger_slice/model_client/recompress_guard + их тесты, без изменений. docs/superpowers — спека и план цикла." \
  -m "Co-Authored-By: Claude Fable 5 <noreply@anthropic.com>"
```

---

### Task 2: snapshot_store под раскладку контент-репо

**Files:**
- Create: `update/snapshot_store.py` (переработка копии)
- Test: `tests/test_snapshot_store.py`

**Interfaces:**
- Produces: `snapshot_store.snapshot_path(service, *, root=None) -> Path` (`<root>/snapshots/<SVC>.json`; дефолт root — `parents[2]` от файла), `read_snapshot(service, *, root=None) -> dict|None`, `write_snapshot(service, normalized_text, *, root=None)`.

- [ ] **Step 1: Написать падающий тест** — `tests/test_snapshot_store.py`:

```python
import json

from update import snapshot_store


def test_snapshot_path_layout(tmp_path):
    p = snapshot_store.snapshot_path("WORK", root=tmp_path)
    assert p == tmp_path / "snapshots" / "WORK.json"


def test_roundtrip(tmp_path):
    assert snapshot_store.read_snapshot("WORK", root=tmp_path) is None
    snapshot_store.write_snapshot("WORK", json.dumps({"openapi": "3.0.1"}), root=tmp_path)
    assert snapshot_store.read_snapshot("WORK", root=tmp_path) == {"openapi": "3.0.1"}


def test_default_root_is_superproject():
    # tools/update/snapshot_store.py -> parents[2] = корень суперпроекта
    assert snapshot_store.REPO_ROOT.name not in ("update", "tools")
```

- [ ] **Step 2: Убедиться, что падает**

Run: `python3 -m pytest tests/test_snapshot_store.py -q` → FAIL (`No module named 'update.snapshot_store'`).

- [ ] **Step 3: Реализация** — `update/snapshot_store.py`:

```python
"""Чтение/запись нормализованных swagger-снапшотов: snapshots/<SVC>.json в корне контент-репо."""
import json
from pathlib import Path

REPO_ROOT = Path(__file__).resolve().parents[2]


def snapshot_path(service: str, *, root: Path | None = None) -> Path:
    base = root if root is not None else REPO_ROOT
    return base / "snapshots" / f"{service}.json"


def read_snapshot(service: str, *, root: Path | None = None):
    p = snapshot_path(service, root=root)
    if not p.exists():
        return None
    return json.loads(p.read_text(encoding="utf-8"))


def write_snapshot(service: str, normalized_text: str, *, root: Path | None = None) -> None:
    p = snapshot_path(service, root=root)
    p.parent.mkdir(parents=True, exist_ok=True)
    p.write_text(normalized_text, encoding="utf-8")
```

- [ ] **Step 4: Тесты зелёные** — `python3 -m pytest tests/test_snapshot_store.py -q` → PASS.

- [ ] **Step 5: Commit** — `git add update/snapshot_store.py tests/test_snapshot_store.py && git commit -m "feat(update): snapshot_store — snapshots/<SVC>.json в корне суперпроекта" -m "Co-Authored-By: Claude Fable 5 <noreply@anthropic.com>"`

---

### Task 3: endpoints_gen — разбор шаблонного description

**Files:**
- Create: `update/endpoints_gen.py` (начало модуля)
- Test: `tests/test_endpoints_gen_desc.py`

**Interfaces:**
- Produces: `endpoints_gen.parse_description(desc: str|None) -> {"permissions": list[str], "paginated": bool, "rest": str}`.

Формат description в HubEx swagger (реальные примеры из WORK):
`'<br />* Для выполнения данного метода требуется любое из перечисленных полномочий: **CheckListDelete**<br />* Метод поддерживает диапазонный запрос через строку или заголовок запроса.'`

- [ ] **Step 1: Падающий тест** — `tests/test_endpoints_gen_desc.py`:

```python
from update import endpoints_gen


def test_permissions_and_pagination_extracted():
    d = ("<br />* Для выполнения данного метода требуется любое из перечисленных "
         "полномочий: **CheckListsList**, **CheckListsAdmin**"
         "<br />* Метод поддерживает диапазонный запрос через строку или заголовок запроса.")
    meta = endpoints_gen.parse_description(d)
    assert meta["permissions"] == ["CheckListsList", "CheckListsAdmin"]
    assert meta["paginated"] is True
    assert meta["rest"] == ""


def test_nonstandard_text_lands_in_rest():
    meta = endpoints_gen.parse_description("<br />* Удаляет безвозвратно, восстановление невозможно.")
    assert meta["permissions"] == [] and meta["paginated"] is False
    assert "безвозвратно" in meta["rest"]


def test_empty_and_none():
    assert endpoints_gen.parse_description(None) == {"permissions": [], "paginated": False, "rest": ""}
```

- [ ] **Step 2: Убедиться, что падает** — `python3 -m pytest tests/test_endpoints_gen_desc.py -q` → FAIL.

- [ ] **Step 3: Реализация** — создать `update/endpoints_gen.py`:

```python
"""Генерация endpoints/<SVC>.md — детерминированный компактный справочник ручек из swagger.

Чистый модуль: ни сети, ни файлов, ни модели. Формат утверждается пилотом (спека §5, §9).
Без штампа даты — дату даёт git-история.
"""
import re

from update.api_diff import _operations, _schemas

_BR_RE = re.compile(r"<br\s*/?>", re.IGNORECASE)
_BOLD_RE = re.compile(r"\*\*([^*]+)\*\*")


def parse_description(desc) -> dict:
    """Шаблонный description операции HubEx → полномочия, флаг пагинации, нешаблонный остаток."""
    perms, paginated, rest = [], False, []
    for chunk in _BR_RE.split(desc or ""):
        chunk = chunk.strip().lstrip("*").strip()
        if not chunk:
            continue
        if "полномочи" in chunk:
            perms.extend(_BOLD_RE.findall(chunk))
        elif "диапазонный запрос" in chunk:
            paginated = True
        else:
            rest.append(chunk)
    return {"permissions": perms, "paginated": paginated, "rest": " ".join(rest)}
```

- [ ] **Step 4: Тесты зелёные** — `python3 -m pytest tests/test_endpoints_gen_desc.py -q` → PASS.

- [ ] **Step 5: Commit** — `git add update/endpoints_gen.py tests/test_endpoints_gen_desc.py && git commit -m "feat(endpoints): разбор шаблонного description — права, пагинация, остаток" -m "Co-Authored-By: Claude Fable 5 <noreply@anthropic.com>"`

---

### Task 4: endpoints_gen — короткие имена схем

**Files:**
- Modify: `update/endpoints_gen.py`
- Test: `tests/test_endpoints_gen_names.py`

**Interfaces:**
- Produces: `endpoints_gen.short_names(schemas: dict) -> dict[full -> short]` — срез неймспейс-префиксов, коллизии уточняются минимальным хвостом сегментов.

- [ ] **Step 1: Падающий тест** — `tests/test_endpoints_gen_names.py`:

```python
from update import endpoints_gen


def test_namespace_stripped():
    names = endpoints_gen.short_names({"HubEx.Service.WORK.Api.Data.TaskResult": {}})
    assert names == {"HubEx.Service.WORK.Api.Data.TaskResult": "TaskResult"}


def test_collision_gets_minimal_suffix():
    schemas = {
        "HubEx.Service.WORK.Api.Data.Tasks.AddData": {},
        "HubEx.Service.WORK.Api.Data.CheckLists.AddData": {},
    }
    names = endpoints_gen.short_names(schemas)
    assert names["HubEx.Service.WORK.Api.Data.Tasks.AddData"] == "Tasks.AddData"
    assert names["HubEx.Service.WORK.Api.Data.CheckLists.AddData"] == "CheckLists.AddData"


def test_plain_name_untouched():
    assert endpoints_gen.short_names({"ErrorModel": {}}) == {"ErrorModel": "ErrorModel"}
```

- [ ] **Step 2: FAIL** — `python3 -m pytest tests/test_endpoints_gen_names.py -q` → `AttributeError: short_names`.

- [ ] **Step 3: Реализация** — добавить в `update/endpoints_gen.py`:

```python
def short_names(schemas: dict) -> dict:
    """Полное имя схемы → короткое: последние сегменты по точкам, минимум до уникальности."""
    fulls = sorted(schemas)
    out = {}
    for full in fulls:
        segs = full.split(".")
        for n in range(1, len(segs) + 1):
            tail = segs[-n:]
            if not any(f != full and f.split(".")[-n:] == tail for f in fulls):
                out[full] = ".".join(tail)
                break
        else:
            out[full] = full
    return out
```

- [ ] **Step 4: PASS** — `python3 -m pytest tests/test_endpoints_gen_names.py -q`.

- [ ] **Step 5: Commit** — `git add -A && git commit -m "feat(endpoints): короткие имена схем со срезом неймспейсов" -m "Co-Authored-By: Claude Fable 5 <noreply@anthropic.com>"`

---

### Task 5: endpoints_gen — компактная запись типов

**Files:**
- Modify: `update/endpoints_gen.py`
- Test: `tests/test_endpoints_gen_types.py`

**Interfaces:**
- Produces: `endpoints_gen.type_str(schema, names) -> str` — `$ref`→короткое имя, `int/float/str/bool/datetime/uuid/date/file`, `T[]`, `map<T>`, `enum(1=A, 2=B)`, инлайн-объекты `{ a: int, b?: str /* комм */ }`, `allOf` → `{ ...Base, extra: int }`.

- [ ] **Step 1: Падающий тест** — `tests/test_endpoints_gen_types.py`:

```python
from update import endpoints_gen

NAMES = {"NS.TaskResult": "TaskResult", "NS.Base": "Base"}


def test_scalars_and_formats():
    assert endpoints_gen.type_str({"type": "integer", "format": "int32"}, {}) == "int"
    assert endpoints_gen.type_str({"type": "number"}, {}) == "float"
    assert endpoints_gen.type_str({"type": "boolean"}, {}) == "bool"
    assert endpoints_gen.type_str({"type": "string"}, {}) == "str"
    assert endpoints_gen.type_str({"type": "string", "format": "date-time"}, {}) == "datetime"
    assert endpoints_gen.type_str({"type": "string", "format": "uuid"}, {}) == "uuid"


def test_ref_array_map():
    assert endpoints_gen.type_str({"$ref": "#/components/schemas/NS.TaskResult"}, NAMES) == "TaskResult"
    assert endpoints_gen.type_str(
        {"type": "array", "items": {"$ref": "#/components/schemas/NS.TaskResult"}}, NAMES) == "TaskResult[]"
    assert endpoints_gen.type_str(
        {"type": "object", "additionalProperties": {"type": "string"}}, {}) == "map<str>"


def test_enum_with_names():
    s = {"type": "integer", "enum": [1, 2], "x-enumNames": ["Active", "Blocked"]}
    assert endpoints_gen.type_str(s, {}) == "enum(1=Active, 2=Blocked)"
    assert endpoints_gen.type_str({"type": "integer", "enum": [1, 2]}, {}) == "enum(1, 2)"


def test_inline_object_with_required_and_comment():
    s = {"type": "object", "required": ["id"],
         "properties": {"id": {"type": "integer"},
                        "name": {"type": "string", "description": "Имя"}}}
    assert endpoints_gen.type_str(s, {}) == "{ id: int, name?: str /* Имя */ }"


def test_allof_spread():
    s = {"allOf": [{"$ref": "#/components/schemas/NS.Base"},
                   {"type": "object", "properties": {"extra": {"type": "integer"}}}]}
    assert endpoints_gen.type_str(s, NAMES) == "{ ...Base, extra?: int }"
```

- [ ] **Step 2: FAIL** — `python3 -m pytest tests/test_endpoints_gen_types.py -q`.

- [ ] **Step 3: Реализация** — добавить в `update/endpoints_gen.py`:

```python
_FORMAT_MAP = {"date-time": "datetime", "date": "date", "uuid": "uuid", "binary": "file"}
_COMMENT_MAX = 80


def _ref_name(ref: str, names: dict) -> str:
    full = ref.rsplit("/", 1)[-1]
    return names.get(full, full)


def _props(schema: dict, names: dict) -> str:
    req = set(schema.get("required") or [])
    parts = []
    for pname, ps in (schema.get("properties") or {}).items():
        opt = "" if pname in req else "?"
        piece = f"{pname}{opt}: {type_str(ps, names)}"
        d = ps.get("description", "").strip() if isinstance(ps, dict) else ""
        if d and len(d) <= _COMMENT_MAX:
            piece += f" /* {d} */"
        parts.append(piece)
    return ", ".join(parts)


def type_str(schema, names: dict) -> str:
    """JSON-схема → компактная запись типа (дом-стиль)."""
    if not isinstance(schema, dict) or not schema:
        return "any"
    if "$ref" in schema:
        return _ref_name(schema["$ref"], names)
    if "allOf" in schema:
        parts = []
        for sub in schema["allOf"]:
            if "$ref" in sub:
                parts.append("..." + _ref_name(sub["$ref"], names))
            elif sub.get("properties"):
                parts.append(_props(sub, names))
        return "{ " + ", ".join(p for p in parts if p) + " }"
    if "enum" in schema:
        labels = schema.get("x-enumNames") or []
        vals = schema["enum"]
        pairs = [f"{v}={l}" for v, l in zip(vals, labels)] if labels else [str(v) for v in vals]
        return "enum(" + ", ".join(pairs) + ")"
    t = schema.get("type")
    if t == "array":
        return type_str(schema.get("items"), names) + "[]"
    if t == "string":
        return _FORMAT_MAP.get(schema.get("format"), "str")
    if t == "integer":
        return "int"
    if t == "number":
        return "float"
    if t == "boolean":
        return "bool"
    ap = schema.get("additionalProperties")
    if isinstance(ap, dict) and ap:
        return f"map<{type_str(ap, names)}>"
    if schema.get("properties"):
        return "{ " + _props(schema, names) + " }"
    return "map" if t == "object" else "any"
```

- [ ] **Step 4: PASS** — `python3 -m pytest tests/test_endpoints_gen_types.py -q`.

- [ ] **Step 5: Commit** — `git add -A && git commit -m "feat(endpoints): компактная запись типов из JSON-схем" -m "Co-Authored-By: Claude Fable 5 <noreply@anthropic.com>"`

---

### Task 6: endpoints_gen — рендер файла и проверка полноты

**Files:**
- Modify: `update/endpoints_gen.py`
- Test: `tests/test_endpoints_gen_render.py`

**Interfaces:**
- Produces: `endpoints_gen.render_endpoints(service, swagger) -> str` (весь md-файл), `endpoints_gen.missing_operations(md, swagger) -> list[str]` (ручки свагера, отсутствующие в md; пустой список = полнота).

- [ ] **Step 1: Падающий тест** — `tests/test_endpoints_gen_render.py`:

```python
from update import endpoints_gen

SWAGGER = {
    "openapi": "3.0.1",
    "info": {"title": "HubEx WORK API"},
    "paths": {
        "/Tasks": {
            "get": {
                "summary": "Возвращает список заявок",
                "description": ("<br />* Для выполнения данного метода требуется любое из "
                                "перечисленных полномочий: **TasksList**"
                                "<br />* Метод поддерживает диапазонный запрос через строку или заголовок запроса."),
                "parameters": [{"name": "offset", "in": "query", "schema": {"type": "integer"}}],
                "responses": {"200": {"content": {"application/json": {"schema": {
                    "type": "object", "additionalProperties":
                        {"$ref": "#/components/schemas/NS.TaskResult"}}}}}},
            },
            "post": {
                "summary": "Создаёт заявку",
                "requestBody": {"content": {"application/json": {"schema":
                    {"$ref": "#/components/schemas/NS.TaskAdd"}}}},
                "responses": {},
            },
        },
        "/CheckLists": {"get": {"summary": "Список чек-листов", "responses": {}}},
    },
    "components": {"schemas": {
        "NS.TaskResult": {"type": "object", "properties": {"id": {"type": "integer"}}},
        "NS.TaskAdd": {"type": "object", "properties": {"notes": {"type": "string"}}},
    }},
}


def test_render_contains_ops_grouped_and_annotated():
    md = endpoints_gen.render_endpoints("WORK", SWAGGER)
    assert md.startswith("# WORK")
    assert "## Tasks" in md and "## CheckLists" in md
    assert "`GET /Tasks` — Возвращает список заявок · права: TasksList · paginated" in md
    assert "→ map<TaskResult>" in md
    assert "← body: TaskAdd" in md
    assert "type TaskResult { id?: int }" in md
    assert "Обновлено" not in md  # генерируемые файлы без штампа даты


def test_completeness_check():
    md = endpoints_gen.render_endpoints("WORK", SWAGGER)
    assert endpoints_gen.missing_operations(md, SWAGGER) == []
    assert endpoints_gen.missing_operations("# пусто", SWAGGER) == [
        "GET /CheckLists", "GET /Tasks", "POST /Tasks"]
```

- [ ] **Step 2: FAIL** — `python3 -m pytest tests/test_endpoints_gen_render.py -q`.

- [ ] **Step 3: Реализация** — добавить в `update/endpoints_gen.py`:

```python
_HTTP_ORDER = {"GET": 0, "POST": 1, "PUT": 2, "PATCH": 3, "DELETE": 4, "HEAD": 5, "OPTIONS": 6}


def _op_sort_key(op_key: str):
    method, path = op_key.split(" ", 1)
    return (path, _HTTP_ORDER.get(method, 9))


def _group(path: str) -> str:
    segs = [s for s in path.split("/") if s]
    return segs[0].split("{")[0] or "/" if segs else "/"


def _op_io(op: dict, names: dict):
    """(строка входов, тип ответа). Входы: path/query/header-параметры и body."""
    by_loc = {}
    for p in (op.get("parameters") or []):
        loc = p.get("in", "query")
        req = "" if p.get("required") else "?"
        by_loc.setdefault(loc, []).append(f"{p.get('name')}{req}:{type_str(p.get('schema'), names)}")
    ins = [f"{loc}: " + ", ".join(by_loc[loc]) for loc in ("path", "query", "header") if loc in by_loc]
    for spec in ((op.get("requestBody") or {}).get("content") or {}).values():
        ins.append("body: " + type_str(spec.get("schema"), names))
        break
    out = ""
    for code in ("200", "201", "206"):
        for spec in (((op.get("responses") or {}).get(code) or {}).get("content") or {}).values():
            out = type_str(spec.get("schema"), names)
            break
        if out:
            break
    return "; ".join(ins), out


def render_endpoints(service: str, swagger: dict) -> str:
    names = short_names(_schemas(swagger))
    ops = _operations(swagger)
    title = ((swagger.get("info") or {}).get("title") or service).strip()
    lines = [
        f"# {service} — справочник ручек",
        "",
        f"> **Что здесь:** все ручки сервиса {service} ({title}): сигнатуры, параметры, права, схемы. Сгенерировано из swagger.",
        f"> **Когда сюда идти:** найти ручку и её вход/выход. Грабли и правила практики — `notes/{service}.md` (если есть).",
        f"> **Источник:** `snapshots/{service}.json` · файл генерируется пайплайном — руками не править.",
        "",
        f"Base: `{{BASE_URL}}/{service}`",
    ]
    current = None
    for key in sorted(ops, key=_op_sort_key):
        _, path = key.split(" ", 1)
        g = _group(path)
        if g != current:
            lines += ["", f"## {g}"]
            current = g
        op = ops[key]
        meta = parse_description(op.get("description"))
        summary = (op.get("summary") or "").strip()
        line = f"- `{key}`"
        if summary:
            line += f" — {summary}"
        if meta["permissions"]:
            line += " · права: " + ", ".join(meta["permissions"])
        if meta["paginated"]:
            line += " · paginated"
        lines.append(line)
        ins, out = _op_io(op, names)
        io_parts = ([f"← {ins}"] if ins else []) + ([f"→ {out}"] if out else [])
        if io_parts:
            lines.append("  " + " ".join(io_parts))
        if meta["rest"]:
            lines.append(f"  {meta['rest']}")
    schemas = _schemas(swagger)
    if schemas:
        lines += ["", "## Схемы", "```"]
        for full in sorted(schemas, key=lambda f: names[f].lower()):
            lines.append(f"type {names[full]} {type_str(schemas[full], names)}")
        lines.append("```")
    return "\n".join(lines) + "\n"


def missing_operations(md: str, swagger: dict) -> list:
    """Проверка полноты: ручки свагера, отсутствующие в md (пустой список = все на месте)."""
    return sorted(k for k in _operations(swagger) if f"`{k}`" not in md)
```

- [ ] **Step 4: PASS** — `python3 -m pytest tests/test_endpoints_gen_render.py -q`, затем весь набор `python3 -m pytest -m "not live" -q`.

- [ ] **Step 5: Commit** — `git add -A && git commit -m "feat(endpoints): рендер справочника ручек + проверка полноты" -m "Co-Authored-By: Claude Fable 5 <noreply@anthropic.com>"`

---

### Task 7: llms_txt — индекс и полная склейка

**Files:**
- Create: `update/llms_txt.py`
- Test: `tests/test_llms_txt.py`

**Interfaces:**
- Produces: `llms_txt.render_llms_txt(services: list[str]) -> str`; `llms_txt.write_llms_files(*, root=None)` — пишет `<root>/llms.txt` и `<root>/llms-full.txt` из `<root>/endpoints/*.md`.

- [ ] **Step 1: Падающий тест** — `tests/test_llms_txt.py`:

```python
from update import llms_txt


def test_render_llms_txt_format():
    text = llms_txt.render_llms_txt(["WORK", "ADM"])
    assert text.startswith("# HubEx API\n\n> ")
    assert "- [ADM](endpoints/ADM.md): " in text
    assert "- [WORK](endpoints/WORK.md): " in text
    assert text.index("[ADM]") < text.index("[WORK]")  # сортировка
    assert "- [overview.md](overview.md)" in text


def test_write_llms_files(tmp_path):
    ep = tmp_path / "endpoints"
    ep.mkdir()
    (ep / "SLA.md").write_text("# SLA — справочник ручек\nтело\n", encoding="utf-8")
    (ep / "ADM.md").write_text("# ADM — справочник ручек\nтело2\n", encoding="utf-8")
    llms_txt.write_llms_files(root=tmp_path)
    idx = (tmp_path / "llms.txt").read_text(encoding="utf-8")
    full = (tmp_path / "llms-full.txt").read_text(encoding="utf-8")
    assert "- [SLA](endpoints/SLA.md)" in idx
    assert "# ADM — справочник ручек" in full and "# SLA — справочник ручек" in full
    assert full.index("# ADM") < full.index("# SLA")
```

- [ ] **Step 2: FAIL** — `python3 -m pytest tests/test_llms_txt.py -q`.

- [ ] **Step 3: Реализация** — `update/llms_txt.py`:

```python
"""Генерация llms.txt (индекс, формат llmstxt.org) и llms-full.txt (полная склейка endpoints/)."""
from pathlib import Path

REPO_ROOT = Path(__file__).resolve().parents[2]

# Курируемые глоссы сервисов (из карты overview.md); новый сервис без глосса — строка без описания.
SERVICE_GLOSS = {
    "ADM": "пользователи (CRUD, роли, участки, навыки), тенанты, лицензии, приглашения",
    "AUTH": "регистрация, верификация email/телефона, смена пароля, logout",
    "AUTHN": "логин (пароль, SSO, SMS), получение realm",
    "AUTHZ": "получение/обновление access_token и service_token",
    "CM": "геолокация клиентов",
    "COMMON": "вложения (загрузка файлов), валюты, часовые пояса, страны, локализация",
    "ES": "объекты/оборудование (CRUD, иерархия, атрибуты), компании, участки, навыки, теги, QR-коды",
    "EXPORT": "экспорт в Excel: заявки, пользователи, объекты, компании, материалы",
    "LIC": "сканер лицензий (запуск/остановка/статус)",
    "MSG": "триггеры уведомлений, шаблоны сообщений, почтовые ящики, push",
    "NEWS": "новости и объявления",
    "PA": "трудоустройство, назначение на объекты, рейтинги сотрудников, геотрекинг",
    "PMP": "плановые заявки: расписания, частоты, автосоздание по графику",
    "PROXY": "проксирование запросов к сторонним сервисам",
    "REPORT": "отчёты: объекты, исполнители, компании, стадии, время реакции, Power BI",
    "SC": "договоры обслуживания: привязка объектов, вложения, атрибуты",
    "SLA": "критичности, правила дедлайнов, атрибуты SLA",
    "TSTG": "жизненные циклы заявок: стадии, переходы, ветки, автоназначение",
    "UI": "компоненты интерфейса, фильтры, шаблоны раскладки",
    "WH": "склады, материалы, приход/расход/перемещение, инвентаризация, штрихкоды",
    "WORK": "заявки (создание, поиск, стадии, назначение), чек-листы, работы, акты, виды работ",
    "WSP": "графики работы: правила смен, расписания, продление",
}

_HEADER = """# HubEx API

> Справочник REST API HubEx — облачной мультитенантной FSM-платформы (заявки с жизненным
> циклом, объекты/оборудование, исполнители, SLA, чек-листы, акты, склад). Авторизация
> Bearer-токеном, пагинация Range-заголовком — детали в overview.

## Обзор

- [overview.md](overview.md): авторизация, пагинация, карта сервисов, типовые сценарии → сервисы
- [entity-map.md](entity-map.md): бизнес-сущность → ручки API

## Сервисы
"""


def render_llms_txt(services) -> str:
    lines = [_HEADER.rstrip()]
    for name in sorted(services):
        gloss = SERVICE_GLOSS.get(name, "")
        line = f"- [{name}](endpoints/{name}.md)"
        lines.append(f"{line}: {gloss}" if gloss else line)
    lines += ["", "## Optional", "", "- [notes/](notes/): проверенные практикой правила и грабли по сервисам"]
    return "\n".join(lines) + "\n"


def write_llms_files(*, root: Path | None = None) -> None:
    base = root if root is not None else REPO_ROOT
    eps = sorted((base / "endpoints").glob("*.md"))
    (base / "llms.txt").write_text(render_llms_txt([p.stem for p in eps]), encoding="utf-8")
    parts = [p.read_text(encoding="utf-8").rstrip() for p in eps]
    (base / "llms-full.txt").write_text("\n\n".join(parts) + "\n", encoding="utf-8")
```

- [ ] **Step 4: PASS** — `python3 -m pytest tests/test_llms_txt.py -q`.

- [ ] **Step 5: Commit** — `git add -A && git commit -m "feat(update): генерация llms.txt и llms-full.txt" -m "Co-Authored-By: Claude Fable 5 <noreply@anthropic.com>"`

---

### Task 8: notes_patch — точечная правка заметок моделью

**Files:**
- Create: `update/notes_patch.py`, `update/prompts/notes-patch.md`
- Test: `tests/test_notes_patch.py`

**Interfaces:**
- Consumes: `model_client.run_model(prompt) -> str`, `recompress_guard.find_phantoms(md, swagger) -> list[str]`, changeset из `api_diff.diff_swagger`.
- Produces: `notes_patch.notes_path(service, *, root=None) -> Path`; `notes_patch.patch_notes(service, swagger, changeset, *, model=..., root=None) -> {"service", "status": "absent"|"clean"|"ok"|"error", "phantoms": [...], "stale": [...], "error"}`; `notes_patch.render_summary(results) -> str`.

- [ ] **Step 1: Падающий тест** — `tests/test_notes_patch.py`:

```python
from update import notes_patch

SWAGGER = {"paths": {"/Tasks": {"get": {}}}, "components": {"schemas": {}}}
CS = {"operations_added": [], "operations_removed": ["GET /Old"],
      "operations_changed": [{"op": "GET /Tasks", "parts": ["parameters"]}],
      "schemas_added": [], "schemas_removed": [], "schemas_changed": []}


def _notes(tmp_path, text):
    d = tmp_path / "notes"
    d.mkdir()
    (d / "WORK.md").write_text(text, encoding="utf-8")


def test_absent_notes_skipped(tmp_path):
    r = notes_patch.patch_notes("WORK", SWAGGER, CS, model=lambda p: "x", root=tmp_path)
    assert r["status"] == "absent"


def test_untouched_notes_left_clean(tmp_path):
    _notes(tmp_path, "# WORK\n- ⚠ грабля про `POST /CompletedWorks`\n")
    called = []
    r = notes_patch.patch_notes("WORK", SWAGGER, CS, model=lambda p: called.append(p) or "x", root=tmp_path)
    assert r["status"] == "clean" and not called  # изменённые ручки в заметках не упомянуты


def test_patch_writes_and_guards(tmp_path):
    _notes(tmp_path, "# WORK\n- правило про `GET /Tasks` и про `GET /Old`\n")
    fixed = "# WORK\n- правило про `GET /Tasks` (параметры изменились)\n"
    r = notes_patch.patch_notes("WORK", SWAGGER, CS, model=lambda p: fixed, root=tmp_path)
    assert r["status"] == "ok" and r["phantoms"] == [] and r["stale"] == []
    assert (tmp_path / "notes" / "WORK.md").read_text(encoding="utf-8") == fixed


def test_stale_removed_op_flagged(tmp_path):
    _notes(tmp_path, "# WORK\n- правило про `GET /Old`\n")
    bad = "# WORK\n- правило про `GET /Old` осталось\n"
    r = notes_patch.patch_notes("WORK", SWAGGER, CS, model=lambda p: bad, root=tmp_path)
    assert r["stale"] == ["GET /Old"]


def test_model_error_leaves_file(tmp_path):
    _notes(tmp_path, "# WORK\nупоминание `GET /Tasks`\n")

    def boom(p):
        raise RuntimeError("claude недоступен")

    r = notes_patch.patch_notes("WORK", SWAGGER, CS, model=boom, root=tmp_path)
    assert r["status"] == "error"
    assert "упоминание" in (tmp_path / "notes" / "WORK.md").read_text(encoding="utf-8")
```

- [ ] **Step 2: FAIL** — `python3 -m pytest tests/test_notes_patch.py -q`.

- [ ] **Step 3: Фикс-промпт** — `update/prompts/notes-patch.md`:

```markdown
Ты редактируешь файл заметок notes/{{SERVICE}}.md репозитория HubEx.API. Заметки — накопленный
практикой слой: ⚠-грабли, правила, типовые связки. Сигнатуры ручек живут в endpoints/ и сюда
не входят.

В API сервиса {{SERVICE}} произошли изменения:
{{DIFF}}

В заметках упомянуты затронутые ручки: {{MENTIONED}}

Задача — ТОЧЕЧНАЯ правка:
- Поправь только строки/абзацы, где упомянуты затронутые ручки: удалённую ручку убери или
  пометь как удалённую из API; у изменённой сверь, не устарело ли утверждение.
- ЗАПРЕЩЕНО переписывать, переформулировать или переупорядочивать остальной текст: он должен
  остаться побайтово тем же.
- ЗАПРЕЩЕНО добавлять новые факты, ручки или разделы.
- Если правка по смыслу не нужна — верни файл без изменений.

Верни ТОЛЬКО полный итоговый markdown файла, без пояснений и обрамления.

Текущий файл:
{{NOTES}}
```

- [ ] **Step 4: Реализация** — `update/notes_patch.py`:

```python
"""Точечная правка notes/<SVC>.md моделью по диффу API. Полная регенерация запрещена промптом."""
from pathlib import Path

from update import model_client, recompress_guard

REPO_ROOT = Path(__file__).resolve().parents[2]
_PROMPT_PATH = Path(__file__).resolve().parent / "prompts" / "notes-patch.md"


def notes_path(service: str, *, root: Path | None = None) -> Path:
    base = root if root is not None else REPO_ROOT
    return base / "notes" / f"{service}.md"


def _touched_ops(changeset: dict) -> list:
    ops = set(changeset["operations_removed"]) | {c["op"] for c in changeset["operations_changed"]}
    return sorted(ops)


def build_prompt(service: str, old_notes: str, changeset: dict, mentioned: list) -> str:
    diff_lines = []
    if changeset["operations_added"]:
        diff_lines.append("добавлены: " + ", ".join(changeset["operations_added"]))
    if changeset["operations_removed"]:
        diff_lines.append("удалены: " + ", ".join(changeset["operations_removed"]))
    if changeset["operations_changed"]:
        diff_lines.append("изменены: " + ", ".join(
            f"{c['op']} ({'/'.join(c['parts'])})" for c in changeset["operations_changed"]))
    return (_PROMPT_PATH.read_text(encoding="utf-8")
            .replace("{{SERVICE}}", service)
            .replace("{{DIFF}}", "\n".join(diff_lines) or "(нет)")
            .replace("{{MENTIONED}}", ", ".join(mentioned))
            .replace("{{NOTES}}", old_notes))


def patch_notes(service: str, swagger: dict, changeset: dict, *,
                model=model_client.run_model, root: Path | None = None) -> dict:
    res = {"service": service, "phantoms": [], "stale": [], "error": None}
    path = notes_path(service, root=root)
    if not path.exists():
        return {**res, "status": "absent"}
    old = path.read_text(encoding="utf-8")
    mentioned = [op for op in _touched_ops(changeset) if op in old]
    if not mentioned:
        return {**res, "status": "clean"}
    try:
        new = model(build_prompt(service, old, changeset, mentioned))
    except Exception as e:  # noqa: BLE001 — падение модели одного сервиса не роняет прогон
        return {**res, "status": "error", "error": str(e)}
    path.write_text(new if new.endswith("\n") else new + "\n", encoding="utf-8")
    return {**res, "status": "ok",
            "phantoms": recompress_guard.find_phantoms(new, swagger),
            "stale": [op for op in changeset["operations_removed"] if op in new]}


def render_summary(results: list) -> str:
    out = ["# Правка заметок"]
    for r in results:
        np = r.get("notes_patch")
        if not np or np["status"] in ("absent", "clean"):
            continue
        if np["status"] == "error":
            out.append(f"- {np['service']}: ошибка модели — {np['error']}")
        elif np["phantoms"] or np["stale"]:
            issues = []
            if np["phantoms"]:
                issues.append("фантомные ручки: " + ", ".join(np["phantoms"]))
            if np["stale"]:
                issues.append("остались удалённые: " + ", ".join(np["stale"]))
            out.append(f"- {np['service']}: ⚠ {'; '.join(issues)} — проверь глазами")
        else:
            out.append(f"- {np['service']}: поправлено, guard чист")
    if len(out) == 1:
        out.append("(заметки не требовали правок)")
    return "\n".join(out) + "\n"
```

- [ ] **Step 5: PASS** — `python3 -m pytest tests/test_notes_patch.py -q`.

- [ ] **Step 6: Commit** — `git add -A && git commit -m "feat(update): notes_patch — точечная правка заметок моделью + guard (фантомы, устаревшие)" -m "Co-Authored-By: Claude Fable 5 <noreply@anthropic.com>"`

---

### Task 9: pipeline + report под новую раскладку

**Files:**
- Create: `update/pipeline.py` (переработка), `update/report.py` (копия с правками)
- Test: `tests/test_pipeline.py`, `tests/test_report.py`

**Interfaces:**
- Produces: `pipeline.run_update_api(services=None, *, fetch=..., manifest=..., root=None, recompress=False, patch_impl=None) -> list[changeset]` — пишет `snapshots/`, `endpoints/`, `llms.txt`/`llms-full.txt`; при `recompress` для `changed` вызывает `patch_impl` и кладёт результат в `cs["notes_patch"]`. `pipeline.endpoints_path(service, *, root=None)`. `report.render(results) -> str`.

- [ ] **Step 1: Падающий тест** — `tests/test_pipeline.py`:

```python
from update import pipeline, snapshot_store


def _swagger(paths):
    return {"openapi": "3.0.1", "paths": paths, "components": {"schemas": {}}}


def test_new_service_seeds_snapshot_endpoints_llms(tmp_path):
    manifest = lambda **k: [("WH", "http://x/WH.json")]
    fetch = lambda url, **k: _swagger({"/A": {"get": {"summary": "Список A"}}})
    results = pipeline.run_update_api(fetch=fetch, manifest=manifest, root=tmp_path)
    assert results[0]["status"] == "new"
    assert snapshot_store.read_snapshot("WH", root=tmp_path) is not None
    ep = (tmp_path / "endpoints" / "WH.md").read_text(encoding="utf-8")
    assert "`GET /A` — Список A" in ep
    assert (tmp_path / "llms.txt").exists() and (tmp_path / "llms-full.txt").exists()


def test_unchanged_run_writes_nothing(tmp_path):
    manifest = lambda **k: [("WH", "http://x/WH.json")]
    fetch = lambda url, **k: _swagger({"/A": {"get": {}}})
    pipeline.run_update_api(fetch=fetch, manifest=manifest, root=tmp_path)
    stamp = (tmp_path / "endpoints" / "WH.md").stat().st_mtime_ns
    results = pipeline.run_update_api(fetch=fetch, manifest=manifest, root=tmp_path)
    assert results[0]["status"] == "unchanged"
    assert (tmp_path / "endpoints" / "WH.md").stat().st_mtime_ns == stamp  # идемпотентность


def test_recompress_patches_only_changed(tmp_path):
    manifest = lambda **k: [("WH", "http://x/WH.json")]
    fetch1 = lambda url, **k: _swagger({"/A": {"get": {}}})
    fetch2 = lambda url, **k: _swagger({"/A": {"get": {}}, "/B": {"get": {}}})
    calls = []

    def fake_patch(service, swagger, cs, *, root=None):
        calls.append(service)
        return {"service": service, "status": "clean", "phantoms": [], "stale": [], "error": None}

    pipeline.run_update_api(fetch=fetch1, manifest=manifest, root=tmp_path,
                            recompress=True, patch_impl=fake_patch)
    assert calls == []  # new — заметки не трогаем
    results = pipeline.run_update_api(fetch=fetch2, manifest=manifest, root=tmp_path,
                                      recompress=True, patch_impl=fake_patch)
    assert calls == ["WH"] and results[0]["notes_patch"]["status"] == "clean"


def test_fetch_error_continues(tmp_path):
    manifest = lambda **k: [("WH", "http://x/WH.json"), ("PA", "http://x/PA.json")]

    def fetch(url, **k):
        if "PA" in url:
            raise RuntimeError("timeout")
        return _swagger({"/A": {"get": {}}})

    results = pipeline.run_update_api(fetch=fetch, manifest=manifest, root=tmp_path)
    by = {r["service"]: r for r in results}
    assert by["PA"]["status"] == "error" and by["WH"]["status"] == "new"
```

- [ ] **Step 2: FAIL** — `python3 -m pytest tests/test_pipeline.py -q`.

- [ ] **Step 3: Реализация** — `update/pipeline.py`:

```python
"""Оркестратор update: манифест → забор → дифф → снапшот + endpoints + llms → отчёт.

Всё пишется unstaged в корень суперпроекта; коммитит человек. --recompress — точечная
правка notes/ моделью только для changed-сервисов (new заметок не имеют по построению).
"""
from pathlib import Path

from update import api_diff, api_fetch, api_manifest, endpoints_gen, llms_txt, notes_patch, snapshot_store

REPO_ROOT = Path(__file__).resolve().parents[2]


def endpoints_path(service: str, *, root: Path | None = None) -> Path:
    base = root if root is not None else REPO_ROOT
    return base / "endpoints" / f"{service}.md"


def run_update_api(services=None, *, fetch=api_fetch.fetch_swagger,
                   manifest=api_manifest.fetch_manifest, root: Path | None = None,
                   recompress=False, patch_impl=None) -> list:
    base = root if root is not None else REPO_ROOT
    impl = patch_impl or notes_patch.patch_notes
    entries = manifest()
    if services:
        wanted = set(services)
        entries = [(n, u) for (n, u) in entries if n in wanted]

    results, touched = [], False
    for name, url in entries:
        try:
            new = fetch(url)
            if not isinstance(new, dict):
                raise ValueError("свагер не является OpenAPI-объектом (ожидался JSON-объект)")
        except Exception as e:  # noqa: BLE001 — сеть/JSON одного сервиса не валят прогон
            results.append({"service": name, "status": "error", "error": str(e)})
            continue
        old = snapshot_store.read_snapshot(name, root=base)
        cs = api_diff.diff_swagger(old, new)
        status = "new" if old is None else ("unchanged" if api_diff.is_empty(cs) else "changed")
        cs.update(service=name, status=status, error=None)
        results.append(cs)
        if status in ("new", "changed"):
            touched = True
            snapshot_store.write_snapshot(name, api_fetch.normalize(new), root=base)
            ep = endpoints_path(name, root=base)
            ep.parent.mkdir(parents=True, exist_ok=True)
            ep.write_text(endpoints_gen.render_endpoints(name, new), encoding="utf-8")
            if recompress and status == "changed":
                cs["notes_patch"] = impl(name, new, cs, root=base)
    if touched:
        llms_txt.write_llms_files(root=base)
    return results
```

- [ ] **Step 4: report.py** — скопировать из монорепы и поправить две подсказки:

```bash
cp /home/cvetkov_es/development/HubEx.AI-2.0/tools/update/report.py update/
cp /home/cvetkov_es/development/HubEx.AI-2.0/tools/tests/test_update_report.py tests/test_report.py
```
В `update/report.py` заменить строку
`lines.append(f"→ проверь дистиллят \`knowledge/api/services/{cs['service']}.md\`")`
на
`lines.append(f"→ endpoints/{cs['service']}.md перегенерирован; загляни в notes/{cs['service']}.md (если есть)")`
и строку с `knowledge/api/entity-map.md` / `knowledge/api/overview.md` на
`"→ затронута ручка из «наиболее используемых»: проверь также \`entity-map.md\` и \`overview.md\`"`.
В `tests/test_report.py` поправить соответствующие ассерты на новые тексты.

- [ ] **Step 5: PASS** — `python3 -m pytest tests/test_pipeline.py tests/test_report.py -q`, затем весь набор `-m "not live"`.

- [ ] **Step 6: Commit** — `git add -A && git commit -m "feat(update): пайплайн под раскладку контент-репо — снапшот + endpoints + llms, notes_patch на changed" -m "Co-Authored-By: Claude Fable 5 <noreply@anthropic.com>"`

---

### Task 10: api_cli.py + check_links + README пайплайна

**Files:**
- Create: `api_cli.py`, `lint/check_links.py`, `README.md`
- Test: `tests/test_cli.py`

**Interfaces:**
- Produces: `python3 tools/api_cli.py update [--service SVC ...] [--report-file PATH] [--recompress]`; exit 0 — чисто, 1 — ошибки забора/грязный guard, 2 — ManifestError.

- [ ] **Step 1: Падающий тест** — `tests/test_cli.py`:

```python
import api_cli


def _ok_results():
    return [{"service": "WH", "status": "unchanged", "error": None,
             "operations_added": [], "operations_removed": [], "operations_changed": [],
             "schemas_added": [], "schemas_removed": [], "schemas_changed": []}]


def test_update_ok(monkeypatch, capsys):
    monkeypatch.setattr("update.pipeline.run_update_api", lambda **kw: _ok_results())
    assert api_cli.main(["update"]) == 0
    assert "Отчёт update api" in capsys.readouterr().out


def test_update_fetch_error_exit_1(monkeypatch):
    monkeypatch.setattr("update.pipeline.run_update_api",
                        lambda **kw: [{"service": "WH", "status": "error", "error": "boom"}])
    assert api_cli.main(["update"]) == 1


def test_dirty_notes_guard_exit_1(monkeypatch):
    res = _ok_results()
    res[0]["status"] = "changed"
    res[0]["notes_patch"] = {"service": "WH", "status": "ok",
                             "phantoms": ["GET /Ghost"], "stale": [], "error": None}
    monkeypatch.setattr("update.pipeline.run_update_api", lambda **kw: res)
    assert api_cli.main(["update", "--recompress"]) == 1


def test_report_file_written(monkeypatch, tmp_path):
    monkeypatch.setattr("update.pipeline.run_update_api", lambda **kw: _ok_results())
    out = tmp_path / "r.md"
    assert api_cli.main(["update", "--report-file", str(out)]) == 0
    assert "Отчёт update api" in out.read_text(encoding="utf-8")
```

- [ ] **Step 2: FAIL** — `python3 -m pytest tests/test_cli.py -q`.

- [ ] **Step 3: Реализация** — `api_cli.py`:

```python
"""CLI пайплайна обновления HubEx.API. Запуск из корня контент-репозитория:

  python3 tools/api_cli.py update [--service WORK ...] [--report-file PATH] [--recompress]

Без флагов — detect-and-report + перезапись snapshots/, endpoints/, llms* (unstaged).
--recompress — дополнительно точечная правка notes/ моделью (claude -p) для changed-сервисов.
"""
import argparse
import sys
from pathlib import Path

from update import api_manifest, notes_patch, pipeline, report


def build_parser() -> argparse.ArgumentParser:
    p = argparse.ArgumentParser(prog="api-pipeline", description="Обновление HubEx.API из swagger.")
    sub = p.add_subparsers(dest="command", required=True)
    up = sub.add_parser("update", help="дифф swagger со снапшотами → снапшоты + endpoints + llms + отчёт")
    up.add_argument("--service", action="append", default=None,
                    help="ограничить одним сервисом (можно повторять)")
    up.add_argument("--report-file", type=Path, default=None, help="продублировать отчёт в файл")
    up.add_argument("--recompress", action="store_true",
                    help="точечная правка notes/ моделью (claude -p) для изменившихся сервисов")
    return p


def main(argv=None) -> int:
    for stream in (sys.stdout, sys.stderr):
        if hasattr(stream, "reconfigure"):
            stream.reconfigure(encoding="utf-8", errors="backslashreplace")
    args = build_parser().parse_args(argv)
    try:
        results = pipeline.run_update_api(services=args.service, recompress=args.recompress)
    except api_manifest.ManifestError as e:
        print(f"ОТКАЗ: {e}", file=sys.stderr)
        return 2
    text = report.render(results)
    print(text, end="")
    if args.recompress:
        print(notes_patch.render_summary(results), end="")
    if args.report_file:
        args.report_file.write_text(text, encoding="utf-8")
    has_err = any(r["status"] == "error" for r in results)
    dirty = any((r.get("notes_patch") or {}).get("status") == "error"
                or (r.get("notes_patch") or {}).get("phantoms")
                or (r.get("notes_patch") or {}).get("stale") for r in results)
    return 1 if (has_err or dirty) else 0


if __name__ == "__main__":
    sys.exit(main())
```

- [ ] **Step 4: check_links** — скопировать и упростить исключения:

```bash
cp /home/cvetkov_es/development/HubEx.AI-2.0/tools/lint/check_links.py lint/
```
В `lint/check_links.py` удалить блок исключения wiki-копий (3 строки: комментарий про «копии wiki-страниц» и `if "wiki" in md.parts and "product" in md.parts: continue`). Остальное без изменений (`ROOT = parents[2]` уже корректен).

- [ ] **Step 5: README.md пайплайна** — создать:

```markdown
# tools — пайплайн обновления HubEx.API

> Подключается git-сабмодулем в `tools/` контент-репозитория `HubEx.API`. Команды даны из корня контент-репозитория.

Забирает swagger 22 сервисов с `doc.hubex.ru`/`api.hubex.ru`, диффит со `snapshots/`, перегенерирует `endpoints/` (полный справочник ручек), `llms.txt` и `llms-full.txt`; `--recompress` — точечная правка `notes/` моделью (`claude -p`) с guard'ом (фантомные ручки, оставшиеся удалённые). Всё unstaged — ревью и коммит за человеком.

## Установка

python3 -m pip install -r tools/requirements.txt

## Команды

python3 tools/api_cli.py update [--service WORK ...] [--report-file PATH] [--recompress]
python3 tools/lint/check_links.py

## Тесты

cd tools && python3 -m pytest -m "not live" -q   # офлайн
cd tools && python3 -m pytest -q                  # + живой смоук (сеть)
```

- [ ] **Step 6: PASS** — `python3 -m pytest -m "not live" -q` (весь набор).

- [ ] **Step 7: Commit** — `git add -A && git commit -m "feat: api_cli (update) + линтер ссылок + README пайплайна" -m "Co-Authored-By: Claude Fable 5 <noreply@anthropic.com>"`

---

### Task 11: [HUMAN-GATED] Пилот формата endpoints на SLA и WORK

**Files:** нет (артефакты в /tmp; правки формата — в `update/endpoints_gen.py` по итогам ревью).

**Interfaces:**
- Consumes: `endpoints_gen.render_endpoints`, `missing_operations`; снапшоты монорепы (офлайн, сеть не нужна).
- Produces: одобренный мейнтейнером формат `endpoints/`; правки генератора закоммичены.

- [ ] **Step 1: Сгенерировать пилотные файлы из снапшотов монорепы**

```bash
cd /home/cvetkov_es/development/HubEx.API.Pipeline
mkdir -p /tmp/api-pilot
python3 - <<'EOF'
import json, sys
from pathlib import Path
sys.path.insert(0, ".")
from update import endpoints_gen

SNAP = Path("/home/cvetkov_es/development/HubEx.AI-2.0/tools/update/snapshots/api")
for svc in ("SLA", "WORK"):
    sw = json.loads((SNAP / f"{svc}.json").read_text(encoding="utf-8"))
    md = endpoints_gen.render_endpoints(svc, sw)
    Path(f"/tmp/api-pilot/{svc}.md").write_text(md, encoding="utf-8")
    missing = endpoints_gen.missing_operations(md, sw)
    print(f"{svc}: {len(md)//1024}K, ручек в swagger: {len(endpoints_gen._operations(sw))}, пропущено: {missing}")
EOF
```
Expected: `пропущено: []` для обоих; SLA ≲ 10К, WORK ≲ 100К.

- [ ] **Step 2: [HUMAN-GATED] Показать мейнтейнеру `/tmp/api-pilot/SLA.md` (целиком) и фрагменты `/tmp/api-pilot/WORK.md`**

Вопросы ревью: читаемость строк ручек, полнота параметров, качество коротких имён схем и enum, что вычищено зря / что осталось лишнего, размер. НЕ продолжать без ответа.

- [ ] **Step 3: Внести правки формата по итогам ревью**

Правки — в `update/endpoints_gen.py` с обновлением тестов (тот же TDD-цикл: тест на новое поведение → FAIL → правка → PASS). Повторить Step 1–2 до одобрения.

- [ ] **Step 4: Commit** — `git add -A && git commit -m "feat(endpoints): формат утверждён пилотом на SLA и WORK" -m "Co-Authored-By: Claude Fable 5 <noreply@anthropic.com>"`

---

### Task 12: Каркас HubEx.API.CLI (живой доступ без db)

**Files:**
- Create: `/home/cvetkov_es/development/HubEx.API.CLI/` — `hubex_cli.py`, `hubex_core/` (без `db.py`), `tenant_*.yaml`, `SAFETY.md`, `README.md`, `conftest.py`, `pytest.ini`, `requirements.txt`, `.gitignore`, `tests/`

**Interfaces:**
- Produces: `python3 cli/hubex_cli.py api tenants sync|list`, `api get|write` (write: dry-run → `--confirm`); групп `db` и `update` нет.

- [ ] **Step 1: Скопировать и инициализировать**

```bash
MONO=/home/cvetkov_es/development/HubEx.AI-2.0/tools
C=/home/cvetkov_es/development/HubEx.API.CLI
mkdir -p $C/hubex_core $C/tests
cd $C && git init -b main
git config user.name "cvetkov-es" && git config user.email "95337410+cvetkov-es@users.noreply.github.com"
cp $MONO/hubex_cli.py $C/
cp $MONO/hubex_core/__init__.py $MONO/hubex_core/api.py $MONO/hubex_core/auth.py \
   $MONO/hubex_core/config.py $MONO/hubex_core/safety.py $MONO/hubex_core/tenants.py $C/hubex_core/
cp $MONO/tenant_base_url_overrides.yaml $MONO/tenant_notes.yaml $C/
cp $MONO/conftest.py $C/
cp $MONO/tests/test_api.py $MONO/tests/test_auth.py $MONO/tests/test_config.py \
   $MONO/tests/test_safety.py $MONO/tests/test_tenants.py $MONO/tests/test_cli.py $C/tests/
cp /home/cvetkov_es/development/HubEx.AI-2.0/knowledge/rules/safety.md $C/SAFETY.md
```

- [ ] **Step 2: Вырезать db и update из `hubex_cli.py`**

Точечные правки (номера строк — по монорепной версии):
1. Docstring (строки 4–11): убрать строку про `db query` и упоминание SQL.
2. Строка 18: `from hubex_core import api, db, tenants` → `from hubex_core import api, tenants`.
3. Удалить строку 20 (`from hubex_core.db import ...`) и строку 23 (`from update import ...`).
4. Удалить строки 25–26 (`HERE`, `DEFAULT_DBCONFIG`) и аргумент `--db-config` (строка 46).
5. Удалить функцию `_print_table` (строки 36–41) — использовалась только db.
6. Удалить блок парсера `db` (строки 78–84) и блок парсера `update` (строки 86–96).
7. Удалить обработчики: `if args.group == "db" ...` (строки 153–161) и `if args.group == "update" ...` (строки 163–182).
8. Строки 183–184: кортеж исключений → `except (TenantNotFound, AdminCredsMissing) as e:`.

Проверка: `grep -n "db\|update\|pipeline\|recompress" hubex_cli.py` — совпадений нет (кроме, возможно, слов в русских help-строках; их тоже вычистить).

- [ ] **Step 3: Вычистить тесты от db/update**

```bash
cd /home/cvetkov_es/development/HubEx.API.CLI
grep -ln "db\|update" tests/*.py
```
В `tests/test_cli.py` удалить тесты групп `db` и `update` (по именам: всё, что вызывает `["db", ...]` или `["update", ...]` либо мокает `pipeline`/`recompress`); в `tests/test_config.py` удалить тесты dbconfig, если есть. `tests/test_db_*.py` не копировались.

- [ ] **Step 4: Конфиги**

`pytest.ini` — как в Task 1 (тот же текст). `.gitignore`:
```gitignore
__pycache__/
*.pyc
.pytest_cache/
.env
dbconfig.yaml
tenants.json
```
`requirements.txt`:
```
pyyaml>=6.0
requests>=2.28
pytest>=7.0
```

- [ ] **Step 5: README.md** — создать:

```markdown
# cli — живой доступ к HubEx API

> Подключается git-сабмодулем в `cli/` контент-репозитория `HubEx.API`. Команды даны из корня контент-репозитория. Нужны креды кросс-тенант админа (`.env`, см. ниже) — потребителям справочника не требуется.

**Железное правило: запись в любой тенант — только dry-run → явное подтверждение человека (`--confirm`).** Полная модель безопасности — [SAFETY.md](SAFETY.md).

## Команды

python3 cli/hubex_cli.py api tenants sync            # логин кросс-тенант админом, кеш тенантов
python3 cli/hubex_cli.py api tenants list [--filter acme]
python3 cli/hubex_cli.py api get   --tenant 310 /WORK/Tasks [--method HEAD] [--json]
python3 cli/hubex_cli.py api write --tenant 310 --method POST /WORK/Tasks --body '{...}' [--confirm]

## Установка

python3 -m pip install -r cli/requirements.txt
Креды: файл `.env` рядом с `hubex_cli.py` (`HUBEX_ADMIN_LOGIN`, `HUBEX_ADMIN_PASSWORD`) — в `.gitignore`.

## Тесты

cd cli && python3 -m pytest -m "not live" -q
```
Примечание исполнителю: сверить имена переменных `.env` с `hubex_core/config.py` при копировании (если там другие имена — поправить README, не код).

- [ ] **Step 6: Тесты зелёные**

```bash
cd /home/cvetkov_es/development/HubEx.API.CLI && python3 -m pytest -m "not live" -q
```
Expected: PASS. Падения импортов = недовычищенные ссылки на db/update — вернуться к Step 2–3.

- [ ] **Step 7: Commit**

```bash
git add -A
git commit -m "feat: живой CLI HubEx API — перенос из монорепы без db-части" \
  -m "api get/write (dry-run→--confirm), tenants sync/list, hubex_core без db.py; SAFETY.md — модель безопасности записи." \
  -m "Co-Authored-By: Claude Fable 5 <noreply@anthropic.com>"
```

---

### Task 13: Контент-репо — роутер (README, CLAUDE, AGENTS, .gitignore)

**Files:**
- Create: `/home/cvetkov_es/development/HubEx.API/README.md`, `CLAUDE.md`, `AGENTS.md`, `.gitignore`
- Delete: `/home/cvetkov_es/development/HubEx.API/docs/` (переехали в пайплайн в Task 1)

- [ ] **Step 1: README.md** — создать (полный текст):

```markdown
# HubEx.API — справочник API HubEx для ИИ-агентов

> **Что здесь:** автономный справочник REST API HubEx: полный каталог ручек 22 сервисов (`endpoints/`), заметки практики (`notes/`), точные схемы (`snapshots/`) и пайплайн обновления.
> **Когда сюда идти:** нужна ручка HubEx API, её параметры или правила работы с API — начни с [overview.md](overview.md).

**HubEx** — облачная мультитенантная FSM-платформа (Field Service Management) для выездного обслуживания: заявки с жизненным циклом, объекты/оборудование, исполнители, SLA, чек-листы, акты, склад, аналитика.

## Слои

| Куда | Что там | Когда идти |
|---|---|---|
| [overview.md](overview.md) | авторизация, пагинация, карта 22 сервисов, сценарии → сервисы, топ-ручки | старт любой задачи с API |
| [entity-map.md](entity-map.md) | бизнес-сущность → ручки | задача сформулирована в терминах сущностей |
| [endpoints/](endpoints/) | **полный** справочник ручек по сервисам (генерируется из swagger) | найти ручку, её параметры и схемы |
| [notes/](notes/) | проверенные практикой правила и ⚠-грабли | перед использованием сервиса |
| [snapshots/](snapshots/) | канонические swagger JSON | нужна точная схема — grep, целиком не читать (до 1.2 МБ) |
| [llms.txt](llms.txt) / [llms-full.txt](llms-full.txt) | индекс и склейка по llmstxt.org | отдать справочник внешнему инструменту |

## Правила

- `endpoints/**`, `snapshots/**`, `llms*.txt` руками не правятся — их перезаписывает пайплайн.
- **Нашёл особенность/правило, которого нет в swagger, — запиши в `notes/<SVC>.md`** (⚠-строка: ссылка на ручку, тире, факт). Кросс-сервисное — в `overview.md`. Запрещено записывать факты, противоречащие `snapshots/`.
- Не выдумывай ручки: нет в `endpoints/` — нет в API; проверь `snapshots/` или скажи, что не нашёл.
- Рецепт поиска: не знаешь сервис — grep по `endpoints/` (summary русские); `overview.md` — выбор сервиса по сценарию.
- Живая запись в тенант — только через `cli/` с dry-run → подтверждение человека (правила — в сабмодуле `cli/`).

## Обновление и живой доступ

`tools/` и `cli/` — git-сабмодули (репозитории `HubEx.API.Pipeline` и `HubEx.API.CLI` рядом, у того же владельца). Обычный `git clone` их не тянет — потребителю справочника они не нужны. Выкачать: `git submodule update --init tools` (или `cli`, или клон с `--recursive`).

python3 tools/api_cli.py update [--service WORK ...] [--recompress]   # обновление (детали: tools/README.md)
python3 cli/hubex_cli.py api get --tenant N /WORK/Tasks               # живой доступ (детали: cli/README.md)

## Комбинирование с другими доменами

Репозиторий автономен (лист): ссылок наружу нет, подключается сабмодулем в комбо-репозитории (API+вики и т.д.). Соседний домен: `HubEx.Wiki`.

Мейнтейнер и единственный коммитер — Евгений Цветков.
```

- [ ] **Step 2: CLAUDE.md**:

```markdown
# Вход для Claude Code

Это автономный справочник API HubEx для ИИ-агентов. **Перед задачей прочитай [README.md](README.md).**

Критичное, дублируется намеренно:
- Ручка API → [overview.md](overview.md) (какой сервис) → `endpoints/<SVC>.md` (сигнатура) → `notes/<SVC>.md` (грабли).
- `endpoints/**`, `snapshots/**`, `llms*.txt` руками не правь — их ведёт пайплайн (`python3 tools/api_cli.py update`).
- Нашёл особенность, которой нет в swagger, — запиши в `notes/<SVC>.md`; противоречить `snapshots/` нельзя.
- Не выдумывай ручки: нет в `endpoints/` — нет в API.
- `snapshots/*.json` целиком не читай (до 1.2 МБ) — только grep/точечная вырезка.
- `tools/`, `cli/` — git-сабмодули; для обновления/живого доступа: `git submodule update --init <путь>`.
- Живая запись в тенант — только dry-run → явное подтверждение человека (`cli/hubex_cli.py api write ... --confirm`).
```

- [ ] **Step 3: AGENTS.md** — тот же текст, что CLAUDE.md, с заголовком `# Вход для агентов`.

- [ ] **Step 4: .gitignore и удаление docs/**

`.gitignore`:
```gitignore
__pycache__/
*.pyc
.pytest_cache/
.superpowers/
```
```bash
cd /home/cvetkov_es/development/HubEx.API
git rm -r docs/
```

- [ ] **Step 5: Commit**

```bash
git add -A
git commit -m "feat: роутер контент-репозитория (README/CLAUDE/AGENTS), docs/ переехали в пайплайн" \
  -m "Co-Authored-By: Claude Fable 5 <noreply@anthropic.com>"
```

---

### Task 14: Контент-репо — перенос overview.md и entity-map.md

**Files:**
- Create: `/home/cvetkov_es/development/HubEx.API/overview.md`, `entity-map.md` (из `HubEx.AI-2.0/knowledge/api/`)

- [ ] **Step 1: Скопировать и поправить пути**

```bash
cd /home/cvetkov_es/development/HubEx.API
cp /home/cvetkov_es/development/HubEx.AI-2.0/knowledge/api/overview.md .
cp /home/cvetkov_es/development/HubEx.AI-2.0/knowledge/api/entity-map.md .
sed -i 's|(services/\([A-Z]*\)\.md)|(endpoints/\1.md)|g' overview.md entity-map.md
```

- [ ] **Step 2: overview.md — ручные правки**

1. Строка 7: `... — [knowledge/product/overview.md](../product/overview.md).` → убрать ссылку: `... — продукт описан в вики HubEx (домен HubEx.Wiki).`
2. В разделе «Кросс-тенант админ»: `tools/hubex_core/api.py` → `cli/hubex_core/api.py`; упоминание CLI-флага `--member-id` (`api get/write`) оставить, уточнив `cli/hubex_cli.py`.
3. Строка 34 (правило isDeleted): `[services/WORK.md](endpoints/WORK.md) (раздел ...)` — заменить хвост на `— [endpoints/WORK.md](endpoints/WORK.md) и [notes/WORK.md](notes/WORK.md)`.
4. Проверить: `grep -n 'knowledge/\|services/\|tools/' overview.md` → допустимо только `tools/api_cli.py` в контексте обновления (если есть); остальное вычистить.

- [ ] **Step 3: entity-map.md — убрать домен БД**

```bash
sed -i '/^- \*\*БД:\*\*/d' entity-map.md
```
Ручные правки: в заголовке и цитате убрать упоминание таблиц БД: `# entity-map.md — связка бизнес-сущностей с ручками API`; в строке «Источник» убрать `knowledge/db/areas/*.md`; строку «> **Что здесь:**» переписать: `связка бизнес-сущностей с ручками API (таблицы БД — домен HubEx.DB, здесь их нет)`.
Проверка: `grep -n 'db/\|БД:' entity-map.md` → пусто.

- [ ] **Step 4: Commit**

```bash
git add overview.md entity-map.md
git commit -m "feat: перенос overview и entity-map из монорепы — пути на endpoints/, без домена БД" \
  -m "Co-Authored-By: Claude Fable 5 <noreply@anthropic.com>"
```

---

### Task 15: Контент-репо — засев notes/

**Files:**
- Create: `/home/cvetkov_es/development/HubEx.API/notes/WORK.md`

По ревизии монорепы ⚠-грабли есть только в `knowledge/api/services/WORK.md` (4 шт.); остальной редакторский слой уже в overview/entity-map. Стартуем с одного файла — остальные `notes/` появятся по мере практики (README задаёт правило записи).

- [ ] **Step 1: Извлечь грабли из монорепного дистиллята**

```bash
grep -n '⚠' /home/cvetkov_es/development/HubEx.AI-2.0/knowledge/api/services/WORK.md
```
Expected: 4 строки (посмотреть содержимое и контекст вокруг каждой).

- [ ] **Step 2: Создать `notes/WORK.md`**

Каркас (в раздел «Грабли» вставить 4 ⚠-строки из Step 1 дословно, поправив ссылки вида `services/X.md` → `endpoints/X.md`, и выбросив чисто-сигнатурные куски):

```markdown
# WORK — заметки практики

> **Что здесь:** проверенные практикой правила и грабли сервиса WORK (заявки). Сигнатуры ручек — [endpoints/WORK.md](../endpoints/WORK.md).
> **Когда сюда идти:** перед работой с заявками через API.

## Грабли

<4 ⚠-строки из монорепного WORK.md>

## Наиболее используемые

`GET /Tasks`, `POST /Tasks`, `GET /Tasks/{taskID}`, `PATCH /Tasks/{taskID}`, `POST /TaskStagingHistory`, `GET /Tasks/{taskID}/stages/next`, `POST /CompletedWorks` — расшифровка в [overview.md](../overview.md).
```

- [ ] **Step 3: Sanity-проверка ссылок вручную** (линтер прогоняется в Task 18, когда появится `endpoints/`): пути `../endpoints/WORK.md`, `../overview.md` корректны относительно `notes/`.

- [ ] **Step 4: Commit**

```bash
cd /home/cvetkov_es/development/HubEx.API
git add notes/
git commit -m "feat: засев notes/WORK.md — грабли из монорепного дистиллята" \
  -m "Co-Authored-By: Claude Fable 5 <noreply@anthropic.com>"
```

---

### Task 16: [HUMAN-GATED] GitHub-репозитории и пуш

**Files:** нет (внешняя ops-операция).

**Interfaces:**
- Produces: `github.com/cvetkov-es/{HubEx.API, HubEx.API.Pipeline, HubEx.API.CLI}` с запушенными `main`.

- [ ] **Step 1: [HUMAN-GATED] Подтвердить видимость (private/public) у пользователя.** По умолчанию `--private`. Не продолжать без ответа.

- [ ] **Step 2: Создать и запушить (подставить видимость)**

```bash
cd /home/cvetkov_es/development/HubEx.API.Pipeline
gh repo create cvetkov-es/HubEx.API.Pipeline --private --source=. --remote=origin --push
cd /home/cvetkov_es/development/HubEx.API.CLI
gh repo create cvetkov-es/HubEx.API.CLI --private --source=. --remote=origin --push
cd /home/cvetkov_es/development/HubEx.API
gh repo create cvetkov-es/HubEx.API --private --source=. --remote=origin --push
```
Expected: три URL; `git ls-remote origin main` в каждом печатает sha.

---

### Task 17: Сабмодули tools/ и cli/ в контент-репо

**Files:**
- Create: `/home/cvetkov_es/development/HubEx.API/.gitmodules`, `tools/` и `cli/` (сабмодули)

**Interfaces:**
- Consumes: запушенные репо из Task 16 (относительный URL резолвится от origin).
- Produces: пины сабмодулей; `python3 tools/api_cli.py ...` работает из корня контента.

- [ ] **Step 1: Добавить сабмодули с относительными URL**

```bash
cd /home/cvetkov_es/development/HubEx.API
git submodule add ../HubEx.API.Pipeline.git tools
git submodule add ../HubEx.API.CLI.git cli
cat .gitmodules
```
Expected в `.gitmodules` — оба URL относительные:
```
[submodule "tools"]
	path = tools
	url = ../HubEx.API.Pipeline.git
[submodule "cli"]
	path = cli
	url = ../HubEx.API.CLI.git
```
Если URL абсолютный — поправить файл + `git submodule sync`.

- [ ] **Step 2: Проверить резолюцию корня из сабмодуля**

```bash
python3 -c "
import sys; sys.path.insert(0, 'tools')
from update import pipeline
print(pipeline.REPO_ROOT)"
```
Expected: `/home/cvetkov_es/development/HubEx.API`.

- [ ] **Step 3: Commit**

```bash
git add .gitmodules tools cli
git commit -m "feat: сабмодули tools/ (HubEx.API.Pipeline) и cli/ (HubEx.API.CLI)" \
  -m "Относительные host-agnostic URL; обычный clone их не тянет." \
  -m "Co-Authored-By: Claude Fable 5 <noreply@anthropic.com>"
```

---

### Task 18: Полный засев и приёмка

**Files:**
- Create (пайплайном): `snapshots/*.json` ×22, `endpoints/*.md` ×22, `llms.txt`, `llms-full.txt`

- [ ] **Step 1: Засев (нужна сеть)**

```bash
cd /home/cvetkov_es/development/HubEx.API
python3 tools/api_cli.py update --report-file /tmp/api-seed-report.md
ls snapshots | wc -l; ls endpoints | wc -l
```
Expected: exit 0, отчёт «22 new»; по 22 файла в `snapshots/` и `endpoints/`; `llms.txt`, `llms-full.txt` в корне. Отчёт заодно показывает дифф свежего swagger против снапшотов монорепы от 2026-07-10 — прочитать глазами.

- [ ] **Step 2: Полнота и идемпотентность**

```bash
python3 - <<'EOF'
import json, sys
sys.path.insert(0, "tools")
from pathlib import Path
from update import endpoints_gen
bad = False
for sj in sorted(Path("snapshots").glob("*.json")):
    sw = json.loads(sj.read_text(encoding="utf-8"))
    md = Path(f"endpoints/{sj.stem}.md").read_text(encoding="utf-8")
    miss = endpoints_gen.missing_operations(md, sw)
    if miss:
        bad = True
        print(f"{sj.stem}: ПРОПУЩЕНО {miss}")
print("полнота: OK" if not bad else "полнота: FAIL")
EOF
python3 tools/api_cli.py update > /tmp/second-run.md
git status --porcelain | grep -v '^??' | wc -l
grep -c 'изменилось 0' /tmp/second-run.md
```
Expected: `полнота: OK`; повторный прогон — «изменилось 0», рабочее дерево без новых модификаций.

- [ ] **Step 3: Линтер ссылок и llms**

```bash
python3 tools/lint/check_links.py
grep -c 'endpoints/' llms.txt
```
Expected: `битых ссылок: 0`; в `llms.txt` — 22 ссылки на `endpoints/`.

- [ ] **Step 4: Голый клон чист**

```bash
rm -rf /tmp/api-plain-check
git clone /home/cvetkov_es/development/HubEx.API /tmp/api-plain-check
( test -z "$(ls -A /tmp/api-plain-check/tools 2>/dev/null)" ) && echo "tools/ пуст — OK"
( test -z "$(ls -A /tmp/api-plain-check/cli 2>/dev/null)" ) && echo "cli/ пуст — OK"
ls /tmp/api-plain-check/endpoints >/dev/null && echo "endpoints/ на месте — OK"
rm -rf /tmp/api-plain-check
```
Expected: три «OK».

- [ ] **Step 4a: [HUMAN-GATED, опционально] Живой смоук CLI**

Если у мейнтейнера настроены креды (`.env` в `cli/`): `python3 cli/hubex_cli.py api tenants list | head -3` и `api get --tenant <тестовый> /WORK/Tasks --method HEAD` → статус 206/200. Без кред — пропустить, отметить в отчёте выполнения.

- [ ] **Step 5: Commit засева + [HUMAN-GATED] пуш**

```bash
git add snapshots endpoints llms.txt llms-full.txt
git commit -m "feat: засев — 22 снапшота swagger + endpoints + llms.txt" \
  -m "Первый прогон пайплайна; формат endpoints утверждён пилотом (SLA, WORK)." \
  -m "Co-Authored-By: Claude Fable 5 <noreply@anthropic.com>"
```
Затем спросить пользователя и запушить все три репо: `git push` в каждом. Опционально — сквозная проверка `git clone --recursive https://github.com/cvetkov-es/HubEx.API.git /tmp/api-recursive-check` → `tools/api_cli.py` и `cli/hubex_cli.py` на месте.

---

## Rollback

До Task 16 всё локально: `rm -rf /home/cvetkov_es/development/HubEx.API.Pipeline /home/cvetkov_es/development/HubEx.API.CLI`, в контент-репо `git reset --hard <до-задачный sha>`. После пуша — удаление/приватизация GitHub-репозиториев отдельным решением. Монорепа не менялась нигде.
