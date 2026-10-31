# Setup

The upstream workflow targets ROS 2 Humble and Gazebo Classic. Use an environment with those installed, typically Ubuntu 22.04. The repository contains standalone ROS Python nodes and SDF assets; it does not contain a colcon package, package.xml or setup.py.

In an existing ROS 2 Humble environment, install the runtime dependencies:

```bash
sudo apt update
sudo apt install python3-numpy ros-humble-rclpy ros-humble-geometry-msgs ros-humble-sensor-msgs ros-humble-std-msgs ros-humble-gazebo-ros-pkgs
git clone https://github.com/Avya18/drone-.git "$HOME/drone-"
cd "$HOME/drone-"
source /opt/ros/humble/setup.bash
python3 -c "import rclpy, numpy; from gazebo_msgs.srv import GetEntityState, SetEntityState"
ros2 pkg prefix gazebo_ros
```

Source ROS in every terminal and use the same ROS_DOMAIN_ID across all processes. Run system Python so that the ROS-installed modules are available.

Continue with [Simulation](SIMULATION.md). The test drone floats with gravity disabled, and the bridge writes simulated velocities directly. Hardware/autopilot integration, takeoff and flight-controller frame conversion are outside the supplied stack.
