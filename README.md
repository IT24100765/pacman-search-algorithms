# 🎮 Pac-Man Search Algorithms

[![Python Version](https://img.shields.io/badge/Python-3.9%20%7C%203.10%20%7C%203.11-blue?style=flat-square)](https://www.python.org/)
[![License](https://img.shields.io/badge/License-MIT-green?style=flat-square)](LICENSE)
[![Course](https://img.shields.io/badge/Course-SE3062-orange?style=flat-square)](https://courseweb.sliit.lk/)
[![Total Marks](https://img.shields.io/badge/Total%20Marks-40-brightgreen?style=flat-square)](#-assignment-tasks)

> A comprehensive implementation of classical search algorithms in Pac-Man, featuring uninformed search strategies (DFS, BFS, UCS) and informed search with A*, coupled with admissible and consistent heuristics.

---

## 📋 Table of Contents

- [Overview](#-overview)
- [Objectives](#-objectives)
- [Project Structure](#-project-structure)
- [Environment Setup](#-environment-setup)
- [Assignment Tasks](#-assignment-tasks)
- [Grading Rubric](#-grading-rubric)
- [Quick Start](#-quick-start)
- [References](#-references)

---

## 🎯 Overview

This project implements classic search algorithms to solve pathfinding and navigation problems in the Pac-Man game environment. Students will explore both uninformed search strategies (that explore the state space systematically) and informed search with heuristics (that leverage domain knowledge to guide the search).

**Key Concepts:**
- Graph-based search with state expansion tracking
- Heuristic design for informed search optimization
- Problem formulation and state representation
- Trade-offs between search complexity and optimality

---

## 🔍 Objectives

Implement and master the following search algorithms:

| Algorithm | Type | Complexity |
|-----------|------|-----------|
| **Depth-First Search (DFS)** | Uninformed | O(b^d) |
| **Breadth-First Search (BFS)** | Uninformed | O(b^d) |
| **Uniform Cost Search (UCS)** | Uninformed | O(b^⌈C*/ε⌉) |
| **A* Search** | Informed | O(b^d) with good heuristic |

Additionally, design **admissible and consistent heuristics** for:
- Finding all corners in a maze
- Eating all the food dots in a maze

---

## 📁 Project Structure

```
pacman-search-algorithms/
├── search.py                    # ✏️  Search algorithms (DFS, BFS, UCS, A*)
├── searchAgents.py              # ✏️  Problem definitions & heuristics
├── util.py                      # 📖 Data structures (Stack, Queue, PriorityQueue)
├── pacman.py                    # 📚 Game runner & GameState definition
├── game.py                      # 📚 Game logic & state management
├── autograder.py                # 🧪 Testing & grading
├── test_cases/                  # 🧪 Test cases for each question
└── README.md                    # 📝 This file
```

### File Descriptions

| File | Status | Purpose |
|------|--------|---------|
| `search.py` | **✏️ Edit** | Implement DFS, BFS, UCS, A* algorithms (Q1–Q4) |
| `searchAgents.py` | **✏️ Edit** | Implement CornersProblem & heuristics (Q5–Q7) |
| `util.py` | **📖 Read Only** | Provides `Stack`, `Queue`, `PriorityQueue` |
| `pacman.py` | **📚 Reference** | Runs the game; describes `GameState` type |
| `game.py` | **📚 Reference** | Game logic: `AgentState`, `Agent`, `Directions`, `Grid` |
| `autograder.py` | **🧪 Run** | Automated testing/grading for all questions |
| `test_cases/` | **🧪 Auto-used** | Test suite for validation |

---

## ⚙️ Environment Setup

### Prerequisites

- **Python:** 3.9 – 3.11
- **Package Manager:** pip or conda

### Installation

1. **Create and activate a conda environment:**

```bash
conda create -n cs188 python=3.11
conda activate cs188
```

2. **Install required packages:**

```bash
pip install numpy matplotlib
```

3. **Verify the installation:**

```bash
cd search
python pacman.py
```

✅ **Success:** A playable Pac-Man game window opens. Use arrow keys to navigate.

---

## 📝 Assignment Tasks

### Q1 — Finding a Fixed Food Dot using Depth First Search

**⭐ Marks:** 4  
**🧪 Autograder:** `python autograder.py -q q1`

Implement `depthFirstSearch` in `search.py`.

**Requirements:**
- Must be a **graph-search** implementation
- Track expanded states to avoid re-expanding the same state
- Use the data structures from `util.py`

**Algorithm Strategy:**
- Use a stack (LIFO) to manage the fringe
- Explore deeply before backtracking

---

### Q2 — Breadth First Search

**⭐ Marks:** 4  
**🧪 Autograder:** `python autograder.py -q q2`

Implement `breadthFirstSearch` in `search.py`.

**Requirements:**
- Must be a **graph-search** implementation
- Track expanded states to avoid cycles
- Use the data structures from `util.py`

**Algorithm Strategy:**
- Use a queue (FIFO) to manage the fringe
- Explore level-by-level before going deeper
- Guarantees shortest path in unweighted graphs

---

### Q3 — Uniform Cost Search (Varying the Cost Function)

**⭐ Marks:** 4  
**🧪 Autograder:** `python autograder.py -q q3`

Implement `uniformCostSearch` in `search.py`.

**Requirements:**
- Generalize BFS by using **accumulated path cost** instead of step count
- Use a priority queue for the fringe
- Track expanded states

**Algorithm Strategy:**
- Expand nodes in order of their path cost (lowest first)
- Guarantees optimal solution when all costs are positive
- Degenerates to BFS when all edge costs are equal

---

### Q4 — A* Search

**⭐ Marks:** 4  
**🧪 Autograder:** `python autograder.py -q q4`

Implement `aStarSearch` in `search.py`.

**Requirements:**
- Takes a `heuristic` argument of form: `heuristic(state, problem)`
- Use priority queue with cost: `f(n) = g(n) + h(n)`
- Default heuristic is `nullHeuristic` (always returns 0)

**Algorithm Strategy:**
```
f(n) = g(n) + h(n)
  where g(n) = cost from start to node n
        h(n) = estimated cost from node n to goal
```

When `h(n) = 0`, A* becomes UCS (uniform cost search).

---

### Q5 — Finding All the Corners (Problem Representation)

**⭐ Marks:** 8  
**🧪 Autograder:** `python autograder.py -q q5`

Implement the `CornersProblem` class in `searchAgents.py`.

**Objective:** Find a path that visits all four corners of the maze.

**Must Implement:**
- `getStartState()` — Return initial state representation
- `isGoalState(state)` — Check if all corners are visited
- `getSuccessors(state)` — Generate successor states and actions
- Proper state bookkeeping

**Critical Constraints:**
- ⚠️ Keep state **small and hashable**
- ⚠️ Do **NOT** store entire `GameState` in state
- ⚠️ Do **NOT** store wall grid in state
- Use tuples for corners visited tracking

**State Design Example:**
```python
state = (current_position, corners_visited_tuple)
# NOT: (entire_game_state, walls, ...)
```

---

### Q6 — Corners Problem: Heuristic

**⭐ Marks:** 8  
**🧪 Autograder:** `python autograder.py -q q6`

Implement `cornersHeuristic` in `searchAgents.py` for the CornersProblem.

**Requirements:**
- ✅ Must be **admissible** (never overestimates cost)
- ✅ Must be **consistent** (h(n) ≤ cost(n→n') + h(n'))
- ✅ Return `0` at goal states
- ✅ Never return negative values

**Heuristic Ideas:**
- Manhattan distance to nearest unvisited corner
- Sum of distances to all unvisited corners
- Maximum distance to any unvisited corner

**Evaluation:** Based on nodes expanded on `mediumCorners` test case.

---

### Q7 — Eating All The Dots: Food Heuristic

**⭐ Marks:** 8 (max 10)  
**🧪 Autograder:** `python autograder.py -q q7`

Implement `foodHeuristic` in `searchAgents.py` for the `FoodSearchProblem`.

**Requirements:**
- ✅ Must be **admissible**
- ✅ Must be **consistent**
- No negative values allowed

**Heuristic Ideas:**
- Distance to nearest food dot
- Maximum distance to any food dot
- Minimum spanning tree of food dots

**Evaluation:** Based on nodes expanded on `trickySearch` test case.

#### 📊 Grading Criteria

| Nodes Expanded | Marks | Performance |
|---|---|---|
| More than 15,000 | 2 / 8 | ❌ Poor |
| At most 15,000 | 4 / 8 | ⚠️ Acceptable |
| At most 12,000 | 6 / 8 | ✅ Good |
| At most 9,000 | 8 / 8 | 🌟 Excellent |

---

## 📊 Overall Grading Rubric

| Question | Marks | Type | Focus |
|----------|-------|------|-------|
| **Q1 — DFS** | 4 | Algorithm | Graph Search |
| **Q2 — BFS** | 4 | Algorithm | Graph Search |
| **Q3 — UCS** | 4 | Algorithm | Cost-Based Search |
| **Q4 — A*** | 4 | Algorithm | Informed Search |
| **Q5 — Corners Problem** | 8 | Problem Formulation | State Representation |
| **Q6 — Corners Heuristic** | 8 | Heuristic Design | Admissibility & Consistency |
| **Q7 — Food Heuristic** | 8 | Heuristic Design | Optimization |
| | | | |
| **TOTAL** | **40** | | |

---

## 🚀 Quick Start

### Run Individual Tests

Test each question with the autograder:

```bash
# Search Algorithms
python autograder.py -q q1  # DFS
python autograder.py -q q2  # BFS
python autograder.py -q q3  # UCS
python autograder.py -q q4  # A*

# Problem Formulation & Heuristics
python autograder.py -q q5  # Corners Problem
python autograder.py -q q6  # Corners Heuristic
python autograder.py -q q7  # Food Heuristic
```

### Run All Tests

```bash
python autograder.py
```

### Manual Testing with Pac-Man

```bash
# Test a specific search algorithm
python pacman.py -l mediumMaze -p SearchAgent -a fn=depthFirstSearch

# Test with different mazes
python pacman.py -l tinyMaze -p SearchAgent
python pacman.py -l bigMaze -p SearchAgent

# Test CornersProblem
python pacman.py -l mediumCorners -p SearchAgent -a fn=bfs,prob=CornersProblem

# Test FoodSearchProblem
python pacman.py -l trickySearch -p AStarFoodSearchAgent
```

---

## 📚 Key Concepts & Tips

### Graph Search vs Tree Search

```python
# Graph Search (Use this!)
expanded_set = set()
while fringe is not empty:
    node = fringe.pop()
    if node in expanded_set:
        continue
    expanded_set.add(node)
    # ... expand node ...

# Tree Search (Don't use!)
# Same node can be expanded multiple times
```

### Heuristic Properties

| Property | Definition | Required |
|----------|-----------|----------|
| **Admissible** | h(n) ≤ actual cost from n to goal | ✅ Q6, Q7 |
| **Consistent** | h(n) ≤ cost(n→n') + h(n') | ✅ Q6, Q7 |
| **Informative** | Larger h(n) expands fewer nodes | 🎯 Bonus |

### Important Notes

- ⚠️ Always use `util.py` data structures, not Python built-ins
- ⚠️ Ensure state representation is hashable (use tuples, not lists)
- ⚠️ Track visited/expanded states to ensure graph search
- 🎯 Test frequently with the autograder during development
- 📝 Comment your code and explain design decisions

---

## 📖 References

- **Course:** SE3062 – Artificial Intelligence
- **Institution:** SLIIT (Sri Lanka Institute of Information Technology)
- **Assignment Link:** [Take-Home Assignment 04](https://courseweb.sliit.lk/mod/resource/view.php?id=496836)
- **Submission:** Group Project Assignment

### Useful Resources

- [Python Official Documentation](https://docs.python.org/3.11/)
- [NumPy Documentation](https://numpy.org/doc/)
- [Matplotlib Documentation](https://matplotlib.org/)

---

## 📬 Submission

**Type:** Group Project  
**Format:** GitHub Repository with Git history  
**Requirements:**
- All code implemented and tested
- Meaningful commit messages
- Comprehensive documentation
- All autograder tests passing

---

<div align="center">

**Happy Searching! 🔍**

Made with ❤️ for SE3062 Students

</div>