# 104-Week Full Mastery Plan (Markdown)

## Resources (primary anchors — open & study these slowly; each entity linked once)

* CS50
* The Cherno
* freeCodeCamp
* Traversy Media
* Stockfish
* Introduction to Algorithms

---

## How to use this Markdown plan (read before week 1)

* Do weeks strictly in order. Don’t skip earlier fundamentals.
* Weekdays: ~30–45 min reading + 30–60 min coding. Weekends: longer blocks (3–5 hrs). Aim ~12–14 hrs/week. Adjust for school.
* Keep `journal.md` updated each week with a 300–500 word reflection, diagram(s), and one question. Save artifacts (screenshots, CSVs, videos) under `artifacts/week-XX/`.
* Use `build/` for CMake builds (MSVC) and `msys2/` shell for MinGW tasks. Run Windows verification commands in PowerShell unless noted.
* Stop and fix any failing verification steps before moving on from phase consolidation weeks.

---

> NOTE: Commands shown below are Windows-friendly. When `g++` / `MinGW` is mentioned, run in **MSYS2 MinGW64 shell**; when `cmake --build` with Visual Studio is shown, run in **PowerShell / Developer PowerShell**.

---

# Phase A — Foundations (Weeks 1–16)

### Week 1 — Setup & environment

* **Reading/Video**: CS50 lecture 0 (overview / environment).
* **Coding exercise**: Install toolchain: Visual Studio (MSVC), MSYS2/MinGW, VS Code. Initialize `your-system-project-windows` repo.
* **Project task**: Create repo skeleton, `README.md`, and a one-page design doc stub.
* **Verification**: PowerShell:

  * `git init && git status`
  * MSYS2: `gcc --version`
  * MSVC (Developer PowerShell): `cl`.
* **Journal/Teach**: Write 300–500 words comparing MSVC vs MinGW toolchains and a diagram of the toolchain.

---

### Week 2 — C basics & compilation on Windows

* **Reading/Video**: CS50 lecture 1 (C fundamentals).
* **Coding exercise**: Implement `my_atoi.c` and `strcpy.c`. Compile with `gcc` (MSYS2) and `cl` (MSVC).
* **Project task**: Add `tools/` and a minimal test harness.
* **Verification** (MSYS2):

  * `g++ -fsanitize=address -O0 -g tools/my_atoi.c -o bin/my_atoi.exe && ./bin/my_atoi.exe`
* **Journal/Teach**: Diagram pointer lifetime and stack vs heap; save PNG to `artifacts/week-02/`.

---

### Week 3 — Pointers, arrays, memory

* **Reading/Video**: Article on Windows memory model (stack vs heap).
* **Coding exercise**: Implement dynamic array in C with `malloc`/`realloc`; tests for edge cases.
* **Project task**: Add CLI to exercise append & print.
* **Verification**: Run with ASan (MSYS2) or Visual Studio Diagnostic Tools; capture output to `artifacts/week-03/asan_output.txt`.
* **Journal/Teach**: Explain pointer aliasing with code examples.

---

### Week 4 — Git discipline & small C utility

* **Reading/Video**: Git branching & rebase guide.
* **Coding exercise**: Build a small C text search utility; use feature branch and rebase into `main`.
* **Project task**: Add GitHub Actions CI YAML stub for `windows-latest` build.
* **Verification**: `git log --oneline --graph` and check Actions run on push.
* **Journal/Teach**: Write a 1-page “How I use Git on Windows”.

---

### Week 5 — C++ intro & `MiniVector` skeleton

* **Reading/Video**: The Cherno videos 1–3 (C++ basics & setup).
* **Coding exercise**: Create `MiniVector<T>` skeleton (header + cpp). Configure `CMakeLists.txt` for MSVC + MinGW.
* **Project task**: Add `src/` + `include/`; basic build targets.
* **Verification** (PowerShell / MSVC):

  * `cmake -S . -B build -G "Visual Studio 17 2022" -A x64`
  * `cmake --build build --config Debug`
* **Journal/Teach**: Short RAII explanation and notes.

---

### Week 6 — RAII & push_back

* **Reading/Video**: RAII & destructor behavior overview.
* **Coding exercise**: Implement `push_back` including resizing and destructor correctness.
* **Project task**: Add unit tests (simple harness or GoogleTest).
* **Verification**: `ctest -C Debug` or run test exe; ensure ASan/Diagnostics report no leaks.
* **Journal/Teach**: Record a 5-min screencast showing `MiniVector` resizing.

---

### Week 7 — Move semantics & rule of five

* **Reading/Video**: Move semantics primer (concise reading).
* **Coding exercise**: Implement move ctor/assignment for `MiniVector`. Add microbench using `std::chrono`.
* **Project task**: Commit bench CSV to `bench/`.
* **Verification**: `build\Debug\mini_bench.exe > bench\week07.csv` and inspect.
* **Journal/Teach**: Explain scenarios where moves avoid copies.

---

### Week 8 — CMake cross-config & CI

* **Reading/Video**: CMake on Windows (Visual Studio vs MinGW).
* **Coding exercise**: Make `CMakeLists.txt` support both MSVC and MinGW; add `ctest` target.
* **Project task**: Add GitHub Actions Windows job that builds and runs tests.
* **Verification**: Push branch and confirm Actions `windows-latest` build passes.
* **Journal/Teach**: Write “Build on Windows” README section.

---

### Week 9 — Discrete math primer (induction)

* **Reading/Video**: Discrete math: induction & proofs (short primer).
* **Coding exercise**: Implement recursive factorial; trace stack frames in Visual Studio and screenshot call stack.
* **Project task**: Add `debug/stack-traces/` instructions.
* **Verification**: Save screenshot to `artifacts/week-09/stack_trace.png`.
* **Journal/Teach**: Map mathematical induction ↔ recursion.

