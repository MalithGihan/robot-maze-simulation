# 🧭 TurtleBot3 Custom Maze Simulation (ROS 2 + Gazebo + RViz)

This README explains how to run a **custom TurtleBot3 maze simulation** using **ROS 2 (Jazzy)**, **Gazebo**, and **RViz** with **Cartographer SLAM**.

---

## 1. Clean Previous Gazebo & ROS2 Build Files

Before starting the simulation, close all running Gazebo instances and clean the workspace.

pkill -9 gazebo  
pkill -9 gzserver  
pkill -9 gzclient  
rm -rf ~/.gazebo/  

cd ~/ros2_ws  
rm -rf build/ install/ log/  

---

## 2. Rebuild ROS2 Workspace

Rebuild your workspace to make sure all packages are up to date.

colcon build --symlink-install  
source ~/ros2_ws/install/setup.bash  

---

## 3. Launch TurtleBot3 in Custom Maze World

Set the TurtleBot3 model and launch your custom maze world in Gazebo.

export TURTLEBOT3_MODEL=burger  
ros2 launch turtlebot3_gazebo maze_world.launch.py x_pose:=-1.3 y_pose:=-1.3  

This command spawns the TurtleBot3 Burger at coordinates (-1.3, -1.3) inside the maze.

---

## 4. Run SLAM with Cartographer

In a new terminal, source your workspace again and start Cartographer for SLAM mapping.

export TURTLEBOT3_MODEL=burger  
ros2 launch turtlebot3_cartographer cartographer.launch.py use_sim_time:=True  

Cartographer will open RViz and start building a live map of your maze.

---

## 5. Control the Robot with Keyboard (Teleop)

Open another terminal, source your workspace, and control the robot manually.

export TURTLEBOT3_MODEL=burger  
ros2 run turtlebot3_teleop teleop_keyboard  

Use the keyboard controls:

w → Move Forward  
a → Turn Left  
s → Stop / Move Backward  
d → Turn Right  

Press CTRL + C to stop teleop.

---

## 6. Summary of Workflow

Terminal 1 → Start Gazebo Maze Simulation  
ros2 launch turtlebot3_gazebo maze_world.launch.py x_pose:=-1.3 y_pose:=-1.3  

Terminal 2 → Run Cartographer SLAM  
ros2 launch turtlebot3_cartographer cartographer.launch.py use_sim_time:=True  

Terminal 3 → Run Teleoperation  
ros2 run turtlebot3_teleop teleop_keyboard  

---

## 7. Notes

- Always export the TurtleBot3 model in every terminal:  
  export TURTLEBOT3_MODEL=burger  

- Always source the setup file before using ROS2 commands:  
  source ~/ros2_ws/install/setup.bash  

- If Gazebo crashes or behaves unexpectedly, repeat Step 1 to clean all processes and rebuild.

---

## 8. Requirements

- Ubuntu 24.04 LTS  
- ROS 2 Jazzy  
- Gazebo Harmonic  
- Packages:
  - turtlebot3_gazebo  
  - turtlebot3_cartographer  
  - turtlebot3_teleop  

---

## 10. Full Command List (All Together)

pkill -9 gazebo  
pkill -9 gzserver  
pkill -9 gzclient  
rm -rf ~/.gazebo/  

cd ~/ros2_ws  
rm -rf build/ install/ log/  
colcon build --symlink-install  
source ~/ros2_ws/install/setup.bash  

export TURTLEBOT3_MODEL=burger  
ros2 launch turtlebot3_gazebo maze_world.launch.py x_pose:=-1.3 y_pose:=-1.3  

export TURTLEBOT3_MODEL=burger  
ros2 launch turtlebot3_cartographer cartographer.launch.py use_sim_time:=True  

export TURTLEBOT3_MODEL=burger  
ros2 run turtlebot3_teleop teleop_keyboard  
