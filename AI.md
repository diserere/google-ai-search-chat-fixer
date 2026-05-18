# AI-Driven Development & QA Guidelines

This document defines the strict workflow, code style, and engineering standards for any AI Assistant contributing to this project. Read this file before writing any code or proposing changes.

## 1. Project Context & Tech Stack
- **Project Type**: UserScript (Tampermonkey / Violentmonkey) for browser automation.
- **Target OS**: Ubuntu Linux (25.10 / 26.04).
- **Environment Constraints**: High-reactivity SPA interfaces (Google AI Studio / Google Search). Native events may be blocked or ignored due to browser security policies (`isTrusted: false`). DOM manipulation and direct injection are preferred for stability.

## 2. Development Cycle & Iteration Policy
- **Atomic Iterations**: Strictly one feature or one bugfix per iteration. Do NOT mix infrastructure changes (e.g., `@match` updates) with business logic fixes in a single response.
- **No Invisible Refactoring**: Do NOT change variable names, indentation, or formatting unless explicitly requested or handled in a separate dedicated cleanup iteration.
- **Mandatory Commits**: Every code block provided by the AI MUST be accompanied by a suggested **Conventional Commit** message. 
  * *Rule*: If the commit message requires the word "and" (e.g., `feat: fix X and change Y`), the code MUST be split into two separate iterations.

## 3. Versioning Policy (SemVer 2.0.0)
The project strictly follows the **MAJOR.MINOR.PATCH** format in the UserScript header metadata:
- **MAJOR**: Architectural changes, complete rewrites, or breaking platform migrations.
- **MINOR**: New features (e.g., supporting a completely new AI platform web interface).
- **PATCH**: Bugfixes, stability improvements, or narrow match adjustments (e.g., updating a broken CSS selector).

## 4. Code Style Guide (Python-Inspired Readability)
To ensure clean Git diffs and readable code, follow these formatting rules:
- **Vertical Object/Event Formatting**: Multi-argument options, large objects, and constructor configurations MUST be formatted as vertical lists (one property per line). Single-line dense bundling is strictly forbidden.
  
  *Bad (Diff-unfriendly)*:
  ```javascript
  const event = new KeyboardEvent('keydown', { key: 'Enter', code: 'Enter', shiftKey: true });
  ```
  
  *Good (Diff-friendly)*:
  ```javascript
  const event = new KeyboardEvent('keydown', {
      key: 'Enter',
      code: 'Enter',
      shiftKey: true,
      bubbles: true,
      cancelable: true
  });
  ```
- **Minimalist Comments**: Do NOT write obvious descriptive comments (e.g., `// check if text box`). Write comments ONLY for non-trivial workarounds or critical architectural constraints (e.g., explaining why a specific browser API bypasses a Google SPA lock). Keep them brief.

## 5. Branching & CLI Workflow (Trunk-Based Development)
The project uses TBD without pull requests. Work is performed in short-lived task branches:
1. `git checkout master && git pull --rebase` (Synchronize)
2. `git checkout -b patch/vX.Y.Z-description` or `git checkout -b feat/vX.Y.Z-description` (Isolate)
3. Direct execution of local testing.
4. Local merge via `git checkout master && git merge branch_name` and immediate pushing.