---

### Week 10 — Debugging mastery on Windows

* **Reading/Video**: Visual Studio Debugger guide (MS docs).
* **Coding exercise**: Introduce a use-after-free in `MiniVector`, reproduce in Visual Studio, fix it.
* **Project task**: Add `debug/` reproduction steps & `.dmp` dump.
* **Verification**: Generate `.dmp`, analyze or save stack trace to `artifacts/week-10/dump_analysis.txt`.
* **Journal/Teach**: 1-page: “How I debug memory issues on Windows”.

---

### Week 11 — Small C++ CLI project

* **Reading/Video**: Design doc template (use one-page template).
* **Coding exercise**: Build a C++ CLI task list using `MiniVector`; file persistence.
* **Project task**: Add `data/sample_tasks.json` and unit tests for persistence.
* **Verification**: Run CLI, add tasks, exit, restart and validate persistence; save run log.
* **Journal/Teach**: Outline file format & error handling decisions.

---

### Week 12 — Phase A consolidation

* **Reading/Video**: Revisit weak points from Phase A.
* **Coding exercise**: Fix platform issues; ensure cross-compiler builds.
* **Project task**: Ensure CI (`windows-latest`) builds/tests pass.
* **Verification**: `build/Debug/tests_results.xml` exists and is green.
* **Journal/Teach**: Phase A reflection (1 page).

---

### Week 13 — Templates & `MiniHashMap`

* **Reading/Video**: Templates & generic programming (Cherno + reference).
* **Coding exercise**: Implement `MiniHashMap<K,V>` (open addressing, resizing).
* **Project task**: Stress tests for collisions.
* **Verification**: `build\Debug\hash_stress.exe > bench\week13_hash.csv`
* **Journal/Teach**: Screencast explaining hashing & rehash.

---

### Week 14 — Iterators & STL reimplement

* **Reading/Video**: Study `std::vector` & iterator concepts.
* **Coding exercise**: Add iterator support to `MiniVector` (`begin()`/`end()`); enable range-for.
* **Project task**: Refactor CLI to use iterators.
* **Verification**: All iterator tests pass; update coverage.
* **Journal/Teach**: Write why iterator abstraction matters.

---

### Week 15 — Amortized analysis & bench

* **Reading/Video**: Amortized analysis (CLRS summary).
* **Coding exercise**: Benchmark `push_back` amortized cost; record times.
* **Project task**: Add plotting instructions for bench CSV.
* **Verification**: Commit bench PNG to `artifacts/week-15/`.
* **Journal/Teach**: Blog post on amortized analysis with your data.

---

### Week 16 — Phase A final checks

* **Reading/Video**: Final review of Phase A materials.
* **Coding exercise**: Fix unresolved issues and polish design doc for persistent project.
* **Project task**: Ensure Phase A artifacts (tests, benches, docs) are present.
* **Verification**: `artifacts/phaseA_checklist.md` all green.
* **Journal/Teach**: 10-minute demo video of Phase A repo.

---

# Phase B — Data Structures & Algorithms (Weeks 17–32)

> Implement each data structure **by hand**, add exhaustive tests and benchmarks, and integrate into your persistent project (`Your System Project`).

### Week 17 — Linked lists & stacks

* **Reading/Video**: CLRS or freeCodeCamp modules on lists/stacks.
* **Coding exercise**: Implement singly & doubly linked lists and stack API; add tests for head/tail cases.
* **Project task**: Add persistent dump of a list to `data/`.
* **Verification**: Unit tests pass & memory checks clean.
* **Journal/Teach**: Screencast pointer handling.

---

### Week 18 — Queues & circular buffers

* **Reading/Video**: Ring buffer articles & videos.
* **Coding exercise**: Implement circular buffer with bounded storage; add wraparound tests.
* **Project task**: Integrate circular buffer in a producer/consumer harness.
* **Verification**: Boundary tests pass; record microbench.
* **Journal/Teach**: Post: when to use ring buffer vs queue.

---

### Week 19 — Hash tables deep

* **Reading/Video**: Deep dive on collisions, load factor, deletion strategies.
* **Coding exercise**: Implement chaining + deletion & rehashing.
* **Project task**: Stress test with pathological inputs.
* **Verification**: Hash stress test CSV recorded.
* **Journal/Teach**: Write open-addressing vs chaining explainer.

---

### Week 20 — Binary Search Trees

* **Reading/Video**: BST invariants & traversal theory.
* **Coding exercise**: Implement BST insert/search/delete and traversals.
* **Project task**: Add traversal outputs for debugging.
* **Verification**: Tests validating tree after deletions.
* **Journal/Teach**: Compare recursion vs iterative implementations.

---

### Week 21 — Balanced trees (AVL)

* **Reading/Video**: AVL rotations & invariants.
* **Coding exercise**: Implement AVL insertion & rotations; maintain height invariants.
* **Project task**: Use AVL for ordered-key map in your project.
* **Verification**: Stress inserting sorted input and confirm height/log behavior.
* **Journal/Teach**: 10-minute screencast walking rotations.

---

### Week 22 — Heaps & priority queues

* **Reading/Video**: Heap theory & heapify.
* **Coding exercise**: Implement binary heap, `push/pop`, and heap-sort.
* **Project task**: Use heap to implement Dijkstra later.
* **Verification**: Bench heap-sort vs `std::sort` on distributions.
* **Journal/Teach**: Explain heap advantages for priority tasks.

---

### Week 23 — Tries & string DS

* **Reading/Video**: Trie & prefix trees.
* **Coding exercise**: Implement trie for ASCII; prefix search & auto-complete demo.
* **Project task**: Add CLI auto-complete.
* **Verification**: Memory & correctness for 50k simulated words.
* **Journal/Teach**: Blog post on tries & use cases.

