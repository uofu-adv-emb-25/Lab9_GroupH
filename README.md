# Invariants

## Example 1

### The barrier must be lowered whenever any train is approaching or present to prevent collisions.

(northbound_present ∨ southbound_present ∨ northbound_approach ∨ southbound_approach) → arms_down

## Example 2

### If the barrier is raised, no train should be near the crossing to ensure roadway safety.

arms_up → ¬(northbound_present ∨ southbound_present ∨ northbound_approach ∨ southbound_approach)

## Example 3

### The alarm must sound whenever a train is approaching or present to warn vehicles and pedestrians.

(northbound_approach ∨ southbound_approach ∨ northbound_present ∨ southbound_present) → alarm_on

# Varying Invariants

The violated invariant is:

(northbound_present ∨ southbound_present ∨ northbound_approach ∨ southbound_approach) → arms_down

This means that whenever a train is approaching or present, the barrier must be lowered.
However, in the FSM, after the nb_approach event, the system enters a “ringing, arms_up” state for 10 seconds before lowering the barrier. During that interval, the train is approaching but the crossing remains open. This is an unsafe transient condition. 

# Prove It

| **number** | **arms_down** | **alarm_on** | **northbound_present** | **southbound_present** | **north_approach** | **south_approach** | **north_depart** | **south_depart** | **time_elapsed** | **safety_hazard** |
| :--------: | :-----------: | :----------: | :--------------------: | :--------------------: | :----------------: | :----------------: | :--------------: | :--------------: | :--------------: | :---------------: |
|      0     |       0       |       0      |            0           |            0           |         6          |         5          |        20         |        21         |        22         |                   |
|      1     |       0       |       0      |            0           |            1           |         7          |          19         |         1        |         22        |         22        |           16        |
|      2     |       0       |       0      |            1           |            0           |         18          |          2         |         21        |         22        |         22        |           16        |
|      3     |       0       |       0      |            1           |            1           |         18          |          19         |        1         |         2        |         22        |           16        |
|      4     |       0       |       1      |            0           |            0           |          6         |          5         |         20        |         21        |         12        |                   |
|      5     |       0       |       1      |            0           |            1           |          7         |          19         |         20        |         4        |         13        |          16         |
|      6     |       0       |       1      |            1           |            0           |          18         |          6         |         4        |         21        |         14        |           16        |
|      7     |       0       |       1      |            1           |            1           |          18         |          19         |         5        |         6        |         12        |            16       |
|      8     |       1       |       0      |            0           |            0           |          14         |          13         |         20        |         21        |         22        |         17          |
|      9     |       1       |       0      |            0           |            1           |          15         |          19         |         20        |         9        |         22        |       17            |
|     10     |       1       |       0      |            1           |            0           |          18         |          14         |         8        |         21        |         33        |         17          |
|     11     |       1       |       0      |            1           |            1           |          18         |          19         |         9        |         10        |         22        |         17          |
|     12     |       1       |       1      |            0           |            0           |          14         |          13         |         20        |         21        |         8        |                   |
|     13     |       1       |       1      |            0           |            1           |          15         |          19         |         19        |         12        |         13        |                   |
|     14     |       1       |       1      |            1           |            0           |          18         |          14         |         12        |         21        |         14        |                   |
|     15     |       1       |       1      |            1           |            1           |          18         |          19         |         13        |         14        |         15        |                   |

| **number** |	**invariant** |
|   16	| If train is present, barrier is lowered|
| 17 | Barrier only lowered when alarm is on |
| 18 | North train approach --> north train present |
| 19 | South train approach --> south train present |
| 20 | Nouth train present -->  north train departs |
| 21 | South train present -->  south train departs |
| 22 | Timer elpased when event occurs |
