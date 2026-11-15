### Experiment settings
- Repetitions per (agent, environment): **20**
- Max steps per episode: **default**
- Agents (all other parameters at defaults):
  - Rollout (h=0): `RolloutLookaheadAgent(receding_horizon=0)`
  - Rollout (h=40): `RolloutLookaheadAgent(receding_horizon=40)`
  - MCTS (10 it): `MCTSAgent(iteration_budget=10, receding_horizon=40)`
  - MCTS (50 it): `MCTSAgent(iteration_budget=50, receding_horizon=40)`
  - Determinized A*: `FireMDPDeterminizedAStarAgent(step_budget=10000)`

### Mean ± std total reward (best per environment in bold)

```
Environment                 maze        just_wait       the_circle       the_choice
Agent                                                                              
Rollout (h=0)        0.00 ± 0.00      0.08 ± 0.95      0.93 ± 0.03      0.18 ± 0.96
Rollout (h=40)       0.30 ± 0.45      0.58 ± 0.78      0.98 ± 0.01      0.20 ± 0.97
MCTS (10 it)         0.59 ± 0.48      0.48 ± 0.82      0.98 ± 0.01     -0.10 ± 0.98
MCTS (50 it)     **0.69 ± 0.45**      0.75 ± 0.58      0.99 ± 0.00      0.10 ± 0.98
Determinized A*      0.30 ± 0.45  **0.95 ± 0.03**  **0.99 ± 0.00**  **0.53 ± 0.76**
```

### `maze`

```
          Agent  N  Mean  Std  Min  Max  Success %  Sec/run
  Rollout (h=0) 20  0.00 0.00  0.0 0.00        0.0     0.00
 Rollout (h=40) 20  0.30 0.45  0.0 0.99       30.0     0.40
   MCTS (10 it) 20  0.59 0.48  0.0 0.99       60.0     1.82
   MCTS (50 it) 20  0.69 0.45  0.0 0.99       70.0     7.38
Determinized A* 20  0.30 0.45  0.0 0.99       30.0    92.12
```

### `just_wait`

```
          Agent  N  Mean  Std   Min  Max  Success %  Sec/run
  Rollout (h=0) 20  0.08 0.95 -0.99 0.96       55.0     0.00
 Rollout (h=40) 20  0.58 0.78 -1.00 0.98       80.0     0.43
   MCTS (10 it) 20  0.48 0.82 -1.00 0.98       75.0     3.22
   MCTS (50 it) 20  0.75 0.58 -1.00 0.98       90.0    17.61
Determinized A* 20  0.95 0.03  0.87 0.98      100.0     7.14
```

### `the_circle`

```
          Agent  N  Mean  Std  Min  Max  Success %  Sec/run
  Rollout (h=0) 20  0.93 0.03 0.85 0.98      100.0     0.00
 Rollout (h=40) 20  0.98 0.01 0.97 0.99      100.0     0.40
   MCTS (10 it) 20  0.98 0.01 0.97 0.99      100.0     1.67
   MCTS (50 it) 20  0.99 0.00 0.98 0.99      100.0     5.52
Determinized A* 20  0.99 0.00 0.99 0.99      100.0     0.00
```

### `the_choice`

```
          Agent  N  Mean  Std  Min  Max  Success %  Sec/run
  Rollout (h=0) 20  0.18 0.96 -1.0 0.99       60.0     0.00
 Rollout (h=40) 20  0.20 0.97 -1.0 0.99       60.0     0.02
   MCTS (10 it) 20 -0.10 0.98 -1.0 0.99       45.0     0.58
   MCTS (50 it) 20  0.10 0.98 -1.0 0.99       55.0     1.64
Determinized A* 20  0.53 0.76 -1.0 0.99       80.0    23.73
```