---

### Week 24 — Union-Find (Disjoint sets)

* **Reading/Video**: Union-find with path compression.
* **Coding exercise**: Implement with union by rank; connectivity tests.
* **Project task**: Add graph connectivity checks.
* **Verification**: Tests show near-constant amortized behavior.
* **Journal/Teach**: Write about amortized inverse-Ackermann complexity.

---

### Week 25 — Sorting algorithms deep

* **Reading/Video**: Quicksort, mergesort, and their proofs.
* **Coding exercise**: Implement quicksort (median-of-three), mergesort, heapsort.
* **Project task**: Benchmark sorts on sorted, reverse, random inputs.
* **Verification**: Bench CSV & analysis.
* **Journal/Teach**: Explain pivot choices & stability tradeoffs.

---

### Week 26 — Graphs basics (BFS/DFS)

* **Reading/Video**: Graph representations & traversal.
* **Coding exercise**: Implement adjacency lists, BFS, DFS, cycle detection.
* **Project task**: Build a maze solver example.
* **Verification**: Traversal correctness and time measurements.
* **Journal/Teach**: Note graph memory layout tradeoffs.

---

### Week 27 — Dijkstra & A*

* **Reading/Video**: Dijkstra algorithm & heuristics for A*.
* **Coding exercise**: Implement Dijkstra using your heap.
* **Project task**: Integrate pathfinding into your persistent project (game or engine module).
* **Verification**: Pathfinding timings for grids up to 200×200.
* **Journal/Teach**: 10-minute screencast on Dijkstra + heuristics.

---

### Week 28 — Dynamic programming fundamentals

* **Reading/Video**: DP patterns: memoization & tabulation.
* **Coding exercise**: Solve classic DP problems (knapsack, edit distance).
* **Project task**: Add algorithm utilities module.
* **Verification**: Tests & runtime verification for increasing N.
* **Journal/Teach**: Map DP patterns to problem archetypes.

---

### Week 29 — Advanced graphs (MST)

* **Reading/Video**: Kruskal & Prim algorithms.
* **Coding exercise**: Implement Kruskal (with union-find) and Prim (with heap).
* **Project task**: Visualize MST for generated graphs.
* **Verification**: Bench on random graphs; validate MST weight.
* **Journal/Teach**: Short guide comparing Prim vs Kruskal.

---

### Week 30 — Complexity class review & proofs

* **Reading/Video**: Big-O, Big-Theta, amortized proofs overview.
* **Coding exercise**: Write formal amortized proofs for earlier structures (e.g., vector push).
* **Project task**: Update design docs to include complexity.
* **Verification**: Journal contains written proofs for 3 algorithms.
* **Journal/Teach**: Reflect on algorithmic tradeoffs you've learned.

---

### Week 31 — In-memory KV store (project)

* **Reading/Video**: Simple storage engine concepts (append-only log).
* **Coding exercise**: Build in-memory KV store with append-only log & compaction.
* **Project task**: CLI for `PUT/GET/DELETE`.
* **Verification**: Persistence replay after restart and unit tests.
* **Journal/Teach**: Blog post: how your KV store handles crashes.

---

### Week 32 — Phase B consolidation

* **Reading/Video**: Review DS modules and proofs.
* **Coding exercise**: Fix failing tests; ensure KV persistence works.
* **Project task**: Document DS implementations & bench results.
* **Verification**: All DS tests passing; KV persistence validated.
* **Journal/Teach**: Phase B reflection & 1-page summary.

---

# Phase C — Systems Programming in C++ (Weeks 33–48)

### Week 33 — Threads & mutexes

* **Reading/Video**: Concurrency basics (std::thread / std::mutex).
* **Coding exercise**: Implement a thread pool and task queue.
* **Project task**: Replace single-threaded KV API with thread-pool dispatch.
* **Verification**: Concurrent PUT/GET tests under MSVC / MinGW; use sanitizers to detect races.
* **Journal/Teach**: Screencast on race conditions & mutex usage.

---

### Week 34 — Atomics & memory ordering

* **Reading/Video**: `std::atomic` and memory orders overview.
* **Coding exercise**: Implement atomic counter and SPSC lock-free queue experiment.
* **Project task**: Microbench lock-free vs mutex queue.
* **Verification**: Stress test with multiple producers/consumers; save results.
* **Journal/Teach**: Note when lock-free helps vs complexity costs.

---

### Week 35 — Deadlocks & safe patterns

* **Reading/Video**: Deadlocks, condition variables, ordered locking.
* **Coding exercise**: Create an intentional deadlock and fix it (ordered locks or `try_lock`).
* **Project task**: Add condition variable workflows to task queue.
* **Verification**: Stress tests showing resolved deadlock scenarios.
* **Journal/Teach**: 1-page “deadlocks for humans”.

---

### Week 36 — Profiling basics (Windows)

* **Reading/Video**: Visual Studio Profiler & Windows Performance Analyzer basics.
* **Coding exercise**: Profile KV store under load, identify hotspots.
* **Project task**: Optimize one hotspot (avoid copies/reserve capacity).
* **Verification**: Save before/after profiler snapshots (`artifacts/week-36/`).
* **Journal/Teach**: Postmortem of a hotspot fix.

---

### Week 37 — Memory allocators & cache behavior

* **Reading/Video**: Allocator basics & cache locality.
* **Coding exercise**: Implement a slab/pool allocator for small objects.
* **Project task**: Replace `new/delete` hot paths with pool allocator.
* **Verification**: Measure memory usage & throughput pre/post.
* **Journal/Teach**: Screencast on cache friendliness.

---

### Week 38 — Async patterns & futures/promises

