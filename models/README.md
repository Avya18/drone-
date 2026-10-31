# Test drone model

`corridor_drone/model.sdf` defines the floating sensor-test model used in the mission walkthrough. Its body has gravity disabled, visual arms show heading, and a Gazebo ROS ray-sensor plugin publishes `/scan` in frame `base_laser`.

Spawn from the repository root after starting Gazebo:

```bash
ros2 run gazebo_ros spawn_entity.py -entity corridor_drone -file "$PWD/models/corridor_drone/model.sdf" -x -1.0 -y 0.65 -z 1.4 -Y 0.30
```

The bridge expects entity `corridor_drone` by default. It applies velocities through Gazebo services; this is a kinematic navigation test rather than a flight-dynamics model.

The file under `gazebo/models/corridor_drone/` is an identical upstream copy retained for compatibility. See [simulation instructions](../docs/SIMULATION.md).
