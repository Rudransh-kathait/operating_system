# Operating Systems Lab Programs

A collection of 11 Python programs demonstrating common Operating Systems concepts and algorithms. The examples are provided in the Jupyter notebook [`os_program.ipynb`](os_program.ipynb).

> **Adaptation and attribution:** This notebook is a lightly refactored adaptation of the notebook supplied as the source for this project. The uploaded source contained a Google Colab link to `Bhoomii22/os_assignment`. Before redistributing this work publicly, check the original repository's license and permissions, and retain any credit required by that license. This project does not claim that derived material is wholly original.

## Programs included

| No. | Program | Concepts demonstrated |
|---:|---|---|
| 1 | Linux process system calls | Process creation with `fork()`, program replacement with `exec()`, and parent synchronization with `wait()` |
| 2 | Thread creation | Creating, starting, and joining Python threads with `threading` |
| 3 | CPU scheduling | First Come First Served (FCFS), non-preemptive Shortest Job First (SJF), non-preemptive Priority Scheduling, and Round Robin |
| 4 | Producer-Consumer | Bounded circular buffer coordinated with semaphores |
| 5 | Readers-Writers | Shared readers and exclusive writer access using semaphores |
| 6 | Dining Philosophers | Fork semaphores and a room semaphore to avoid circular wait |
| 7 | Banker's Algorithm | Safe-state checking and resource-request handling for deadlock avoidance |
| 8 | Contiguous memory allocation | First Fit, Best Fit, and Worst Fit |
| 9 | Page replacement | FIFO, LRU, and Optimal page replacement |
| 10 | Disk scheduling | FCFS, SSTF, SCAN, and C-SCAN |
| 11 | File allocation | Contiguous, linked, and indexed allocation on a simulated disk |

## Requirements

- Python 3
- Jupyter Notebook or JupyterLab, or a Google Colab account
- No third-party Python packages are required; the programs use Python's standard library
- A Unix-like operating system (such as Linux) for Program 1, because it calls `os.fork()`

**Note about Program 2:** It demonstrates Python's `threading` module. It is not a direct implementation of POSIX `pthread` APIs.

## Run the notebook

### Option 1: Google Colab

1. Open [Google Colab](https://colab.research.google.com/).
2. Select **File → Upload notebook**.
3. Upload `os_program.ipynb`.
4. Run cells from top to bottom, or use **Runtime → Run all**.
5. Enter the requested values when an interactive cell prompts for input.

### Option 2: Jupyter Notebook / JupyterLab

1. Install Jupyter if it is not already installed:

   ```bash
   python -m pip install notebook
   ```

2. Place `os_program.ipynb` in your working directory.
3. Start Jupyter:

   ```bash
   jupyter notebook
   ```

4. Open `os_program.ipynb` in the browser and run the cells.

### Run individual programs

The notebook is organized into a Markdown heading and a code cell for each program. Run the code cell below the relevant heading. Programs that use `input()` will ask for their data during execution.

For Program 1, use Linux or another Unix-like system that supports `fork()`. Running `fork()` from a multi-threaded notebook kernel can produce runtime warnings; running it from a normal Python process in a Linux terminal is preferable:

```bash
python program1_process_system_calls.py
```

The standalone filename above is an example only; the supplied project currently contains the combined notebook rather than separate `.py` files.

## Sample data and verification

The notebook includes sample input instructions alongside the interactive programs, plus verification notes and expected results. Some recorded checks include:

### CPU scheduling sample

The saved sample data uses four processes:

| Process | Arrival time | Burst time | Priority |
|---:|---:|---:|---:|
| P1 | 0 | 5 | 2 |
| P2 | 1 | 3 | 1 |
| P3 | 2 | 8 | 3 |
| P4 | 4 | 3 | 4 |

With Round Robin, the sample uses a time quantum of `2`.

| Choice | Algorithm | Average waiting time | Average turnaround time |
|---:|---|---:|---:|
| 1 | FCFS | 5.50 | 10.25 |
| 2 | SJF | 4.25 | 9.00 |
| 3 | Priority | 5.50 | 10.25 |
| 4 | Round Robin (quantum 2) | 8.25 | 13.00 |

### Other recorded sample results

| Program | Recorded result |
|---|---|
| Banker's Algorithm | Safe sequence: `P1 P3 P4 P0 P2`; the sample request for P1 (`1 0 2`) is granted safely |
| Page replacement | FIFO: 10 page faults; LRU: 9; Optimal: 7 |
| Disk scheduling | FCFS: 608; SSTF: 291; SCAN: 329; C-SCAN: 380 cylinders of head movement |
| File allocation | Linked-allocation sample includes chains `0 -> 1 -> 2` and `3 -> 4 -> 5 -> 6` |

The notebook's verification notes report that the sample runs completed with exit code `0`. CPU scheduling choices and file-allocation menu options were also checked individually. The order of printed messages in concurrent programs (Programs 2, 4, 5, and 6) can vary from run to run; exact line ordering is not guaranteed.

These are sample-case checks, not proof that every possible input or edge case has been tested.

## Important implementation notes

- Program 1 uses operating-system process calls and is platform-dependent.
- Program 2 uses Python threads, not POSIX pthreads.
- Programs 4–6 are concurrency demonstrations. Thread scheduling can change the order of console messages.
- Program 11 simulates allocation in an in-memory disk-block array; it does not create real files on the computer's filesystem.
- Interactive examples expect inputs in the format requested by their prompts. Use non-negative values and valid menu selections where applicable.

## Repository structure

If you keep the notebook and this README in the same folder, the project can be as simple as:

```text
operating-systems-lab/
├── README.md
└── os_program.ipynb
```

## License

No license is declared by this README. Check the source notebook's original license and permissions before making this repository public or applying a new license to the adapted material.
