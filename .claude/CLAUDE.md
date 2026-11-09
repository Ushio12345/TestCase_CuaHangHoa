Manual QA repo (no application code). All deliverables are written in Vietnamese.
General rules (Planning, Sync, Constraints) live in `~/.claude/CLAUDE.md`; below are project-specific rules only.

## Inputs (read yourself, do not ask the user)

| Source | What |
|---|---|
| `docs/SRS_Web_ban_hoa_v2.docx` (read with `textutil -convert txt -stdout`) | Function section, permission matrix, DB table, message list, validation rules table, intentional-bug appendix |
| `docs/srs-review.md`, `docs/test-plan.md` | Known SRS issues, scope, environment, Priority |
| Root `README.md` | Function number, name, URL → module folder `modules/NN-<slug>/` |
| `modules/NN-*/qa-log.md`, `test-design.md`, `test-cases.xlsx` | Current state of the module |
| `.claude/templates/` | Empty templates for a new module |

- Ask the user only for BA/PO answers.
- `modules/01-gio-hang/test-cases.xlsx` is the **old format**: do not use it as a template.

## New module workflow

Trigger: "Làm module NN" / "Làm chức năng <tên>". Goal: one request → full module, no repeated calls.

1. **Read all inputs** above.
2. **One plan for the whole module**: `.claude/review/YYYYMMDD_HHmm_module_NN.md`, sections:
   SRS Review (new findings) · qa-log questions · Init files · Test Design (6 parts) · Test Case (estimate) · Sync.
   Changes discovered later in the same module → append to a **"Bổ sung"** section of that plan; no new plan file.
3. **Gates (only stops):** (a) plan approval; (b) a ❓ question blocks Expected Result → stop and wait for BA/PO answers.
   Otherwise run every step to the end.
4. **Steps and required output:**

| Step | Required output |
|---|---|
| Init | Copy `.claude/templates/` → `modules/NN-<slug>/` (README.md, qa-log.md, test-design.md, test-cases.xlsx), fill function name / URL; root README row: link + 🟡 |
| SRS Review | New rows in `docs/srs-review.md`; ❓ questions in `qa-log.md` (see "SRS Review") |
| Test Design | `test-design.md` meets "Done when" (see "Test Design"). No `.xmind` |
| Test Case | `test-cases.xlsx` per template; every node covered by ≥ 1 TC; sheet Tổng hợp filled |
| Sync | Module README (rules, TC stats) + root README (TC count, status) |

5. **Before finishing**, re-check each row of the table above; report anything not done.

### qa-log numbering

`#` only increases: never insert in the middle, never renumber. New questions go at the end
(add a section "Bổ sung …" if needed). When answered, edit the row in place.

### Tools

- `.xlsx`: Python `openpyxl` in a venv under the scratchpad (never install system-wide).
- No `.xmind` for new modules; `test-design.md` is the mindmap.

## Execution

- Workflow: SRS → Q&A → Test Design → Test Case → Execute → Bug Report.
- Expected Result must come from the SRS or a confirmed (✅) answer in `qa-log.md`.
  If unclear: mark `[Cần xác nhận BA/PO]` and add a ❓ question to `qa-log.md`.
- Priority: see "Manual QA" in `~/.claude/CLAUDE.md` (same as `docs/test-plan.md`).

## SRS Review

Read every requirement of the function carefully (flow steps, field tables, business rules, error codes,
DB schema, appendix) and cross-check them against each other. Report every point that is:

| Type                      | What to look for                                                                                                          | Example                                                    |
| ------------------------- | ------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------- |
| Mơ hồ (ambiguous)         | Missing value, limit, format, error message, or behavior; vague words ("hợp lệ", "phù hợp", "nhanh"); undefined edge case | Nhập số lượng 0 / âm / > max xử lý thế nào?                |
| Mâu thuẫn (contradiction) | Two places in the SRS say different things                                                                                | Mã lỗi để trống `ten_dn`: Đăng ký = FC_01, Phụ lục = FC_02 |
| Sai lệch (deviation)      | SRS vs UI vs DB vs BA/PO answer vs actual app do not match                                                                | UI `email` tối đa 50 ký tự, DB VARCHAR(100)                |
| Thiếu (missing)           | Referenced item not defined, field with no storage column, function with no screen/API                                    | BR-01, BR-02 không được định nghĩa                         |

