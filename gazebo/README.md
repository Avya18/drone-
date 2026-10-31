# Earlier Gazebo assets

This directory preserves the upstream asset layout:

- `models/corridor_drone/model.sdf`: identical to the recommended model under [models](../models/README.md).
- `worlds/corridor_test.sdf`: earlier corridor world, distinct from the two-obstacle mission world.

For the complete mission, use [worlds/corridor_obstacles_2m_fsm_test.sdf](../worlds/corridor_obstacles_2m_fsm_test.sdf) with the model under `models/`. The [simulation walkthrough](../docs/SIMULATION.md) uses those paths consistently.

The assets use Gazebo Classic plugins. They are not directly interchangeable with modern Gazebo plugin interfaces.
