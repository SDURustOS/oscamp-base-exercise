# OS Camp - Rust & OS Advanced Experiments
 
A Rust advanced and operating system introductory exercise repository in the style of [rustlings](https://github.com/rust-lang/rustlings).
Learn Rust concurrency programming, async programming, `no_std` development, and operating system core concepts through completing code and passing tests.

## Prerequisites

- Rust toolchain (stable, >= 1.75)
- Linux environment: most exercises target x86_64; **Module 4 (context switching) only supports riscv64** and requires a riscv64 environment or QEMU user-mode emulation

```bash
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
```

## Exercise Structure

**6 modules, 23 exercises** in total, from easy to advanced:

### Module 1: Concurrency (Synchronous) — `01_concurrency_sync/`

| # | Exercise | Concepts |
|---|----------|----------|
| 1 | `01_thread_spawn` | `thread::spawn`, `move` closures, `join` |
| 2 | `02_mutex_counter` | `Arc<Mutex<T>>`, shared state concurrency |
| 3 | `03_channel` | `mpsc::channel`, multiple producer pattern |
| 4 | `04_process_pipe` | `Command`, `Stdio::piped()`, process pipes |

### Module 2: no_std Development — `02_no_std_dev/`

| # | Exercise | Concepts |
|---|----------|----------|
| 1 | `01_mem_primitives` | `no_std` memory primitives: memcpy, memset, memmove, strlen, strcmp |
| 2 | `02_bump_allocator` | `GlobalAlloc` trait, Bump allocator, CAS-based thread safety |
| 3 | `03_free_list_allocator` | Free-list allocator, intrusive linked list, first-fit strategy |
| 4 | `04_syscall_wrapper` | Cross-arch syscall ABI (x86_64/aarch64/riscv64), inline assembly |
| 5 | `05_fd_table` | File descriptor table, `Arc<dyn File>`, fd reuse strategy |

### Module 3: OS Concurrency Advanced — `03_os_concurrency/`

| # | Exercise | Concepts |
|---|----------|----------|
| 1 | `01_atomic_counter` | `AtomicU64`, `fetch_add`, CAS loop |
| 2 | `02_atomic_ordering` | Memory ordering, Release-Acquire, `OnceCell` |
| 3 | `03_spinlock` | Spinlock implementation, `compare_exchange`, `spin_loop` |
| 4 | `04_spinlock_guard` | RAII guard, `Deref`/`DerefMut`/`Drop` |
| 5 | `05_rwlock` | Writer-priority read-write lock from scratch (no `std::sync::RwLock`) |

### Module 4: Context Switching — `04_context_switch/` (riscv64 only)

| # | Exercise | Concepts |
|---|----------|----------|
| 1 | `01_stack_coroutine` | Callee-saved registers, stack frames, context switching |
| 2 | `02_green_threads` | Green thread scheduler, cooperative scheduling, yield |

Module 4 only runs on **riscv64**. Run `./check.sh` or use the `oscamp` CLI as with the rest of the repository — no separate scripts needed. See `exercises/04_context_switch/README.md` for details.

### Module 5: Async Programming — `05_async_programming/`

| # | Exercise | Concepts |
|---|----------|----------|
| 1 | `01_basic_future` | Manual implementation of `Future` trait, `Poll`, `Waker` |
| 2 | `02_tokio_tasks` | `tokio::spawn`, `JoinHandle`, concurrent tasks |
| 3 | `03_async_channel` | `tokio::sync::mpsc`, async producer-consumer |
| 4 | `04_select_timeout` | `tokio::select!`, timeout control, race execution |

### Module 6: Page Tables — `06_page_table/`

| # | Exercise | Concepts |
|---|----------|----------|
| 1 | `01_pte_flags` | SV39 PTE bit layout, bit operations to construct/parse page table entries |
| 2 | `02_page_table_walk` | Single-level page tables, VPN/offset splitting, address translation, page faults |
| 3 | `03_multi_level_pt` | SV39 three-level page tables, page table walk, huge pages (2MB) mapping |
| 4 | `04_tlb_sim` | TLB lookup/insert/FIFO replacement, flush (all/by page/by ASID), MMU simulation |


# Getting Started

## Step 1. Create Your Own Repository

Open the course template repository.

Click:

```text
Use this template
```

Then choose:

```text
Create a new repository
```

Repository Owner:

```
Your GitHub Account
```

Repository Name (recommended):

```
oscamp-<your-github-username>
```

Example:

```
oscamp-Bitter127
```

Create the repository.

---

## Step 2. Clone Your Repository

```bash
git clone https://github.com/<your-github-username>/<repository>.git

cd <repository>
```

---

## Step 3. Build the Interactive Tool

```bash
cargo build -p oscamp-cli
```

---

## Step 4. Start Learning

Start watch mode:

```bash
./target/debug/oscamp watch
```

The tool automatically:

* detects file changes
* reruns tests
* tracks progress
* jumps to the next exercise

---

# Interactive CLI

Built-in interactive terminal tool similar to rustlings, supporting real-time file watching and progress tracking:

```bash
oscamp              # Start interactive watch mode (default)
oscamp watch        # Same as above
oscamp list         # View completion status of all exercises
oscamp check        # Check all exercises in batch
oscamp run <pkg>    # Run tests for specified exercise
oscamp hint <pkg>   # View exercise hint
oscamp help         # Show help
```

### Watch Mode Features

- **Automatic file change detection**: Automatically re-run tests after saving files
- **Auto-jump**: Automatically jump to next unfinished exercise after current one passes
- **Real-time progress bar**: Show overall completion progress
- **Shortcuts**:
  - `h` — View hint for current exercise
  - `l` — View list of all exercises
  - `n` / `p` — Next / Previous exercise
  - `r` / `Enter` — Re-run tests
  - `q` / `Esc` — Quit
---

# Manual Testing

Run one exercise:

```bash
cargo test -p thread_spawn
```

Run with output:

```bash
cargo test -p thread_spawn -- --nocapture
```

Run all exercises:

```bash
cargo test --workspace
```

---

# Recommended Workflow

For each exercise:

1. Open `src/lib.rs`
2. Read the comments
3. Find `todo!()`
4. Implement the missing code
5. Save the file
6. Re-run tests
7. Continue to the next exercise

---

# GitHub Actions Auto Grading

Every push to the **main** branch automatically triggers GitHub Actions.

The workflow will:

* Build the project
* Run all tests
* Execute the grading script
* Calculate your score
* Generate a grading report

---

# Submit Your Work

After completing one or more exercises:

```bash
git add .

git commit -m "Finish Module"

git push origin main
```

After pushing:

Open your repository:

```text
Actions
```

Select:

```text
OSCamp Autograding
```

Wait until the workflow finishes.

You can then view:

* Passed exercises
* Failed exercises
* Total score

---

# Submit Repository

After finishing the assignment, submit your repository URL to the instructor.

Example:

```text
https://github.com/Bitter127/oscamp-Bitter127
```

---

# Frequently Asked Questions

## GitHub Actions is not running

Please check:

* Did you push to the `main` branch?
* Did you successfully push to GitHub?
* Is GitHub Actions enabled for your repository?

---

## GitHub Actions failed

Open:

```text
Actions
→ OSCamp Autograding
```

Expand the failed step and inspect the log.

---

## Local tests pass but GitHub Actions fail

Common causes include:

* Missing files
* Environment differences
* Forgot to push the latest commit

Always ensure you have pushed the newest code before checking GitHub Actions.

---



## Notes

- Some exercises (e.g., Module 2 syscall wrapper, Module 4 assembly) require a **Linux** environment; Module 4 only supports **riscv64**
- It is recommended to complete exercises in module order; within each module, exercises progress from easy to advanced

## License

MIT

