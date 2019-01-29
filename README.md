# gym-gazebo2

<a href="http://www.acutronicrobotics.com"><img src="/imgs/alr_logo.png" align="left" width="190"></a>

**gym-gazebo2 is a toolkit for developing and comparing reinforcement learning algorithms using ROS 2.0 and Gazebo**. Built as an extension of [gym-gazebo](https://github.com/erlerobot/gym-gazebo/tree/master), gym-gazebo2 has been redesigned with community feedback and adopts now a standalone architecture while mantaining the core concepts of previous work inspired originally by the OpenAI gym.


A whitepaper regarding previous work of gym-gazebo is available at https://arxiv.org/abs/1608.05742. Please use the following BibTex entry to cite our work::

    @article{zamora2016extending,
      title={Extending the OpenAI Gym for robotics: a toolkit for reinforcement learning using ROS and Gazebo},
      author={Zamora, Iker and Lopez, Nestor Gonzalez and Vilches, Victor Mayoral and Cordero, Alejandro Hernandez},
      journal={arXiv preprint arXiv:1608.05742},
      year={2016}
    }

**gym-gazebo2** is a complex piece of software for roboticists that puts together simulation tools, robot middlewares (ROS, ROS 2), machine learning and reinforcement learning techniques. All together to create an environment whereto benchmark and develop behaviors with robots. Setting up `gym-gazebo2` appropriately requires relevant familiarity with these tools.

**Docs**. In-depth explanations and actively growing tutorials can be found at https://acutronicrobotics.com/docs. _WIP, the following images will show a couple interesting tutorials that will atract people to visit the webpage_

<p align="center">
  <a href="https://acutronicrobotics.com/docs/technology/api/ros_api/gym_gazebo"><img height="300" src="/imgs/gym-gazebo-docs.png"> <img height="300" src="/imgs/gym-gazebo-docs2.png"></a>
</p>

---

## Table of Contents
- [Environments](#environments)
  - [MARA](#mara)
    - [Real Robot](#real-robot)
    - [Simulated Robot](#simulated-robot)
- [Installation](#installation)
- [Usage](#usage)
  - [Executing an algorithm](#executing-an-algorithm)
  - [Script parameters](#script-parameters)
  - [gzserver-gzclient](#gzserver-gzclient)


## Environments
The code for each environment group is housed in its own subdirectory
[gym_gazebo2/envs](https://github.com/erlerobot/gym-gazebo2/blob/master/gym_gazebo2/envs). Robot specific simulation files should be housed in robot specific ROS2 packages.

### MARA
#### Real Robot

<p>
<img src="/imgs/mara1_2.jpeg" align="left" height="150"> 

MARA stands for Modular Articulated Robotic Arm and is a collaborative robotic arm with ROS 2.0 in each actuator, sensor or any other representative module. Each module has native ROS 2.0 support, can be physically extended in a seamless manner and delivers industrial-grade features including synchronization, deterministic communication latencies, a ROS 2.0 software and hardware component lifecycle, and more. Altogether, MARA empowers new possibilities and applications in the professional landscape of robotics. Learn more or even order one at [acutronicrobotics.com](https://acutronicrobotics.com)!
</p>

#### Simulated Robot

<p>
<img src="imgs/mara_2.gif" align="left" height="125">

MARA also provides an accurate simulated version in Gazebo, which allows to translate behaviors from the simulated environment to the real robot. This is the version we will be training in gym-gazebo2. Please refer to [github.com/acutronicRobotics/MARA](https://github.com/acutronicRobotics/MARA) for additional simulation related content for Gazebo, MoveIt! and rviz2.
</p><br>

## Installation

Please refer to [INSTALL.md](/INSTALL.md).

## Usage

### Executing an algorithm

If you added the privisioning script to your `~/.bashrc`, you can directly execute the algorithm. Load the environment variables manually otherwise.

```sh
cd ~/gym-gazebo2/examples/MARA
python3 gazebo_mara_4actions.py
```
### Script parameters

Every MARA environment provides three command-line customization arguments. You can read the details by using the ``-h`` option in any MARA-script (e.g: `python3 gazebo_mara_4actions.py -h`). The help message is the following:

```sh
usage: gazebo_mara_4actions.py [-h] [-g] [-r] [-v VELOCITY] [-m | -p PORT]

MARA environment argument provider.

optional arguments:
  -h, --help            show this help message and exit
  -g, --gzclient        Run user interface.
  -r, --real_speed      Execute the simulation in real speed. RTF=1.
  -v VELOCITY, --velocity VELOCITY
                        Set servo motor velocity. Keep < 1.41 for real speed.
  -m, --multi_instance  Provide network segmentation to allow multiple
                        instances.
  -p PORT, --port PORT  Provide exact port to the network segmentation to
                        allow multiple instances.
```

### gzserver-gzclient

If you want to get faster simulation speeds, you should launch the simulation withouht the visual interface of gazebo. But it is possible that you want to check the learnt policy at some point without stoping the training, so this is how you do it:

- Launch the visual interfaze of gazebo:

```sh
gzclient
``` 

- If you used the `-m --multi_instance` option to provide network segmentation, do the following:

In a new terminal, set the corresponding `GAZEBO_MASTER_URI`: For convinience, this environment variable is printed at the beginning of every Env execution. Just copy and export it. You can also find information related to any running execution inside `/tmp/gym-gazebo2/running/` folder. Example:
```sh
export GAZEBO_MASTER_URI=http://localhost:11285
```
Finally launch the client:
```sh
gzclient
```
Final note: you can launch as many `gzserver` and `gzclient` instances as you want as long as you manage properly the `GAZEBO_MASTER_URI` environment variable.

## What's new

- 2019-02-25: Release of gym-gazebo2 with ROS2 compatibility and MARA environments.
