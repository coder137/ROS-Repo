# Getting Started

ESP8266 Interfacing with ROS

> Using Nodemcuv2 Devkit (ESP 12E Module) 

# Running the Code

## Condensed Steps

**Steps to Follow on Windows Server side**

1. `roscore`
2. `roslaunch rosserial_server socket.launch`
3. `rostopic list`
4. `rostopic echo /chatter`

**Steps to Follow on NodeMCU Side**

*Note: Platformio has been used to ease the build process*

- Install `ros_lib Arduino` through the platformio library install
- You can also manually build the entire packages and add it to platformio from [here](http://wiki.ros.org/rosserial_arduino/Tutorials/Arduino%20IDE%20Setup)
- Make sure you check the src `main.cpp` code, build and upload it

## Step by step (For Windows ROS Server)

### Step 1

- Install the entire `ros packages` then run `roscore` command

[Install ROS](http://wiki.ros.org/ROS/Installation)

### Step 2

- Install the entire packages from [here](http://wiki.ros.org/rosserial_arduino/Tutorials/Arduino%20IDE%20Setup)

    `cd <ws>/src`<br>
    `git clone https://github.com/ros-drivers/rosserial.git`<br>
    `cd <ws>`<br>
    `catkin_make`<br>
    `catkin_make install`

- make sure you `source devel/setup.bash`
- run `roslaunch rosserial_server socket.launch`

**NOTE: Default runs on port 11411**

**NOTE: If you are Running on Windows WSL, you need to perform additional steps to get it running (Highlighted below)**

### Step 3/4

- `rostopic list`
    - List all the topics present in the environment
-  `rostopic echo /chatter` 
    -  Subscribe to the topic `"chatter"` and see all messages published to it

## Problems with WSL Windows

- The first problem encountered by me was setting up ROS on Windows with WSL. Check [this article](https://janbernloehr.de/2017/06/10/ros-windows)

- Windows by default **allows** outgoing connections i.e from windows to any other system

- However, Windows by default **blocks** incoming connections i.e from another system to windows.

### Firewall Configuration on System to bypass Windows Inbound Restriction

- First check if you can `ping` your own system using `ping <local ip_address>`
- If you are blocked from pinging another local machine perform the below steps

1. Enter `RUN` (Windows_key+R)
2. `firewall.cpl`
3. `Advanced Settings`
4. Go to `Inbound Rules`
5. Create `New Rule` on the right side of the screen
6. Create `Custom Rule` under `Rule Type`
7. `All Programs` under `Program`
8. Either `Any` or `TCP` under `protocol type` in `Protocol and Ports`
9. Make sure the port used is 11311 upward if `TCP` port is selected (`Protocol and Ports`)
10. Allow everything for `Scope`, `Action` and `Profile`
11. Set the name as anything you wish. I set it as `ros_inbound_connect`
