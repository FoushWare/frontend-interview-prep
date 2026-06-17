# Frontend System Design Questions

## 1. How would you design a scalable React application?

### Answer

Key principles:

1. Feature-based architecture
2. Shared component library
3. Centralized API layer
4. State management strategy
5. Code splitting
6. Automated testing

Example:

```

src/
features/
shared/
services/
hooks/
components/

```

---

## 2. How would you optimize performance?

### Answer

Techniques:

- React.memo
- useMemo
- useCallback
- Lazy loading
- Code splitting
- Virtualization
- Image optimization
- API caching

---

## 3. How would you structure API calls?

### Answer

```

services/
userService.ts
productService.ts

```

Avoid calling APIs directly inside components.

---

## 4. What is API caching?

### Answer
Caching stores previously fetched data to avoid unnecessary network requests.

Common tools:

- React Query
- SWR
- Browser cache
