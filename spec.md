# YYPS — YY Procurement System

采购 / 物流跟踪系统. Tracks goods from China factory to US warehouse receiving.

**Business flow:** 中国工厂 → 中国仓 → 海运 → 美国仓 → Receiving

**Roles:** Product Owner (Jelin) · Developer

---

## Tech Stack (frozen)

| Layer | Choice |
|-------|--------|
| Framework | Next.js 15 (App Router) |
| Language | TypeScript (strict) |
| Backend / DB / Auth | Supabase |
| Styling | TailwindCSS |
| UI components | Shadcn/ui |
| Validation | zod |
| Forms | react-hook-form |

## Coding Principles

1. TypeScript strict mode
2. No `any`
3. Mobile first
4. Status driven (records move through explicit status states)
5. Simple first
6. One iteration = one deliverable module

---

## Modules

### MVP (Batch 1)
- **Login** — email/password auth, session, logout
- **Dashboard** — KPI cards, my actions, exception summary
- **PO** — purchase orders
- **Container** — shipping containers, list + detail
- **Receiving** — receive goods at US warehouse
- **Exception** — flag/track problems

### Batch 2
- Products
- Suppliers
- Inventory
- Notifications
- YY Assistant

---

## Iteration Plan

One module per iteration. Deliver → PO reviews (UAT) → fix → next.

| Iteration | Module | Files |
|-----------|--------|-------|
| 1 | Login | `lib/supabase/client.ts`, `components/auth/LoginForm.tsx`, `app/login/page.tsx`, `middleware.ts` |
| 2 | Dashboard | `app/dashboard/page.tsx`, `components/dashboard/KPICard.tsx`, `MyActions.tsx`, `ExceptionSummary.tsx` |
| 3 | Container | `app/containers/page.tsx`, `app/containers/[id]/page.tsx` |
| 4 | PO | TBD |

### Iteration 1 — Login: Definition of Done
- [ ] Email input + validation
- [ ] Password input + validation
- [ ] Login works, session saved
- [ ] Logout works
- [ ] Mobile friendly
- [ ] Desktop friendly
- [ ] Redirect to Dashboard on success

---

## Open Questions (not yet decided)

- Database schema — tables, relationships, ER diagram. **Nothing designed yet.**
- Status engine — what states each entity (PO, Container, Receiving) moves through
- Exception engine — rules for raising/clearing exceptions
- Notification engine — triggers and channels
- YY Assistant — scope unknown