* **Reading/Video**: `std::future`, `std::promise`, and `std::async`.
* **Coding exercise**: Add async API to KV store returning futures.
* **Project task**: Build a client using futures for long ops.
* **Verification**: Tests for async correctness and cancellation handling.
* **Journal/Teach**: API design notes: sync vs async choices.

---

### Week 39 — Fault injection & robustness

* **Reading/Video**: Intro to chaos engineering (conceptual).
* **Coding exercise**: Add fault injection simulating disk errors & partial writes.
* **Project task**: Implement recovery logic for corrupted segments.
* **Verification**: Run recovery tests; document results.
* **Journal/Teach**: Blog post: design for failure.

---

### Week 40 — RPC & protocol design

* **Reading/Video**: Message framing & basic RPC patterns.
* **Coding exercise**: Design framing (length-prefixed or delimiter) and implement handler.
* **Project task**: Add binary/JSON RPC server handler and tests for pipelining.
* **Verification**: Unit tests for message boundaries & multi-request scenarios.
* **Journal/Teach**: Design doc explaining framing choices.

---

### Week 41 — Load harness & p99 measurement

* **Reading/Video**: How to design fair microbenchmarks.
* **Coding exercise**: Implement a load generator (multithreaded client) in C++ or Node.
* **Project task**: Run concurrent PUT/GET workloads; record p99 latency.
* **Verification**: Save CSV throughput vs concurrency to `bench/`.
* **Journal/Teach**: Write up load test results & implications.

---

### Week 42 — CI polish & code review

* **Reading/Video**: CI best practices & PR workflows.
* **Coding exercise**: Add GitHub Actions `windows-latest` job running build & tests.
* **Project task**: Create PR template & checklist; get one external reviewer.
* **Verification**: PR merged after addressing review; CI green.
* **Journal/Teach**: Document review feedback & how you addressed it.

---

### Week 43 — Core dumps & postmortem

* **Reading/Video**: How to generate/analyze `.dmp` on Windows (WinDbg basics).
* **Coding exercise**: Force a crash, capture `.dmp`, and analyze.
* **Project task**: Add crash-safe logging / backtrace generation.
* **Verification**: `.dmp` and analysis saved to `artifacts/week-43/`.
* **Journal/Teach**: Postmortem writeup for bug & fix.

---

### Week 44 — Security basics & input validation

* **Reading/Video**: OWASP Top10 overview (conceptual).
* **Coding exercise**: Harden RPC input validation and add auth token system.
* **Project task**: Add tests confirming invalid inputs are rejected.
* **Verification**: Security unit tests pass; audit notes saved.
* **Journal/Teach**: Short threat model for your service.

---

### Week 45 — Packaging & distribution (Windows)

* **Reading/Video**: Packaging basics (zip, simple install scripts).
* **Coding exercise**: Add `install.ps1` and `make package` steps via CMake.
* **Project task**: Create a release candidate zip & test install on a clean VM (or WSL).
* **Verification**: Install logs saved to `artifacts/week-45/install_log.txt`.
* **Journal/Teach**: Write install instructions for contributors.

---

### Week 46 — Instrumentation & metrics

* **Reading/Video**: Metrics basics (counters, histograms).
* **Coding exercise**: Expose `/metrics` HTTP endpoint with counters and histograms.
* **Project task**: Hook frontend to display basic metrics (later).
* **Verification**: Run load and verify metrics change accordingly.
* **Journal/Teach**: Document which metrics matter and why.

---

### Week 47 — Graceful shutdown & resource cleanup

* **Reading/Video**: Clean shutdown patterns and signal handling on Windows (Console Control Events).
* **Coding exercise**: Implement graceful shutdown & resource cleanup handlers.
* **Project task**: Add tests to simulate SIGTERM/Console Ctrl events.
* **Verification**: Long-running test (10+ mins) shows clean shutdown with no leaks.
* **Journal/Teach**: 5-min video on graceful shutdown patterns.

---

### Week 48 — Phase C checkpoint

* **Reading/Video**: Review concurrency, profiling, and stability notes.
* **Coding exercise**: Fix outstanding concurrency issues; consolidate profiler findings.
* **Project task**: Ensure multithreaded KV store stable under stress and CI green.
* **Verification**: Stress test logs + profiler snapshots in `artifacts/week-48/`.
* **Journal/Teach**: Phase C reflection and action items.

---

# Phase D — Python Deep Dive & Integration (Weeks 49–64)

### Week 49 — Python basics & environment

* **Reading/Video**: Python fundamentals; set up `pyenv`/venv on Windows.
* **Coding exercise**: Reimplement core DS in Python (list, deque, dict mimic); tests via `pytest`.
* **Project task**: Add `pytools/` folder that can talk to your C++ server (RPC/subprocess).
* **Verification**: `.\.venv\Scripts\Activate.ps1` then `pytest -q`.
* **Journal/Teach**: Compare Python lists to C++ vector (behavior & complexity).

---

### Week 50 — Python internals & `dis`

* **Reading/Video**: `dis` module & Python bytecode overview.
* **Coding exercise**: Inspect bytecode of small functions and write a tiny bytecode generator for arithmetic exprs.
* **Project task**: Add Python script calling C++ server and logging results.
* **Verification**: `python -m dis yourfunc` outputs opcodes; save analysis.
* **Journal/Teach**: Explain source → bytecode → execution flow.

---

### Week 51 — GIL & concurrency

* **Reading/Video**: GIL explanation and `multiprocessing` vs `threading` tradeoffs.
* **Coding exercise**: Benchmark CPU-bound vs IO-bound tasks with threads & processes.
* **Project task**: Add Python analytics worker using `multiprocessing` for CPU work.
* **Verification**: Compare throughput; save CSV to `bench/`.
* **Journal/Teach**: When to use threads vs processes on Windows.

