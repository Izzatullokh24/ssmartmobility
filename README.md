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


```
