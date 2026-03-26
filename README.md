# AsyncDashboard — Final Exam Project
### JavaScript Async Module | Student Submission

---

## 👤 Student Info

| Field | Value |
|-------|-------|
| **Name** | *(Your Name)* |
| **Date Submitted** | *(DD/MM/YYYY)* |
| **Module** | JavaScript Asynchronous Programming |
| **Examiner** | Senior Lead Developer |

---

## 🚀 How to Run This Project

```bash
# Clone the repository
git clone <your-repo-url>
cd async-dashboard

# Run with a local server (required for AJAX to work — no file:// protocol)
# Option 1: VS Code Live Server extension
# Option 2: Python
python -m http.server 8080

# Then open:
# http://localhost:8080
```

> ⚠️ **Important:** This project MUST be served from a local HTTP server. Opening `index.html` directly via `file://` will cause AJAX/Fetch CORS errors.

---

## 📁 Project Structure

```
async-dashboard/
│
├── index.html              ← Main HTML shell
├── style.css               ← Dashboard styles
├── README.md               ← This file
│
├── main.js                 ← Main thread: all features logic
├── worker.js               ← Web Worker: prime number computation
│
└── api/
    ├── mock.json           ← Products data (Feature 2)
    ├── users.json          ← Users data (Feature 3)
    ├── orders.json         ← Orders data (Feature 3)
    └── stats.json          ← Stats data (Feature 3)
```

---

## ✅ Feature Completion Checklist

> Mark each item with [x] when complete.

### Feature 1 — Live Clock & Countdown Timer (Callbacks)
- [ ] Live clock displays `HH:MM:SS` and updates every second
- [ ] Countdown timer starts at `10:00` and ticks down
- [ ] Expiry notification fires using `setTimeout` when timer hits `00:00`
- [ ] Reset button clears existing interval before starting new one
- [ ] No stacked/duplicate intervals (no memory leak)
- [ ] `console.log` before interval proves non-blocking execution

### Feature 2 — AJAX Data Loader (XMLHttpRequest)
- [ ] `api/mock.json` created with 5+ product objects
- [ ] Products rendered in HTML table from XHR response
- [ ] All 5 `readyState` values (0–4) displayed with labels in UI
- [ ] `response.status === 200` check before parsing
- [ ] Error URL test button shows graceful error message in UI
- [ ] Both `onload` and `addEventListener("load")` used with comments

### Feature 3 — Promise-Wrapped AJAX (Promise API)
- [ ] `getProduct(filename)` function returns a `Promise`
- [ ] 3 additional JSON files created
- [ ] `Promise.all()` fetches all 4 resources and renders summary
- [ ] `Promise.any()` races between sources, displays fastest winner
- [ ] `.then()`, `.catch()`, `.finally()` used correctly
- [ ] Loading spinner shown during fetch, hidden in `.finally()`

### Feature 4 — Fetch API with Public REST API
- [ ] `new Request()` object used for at least one request
- [ ] `URLSearchParams` used for GET query filtering by userId
- [ ] POST request sends JSON body with `Content-Type` header
- [ ] Response metadata (`status`, `ok`, `statusText`) displayed in UI
- [ ] `response.ok` checked before parsing; custom error thrown if false
- [ ] Network errors caught and displayed in UI

### Feature 5 — Async/Await Refactor
- [ ] Feature 4 logic refactored to `async/await`
- [ ] Both versions present in code (`// BEFORE` and `// AFTER` comments)
- [ ] Every `await` wrapped in `try/catch/finally`
- [ ] App bootstrapped with `(async function() { ... })()`
- [ ] "Simulate Async Error" button shows toast with error message

### Feature 6 — Web Worker
- [ ] `worker.js` is a separate file
- [ ] `new Worker("worker.js")` instantiated correctly
- [ ] `postMessage()` sends task data to worker
- [ ] Progress updates received and shown in real-time
- [ ] Live clock from Feature 1 remains unblocked during computation
- [ ] Final result: prime count + largest prime + elapsed time displayed
- [ ] "Terminate Worker" button calls `worker.terminate()`

---

## 💬 Conceptual Questions — Written Answers

> Answer each question in your own words. Be direct and precise.

---

### 1. Difference Between Synchronous and Asynchronous Execution

*(Write your answer here — minimum 3 sentences, include a real-world analogy that is NOT from the slides)*

**Answer:**

---

### 2. Why Does "Callback Hell" Happen? How Does Promise Solve It?

*(Show a pseudocode example of callback hell, then show the Promise chain version)*

**Callback Hell Example:**
```javascript
// Write your example here
```

**Promise Chain Solution:**
```javascript
// Write your solution here
```

**Explanation:**

---

### 3. `Promise.all()` vs `Promise.any()` — When to Use Each?

*(Explain the difference and give a real production scenario for each)*

**`Promise.all()` — What it does:**

**`Promise.any()` — What it does:**

**Production Scenario for `Promise.all()`:**

**Production Scenario for `Promise.any()`:**

---

### 4. What is `readyState` in XMLHttpRequest? Why Does It Matter?

*(Explain each state value 0–4 in your own words and why tracking them matters)*

**Answer:**

| Value | State Name | What it Means (in your words) |
|-------|-----------|-------------------------------|
| 0 | UNSENT | |
| 1 | OPENED | |
| 2 | HEADERS_RECEIVED | |
| 3 | LOADING | |
| 4 | DONE | |

**Why it matters:**

---

### 5. `async/await` vs Raw Promise Chains — Advantages and Downsides

*(Be honest about both sides — don't just praise async/await)*

**Advantages of `async/await`:**

**Downsides / Gotchas:**

---

### 6. Why Can't JavaScript Do True Parallel Execution in the Main Thread?

*(Explain the single-threaded nature of JS, what Web Worker solves, and its limitations)*

**Why JavaScript is single-threaded:**

**What Web Worker solves:**

**Limitations of Web Workers:**

---

### 7. When Would You Use `fetch()` Over `XMLHttpRequest`?

*(Give at least one case where you'd still prefer XHR)*

**When to use `fetch()`:**

**When you might still use `XMLHttpRequest`:**

---

## 🐛 Known Issues / Limitations

*(Be transparent — list any features that don't fully work or known bugs)*

- 

---

## 📚 References Used

*(List any MDN articles, documentation pages you referenced — no shame, this is expected)*

- [MDN — XMLHttpRequest](https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest)
- [MDN — Fetch API](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API)
- [MDN — Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise)
- [MDN — Web Workers API](https://developer.mozilla.org/en-US/docs/Web/API/Web_Workers_API)
- *(Add others here)*

---

## 🙋 Self-Assessment

Rate yourself honestly (1–5) on each competency:

| Competency | Self-Rating (1–5) | Notes |
|-----------|------------------|-------|
| Understanding Sync vs Async | | |
| Callback with setTimeout/setInterval | | |
| XMLHttpRequest & AJAX | | |
| readyState lifecycle | | |
| Promise (constructor + methods) | | |
| Promise.all() / Promise.any() | | |
| Fetch API with Request/Response | | |
| Sending data (JSON, URLSearchParams, FormData) | | |
| async/await with error handling | | |
| Web Worker communication | | |

---

*Submitted for: JavaScript Async Module Final Exam | Next Module: JavaScript Web API*
