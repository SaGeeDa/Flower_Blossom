.. ============================================================
   Technical Debt Register & Assessment
   Flower_Blossom Project
   ============================================================

.. |project| replace:: Flower_Blossom
.. |repo|    replace:: https://github.com/SaGeeDa/Flower_Blossom

=====================================
Technical Debt Register & Assessment
=====================================

.. meta::
   :description: Technical debt identification, scoring, and remediation plan for the Flower_Blossom project.
   :keywords: technical debt, code quality, refactoring, maintainability

.. contents:: Table of Contents
   :depth: 3
   :local:
   :backlinks: none

----

Document Control
================

.. list-table::
   :widths: 25 75
   :header-rows: 0

   * - **Project**
     - |project|
   * - **Repository**
     - |repo|
   * - **Document Version**
     - 1.0.0
   * - **Created**
     - 2026-05-25
   * - **Last Reviewed**
     - 2026-05-25
   * - **Owner**
     - SaGeeDa
   * - **Review Cycle**
     - Monthly (or after each sprint)

----

1. Purpose & Scope
==================

This document serves as the authoritative register for all **identified technical debt**
in the |project| repository. It provides:

* A structured inventory of every debt item.
* A reproducible scoring methodology (Impact × Effort).
* Clear ownership, target dates, and remediation guidance.
* Progress tracking to be updated each sprint.

**Scope**

The scope covers all source files currently tracked under the repository, including:

* ``index.html`` — front-end markup, inline styles, and inline JavaScript.
* ``README.md`` — documentation completeness and accuracy.
* ``.github/workflows/`` — CI/CD pipeline reliability and maintainability.

----

2. Definitions
==============

