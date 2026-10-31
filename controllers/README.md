# Controller reference implementations

This directory preserves the upstream controller implementations. The [scripts directory](../scripts/README.md) contains the recommended complete mission set.

| File | Relationship to recommended scripts |
| --- | --- |
| `pre_entry_geometry_lock_v3_hybrid.py` | Identical upstream copy of the script with the same name. |
| `corridor_cruise_v2_integrated.py` | Identical upstream copy of the script with the same name. |
| `exit_detection.py` | Earlier probing/clearing exit controller, distinct from the committed-traversal V2 script. |

The earlier exit controller uses the `/corridor/exit_detection/*` interface; the recommended V4 bridge and V2 exit script use `/corridor/exit/*`. Do not substitute them without adapting the interfaces. Keep duplicate implementations synchronized if modifying both copies.