---

### Week 52 — `asyncio` & event loop

* **Reading/Video**: `asyncio` core concepts.
* **Coding exercise**: Implement an async client that sends concurrent RPC requests to your C++ server.
* **Project task**: Integrate async worker with metrics reporting.
* **Verification**: Compare async throughput to threaded clients; document.
* **Journal/Teach**: 10-min screencast on `asyncio` basics.

---

### Week 53 — Packaging & distribution (Python)

* **Reading/Video**: `pyproject.toml` and modern packaging basics.
* **Coding exercise**: Package Python analytics module; install in fresh venv.
* **Project task**: Add packaging step to CI.
* **Verification**: `pip install .` in new venv and `pytest`.
* **Journal/Teach**: Packaging pitfalls & notes.

---

### Week 54 — Python profiling & optimization

* **Reading/Video**: `cProfile`, `timeit`, micro-optimizations.
* **Coding exercise**: Profile analytics worker; optimize hotspots (algorithmic or use C extensions if needed).
* **Project task**: Record profiling reports to `bench/`.
* **Verification**: Save `cProfile` output and optimized run times.
* **Journal/Teach**: “How I profiled the Python worker” blog post.

---

### Week 55 — C++ / Python interop

* **Reading/Video**: `pybind11` vs subprocess/IPC patterns.
* **Coding exercise**: Expose a C++ function to Python via `pybind11` (or use JSON RPC).
* **Project task**: Python script calls C++ logic directly via binding.
* **Verification**: Binding tests run in CI and memory checks pass.
* **Journal/Teach**: Tradeoffs: subprocess vs bindings.

---

### Week 56 — Type hints & static checking

* **Reading/Video**: Python type hints & mypy basics.
* **Coding exercise**: Annotate Python modules and add `mypy` to CI.
* **Project task**: Typecheck and fix issues.
* **Verification**: `mypy .` clean in CI.
* **Journal/Teach**: Short guide on benefits of static typing in Python.

---

### Week 57 — Metaclasses, descriptors & DSL patterns

* **Reading/Video**: Metaclasses & descriptors overview.
* **Coding exercise**: Build a decorator/registration DSL for analytics handlers.
* **Project task**: Use decorators for auto-registration of handlers in the Python module.
* **Verification**: Tests for registration & invocation order.
* **Journal/Teach**: Examples & pitfalls of metaclasses.

---

### Week 58 — Backpressure & queue management

* **Reading/Video**: Backpressure patterns & queue throttling.
* **Coding exercise**: Implement queue throttling and retries in Python worker.
* **Project task**: Add alerting if backlog grows past threshold (simple log threshold).
* **Verification**: Simulate burst load and capture throttling behavior.
* **Journal/Teach**: Post on designing backpressure.

---

### Week 59 — Documentation (Sphinx / MkDocs)

* **Reading/Video**: Sphinx or MkDocs guide.
* **Coding exercise**: Generate API docs for Python module and publish locally.
* **Project task**: Add docs build to CI.
* **Verification**: `mkdocs build` or `sphinx-build` output saved to `artifacts/docs/`.
* **Journal/Teach**: Document an API design choice.

---

### Week 60 — Python integration checkpoint

* **Reading/Video**: Review Python <> C++ integration notes.
* **Coding exercise**: Fix integration issues; ensure binding correctness and no memory leaks.
* **Project task**: Ensure Python tests + bindings run on `windows-latest` CI.
* **Verification**: CI green; coverage report added.
* **Journal/Teach**: Phase D reflection.

---

# Phase E — Web Stack & JS/TS Internals (Weeks 61–80)

### Week 61 — HTTP basics & DNS on Windows

* **Reading/Video**: Traversy Media HTTP crash course.
* **Coding exercise**: Implement a tiny HTTP client in Python and tiny HTTP server in C++ (sockets).
* **Project task**: Document request lifecycle in `journal.md`.
* **Verification**: `curl -v http://localhost:8080/` or PowerShell `Invoke-WebRequest -Uri http://localhost:8080/ -UseBasicParsing`.
* **Journal/Teach**: Draw the HTTP request/response flow.

---

### Week 62 — Static UI & hosting

* **Reading/Video**: HTML/CSS fundamentals (semantic markup & box model).
* **Coding exercise**: Build a static status dashboard (HTML/CSS).
* **Project task**: Serve static files from C++ HTTP server.
* **Verification**: Open the dashboard in browser; test mobile viewport sizes.
* **Journal/Teach**: Accessibility checklist used.

---

### Week 63 — Vanilla JS & DOM

* **Reading/Video**: freeCodeCamp JS fundamentals.
* **Coding exercise**: Implement DOM update logic to render metrics JSON.
* **Project task**: Add a control panel to dashboard that fetches `/metrics`.
* **Verification**: Use DevTools Network tab to confirm fetch and parse.
* **Journal/Teach**: 5-min demo showing DOM updates.

---

### Week 64 — Event loop internals (JS)

* **Reading/Video**: Event loop, microtask vs macrotask explanation.
* **Coding exercise**: Create examples with `setTimeout`, `Promise.then`, `async/await` to observe ordering.
* **Project task**: Refactor polling client to WebSocket (if available).
* **Verification**: Console timestamps showing ordering; save to `artifacts/`.
* **Journal/Teach**: Explain microtask queue behavior.

---

### Week 65 — TypeScript basics & bundling

* **Reading/Video**: TypeScript intro; `tsc` basics.
* **Coding exercise**: Convert frontend code to TypeScript modules; set up `esbuild` bundler.
* **Project task**: Add `npm` scripts for build/dev with sourcemaps.
* **Verification**: `npm run build` produces sourcemapped bundle; open in DevTools.
* **Journal/Teach**: Post on benefits of types in frontend code.

