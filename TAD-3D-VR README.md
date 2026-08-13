# ТАД-3Д-ВР · TAD-3D-VR

**Trajectory Audit & Diagnostic — 3D Visualization & Verification of Reasoning**
**Пространственная визуализация и операторская верификация траектории рассуждения нейросети**

[![Версия](https://img.shields.io/badge/версия-2.1-blue.svg)](https://github.com/USERNAME/tad-3d-vr)
[![Протокол](https://img.shields.io/badge/протокол-2.2-green.svg)](https://github.com/USERNAME/tad-3d-vr)
[![Методология](https://img.shields.io/badge/МФО--НС-12.3.4-orange.svg)](https://github.com/USERNAME/tad-3d-vr)
[![Лицензия](https://img.shields.io/badge/лицензия-CC%20BY--NC%204.0-lightgrey.svg)](https://creativecommons.org/licenses/by-nc/4.0/)

> Экспериментальный инструмент совместной пространственной верификации решений, принимаемых языковыми моделями. Оператор контролирует не только конечный ответ нейросети, но и предъявленную структуру его обоснования.

---

## 🌐 Языки / Languages

- [🇷🇺 Русская версия](#ru)
- [🇬🇧 English version](#en)

---

<a name="ru"></a>
# 🇷🇺 РУССКАЯ ВЕРСИЯ

## Содержание

1. [Назначение](#ru-naznachenie)
2. [Основание и иерархия](#ru-osnovanie)
3. [Возможности](#ru-vozmozhnosti)
4. [Быстрый старт](#ru-bystriy-start)
5. [Управление](#ru-upravlenie)
6. [Типы узлов и связей](#ru-tipy)
7. [Экспорт и импорт JSON](#ru-json)
8. [Инструкции для следующего цикла](#ru-instrukcii)
9. [Протокол для нейросетей](#ru-protokol)
10. [Структура репозитория](#ru-struktura)
11. [Ограничения](#ru-ogranicheniya)
12. [Авторство](#ru-avtorstvo)

---

<a name="ru-naznachenie"></a>
## 1. Назначение

**ТАД-3Д-ВР** — экспериментальное дополнение к методологии МФО-НС-12.3.4, которое переводит контроль ответов нейросетей из текстового режима в режим **совместной пространственной верификации**.

Каждое значимое решение нейросети представляется в виде **интерактивного 3D-графа**:

```
ЧЕЛОВЕК
    ↕
3D-ГРАФ
    ↕
ТРАЕКТОРИЯ РАССУЖДЕНИЯ
    ↕
16 ЛОГИК · КРИТЕРИИ · ОГРАНИЧЕНИЯ
    ↕
ТЕКСТОВЫЙ РЕЗУЛЬТАТ
    ↕
ИНСТРУКЦИИ ДЛЯ СЛЕДУЮЩЕГО ЦИКЛА
```

**Ключевой принцип:** граф не является прямым отображением скрытых вычислений нейросети. Он является явной, предъявляемой и проверяемой моделью траектории обоснования результата.

---

<a name="ru-osnovanie"></a>
## 2. Основание и иерархия

Проект опирается на систему стандартов МФО-НС-12.3.4:

```
МФО-НС-12.3.4          ← базовая методология (приоритет)
        ↓
ТАД-1.0-И2             ← траекторный аудит и диагностика
        ↓
ТАД-3Д-ВР 1.0          ← пространственная визуализация
        ↓
ТАД-3Д-ВР 2.1          ← рабочий инструмент (этот репозиторий)
ТАД-3Д-ВР 2.2-ПРОТОКОЛ ← инструкция для нейросетей
```

При конфликте рекомендаций приоритет имеет вышестоящий документ.

---

<a name="ru-vozmozhnosti"></a>
## 3. Возможности

| Возможность | Описание |
|---|---|
| **3D-граф траектории** | Интерактивная сцена на Three.js: узлы, связи, стрелки, подписи |
| **Панель узла** | Полная информация: тип, описание, статус, комментарий, трассировка |
| **Операторская верификация** | Подтвердить / отклонить / сбросить статус любого узла |
| **Комментарии** | Текстовые замечания к каждому узлу |
| **Режим выделения** | Выделение группы узлов для создания инструкции |
| **Инструкции для следующего цикла** | Приоритетные указания нейросети (HIGH / MEDIUM / LOW) |
| **Экспорт / импорт JSON** | Полное состояние графа для передачи между чатами |
| **Фильтр логик** | Скрытие/показ неприменённых логик |
| **Полный аудит** | Счётчики по типам узлов, трассировка до источников |
| **16 логик карты расширений** | Триада + 13 расширений по триггерам |

---

<a name="ru-bystriy-start"></a>
## 4. Быстрый старт

### Вариант 1 — использование готового инструмента

```bash
# 1. Клонировать репозиторий
git clone https://github.com/USERNAME/tad-3d-vr.git
cd tad-3d-vr

# 2. Открыть файл в браузере
#    (Chrome, Firefox, Edge, Safari)
open tad-3d-vr-2.1.html
```

Инструмент самодостаточен: все стили и скрипты внутри одного HTML-файла. Внешние зависимости загружаются через CDN (Three.js r128).

### Вариант 2 — генерация нового графа нейросетью

1. Откройте любую нейросеть (Qwen, DeepSeek, GPT, Gemini, Claude).
2. Прикрепите файл `tad-3d-vr-2.2-protocol.html`.
3. Отправьте запрос по шаблону из раздела 9.
4. Нейросеть сгенерирует новый HTML-файл с 3D-графом по вашей задаче.

---

<a name="ru-upravlenie"></a>
## 5. Управление

| Действие | Управление |
|---|---|
| Перемещение камеры | ЛКМ + тянуть |
| Вращение камеры | ПКМ + тянуть |
| Масштаб | Колёсико мыши |
| Авто-вращение вкл/выкл | **Page Up** |
| Детали узла | Клик по узлу |
| Закрыть панели / снять фокус | Esc |

> ⚠ **Важно:** клавиша **Пробел** не используется для управления вращением — она зарезервирована для ввода текста в поля комментариев и инструкций.

---

<a name="ru-tipy"></a>
## 6. Типы узлов и связей

### 6.1. Типы узлов

| Тип | Содержание | Цвет |
|---|---|---|
| `SOURCE` | Нормативный документ, источник | `#7aafff` |
| `SOURCE_FRAGMENT` | Фрагмент источника (статья, пункт) | `#5ac8e8` |
| `EVIDENCE` | Установленное основание | `#4ad8ff` |
| `CLAIM` | Утверждение, требующее проверки | `#ffffff` |
| `LOGIC_OPERATION` | Применённая логика (16 логик КЛ) | `#60ff90` / `#444455` |
| `CRITERION` | Критерий проверки (К1–К6) | `#50d0d0` |
| `CONSTRAINT` | Ограничение | `#ffd700` |
| `RESULT` | Итоговый вывод | `#ff9060` |
| `OPERATOR_REMARK` | Замечание оператора | `#ffb060` |
| `DIAGNOSIS` / `REPAIR_PLAN` | Диагноз и план исправления | `#d090ff` |

### 6.2. Типы связей

| Тип | Значение |
|---|---|
| `SUPPORTS` | поддерживает |
| `DERIVES` | выводится из |
| `CAUSES` | является причиной |
| `CONTRADICTS` | противоречит |
| `ACTIVATES` | активирует логику |
| `CONSTRAINS` | ограничивает переход |
| `VALIDATES` | проверяет |
| `INVALIDATES` | опровергает |
| `REVISES` | пересматривает |
| `RETAINS` | сохраняет рациональное содержание |
| `FEEDS` | передаёт результат следующему уровню |

### 6.3. Шестнадцать логик

**Триада (примат):** Диалектическая · Математическая · Формальная

**Тринадцать расширений (по триггерам):** Паранепротиворечивая · Нечёткая · Вероятностная · Темпоральная · Алетическая модальная · Линейная · Эпистемическая · Деонтическая · STIT · Аргументационная · Немонотонная · Диатопическая · Прагматическая

---

<a name="ru-json"></a>
## 7. Экспорт и импорт JSON

Экспортированный файл содержит **полное состояние** графа и может быть передан в следующий чат с нейросетью.

```json
{
  "protocol": "TAD-3D-VR",
  "version": "2.1",
  "timestamp": "2026-08-13T15:13:25.763Z",
  "applied_logics": [
    { "id": "log_dialectical", "name": "Диалектическая", "used": true }
  ],
  "graph": {
    "nodes": [
      {
        "id": "src1",
        "name": "Договор №01-2026",
        "type": "SOURCE",
        "desc": "Анализируемый документ",
        "color": 8040447,
        "pos": [-12, 6, 0],
        "status": "ok",
        "comment": "Замечание оператора",
        "used": true
      }
    ],
    "edges": [
      { "from": "src1", "to": "frg1", "relation": "DERIVES" }
    ],
    "metadata": {
      "total_nodes": 47,
      "total_edges": 35,
      "logic_count": 3
    }
  },
  "operator_instructions": [
    {
      "id": "instr-001",
      "target_nodes": ["cl1", "ev1"],
      "instruction": "Проверить актуальность ссылок в следующей итерации",
      "priority": "HIGH",
      "created_at": "2026-08-13T15:12:46.939Z"
    }
  ]
}
```

### Протокол передачи между циклами

```
Цикл N (текущий чат)
   ↓ оператор верифицирует, создаёт инструкции
Экспорт JSON (кнопка «📥 Экспорт JSON»)
   ↓ файл tad-3d-vr-2.1-YYYY-MM-DD.json
Цикл N+1 (новый чат с нейросетью)
   ↓ прикрепить JSON + запрос
Импорт / продолжение работы
```

---

<a name="ru-instrukcii"></a>
## 8. Инструкции для следующего цикла

Оператор может создавать **приоритетные указания** для следующего цикла рассуждения нейросети:

1. Включить **«Режим выделения»** в панели управления.
2. Кликнуть по узлам, требующим внимания.
3. Нажать **«📝 Создать инструкцию»**.
4. Ввести текст и выбрать приоритет:

| Приоритет | Значение |
|---|---|
| `HIGH` | Критическое замечание, требует обязательной обработки |
| `MEDIUM` | Важное замечание, рекомендуется учесть |
| `LOW` | Рекомендация, может быть учтена по возможности |

Инструкции сохраняются в массиве `operator_instructions` и экспортируются вместе с графом.

---

<a name="ru-protokol"></a>
## 9. Протокол для нейросетей

Для генерации нового 3D-графа направьте нейросети запрос по следующему шаблону:

```
Создай HTML-файл 3D-визуализации траектории рассуждения
по протоколу ТАД-3Д-ВР 2.2-ПРОТОКОЛ.

КРИТИЧЕСКИЕ ТРЕБОВАНИЯ:
1. Используй Three.js r128 через CDN.
2. Создай узлы по типам: SOURCE, SOURCE_FRAGMENT, EVIDENCE,
   CLAIM, LOGIC_OPERATION, CRITERION, CONSTRAINT, RESULT,
   OPERATOR_REMARK, DIAGNOSIS, REPAIR_PLAN.
3. Создай связи с семантическими типами.
4. Все 16 логик как узлы LOGIC_OPERATION с полем used.
5. Управление авто-вращением — Page Up (НЕ Пробел).
6. Реализуй режим выделения и создание инструкций.
7. Экспорт/импорт JSON со всеми данными.
8. Панель узла — минимум 10 полей.
9. Файл должен быть самодостаточным (один HTML).

Данные задачи:
[описание источников, утверждений, логик, результатов]
```

Полный протокол — в файле [`tad-3d-vr-2.2-protocol.html`](tad-3d-vr-2.2-protocol.html).

---

<a name="ru-struktura"></a>
## 10. Структура репозитория

```
tad-3d-vr/
├── README.md                        ← этот файл
├── tad-3d-vr-2.1.html               ← рабочий инструмент
├── tad-3d-vr-2.2-protocol.html      ← протокол для нейросетей
├── tad-3d-vr-1.0.html               ← методология визуализации
├── tad-1.0-i2.html                  ← траекторный аудит
├── examples/
│   ├── example-author-contract.html ← демо-граф
│   └── example-author-contract.json ← демо-данные
└── mfo-ns/
    └── mfo-ns-12.3.4.html           ← базовая методология
```

---

<a name="ru-ogranicheniya"></a>
## 11. Ограничения

> ⚠ **Граф не является доказательством истинности сам по себе.**
> Граф фиксирует структуру обоснования. Наличие корректной структуры не заменяет проверку содержания и источников.

> ⚠ **Нельзя обещать полную автоматическую верификацию.**
> В силу теоремы Чёрча общезначимость произвольных формул логики предикатов алгоритмически неразрешима. Неразрешимые случаи передаются эксперту.

> ⚠ **Граф не является внутренним процессом нейросети.**
> 3D-граф — эксплицированная модель траектории рассуждения, доступная для контроля. Он не доказывает, что скрытые вычислительные состояния модели имели изображённую структуру.

---

<a name="ru-avtorstvo"></a>
## 12. Авторство

**© Гурин Сергей Евгеньевич**, к.т.н., 2026
**© Gurin Sergey Evgenievich**, PhD in Technical Sciences, 2026

Создано при участии нейросетей: Qwen · DeepSeek · MiniMax

**Основание:**
- МФО-НС-12.3.4 — Методология формирования и проверки ответов нейросетей
- ТАД-1.0-И2 — Траекторный аудит и диагностика
- ТАД-3Д-ВР 1.0 — Пространственная визуализация
- SearchAuditor, arXiv:2608.05212 (внешнее основание гипотезы)

**Лицензия:** CC BY-NC 4.0

---
---

<a name="en"></a>
# 🇬🇧 ENGLISH VERSION

## Table of Contents

1. [Purpose](#en-purpose)
2. [Foundation and Hierarchy](#en-foundation)
3. [Features](#en-features)
4. [Quick Start](#en-quick-start)
5. [Controls](#en-controls)
6. [Node and Edge Types](#en-types)
7. [JSON Export and Import](#en-json)
8. [Instructions for the Next Cycle](#en-instructions)
9. [Protocol for Neural Networks](#en-protocol)
10. [Repository Structure](#en-structure)
11. [Limitations](#en-limitations)
12. [Attribution](#en-attribution)

---

<a name="en-purpose"></a>
## 1. Purpose

**TAD-3D-VR** (Trajectory Audit & Diagnostic — 3D Visualization & Verification of Reasoning) is an experimental extension to the MFO-NS-12.3.4 methodology. It shifts the control of neural network answers from a text-only mode to a **collaborative spatial verification** mode.

Every significant decision made by a neural network is represented as an **interactive 3D graph**:

```
HUMAN
    ↕
3D GRAPH
    ↕
REASONING TRAJECTORY
    ↕
16 LOGICS · CRITERIA · CONSTRAINTS
    ↕
TEXT RESULT
    ↕
INSTRUCTIONS FOR THE NEXT CYCLE
```

**Key principle:** the graph is not a direct mapping of the neural network's hidden computations. It is an explicit, presentable, and verifiable model of the trajectory of the result's justification.

---

<a name="en-foundation"></a>
## 2. Foundation and Hierarchy

The project is based on the MFO-NS-12.3.4 standard system:

```
MFO-NS-12.3.4              ← base methodology (priority)
        ↓
TAD-1.0-I2                 ← trajectory audit & diagnostic
        ↓
TAD-3D-VR 1.0              ← spatial visualization
        ↓
TAD-3D-VR 2.1              ← working tool (this repository)
TAD-3D-VR 2.2-PROTOCOL     ← instruction for neural networks
```

In case of conflict, the higher-level document takes priority.

---

<a name="en-features"></a>
## 3. Features

| Feature | Description |
|---|---|
| **3D trajectory graph** | Interactive Three.js scene: nodes, edges, arrows, labels |
| **Node panel** | Full info: type, description, status, comment, traceability |
| **Operator verification** | Confirm / reject / reset the status of any node |
| **Comments** | Text remarks for each node |
| **Selection mode** | Select a group of nodes to create an instruction |
| **Next-cycle instructions** | Priority directives for the neural network (HIGH / MEDIUM / LOW) |
| **JSON export / import** | Full graph state for transfer between chats |
| **Logic filter** | Show / hide unused logics |
| **Full audit** | Counters by node type, traceability to sources |
| **16 logics of the extension map** | Triad + 13 extensions by triggers |

---

<a name="en-quick-start"></a>
## 4. Quick Start

### Option 1 — Use the ready-made tool

```bash
# 1. Clone the repository
git clone https://github.com/USERNAME/tad-3d-vr.git
cd tad-3d-vr

# 2. Open the file in a browser
#    (Chrome, Firefox, Edge, Safari)
open tad-3d-vr-2.1.html
```

The tool is self-contained: all styles and scripts are inside a single HTML file. External dependencies are loaded via CDN (Three.js r128).

### Option 2 — Generate a new graph with a neural network

1. Open any neural network (Qwen, DeepSeek, GPT, Gemini, Claude).
2. Attach the file `tad-3d-vr-2.2-protocol.html`.
3. Send a request using the template from Section 9.
4. The neural network will generate a new HTML file with a 3D graph for your task.

---

<a name="en-controls"></a>
## 5. Controls

| Action | Control |
|---|---|
| Pan camera | Left mouse button + drag |
| Rotate camera | Right mouse button + drag |
| Zoom | Mouse wheel |
| Toggle auto-rotation | **Page Up** |
| Node details | Click on a node |
| Close panels / blur focus | Esc |

> ⚠ **Important:** the **Space** key is not used for rotation control — it is reserved for typing text into comment and instruction fields.

---

<a name="en-types"></a>
## 6. Node and Edge Types

### 6.1. Node Types

| Type | Content | Color |
|---|---|---|
| `SOURCE` | Normative document, source | `#7aafff` |
| `SOURCE_FRAGMENT` | Source fragment (article, clause) | `#5ac8e8` |
| `EVIDENCE` | Established ground | `#4ad8ff` |
| `CLAIM` | Assertion requiring verification | `#ffffff` |
| `LOGIC_OPERATION` | Applied logic (16 logics) | `#60ff90` / `#444455` |
| `CRITERION` | Verification criterion (K1–K6) | `#50d0d0` |
| `CONSTRAINT` | Constraint | `#ffd700` |
| `RESULT` | Final conclusion | `#ff9060` |
| `OPERATOR_REMARK` | Operator remark | `#ffb060` |
| `DIAGNOSIS` / `REPAIR_PLAN` | Diagnosis and repair plan | `#d090ff` |

### 6.2. Edge Types

| Type | Meaning |
|---|---|
| `SUPPORTS` | supports |
| `DERIVES` | is derived from |
| `CAUSES` | is the cause of |
| `CONTRADICTS` | contradicts |
| `ACTIVATES` | activates a logic |
| `CONSTRAINS` | constrains a transition |
| `VALIDATES` | validates |
| `INVALIDATES` | invalidates |
| `REVISES` | revises |
| `RETAINS` | retains rational content |
| `FEEDS` | feeds result to the next level |

### 6.3. The Sixteen Logics

**Triad (primacy):** Dialectical · Mathematical · Formal

**Thirteen extensions (by triggers):** Paraconsistent · Fuzzy · Probabilistic · Temporal · Alethic Modal · Linear · Epistemic · Deontic · STIT · Argumentative · Non-monotonic · Diatopic · Pragmatic

---

<a name="en-json"></a>
## 7. JSON Export and Import

The exported file contains the **full state** of the graph and can be passed to the next chat with a neural network.

```json
{
  "protocol": "TAD-3D-VR",
  "version": "2.1",
  "timestamp": "2026-08-13T15:13:25.763Z",
  "applied_logics": [
    { "id": "log_dialectical", "name": "Dialectical", "used": true }
  ],
  "graph": {
    "nodes": [
      {
        "id": "src1",
        "name": "Contract No. 01-2026",
        "type": "SOURCE",
        "desc": "The document under analysis",
        "color": 8040447,
        "pos": [-12, 6, 0],
        "status": "ok",
        "comment": "Operator remark",
        "used": true
      }
    ],
    "edges": [
      { "from": "src1", "to": "frg1", "relation": "DERIVES" }
    ],
    "metadata": {
      "total_nodes": 47,
      "total_edges": 35,
      "logic_count": 3
    }
  },
  "operator_instructions": [
    {
      "id": "instr-001",
      "target_nodes": ["cl1", "ev1"],
      "instruction": "Verify the relevance of references in the next iteration",
      "priority": "HIGH",
      "created_at": "2026-08-13T15:12:46.939Z"
    }
  ]
}
```

### Protocol for transferring between cycles

```
Cycle N (current chat)
   ↓ operator verifies, creates instructions
JSON Export ("📥 Export JSON" button)
   ↓ file tad-3d-vr-2.1-YYYY-MM-DD.json
Cycle N+1 (new chat with a neural network)
   ↓ attach JSON + request
Import / continuation of work
```

---

<a name="en-instructions"></a>
## 8. Instructions for the Next Cycle

The operator can create **priority directives** for the next reasoning cycle of the neural network:

1. Enable **"Selection Mode"** in the control panel.
2. Click on the nodes that require attention.
3. Press **"📝 Create Instruction"**.
4. Enter the text and select a priority:

| Priority | Meaning |
|---|---|
| `HIGH` | Critical remark, requires mandatory processing |
| `MEDIUM` | Important remark, recommended to consider |
| `LOW` | Recommendation, may be considered if possible |

Instructions are stored in the `operator_instructions` array and exported together with the graph.

---

<a name="en-protocol"></a>
## 9. Protocol for Neural Networks

To generate a new 3D graph, send the neural network a request using the following template:

```
Create an HTML file for 3D visualization of the reasoning trajectory
according to the TAD-3D-VR 2.2-PROTOCOL.

CRITICAL REQUIREMENTS:
1. Use Three.js r128 via CDN.
2. Create nodes by types: SOURCE, SOURCE_FRAGMENT, EVIDENCE,
   CLAIM, LOGIC_OPERATION, CRITERION, CONSTRAINT, RESULT,
   OPERATOR_REMARK, DIAGNOSIS, REPAIR_PLAN.
3. Create edges with semantic types.
4. All 16 logics as LOGIC_OPERATION nodes with the "used" field.
5. Auto-rotation control — Page Up (NOT Space).
6. Implement selection mode and instruction creation.
7. JSON export/import with all data.
8. Node panel — at least 10 fields.
9. The file must be self-contained (single HTML).

Task data:
[description of sources, claims, logics, results]
```

The full protocol is in the file [`tad-3d-vr-2.2-protocol.html`](tad-3d-vr-2.2-protocol.html).

---

<a name="en-structure"></a>
## 10. Repository Structure

```
tad-3d-vr/
├── README.md                        ← this file
├── tad-3d-vr-2.1.html               ← working tool
├── tad-3d-vr-2.2-protocol.html      ← protocol for neural networks
├── tad-3d-vr-1.0.html               ← visualization methodology
├── tad-1.0-i2.html                  ← trajectory audit
├── examples/
│   ├── example-author-contract.html ← demo graph
│   └── example-author-contract.json ← demo data
└── mfo-ns/
    └── mfo-ns-12.3.4.html           ← base methodology
```

---

<a name="en-limitations"></a>
## 11. Limitations

> ⚠ **The graph is not proof of truth in itself.**
> The graph fixes the structure of justification. The presence of a correct structure does not replace verification of content and sources.

> ⚠ **Full automatic verification cannot be promised.**
> Due to Church's theorem, the validity of arbitrary predicate logic formulas is algorithmically undecidable. Undecidable cases are transferred to an expert.

> ⚠ **The graph is not the internal process of the neural network.**
> The 3D graph is an explicated model of the reasoning trajectory available for control. It does not prove that the model's hidden computational states literally had the depicted structure.

---

<a name="en-attribution"></a>
## 12. Attribution

**© Gurin Sergey Evgenievich**, PhD in Technical Sciences, 2026

Created with the participation of neural networks: Qwen · DeepSeek · MiniMax

**Foundation:**
- MFO-NS-12.3.4 — Methodology of Formation and Verification of Neural Network Answers
- TAD-1.0-I2 — Trajectory Audit & Diagnostic
- TAD-3D-VR 1.0 — Spatial Visualization
- SearchAuditor, arXiv:2608.05212 (external ground for the hypothesis)

**License:** CC BY-NC 4.0

---

*Система стандартов Гурина · Gurin Standards System · 2026*