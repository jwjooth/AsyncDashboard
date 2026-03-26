# 🧪 FINAL EXAM — JavaScript Async Module
### Issued by: Senior Lead Developer | Module: JavaScript Asynchronous Programming

---

> **⚠️ READ THIS FIRST — FROM YOUR SENIOR LEAD DEV:**
>
> *"Hey, before we move on to the next module, I need to make sure you actually understand what we've covered — not just memorized it. I've seen too many devs skip this and then crash in production because they don't know the difference between a callback hell and a clean async/await chain. So here's the deal: you're going to build one real project from scratch. No shortcuts. No copy-paste from Stack Overflow. This exam covers everything: Synchronous vs Asynchronous, Callbacks, AJAX, Promises, Fetch API, Async/Await, and Web Workers. Build it right, and we move on. Build it sloppy — we go back to page one."*
>
> — **Senior Lead Dev, Eko's Team**

---

## 📋 PROJECT BRIEF

**Project Name:** `AsyncDashboard` — A Real-Time Public API Dashboard

**Description:**
You are tasked with building a **single-page web application** that acts as a live data dashboard. It fetches data from public APIs, handles all async operations correctly, offloads heavy computation to a Web Worker, and presents everything in a clean, interactive UI.

This is not a tutorial. This is a **professional-level deliverable**. You will be evaluated on **code quality**, **async pattern correctness**, and **error handling discipline**.

---

## 🎯 LEARNING OBJECTIVES TESTED

| # | Competency | Coverage |
|---|-----------|---------|
| 1 | Understand Synchronous vs Asynchronous execution flow | Concept + Implementation |
| 2 | Implement Callback-based async with `setTimeout` & `setInterval` | Feature 1 |
| 3 | Build AJAX requests using `XMLHttpRequest` | Feature 2 |
| 4 | Handle AJAX response status codes & `readyState` lifecycle | Feature 2 |
| 5 | Wrap AJAX in a Promise pattern | Feature 3 |
| 6 | Use `Promise.all()` and `Promise.any()` static methods | Feature 3 |
| 7 | Use Fetch API with `Request` object and handle `Response` | Feature 4 |
| 8 | Send data with Fetch API (JSON, URLSearchParams, FormData) | Feature 4 |
| 9 | Write `async/await` functions with proper `try/catch` | Feature 5 |
| 10 | Implement Web Worker to offload CPU-intensive tasks | Feature 6 |

---

## 🛠️ TECHNICAL REQUIREMENTS

### Stack
- **Vanilla HTML5, CSS3, JavaScript (ES6+)**
- No frameworks (no React, Vue, Angular, jQuery)
- No TypeScript
- No build tools required

### Project Structure (Mandatory)

```
async-dashboard/
│
├── index.html              ← Main HTML shell
├── style.css               ← Your styles
│
├── main.js                 ← Main thread logic (all features)
├── worker.js               ← Web Worker script (Feature 6)
│
└── api/
    └── mock.json           ← Local mock JSON for AJAX feature
```

---

## 🔨 FEATURES TO BUILD

---

### ✅ FEATURE 1 — Live Clock & Countdown Timer *(Callback — `setInterval` / `setTimeout`)*

**Task:**
- Build a **live clock** in the top header of the dashboard that updates every second using `setInterval`.
- Build a **session countdown timer** that starts at `10:00` (10 minutes) when the page loads and counts down to `00:00` using `setInterval`. When it reaches zero, display an alert/notification: `"Session expired. Refresh to continue."` using `setTimeout` with `0ms` delay (demonstrate you understand the event loop).
- Add a **"Reset Timer"** button that clears the existing interval and starts a new one.

**Proof of Knowledge Required:**
- Correct use of `setInterval(callback, ms)` and `setTimeout(callback, ms)`
- Correct use of `clearInterval()` to prevent memory leaks
- Demonstrate that you understand JavaScript's Synchronous execution by adding a `console.log("Timer initialized")` **before** starting the interval and proving the rest of the code continues executing without blocking.

**Acceptance Criteria:**
- [ ] Clock displays real-time `HH:MM:SS`
- [ ] Countdown timer ticks correctly
- [ ] Reset button works without creating duplicate intervals
- [ ] No memory leaks (no stacking intervals)

---

### ✅ FEATURE 2 — AJAX Data Loader with Full State Tracking *(XMLHttpRequest + Callback)*

**Task:**
- Create a local file `api/mock.json` with an array of at least **5 product objects** (id, name, price, category, stock).
- Use `XMLHttpRequest` (raw AJAX — **not Fetch**) to load this file.
- Display all **5 `readyState` transitions** (0 → 1 → 2 → 3 → 4) in a visible **"AJAX State Log"** section on the page, using `onreadystatechange`.
- On success (`status === 200`), render the products into a table on the page.
- Simulate an error by adding a second button that fires an AJAX request to a **deliberately wrong URL** (e.g. `api/not-found.json`), and handle the non-200 response gracefully with a visible error message.

