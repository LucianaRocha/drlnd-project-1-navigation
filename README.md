[//]: # (Image References)

[image1]: https://user-images.githubusercontent.com/10624937/42135619-d90f2f28-7d12-11e8-8823-82b970a54d7e.gif "Trained Agent"
[image2]: https://github.com/LucianaRocha/drlnd-project-1-navigation/blob/master/images/a.png "Packages"
[image3]: https://github.com/LucianaRocha/drlnd-project-1-navigation/blob/master/images/b.png "Environment"
[image4]: https://github.com/LucianaRocha/drlnd-project-1-navigation/blob/master/images/c.png "Brain"
[image5]: https://github.com/LucianaRocha/drlnd-project-1-navigation/blob/master/images/d.png "State"
[image6]: https://github.com/LucianaRocha/drlnd-project-1-navigation/blob/master/images/e.png "Control"
[image7]: https://github.com/LucianaRocha/drlnd-project-1-navigation/blob/master/images/f.png "Scores"
[image8]: https://github.com/LucianaRocha/drlnd-project-1-navigation/blob/master/images/g.png "Close"
[image10]: https://github.com/LucianaRocha/drlnd-project-1-navigation/blob/master/images/download.png "Download"
[image11]: https://github.com/LucianaRocha/drlnd-project-1-navigation/blob/master/images/Navigate.png "Navigate"
[image12]: https://github.com/LucianaRocha/drlnd-project-1-navigation/blob/master/images/clone.png "Clone"
[image13]: https://github.com/LucianaRocha/drlnd-project-1-navigation/blob/master/images/Run.png "Run"
[image14]: https://github.com/LucianaRocha/drlnd-project-1-navigation/blob/master/images/Jupyter.png "Jupyter"

# Project 1: Navigation

## Project Details

This project is part of the [Deep Reinforcement Learning Nanodegree Program](https://www.udacity.com/course/deep-reinforcement-learning-nanodegree--nd893), by Udacity .
In this project, an agent is created and trained to navigate (and collect bananas!) in a large, square world.

![Trained Agent][image1]

A reward of +1 is provided for collecting a yellow banana, and a reward of -1 is provided for collecting a blue banana. Thus, the goal in this project is that the agent collects as many yellow bananas as possible while avoiding blue bananas.

The state space has 37 dimensions and contains the agent's velocity, along with ray-based perception of objects around agent's forward direction. Given this information, the agent has to learn how to best select actions. Four discrete actions are available, corresponding to:
- **`0`** - move forward.
- **`1`** - move backward.
- **`2`** - turn left.
- **`3`** - turn right.

The task is episodic, and in order to solve the environment, the agent must get an average score of +13 over 100 consecutive episodes.

## Getting Started

### Files included in this repository:
- The files below are needed to create and to train the Agent:
    - Navigation.ipynb
    - dqn_agent.py
    - model.py

- The trained model:
    - checkpoint.pth

- Log file:
    - unity-environment.log

- Useful information about the project:
    - README.md

- File describing the development process and the learning algorithm:
    - Report.md

### Getting the code:
- There are two options to get this project:
    - Download it as a zip file 
    ![Download][image10]
    - Clone this repository using Git version control system Clone
    ![Clone][image12]

- Install the Anaconda Platform:
    - Download the installer: [Anaconda](https://www.anaconda.com/distribution/)
    - Installation Guide: [Anaconda Installation Guide](https://docs.anaconda.com/anaconda/install/)
    - If you are keen to know more about notebooks and other tools of Project Jupyter, you find more information on [this website](https://jupyter.org/index.html).

## Instructions
- Open the Anaconda Platform and next open the Jupyter: 

![Jupyter][image14]

- Navigate to the root of the project in your system and click on the Navigation.ipynb notebook. Follow the instructions in Navigation.ipynb to get started with training the agent: 

![Navigate][image11]

### Explore the Environment and next Run the Jupyter Notebook:
Follow the instructions to learn how to use the Python API to control the agent. See below what kind of output to expect from the notebook, if everything is working properly.

- Begin by importing the necessary packages. If the code cell below returns an error, please revisit the project instructions to double-check that you have installed [Unity ML-Agents](https://github.com/Unity-Technologies/ml-agents/blob/master/docs/Installation.md) and [NumPy](https://numpy.org/).

![Packages][image2]

- Set your operational system by changing the value of the variable operational_system in the second cell code: 

![Environment][image3]

- Environments contain brains that are responsible for deciding the actions of their associated agents. Check for the first brain available, and set it as the default brain it will be controlled from Python. 

![Brain][image4]

- Examine the State and Action Spaces running the code below to print some information about the environment. 

![State][image5]

- In the next code cell, learn how to use the Python API to control the agent and receive feedback from the environment. Note that in this coding environment, it is not possible to watch the agent while it is training. Set the train_mode=True to restart the environment.

![Control][image6]

- The next code cell plots the scores.

![Scores][image7]

- Close the environment.

![Close][image8]

- Run the notebook:

![Run][image13]