Checklist per function:

- Each input field: required?, type, min/max length, format, default value, error code + message.
- Each action: precondition, steps, success result, failure result, redirect target.
- Each actor: allowed / blocked, and how blocked.
- Numbers and IDs (error codes, BR-xx, URLs, table/column names) match across all sections.
- Data flow: every UI field has a DB column with a compatible type and length.

Output:

- Contradictions / deviations / missing → add rows to `docs/srs-review.md` (keep its table format and running `#`),
  with exact location (section, field, code) and the conflicting values side by side.
- Ambiguities that affect Expected Result → add as ❓ questions to the module's `qa-log.md`.
- Do not list the intentional bugs in the SRS appendix as SRS issues.
- Never resolve an issue by guessing; state the issue and ask.

## Test Design

Reference: `modules/01-gio-hang/test-design.md`.

### Plan (save to `.claude/review/` before writing)

1. **Scope:** function name, URL, actors (Guest · Member · Admin), related functions.
2. **Business rules:** list each rule with its source (SRS section or `qa-log.md` #).
3. **Open questions:** ❓ items that block Expected Result → add to `qa-log.md`.
4. **Intentional bugs:** SRS appendix bugs that touch this function (note "đối chiếu lỗi cố ý số N").
5. **Outline:** the 5 groups below with planned level-2/level-3 nodes and the technique used per node.
6. **Estimate:** rough number of nodes / test cases per group.

### Structure (`test-design.md`, title = function name)

| Group      | Content                                                                                                                                                                                          | Technique                                      |
| ---------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ---------------------------------------------- |
| Function   | Main flows per sub-feature (view, add, update, delete…), navigation in/out, data persistence                                                                                                     | State Transition, Decision Table               |
| Validation | Every input / limit: valid, invalid, empty, whitespace, type, format, paste                                                                                                                      | EP + BVA: min−1, min, min+1, max−1, max, max+1 |
| UI         | Default state (empty / with data), each field (read-only / editable, format), buttons (enable/disable), messages, layout, behavior (tab, hover, scroll), responsive (tablet 768px, mobile 375px) | Checklist                                      |
| Phân quyền | Per actor: allowed actions, blocked actions + how blocked (hide / redirect / message), access to other users' data (UI and API)                                                                  | Decision Table                                 |
| Ảnh hưởng  | Upstream / downstream functions, data changed by Admin (hide, delete, edit price/name), duplicates, post-action state                                                                            | Error Guessing                                 |

### Node rules

- One node = one verifiable condition; write it as `Condition → Expected result` when the result is not obvious.
- Use numbers from confirmed rules (e.g. `= 99 (max)`, `= 100 (max + 1)`), not vague wording.
- Cover Positive / Negative / Boundary / Exception in every group that applies.
- Unconfirmed behavior: keep the node and append `[Cần xác nhận BA/PO]`.
- Group similar cases under a shared parent (e.g. `Giỏ hàng có nhiều sản phẩm` → `≤ 10` / `11 – 20`).

### Done when

- Every confirmed rule in `qa-log.md` maps to at least one node.
- Every ❓ question has a matching `[Cần xác nhận BA/PO]` node.
- If the module already has a `.xmind` (01, 12): `test-design.md` matches it.

## Test Case

Reference: `.claude/templates/test-cases.xlsx` (not module 01 – old format). One TC per Test Design node (or a small group of related nodes).
How to write each field (ID, Title, Pre-conditions, Steps, Expected, Test Datas), Impact, Priority:
see "Manual QA" in `~/.claude/CLAUDE.md`. Below is this project's template only.

### Template (sheet "Test Case")

**Row layout**

| Row  | Content                                                                                  |
| ---- | ---------------------------------------------------------------------------------------- |
| 1    | `TÍNH NĂNG: <Tên chức năng>` – dark blue, bold, large                                    |
| 2    | A: `Build Version:` (bold) · B: `vX.Y.Z`                                                 |
| 3    | Empty                                                                                    |
| 4    | Summary header: B `High` · C `Medium` · D `Low` · E `Total`                              |
| 5–10 | A: `Total` (bold) / `Passed` / `Failed` / `Untested` / `Accepted` / `N/A`; B–E: formulas |
| 11   | Empty                                                                                    |
| 12   | Test case column header (ID → Notes)                                                     |
| 13+  | Data: group row → scenario row → TC rows                                                 |

Counts are formulas (COUNTIFS on Priority × R1 Results), not typed numbers.

**Formatting**

| Area                    | Format                                                                                                                  |
| ----------------------- | ----------------------------------------------------------------------------------------------------------------------- |
| Header rows 4 and 12    | Dark blue fill, white bold text, centered                                                                               |
| Summary table           | Thin borders, numbers centered; `Total` row and `Total` column bold                                                     |
| Group row (`Function`…) | Light purple fill, dark blue bold text, merged across all columns                                                       |
| Scenario row            | Light blue fill, dark blue text, merged across all columns                                                              |
| TC rows                 | Thin borders, wrap text, top-aligned                                                                                    |
| Priority cell           | Conditional fill by level, one distinct light color each (e.g. HIGH light orange, MEDIUM light yellow, LOW light green) |

**Columns**

| Column             | Content                                                                                                  |
| ------------------ | -------------------------------------------------------------------------------------------------------- |
| ID                 | `TC_01`, `TC_02`… running across the whole sheet                                                         |
| Test case Title    | Starts with "Kiểm tra …", one condition, ends with "." (global rule)                                     |
| Pre-conditions     | Numbered: quyền · data test · vị trí màn hình (global rule)                                               |
| Test Steps         | Numbered; adverbial phrases may merge simple actions (global rule)                                       |
| Test Datas         | Named data (`SP1: 150.000đ`, `Thành viên A`), URL, input values                                          |
| Expected result    | Numbered by step; last step required (global rule); exact values (số lượng, tiền, message, redirect)     |
| Test Environment   | e.g. `Web Chrome (desktop) – <URL>`                                                                      |
| Priority           | HIGH / MEDIUM / LOW (see Priority rule)                                                                  |
| Query Data         | SQL to verify DB after the action (if applicable)                                                        |
| Actual Result      | Filled at execution                                                                                      |
| R1 Results         | Passed / Failed / Untested / Accepted / N/A                                                              |
| <Platform> Results | Extra result column per extra platform (e.g. Android Results); omit if web only                          |
| BugID              | Bug ID from `bug-reports/bug-list.xlsx` when Failed                                                      |
| Notes              | Source of Expected Result (`BA/PO confirm: …`, SRS section), `[Cần xác nhận BA/PO]`, intentional bug ref |

**Rows**

- Group row = Test Design group (`Function`, `Validation`, `UI`, `Phân quyền`, `Ảnh hưởng`).
- Scenario row = sentence describing the main scenario under the group
  (e.g. `Update Account nhóm tài khoản thành công khi thực hiện thêm thành viên vào nhóm`).
- TC rows under each scenario.

### Other sheets

- **Tổng hợp:** per scenario: Số TC, HIGH, MEDIUM, LOW, Pass / Fail / Untested (R1).
- **Test Data & Hướng dẫn:** test data to prepare (named items) and confirmed BA/PO rules. No passwords.

### Writing rules

- Each TC is independent: Pre-conditions fully set up the state it needs.
- Expected Result is concrete and checkable; no "hiển thị đúng" without saying what is correct.
- New TCs start as `Untested`.

## Sync

After a deliverable changes, update: module README (TC stats, results, bugs)
and root README (progress table, total TC, summary).
If a `.xmind` exists, keep `test-design.md` in sync with it.
