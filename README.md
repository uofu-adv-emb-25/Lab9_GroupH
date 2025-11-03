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
|      0     |       0       |       0      |            0           |            0           |          12         |          12         |         0        |         0        |         —        |           —        |
|      1     |       0       |       0      |            0           |            1           |          13         |          0         |         —        |         —        |         —        |           16        |
|      2     |       0       |       0      |            1           |            0           |          —         |          —         |         —        |         —        |         —        |           16        |
|      3     |       0       |       0      |            1           |            1           |          —         |          —         |         —        |         —        |         —        |           16        |
|      4     |       0       |       1      |            0           |            0           |          —         |          —         |         —        |         —        |         —        |           16        |
|      5     |       0       |       1      |            0           |            1           |          —         |          —         |         —        |         —        |         —        |           16        |
|      6     |       0       |       1      |            1           |            0           |          —         |          —         |         —        |         —        |         —        |           16        |
|      7     |       0       |       1      |            1           |            1           |          —         |          —         |         —        |         —        |         —        |           16        |
|      8     |       1       |       0      |            0           |            0           |          —         |          —         |         —        |         —        |         —        |                   |
|      9     |       1       |       0      |            0           |            1           |          —         |          —         |         —        |         —        |         —        |                   |
|     10     |       1       |       0      |            1           |            0           |          —         |          —         |         —        |         —        |         —        |                   |
|     11     |       1       |       0      |            1           |            1           |          —         |          —         |         —        |         —        |         —        |                   |
|     12     |       1       |       1      |            0           |            0           |          —         |          —         |         —        |         —        |         —        |                   |
|     13     |       1       |       1      |            0           |            1           |          —         |          —         |         —        |         —        |         —        |                   |
|     14     |       1       |       1      |            1           |            0           |          —         |          —         |         —        |         —        |         —        |                   |
|     15     |       1       |       1      |            1           |            1           |          —         |          —         |         —        |         —        |         —        |                   |
