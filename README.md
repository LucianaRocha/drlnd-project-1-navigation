[//]: # (Image References)

[image1]: https://user-images.githubusercontent.com/10624937/42135619-d90f2f28-7d12-11e8-8823-82b970a54d7e.gif "Trained Agent"
[image2]: ./images/a.png "Packages"
[image3]: ./images/b.png "Environment"
[image4]: ./images/c.png "Brain"
[image5]: ./images/d.png "State"
[image6]: ./images/e.png "Control"
[image7]: ./images/f.png "Scores"
[image8]: ./images/g.png "Close"
[image10]: ./images/download.png "Download"
[image11]: ./images/Navigate.png "Navigate"
[image12]: ./images/clone.png "Clone"
[image13]: ./images/Run.png "Run"
[image14]: ./images/Jupyter.png "Jupyter"

# Project 1: Navigation

## Project Details

This project is part of the [Deep Reinforcement Learning Nanodegree Program](https://www.udacity.com/course/deep-reinforcement-learning-nanodegree--nd893), by Udacity.
In this project, an agent is created and trained to navigate (and collect bananas!) in a large, square world.

![Trained Agent][image1]

A reward of +1 is provided for collecting a yellow banana, and a reward of -1 is provided for collecting a blue banana. Thus, the goal in this project is that the agent collects as many yellow bananas as possible while avoiding blue bananas.

The state space has 37 dimensions and contains the agent's velocity, along with ray-based perception of objects around agent's forward direction. Given this information, the agent has to learn how to best select actions. Four discrete actions are available, corresponding to:  

- **`0`** - move forward.
- **`1`** - move backward.
- **`2`** - turn left.
- **`3`** - turn right.

The task is episodic, and in order to solve the environment, the agent must get an average score of +13 over 100 consecutive episodes.

## Files included in this repository
- The files below are needed to create and to train the Agent:
    - Navigation.ipynb
    - dqn_agent.py
    - model.py

- The trained model:
    - checkpoint.pth

- Useful information about the project:
    - README.md

- File describing the development process and the learning algorithm:
    - Report.md
    

## Preparing the environment to run the project

**1.** Install the Anaconda Platform

- For more information about it, see [Anaconda Installation Guide](https://docs.anaconda.com/anaconda/install/)
- Download the [Anaconda Installer](https://www.anaconda.com/distribution/), version Python 3.x

**2.** Create and activate a new environment for this project

- Open Anaconda Prompt (Windows) or Terminal (Linux) and type

```
conda create --name navigation python=3.6 -y
```  

```
conda activate navigation
```

**3.** Install Pytorch  
Numpy and other required libraries will be installed with Pytorch.

 - In your Anaconda Prompt (Windows) or Terminal (Linux) type the line command below

```
conda install pytorch -c pytorch -y
```
**4.** Install Unity Agents  
Matplotlib, Jupyter, TensorFlow, and other required libraries will be installed with Unity Agents.

 - In your Anaconda Prompt (Windows) or Terminal (Linux) type the line command below
 
```
pip install unityagents
```


## Getting the code
There are two options to get this project:

**1.** Download it as a zip file  

 - Do the download in this [link](https://github.com/LucianaRocha/drlnd-project-1-navigation/archive/master.zip).  
 - Unzip the file in a folder of your choice.

**2.** Clone this repository using Git version control system 
 
 - Open Anaconda Prompt (Windows) or Terminal (Linux), navigate to the folder of your choice, and type the command below:  

```
git clone https://github.com/LucianaRocha/drlnd-project-1-navigation.git
```

 - If you want to know more about Git, see this [link](https://git-scm.com/downloads).

## Download the Unity environment 
 
- Download the environment, unzip (or decompress) the file, and place it inside the folder `drlnd-project-1-navigation`, where  you downloaded or cloned the repository. You need only select the environment that matches your operating system

 - Linux: [click here](https://s3-us-west-1.amazonaws.com/udacity-drlnd/P1/Banana/Banana_Linux.zip)
 - Mac OSX: [click here](https://s3-us-west-1.amazonaws.com/udacity-drlnd/P1/Banana/Banana.app.zip)
 - Windows (32-bit): [click here](https://s3-us-west-1.amazonaws.com/udacity-drlnd/P1/Banana/Banana_Windows_x86.zip)
 - Windows (64-bit): [click here](https://s3-us-west-1.amazonaws.com/udacity-drlnd/P1/Banana/Banana_Windows_x86_64.zip)

    
(_For Windows users_) Check out this [link](https://support.microsoft.com/en-us/help/827218/how-to-determine-whether-a-computer-is-running-a-32-bit-version-or-64) if you need help with determining if your computer is running a 32-bit version or 64-bit version of the Windows operating system.

(_For AWS_) If you'd like to train the agent on AWS (and have not [enabled a virtual screen](https://github.com/Unity-Technologies/ml-agents/blob/master/docs/Training-on-Amazon-Web-Service.md)), then please use this [link](https://s3-us-west-1.amazonaws.com/udacity-drlnd/P1/Banana/Banana_Linux_NoVis.zip) to obtain the environment.

## Running the project

- Open Anaconda Prompt (Windows) or Terminal (Linux), navigate to the project folder, and type the commands below to activate the project environment, and to open Jupyter.  
If you are keen to know more about notebooks and other tools of Project Jupyter, you find more information on this [website](https://jupyter.org/index.html).  

```
conda activate navigation  
```

```
jupyter notebook  
```

- Click on the Navigation.ipynb to open the notebook. 

![Navigate][image11]

- Next, we will start the environment! Before running the code cell below, change the file_name parameter to match the location of the Unity environment that you downloaded.

![Environment][image3]

- Run the notebook:

![Run][image13]
