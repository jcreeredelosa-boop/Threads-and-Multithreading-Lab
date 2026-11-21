# Laboratory Guide: Implementing Threads and Multithreading

## Before you begin
1. Install Python 3.x.
2. Open this folder in Visual Studio Code.
3. Open Terminal > New Terminal.
4. Check Python is available by running `python --version`.

## Task 1 — Single Thread
Run:
`python task1_single_thread.py`

Expected output:
```text
Number: 1
Number: 2
Number: 3
Number: 4
Number: 5
Program completed.
```

Guide questions:
1. What is the purpose of `threading.Thread()`?
   - It creates a new thread that can execute a specified function.
2. What happens when `start()` is executed?
   - It starts the thread and allows its assigned function to run.
3. What is the purpose of `join()`?
   - It makes the calling thread wait until the specified thread finishes.
4. What happens if `join()` is removed?
   - The main program does not wait for that thread and may continue while it is still running.

## Task 2 — Multiple Threads
Run:
`python task2_multiple_threads.py`

Sample output (the order may vary):
```text
Thread 1: 1
Thread 2: 1
Thread 1: 2
Thread 2: 2
Thread 1: 3
Thread 2: 3
Thread 1: 4
Thread 2: 4
Thread 1: 5
Thread 2: 5
Both threads completed.
```

Guide questions:
1. How many threads are created?
   - Two worker threads are created.
2. Do the two threads execute independently?
   - Yes. Each executes its own function, while sharing the same process.
3. Why might the output order change?
   - The operating system scheduler and runtime determine when each thread runs.
4. What is the difference between sequential and concurrent execution?
   - Sequential execution performs tasks one after another. Concurrent execution allows multiple tasks to make progress during overlapping periods.

## Task 3 — Synchronization using `join()`
Run:
`python task3_thread_synchronization.py`

Expected output:
```text
Downloading file...
Main program is waiting...
Download completed.
Main program continues.
```

Experiment:
1. Open `task3_thread_synchronization.py`.
2. Temporarily remove or comment out `t1.join()`.
3. Run the program again and observe the order. The main program may continue before the download thread finishes.
4. Restore `t1.join()` before committing/submitting the final version.

Guide questions:
1. Why does the main program wait when `join()` is used?
   - `join()` blocks the calling thread until the target thread completes.
2. What happens when `join()` is removed?
   - The main program continues without waiting for the worker thread.
3. When is thread synchronization necessary?
   - When later work depends on another thread finishing, or when threads coordinate access to shared data.

## Task 4 — Shared resources and locks
Run:
`python task4_thread_lock.py`

Expected output:
```text
Final Counter: 200000
```

Experiment:
1. Temporarily remove the `with lock:` line and unindent `counter += 1`.
2. Run the program several times and observe the result.
3. Restore the lock before committing/submitting the final version.

Note: A lost update is not guaranteed to appear on every run or every Python implementation. The lock protects the critical section regardless.

Guide questions:
1. What is a shared resource?
   - Data or an object that multiple threads can access.
2. What is a race condition?
   - A situation where the result depends on the timing or interleaving of concurrent operations, potentially producing incorrect results.
3. What is the purpose of `threading.Lock()`?
   - It provides mutual exclusion so only one thread at a time can enter a protected section.
4. What is a critical section?
   - A part of a program that accesses or modifies shared data and needs protection.
5. Why is synchronization important?
   - It helps prevent conflicting updates and protects data consistency.

## General guide questions

1. **What is the difference between a process and a thread?**  
   A process is an executing program with its own memory space and resources. A thread is an execution unit within a process. Threads in one process share memory and resources.

2. **What are the advantages of multithreading?**  
   It can improve responsiveness, allow tasks to make progress concurrently, and help structure programs that perform waiting and background work.

3. **How does multithreading improve application responsiveness?**  
   A program can perform background work without making its user-facing thread wait for every operation.

4. **What is the difference between concurrency and parallelism?**  
   Concurrency means tasks make progress over overlapping periods. Parallelism means tasks execute at the same instant on separate processing resources.

5. **Why is a lock necessary when multiple threads access shared data?**  
   A lock protects a critical section from simultaneous entry and helps prevent race conditions.

6. **What might happen if a thread is not properly synchronized?**  
   The program may produce inconsistent data, race conditions, or unexpected behavior.

7. **Can multiple threads execute simultaneously on a single-core processor? Explain.**  
   A single core executes only one thread at an instant, but rapid context switching lets multiple threads make concurrent progress.

8. **How does the operating system manage kernel-level threads?**  
   The OS scheduler manages their execution, assigns CPU time, performs context switches, and handles scheduling priorities and states.

## Screenshots and submission
Capture a screenshot of the code and terminal output for each of the four tasks. Save them in this folder, for example:
- `task1_screenshot.png`
- `task2_screenshot.png`
- `task3_screenshot.png`
- `task4_screenshot.png`

Before submitting, confirm that Task 3 has `t1.join()` restored and Task 4 uses `with lock:`. Update the student information in `README.md`, push all files to your public GitHub repository, and submit the repository URL in Google Classroom.
