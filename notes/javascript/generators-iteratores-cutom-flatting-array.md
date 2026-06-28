# JavaScript Mastery Notes — Flattening Arrays, Generators & Iterators

---

## Part 1: Flattening Arrays

### `Array.prototype.flat` — built-in, use this in production
```js
const nested = [1, [2, [3, [4, [5]]]]];

nested.flat();         // [1, 2, [3, [4, [5]]]]   — one level
nested.flat(2);        // [1, 2, 3, [4, [5]]]      — two levels
nested.flat(Infinity); // [1, 2, 3, 4, 5]           — all levels
```
Returns a **new** array, doesn't mutate the original.

### When you need a custom `flatten`

**1. Skip-flattening certain values**
Some objects look array-ish (they have a `length`, they're iterable) but aren't
plain arrays — `Buffer` (Node) or typed arrays like `Uint8Array`. A naive flatten
sees "this has a length, let me dig in" and shreds it into its raw bytes. A
custom `flatten` needs an extra check — "is this a *real* plain array, or just
something array-shaped I should leave whole?" — before deciding to recurse into
it.

**2. Flattening trees of objects, not arrays**
A nested array only ever nests one way: array inside array inside array. A tree
is a different shape — objects with a `children` property, like a folder
structure:
```js
{ name: "root", children: [
  { name: "a", children: [] },
  { name: "b", children: [{ name: "c", children: [] }] },
]}
```
The recursive *idea* is identical to array-flatten (dig into the smaller thing,
collect results) — you just follow `.children` instead of checking
`Array.isArray`.

**3. Iterative flattening to avoid recursion limits**
Every recursive call adds a frame to the JS call stack, which has a hard,
engine-enforced limit (often in the low thousands). Real data is rarely nested
that deep — but "potentially adversarial" means someone could *deliberately*
hand you an array nested thousands of levels deep just to crash your process
with a `RangeError`. The fix is the iterative, explicit-stack version covered
below: it moves the "remember where I am" bookkeeping off the fragile call stack
and onto a plain array on the heap, which has a far higher ceiling.

**4. Lazy flattening with a generator**
If the flattened result could be huge — millions of items — and the caller only
wants the first few, building the *entire* flattened array up front wastes work.
A generator-based flatten can pause mid-traversal and `yield` one value at a
time, so the caller only pays for exactly as much flattening as they actually
use.

```js
function* flattenLazy(arr) {
  for (const item of arr) {
    if (Array.isArray(item)) {
      yield* flattenLazy(item); // delegate to the inner generator
    } else {
      yield item;
    }
  }
}
```
`yield*` is "yield delegation" — shorthand for looping over another generator
and yielding each of its values one by one (`for (const v of flattenLazy(item)) yield v;`).

```js
const huge = [1, [2, [3, [4, [5, [6, [7 /* ...thousands more... */]]]]]]];

const gen = flattenLazy(huge);
const firstThree = [];
for (const val of gen) {
  firstThree.push(val);
  if (firstThree.length === 3) break; // generator freezes right here
}
// firstThree = [1, 2, 3] — the rest of `huge` is never traversed at all
```
Compare this to the eager `flatten(huge)`, which must fully recurse through
every level before returning anything — even if only the first 3 values were
ever needed.

Note these aren't four separate algorithms — they're the same recursive
flattening idea with one extra constraint bolted on each time (skip some types /
different data shape / no call stack / pause between values).

### Recursive version — the core logic
Every recursive function needs a fork:
- **Recursive case**: the item is itself an array → flatten it, merge the result in
- **Base case**: the item is not an array → just keep it

```js
function flatten(arr) {
  let result = [];
  for (const item of arr) {
    if (Array.isArray(item)) {
      result = result.concat(flatten(item)); // recurse on the smaller piece
    } else {
      result.push(item);
    }
  }
  return result;
}
```

### Why recursion can fail: the call stack
Each recursive call adds a frame to the JS **call stack** — a fixed-size structure
the engine controls. Nest deep enough (especially with adversarial input) and you
get:
```
RangeError: Maximum call stack size exceeded
```

### Iterative version — your own stack instead of the call stack
Use a plain array as a manual "to-do pile" and a `while` loop. No function calls
pile up — only the array grows, and arrays aren't bound by the call stack's limit.

```js
function flattenIterative(inputArray) {
  const stack = [...inputArray]; // copy input into our working stack
  const result = [];

  while (stack.length > 0) {
    const next = stack.pop();           // take the LAST item out
    if (Array.isArray(next)) {
      stack.push(...next);              // spread its items back onto the stack
    } else {
      result.push(next);
    }
  }

  // We popped from the end, so items come out back-to-front — reverse to fix it.
  return result.reverse();
}
```

**Key line explained — `stack.push(...next)`**
`...next` is the **spread operator**: it unpacks an array into individual items.
`stack.push(...next)` on `next = [5, 6]` is the same as `stack.push(5, 6)`.
Without the spread, you'd push the whole array back as one item and loop forever
on the same nested array.

**Why `.reverse()` at the end?**
We always pop from the *end* of the stack, so the deepest-processed values land in
`result` first — in reverse order relative to the original array. Reversing once at
the end restores the correct order.

### Complexity
| | Recursive | Iterative |
|---|---|---|
| Time | O(n) — every element visited once | O(n) — same |
| Space | O(n) — lives on the call stack (hard, fixed limit) | O(n) — lives in a plain array on the heap (much higher ceiling) |

The iterative version isn't "more efficient" in big-O terms — it just moves the
memory from a fragile, engine-enforced limit to ordinary heap memory.

---

## Part 2: Generators & Iterators

### The core problem they solve
A normal function has no memory between calls — each call starts completely
fresh and forgets everything once it returns. Generators let a function **pause**
mid-execution, remembering exactly where it left off, and resume later.

### The Iterator protocol — no special syntax required
An **iterator** is just any object with a `.next()` method that returns
`{ value, done }`. You can build one by hand with a closure:

```js
function makeCounter() {
  let count = 0; // stays alive between calls because of the closure

  return {
    next() {
      count++;
      return { value: count, done: count > 3 };
    },
  };
}

const counter = makeCounter();
counter.next(); // { value: 1, done: false }
counter.next(); // { value: 2, done: false }
counter.next(); // { value: 3, done: false }
counter.next(); // { value: 4, done: true }
```
Caveat: this hand-rolled version doesn't actually *stop* — call `.next()` again
and `count` keeps climbing while `done` stays `true`. A real generator doesn't
have this bug.

### Generator syntax — `function*` and `yield`
```js
function* realCounter() {
  yield 1;
  yield 2;
  yield 3;
}

const it = realCounter();
it.next(); // { value: 1, done: false }
it.next(); // { value: 2, done: false }
it.next(); // { value: 3, done: false }
it.next(); // { value: undefined, done: true }
it.next(); // { value: undefined, done: true } — frozen here forever, no more work
```
- `function*` marks a generator. **Calling it runs none of the body** — it just
  returns a paused iterator.
- `yield` is the pause button. Execution stops there until `.next()` is called
  again, and resumes from exactly that point — variables and all.
- `done` becomes `true` only once execution literally runs off the end of the
  function — it's not a calculated condition, it's a physical fact about whether
  there's any code left to run.

**Side effects run regardless of `done`:**
```js
function* weird() {
  console.log("a");
  yield 1;
  console.log("b");
}
// .next() twice logs "a" then "b", returning {value:1,done:false} then {value:undefined,done:true}
```

### Iterable vs Iterator vs Generator
- **Iterator** — an object with `.next()` returning `{ value, done }`.
- **Iterable** — an object with a `[Symbol.iterator]()` method that *produces* an
  iterator. This is what makes `for...of`, spread, and `Array.from()` work.
- **Generator function** — a shortcut that builds something which is *both* at
  once, automatically.

### `for...of` — automatic `.next()` calls
```js
for (const num of realCounter()) {
  console.log(num);
}
// logs: 1, 2, 3
```
`for...of` calls `.next()` for you, unwraps `.value` for the loop body, and stops
**silently** the moment `done` is `true` — it never logs or processes that final
`{ value: undefined, done: true }` result.

### Custom iterable class
```js
class TicketQueue {
  constructor(tickets) {
    this.tickets = tickets;
  }
  [Symbol.iterator]() {
    let i = 0;
    return {
      next: () => i < this.tickets.length
        ? { value: this.tickets[i++], done: false }
        : { value: undefined, done: true },
    };
  }
}

const queue = new TicketQueue(["Ticket 1", "Ticket 2"]);
for (const ticket of queue) {
  console.log(ticket);
}
```

### Real-world use cases
1. **Async control flow — `redux-saga`**
   ```js
   import { call, put } from "redux-saga/effects";

   function* submitClaimSaga(action) {
     try {
       const data = yield call(submitWorkFlow, action.payload);
       yield put({ type: "SUBMIT_SUCCESS", payload: data });
     } catch (error) {
       yield put({ type: "SUBMIT_FAILURE", error });
     }
   }
   ```
   The middleware calls `.next()` for you, pausing at each `yield` until a promise
   resolves — this is why sagas read like linear code instead of `.then()` chains,
   and why they're easy to test (you can step through yields manually).

2. **Streaming large files — Node's `readline`**
   ```js
   for await (const line of rl) {
     console.log(line); // one line at a time, file never fully loaded in memory
   }
   ```

3. **Database cursors (e.g. MongoDB)** — fetch results in batches as you iterate,
   never loading a huge result set into memory at once.

4. **Lazy, possibly-infinite sequences**
   ```js
   function* idGenerator() {
     let id = 1000;
     while (true) yield `ORD-${id++}`;
   }
   ```
   Nothing is computed until `.next()` is actually called.

### Heuristic: when to actually use this
- Already have a full in-memory array, just transforming it? → Use `.map()` /
  `.filter()`, skip generators.
- Data could be huge, unknown, or infinite, and you only need part of it? →
  Lazy generator/iterator.
- Want your own class to work with `for...of` / spread / destructuring? →
  Implement `[Symbol.iterator]()`.
- Modeling something that pauses and resumes over time (multi-step async flow,
  retries, wizards, turn-based logic)? → Generator.
