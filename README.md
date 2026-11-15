# 🌌 Сингулярность / Singularity

![Скриншот 1](Screenshot_2026-11-10-06-19-45-51_40deb401b9ffe8e1df2f1cc5ba480b12.jpg)

[Русский](#русский) | [English](#english)

---

## Русский

**Сингулярность** — это универсальное cross-platform приложение «всё в одном» с гибким доступом для работы с данными, заметками, расчетами и чертежами. Программа объединяет текстовый редактор, урезанный Excel, SQL-движок, Канбан, ТРИЗ-модуль и CAD-систему.

### 🌐 Концепция и Доступность
* **Полная кроссплатформенность:** Работает онлайн, как веб-офлайн (PWA приложение), а также в виде отдельных сборок с диска устройства (APK для Android и EXE для Windows). Внутри APK и EXE используются свои изолированные WEB-окружения (WebView).
* **Локальное хранение:** Все данные хранятся в `localStorage` вашего браузера или WebView. Полная приватность — никаких внешних серверов.
* **Автономность:** При первом запуске библиотека SQL кэшируется для работы офлайн. Дашборды и Лог работают офлайн «из коробки».
* **Перенос данных:** Файл базы данных легко переносится между устройствами любым удобным способом (например, через облако).

---

### 🛠️ Основные возможности

#### 1. Текстовые заметки & База знаний (Wiki)
* **Семантические связи:** Связывайте заметки по смыслу через Wiki-ссылки: `[[ссылка на другую заметку]]`.
* **Блочная структура:** Текст делится на блоки (абзацы). Нажмите на 6 точек слева от блока (или зажмите пальцем на телефоне), дождитесь подсветки и перетащите блок в нужное место.
* **Быстрое меню (`/` или `+`):** Нажмите `/` на ПК или кнопку `+` на телефоне в начале строки для вызова меню вставки блоков (таблицы, разделители, стили). Доступен быстрый поиск по меню.
* **Управление:** Кнопка **«+ Новая заметка»** на сайдбаре создает документ. Кнопка **«Удалить»** (с подтверждением) очищает заметки.
* **Экспорт:** Поддерживается выгрузка в форматы **Word** и **TXT**.

#### 2. Табличные заметки & Урезанный Excel
* **Управление строками и столбцами:** Копируйте/вставляйте строки кликом по номеру слева. Столбцы управляются через меню фильтров (кнопка «Стрелочка» в заголовке).
* **Перенос данных (ПК):** Сделайте ввод в ячейке неактивным, зажмите ЛКМ на пустом месте ячейки и перетащите её содержимое в другую.
* **Формулы:** Поддерживаются формулы в стиле Excel. Заголовки столбцов соответствуют буквам (A, B, C...). Формулы пишутся поячеечно (без растягивания диапазонов), что подходит для быстрых расчетов.
* **Импорт/Экспорт Excel:** Поддерживается загрузка файлов `.xlsx` (первая строка обязательно должна быть заголовками) с сохранением и переносом формул.
* *Примечание:* Для обновления результатов формул и выравнивания ширины колонок после импорта нажмите на название заметки в сайдбаре.

#### 3. SQL-аналитика (SQLite движок)
* **Полноценный SQL:** К табличным заметкам можно применять SQL и сложные CTE-запросы.
* **Регистронезависимость для кириллицы:** Реализована кастомная функция `fold()` для обхода ограничений SQLite.
  * *Пример запроса:*
    ```sql
    SELECT s.Имя, s.Фамилия, w.Стаж 
    FROM Сотрудники s 
    LEFT JOIN "Опыт работы" w ON fold(s.Имя) = fold(w.Имя);
    ```
    *(Внимание: из-за внешнего обработчика функция fold() снижает скорость выполнения).*
* **Сохранение:** Запросы сохраняются вместе с базой данных. Результат можно экспортировать в новую табличную заметку или встроить таблицей в текстовую заметку.
* **OLAP-аналитика:** Кнопка **«Куб»** на сайдбаре открывает меню для построения OLAP-матриц на основе выбранных таблиц.

#### 4. Проекты, Логи и ТРИЗ
* **Канбан-доска:** Простая доска для контроля процессов, задач и фиксации важной информации.
* **Лог (Журнал действий):** Фиксирует все действия по времени (включая импорт). На оси времени строится **Диаграмма Ганта** от предыдущего события до текущего времени (красная черта). Лог можно выгружать.
* **Модуль ТРИЗ:** Инструмент для фиксации мыслительного процесса по АРИЗ и сохранения изобретательских идей. Требует понимания методологии ТРИЗ. Данные выводятся в Word, TXT или Excel (в файл общей базы при экспорте этот раздел не сохраняется).

#### 5. Чертежный модуль (Аналог AutoCAD R13)
* **Форматы:** Чертежи сохраняются/загружаются как координаты объектов в **JSON** или **DXF**. Экспорт доступен в **SVG** и **PNG** (с отступами в 2 единицы от рамки или крайних элементов).
* **Управление на ПК:** ПКМ — перемещение по холсту, ЛКМ — выделение объектов.
* **Управление на смартфоне:** Инструмент **«РАМКА»** переключает режим выделения или перемещения пальцем (допуск погрешности пальца 2.5 пункта).
* **Интерпретатор Автолиспа:** Позволяет описывать чертеж кодом (лисп-программой). Пример доступен по кнопке «Пример» в интерпретаторе. При замене команд (например, `PLINE` на `LINE`) результат чертежа изменится.
* **Свойства и Стили:** Функция **СВОЙ** изменяет свойства выделенной группы объектов. Функция **СТИЛЬ** задает стиль линии (для новых линий или для выделенной).
  
При разработке использовались технологии искусственного интеллекта

---
---

## English

**Singularity** is a universal, cross-platform, "all-in-one" application with flexible access modes for managing data, notes, calculations, and drawings. The program combines a text editor, a lightweight Excel alternative, an SQL engine, a Kanban board, a TRIZ module, and a CAD system.

### 🌐 Concept & Accessibility
* **True Cross-Platform:** Works online, web-offline (as a Progressive Web App - PWA), and natively from device storage (APK for Android, EXE for Windows). APK and EXE versions run in isolated web environments (WebView).
* **Local Storage:** All data is kept inside your browser's or WebView's `localStorage`. Complete privacy — no external servers.
* **Offline-First:** On the first launch, the SQL library is cached for offline use. Dashboards and Logs work offline out of the box.
* **Data Portability:** The database file can be transferred between devices using any preferred method (e.g., via cloud storage).

---

### 🛠️ Key Features

#### 1. Text Notes & Knowledge Base (Wiki)
* **Semantic Connections:** Connect notes using Wiki-links: `[[link to another note]]`.
* **Block-Based Structure:** Text is split into movable blocks. Click and hold the 6 dots on the left (or long-press on mobile) until highlighted, then drag and drop the block to rearrange.
* **Quick Insert Menu (`/` or `+`):** Type `/` on PC or press `+` on mobile at the start of a block to open the insertion menu (tables, dividers, styles). Features built-in search.
* **Management:** The **"+ New Note"** button on the sidebar creates documents. The red **"Delete"** button (with confirmation) deletes notes.
* **Export:** Supports exporting to **Word** and **TXT** files.

#### 2. Table Notes & Lightweight Excel
* **Row & Column Management:** Copy/paste rows by clicking row numbers on the left. Manage columns (copy, insert left/right, clear, delete) using the arrow menu in the column header.
* **Data Transfer (PC):** Deactivate cell text input, click and hold LMB on empty space inside the cell, and drag its content to another cell.
* **Formulas:** Excel-like formulas are supported. Column headers represent letters (A, B, C...). Formulas are applied per cell (no range stretching), which is optimal for quick, small-scale calculations.
* **Excel Import/Export:** Import `.xlsx` files (the first row must contain headers). Formulas are fully preserved during import/export.
* *Note:* To refresh formula results and auto-align column widths after importing, click the note's name in the sidebar.

#### 3. SQL Analytics (SQLite Engine)
* **Full-fledged SQL:** Apply SQL and complex CTE queries directly to table notes.
* **Cyrillic Case Insensitivity:** Features a custom `fold()` function to overcome standard SQLite limitations.
  * *Query Example:*
    ```sql
    SELECT s.Имя, s.Фамилия, w.Стаж 
    FROM Сотрудники s 
    LEFT JOIN "Опыт работы" w ON fold(s.Имя) = fold(w.Имя);
    ```
    *(Note: Using the fold() function impacts query execution speed due to external processing).*
* **Persistence:** Saved queries are stored within the database. Results can be saved as a new table note or inserted as a table block into a text note.
* **OLAP Analytics:** The **"Cube"** button in the sidebar opens the OLAP analytics menu to generate multidimensional matrices from selected tables.

#### 4. Projects, Logs, and TRIZ
* **Kanban Board:** A simple board to monitor workflows, track tasks, and pin important data.
* **Log (Action Journal):** Timestamps all actions (including data imports). A **Gantt Chart** is automatically plotted on the timeline from the previous event to the current time (marked by a red line). Logs can be exported.
* **TRIZ Module:** A workspace for structuring the thinking process via ARIZ algorithms and saving inventive ideas. Requires a prior understanding of TRIZ methodology. Data can be exported to Word, TXT, or Excel (not included in the main database backup).

#### 5. Drawing Module (Early AutoCAD R13 Paradigm)
* **Formats:** Drawings are saved and loaded as object coordinate sets in **JSON** or **DXF** formats. Exporting is available in **SVG** and **PNG** (with 2-unit margins from the border frame or outermost elements).
* **PC Controls:** RMB to pan across the canvas, LMB to select objects.
* **Mobile Controls:** The **"FRAME"** tool toggles between selection and finger panning (features a 2.5-point touch tolerance).
* **AutoLISP-like Interpreter:** Allows defining drawings using LISP-like programming code. A preset is available via the "Example" button. Changing commands (e.g., `PLINE` to `LINE`) yields different drawing results.
* **Properties & Styles:** The **PROPS** function modifies properties of a selected object group. The **STYLE** function sets line styles (applies to new lines or changes currently selected ones).

Artificial intelligence technologies were used during development.

More on OLAP: An example of implementing a cube in SQL

<details>
<summary>Click to expand an example of a sequence of SQL queries</summary>

```SQL
 -- 1. Receipts of finished products: all packers in one table

CREATE TEMP TABLE GP_ALL AS
SELECT 'З' AS Packer, 10 AS Plant, Product, Batch, SUM(Quantity) AS TotalQuantity FROM "GP Receipts Z November 2026" GROUP BY Product, Batch
UNION ALL
SELECT 'A' AS Packer, 30 AS Plant, Product, Batch, SUM(Quantity) AS TotalQuantity FROM "GP A Receipts November 2026" GROUP BY Product, Batch
UNION ALL
SELECT 'B' AS Packer, 30 AS Plant, Product, Batch, SUM(Quantity) AS TotalQuantity FROM "GP B Receipts November 2026" GROUP BY Product, Batch
UNION ALL
SELECT 'V' AS Packer, 30 AS Plant, Product, Batch, SUM(Quantity) AS TotalQuantity FROM "GP Incoming V November 2026" GROUP BY Product, Batch
UNION ALL
SELECT 'G' AS Packer, 30 AS Plant, Product, Batch, SUM(Quantity) AS TotalQuantity FROM "GP Incoming G November 2026" GROUP BY Product, Batch
UNION ALL
SELECT 'D' AS Packer, 30 AS Plant, Product, Batch, SUM(Quantity) AS TotalQuantity FROM "GP Receipts D November 2026" GROUP BY Product, Batch
UNION ALL
SELECT 'E' AS Packer, 30 AS Plant, Product, Batch, SUM(Quantity) AS TotalQuantity FROM "GP Receipts E November 2026" GROUP BY Product, Batch
UNION ALL
SELECT 'Ж' AS Packer, 30 AS Plant, Drug, Batch, SUM(Amount) AS TotalAmount FROM "GP Receipts Zh November 2026" GROUP BY Drug, Batch;

-- 2. Plans for all packers in one table, deducting the supplied GP

CREATE TEMP TABLE PLAN_ALL AS
SELECT 'З' AS Packer, 10 AS Plant, s.Product, s.Quantity AS Plan, s.Batch, s.Month, COALESCE(g.Amount, 0) AS Delivered, COALESCE(s.Quantity, 0) - COALESCE(g.Amount, 0) AS Remaining, s.VM, s.Raw Material, s.Note
FROM "Plan З November 2026" s
LEFT JOIN GP_ALL g ON g.Packer = 'З' AND fold(s.Drug) = fold(g.Drug) AND s.Month = g.Party
UNION ALL
SELECT 'A' AS Packer, 30 AS Plant, s.Drug, s.Quantity AS Plan, s.Batch, s.Month, COALESCE(g.SumAmount, 0) AS Delivered, COALESCE(s.Quantity, 0) - COALESCE(g.SumAmount, 0) AS Remaining, s.VM, s.Raw Material, s.Note
FROM "Plan A November 2026" s
LEFT JOIN GP_ALL g ON g.Packer = 'A' AND fold(s.Drug) = fold(g.Drug) AND s.Batch = g.Party
UNION ALL
SELECT 'B' AS Packer, 30 AS Plant, s.Drug, s.Quantity AS Plan, s.Batch, s.Month, COALESCE(g.SumAmount, 0) AS Delivered, COALESCE(s.Quantity, 0) - COALESCE(g.SumAmount, 0) AS Remaining, s.VM, s.Raw Material, s.Note
FROM "Plan B November 2026" s
LEFT JOIN GP_ALL g ON g.Packer = 'Б' AND fold(s.Drug) = fold(g.Drug) AND s.Batch = g.Party
UNION ALL
SELECT 'В' AS Packer, 30 AS Plant, s.Drug, s.Quantity AS Plan, s.Batch, s.Month, COALESCE(g.SumAmount, 0) AS Delivered, COALESCE(s.Quantity, 0) - COALESCE(g.SumAmount, 0) AS Remaining, s.VM, s.Raw Material, s.Note
FROM "Plan In November 2026" s
LEFT JOIN GP_ALL g ON g.Packer = 'В' AND fold(s.Drug) = fold(g.Drug) AND s.Batch = g.Party
UNION ALL
SELECT 'Г' AS Packer, 30 AS Plant, s.Drug, s.Quantity AS Plan, s.Batch, s.Month, COALESCE(g.SumAmount, 0) AS Delivered, COALESCE(s.Quantity, 0) - COALESCE(g.SumAmount, 0) AS Remaining, s.VM, s.Raw Material, s.Note
FROM "Plan Г November 2026" s
LEFT JOIN GP_ALL g ON g.Packer = 'Г' AND fold(s.Product) = fold(g.Product) AND s.Batch = g.Party
UNION ALL
SELECT 'D' AS Packer, 30 AS Plant, s.Drug, s.Quantity AS Plan, s.Batch, s.Month, COALESCE(g.SumAmount, 0) AS Delivered, COALESCE(s.Quantity, 0) - COALESCE(g.SumAmount, 0) AS Remaining, s.VM, s.RawMaterial, s.Note
FROM "Plan D November 2026" s
LEFT JOIN GP_ALL g ON g.Packer = 'D' AND fold(s.Drug) = fold(g.Drug) AND s.Batch = g.Party
UNION ALL
SELECT 'E' AS Packer, 30 AS Plant, s.Drug, s.Quantity AS Plan, s.Batch, s.Month, COALESCE(g.SumAmount, 0) AS Delivered, COALESCE(s.Quantity, 0) - COALESCE(g.SumAmount, 0) AS Remaining, s.VM, s.Raw Material, s.Note
FROM "Plan E November 2026" s
LEFT JOIN GP_ALL g ON g.Packer = 'E' AND fold(s.Drug) = fold(g.Drug) AND s.Batch = g.Party
UNION ALL
SELECT 'Ж' AS Packer, 30 AS Plant, s.Drug, s.Quantity AS Plan, s.Batch, s.Month, COALESCE(g.SumAmount, 0) AS Delivered, COALESCE(s.Quantity, 0) - COALESCE(g.SumAmount, 0) AS Remaining, s.VM, s.Raw Material, s.Note
FROM "Plan Ж November 2026" s
LEFT JOIN GP_ALL g ON g.Packer = 'Ж' AND fold(s.Drug) = fold(g.Drug) AND s.Batch = g.Batch;

-- 3. Fact: plan × norms. Rows without a found norm are NOT lost (norm 0, note)

CREATE TEMP TABLE FACT AS
SELECT IIF(p.Packer = 'Z', 'Report Z', 'Main') AS Report
       p.Packer, p. Factory, p. Preparation, p. Month, p. Batch, p. Plan, p. Delivered, p.Left,
       COALESCE(s.ShortTextOfObject, '(no norm found)') AS Component,
       COALESCE(s."Norm per 1 pc", 0) AS "Norm per 1 pc",
       IIF(COALESCE(p.Left, 0) > 0, COALESCE(p.Left, 0) * COALESCE(s."Norm per 1 pc", 0), 0) AS Needed
       p.VM, p.Raw Material, p.Note,
       (SELECT w.Description FROM "Preparations - description of type and purpose of use" w
         WHERE fold(p.Preparation) LIKE fold('%' || w.NameOfPreparation || '%') LIMIT 1) AS Description
FROM PLAN_ALL p
LEFT JOIN (SELECT DISTINCT Factory, "Material Name", Short Text of Object, "Standard per 1 unit" FROM "Standards for SI") s
       ON fold(p.Drug) = fold(s."Material Name") AND s.Factory = p.Factory;

-- 4. Warehouse snapshots: one value per component (without line‑by‑line replication)

CREATE TEMP TABLE UNISK AS
SELECT 'H' AS Packer, "Name of material", TotaLsaldo FROM "Warehouse 10 dated 11/01/2026"
UNION ALL SELECT 'A' AS Packer, "Name of material", TotaLsaldo FROM "Warehouse A 11/01/2026"
UNION ALL SELECT 'B' AS Packer, "Name of material", TotaLsaldo FROM "Warehouse B 11/01/2026"
UNION ALL SELECT 'B' AS Packer, "Name of material", TotaLsaldo FROM "Warehouse ON 11/01/2026"
UNION ALL SELECT 'D' AS Packer, "Name of material", TotaLsaldo FROM "Warehouse ON 11/01/2026"
UNION ALL SELECT 'D' AS Packer, "Name of material", TotaLsaldo FROM "Warehouse D 11/01/2026"
UNION ALL SELECT 'E' AS Packer, "Material name", Total amount FROM "Warehouse E 11/01/2026"
UNION ALL SELECT 'W' AS Packer, "Material name", Total amount FROM "Warehouse W 11/01/2026";

CREATE TEMP TABLE SK_FAS AS
SELECT Packer, "Material Name", SUM(TotalBalance) AS Balance
FROM UNISK GROUP BY Packer, "Material Name";

CREATE TEMP TABLE SK_CS AS
SELECT "Material Name", SUM(TotalBalance) AS Balance
FROM "CS Warehouse 01.11.2026" GROUP BY "Material Name";

CREATE TEMP TABLE SK_PF AS
SELECT "Material Name", SUM(TotalBalance) AS Balance
FROM "Warehouse 113 dated 01.11.2026" GROUP BY "Material Name";

-- 5. Total requirement by (packer, component): one aggregate instead of self-joins (Cartesian product)

CREATE TEMP TABLE AGG_KF AS
SELECT Report, Packer, Component, SUM(Need) AS Need_Total, COUNT(*) AS Rows
FROM FACT GROUP BY Report, Packer, Component;

-- 6. Packer balance by component (one row per pair)

CREATE TEMP TABLE DEF_KF AS
SELECT k.Report, k.Packer, k.Component, k.Need_Total, k.Lines,
       COALESCE(sk.Balance, 0) AS "Packer warehouse",
       COALESCE(sk.Balance, 0) - k.Need_Total AS "Packer Balance"
FROM AGG_KF k
LEFT JOIN SK_FAS sk ON k.Packer = sk.Packer AND fold(k.Component) = fold(sk."Material Name");

-- 7. Total deficit by component, CS warehouse, and "CS Total" (one row per component)

CREATE TEMP TABLE DEF_K AS
SELECT Report, Component, SUM(MIN("Filler Balance", 0)) AS Deficit_Total
FROM DEF_KF GROUP BY Report, Component;

CREATE TEMP TABLE CS_K AS
SELECT d.Report, d.Component,
       COALESCE(cs.Balance, 0) AS CS,
       COALESCE(cs.Balance, 0) + COALESCE(dk.Deficit_Obsh, 0) AS "Total CS"
FROM (SELECT DISTINCT Report, Component FROM DEF_KF) d
LEFT JOIN SK_CS cs ON fold(d.Component) = fold(cs."Material Name")
LEFT JOIN DEF_K dk ON dk.Report = d.Report AND fold(dk.Component) = fold(d.Component);

-- 8. Denominator of the distribution: total demand and the number of rows per component (for Kimbell)

CREATE TEMP TABLE AGG_K AS
SELECT Report, Component, SUM(Need) AS Need_Total, COUNT(*) AS Lines_Total
FROM FACT GROUP BY Report, Component;

-- 9. Final table for OLAP. Grain: ```sql
-- 1. Receipts of finished products: all packers in one table

CREATE TEMP TABLE GP_ALL AS
SELECT 'З' AS Packer, 10 AS Plant, Product, Batch, SUM(Quantity) AS TotalQuantity FROM "GP Receipts Z November 2026" GROUP BY Product, Batch
UNION ALL
SELECT 'A' AS Packer, 30 AS Plant, Product, Batch, SUM(Quantity) AS TotalQuantity FROM "GP A Receipts November 2026" GROUP BY Product, Batch
UNION ALL
SELECT 'B' AS Packer, 30 AS Plant, Product, Batch, SUM(Quantity) AS TotalQuantity FROM "GP B Receipts November 2026" GROUP BY Product, Batch
UNION ALL
SELECT 'V' AS Packer, 30 AS Plant, Product, Batch, SUM(Quantity) AS TotalQuantity FROM "GP Incoming V November 2026" GROUP BY Product, Batch
UNION ALL
SELECT 'G' AS Packer, 30 AS Plant, Product, Batch, SUM(Quantity) AS TotalQuantity FROM "GP Incoming G November 2026" GROUP BY Product, Batch
UNION ALL
SELECT 'D' AS Packer, 30 AS Plant, Product, Batch, SUM(Quantity) AS TotalQuantity FROM "GP Receipts D November 2026" GROUP BY Product, Batch
UNION ALL
SELECT 'E' AS Packer, 30 AS Plant, Product, Batch, SUM(Quantity) AS TotalQuantity FROM "GP Receipts E November 2026" GROUP BY Product, Batch
UNION ALL
SELECT 'Ж' AS Packer, 30 AS Plant, Drug, Batch, SUM(Amount) AS TotalAmount FROM "GP Receipts Zh November 2026" GROUP BY Drug, Batch;

-- 2. Plans for all packers in one table, deducting the supplied GP

CREATE TEMP TABLE PLAN_ALL AS
SELECT 'З' AS Packer, 10 AS Plant, s.Product, s.Quantity AS Plan, s.Batch, s.Month, COALESCE(g.Amount, 0) AS Delivered, COALESCE(s.Quantity, 0) - COALESCE(g.Amount, 0) AS Remaining, s.VM, s.Raw Material, s.Note
FROM "Plan З November 2026" s
LEFT JOIN GP_ALL g ON g.Packer = 'З' AND fold(s.Drug) = fold(g.Drug) AND s.Month = g.Party
UNION ALL
SELECT 'A' AS Packer, 30 AS Plant, s.Drug, s.Quantity AS Plan, s.Batch, s.Month, COALESCE(g.SumAmount, 0) AS Delivered, COALESCE(s.Quantity, 0) - COALESCE(g.SumAmount, 0) AS Remaining, s.VM, s.Raw Material, s.Note
FROM "Plan A November 2026" s
LEFT JOIN GP_ALL g ON g.Packer = 'A' AND fold(s.Drug) = fold(g.Drug) AND s.Batch = g.Party
UNION ALL
SELECT 'B' AS Packer, 30 AS Plant, s.Drug, s.Quantity AS Plan, s.Batch, s.Month, COALESCE(g.SumAmount, 0) AS Delivered, COALESCE(s.Quantity, 0) - COALESCE(g.SumAmount, 0) AS Remaining, s.VM, s.Raw Material, s.Note
FROM "Plan B November 2026" s
LEFT JOIN GP_ALL g ON g.Packer = 'Б' AND fold(s.Drug) = fold(g.Drug) AND s.Batch = g.Party
UNION ALL
SELECT 'В' AS Packer, 30 AS Plant, s.Drug, s.Quantity AS Plan, s.Batch, s.Month, COALESCE(g.SumAmount, 0) AS Delivered, COALESCE(s.Quantity, 0) - COALESCE(g.SumAmount, 0) AS Remaining, s.VM, s.Raw Material, s.Note
FROM "Plan In November 2026" s
LEFT JOIN GP_ALL g ON g.Packer = 'В' AND fold(s.Drug) = fold(g.Drug) AND s.Batch = g.Party
UNION ALL
SELECT 'Г' AS Packer, 30 AS Plant, s.Drug, s.Quantity AS Plan, s.Batch, s.Month, COALESCE(g.SumAmount, 0) AS Delivered, COALESCE(s.Quantity, 0) - COALESCE(g.SumAmount, 0) AS Remaining, s.VM, s.Raw Material, s.Note
FROM "Plan Г November 2026" s
LEFT JOIN GP_ALL g ON g.Packer = 'Г' AND fold(s.Product) = fold(g.Product) AND s.Batch = g.Party
UNION ALL
SELECT 'D' AS Packer, 30 AS Plant, s.Drug, s.Quantity AS Plan, s.Batch, s.Month, COALESCE(g.SumAmount, 0) AS Delivered, COALESCE(s.Quantity, 0) - COALESCE(g.SumAmount, 0) AS Remaining, s.VM, s.RawMaterial, s.Note
FROM "Plan D November 2026" s
LEFT JOIN GP_ALL g ON g.Packer = 'D' AND fold(s.Drug) = fold(g.Drug) AND s.Batch = g.Party
UNION ALL
SELECT 'E' AS Packer, 30 AS Plant, s.Drug, s.Quantity AS Plan, s.Batch, s.Month, COALESCE(g.SumAmount, 0) AS Delivered, COALESCE(s.Quantity, 0) - COALESCE(g.SumAmount, 0) AS Remaining, s.VM, s.Raw Material, s.Note
FROM "Plan E November 2026" s
LEFT JOIN GP_ALL g ON g.Packer = 'E' AND fold(s.Drug) = fold(g.Drug) AND s.Batch = g.Party
UNION ALL
SELECT 'Ж' AS Packer, 30 AS Plant, s.Drug, s.Quantity AS Plan, s.Batch, s.Month, COALESCE(g.SumAmount, 0) AS Delivered, COALESCE(s.Quantity, 0) - COALESCE(g.SumAmount, 0) AS Remaining, s.VM, s.Raw Material, s.Note
FROM "Plan Ж November 2026" s
LEFT JOIN GP_ALL g ON g.Packer = 'Ж' AND fold(s.Drug) = fold(g.Drug) AND s.Batch = g.Batch;

-- 3. Fact: plan × norms. Rows without a found norm are NOT lost (norm 0, note)

CREATE TEMP TABLE FACT AS
SELECT IIF(p.Packer = 'Z', 'Report Z', 'Main') AS Report
       p.Packer, p. Factory, p. Preparation, p. Month, p. Batch, p. Plan, p. Delivered, p.Left,
       COALESCE(s.ShortTextOfObject, '(no norm found)') AS Component,
       COALESCE(s."Norm per 1 pc", 0) AS "Norm per 1 pc",
       IIF(COALESCE(p.Left, 0) > 0, COALESCE(p.Left, 0) * COALESCE(s."Norm per 1 pc", 0), 0) AS Needed
       p.VM, p.Raw Material, p.Note,
       (SELECT w.Description FROM "Preparations - description of type and purpose of use" w
         WHERE fold(p.Preparation) LIKE fold('%' || w.NameOfPreparation || '%') LIMIT 1) AS Description
FROM PLAN_ALL p
LEFT JOIN (SELECT DISTINCT Factory, "Material Name", Short Text of Object, "Standard per 1 unit" FROM "Standards for SI") s
       ON fold(p.Drug) = fold(s."Material Name") AND s.Factory = p.Factory;

-- 4. Warehouse snapshots: one value per component (without line‑by‑line replication)

CREATE TEMP TABLE UNISK AS
SELECT 'H' AS Packer, "Name of material", TotaLsaldo FROM "Warehouse 10 dated 11/01/2026"
UNION ALL SELECT 'A' AS Packer, "Name of material", TotaLsaldo FROM "Warehouse A 11/01/2026"
UNION ALL SELECT 'B' AS Packer, "Name of material", TotaLsaldo FROM "Warehouse B 11/01/2026"
UNION ALL SELECT 'B' AS Packer, "Name of material", TotaLsaldo FROM "Warehouse ON 11/01/2026"
UNION ALL SELECT 'D' AS Packer, "Name of material", TotaLsaldo FROM "Warehouse ON 11/01/2026"
UNION ALL SELECT 'D' AS Packer, "Name of material", TotaLsaldo FROM "Warehouse D 11/01/2026"
UNION ALL SELECT 'E' AS Packer, "Material name", Total amount FROM "Warehouse E 11/01/2026"
UNION ALL SELECT 'W' AS Packer, "Material name", Total amount FROM "Warehouse W 11/01/2026";

CREATE TEMP TABLE SK_FAS AS
SELECT Packer, "Material Name", SUM(TotalBalance) AS Balance
FROM UNISK GROUP BY Packer, "Material Name";

CREATE TEMP TABLE SK_CS AS
SELECT "Material Name", SUM(TotalBalance) AS Balance
FROM "CS Warehouse 01.11.2026" GROUP BY "Material Name";

CREATE TEMP TABLE SK_PF AS
SELECT "Material Name", SUM(TotalBalance) AS Balance
FROM "Warehouse 113 dated 01.11.2026" GROUP BY "Material Name";

-- 5. Total requirement by (packer, component): one aggregate instead of self-joins (Cartesian product)

CREATE TEMP TABLE AGG_KF AS
SELECT Report, Packer, Component, SUM(Need) AS Need_Total, COUNT(*) AS Rows
FROM FACT GROUP BY Report, Packer, Component;

-- 6. Packer balance by component (one row per pair)

CREATE TEMP TABLE DEF_KF AS
SELECT k.Report, k.Packer, k.Component, k.Need_Total, k.Lines,
       COALESCE(sk.Balance, 0) AS "Packer warehouse",
       COALESCE(sk.Balance, 0) - k.Need_Total AS "Packer Balance"
FROM AGG_KF k
LEFT JOIN SK_FAS sk ON k.Packer = sk.Packer AND fold(k.Component) = fold(sk."Material Name");

-- 7. Total deficit by component, CS warehouse, and "CS Total" (one row per component)

CREATE TEMP TABLE DEF_K AS
SELECT Report, Component, SUM(MIN("Filler Balance", 0)) AS Deficit_Total
FROM DEF_KF GROUP BY Report, Component;

CREATE TEMP TABLE CS_K AS
SELECT d.Report, d.Component,
       COALESCE(cs.Balance, 0) AS CS,
       COALESCE(cs.Balance, 0) + COALESCE(dk.Deficit_Obsh, 0) AS "Total CS"
FROM (SELECT DISTINCT Report, Component FROM DEF_KF) d
LEFT JOIN SK_CS cs ON fold(d.Component) = fold(cs."Material Name")
LEFT JOIN DEF_K dk ON dk.Report = d.Report AND fold(dk.Component) = fold(d.Component);

-- 8. Denominator of the distribution: total demand and the number of rows per component (for Kimbell)

CREATE TEMP TABLE AGG_K AS
SELECT Report, Component, SUM(Need) AS Need_Total, COUNT(*) AS Lines_Total
FROM FACT GROUP BY Report, Component;

-- 9. Final table for OLAP. Grain: Report × Packer × Component × Drug × Month × Batch

CREATE TEMP TABLE OLAP_DEFICIT AS
SELECT f.Report, f.Packer, f.Factory, f.Component, f.Drug,
       f.Month AS “Production Period”, f. Batch
       f.Description, f.VM, f.Raw materials, f.Note, f."Norm per 1 unit",
       f.Plan, f.Delivered AS "Delivered finished product", f.Remaining AS "Remaining finished product",
       f.Need AS "Requirement",
       dk.Need_Total AS "Total requirement",
       dk."Packer's warehouse", dk."Packer's Remainder",
       ck.CS AS "CS Remainder", ck."Total CS",
       -- Distribution by lines (Kimbell): the share of the line in the component's requirement
       CASE WHEN dk."Packer's Remainder" < 0 AND dk.Required_Total > 0 AND f.Required > 0
            THEN dk."Packer's Remainder" * f.Required / dk.Required_Total
            WHEN dk.“Packer’s Remainder” < 0
            THEN dk.“Packer’s Remainder” / dk.Rows ELSE 0 END AS “Deficit (distribution)”,
       CASE WHEN ck.CS IS NOT NULL AND ak.Need_Total > 0 AND f.Need > 0
            THEN ck.CS * f.Need / ak.Need_Total
            ELSE COALESCE(ck.ЦС, 0) / ak.Строк_Общ END AS "ЦС (распр.)",
       CASE WHEN ck."Итого ЦС" IS NOT NULL AND ak.Нужно_Общ > 0 AND f.Нужно > 0
            THEN ck."Итого ЦС" * f.Нужно / ak.Нужно_Общ
            ELSE COALESCE(ck."Total CS", 0) / ak.Rows_Total END AS "Total CS (distrib.)"
FROM FACT f
LEFT JOIN DEF_KF dk ON f.Report = dk.Report AND f.Packer = dk.Packer AND fold(f.Component) = fold(dk.Component)
LEFT JOIN CS_K ck   ON f.Report = ck.Report AND fold(f.Component) = fold(ck.Component)
LEFT JOIN AGG_K ak ON f.Report = ak.Report AND fold(f.Component) = fold(ak.Component);

SELECT * FROM OLAP_DEFICIT;
```
</details>
