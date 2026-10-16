# 💽 Disk Scheduling Algorithm Visualizer

An interactive, browser-based tool that animates how an operating system's disk scheduler moves the read/write head across cylinders for **FCFS, SSTF, SCAN, C-SCAN, LOOK and C-LOOK**, and compares their total head movement.

## Features
- Custom request queue, initial head position, disk size and direction
- Step-by-step animated head-movement chart
- Live metrics: total head movement, average seek, requests served
- Side-by-side comparison of all six algorithms (best one highlighted)
- Light/dark theme, responsive layout, no dependencies

## Setup & Run
No installation or compilation is needed (plain HTML + JavaScript).
```bash
git clone <your-repo-url>
cd disk-scheduling-visualizer
# Option 1: just open index.html in any modern browser
# Option 2: serve locally
python3 -m http.server 8000     # then open http://localhost:8000
```

## Run the tests
Requires Node.js 14+.
```bash
node tests/test.js
```
Expected: `All 11 tests passed`.

## Project structure
```
index.html          UI + visualization (self-contained, includes algorithm code)
src/algorithms.js   Pure algorithm module (used by the test-suite)
tests/test.js       Validation against the classic textbook example
docs/REPORT.md      Project report
```

## Algorithms in brief
| Algorithm | Idea | Trade-off |
|---|---|---|
| FCFS | Serve in arrival order | Fair, but long seeks |
| SSTF | Nearest request next | Low movement; can starve far requests |
| SCAN | Sweep to disk end, reverse | Better fairness; goes to the edge |
| C-SCAN | Sweep one way, jump back | Uniform wait times |
| LOOK | SCAN but reverse at last request | Less wasted movement |
| C-LOOK | C-SCAN but jump from last request | Best of both |

Sample input: queue `98,183,37,122,14,124,65,67`, head `53`, disk `0–199`.
Expected totals: FCFS 640, SSTF 236, SCAN 331, C-SCAN 382, LOOK 299, C-LOOK 322.

## Notes
This is a simulation only; it runs entirely in the browser and never touches real disks or system processes. C-SCAN/C-LOOK count the return jump as head movement (some textbooks exclude it).

## License
MIT
