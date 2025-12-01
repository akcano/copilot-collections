<!-- Guidance for AI agents and contributors who will edit files under `docs/` -->
# Documentation instructions (docs/ only)

Purpose: short, actionable rules for editing, adding or validating content under `docs/`.

- Scope: apply these rules only to files in the `docs/` directory. Do not modify other project docs unless explicitly requested.

- Structure
  - Top-level files: `docs/index.md`, `docs/tutorial.md`, `docs/changelog.md`.
  - Sections: `docs/how-to/`, `docs/reference/`, `docs/explanation/`.
  - Links inside `docs/` use relative paths (examples in `docs/index.md`). Keep link targets relative and update `docs/index.md` Contents when adding/removing pages.

- Style & conventions
  - Use Git-flavoured Markdown with fenced code blocks (```) and command examples as shell blocks.
  - Keep docs imperative and task-focused in `how-to` and `tutorial` pages; keep conceptual explanations in `explanation/`.
  - When documenting runtime behavior or configuration, reference exact symbols or files from the codebase (e.g., `src/charm.py`, `database.py`, `config.yaml`).
  - When describing procedures that depend on the charm runtime (Pebble, Juju, Kubernetes), include the exact commands shown in existing docs (see `docs/tutorial.md`).

- Linting & checks (how to run)
  - Run the docs linters via the top-level Makefile targets: `make docs-check` (this runs `vale` and `lychee`).
  - To regenerate API-style docs for `src/` (if needed): `./generate-src-docs.sh` (produces `src-docs/`).

- Examples & cross-references
  - For operational examples use the same Juju commands as `docs/tutorial.md` (e.g. `juju deploy redis-k8s --channel latest/edge`).
  - When referencing integrations, point to the corresponding `reference/` page (e.g., `docs/reference/integrations.md`).
  - If architecture changes are made, update `docs/explanation/charm-architecture.md` and include references to the changed code (for example `src/charm.py` Pebble layer generation and `lib/charms/*/v0` relation libraries).

- Tests & CI
  - CI expects docs to pass `vale` and `lychee`; address reported issues rather than silencing the tools.

- Small-edit rules for AI agents
  - Preserve existing link targets and code samples formatting. If you change any heading filename or path, update all relative links in `docs/` accordingly.
  - Do not change `docs/index.md` structure without updating the numeric Contents list — keep the order and paths in sync with files under `docs/`.
  - When adding new how-to or reference pages, add a short entry to the appropriate folder's landing page (e.g. `how-to/landing-page.md`) and to `docs/index.md` if it's a top-level content item.

- When to open PR notes
  - If you modify a procedure (commands, required versions, prerequisites), add a short note in `docs/changelog.md` summarizing the user-facing change.

If anything in these instructions is unclear or incomplete, ask for the specific area you want to edit and I will expand the guidance or update this file.
