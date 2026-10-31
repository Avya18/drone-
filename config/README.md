# Gazebo test configuration

`corridor_fsm_gazebo_test_params_v2.yaml` holds overrides for a 3.5 m corridor with 2 m side obstacles.

| Node | Parameter | Value | Purpose |
| --- | --- | --- | --- |
| `corridor_cruise_v2` | `front_cone_deg` | 35.0 | Wider forward obstacle cone. |
| `corridor_cruise_v2` | `correction_extreme_lateral_m` | 1.10 | Permit the lateral offset produced by bypassing the obstacle. |
| `obstacle_avoidance_v1` | `avoid_timeout_s` | 28.0 | Allow enough time for shifting and passing. |
| `obstacle_avoidance_v1` | `shift_timeout_s` | 8.0 | Allow the larger lateral shift. |

Apply the file independently to both nodes:

```bash
python3 scripts/corridor_cruise_v2_integrated.py --ros-args --params-file config/corridor_fsm_gazebo_test_params_v2.yaml
python3 scripts/obstacle_avoidance_v1.py --ros-args --params-file config/corridor_fsm_gazebo_test_params_v2.yaml
```

Run those commands in separate terminals. Other settings remain at defaults declared in each Python node. Inspect them with `ros2 param dump /corridor_cruise_v2` or `ros2 param dump /obstacle_avoidance_v1`. These overrides are specific to the supplied simulation geometry.
