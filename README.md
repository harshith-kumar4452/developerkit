# Developer Toolkit

A personal developer kit created to store reusable assets, tools, architecture patterns, and prompts to quickly kickstart and support ongoing and future software projects.

---

## 📌 What This Repo Is For

This repository acts as a central toolkit to reuse across different projects. It is intended to collect:
- **Interactive Visualizers**: Tools to quickly map and visualize databases, system flows, and data models.
- **Architectures & Blueprints**: System designs, database schemas, and data structures.
- **AI Prompts**: Tested prompts for generating schemas, designing architectures, writing boilerplate code, and creating API specs.
- **Templates & Boilerplates**: Starter files and configurations for fast project setup.

---

## 📂 Current Contents

Right now, this repository includes:

### 1. `database_diagram.html`
A single-file, interactive database ER (entity-relationship) diagram template that runs directly in any browser with zero dependencies.

**Features:**
- **Interactive Canvas**: Drag to pan, scroll wheel or pinch to zoom, and fit-to-screen (`F`).
- **Relationship Connectors**: Visual SVG lines connecting Foreign Keys (FK) to Primary Keys (PK). Hovering over a column highlights related tables and links.
- **Search**: Press `/` to quickly find tables and columns.
- **Inspector Drawer**: Click any table to inspect column data types, keys, technical notes, and sample row data.
- **Guided Tours**: Built-in step-by-step walkthroughs to follow data lifecycles across related entities.
- **Theme Toggle**: Light and dark mode with state saved in `localStorage`.

### 2. `database_diagram.md`
The companion specification and AI prompt guide for `database_diagram.html`.

**Includes:**
- A ready-to-use prompt you can paste into ChatGPT, Claude, or Gemini to convert any SQL DDL, Prisma schema, or feature list into the exact JavaScript configuration format for `database_diagram.html`.
- Reference for data structures (`TABLES`, `GROUPS`, `STORES`, `TYPES`, `SAMPLE`, `STORIES`) and color presets.

---

## 🚀 How to Use in Your Projects

Whenever you start a new project and need an interactive database diagram:

1. Copy `database_diagram.html` into your project's docs or architecture folder.
2. Open `database_diagram.md` and copy the **AI Prompt**.
3. Paste the prompt along with your project requirements or SQL schema into an AI model (Gemini, Claude, or ChatGPT).
4. Paste the generated JavaScript block into `database_diagram.html` (inside the `<script>` section).
5. Open `database_diagram.html` in your browser to view and present your interactive schema.

---

## 🔮 Future Additions

As new projects are built, this repository will continue to expand with:
- System architecture templates and sequence flow diagrams
- Curated AI prompt collections for backend, frontend, and API design
- Reusable starter templates and project configuration files
