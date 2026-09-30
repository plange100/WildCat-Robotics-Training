# README.md 

## 📝 Markdown Style & Formatting Standards

## Step 1. Conventions

To keep our repository documentation clean, readable, and uniform across all pages, follow these conventions:

### A. Document Structure & Headings
* Use a single `# Title` (H1) at the top of each document.
* Use `## Section` (H2) for primary steps or major topics.
* Use `### Subsection` (H3) for granular steps or subtopics.
* Avoid skipping levels (e.g., do not jump from `#` directly to `###`).
* Always leave **one empty blank line** above and below any heading.

### B. Spacing & Section Dividers
* Separate major sections (`##`) with a horizontal rule (`---`).
* **Critical syntax rule:** Always leave a blank line both **above** and **below** `---` to prevent the line above from accidentally rendering as a giant header underline:
  ```markdown
  End of previous section.

---

## Step 2. Next Major Section

### A. Code Blocks & Terminal Commands
* Always specify the language tag after the opening triple backticks (e.g., `bash`, `java`, `json`).
* Use single inline backticks (`like this`) for filenames, commands, key bindings (`Ctrl + S`), and inline code symbols.
* Ensure closing triple backticks are placed on their own dedicated line with no preceding spaces.

### B. Lists & Steps
* Use numbered lists (`1. 2. 3.`) for ordered procedures where sequence matters.
* Use asterisks or hyphens (`*` or `-`) for unordered item lists; keep bullet types consistent within each document.
* Nest sub-bullets with a 2-space or 4-space indentation:
  * Primary item
    * Indented sub-detail
    * Another sub-detail

---

## Step 3. Continuation

### A. Tables
* Use clean Markdown tables for hardware maps (CAN IDs, ports), shortcuts, and comparative references.
* Explicitly declare column alignments in the header divider row:
  * `:---` for Left-aligned (standard text, descriptions)
  * `:---:` for Center-aligned (IDs, status badges, pin numbers)
  * `---:` for Right-aligned (numeric quantities, measurements)

### B. GitHub Callout Alerts
Highlight critical warnings or safety tips using official GitHub blockquote alerts:

> [!NOTE]
> Helpful context, tips, or non-blocking suggestions.

> [!IMPORTANT]
> Key configuration details or required prerequisites.

> [!WARNING]
> Steps where common errors occur (e.g., mismatched emails or CAN IDs).

> [!CAUTION]
> Hardware or benchtop safety hazards (e.g., powered motors or unpropped robots).
>

### C. GitHub Callout Alerts
Highlight critical warnings or safety tips using official GitHub blockquote alerts.

#### How to write them in Markdown:
```text
> [!NOTE]
> Helpful context, tips, or non-blocking suggestions.

> [!IMPORTANT]
> Key configuration details or required prerequisites.

> [!WARNING]
> Steps where common errors occur (e.g., mismatched emails or CAN IDs).

> [!CAUTION]
> Hardware or benchtop safety hazards (e.g., powered motors or unpropped robots)
```

## Flowcharts
Flowcharts made using mermaid.ai