---

### Week 66 — Node.js backend & event loop

* **Reading/Video**: Node event loop model and single-threaded nature.
* **Coding exercise**: Create Node/TypeScript proxy that forwards to C++ server and adds auth middleware.
* **Project task**: Implement simple rate-limiting middleware.
* **Verification**: End-to-end request: browser → Node → C++ server works.
* **Journal/Teach**: Discuss Node event loop tradeoffs.

---

### Week 67 — WebSockets & realtime UI

* **Reading/Video**: WebSocket concepts & lifecycle.
* **Coding exercise**: Implement WebSocket server (Node) and client (TS) to stream metrics.
* **Project task**: Add live charts to dashboard (plain `<canvas>` or light library).
* **Verification**: Live chart updates under load; record p99 latency.
* **Journal/Teach**: 10-minute demo: live charting pipeline.

---

### Week 68 — TLS & CORS (local dev)

* **Reading/Video**: TLS basics & CORS explanation.
* **Coding exercise**: Create a self-signed certificate for localhost (OpenSSL/MSYS2) or use PowerShell `New-SelfSignedCertificate`.
* **Project task**: Configure Node & C++ servers to serve via HTTPS and set CORS headers properly.
* **Verification**: Browser shows secure connection & devtools show expected headers.
* **Journal/Teach**: Note CSP and CORS security implications.

---

### Week 69 — PostgreSQL basics

* **Reading/Video**: SQL & ACID fundamentals.
* **Coding exercise**: Design schema for users & metadata; write migration scripts.
* **Project task**: Connect Node backend to PostgreSQL and implement CRUD endpoints.
* **Verification**: `psql` or pgAdmin run queries; `EXPLAIN` query plan shown.
* **Journal/Teach**: Why indexing matters (example).

---

### Week 70 — Query planning & indexes

* **Reading/Video**: EXPLAIN ANALYZE & index theory.
* **Coding exercise**: Identify a slow query via logs and add appropriate index.
* **Project task**: Add slow query logging & a simple index maintenance script.
* **Verification**: Save before/after `EXPLAIN ANALYZE` outputs to `artifacts/week-70/`.
* **Journal/Teach**: Short writeup of index impact.

---

### Week 71 — Frontend memory leaks & profiling

* **Reading/Video**: Memory leak causes in browsers.
* **Coding exercise**: Profile the frontend in Chrome/Edge DevTools and fix leaks (unbound listeners, closures).
* **Project task**: Ensure dashboard survives long runs without memory growth.
* **Verification**: Heap snapshot after 30 mins shows no increasing trend.
* **Journal/Teach**: 5-min tutorial on detecting leaks.

---

### Week 72 — Load testing & capacity planning

* **Reading/Video**: Load testing fundamentals (k6 or custom Node harness).
* **Coding exercise**: Build a client simulator to emulate N concurrent clients.
* **Project task**: Run tests, record p95/p99 latency and throughput.
* **Verification**: CSV of concurrency vs latency saved to `bench/`.
* **Journal/Teach**: Capacity planning notes.

---

### Week 73 — Caching strategies & CDN concepts

* **Reading/Video**: HTTP caching headers, TTL, server caches.
* **Coding exercise**: Implement server cache for /metrics with TTL & cache-control headers.
* **Project task**: Measure reduced backend load & latencies.
* **Verification**: Compare load before/after caching; save graphs.
* **Journal/Teach**: Short guide on when caching helps.

---

### Week 74 — Observability: logs & tracing

* **Reading/Video**: Structured logging & request IDs basics.
* **Coding exercise**: Add structured JSON logs and simple trace IDs propagating through services.
* **Project task**: Add a local viewer (or parse scripts) to visualize traces.
* **Verification**: Sample trace shows timing breakdown saved in `artifacts/`.
* **Journal/Teach**: Why traces are valuable.

---

### Week 75 — Docker on Windows (WSL2 backend)

* **Reading/Video**: Docker Desktop + WSL2 guidance (Windows notes).
* **Coding exercise**: Create `Dockerfile` for C++ server and `docker-compose.yml` for full stack.
* **Project task**: Verify local stack brings up via Docker Desktop (WSL2).
* **Verification**: `docker-compose up` smoke tests pass; save logs.
* **Journal/Teach**: Document Docker quirks on Windows.

---

### Week 76 — UX & accessibility polish

* **Reading/Video**: UI clarity & keyboard accessibility basics.
* **Coding exercise**: Polish dashboard UI, ensure keyboard navigation and color contrast.
* **Project task**: Conduct a small user test (friend) and record feedback.
* **Verification**: Log UX fixes & iterate.
* **Journal/Teach**: Summarize user feedback & changes.

---

### Week 77 — Staging & release candidate

* **Reading/Video**: Release best practices & semantic versioning.
* **Coding exercise**: Prepare staging build & deploy on VM or local Docker.
* **Project task**: Run integration tests on staging and fix deployment issues.
* **Verification**: Staging smoke tests pass; save `artifacts/week-77/staging_report.md`.
* **Journal/Teach**: Release notes draft.

---

### Week 78 — Performance audit & bundle optimizations

* **Reading/Video**: Lighthouse / manual performance checklist.
* **Coding exercise**: Reduce JS bundle size (tree shaking, code splitting) and improve LCP.
* **Project task**: Document improvements and final scores.
* **Verification**: Save Lighthouse report to `artifacts/week-78/`.
* **Journal/Teach**: List tradeoffs made.

---

### Week 79 — Web checkpoint

* **Reading/Video**: Fullstack review notes.
* **Coding exercise**: Run end-to-end tests & memory/latency checks; fix issues.
* **Project task**: Confirm metrics/logs/tracing pipeline works under moderate load.
* **Verification**: Save end-to-end test logs and p99 latencies.
* **Journal/Teach**: Web stack reflection.

