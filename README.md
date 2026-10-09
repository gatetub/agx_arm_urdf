# AgileX Robotic Arm URDF Models

[中文](./README.md)

This repository contains the URDF / Xacro model files and the corresponding 3D mesh assets for AgileX robotic arms, for use in ROS / ROS2 visualization, simulation, and motion planning.

> **Scope**: This repository **primarily serves** the main [agx_arm_ros](https://github.com/agilexrobotics/agx_arm_ros) repository, where it is included as a submodule and installed together with the `agx_arm_description` package in the main repository.  
> If you are using it outside the AgileX main repository, you can create a package with the **same name** yourself, as described under "Standalone Use" below.

---

## Supported Models

| Model | Directory | Base URDF | Gripper Xacro | Dexterous Hand Xacro |
|------|------|-----------|------------|--------------|
| Piper | `piper/` | `piper_description.urdf` | `piper_with_gripper_description.xacro` | `piper_with_left_revo2_description.xacro` / `piper_with_right_revo2_description.xacro` |
| Piper H | `piper_h/` | `piper_h_description.urdf` | `piper_h_with_gripper_description.xacro` | `piper_h_with_left_revo2_description.xacro` / `piper_h_with_right_revo2_description.xacro` |
| Piper L | `piper_l/` | `piper_l_description.urdf` | `piper_l_with_gripper_description.xacro` | `piper_l_with_left_revo2_description.xacro` / `piper_l_with_right_revo2_description.xacro` |
| Piper X | `piper_x/` | `piper_x_description.urdf` | `piper_x_with_gripper_description.xacro` | `piper_x_with_left_revo2_description.xacro` / `piper_x_with_right_revo2_description.xacro` |
| Nero | `nero/` | `nero_description.urdf` | `nero_with_gripper_description.xacro` | `nero_with_left_revo2_description.xacro` / `nero_with_right_revo2_description.xacro` |
| AGX Gripper | `agx_gripper/` | `agx_gripper_description.urdf` | — | — |
| Revo2 Dexterous Hand | `revo2/` | `revo2_left_hand.urdf` / `revo2_right_hand.urdf` | — | — |

---

## Directory Structure

```
agx_arm_urdf/
├── piper/
│   ├── meshes/dae/
│   └── urdf/
├── piper_h/
│   ├── meshes/dae/
│   └── urdf/
├── piper_l/
│   ├── meshes/dae/
│   └── urdf/
├── piper_x/
│   ├── meshes/dae/
│   └── urdf/
├── nero/
│   ├── meshes/dae/
│   └── urdf/
├── agx_gripper/
│   ├── meshes/dae/
│   └── urdf/
└── revo2/
    ├── meshes/dae/
    └── urdf/
```

---

## Usage

### Recommended: Use with the Main Repository

Clone via [agx_arm_ros](https://github.com/agilexrobotics/agx_arm_ros), including submodules:

```bash
git clone -b ros2 --recurse-submodules https://github.com/agilexrobotics/agx_arm_ros.git
```

Load a model for visualization in ROS2 (the launch file is provided by the main repository):

```bash
ros2 launch agx_arm_description display.launch.py arm_type:=piper
```

For more usage details, see the [agx_arm_ros documentation](https://github.com/agilexrobotics/agx_arm_ros).

---

### Standalone Use (Your Own Workspace)

If you are not using the full `agx_arm_ros`, you can still clone only this repository, but you must provide the **ROS package** yourself, and the package **name** must be: `agx_arm_description`

#### ROS 2 (ament_cmake)

```bash
mkdir -p ~/ws/src && cd ~/ws/src
ros2 pkg create --build-type ament_cmake agx_arm_description
cd agx_arm_description
git clone https://github.com/agilexrobotics/agx_arm_urdf.git agx_arm_urdf
```

Add the following to the package's `CMakeLists.txt`:

```cmake
install(DIRECTORY agx_arm_urdf
  DESTINATION share/${PROJECT_NAME}
)
```

Then:

```bash
cd ~/ws
colcon build --packages-select agx_arm_description
source install/setup.bash
```

#### ROS 1 (catkin)

```bash
mkdir -p ~/catkin_ws/src && cd ~/catkin_ws/src
catkin_create_pkg agx_arm_description
cd agx_arm_description
git clone https://github.com/agilexrobotics/agx_arm_urdf.git agx_arm_urdf
```

Add the following to the package's `CMakeLists.txt`:

```cmake
install(DIRECTORY agx_arm_urdf
  DESTINATION ${CATKIN_PACKAGE_SHARE_DESTINATION}
)
```

Then:

```bash
cd ~/catkin_ws
catkin_make   # or catkin build
source devel/setup.bash
```

---

## License

This project is released under the [MIT License](./LICENSE).
