[//]: # (Image References)

[image1]: https://github.com/LucianaRocha/drlnd-project-1-navigation/blob/master/images/architecture.png "Architecture"
[image2]: https://github.com/LucianaRocha/drlnd-project-1-navigation/blob/master/images/Hyperparameters.png "Hyperparameters"
[image3]: https://github.com/LucianaRocha/drlnd-project-1-navigation/blob/master/images/f.png "Scores"
[image4]: 

# Project 1: Navigation
## Description of the implementation

### Algorithms
- I defined a neural network architecture in model.py that maps states to action values. See the architecture below. 
![Architecture][image1]
- Finished the learn method in the Agent class in dqn_agent.py.
- Once I have completed the code in dqn_agent.py and model.py, I ran the Jupyter notebook step by step.
- This model solved the environment in 130 episodes.

### Hyperparameters
My next step was a tunning phase on the hyperparameters. Within this phase, I also revisited my implementations to verify if I had written the code correctly.

It's a difficult task since a minimal change in one hyperparameter can lead to a significant change in the final result.

Below I showed the defined hyperparameters.
![Hyperparameters][image2]

### Plot of Rewards
This graph shows the rewards per episode within the training phase, as well as the moving mean.
It illustrates that the Agent is able to receive an average reward of at least +13 over 100 episodes.

In this case, the Agent solved the environment after 130 episodes.

![Scores][image3]

### Conclusion
In spite of being able to solve the environment in only 130 episodes, DQN architecture can be enhanced by those proposed algorithms (see the list below) to solve the environment even faster!

### Ideas for Future Work
There are other algorithms proposed to enhance the performance of the Deep Q-Network. One future work could implement them to verify their performance in this environment. Those algorithms are:

- Double Deep Q-Network
- Dueling Q-Network
- Prioritized Experience Replay