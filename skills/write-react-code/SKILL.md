---
name: write-react-code
description: Writes React components and hooks with a fixed body order under padded section headers, stable callback refs, and repeated markup rendered from data with map. Use when writing, refactoring, or reviewing React components or hooks, or when the user says "clean up this component", "this hook is messy", "copy-pasted JSX", "duplicated markup", or "ref is null in my effect".
when_to_use: |
  - Any time Claude writes or edits a React component or hook (.tsx/.jsx), even if the user never mentions structure
  - User asks to review or refactor React code: "clean up this component", "this hook is messy", "hard to find things in this file"
  - JSX repeats the same structure several times with only text, icons, or links changing
  - A callback ref flickers to null, or an effect that reads a ref sees it detached
  - Do NOT use for: Vue/Svelte/Angular, React Native, plain .ts utilities with no components or hooks, test specs, or generated code
license: MIT
metadata:
  author: piplupjs
  version: "1.0.0"
---

# Write React Code

Three rules for every React component and hook. Not for Vue/Svelte/Angular, React Native, component-free `.ts` utilities, test specs, or generated code.

## Workflow

1. **Write** — order the body by the table below; apply the ref and markup rules as you go.
2. **Review** — one pass: sections in order with padded headers, no inline callback ref read by an effect, no copy-pasted markup.

## 1. Body order

Order every component/hook body as below. Each section except the first starts with `// ─── Name ───` padded with `─` to 74 characters (indent included). Omit empty sections.

| # | Section | Holds |
|---|---|---|
| 1 | *(no header)* | Unclassified hooks: `useCurrentUser()`, `useSidebar()` |
| 2 | State | `useState`, `useReducer`, `useParams`, search params, other state hooks |
| 3 | Compute | Optional: values derived from the state |
| 4 | Services | API calls: `useQuery`, `useMutation` |
| 5 | Compute | Optional: values derived from the services |
| 6 | Form | `useForm` and its options |
| 7 | Callbacks | Event handlers and other functions |
| 8 | Table | Table hook and column hooks, when the component renders a data table |
| 9 | Effects | `useEffect` and friends |

Form comes after Compute and before Callbacks because callbacks (such as a cancel handler) use the form.

```tsx
// bad — state, queries, handlers and effects interleaved
export function InvoiceView({ id }: { id: string }) {
  const { data } = useQuery(invoiceQueryOptions(id));
  const handlePay = () => pay(id);
  const [isEditing, setIsEditing] = useState(false);
  useEffect(() => track('invoice'), []);
  const user = useCurrentUser();
  // ...
}

// good
export function InvoiceView({ id }: { id: string }) {
  const user = useCurrentUser();

  // ─── State ───────────────────────────────────────────────────────────
  const [isEditing, setIsEditing] = useState(false);

  // ─── Services ────────────────────────────────────────────────────────
  const { data } = useQuery(invoiceQueryOptions(id));

  // ─── Compute ─────────────────────────────────────────────────────────
  const isPaid = data?.status === 'PAID';

  // ─── Callbacks ───────────────────────────────────────────────────────
  const handlePay = useCallback(() => pay(id), [id]);

  // ─── Effects ─────────────────────────────────────────────────────────
  useEffect(() => track('invoice'), []);

  // ...
}
```

## 2. Stable callback refs

When anything reads a ref in an effect, the callback ref must be stable (`useCallback`), never an inline arrow function. React detaches an inline callback ref (calls it with `null`) and re-attaches it on every commit, and a child's layout effect runs in between.

```tsx
// bad — new function every render: ref goes null → node each commit
<div ref={(node) => setContainer(node)} />

// good
const containerRef = useCallback((node: HTMLDivElement | null) => {
  setContainer(node);
}, []);

<div ref={containerRef} />
```

## 3. Repeated markup from data

When repeated UI markup shares the same structure, represent the items as data and render them with `map`.

```tsx
// bad
<nav>
  <a href="/profile"><UserIcon /> Profile</a>
  <a href="/security"><LockIcon /> Security</a>
  <a href="/sessions"><MonitorIcon /> Sessions</a>
</nav>

// good
const links = [
  { href: '/profile', icon: UserIcon, label: 'Profile' },
  { href: '/security', icon: LockIcon, label: 'Security' },
  { href: '/sessions', icon: MonitorIcon, label: 'Sessions' },
];

<nav>
  {links.map(({ href, icon: Icon, label }) => (
    <a key={href} href={href}><Icon /> {label}</a>
  ))}
</nav>
```