**Proof of Knowledge Required:**
- Raw `XMLHttpRequest` — no wrappers
- `addEventListener("load", callback)` vs `onload` — use both in different places and add a comment explaining the difference
- Check `ajax.status` explicitly before parsing `responseText`
- Log all `readyState` values with their state names (UNSENT, OPENED, HEADERS_RECEIVED, LOADING, DONE)

**Acceptance Criteria:**
- [ ] Products table renders from local JSON file
- [ ] State log panel shows all 5 readyState transitions with labels
- [ ] Error URL shows a visible error message, not a crash
- [ ] Console shows no unhandled errors

---

### ✅ FEATURE 3 — Promise-Wrapped AJAX + Parallel Fetching *(`Promise`, `Promise.all`, `Promise.any`)*

**Task:**
- Refactor the AJAX call from Feature 2 into a **reusable function** `getProduct(filename)` that returns a `Promise`.
- Add **3 additional JSON files** (e.g. `api/users.json`, `api/orders.json`, `api/stats.json`) — each with at least 3 records.
- Create a **"Load All Data"** button that uses `Promise.all()` to fetch all 4 resources simultaneously and display a summary when all are resolved.
- Create a **"Load Fastest"** button that uses `Promise.any()` to race between `api/users.json` and two artificial delayed promises (wrap them in `setTimeout` inside a Promise), and display whichever resolves first.
- Use `.then()`, `.catch()`, and `.finally()` correctly on all promise chains.

**Proof of Knowledge Required:**
- `Promise` constructor with `resolve` and `reject`
- Chained `.then()` for data transformation (not just logging)
- `.catch()` for error boundary
- `.finally()` to hide a loading spinner
- `Promise.all()` — correctly handles all resolved / one rejected
- `Promise.any()` — correctly returns the first resolved

**Acceptance Criteria:**
- [ ] `getProduct()` returns a proper Promise
- [ ] `Promise.all()` loads all 4 resources and summarizes counts
- [ ] `Promise.any()` correctly identifies the fastest resolver
- [ ] A loading spinner appears during fetch and disappears in `.finally()`
- [ ] Rejection in `Promise.all()` is caught and displayed gracefully

---

### ✅ FEATURE 4 — Fetch API Integration with Public REST API *(Fetch API + Request/Response)*

**Task:**
- Use the **public JSONPlaceholder API** (`https://jsonplaceholder.typicode.com`) — no API key needed.
- Implement a **search/filter panel** where the user can:
  1. Type a User ID (1–10) and click "Get User Posts" → fetches `GET /posts?userId={id}` using a `Request` object with `URLSearchParams`.
  2. Click "Create Post" after filling a small form (title + body) → sends a `POST /posts` request using `fetch()` with JSON body and `Content-Type: application/json` header.
  3. View the raw `Response` details: `status`, `statusText`, `ok`, and parsed JSON body displayed on screen.

**Proof of Knowledge Required:**
- `new Request(url, options)` object construction
- `URLSearchParams` appended to URL for GET query
- `fetch()` with headers and JSON body for POST
- Chaining `.then(response => response.json()).then(data => ...)` 
- Check `response.ok` before processing — throw custom error if false

**Acceptance Criteria:**
- [ ] GET with URLSearchParams correctly filters posts by userId
- [ ] POST request sends JSON and displays the mocked created resource
- [ ] Response metadata panel shows `status`, `ok`, `statusText`
- [ ] Network errors are caught and shown in UI — no unhandled rejections

---

### ✅ FEATURE 5 — Async/Await Refactor + Error Boundary *(`async/await`, `try/catch`)*

**Task:**
- Take **Feature 4's entire fetch logic** and refactor it completely to use `async/await` syntax.
- The original Promise chain version should remain in the codebase as **commented-out code** with a comment: `// BEFORE: Promise chain` above it and `// AFTER: async/await` above the refactored version.
- Wrap all `await` calls in `try/catch/finally` blocks.
- Implement a **global async error handler** as an IIFE (Immediately Invoked Function Expression):

```js
(async function() {
    // bootstrap app here
})();
```

- Add a **"Simulate Async Error"** button that `await`s a promise that intentionally `reject`s after 1.5 seconds, and shows the error message in a visible toast/notification UI.

**Proof of Knowledge Required:**
- `async function` declaration and arrow function variants
- `await` unwrapping a Promise result
- `try/catch` catching rejected promises in async context
- `finally` block always running (show/hide UI element)
- IIFE async pattern for top-level execution

**Acceptance Criteria:**
- [ ] All fetch logic rewritten with `async/await`
- [ ] Both versions present (commented vs active) with labels
- [ ] `try/catch/finally` used in every async function
- [ ] Simulated error renders in a toast — not just console
- [ ] IIFE wraps the app bootstrap

---

### ✅ FEATURE 6 — Web Worker for CPU-Intensive Task *(Web Worker, `postMessage`, `onmessage`)*

