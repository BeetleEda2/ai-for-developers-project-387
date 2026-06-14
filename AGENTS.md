# Project Context

## Project
- Calendar booking app (Design First: API contract in `spec/main.tsp`)
- Stack: TypeSpec → auto-generated types, Express.js backend, React + Mantine frontend, Playwright e2e
- Backend: in-memory storage (resets on restart)
- `opencode.json`: model `opencode/deepseek-v4-flash-free` (free OpenCode Zen)

## OpenCode GitHub Integration
- `.github/workflows/opencode.yml` — triggers on `/oc` or `/opencode` in issue/PR comments
- Uses `anomalyco/opencode/github@latest` action with `model: opencode/deepseek-v4-flash-free`
- Permissions: `contents: write`, `pull-requests: write`, `issues: write`, `id-token: write`
- GITHUB_TOKEN + OPENCODE_API_KEY in env
- `persist-credentials: false` on checkout (avoids Duplicate Authorization header)

## What's Done
1. **Code transferred** from previous repo to project-387
2. **`docs/roadmap.md`** — 3 features + 3 bugs with order
3. **Feature #1 "Cancel booking"** — PR #3 (merged? check)
4. **Triage step** — Issue #4 (vague bug report) → agent explained root cause (groupSlotsByDay without useMemo)
5. **PR #5** — Fix: `groupSlotsByDay` wrapped in `useMemo([slots, tz])`
6. **Review cycle** — 2 review comments (general + line-level) → both addressed in PR #5

## Roadmap (docs/roadmap.md)
1. ✅ Cancel booking (guest self-service) — PR #3
2. ⬜ Отображение слотов в таймзоне гостя
3. ⬜ Страница «Мои бронирования» для гостя
4. ⬜ Bug: не сбрасывается выбранный слот при возврате
5. ⬜ Bug: некорректное сообщение при 409 с Prism
6. ⬜ Bug: отсутствует валидация длины заметок

## Known Issues
- `release-please.yml` fails: "GitHub Actions is not permitted to create or approve pull requests" — needs repo Settings → Actions → "Allow GitHub Actions to create and approve pull requests" enabled
- Workflow double-triggers when agent responds (its comment may contain `/oc`)