---

### Week 80 — Optional: TypeScript backend migration

* **Reading/Video**: TypeScript server patterns & typing strategies.
* **Coding exercise**: Migrate a critical Node module to TypeScript and add types.
* **Project task**: Ensure types & unit tests pass.
* **Verification**: `tsc` + unit tests pass in CI.
* **Journal/Teach**: Reflection on the benefits of TypeScript in your backend.

---

# Phase F — Advanced Systems, Compilers, OS Basics, Polish (Weeks 81–104)

### Week 81 — Compilers: lexing & parsing

* **Reading/Video**: Intro to compilers: lexing & parsing tutorials.
* **Coding exercise**: Design a tiny expression grammar and implement a lexer (Python or C++).
* **Project task**: Create AST nodes for `1 + 2 * (3 - 4)`.
* **Verification**: Unit tests for lexer & parser; print AST samples.
* **Journal/Teach**: Blog post: tokens → AST.

---

### Week 82 — Tiny interpreter & REPL

* **Reading/Video**: AST evaluation patterns & scoping.
* **Coding exercise**: Implement evaluator supporting variables and functions; add REPL.
* **Project task**: Add language tests & examples.
* **Verification**: Run REPL examples and unit tests.
* **Journal/Teach**: Notes on scoping & closures.

---

### Week 83 — Bytecode VM (optional stretch)

* **Reading/Video**: Stack VM architecture tutorials.
* **Coding exercise**: Compile AST to bytecode & implement a stack VM.
* **Project task**: Compare interpreter vs VM performance on microbenchmarks.
* **Verification**: Correctness tests & microbench CSV saved.
* **Journal/Teach**: 10-min screencast: building a tiny VM.

---

### Week 84 — OS basics: processes & syscalls

* **Reading/Video**: Processes, `CreateProcess` & `WaitForSingleObject` (Windows) or `fork/exec` (WSL).
* **Coding exercise**: Implement small supervisor script that restarts child process on crash.
* **Project task**: Add supervisor to your project to auto-restart the server.
* **Verification**: Demonstrate restart on crash and save logs.
* **Journal/Teach**: Summarize process creation flow.

---

### Week 85 — Memory-mapped IO

* **Reading/Video**: Memory mapping concepts (`CreateFileMapping` / `MapViewOfFile` on Windows or `mmap` on POSIX).
* **Coding exercise**: Experiment with `mmap` or Windows mapping APIs to memory-map files.
* **Project task**: Use memory-mapped files for a fast persistence module (optional).
* **Verification**: Tests for file-backed mapping & crash recovery.
* **Journal/Teach**: Note when `mmap` is appropriate.

---

### Week 86 — Distributed systems design (conceptual)

* **Reading/Video**: Raft overview & eventual consistency (conceptual).
* **Coding exercise**: (Design) Draft replication strategy for KV store (no full implementation required).
* **Project task**: Produce a 2-page design doc with failure modes & replication plan.
* **Verification**: Design doc reviewed by a peer/mentor.
* **Journal/Teach**: Reflect on tradeoffs between consistency & availability.

---

### Week 87 — Tracing & instrumentation deep dive

* **Reading/Video**: Distributed tracing basics and span design.
* **Coding exercise**: Add span timing for RPC calls and propagate trace IDs.
* **Project task**: Visualize a simple trace in your frontend dashboard.
* **Verification**: Example trace showing timing breakdown saved to `artifacts/week-87/`.
* **Journal/Teach**: Blog post: Why tracing matters.

---

### Week 88 — Fuzz testing & hardening

* **Reading/Video**: Fuzz testing intro (boofuzz or custom harness).
* **Coding exercise**: Add fuzz harness for RPC parser; run fuzzing for X minutes.
* **Project task**: Fix crashes found by fuzzing; add tests to prevent regressions.
* **Verification**: Fuzz run logs & fixes committed.
* **Journal/Teach**: Postmortem of a bug found & fixed by fuzzing.

---

### Week 89 — Final performance tuning

* **Reading/Video**: Performance tuning checklist & techniques.
* **Coding exercise**: Optimize the top 1–2 hotspots from profiling.
* **Project task**: Re-run benchmarks and record before/after CSV + charts.
* **Verification**: Show measurable improvements in `bench/`.
* **Journal/Teach**: Explain optimizations & why they help.

---

### Week 90 — Documentation & README polish

* **Reading/Video**: Docs best practices & architecture writing.
* **Coding exercise**: Finalize README, architecture doc (10 pages), API docs, and contribution guide.
* **Project task**: Create a “Getting started” tutorial for contributors.
* **Verification**: On a fresh VM/container, follow tutorial and fix missing steps.
* **Journal/Teach**: Postmortem draft started.

---

### Week 91 — Release prep & packaging

* **Reading/Video**: Release workflows & semantic versioning.
* **Coding exercise**: Tag release, create a release zip/installer (simple).
* **Project task**: Build release artifacts and test installation on fresh Windows VM.
* **Verification**: Install log & smoke test saved.
* **Journal/Teach**: Release notes for your project.

---

### Week 92 — Teaching artifact #1 (long tutorial)

* **Reading/Video**: Review teaching methods & write-up structure.
* **Coding exercise**: Draft a long tutorial teaching a deep topic (e.g., hash tables end-to-end).
* **Project task**: Publish tutorial (blog post or repo `docs/`).
* **Verification**: Tutorial published and linked in `README.md`.
* **Journal/Teach**: Collect feedback & iterate.

---

### Week 93 — Teaching artifact #2 (screencast)