**Task:**
- Create `worker.js` — a separate Web Worker file.
- Implement a **"Calculate Primes"** feature: the user inputs a number N (e.g. 50000) and clicks "Run in Worker". The worker calculates all prime numbers up to N using a brute-force algorithm (intentionally slow, to demonstrate the point).
- The **Main Thread must remain responsive** during the calculation — prove this by ensuring the live clock from Feature 1 keeps ticking while the worker runs.
- The worker sends progress updates back to the main thread every 1000 numbers processed using `postMessage()`.
- When complete, the worker sends the final array of primes and the main thread displays: count, largest prime, and time taken.
- Add a **"Terminate Worker"** button that calls `worker.terminate()`.

**Proof of Knowledge Required:**
- `new Worker("worker.js")` instantiation in main thread
- `worker.postMessage(data)` to send task to worker
- `worker.addEventListener("message", callback)` to receive results
- Inside `worker.js`: `addEventListener("message", callback)` to receive from main
- Inside `worker.js`: `postMessage(result)` to send back to main
- `worker.terminate()` for cleanup
- Clear demonstration that Main Thread is NOT blocked (clock keeps ticking)

**Acceptance Criteria:**
- [ ] Worker file is separate (`worker.js`)
- [ ] Live clock continues ticking during computation
- [ ] Progress bar or counter updates in real-time from worker messages
- [ ] Final result shows prime count, largest prime, elapsed time
- [ ] Terminate button stops the worker mid-computation

---

## 📐 UI/UX REQUIREMENTS

- Dashboard must have a **navigation/tab system** (not separate pages — use JS to show/hide sections)
- Each Feature gets its own **section/panel** on the dashboard
- All async operations must show a **loading state** (spinner, skeleton, or progress indicator)
- All errors must be shown **in the UI** — not just in `console.error()`
- Use a **consistent color scheme** (dark theme recommended)
- **Mobile-responsive** layout (flexbox or grid)

---

## 📝 CODE QUALITY REQUIREMENTS

1. **No `var`** — use only `const` and `let`
2. **Arrow functions** where appropriate, regular functions where semantically correct
3. **Comments** on every major async operation explaining WHY, not WHAT
4. **No callback hell** — maximum 2 levels of nesting before you must refactor
5. **Console discipline** — use `console.info()`, `console.warn()`, `console.error()` appropriately
6. All event listeners must be attached via `addEventListener` — no inline `onclick` in HTML
7. All intervals/timeouts must be stored in variables and cleaned up when not needed

---

## 🧠 CONCEPTUAL QUESTIONS (Written Answers in README.md)

Answer the following questions **in your own words** inside the `README.md` file. These will be reviewed:

1. **Explain the difference between Synchronous and Asynchronous execution in JavaScript.** Give a real-world analogy (not the one from the slides).

2. **Why does "Callback Hell" happen?** Show a pseudocode example of callback hell and then show how Promise chaining solves it.

3. **What is the difference between `Promise.all()` and `Promise.any()`?** When would you choose one over the other in a production scenario?

4. **Explain what `readyState` is in XMLHttpRequest.** Why does it matter to track state transitions?

5. **What is the key advantage of `async/await` over raw Promise chains?** Are there any downsides?

6. **Why can't JavaScript do true parallel execution in the Main Thread?** What problem does Web Worker solve, and what are its limitations (e.g. DOM access)?

7. **When would you use `fetch()` over `XMLHttpRequest` in a new project?** Is there any case where you'd still choose XHR?

---

## 🏆 GRADING RUBRIC

| Area | Weight | Criteria |
|------|--------|---------|
| Feature 1 — Callbacks | 10% | Clock works, no stacked intervals, reset works |
| Feature 2 — AJAX/XHR | 20% | All readyState shown, error handled, table renders |
| Feature 3 — Promise | 20% | Promise constructor correct, `.all()` and `.any()` work |
| Feature 4 — Fetch API | 15% | Request object used, GET/POST correct, response parsed |
| Feature 5 — Async/Await | 20% | Full refactor, both versions shown, error boundary works |
| Feature 6 — Web Worker | 15% | Worker separate file, UI unblocked, progress updates |
| Written Answers (README) | 10% | Clear, accurate, in own words |
| Code Quality | Bonus +5% | Clean, commented, no var, no callback hell |

**Passing Grade: 70% and above**

---

## ⏱️ DEADLINE

You have **72 hours** from the time this document is handed to you.

**Submission:** Push to your GitHub repository with the folder structure intact. Share the repo link with your Senior Lead Dev.

---

## 🚫 RULES

- ❌ No external JavaScript libraries (Axios, jQuery, lodash — all banned)
- ❌ No frameworks
- ❌ No AI-generated code submitted without understanding — you WILL be asked to explain any line
- ✅ MDN Web Docs is allowed
- ✅ The course slides are allowed
- ✅ Your own notes are allowed

---

## 💬 FINAL WORDS FROM YOUR SENIOR LEAD DEV

> *"I don't care how the UI looks. I care that you understand WHY each async pattern exists and WHEN to use it. A beautiful dashboard with broken async logic is worse than an ugly one that handles errors correctly. Good luck — and remember: the goal isn't to finish. The goal is to understand."*

---

*Module: JavaScript Async | Issued by: Senior Lead Developer | Next Module: JavaScript Web API*
