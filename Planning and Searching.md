# CS 309: Planning and Searching

## The planning problem
Given:
<ol>
	<li>An **initial state** of the world</li>
	<li>A set of **avaliable actions**, their requirements, and their effects
	<li>A **goal state**</li>
	<li>(Optionally) **Costs** associated with each action
</ol>

Compute: A **valid sequence of actions (the plan)** that starts from the initial state and terminates at the goal state (with the fewest actions/minimum cost)

## Planning via search
Starting from initial state:
<ol>
	<li>Enumerate all possible actions available, and the resulting states</li>
	<li>Check if goal state reached</li>
	<li>If not, for every possible outcome, repeat step 1 for all new states</li>
</ol>

### Problems with search-based planning
Many real-world problems quickly became intractable
- Too many action options
- Too many branching options
- Unable to enumerate till goal reached

**Pruning**: Eliminate duplicated sub-trees

## Heuristics

A planning heuristic is an (optmistic) estimate of how close a state is to the goal.
One way to use heuristics with planning (there are others):
Prioritize taking actions that have better heuristic scores.

**Example Heuristic**
- Optimism: assume goal conditions are independently achievable
- Heuristic value: How many goal conditions are met

## What is intelligence? Adversarial Planning

### Planning via search (chess, revised)

Starting from initial state:
1. Enumerate all possible actions available, and the resulting states
2. Check if goal state reached
3. If not, for every possible outcome, repeat step 1 for all new states

**Adversarial** Planning (through search)
1. Enumerate all possible actions available to you
2. Enumerate all possible actions available to opponent
3. Repeat 1, 2 until game ends
4. Rewind from game end back to now:
	1. For each level pick action most favorable to the player (most games won)
	2. Stop when rewound back to now
5. Pick most favorable action (most games won)

**Adversarial** Planning (through search) + **Heuristics**
1. Enumerate all possible actions available to you
2. Enumerate all possible actions available to opponent
3. Repeat 1, 2 until game ends up to max ***d** steps
4. Rewind from game end back to now:
	1. If not game end, use heuristic value of game state
	2. For each level pick action most favorable to the player (most games won)
	3. Stop when rewound back to now
5. Pick most favorable action (most games won)


Algorithm: Tree search with some clever strategies to prune the search tree

## Adversarial Planning via Tree Search + Deep Learning
1. Enumerate **promising actions (policy network)** available to you
2. Enumerate **promising actions (policy network)** available to opponent
3. Repeat 1, 2 until game ends up to max **d** steps
4. Rewind from game end back to now:
	1. If not game end, use **learned value (value network)** of game state
	2. For each level pick action most favorable to the player (best value for player)
	3. Stop when rewound back to now
5. Pick most favorable action (most games won)
