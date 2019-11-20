[//]: # (Image References)

[image1]: https://user-images.githubusercontent.com/10624937/42135619-d90f2f28-7d12-11e8-8823-82b970a54d7e.gif "Trained Agent"
[image2]: ./images/a.png "Packages"
[image3]: ./images/q_table_example.png "MDP"
[image4]: ./images/network.png "Net"
[image5]: ./images/Rewards.png "Rewards"
[image6]: ./images/Hyperparameters.png "Hyper"


# Project 1: Navigation
## Introduction
To develop this solution I used the concepts learned in the [DQN paper](https://storage.googleapis.com/deepmind-media/dqn/DQNNaturePaper.pdf) and in the [Udacity Deep Reinforcement Learning Nanodegree](https://www.udacity.com/course/deep-reinforcement-learning-nanodegree--nd893) course.

#### Reinforcement Learning
Reinforcement Learning (RL) framework is characterized by having an agent learning while interacting with an unknown environment.  
At each time step, the agent receives the environment's state and chooses the best-believed action. Having performed that action, the agent receives a reward and a new state. The agent's goal is maximizing the cumulative reward received over all time steps.  
Through those interaction with the environment and after receiving positive and negative rewards, the agent may learn how to choose the most appropriate actions to accomplish its goal. The set of the best actions to be chosen for each one of the known states of the environment is denominated as the best-policy, or also the state-action function: _**π(s) = a**_.

#### Markov Decision Process (MDP)
In the finite Markov Decision Processes (MDP) where the number of states and actions are limited, it is possible to represent the mapping of states, actions and rewards in a table, knows as Q-table, also represented by **_Q(s,a)_**, as the following example:  
![MDP][image3]


However, when a large number of variables is necessary to represent the environment, or when this representation is a set of continuous numbers, it becomes unfeasible to build that Q-table. In summary, traditional reinforcement learning techniques use a finite MDP model to solve an environment, which limits the use to environments with discrete state and action spaces.  

#### Function Approximator

To overcome this issue, an alternative is using a function to substitute the Q-table. That function is know as function approximator because it approximate the value of the pair state-action to the value that would be found if the Q-table was built.  

Another problem rises when the function approximator need to map a non-linear state-space. That means, the state-space cannot be represented as a linear function. Thus, the idea is to use a neural network to find the parameters of this non-linear function.  

#### DQN: Neural Network as the Function Approximator
As the Deep Q-Network (DQN) paper mentions:
> _Reinforcement learning is known to be unstable or even to diverge when a nonlinear function approximator is used to represent the action-value function_ Q(s,a)_._

That is the issue DQN proposes to solve.  
DQN uses a neural network as the function approximator to find the maximum expected reward for each possible pair state-action in the environment: **_Q(s,a) = max E_**.  

In order to solve the mentioned instability, DQN proposes two key ideas:

- **Experience Replay**: This method stores the agent’s experience at each time step in a replay-buffer that is accessed to perform the weight updates. Experience replay reduces the variance of the updates because successive updates are not correlated with one another as they would be with standard Q-learning. And by removing the dependence of successive experiences on the current weights, experience replay eliminated one source of instability.

- **Fixed Q-Targets**: it is an iterative update that adjusts the action-values (Q) towards target values that are only periodically updated, thereby reducing correlations with the target.

In this project, I used those ideas to solve the navigation challenge, as I describe in the next section.  

## Implementation
### Model architecture  

The Deep Q-Network (DQN) uses a deep neural network to act as the function approximator for the optimal action-value function _Q(s,a) = maxE_. The DQN paper describes a powerful neural network architecture where the input are pixels extracted from the game screen after having been treated (resized and converted to grayscale). That input is first processed by three convolutional layers with ReLU activation. This allows the system to exploit spatial relationships. Also, since four frames are stacked and provided as input, these convolutional layers also extract some temporal properties across those frames. The layers are followed by one fully-connected hidden layer with ReLU activation and one fully-connected linear output layer with a single output unit for each valid action, corresponding to the predicted Q-values of the individual actions for the input state.

For this project, the environment provides 37 variables representing the state-space, instead of the raw pixels of the images. Thus, it was not necessary to have those convolutional layers mentioned in the DQN paper. Then, I had to build only the fully-connected layers that map the input state to actions, as well as the predicted expected rewards for each one of them.
In this way, my neural network correspond to two fully-connected hidden layers with ReLU activation and one fully-connected linear output layer.
After some tests, I defined my network as having an input of 37 variables, 128 nodes for the first hidden layer, 32 nodes for the second one, and 4 nodes for the output layer, corresponding to the possible actions.

![Net][image4]

### The training phase

In order to train my network to solve this environment, I applied the concepts presented in the DQN paper.

#### e-greedy policy
After receiving the environment state, I select the action to take following an e-greedy policy. That means, based on an epsilon (eps) value, I select the action with the probability:  

- (1 - eps) * 100% of chance to select the best-believed action calculated by the neural network (that means, the greedy action)
- eps * 100% of chance to select a random action (equiprobable distribution)

By doing that, my model can explore other actions than the best-believed one.  
As the training phase advances, the model becomes more reliable, so the epsilon value can be downgraded, decreasing the exploration of the environment and increasing the exploitation of the learned policy.

#### Experience Replay

I store the experiences (state, action, reward, next state) of each interaction between agent and environment in a experience replay buffer. Then, after some interactions have been stored (every 4), I perform one step of training.  
In the training loop, I select a minibatch (size of 64) of experiences in a uniform random distribution and pass it into the neural network to calculate the loss and perform the update of the network weights.

#### Fixed Q-Targets

According to the DQN paper, in order to reduce the correlations with the target, two networks are maintained: one to calculate the actions to take (the local network) and another to calculate the target values (the target network).  
During the training phase, the weights of the local network are updated according to the loss function (described below) while the weights of the target network are kept fixed for some steps before being updated with the weights of the local network.

#### Soft-update for the target network

DQN paper suggests to keep the weights of the target network fixed for some time steps and then replace it by the weights of the trained network.  
One way to do that is transferring the weights slowly, a small portion on each learning step, instead of doing a hard copy after some fixed time steps. This process is known as soft-update.  
In this project, I adopted the soft-update, transferring the weights from the local to the target network in a rate of 0.01 (represented by the greek letter tau **τ**), which substitute the weights of the target network about each 100 learning steps.


#### Loss function

DQN performs Q-learning updates. For each step of the learning process, the value estimated by the local network for the given state is compared with the value estimated by the target network for the next given state plus the received reward. This difference is the error for that state. This error is then squared to eliminate the negative signal, when present.  
The squared error is calculated for each one of the experiences in the minibatch. The average of those squared errors are calculated to summarize the minibatch error in one value.  
This process is known as Mean Squared Error Loss.  
The loss function can be represented by the following formula:  
L(0) = E [ (r + g*Q(s',a',0^- ) - Q(s,a;0))^2 ]

#### Reducing the error

After calculating the minibatch loss, the backpropagation of those calculations is made and one step of a gradient descent is performed.  
For this project, I used the Adam optimizer.


## Hyperparameters
My next step was a tunning phase on the hyperparameters. Within this phase, I also revisited my implementations to verify if I had written the code correctly.  
It's a difficult task since a minimal change in one hyperparameter can lead to a significant change in the final result.  
Below I showed the defined hyperparameters.

![Hyper][image6]

## Plot of Rewards
This graph shows the rewards per episode within the training phase, as well as the moving mean. It illustrates that the Agent is able to receive an average reward of at least +13 over 100 episodes.  
In this case, the Agent solved the environment after 130 episodes.

![Rewards][image5]

## Conclusion
Although there are other algorithms  (see the list in "Ideas for future work") that propose a better performance I got a good result with the Vanilla DQN where the solution was able to solve the environment in only 130 episodes.

## Ideas for Future Work
There are other algorithms proposed to enhance the performance of the Deep Q-Network. One future work could implement them to verify their performance in this environment. Those algorithms are:

- [Double Deep Q-Network](https://arxiv.org/abs/1509.06461)  
Deep Q-Learning tends to overestimate action values. Double Q-Learning has been shown to work well in practice to help with this.  
- [Prioritized Experience Replay](https://arxiv.org/abs/1511.05952)  
Deep Q-Learning samples experience transitions uniformly from a replay memory. Prioritized experienced replay is based on the idea that the agent can learn more effectively from some transitions than from others, and the more important transitions should be sampled with higher probability.
- [Dueling Q-Network](https://arxiv.org/abs/1511.06581)  
Currently, in order to determine which states are (or are not) valuable, we have to estimate the corresponding action values for each action. However, by replacing the traditional Deep Q-Network (DQN) architecture with a dueling architecture, we can assess the value of each state, without having to learn the effect of each action.
- Other extensions proposed:
	- Learning from [multi-step bootstrap targets](https://arxiv.org/abs/1602.01783)
	- [Distributional DQN](https://arxiv.org/abs/1707.06887)
	- [Noisy DQN](https://arxiv.org/abs/1706.10295)

