# A* Route Planner: Egypt

**Course:** Fundamentals of AI (CF321), Project 1: Search Algorithms
**Team:** _add member names and IDs here_

An interactive map of 22 Egyptian cities and the roads between them. Pick a start and a goal city and watch **A\* search** find the cheapest route, step by step.

## Idea

Route planning between cities on a map. The agent starts in one city and must reach another by driving along roads. The animation shows which cities A* explores, which ones are waiting on the frontier, and the final route.

## Algorithm: A\*

A* always expands the node with the lowest `f(n) = g(n) + h(n)`:

- `g(n)`: the cost of the best known route from the start to `n`
- `h(n)`: the estimated cost from `n` to the goal (the heuristic)

With an admissible heuristic, the first time the goal is expanded, the route is optimal.

## Problem definition

| Element | Definition |
|---|---|
| **States** | The city the agent is currently in (22 cities) |
| **Initial state** | The start city chosen by the user |
| **Goal state** | The destination city chosen by the user |
| **Actions** | Drive along a road to a directly connected neighbouring city |
| **Action cost** | Road distance in km = straight-line distance × 1.2 (rounded) |

## Heuristic

`h(n)` = **straight-line (haversine) distance** from city `n` to the goal, computed from real latitude/longitude.

**Why this heuristic?**

- **Admissible:** every road costs 1.2× its straight-line length, and a straight line is the shortest possible path, so `h` never overestimates the true remaining cost.
- **Consistent:** it follows the triangle inequality, so a city is never expanded twice.
- **Informative:** it points the search toward the goal, so fewer cities are explored.

## Results

The side panel reports, for each run:

- whether a solution was found
- the route and its cost in km
- the number of nodes explored
- the number of nodes explored **without** the heuristic (uniform-cost search, `h = 0`), so you can see how much the heuristic helps

Untick **Use heuristic** to watch the blind version of the search.

Example (Alexandria → Aswan): A* explores fewer cities than the uninformed search and returns the same optimal route.

## How to run

No installation needed.

1. Download or clone the repository.
2. Open `index.html` in any modern browser.

To run it from a local server instead: `python -m http.server`, then open `http://localhost:8000`.

## Files

- `index.html`: the whole project (A* implementation, map, animation, UI)
- `README.md`: this file

## Notes

Road costs are approximated from coordinates, not taken from a live maps service. City positions are real; the road network is a simplified version of Egypt's main highways.