.. glossary::

   Technical Debt
      The implied cost of additional rework caused by choosing an easy (limited)
      solution now instead of using a better approach that would take longer.

   Debt Item
      A single, atomic piece of technical debt with a unique identifier, owner,
      severity, and remediation action.

   Impact Score
      A 1–5 rating of how severely the debt affects quality, security,
      maintainability, or user experience if left unaddressed.

      * **5 — Critical** : Security vulnerability or data-loss risk; fix immediately.
      * **4 — High**     : Blocks features or degrades reliability significantly.
      * **3 — Medium**   : Causes repeated friction; slows development.
      * **2 — Low**      : Minor quality issue; noticeable but manageable.
      * **1 — Negligible**: Cosmetic or style concern only.

   Effort Score
      A 1–5 rating of the estimated work required to remediate the debt item.

      * **1 — Trivial**  : < 30 minutes; one-liner fix.
      * **2 — Small**    : 30 min – 2 hours; isolated change.
      * **3 — Medium**   : Half-day; touches multiple files.
      * **4 — Large**    : 1–2 days; requires planning.
      * **5 — Epic**     : > 2 days; may need dedicated sprint.

   Priority Score
      Calculated as ``Impact × (6 − Effort)``; higher score → fix sooner.
      This formula rewards high-impact, low-effort items.

   Status
      One of: ``Open``, ``In Progress``, ``Resolved``, ``Accepted (Won't Fix)``.

----

3. Scoring Methodology
======================

3.1 Scoring Formula
-------------------

.. code-block:: text

   Priority = Impact × (6 - Effort)

   Range : 1 (low priority) → 25 (highest priority)

3.2 Priority Bands
------------------

.. list-table:: Priority Bands
   :widths: 20 20 60
   :header-rows: 1

   * - Score Range
     - Band
     - Recommended Action
   * - 20 – 25
     - 🔴 Critical
     - Fix within current sprint; block merge if applicable.
   * - 12 – 19
     - 🟠 High
     - Schedule in next sprint; do not let it age.
   * - 6  – 11
     - 🟡 Medium
     - Add to backlog; address within 2 sprints.
   * - 1  –  5
     - 🟢 Low
     - Track only; fix opportunistically.

3.3 Re-Assessment Triggers
--------------------------

Re-assess a debt item's scores when any of the following occur:

* A related dependency is updated.
* The affected code is touched during a sprint.
* A new security advisory is published for a component.
* The item has been open for more than 60 days with no change.

----

4. Debt Inventory
=================

.. note::

   Each item is assigned a unique ID in the format ``TD-NNN``.
   Columns: **ID · Category · Title · File(s) · Impact · Effort · Priority · Status · Owner · Target Date**.

4.1 Security Debt
-----------------

.. list-table::
   :widths: 8 14 32 18 8 8 8 10 14 14
   :header-rows: 1

   * - ID
     - Category
     - Title
     - File(s)
     - Impact
     - Effort
     - Priority
     - Status
     - Owner
     - Target Date
   * - TD-001
     - Security
     - Hardcoded local file path exposed in ``src`` attribute (``C:\Users\WGE2KOR\Documents\…``)
     - ``index.html:66``
     - 4
     - 1
     - 20
     - Open
     - SaGeeDa
     - 2026-06-01
   * - TD-002
     - Security
     - External audio ``src`` pointing to JioSaavn (potential mixed-content / CORS risk)
     - ``index.html:75``
     - 3
     - 2
     - 12
     - Open
     - SaGeeDa
     - 2026-06-15
   * - TD-003
     - Security
     - Placeholder images from ``via.placeholder.com`` (third-party dependency, no SRI)
     - ``index.html:67-68``
     - 2
     - 1
     - 10
     - Open
     - SaGeeDa
     - 2026-07-01

4.2 Code Quality Debt
---------------------

.. list-table::
   :widths: 8 14 32 18 8 8 8 10 14 14
   :header-rows: 1

   * - ID
     - Category
     - Title
     - File(s)
     - Impact
     - Effort
     - Priority
     - Status
     - Owner
     - Target Date
   * - TD-004
     - Code Quality
     - Inline ``<style>`` block should be extracted to an external CSS file
     - ``index.html:7-25``
     - 3
     - 2
     - 12
     - Open
     - SaGeeDa
     - 2026-06-15
   * - TD-005
     - Code Quality
     - Inline ``<script>`` block should be extracted to an external JS file
     - ``index.html:93-96``
     - 3
     - 2
     - 12
     - Open
     - SaGeeDa
     - 2026-06-15
   * - TD-006
     - Code Quality
     - Broken ``<img>`` ``src`` with mismatched double-quotes (malformed attribute)
     - ``index.html:66``
     - 4
     - 1
     - 20
     - Open
     - SaGeeDa
     - 2026-06-01
   * - TD-007
     - Code Quality
     - Missing ``alt`` attribute on first ``<img>`` tag (accessibility + SEO)
     - ``index.html:66``
     - 3
     - 1
     - 15
     - Open
     - SaGeeDa
     - 2026-06-01
   * - TD-008
     - Code Quality
     - No ``<meta name="description">`` tag present for SEO
     - ``index.html``
     - 2
     - 1
     - 10
     - Open
     - SaGeeDa
     - 2026-07-01

4.3 Maintainability Debt
------------------------

.. list-table::
   :widths: 8 14 32 18 8 8 8 10 14 14
   :header-rows: 1

   * - ID
     - Category
     - Title
     - File(s)
     - Impact
     - Effort
     - Priority
     - Status
     - Owner
     - Target Date
   * - TD-009
     - Maintainability
     - No ``package.json`` / build tooling; no reproducible dependency management
     - ``/``
     - 3
     - 3
     - 9
     - Open
     - SaGeeDa
     - 2026-07-15
   * - TD-010
     - Maintainability
     - No ``.editorconfig`` or ``prettier`` config; inconsistent formatting possible
     - ``/``
     - 2
     - 1
     - 10
     - Open
     - SaGeeDa
     - 2026-07-01
   * - TD-011
     - Maintainability
     - Footer comment instructs to "remove it after 24 hours" — dead instruction left in code
     - ``index.html:89``
     - 1
     - 1
     - 5
     - Open
     - SaGeeDa
     - 2026-07-15
   * - TD-012
     - Maintainability
     - ``README.md`` contains only one line; no setup, deploy, or usage instructions
     - ``README.md``
     - 2
     - 2
     - 8
     - Open
     - SaGeeDa
     - 2026-07-15

4.4 Accessibility Debt
----------------------

.. list-table::
   :widths: 8 14 32 18 8 8 8 10 14 14
   :header-rows: 1

   * - ID
     - Category
     - Title
     - File(s)
     - Impact
     - Effort
     - Priority
     - Status
     - Owner
     - Target Date
   * - TD-013
     - Accessibility
     - ``<audio controls>`` has no accessible label / ``<figcaption>``
     - ``index.html:75``
     - 3
     - 1
     - 15
     - Open
     - SaGeeDa
     - 2026-06-15
   * - TD-014
     - Accessibility
     - Button ``id="btn"`` lacks descriptive ``aria-label``
     - ``index.html:81``
     - 2
     - 1
     - 10
     - Open
     - SaGeeDa
     - 2026-06-15
   * - TD-015
     - Accessibility
     - ``<div class="logo">`` used as decorative logo; should use ``<img>`` or ``role`` attribute
     - ``index.html:30``
     - 2
     - 2
     - 8
     - Open
     - SaGeeDa
     - 2026-07-01

4.5 CI/CD & Process Debt
------------------------

.. list-table::
   :widths: 8 14 32 18 8 8 8 10 14 14
   :header-rows: 1

   * - ID
     - Category
     - Title
     - File(s)
     - Impact
     - Effort
     - Priority
     - Status
     - Owner
     - Target Date
   * - TD-016
     - CI/CD
     - No CI pipeline existed before this audit; no automated quality gate on PRs
     - ``.github/``
     - 4
     - 3
     - 12
     - Resolved
     - SaGeeDa
     - 2026-05-25
   * - TD-017
     - CI/CD
     - No branch protection rules set on ``main`` (direct push allowed)
     - GitHub Settings
     - 3
     - 1
     - 15
     - Open
     - SaGeeDa
     - 2026-06-01
   * - TD-018
     - CI/CD
     - No ``CODEOWNERS`` file; review responsibilities undefined
     - ``/``
     - 2
     - 1
     - 10
     - Open
     - SaGeeDa
     - 2026-06-15

----

5. Prioritised Remediation Roadmap
====================================

The table below orders all **Open** items by Priority Score (descending).

.. list-table:: Prioritised Open Items
   :widths: 10 12 45 10 13
   :header-rows: 1

   * - Priority
     - ID
     - Title
     - Score
     - Sprint Target
   * - 🔴 Critical
     - TD-001
     - Hardcoded local file path in ``src`` attribute
     - 20
     - Sprint 1
   * - 🔴 Critical
     - TD-006
     - Broken ``<img>`` ``src`` with malformed double-quotes
     - 20
     - Sprint 1
   * - 🟠 High
     - TD-007
     - Missing ``alt`` attribute on first ``<img>``
     - 15
     - Sprint 1
   * - 🟠 High
     - TD-013
     - ``<audio>`` has no accessible label
     - 15
     - Sprint 1
   * - 🟠 High
     - TD-017
     - No branch protection on ``main``
     - 15
     - Sprint 1
   * - 🟠 High
     - TD-002
     - External audio ``src`` — mixed-content / CORS risk
     - 12
     - Sprint 2
   * - 🟠 High
     - TD-004
     - Inline ``<style>`` should be extracted to external CSS
     - 12
     - Sprint 2
   * - 🟠 High
     - TD-005
     - Inline ``<script>`` should be extracted to external JS
     - 12
     - Sprint 2
   * - 🟠 High
     - TD-016
     - No CI pipeline (now Resolved)
     - 12
     - ✅ Done
   * - 🟡 Medium
     - TD-003
     - Placeholder images from ``via.placeholder.com`` (no SRI)
     - 10
     - Sprint 3
   * - 🟡 Medium
     - TD-008
     - No ``<meta name="description">`` for SEO
     - 10
     - Sprint 3
   * - 🟡 Medium
     - TD-010
     - No ``.editorconfig`` / ``prettier`` config
     - 10
     - Sprint 3
   * - 🟡 Medium
     - TD-014
     - Button lacks ``aria-label``
     - 10
     - Sprint 3
   * - 🟡 Medium
     - TD-018
     - No ``CODEOWNERS`` file
     - 10
     - Sprint 3
   * - 🟡 Medium
     - TD-009
     - No ``package.json`` / build tooling
     - 9
     - Sprint 4
   * - 🟡 Medium
     - TD-012
     - ``README.md`` minimal / no setup docs
     - 8
     - Sprint 4
   * - 🟡 Medium
     - TD-015
     - ``<div class="logo">`` missing ``role`` or ``<img>``
     - 8
     - Sprint 4
   * - 🟢 Low
     - TD-011
     - Stale "remove after 24 hours" comment in footer
     - 5
     - Opportunistic

----

6. Sprint-by-Sprint Action Plan
================================

Sprint 1 — Immediate Fixes (≤ 1 week)
---------------------------------------

.. code-block:: text

   Goal: Eliminate security & broken-markup issues.

   TD-001  Replace hardcoded ``C:\...`` path with a hosted image URL or a relative asset.
   TD-006  Fix the malformed double-quote in the <img> src attribute.
   TD-007  Add descriptive alt="..." to the first <img> tag.
   TD-013  Wrap <audio> in <figure> and add <figcaption> or aria-label.
   TD-017  Enable branch protection on main (require PR + 1 approver + CI pass).

Sprint 2 — Code Structure (1–2 weeks)
---------------------------------------

.. code-block:: text

   Goal: Separate concerns; improve maintainability.

   TD-002  Self-host the audio file (or use a CORS-safe streaming source).
   TD-004  Extract inline <style> → styles/main.css and <link> it.
   TD-005  Extract inline <script> → scripts/main.js and <script src> it.

Sprint 3 — Quality & Process Polish (2–4 weeks)
-------------------------------------------------

.. code-block:: text

   Goal: Harden quality gates and developer experience.

   TD-003  Replace placeholder images with real hosted assets.
   TD-008  Add <meta name="description" content="..."> to <head>.
   TD-010  Add .editorconfig and/or .prettierrc for consistent formatting.
   TD-014  Add aria-label="Reveal surprise" to #btn button.
   TD-018  Create CODEOWNERS file assigning review responsibilities.

Sprint 4 — Long-term Maintainability (1 month)
------------------------------------------------

.. code-block:: text

   Goal: Add build tooling and improve documentation.

   TD-009  Introduce package.json, npm scripts, and optional bundler (Vite / Parcel).
   TD-012  Expand README.md with setup, deployment, and contribution guide.
   TD-015  Replace <div class="logo"> with a proper <img> or add role="img" + aria-label.

Opportunistic (no fixed sprint)
--------------------------------

.. code-block:: text

   TD-011  Remove or update the stale "Remove it after 24 hours" footer comment.

----

7. Debt Metrics & Trend Tracking
==================================

Update this section after each sprint review.

.. list-table:: Sprint-by-Sprint Debt Metrics
   :widths: 15 12 12 12 12 12 12
   :header-rows: 1

   * - Sprint / Date
     - Total Items
     - Critical 🔴
     - High 🟠
     - Medium 🟡
     - Low 🟢
     - Resolved ✅
   * - Baseline 2026-05-25
     - 18
     - 2
     - 7
     - 7
     - 1
     - 1
   * - Sprint 1 (planned)
     - —
     - 0
     - —
     - —
     - —
     - +5
   * - Sprint 2 (planned)
     - —
     - 0
     - 0
     - —
     - —
     - +3
   * - Sprint 3 (planned)
     - —
     - 0
     - 0
     - 0
     - —
     - +5
   * - Sprint 4 (planned)
     - —
     - 0
     - 0
     - 0
     - 0
     - +3

----

8. Accepted / Won't-Fix Items
================================

Items in this section have been deliberately accepted with justification.
They are **not** to be re-opened unless the risk profile changes.

.. list-table::
   :widths: 10 40 50
   :header-rows: 1

   * - ID
     - Title
     - Acceptance Rationale
   * - *(none yet)*
     - —
     - —

----

9. Review & Approval History
==============================

.. list-table::
   :widths: 20 20 25 35
   :header-rows: 1

   * - Version
     - Date
     - Reviewer
     - Changes
   * - 1.0.0
     - 2026-05-25
     - SaGeeDa
     - Initial document; baseline debt captured from automated audit.

----

10. References
===============

* `GitHub Actions Documentation <https://docs.github.com/en/actions>`_
* `HTMLHint Rules <https://htmlhint.com/docs/user-guide/list-rules>`_
* `ESLint Complexity Rule <https://eslint.org/docs/rules/complexity>`_
* `axe-core Accessibility Rules <https://dequeuniversity.com/rules/axe/>`_
* `OWASP Top 10 <https://owasp.org/www-project-top-ten/>`_
* `reStructuredText Specification <https://docutils.sourceforge.io/rst.html>`_

----

.. note::

   This document is auto-generated from the findings of the
   ``Technical Debt Audit`` GitHub Actions workflow
   (``.github/workflows/technical_debt_audit.yml``).
   Run the workflow and update the tables above after each execution.

.. |date| date::
.. footer::

   Last built: |date|