* **Reading/Video**: Video production basics (short).
* **Coding exercise**: Produce a polished 20–30 min screencast teaching a subsystem.
* **Project task**: Upload or store the video and link in repo.
* **Verification**: Video uploaded & feedback collected.
* **Journal/Teach**: Summarize viewer feedback.

---

### Week 94 — Community review & mentorship

* **Reading/Video**: How to solicit useful code reviews.
* **Coding exercise**: Open a “request for review” in developer forum & respond to comments.
* **Project task**: Address at least one external review comment with a PR.
* **Verification**: Reviewer feedback addressed & PR merged.
* **Journal/Teach**: Reflect on review & what you learned.

---

### Week 95 — Architecture doc finalization

* **Reading/Video**: Architecture doc examples & diagrams.
* **Coding exercise**: Finalize 10-page architecture + diagrams.
* **Project task**: Share doc with a mentor and incorporate feedback.
* **Verification**: Mentor confirms understandability in writing.
* **Journal/Teach**: Extract slides summarizing the doc.

---

### Week 96 — Final tests & CI

* **Reading/Video**: CI best practices & multi-platform testing.
* **Coding exercise**: Ensure CI runs on `windows-latest` and `ubuntu-latest`; fix platform edge cases.
* **Project task**: Add lighter benchmark job to CI (smoke run).
* **Verification**: CI passing on both platforms.
* **Journal/Teach**: Checklist of CI improvements.

---

### Week 97 — Launch & outreach

* **Reading/Video**: How to write an effective launch post.
* **Coding exercise**: Prepare announcement & share repo + tutorial.
* **Project task**: Present project to school club or online community.
* **Verification**: Track issues & community responses for the first 2 weeks.
* **Journal/Teach**: Record Q&A & feedback.

---

### Week 98 — Reimplement core DS in another language

* **Reading/Video**: Language-specific notes for target language (Python/TS).
* **Coding exercise**: 24-hour challenge: reimplement a DS (e.g., AVL or hash map) from memory.
* **Project task**: Run tests & compare idiomatic differences.
* **Verification**: Tests pass; save step-by-step notes to `journal.md`.
* **Journal/Teach**: Comparative post: C++ vs Python/TS implementations.

---

### Week 99 — Optional deep dive (Rust/Go or compilers)

* **Reading/Video**: Intro tutorials for chosen deep dive (Rust/Go).
* **Coding exercise**: 2-week focused prototype (small project).
* **Project task**: Add small POC and write about how the mental model differs.
* **Verification**: Working prototype + short writeup.
* **Journal/Teach**: Note mental model shifts.

---

### Week 100 — Reflection & next roadmap

* **Reading/Video**: Reflective articles on learning & skill growth.
* **Coding exercise**: None required — consolidate artifacts.
* **Project task**: Write 2-page reflection describing growth, gaps, and next 12 months.
* **Verification**: Reflection saved to `journal.md`.
* **Journal/Teach**: Present reflection to a mentor.

---

### Week 101 — Mentorship (teach others)

* **Reading/Video**: How to mentor effectively.
* **Coding exercise**: Mentor a beginner for 4 weeks (pair programming sessions).
* **Project task**: Help mentee produce a mini-project and reflection.
* **Verification**: Mentee produces a small project & reflection.
* **Journal/Teach**: Reflect on what mentoring taught you.

---

### Week 102 — Portfolio & CV

* **Reading/Video**: Portfolio design & concise CV tips.
* **Coding exercise**: Build portfolio page (GitHub Pages) showcasing your projects & artifacts.
* **Project task**: Create a one-page programming CV (PDF) to share.
* **Verification**: Portfolio hosted & CV downloadable.
* **Journal/Teach**: Present portfolio to a mentor & collect feedback.

---

### Week 103 — Final presentation

* **Reading/Video**: Presentation best practices.
* **Coding exercise**: Prepare a 30–45 minute talk showing architecture, demos, and lessons.
* **Project task**: Deliver the presentation to peers/online community.
* **Verification**: Record of the talk and feedback saved to `artifacts/week-103/`.
* **Journal/Teach**: Summarize audience questions and followups.

---

### Week 104 — Wrap-up & maintenance plan

* **Reading/Video**: Maintenance & roadmap planning.
* **Coding exercise**: Finalize backlog and create a 6-month maintenance roadmap.
* **Project task**: Ensure all core tests pass; finalize docs and release artifacts.
* **Verification**: `artifacts/final_checklist.md` with green checks.
* **Journal/Teach**: Final “How I learned full mastery” post + next steps.

---

## Ongoing micro-habits (throughout all 104 weeks)

* Weekly: get at least one external code review on major PRs.
* Monthly: teach (blog post or 10–20 min screencast).
* Quarterly: external mentor review of architecture docs.
* Every week: update `journal.md` with concept, diagram, and question.

---

## Windows-specific verification commands (copy into PowerShell or MSYS2 as needed)

**MSVC / PowerShell build**

```powershell
cmake -S . -B build -G "Visual Studio 17 2022" -A x64
cmake --build build --config Debug
.\build\Debug\run.exe
```

**MSYS2 / MinGW64 build (example)**

```bash
g++ -std=c++20 -O0 -g -fsanitize=address,undefined -fno-omit-frame-pointer src/*.cpp -Iinclude -o bin/run.exe
./bin/run.exe
```

**Python venv on Windows (PowerShell)**

```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
pip install -r requirements.txt
pytest -q
```

**Simple PowerShell HTTP health test**

```powershell
1..50 | ForEach-Object { Invoke-WebRequest -Uri "http://localhost:8080/health" -UseBasicParsing -TimeoutSec 5 } 
```

**PowerShell verification script (example)**

```powershell
cmake -S . -B build -G "Visual Studio 17 2022" -A x64
cmake --build build --config Debug
cd build
ctest -C Debug --output-on-failure
```

---

