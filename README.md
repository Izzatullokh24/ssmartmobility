# smartmobility
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
 `colcon test`


![Screenshot from 2022-09-27 11-10-59](https://user-images.githubusercontent.com/86156093/192687630-b2326cf5-de1d-43c6-83d2-33a55e87b885.png)



# Create a package
`ros2 pkg create --build-type ament_python py_pubsub`
![Screenshot from 2022-09-27 11-11-08](https://user-images.githubusercontent.com/86156093/192688972-dc3d2e99-81c9-4fe0-aab9-46d35383f317.png)

![Screenshot from 2022-09-27 11-11-16](https://user-images.githubusercontent.com/86156093/192689160-7b45501e-1703-4e23-aec7-afcda02ce7f2.png)



