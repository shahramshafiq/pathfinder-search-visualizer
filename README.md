<div align="center">

# Dungeon Pathfinder

A dungeon-themed desktop visualizer that shows how BFS, DFS, UCS and A* search a grid, step by step.

![Python](https://img.shields.io/badge/Python-3-3776AB?style=flat-square&logo=python&logoColor=white)
![Tkinter](https://img.shields.io/badge/GUI-Tkinter-4B8BBE?style=flat-square&logo=python&logoColor=white)
![Algorithms](https://img.shields.io/badge/Search-BFS%20%7C%20DFS%20%7C%20UCS%20%7C%20A*-2B2D42?style=flat-square)
![Dependencies](https://img.shields.io/badge/Dependencies-Standard%20Library%20Only-success?style=flat-square)

</div>

## Overview

Search algorithms are easy to describe and hard to picture. Dungeon Pathfinder lets you build a grid dungeon with walls, place a hero and a dragon, pick an algorithm, and watch it explore the map cell by cell before the hero walks the final path. All five searches are written by hand on top of fixed-size arrays with manual index tracking, so the code shows exactly how a queue, a stack and a priority queue behave. The whole app is a single Python file that uses only the standard library.

## Key Features

- **Five search strategies:** Breadth-First Search, Depth-First Search, Uniform Cost Search, A* with a Manhattan heuristic, and A* with a Euclidean heuristic.
- **Hand-written data structures:** the BFS queue, the DFS stack and the UCS/A* priority queue are preallocated arrays of size `rows * cols`, managed with `front`, `rear` and `top` indices. The priority queues find the minimum with a linear scan.
- **Editable dungeon grid:** click or drag to toggle walls, then place the hero and the dragon. The grid can be resized from 10x10 up to 50x50.
- **Dungeon generators:** a Random button (about 28 percent wall density) and a Maze button (about 35 percent density, with cells at odd row and odd column kept open).
- **Live exploration view:** every cell the algorithm discovers is painted as it is found, then the hero walks the final path with a coin dropped on each step.
- **Quest stats:** a header shows tiles explored and coins collected, and a side label shows the quest cost for Uniform Cost Search.
- **Weighted costs for UCS:** each open cell gets a random cost from 1 to 10 on every run, so UCS can pick a cheaper route that is longer than the shortest one.
- **Unreachable targets handled:** when the dragon cannot be reached, the app reports it and clears the exploration markers instead of crashing.

## Tech Stack

| Area | Technology |
|---|---|
| Language | Python 3 |
| GUI | Tkinter (`tkinter`, `ttk`, `messagebox`) |
| Rendering | Tkinter `Canvas` with cell rectangles and emoji sprites |
| Algorithms | BFS, DFS, Uniform Cost Search, A* (Manhattan and Euclidean) |
| Other | Python standard library only (`random`, `time`) |

## Project Structure

```text
.
|-- main.py      # Tkinter app: UI, grid editor, animation and all five search algorithms
|-- README.md
`-- .gitignore
```

## Getting Started

### Prerequisites

- Python 3 with Tkinter. Tkinter ships with the standard Python installers for Windows and macOS. On some Linux distributions it is a separate package (for example `python3-tk`).

### Installation

```bash
git clone https://github.com/shahramshafiq/pathfinder-search-visualizer.git
cd pathfinder-search-visualizer
```

There are no third-party packages to install and no environment variables to set.

### Run

```bash
python main.py
```

A 1400x800 window opens centered on the screen.

## Usage

1. Pick **Wall**, **Hero** or **Dragon** in the Map Builder panel, then click the grid. In Wall mode you can drag to paint walls, and clicking a wall again removes it.
2. Optionally use **Resize** to change the grid size, or **Maze** and **Random** to generate a layout.
3. Choose a strategy in the Strategy panel.
4. Press **Begin Quest** to watch the search and the hero's walk. Use **Clear Path** to remove the markers or **Reset Grid** to wipe everything.

How the algorithms behave in this app:

| Algorithm | Frontier structure | Path guarantee | Time (R rows, C columns) |
|---|---|---|---|
| BFS | Array queue | Fewest steps | O(R x C) |
| DFS | Array stack | Any valid path | O(R x C) |
| UCS | Array priority queue, linear min scan | Lowest total cost (random cell costs 1 to 10) | O((R x C)^2) |
| A* Manhattan / Euclidean | Array priority queue, linear min scan | Fewest steps (unit step cost) | O((R x C)^2) |

## Limitations and Roadmap

- There are no automated tests yet. Adding unit tests would first require moving the search functions out of the GUI class so they can run without a window.
- The whole app lives in one file and the searches read and write widgets directly. Separating the algorithms from the UI is the natural next refactor.
- The hero HP value in the header is a static display and does not change during a quest.
- The animation uses `time.sleep` with `root.update()`, so the window is not responsive to input while the hero is walking.

## Author

**Shahram Shafiq** - [GitHub](https://github.com/shahramshafiq) | [LinkedIn](https://www.linkedin.com/in/shahramshafiq/)
