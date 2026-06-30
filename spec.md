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

## Container Module (designed in demo)

A container is a shipment that holds a list of products. Each line = one product with a quantity.

### Status flow
`中国仓 → 海运 → 美国仓 → Receiving`, plus `Exception` as a side-state (toggle on/off, returns to 中国仓).

### Data model

```
containers
  id          text   PK   -- e.g. CN-4471
  po          text        -- FK → purchase_orders, e.g. PO-1032
  status      text        -- 中国仓 | 海运 | 美国仓 | Receiving | Exception
  eta         date

container_items
  id          uuid   PK
  container_id text  FK → containers.id
  product     text        -- later FK → products
  sku         text
  qty         int
```

### Container UI (per demo.html)
- **Home** — single screen: dashboard KPI cards on top, container list directly below (no separate Dashboard/Containers tabs)
- **List** — container, PO, status badge, ETA, item summary (line count · total pcs), manage actions (advance status, toggle exception)
- **Detail** — container header + product table (product / SKU / qty) with running total; add / remove line items; Back returns to Home
- **Add Container** — container no, PO, ETA → starts at 中国仓 with empty item list

---

## Open Questions (not yet decided)

- Database schema for other entities — PO, Receiving, Products, Suppliers, Inventory. (Container/items drafted above.)
- Status engine — states for PO and Receiving (Container flow decided above)
- Exception engine — rules for raising/clearing exceptions
- Notification engine — triggers and channels
- YY Assistant — scope unknown
