# Troubleshooting

## Bridge waits for Gazebo services

```bash
ros2 service list
```

Check for `/gazebo/get_entity_state` and `/gazebo/set_entity_state`. Both supplied worlds include `libgazebo_ros_state.so`; use one of those worlds, verify Gazebo ROS packages are installed and check the Gazebo console for plugin load failures. Confirm the model was spawned as `corridor_drone`.

## No scan or motion

```bash
ros2 topic hz /scan
ros2 topic echo /corridor/mission/state
ros2 topic echo /corridor/mission/diagnostics
```

Check the ray-sensor plugin loaded, the simulation is unpaused and every terminal sourced the same ROS environment. Start all five controllers before starting the V4 bridge. Start only one bridge. Do not mix the older exit controller with the V4 bridge.

## Recovery repeats or mission aborts

```bash
ros2 topic echo /corridor/reassess/diagnostics
ros2 topic echo /corridor/obstacle/diagnostics
ros2 topic echo /corridor/exit/diagnostics
ros2 topic echo /corridor/mission/result
```

The bridge intentionally bounds recovery chains, repeated recovery from the same state and total recoveries. Inspect the published reasons, scan freshness and geometry before changing limits.

## Cruise fails after bypass or avoidance times out

```bash
ros2 param get /corridor_cruise_v2 correction_extreme_lateral_m
ros2 param get /obstacle_avoidance_v1 avoid_timeout_s
ros2 param get /obstacle_avoidance_v1 shift_timeout_s
```

For the supplied two-obstacle world these must be 1.1, 28.0 and 8.0 respectively. Load the YAML file into both cruise and obstacle nodes. Internal cruise CORRECTING mode after bypass is expected.

## Entry times out

The upstream walkthrough overrides `enter_corridor_timeout_s` to 12.0; the bridge default is 5.0. Use the documented spawn pose and override.

## Restarting

Stop the mission nodes and Gazebo launched for this test, then launch a fresh world and spawn the model again before restarting all controllers. Starting the bridge begins a new mission. A successful mission publishes `SUCCESS:CORRIDOR_EXITED`; the expected sequence is documented in [Simulation](SIMULATION.md).
