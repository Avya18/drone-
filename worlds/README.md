# Two-obstacle test world

`corridor_obstacles_2m_fsm_test.sdf` is the recommended full-mission world.

- Internal corridor width: 3.50 m; length: 28 m; height: 3.048 m.
- Left-wall obstacle at x = 8 m; right-wall obstacle at x = 18 m.
- Each obstacle intrudes 2 m, leaving a 1.50 m passage.
- Expected decisions: AVOID_RIGHT, then AVOID_LEFT, then exit.
- The Gazebo ROS state plugin exposes the services used by the bridge.

From the repository root:

```bash
ros2 launch gazebo_ros gazebo.launch.py world:="$PWD/worlds/corridor_obstacles_2m_fsm_test.sdf"
```

Use the [configuration overrides](../config/README.md), then follow the [complete simulation sequence](../docs/SIMULATION.md). The earlier corridor-only world remains in `gazebo/worlds/`.
