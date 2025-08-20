# Continuous-Control-Optimized-Sampling
![Continuous Control snapshot](https://github.com/KingCoding/Continuous-Control-Optimized-Sampling/blob/main/pictures/Continuous%20Control%20Snapshot.png)
## Description
Implementation of a solution to training a Tennis environment with 20 agents using a Policy based method of deep reinforcement learning with DDPG algorithm.

The environment provides observation states for 20 agents containing information for 20 robotic arms each having 2 parts. The goal of the 2o agents is to collaborate through a deep reinforcement learning method like the DDPG algorithm in order to synchronize each robotic arm with its target.
In this environment, a double-jointed arm can move to target locations. A reward of +0.1 is provided for each step that the agent's hand is in the goal location. Thus, the goal of your agent is to maintain its position at the target location for as many time steps as possible.

The observation space consists of 33 variables corresponding to position, rotation, velocity, and angular velocities of the arm. Each action is a vector with four numbers, corresponding to torque applicable to two joints. Every entry in the action vector should be a number between -1 and 1.\
\
agents must get an average score of +30 (over 100 consecutive episodes, and over all agents). Specifically,
After each episode, we add up the rewards that each agent received (without discounting), to get a score for each agent. This yields 20 (potentially different) scores. We then take the average of these 20 scores.
This yields an average score for each episode (where the average is over all 20 agents).

## REQUIREMENTS AND SETUP
To set up your python environment to run the code in this repository, follow the instructions below.\
1- Create (and activate) a new environment with Python 3.6.
- **Linux** or **Mac:**
  ```
  conda create --name drlnd python=3.6
  source activate drlnd
  ```
- ***Windows:***
  ```
  conda create --name drlnd python=3.6 
  activate drlnd
  ```

2- Install OpenAi gym from [this repository](https://github.com/openai/gym)
- install the classic control environment group through [this link](https://github.com/openai/gym#classic-control)
- install the box2d environment group through [this link](https://github.com/openai/gym#box2d)

3- If you haven't yet done it, clone this repository, then navigate to the main Tennis-Maddpg-Collab-Comp/ folder.\
   There is no need to run the command pip install . in order to make initial python installation, because the main project file does it first
  ```
  git clone https://github.com/KingCoding/Continuous-Control-Optimized-Sampling.git
  cd Continuous-Control-Optimized-Sampling
  ```
4- Download the Unity environment for this project that mathes your operating system:
- Linux: [click here](https://s3-us-west-1.amazonaws.com/udacity-drlnd/P2/Reacher/Reacher_Linux.zip)
- Mac OSX: [click here](https://s3-us-west-1.amazonaws.com/udacity-drlnd/P2/Reacher/Reacher.app.zip)
- Windows (32-bit): [click here](https://s3-us-west-1.amazonaws.com/udacity-drlnd/P2/Reacher/Reacher_Windows_x86.zip)
- Windows (64-bit): [click here](https://s3-us-west-1.amazonaws.com/udacity-drlnd/P2/Reacher/Reacher_Windows_x86_64.zip)

(For Windows users) Check out [this link](https://support.microsoft.com/en-us/help/827218/how-to-determine-whether-a-computer-is-running-a-32-bit-version-or-64) if you need help with determining if your computer is running a 32-bit version or 64-bit version of the Windows operating system.

(For AWS) If you'd like to train the agent on AWS (and have not [enabled a virtual screen](https://github.com/Unity-Technologies/ml-agents/blob/master/docs/Training-on-Amazon-Web-Service.md)), then please use [this link](https://s3-us-west-1.amazonaws.com/udacity-drlnd/P3/Tennis/Tennis_Linux_NoVis.zip) to obtain the "headless" version of the environment. You will not be able to watch the agent without enabling a virtual screen, but you will be able to train the agent. (To watch the agent, you should follow the instructions to [enable a virtual screen](https://github.com/Unity-Technologies/ml-agents/blob/master/docs/Training-on-Amazon-Web-Service.md), and then download the environment for the Linux operating system above.)


5- In the Continuous-Control-Optimized-Sampling/ repository folder, unzip (or decompress) the downloaded Unity environment file.

6- Open the Continuous_Control_Optimized_Sampling.ipynb file and replace the unity environment file name with the name of the unity environment corresponding to your plateform that you have donwloaded
```
change this line:
env = UnityEnvironment(file_name='/data/Reacher_Linux_NoVis/Reacher.x86_64')
with this:
env = UnityEnvironment(file_name="YOUR_SYSTEM_UNITY_ENVIRONMENT_FILE_NAME")
```

## EXECUTION
Run all the intructions in the Continuous_Control_Optimized_Sampling.ipynb file to train the agent.

## TRAINING RESULT GRAPH
![Training result graph](https://github.com/KingCoding/Continuous-Control-Optimized-Sampling/blob/main/pictures/Continuous%20Control%20Chart.png)
