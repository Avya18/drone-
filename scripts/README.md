# Mission scripts

These six executables form the recommended full mission. Run them from the repository root after sourcing ROS 2. See the [simulation walkthrough](../docs/SIMULATION.md) for all terminal commands.

| Script | Responsibility |
| --- | --- |
| `pre_entry_geometry_lock_v3_hybrid.py` | Fit corridor walls, align yaw and center laterally without forward motion. |
| `corridor_cruise_v2_integrated.py` | Cruise, recenter internally, detect obstacles and exit candidates. |
| `obstacle_avoidance_v1.py` | Decide the open side, shift laterally, pass an obstacle and return control to cruise. |
| `exit_detection_v2_commit.py` | Commit forward through a confirmed exit candidate using a speed × time travel estimate. |
| `hover_and_reassess_v2_loop_safe.py` | Hold zero velocity, assess fresh scans and request recovery or abort. |
| `corridor_mission_bridge_v4_loop_safe.py` | Select the active controller and apply commands through Gazebo state services. |

Start the bridge last: it starts the mission. Run only one bridge and one instance of each controller. Cruise and avoidance require the supplied YAML overrides for the two-obstacle world.

Nodes communicate with `LaserScan`, `TwistStamped`, `Bool` and `String` messages. Command frames use FLU: forward +x, left +y, up +z, counter-clockwise positive yaw. Parameters can be inspected with `ros2 param list NODE_NAME` and `ros2 param dump NODE_NAME`.

Exit travel is a commanded-distance estimate, not odometry; keep the simulation running during exit traversal.
