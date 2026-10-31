# Drone Corridor Navigation FSM

ROS 2 / Gazebo Classic corridor navigation using a 2-D LiDAR: align at the entrance, cruise and recenter, bypass side obstacles, recover from uncertain geometry and leave the corridor.

Imported from [sidkakroo770/something-secret](https://github.com/sidkakroo770/something-secret). Original author: Siddharth Kakroo. See [source attribution](docs/UPSTREAM.md).

## Getting started

1. Follow [Setup](docs/SETUP.md) to install the runtime dependencies and clone this repository.
2. Follow [Simulation](docs/SIMULATION.md) to start Gazebo, spawn the test drone and run the controllers.
3. Start the V4 mission bridge last; it begins the mission.
4. Monitor `/corridor/mission/result` for `SUCCESS:CORRIDOR_EXITED`.

The supplied workflow targets ROS 2 Humble and Gazebo Classic. Nodes run directly with Python; no colcon build is needed.

## Mission flow

```text
PRE_ENTRY_GEOMETRY_LOCK → ENTER_CORRIDOR → CORRIDOR_CRUISE
                                             ↓
                                      OBSTACLE_DECISION
                                             ↓
                                    AVOID_LEFT / AVOID_RIGHT
                                             ↓
                                       CORRIDOR_CRUISE
                                             ↓
                                       EXIT_DETECTION
                                             ↓
                                      CORRIDOR_EXITED
```

Unreliable geometry can trigger HOVER_AND_REASSESS. The V4 bridge bounds recovery loops and can terminate with ABORT_CORRIDOR. Cruise handles recentering internally through NOMINAL and CORRECTING modes.

## Repository guide

| Directory | Contents |
| --- | --- |
| [scripts/](scripts/README.md) | Recommended six-node mission stack, including V4 bridge and V2 exit/recovery. |
| [config/](config/README.md) | Two-obstacle test parameters and explanations. |
| [models/](models/README.md) | Floating LiDAR test-drone model. |
| [worlds/](worlds/README.md) | 3.5 m wide, 28 m long corridor with alternating 2 m obstacles. |
| [controllers/](controllers/README.md) | Preserved controller copies and earlier exit implementation. |
| [fsm/](fsm/README.md) | Earlier mission bridge retained for reference. |
| [gazebo/](gazebo/README.md) | Earlier world and duplicate model assets. |
| [docs/](docs/README.md) | Setup, full walkthrough, troubleshooting and upstream documentation. |

All upstream source paths remain available. Use the scripts under `scripts/` together for the full mission; earlier variants have different capabilities and exit-topic interfaces.

## Diagnostics and configuration

```bash
ros2 topic echo /corridor/mission/state
ros2 topic echo /corridor/mission/diagnostics
ros2 topic echo /corridor/mission/result
ros2 topic hz /scan
```

Use the [YAML overrides](config/README.md) for both cruise and avoidance in the supplied test world. See [Troubleshooting](docs/TROUBLESHOOTING.md) for missing services, stale scans, recovery and timeouts.

## Scope and validation

Commands use body FLU (+x forward, +y left, +z up, positive yaw counter-clockwise). The Gazebo bridge applies simulated velocities through entity-state services. The model has gravity disabled; hardware flight control is not included. Exit completion uses speed × active elapsed time, so do not pause the simulation during exit traversal.

The import was checked for Python syntax, SDF XML structure, documentation links and preservation of source files. A full ROS/Gazebo mission was not executed in the import environment.

## Attribution and license

The source revision is recorded in [UPSTREAM.md](docs/UPSTREAM.md), and its README is preserved in [UPSTREAM_README.md](docs/UPSTREAM_README.md). Upstream did not provide a LICENSE file; no new license is asserted by this copy.
