# YACLOCK: Enhanced PostgreSQL Buffer Replacement Policy

This project introduces **YACLOCK (Yet Another Clock)**, a custom buffer replacement policy for PostgreSQL 17.6. It demonstrates modifications to PostgreSQL’s buffer manager to improve memory management efficiency in database systems.

## Overview

PostgreSQL uses shared buffers to store frequently accessed disk pages in memory. By default, it implements a variant of the Clock algorithm for buffer replacement. YACLOCK extends this by:

- Maintaining a circular queue of buffer frames.
- Using a reference bit (`refBit`) per buffer to track usage.
- Employing a clock-hand pointer (`next`) to efficiently identify victim buffers for eviction.
- Handling concurrent access with PostgreSQL’s shared memory locks.

This allows more fine-grained control over buffer replacement, improving buffer hit ratios and transaction throughput in certain workloads.

## Features

- Fully implemented **YACLOCK replacement policy** integrated with PostgreSQL.
- Benchmarking scripts to compare YACLOCK against the default Clock policy.
- Automated test cases validating correct behavior for pin/unpin operations on pages.
- Configurable PostgreSQL server setup using included scripts (`install.sh`, `settings.sh`).

## Installation & Setup

1. Clone this repository:
   ```bash
   git clone https://github.com/<username>/yaclock-postgresql.git
   cd yaclock-postgresql
````

2. Install PostgreSQL 17.6 from source:

   ```bash
   ./install.sh
   source ~/.bash_profile
   ```

3. Compile the YACLOCK buffer manager:

   ```bash
   make freelist_yaclock.o
   make yaclock
   ```

4. Run tests to ensure correctness:

   ```bash
   ./test-yaclock.sh
   ./diff.sh
   ```

5. Benchmark performance:

   ```bash
   ./part3.sh
   ```

## File Structure

* `freelist_yaclock.c` – Implementation of the YACLOCK policy.
* `bufmgr_yaclock.c` – Modified buffer manager supporting YACLOCK.
* `test_bufmgr/` – Test cases for verifying buffer operations.
* `testresults-yaclock-soln/` – Reference results for validation.
* Scripts: `install.sh`, `part1.sh`, `part3.sh`, `test-yaclock.sh`, `diff.sh`.

## Performance

YACLOCK aims to improve PostgreSQL’s buffer hit ratio by minimizing unnecessary disk I/O while maintaining thread-safe access to shared buffers. Performance results can be generated using the included benchmarking scripts.

## Contributing

Contributions and optimizations are welcome. Please ensure that all changes preserve correct behavior of buffer management and shared memory synchronization.

## License

This project is open source and available under the MIT License.

```

---

If you want, I can also create a **shorter, punchier version of the README** that’s more GitHub-friendly with badges and highlights for performance/tech stack, which often looks nicer for recruiters or open-source viewers.  

Do you want me to do that?
```
