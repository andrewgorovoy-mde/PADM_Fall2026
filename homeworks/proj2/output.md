### Experiment settings
- Repetitions per (agent, environment): **20**
- Max steps per episode: **default**
- Agents (all other parameters at defaults):
  - Rollout (h=0): `RolloutLookaheadAgent(receding_horizon=0)`
  - Rollout (h=40): `RolloutLookaheadAgent(receding_horizon=40)`
  - MCTS (10 it): `MCTSAgent(iteration_budget=10, receding_horizon=40)`
  - MCTS (50 it): `MCTSAgent(iteration_budget=50, receding_horizon=40)`
  - Determinized A*: `FireMDPDeterminizedAStarAgent(step_budget=10000)`

### Mean ± std total reward

```
Environment                 maze        just_wait       the_circle       the_choice
Agent                                                                              
Rollout (h=0)        0.00 ± 0.00      0.27 ± 0.92      0.93 ± 0.04     -0.31 ± 0.94
Rollout (h=40)       0.20 ± 0.39      0.77 ± 0.58      0.98 ± 0.01      0.10 ± 0.99
MCTS (10 it)         0.30 ± 0.45      0.67 ± 0.69      0.98 ± 0.00     -0.11 ± 0.98
MCTS (50 it)         0.94 ± 0.21      0.76 ± 0.58      0.99 ± 0.00      0.39 ± 0.90
Determinized A*      0.29 ± 0.45      0.77 ± 0.57      0.99 ± 0.00      0.64 ± 0.69
```

### `maze`

```
          Agent  N  Mean  Std  Median  Min  Max
  Rollout (h=0) 20  0.00 0.00    0.00 0.00 0.00
 Rollout (h=40) 20  0.20 0.39    0.00 0.00 0.99
   MCTS (10 it) 20  0.30 0.45    0.00 0.00 0.99
   MCTS (50 it) 20  0.94 0.21    0.99 0.00 0.99
Determinized A* 20  0.29 0.45    0.00 0.00 0.99
```

### `just_wait`

```
          Agent  N  Mean  Std  Median   Min  Max
  Rollout (h=0) 20  0.27 0.92    0.93 -1.00 0.97
 Rollout (h=40) 20  0.77 0.58    0.97 -0.97 0.98
   MCTS (10 it) 20  0.67 0.69    0.96 -0.99 0.97
   MCTS (50 it) 20  0.76 0.58    0.96 -0.99 0.97
Determinized A* 20  0.77 0.57    0.97 -0.95 0.98
```

### `the_circle`

```
          Agent  N  Mean  Std  Median  Min  Max
  Rollout (h=0) 20  0.93 0.04    0.93 0.80 0.98
 Rollout (h=40) 20  0.98 0.01    0.98 0.96 0.99
   MCTS (10 it) 20  0.98 0.00    0.99 0.97 0.99
   MCTS (50 it) 20  0.99 0.00    0.99 0.98 0.99
Determinized A* 20  0.99 0.00    0.99 0.99 0.99
```

### `the_choice`

```
          Agent  N   Mean  Std  Median   Min  Max
  Rollout (h=0) 20  -0.31 0.94   -0.99 -1.00 0.99
 Rollout (h=40) 20   0.10 0.99    0.99 -1.00 0.99
   MCTS (10 it) 20  -0.11 0.98   -0.99 -1.00 0.99
   MCTS (50 it) 20   0.39 0.90    0.97 -1.00 0.99
Determinized A* 20   0.64 0.69    0.93 -1.00 0.99
```

### Insights

- On the just_wait map, overall the determinized A* program performed better than MCTS, with a mean reward >= that of any other algo and the smallest std. This is interesting because I imagined MCTS could really start to see paths forward across rollouts, while determinized A* has to decide a path given the known knowledge at a given moment and does not have the ability to actually react to fire stochasticity involved.

- On a simple environment like the circle, agent choice does not really seem to be an issue. I think this is interesting because these agents all have different computational demands. Simpler environments then require simpler agents. This is akin to modern day model routers that decide how much model horsepower a task needs.

- On the choice, Determinized A* far outperformed MCTS. Between the MCTS algos, 50 iterations beats out 10 iterations, which leads me to believe further increasing iterations will continue to improve total rewards at the cost of computational demand. I think this speaks to certain environments being better suited for specific agents. If thinking about the choice as a binary tree (down or right) with mostly random movements in between, it makes sense that A* outperforms, as MCTS may struggle to really understand the best approach from an initially random policy in limited moves.