# Earlier mission bridge

`corridor_mission_bridge.py` preserves the upstream early Gazebo bridge. It supports pre-entry, entry, cruise and exit, with unsupported obstacle/recovery requests going to HOLD.

For the full two-obstacle mission, use [`../scripts/corridor_mission_bridge_v4_loop_safe.py`](../scripts/corridor_mission_bridge_v4_loop_safe.py). That version includes obstacle arbitration, loop-bounded reassessment, command expiry and mission results.

The earlier bridge pairs with the earlier exit interface in [controllers](../controllers/README.md). Run only one mission bridge at a time.
