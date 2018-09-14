Once your robot is up and running. You can use the ROS controller messages to move Valkyrie


**Setup a new workspace**

Create a new workspace which overlays the valkyrie and ihmc workspaces.
````
mkdir -p ~/val_test_script_ws/src
cd ~/val_test_script_ws
catkin config --install --extend ~/ihmc_ws/install
````
**Get the test scripts:**
````
cd src
git clone https://github.com/stevenjj/valkyrie_testing_edi
rosdep install --from-path . --ignore-src -y
catkin build
````
**Run the scripts!**

````
source ~/val_test_script_ws/install/setup.bash
# Example Script
roslaunch valkyrie_testing_edi whole_body_left_arm_right_bend_torso.launch
````
* Launch files with `suite` in their name will launch multiple ROS controller messages in sequence. 
* A `walk` script sends footstep messages.
* A `whole_body` script send a whole body message. 
* A `neck` script sends a neck trajectory message.
* A `go home` script sends a go home message.

See the files under `/data` and `/data/multiple_tests` to view the data used for the scripts. 

Note that the yaml files for a whole body message encodes the SE(3) and SO(3) data initially with respect to the midfeet frame. Later, a script transforms these waypoints to world frame when an update on the robot pose is received.