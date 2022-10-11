# Smartmobility
to update 

```
sudo apt update
```
To install the turtlesim humble version

```
sudo apt install ros-humble-turtlesim

```


And then I tried to check the package is installed or not. then terminal returned the command

```
turtlesim draw_square
turtlesim mimic
turtlesim turtle_teleop_key
turtlesim turtlesim_node
```
To start the turtlesim, 

```
ros2 run turtlesim turtlesim_node
```


![Screenshot from 2022-09-21 15-17-09](https://user-images.githubusercontent.com/86156093/191428482-9a045ccc-fb34-4a8e-a5db-e5b8bd706768.png)


The simulator window appeated with a random turtle in the center.



![Screenshot from 2022-09-21 15-17-14](https://user-images.githubusercontent.com/86156093/192296185-590275c2-ae29-455b-b860-80d4d3682754.png)

# Start turtlesim
```
ros2 run turtlesim turtlesim_node
```

![Screenshot from 2022-09-21 15-17-09](https://user-images.githubusercontent.com/86156093/192296607-eb060f72-dfd1-4d3b-b233-bf5c6d6757a2.png)

# Use of rqt
code for using rqt 

```
Install rqt

```

![Screenshot from 2022-09-21 14-33-57](https://user-images.githubusercontent.com/86156093/192297230-3d80810b-bbf0-4190-9e34-c036940d350e.png)

## working turtlesim

![Screenshot from 2022-09-21 15-17-09](https://user-images.githubusercontent.com/86156093/192296607-eb060f72-dfd1-4d3b-b233-bf5c6d6757a2.png)

## working of rqt
![Screenshot from 2022-09-20 11-55-13](https://user-images.githubusercontent.com/86156093/192297497-40ba4a86-6d79-4389-8142-319961e9365b.png)

![Screenshot from 2022-09-21 14-34-34](https://user-images.githubusercontent.com/86156093/192297874-6347c4ca-6a53-45d5-abff-10cbd9018d0f.png)

# Using colcon to build packages
```
sudo apt install python3-colcon-common-extensions
```

First, create a directory (ros2_ws) to contain our workspace:


![Screenshot from 2022-09-27 11-10-22](https://user-images.githubusercontent.com/86156093/192686827-89932b20-8250-4aa1-b80b-18d7fd1d606a.png)

![Screenshot from 2022-09-27 11-10-29](https://user-images.githubusercontent.com/86156093/192687008-1765501e-c664-4f8c-8307-717c606f3172.png)

![Screenshot from 2022-09-27 11-10-33](https://user-images.githubusercontent.com/86156093/192687045-0ba9ffe1-5b59-4440-80f2-a4a57225501c.png)

![Screenshot from 2022-09-27 11-10-45](https://user-images.githubusercontent.com/86156093/192687130-601bc2f8-1429-441d-aab2-905fb9d8f4f1.png)



## build the workspace

![Screenshot from 2022-09-27 11-10-45](https://user-images.githubusercontent.com/86156093/192687168-17f7994d-3eba-46ad-8710-89e824d3fe69.png)


![Screenshot from 2022-09-27 11-10-48](https://user-images.githubusercontent.com/86156093/192687447-7e80c15a-82a3-4060-8ad6-a53122640018.png)


![Screenshot from 2022-09-27 11-10-51](https://user-images.githubusercontent.com/86156093/192687507-017de4b9-bd3e-4118-8ae5-14c702c1a58f.png)

# Run tests
 ```
 colcon test
 ```


![Screenshot from 2022-09-27 11-10-59](https://user-images.githubusercontent.com/86156093/192687630-b2326cf5-de1d-43c6-83d2-33a55e87b885.png)



# Create a package
```
ros2 pkg create --build-type ament_python py_pubsub
```
![Screenshot from 2022-09-27 11-11-08](https://user-images.githubusercontent.com/86156093/192688972-dc3d2e99-81c9-4fe0-aab9-46d35383f317.png)

![Screenshot from 2022-09-27 11-11-16](https://user-images.githubusercontent.com/86156093/192689160-7b45501e-1703-4e23-aec7-afcda02ce7f2.png)


# WEEK 5
 ## first, open a new terminal and source the ros2 and then navigate tothe ros2_1_ws in my case  and recall the src directory
 ## 1. create a package 
 
 
 
 ```
 ros2 pkg create --build-type ament_python py_srvcli --dependencies rclpy example_interfaces
 ```
### by entering this command, all its necessary files and folders
## 1.2 update the package.xml file
```
<description>Python client server tutorial</description>
<maintainer email="izzatullokhmail.com">Izzatullokh</maintainer>
<license>Apache License 2.0</license>
```
## 1.3 update setup.py file
```
      maintainer='izzatullokh',
    maintainer_email='izzatullokh@gmail.com',
    description='Python client server tutorial',
    license='Apache License 2.0',
    
 ```
 
# 2. Write the service node
 I created a new file  service_member_function.py Inside the ros2_1_ws/src/py_srvcli/py_srvcli directory, create a new and  pasted the following code within: 
 
 ```
 from example_interfaces.srv import AddTwoInts

import rclpy
from rclpy.node import Node


class MinimalService(Node):

    def __init__(self):
        super().__init__('minimal_service')
        self.srv = self.create_service(AddTwoInts, 'add_two_ints', self.add_two_ints_callback)

    def add_two_ints_callback(self, request, response):
        response.sum = request.a + request.b
        self.get_logger().info('Incoming request\na: %d b: %d' % (request.a, request.b))

        return response


def main():
    rclpy.init()

    minimal_service = MinimalService()

    rclpy.spin(minimal_service)

    rclpy.shutdown()


if __name__ == '__main__':
    main()
    
   ```
   
 ## Next step is adding  the following line between the 'console_scripts': brackets:
 
 ```
 'service = py_srvcli.service_member_function:main',
 ```
# 3 Write the client node
## as same the last code I created a file called 
client_member_function.py and wrote the following code inside of it
```
import sys

from example_interfaces.srv import AddTwoInts
import rclpy
from rclpy.node import Node


class MinimalClientAsync(Node):

    def __init__(self):
        super().__init__('minimal_client_async')
        self.cli = self.create_client(AddTwoInts, 'add_two_ints')
        while not self.cli.wait_for_service(timeout_sec=1.0):
            self.get_logger().info('service not available, waiting again...')
        self.req = AddTwoInts.Request()

    def send_request(self, a, b):
        self.req.a = a
        self.req.b = b
        self.future = self.cli.call_async(self.req)
        rclpy.spin_until_future_complete(self, self.future)
        return self.future.result()


def main():
    rclpy.init()

    minimal_client = MinimalClientAsync()
    response = minimal_client.send_request(int(sys.argv[1]), int(sys.argv[2]))
    minimal_client.get_logger().info(
        'Result of add_two_ints: for %d + %d = %d' %
        (int(sys.argv[1]), int(sys.argv[2]), response.sum))

    minimal_client.destroy_node()
    rclpy.shutdown()


if __name__ == '__main__':
    main()
```
### Like the service node, you also have to add an entry point to be able to run the client node

```
entry_points={
    'console_scripts': [
        'service = py_srvcli.service_member_function:main',
        'client = py_srvcli.client_member_function:main',
    ],
},
```
# 4.1 Build and run the Service 

![Screenshot from 2022-10-04 14-41-20](https://user-images.githubusercontent.com/86156093/193744140-cdc33db8-24c7-4317-a372-0b454af40fbf.png)

```
izzatullokh@izzatullokh-virtual-machine:~$ cd ros2_1_ws
izzatullokh@izzatullokh-virtual-machine:~/ros2_1_ws$ rosdep install -i --from-path src --rosdistro humble -y

#All required rosdeps installed successfully
izzatullokh@izzatullokh-virtual-machine:~/ros2_1_ws$ 
izzatullokh@izzatullokh-virtual-machine:~/ros2_1_ws$ colcon build --packages-select py_srvcli
Starting >>> py_srvcli
--- stderr: py_srvcli                   
/usr/lib/python3/dist-packages/setuptools/command/install.py:34: SetuptoolsDeprecationWarning: setup.py install is deprecated. Use build and pip and other standards-based tools.
  warnings.warn(
---
Finished <<< py_srvcli [1.32s]

Summary: 1 package finished [1.68s]
  1 package had stderr output: py_srvcli
izzatullokh@izzatullokh-virtual-machine:~/ros2_1_ws$ . install/setup.bash
izzatullokh@izzatullokh-virtual-machine:~/ros2_1_ws$ ros2 run py_srvcli service
[INFO] [1664862041.390463826] [minimal_service]: Incoming request
a: 2 b: 3

```
# 4.2 build and run the client

![Screenshot from 2022-10-04 14-46-37](https://user-images.githubusercontent.com/86156093/193744007-bd3cbb78-caae-4b0c-98ea-dbe91ffebf74.png)


```
@izzatullokh-virtual-machine:~/ros2_1_ws$ # Replace ".bash" with your shell if you're not using bash
# Possible values are: setup.bash, setup.sh, setup.zsh
source /opt/ros/humble/setup.bash
izzatullokh@izzatullokh-virtual-machine:~/ros2_1_ws$ rosdep install -i --from-path src --rosdistro humble -y
#All required rosdeps installed successfully
izzatullokh@izzatullokh-virtual-machine:~/ros2_1_ws$ colcon build --packages-select py_srvcli
Starting >>> py_srvcli
--- stderr: py_srvcli                   
/usr/lib/python3/dist-packages/setuptools/command/install.py:34: SetuptoolsDeprecationWarning: setup.py install is deprecated. Use build and pip and other standards-based tools.
  warnings.warn(
---
Finished <<< py_srvcli [1.17s]

Summary: 1 package finished [1.39s]
  1 package had stderr output: py_srvcli
izzatullokh@izzatullokh-virtual-machine:~/ros2_1_ws$ . install/setup.bash
izzatullokh@izzatullokh-virtual-machine:~/ros2_1_ws$ ros2 run py_srvcli client 2 3
[INFO] [1664862041.103507627] [minimal_client_async]: service not available, waiting again...
[INFO] [1664862041.391779279] [minimal_client_async]: Result of add_two_ints: for 2 + 3 = 5
izzatullokh@izzatullokh-virtual-machine:~/ros2_1_ws$ 
```


# Action
## terminal for turtlesim
```
izzatullokh@izzatullokh-virtual-machine:~$ # Replace ".bash" with your shell if you're not using bash
# Possible values are: setup.bash, setup.sh, setup.zsh
source /opt/ros/humble/setup.bash
izzatullokh@izzatullokh-virtual-machine:~$ ros2 run turtlesim turtlesim_node
Warning: Ignoring XDG_SESSION_TYPE=wayland on Gnome. Use QT_QPA_PLATFORM=wayland to run on Wayland anyway.
[INFO] [1664894097.902534336] [turtlesim]: Starting turtlesim with node name /turtlesim
[INFO] [1664894097.929237142] [turtlesim]: Spawning turtle [turtle1] at x=[5.544445], y=[5.544445], theta=[0.000000]
[INFO] [1664894122.950869168] [turtlesim]: Rotation goal completed successfully
[INFO] [1664894123.221407241] [turtlesim]: Rotation goal completed successfully
[INFO] [1664894123.572600221] [turtlesim]: Rotation goal completed successfully
[INFO] [1664894123.781802796] [turtlesim]: Rotation goal completed successfully
[INFO] [1664894123.942595878] [turtlesim]: Rotation goal completed successfully
[INFO] [1664894124.101750008] [turtlesim]: Rotation goal completed successfully
[WARN] [1664894135.620880179] [turtlesim]: Rotation goal received before a previous goal finished. Aborting previous goal
[WARN] [1664894135.828265964] [turtlesim]: Rotation goal received before a previous goal finished. Aborting previous goal
[WARN] [1664894136.563845683] [turtlesim]: Rotation goal received before a previous goal finished. Aborting previous goal

```
![Screenshot from 2022-10-04 23-45-26](https://user-images.githubusercontent.com/86156093/193852179-0914d90e-5c10-430f-b281-3c239bcec26c.png)

## terminal for teleop_turtle


```
izzatullokh@izzatullokh-virtual-machine:~$  # Replace ".bash" with your shell if you're not using bash
# Possible values are: setup.bash, setup.sh, setup.zsh
source /opt/ros/humble/setup.bash
izzatullokh@izzatullokh-virtual-machine:~$ ros2 run turtlesim turtle_teleop_key
Reading from keyboard
---------------------------
Use arrow keys to move the turtle.
Use G|B|V|C|D|E|R|T keys to rotate to absolute orientations. 'F' to cancel a rotation.
'Q' to quit.


```
![Screenshot from 2022-10-04 23-45-34](https://user-images.githubusercontent.com/86156093/193852360-0a55d86e-5443-42c3-832a-0a06a9c11569.png)

![Screenshot from 2022-10-04 23-45-57](https://user-images.githubusercontent.com/86156093/193852017-63b6e87a-adae-4124-863c-62f5f7809a72.png)

## terminal to see the turtlesim node's actions  and action list ,action info ros2 interface show and ros2 actoin send_goal

```
izzatullokh@izzatullokh-virtual-machine:~$ source /opt/ros/humble/setup.bash
izzatullokh@izzatullokh-virtual-machine:~$ ros2 node info /turtlesim
/turtlesim
  Subscribers:
    /parameter_events: rcl_interfaces/msg/ParameterEvent
    /turtle1/cmd_vel: geometry_msgs/msg/Twist
  Publishers:
    /parameter_events: rcl_interfaces/msg/ParameterEvent
    /rosout: rcl_interfaces/msg/Log
    /turtle1/color_sensor: turtlesim/msg/Color
    /turtle1/pose: turtlesim/msg/Pose
  Service Servers:
    /clear: std_srvs/srv/Empty
    /kill: turtlesim/srv/Kill
    /reset: std_srvs/srv/Empty
    /spawn: turtlesim/srv/Spawn
    /turtle1/set_pen: turtlesim/srv/SetPen
    /turtle1/teleport_absolute: turtlesim/srv/TeleportAbsolute
    /turtle1/teleport_relative: turtlesim/srv/TeleportRelative
    /turtlesim/describe_parameters: rcl_interfaces/srv/DescribeParameters
    /turtlesim/get_parameter_types: rcl_interfaces/srv/GetParameterTypes
    /turtlesim/get_parameters: rcl_interfaces/srv/GetParameters
    /turtlesim/list_parameters: rcl_interfaces/srv/ListParameters
    /turtlesim/set_parameters: rcl_interfaces/srv/SetParameters
    /turtlesim/set_parameters_atomically: rcl_interfaces/srv/SetParametersAtomically
  Service Clients:

  Action Servers:
    /turtle1/rotate_absolute: turtlesim/action/RotateAbsolute
  Action Clients:

izzatullokh@izzatullokh-virtual-machine:~$ 
izzatullokh@izzatullokh-virtual-machine:~$ source /opt/ros/humble/setup.bash
izzatullokh@izzatullokh-virtual-machine:~$ ros2 node info /turtlesim
/turtlesim
  Subscribers:
    /parameter_events: rcl_interfaces/msg/ParameterEvent
    /turtle1/cmd_vel: geometry_msgs/msg/Twist
  Publishers:
    /parameter_events: rcl_interfaces/msg/ParameterEvent
    /rosout: rcl_interfaces/msg/Log
    /turtle1/color_sensor: turtlesim/msg/Color
    /turtle1/pose: turtlesim/msg/Pose
  Service Servers:
    /clear: std_srvs/srv/Empty
    /kill: turtlesim/srv/Kill
    /reset: std_srvs/srv/Empty
    /spawn: turtlesim/srv/Spawn
    /turtle1/set_pen: turtlesim/srv/SetPen
    /turtle1/teleport_absolute: turtlesim/srv/TeleportAbsolute
    /turtle1/teleport_relative: turtlesim/srv/TeleportRelative
    /turtlesim/describe_parameters: rcl_interfaces/srv/DescribeParameters
    /turtlesim/get_parameter_types: rcl_interfaces/srv/GetParameterTypes
    /turtlesim/get_parameters: rcl_interfaces/srv/GetParameters
    /turtlesim/list_parameters: rcl_interfaces/srv/ListParameters
    /turtlesim/set_parameters: rcl_interfaces/srv/SetParameters
    /turtlesim/set_parameters_atomically: rcl_interfaces/srv/SetParametersAtomically
  Service Clients:

  Action Servers:
    /turtle1/rotate_absolute: turtlesim/action/RotateAbsolute
  Action Clients:

izzatullokh@izzatullokh-virtual-machine:~$ ros2 node info /teleop_turtle
/teleop_turtle
  Subscribers:
    /parameter_events: rcl_interfaces/msg/ParameterEvent
  Publishers:
    /parameter_events: rcl_interfaces/msg/ParameterEvent
    /rosout: rcl_interfaces/msg/Log
    /turtle1/cmd_vel: geometry_msgs/msg/Twist
  Service Servers:
    /teleop_turtle/describe_parameters: rcl_interfaces/srv/DescribeParameters
    /teleop_turtle/get_parameter_types: rcl_interfaces/srv/GetParameterTypes
    /teleop_turtle/get_parameters: rcl_interfaces/srv/GetParameters
    /teleop_turtle/list_parameters: rcl_interfaces/srv/ListParameters
    /teleop_turtle/set_parameters: rcl_interfaces/srv/SetParameters
    /teleop_turtle/set_parameters_atomically: rcl_interfaces/srv/SetParametersAtomically
  Service Clients:

  Action Servers:

  Action Clients:
    /turtle1/rotate_absolute: turtlesim/action/RotateAbsolute
izzatullokh@izzatullokh-virtual-machine:~$ ros2 action list
/turtle1/rotate_absolute
izzatullokh@izzatullokh-virtual-machine:~$ ros2 action list -t
/turtle1/rotate_absolute [turtlesim/action/RotateAbsolute]
izzatullokh@izzatullokh-virtual-machine:~$ ros2 action info /turtle1/rotate_absolute
Action: /turtle1/rotate_absolute
Action clients: 1
    /teleop_turtle
Action servers: 1
    /turtlesim
izzatullokh@izzatullokh-virtual-machine:~$ ros2 interface show turtlesim/action/RotateAbsolute
# The desired heading in radians
float32 theta
---
# The angular displacement in radians to the starting position
float32 delta
---
# The remaining rotation in radians
float32 remaining
izzatullokh@izzatullokh-virtual-machine:~$ ros2 action send_goal <action_name> <action_type> <values>
bash: syntax error near unexpected token `<'
izzatullokh@izzatullokh-virtual-machine:~$ ros2 action send_goal /turtle1/rotate_absolute turtlesim/action/RotateAbsolute "{theta: 1.57}"
Waiting for an action server to become available...
Sending goal:
     theta: 1.57

Goal accepted with ID: 56d92799758448d89f045488c7592e24

Result:
    delta: -1.5679999589920044

Goal finished with status: SUCCEEDED
izzatullokh@izzatullokh-virtual-machine:~$ ros2 action send_goal /turtle1/rotate_absolute turtlesim/action/RotateAbsolute "{theta: -1.57}" --feedback
Waiting for an action server to become available...
Sending goal:
     theta: -1.57

Feedback:
    remaining: -3.126814842224121

Goal accepted with ID: a60226449ac5471b8e2d609dc36a8cbe

Feedback:
    remaining: -3.1108148097991943

Feedback:
    remaining: -3.0948147773742676

Feedback:
    remaining: -3.078814744949341

Feedback:
    remaining: -3.062814712524414

Feedback:
    remaining: -3.0468149185180664

Feedback:
    remaining: -3.0308146476745605

Feedback:
    remaining: -3.014814853668213

Feedback:
    remaining: -2.998814582824707

Feedback:
    remaining: -2.9828147888183594

Feedback:
    remaining: -2.9668147563934326

Feedback:
    remaining: -2.950814723968506

Feedback:
    remaining: -2.934814929962158

Feedback:
    remaining: -2.9188146591186523

Feedback:
    remaining: -2.9028148651123047

Feedback:
    remaining: -2.886814594268799

Feedback:
    remaining: -2.870814800262451

Feedback:
    remaining: -2.8548147678375244

Feedback:
    remaining: -2.8388147354125977

Feedback:
    remaining: -2.822814702987671

Feedback:
    remaining: -2.806814670562744

Feedback:
    remaining: -2.7908148765563965

Feedback:
    remaining: -2.7748146057128906

Feedback:
    remaining: -2.758814811706543

Feedback:
    remaining: -2.742814779281616

Feedback:
    remaining: -2.7268147468566895

Feedback:
    remaining: -2.7108147144317627

Feedback:
    remaining: -2.694814682006836

Feedback:
    remaining: -2.6788148880004883

Feedback:
    remaining: -2.6628146171569824

Feedback:
    remaining: -2.6468148231506348

Feedback:
    remaining: -2.630814790725708

Feedback:
    remaining: -2.6148147583007812

Feedback:
    remaining: -2.5988147258758545

Feedback:
    remaining: -2.5828146934509277

Feedback:
    remaining: -2.56681489944458

Feedback:
    remaining: -2.550814628601074

Feedback:
    remaining: -2.5348148345947266

Feedback:
    remaining: -2.5188148021698

Feedback:
    remaining: -2.502814769744873

Feedback:
    remaining: -2.4868147373199463

Feedback:
    remaining: -2.4708147048950195

Feedback:
    remaining: -2.4548146724700928

Feedback:
    remaining: -2.438814640045166

Feedback:
    remaining: -2.4228148460388184

Feedback:
    remaining: -2.4068148136138916

Feedback:
    remaining: -2.390814781188965

Feedback:
    remaining: -2.374814748764038

Feedback:
    remaining: -2.3588147163391113

Feedback:
    remaining: -2.3428146839141846

Feedback:
    remaining: -2.326814651489258

Feedback:
    remaining: -2.31081485748291

Feedback:
    remaining: -2.2948148250579834

Feedback:
    remaining: -2.2788147926330566

Feedback:
    remaining: -2.26281476020813

Feedback:
    remaining: -2.246814727783203

Feedback:
    remaining: -2.2308146953582764

Feedback:
    remaining: -2.2148146629333496

Feedback:
    remaining: -2.198814868927002

Feedback:
    remaining: -2.182814836502075

Feedback:
    remaining: -2.1668148040771484

Feedback:
    remaining: -2.1508147716522217

Feedback:
    remaining: -2.134814739227295

Feedback:
    remaining: -2.118814706802368

Feedback:
    remaining: -2.1028146743774414

Feedback:
    remaining: -2.0868148803710938

Feedback:
    remaining: -2.070814609527588

Feedback:
    remaining: -2.0548148155212402

Feedback:
    remaining: -2.0388147830963135

Feedback:
    remaining: -2.0228147506713867

Feedback:
    remaining: -2.00681471824646

Feedback:
    remaining: -1.9908146858215332

Feedback:
    remaining: -1.974814772605896

Feedback:
    remaining: -1.9588147401809692

Feedback:
    remaining: -1.9428147077560425

Feedback:
    remaining: -1.9268147945404053

Feedback:
    remaining: -1.9108147621154785

Feedback:
    remaining: -1.8948147296905518

Feedback:
    remaining: -1.878814697265625

Feedback:
    remaining: -1.8628147840499878

Feedback:
    remaining: -1.846814751625061

Feedback:
    remaining: -1.8308147192001343

Feedback:
    remaining: -1.814814805984497

Feedback:
    remaining: -1.7988147735595703

Feedback:
    remaining: -1.7828147411346436

Feedback:
    remaining: -1.7668147087097168

Feedback:
    remaining: -1.7508147954940796

Feedback:
    remaining: -1.7348147630691528

Feedback:
    remaining: -1.718814730644226

Feedback:
    remaining: -1.7028148174285889

Feedback:
    remaining: -1.686814785003662

Feedback:
    remaining: -1.6708147525787354

Feedback:
    remaining: -1.6548147201538086

Feedback:
    remaining: -1.6388148069381714

Feedback:
    remaining: -1.6228147745132446

Feedback:
    remaining: -1.6068147420883179

Feedback:
    remaining: -1.5908147096633911

Feedback:
    remaining: -1.574814796447754

Feedback:
    remaining: -1.5588147640228271

Feedback:
    remaining: -1.5428147315979004

Feedback:
    remaining: -1.5268146991729736

Feedback:
    remaining: -1.5108147859573364

Feedback:
    remaining: -1.4948147535324097

Feedback:
    remaining: -1.478814721107483

Feedback:
    remaining: -1.4628148078918457

Feedback:
    remaining: -1.446814775466919

Feedback:
    remaining: -1.4308147430419922

Feedback:
    remaining: -1.4148147106170654

Feedback:
    remaining: -1.3988147974014282

Feedback:
    remaining: -1.3828147649765015

Feedback:
    remaining: -1.3668147325515747

Feedback:
    remaining: -1.3508148193359375

Feedback:
    remaining: -1.3348147869110107

Feedback:
    remaining: -1.318814754486084

Feedback:
    remaining: -1.3028147220611572

Feedback:
    remaining: -1.2868146896362305

Feedback:
    remaining: -1.2708147764205933

Feedback:
    remaining: -1.2548147439956665

Feedback:
    remaining: -1.2388147115707397

Feedback:
    remaining: -1.2228147983551025

Feedback:
    remaining: -1.2068147659301758

Feedback:
    remaining: -1.190814733505249

Feedback:
    remaining: -1.1748147010803223

Feedback:
    remaining: -1.158814787864685

Feedback:
    remaining: -1.1428147554397583

Feedback:
    remaining: -1.1268147230148315

Feedback:
    remaining: -1.1108148097991943

Feedback:
    remaining: -1.0948147773742676

Feedback:
    remaining: -1.0788147449493408

Feedback:
    remaining: -1.062814712524414

Feedback:
    remaining: -1.0468146800994873

Feedback:
    remaining: -1.03081476688385

Feedback:
    remaining: -1.0148147344589233

Feedback:
    remaining: -0.9988147616386414

Feedback:
    remaining: -0.9828147292137146

Feedback:
    remaining: -0.9668147563934326

Feedback:
    remaining: -0.9508147239685059

Feedback:
    remaining: -0.9348147511482239

Feedback:
    remaining: -0.9188147783279419

Feedback:
    remaining: -0.9028147459030151

Feedback:
    remaining: -0.8868147730827332

Feedback:
    remaining: -0.8708147406578064

Feedback:
    remaining: -0.8548147678375244

Feedback:
    remaining: -0.8388147354125977

Feedback:
    remaining: -0.8228147625923157

Feedback:
    remaining: -0.8068147301673889

Feedback:
    remaining: -0.7908147573471069

Feedback:
    remaining: -0.7748147249221802

Feedback:
    remaining: -0.7588147521018982

Feedback:
    remaining: -0.7428147792816162

Feedback:
    remaining: -0.7268147468566895

Feedback:
    remaining: -0.7108147740364075

Feedback:
    remaining: -0.6948147416114807

Feedback:
    remaining: -0.6788147687911987

Feedback:
    remaining: -0.662814736366272

Feedback:
    remaining: -0.64681476354599

Feedback:
    remaining: -0.6308147311210632

Feedback:
    remaining: -0.6148147583007812

Feedback:
    remaining: -0.5988147258758545

Feedback:
    remaining: -0.5828147530555725

Feedback:
    remaining: -0.5668147802352905

Feedback:
    remaining: -0.5508147478103638

Feedback:
    remaining: -0.534814715385437

Feedback:
    remaining: -0.5188148021697998

Feedback:
    remaining: -0.502814769744873

Feedback:
    remaining: -0.4868147373199463

Feedback:
    remaining: -0.47081470489501953

Feedback:
    remaining: -0.4548147916793823

Feedback:
    remaining: -0.43881475925445557

Feedback:
    remaining: -0.4228147268295288

Feedback:
    remaining: -0.40681469440460205

Feedback:
    remaining: -0.39081478118896484

Feedback:
    remaining: -0.3748147487640381

Feedback:
    remaining: -0.35881471633911133

Feedback:
    remaining: -0.3428148031234741

Feedback:
    remaining: -0.32681477069854736

Feedback:
    remaining: -0.3108147382736206

Feedback:
    remaining: -0.29481470584869385

Feedback:
    remaining: -0.27881479263305664

Feedback:
    remaining: -0.2628147602081299

Feedback:
    remaining: -0.24681472778320312

Feedback:
    remaining: -0.23081469535827637

Feedback:
    remaining: -0.21481478214263916

Feedback:
    remaining: -0.1988147497177124

Feedback:
    remaining: -0.18281471729278564

Feedback:
    remaining: -0.16681480407714844

Feedback:
    remaining: -0.15081477165222168

Feedback:
    remaining: -0.13481473922729492

Feedback:
    remaining: -0.11881470680236816

Feedback:
    remaining: -0.10281479358673096

Feedback:
    remaining: -0.0868147611618042

Feedback:
    remaining: -0.07081472873687744

Feedback:
    remaining: -0.054814696311950684

Feedback:
    remaining: -0.03881478309631348

Feedback:
    remaining: -0.02281475067138672

Feedback:
    remaining: -0.006814718246459961

Result:
    delta: 3.119999885559082

Goal finished with status: SUCCEEDED
izzatullokh@izzatullokh-virtual-machine:~$ 

```

# Using rqt_console to view logs
### source ROS 2
## Start rqt_console in a new terminal with the following command:

![Screenshot from 2022-10-11 11-06-03](https://user-images.githubusercontent.com/86156093/194981022-e6cc30fd-c689-43b5-af26-80768e81036a.png)
## Now start turtlesim in a new terminal with the following command:
```
ros2 run turtlesim turtlesim_node
```
## Messages on the rqt_console

I entered the following command:
```
ros2 topic pub
```
and the terminal will return following commands:
```
source /opt/ros/humble/setup.bash
izzatullokh@izzatullokh-virtual-machine:~$ ros2 topic pub
usage: ros2 topic pub [-h] [-r N] [-p N] [-1 | -t TIMES] [-w WAIT_MATCHING_SUBSCRIPTIONS] [--keep-alive N]
                      [-n NODE_NAME]
                      [--qos-profile {unknown,system_default,sensor_data,services_default,parameters,parameter_events,action_status_default}]
                      [--qos-depth N] [--qos-history {system_default,keep_last,keep_all,unknown}]
                      [--qos-reliability {system_default,reliable,best_effort,unknown}]
                      [--qos-durability {system_default,transient_local,volatile,unknown}]
                      topic_name message_type [values]
ros2 topic pub: error: the following arguments are required: topic_name, message_type
izzatullokh@izzatullokh-virtual-machine:~$ ros2 topic pub -r 1 /turtle1/cmd_vel geometry_msgs/msg/Twist "{linear: {x: 2.0, y: 0.0, z: 0.0}, angular: {x: 0.0,y: 0.0,z: 0.0}}"
publisher: beginning loop
publishing #1: geometry_msgs.msg.Twist(linear=geometry_msgs.msg.Vector3(x=2.0, y=0.0, z=0.0), angular=geometry_msgs.msg.Vector3(x=0.0, y=0.0, z=0.0))

publishing #2: geometry_msgs.msg.Twist(linear=geometry_msgs.msg.Vector3(x=2.0, y=0.0, z=0.0), angular=geometry_msgs.msg.Vector3(x=0.0, y=0.0, z=0.0))

publishing #3: geometry_msgs.msg.Twist(linear=geometry_msgs.msg.Vector3(x=2.0, y=0.0, z=0.0), angular=geometry_msgs.msg.Vector3(x=0.0, y=0.0, z=0.0))

publishing #4: geometry_msgs.msg.Twist(linear=geometry_msgs.msg.Vector3(x=2.0, y=0.0, z=0.0), angular=geometry_msgs.msg.Vector3(x=0.0, y=0.0, z=0.0))

publishing #5: geometry_msgs.msg.Twist(linear=geometry_msgs.msg.Vector3(x=2.0, y=0.0, z=0.0), angular=geometry_msgs.msg.Vector3(x=0.0, y=0.0, z=0.0))

publishing #6: geometry_msgs.msg.Twist(linear=geometry_msgs.msg.Vector3(x=2.0, y=0.0, z=0.0), angular=geometry_msgs.msg.Vector3(x=0.0, y=0.0, z=0.0))

publishing #7: geometry_msgs.msg.Twist(linear=geometry_msgs.msg.Vector3(x=2.0, y=0.0, z=0.0), angular=geometry_msgs.msg.Vector3(x=0.0, y=0.0, z=0.0))

publishing #8: geometry_msgs.msg.Twist(linear=geometry_msgs.msg.Vector3(x=2.0, y=0.0, z=0.0), angular=geometry_msgs.msg.Vector3(x=0.0, y=0.0, z=0.0))

publishing #9: geometry_msgs.msg.Twist(linear=geometry_msgs.msg.Vector3(x=2.0, y=0.0, z=0.0), angular=geometry_msgs.msg.Vector3(x=0.0, y=0.0, z=0.0))

```
## setup
```
izzatullokh@izzatullokh-virtual-machine:~$ # Replace ".bash" with your shell if you're not using bash
# Possible values are: setup.bash, setup.sh, setup.zsh
source /opt/ros/humble/setup.bash
izzatullokh@izzatullokh-virtual-machine:~$ ros2 run rqt_console rqt_console

```
![Screenshot from 2022-10-11 11-20-11](https://user-images.githubusercontent.com/86156093/194982589-ec05a75a-b08f-4e74-82ee-98c19e0a162e.png)


## setup

```
~$ ros2 run turtlesim turtlesim_node

Warning: Ignoring XDG_SESSION_TYPE=wayland on Gnome. Use QT_QPA_PLATFORM=wayland to run on Wayland anyway.
[INFO] [1665453541.629632638] [turtlesim]: Starting turtlesim with node name /turtlesim
[INFO] [1665453541.698312815] [turtlesim]: Spawning turtle [turtle1] at x=[5.544445], y=[5.544445], theta=[0.000000]
[WARN] [1665453611.598193384] [turtlesim]: Oh no! I hit the wall! (Clamping from [x=11.112445, y=5.544445])
[WARN] [1665453611.614708689] [turtlesim]: Oh no! I hit the wall! (Clamping from [x=11.120889, y=5.544445])
[WARN] [1665453611.630719307] [turtlesim]: Oh no! I hit the wall! (Clamping from [x=11.120889, y=5.544445])
[WARN] [1665453611.645952505] [turtlesim]: Oh no! I hit the wall! (Clamping from [x=11.120889, y=5.544445])
[WARN] [1665453611.661930110] [turtlesim]: Oh no! I hit the wall! (Clamping from [x=11.120889, y=5.544445])
[WARN] [1665453611.677595772] [turtlesim]: Oh no! I hit the wall! (Clamping from [x=11.120889, y=5.544445])
[WARN] [1665453611.694433675] [turtlesim]: Oh no! I hit the wall! (Clamping from [x=11.120889, y=5.544445])
[WARN] [1665453611.710257479] [turtlesim]: Oh no! I hit the wall! (Clamping from [x=11.120889, y=5.544445])
[WARN] [1665453611.726236299] [turtlesim]: Oh no! I hit the wall! (Clamping from [x=11.120889, y=

```


