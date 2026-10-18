# 📊 Interactive Database Diagram Guide & Schema Specification

This document provides the full data specification, AI prompt templates, and integration steps for the [`database_diagram.html`](./database_diagram.html) interactive entity-relationship visualizer.

---

## 🎯 Purpose

[`database_diagram.html`](./database_diagram.html) is an interactive, browser-based database schema visualizer designed to replace static ER diagrams. It supports:
- Interactive pan and zoom with foreign-key connection lines
- Table search by table name or column name (<kbd>/</kbd>)
- Rich inspector modal with business descriptions and mock data
- Guided step-by-step user journey tours through database entities
- Zero external dependencies (Vanilla JS, Canvas, SVG, CSS)

---

## 🤖 AI Prompt to Generate Diagram Data

Copy and paste this prompt into your LLM (Claude, ChatGPT, Gemini) along with your SQL DDL or product requirements to instantly generate data for [`database_diagram.html`](./database_diagram.html):

```markdown
You are an expert Database Architect. I need you to generate the JavaScript configuration data for my interactive database diagram tool.

Below are my project requirements / database models:
<PASTE YOUR SQL DDL, PRISMA SCHEMA, OR REQUIREMENTS HERE>

Please generate the following JavaScript variables formatted exactly as shown below:

```javascript
// 1. PROJECT CONFIGURATION
const CONFIG = {
  title: "Your Project Name - Database Architecture",
  subtitle: "X entities, Y relationships • Primary DB Engine",
  defaultTheme: "dark" // "light" or "dark"
};

// 2. DOMAIN GROUPS & COLORS
// Group entities logically (e.g. auth, billing, catalog, logistics).
// Use presets --c-1 through --c-8 and --t-1 through --t-8 for colors.
const GROUPS = {
  users:    { label: "Users & Auth",      c: "--c-1", t: "--t-1" },
  orders:   { label: "Orders & Payments",  c: "--c-2", t: "--t-2" },
  products: { label: "Catalog & Inventory",c: "--c-3", t: "--t-3" }
};

// 3. DATA STORE BADGES
const STORES = {
  pg:    { short: "PG",    label: "PostgreSQL Relational" },
  cache: { short: "REDIS", label: "Redis In-Memory Cache" },
  doc:   { short: "JSON",  label: "Document / Blob Store" }
};

// 4. COLUMN DATA TYPES
const TYPES = {
  int:   ["integer", "INTEGER"],
  str:   ["string", "VARCHAR(255)"],
  float: ["decimal number", "NUMERIC(10,2)"],
  bool:  ["boolean", "BOOLEAN"],
  ts:    ["timestamp", "TIMESTAMP WITH TIME ZONE"],
  text:  ["unbounded text", "TEXT"],
  json:  ["JSON object", "JSONB"]
};

// 5. TABLE DEFINITIONS
// cols format: ["col_name", "type_key", "PK" | "FK:target_table.col" | "", "Description"]
const TABLES = [
  {
    id: "users",
    g: "users",
    s: "pg",
    core: true,
    purpose: "Stores user credentials, profile information, and roles.",
    used: "Authentication, RBAC checks, and foreign key anchor for all user actions.",
    cols: [
      ["id", "int", "PK", "Primary identifier"],
      ["email", "str", "", "Unique verified email address"],
      ["role", "str", "", "User role: ADMIN, CUSTOMER, VENDOR"],
      ["created_at", "ts", "", "Account creation timestamp"]
    ]
  }
];

// 6. SAMPLE DATA
// 1 sample mock record per table for inspector drawer preview
const SAMPLE = {
  users: { id: "1", email: "user@example.com", role: "CUSTOMER", created_at: "2026-01-01 10:00:00" }
};

// 7. GUIDED STORIES
// 1-2 key lifecycle walkthroughs tracing how data flows through tables
const STORIES = {
  checkout: {
    title: "Order Placement Flow",
    steps: [
      ["users", "Customer signs in with verified profile."],
      ["orders", "Customer creates new pending order consignment."]
    ]
  }
};
```

Make sure all Foreign Keys use the syntax "FK:target_table.target_col" so lines are automatically drawn between tables.
```

---

## 📋 Data Specification Reference

### 1. `GROUPS`
Defines logical clusters of tables. Available built-in color pairs:
- `--c-1` / `--t-1` (Teal)
- `--c-2` / `--t-2` (Warm Amber/Brown)
- `--c-3` / `--t-3` (Olive Green)
- `--c-4` / `--t-4` (Golden Yellow)
- `--c-5` / `--t-5` (Coral Red)
- `--c-6` / `--t-6` (Warm Gray)
- `--c-7` / `--t-7` (Steel Blue)
- `--c-8` / `--t-8` (Purple)

### 2. `TABLES`
Each item in `TABLES` requires:
- `id`: Unique name matching database table (e.g. `users`, `orders`).
- `g`: Key of the matching domain in `GROUPS`.
- `s`: Key of the matching data store in `STORES`.
- `core`: `true` or `false`. Core tables have a highlighted badge in the UI.
- `purpose`: 1-sentence explanation of what this table models.
- `used`: Context on how applications query or join this table.
- `cols`: 2D Array of column definitions:
  - Index 0: Column name (string)
  - Index 1: Type alias matching `TYPES` (e.g. `"int"`, `"str"`, `"ts"`, `"json"`)
  - Index 2: Key constraint (`"PK"` for primary key, `"FK:table_name.col_name"` for foreign key, or `""` for normal column)
  - Index 3: Brief description of the column

### 3. `STORIES`
Defines step-by-step guided animations.
- Key: unique ID (e.g., `checkout`, `onboarding`)
- `title`: Display name in the story menu
- `steps`: Array of `["table_id", "Explanation text for this step"]`

---

## 🚀 How to Apply to `database_diagram.html`

1. Open `database_diagram.html` in your text editor.
2. Locate the `<script>` tag (starts around line 311).
3. Replace the `CONFIG`, `GROUPS`, `STORES`, `TYPES`, `TABLES`, `SAMPLE`, and `STORIES` objects with your generated data.
4. Save and open `database_diagram.html` directly in any web browser!
