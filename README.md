# Cogs182_Final_RickyMartin
Implementation of Q-Learning vs. Dyna Q Reinforcement Learning Algorithms in application to package sorting done through robotic arm.


Below will be an explination of how to execute the code for the Cogs 182 Final Project 

The Code is seperated into sections so I will be going through each below:

We start in part 1:

* We import files such as numpy, pandas, and matplot lib for usage later, I also included tqdm which helps track timing of learning, as well as some visual imports. In order to download any of these just google: "installing tqdm for python" followed by your OS. If you are using microsoft I personally recommend getting familiar with VS Code so you can use the terminal withing VS Code to import needed packages into an environment.

* We Start this project by creating the environment. For this iteration it will be an 11x11 grid, so 121 state, maze like structure where the agent of the Reinforcement Learning Algorithm will have to learn how to navigate through. The goal is to pick up a package at a random location and drop off said package at the "Goal Area". Here we also define our actions, very simple up, right, down, left due to the design of the grid world, and visualize our environment.

* Next we create our environment. Here we can visualize what it looks like and make changes if need be.

* The ls List is used later, ignore for now.

* Next We define helper functions. I chose to create 3, one that starts the agent at a random point that is not a black box or the goal, next is the next_state function which returns the next state post action, lastly is the next action function which given e-greedy exploration either returns a random action or returns the recommended action of the q_values.

* The next section is where the environment is tested, making sure everything is working correctly. This is done through a create_env_test function which creates an environemtn exactly like the previos one to test and mess with, as well as a graph_env function which tracks the movement taken by the agent. Here we test the environment, the start state, the next action, the next state, and the reward of our environment. With this we can be confident that our system will perform properly. 

* Next is our RL Models, this includes a Q-Learning (off-policy TD control) algorithm and a Tabular Dyna Q algorithm. These have been commented upon so you should be able to easily follow along. 

* After this we define our constants which includes our alpha, gamma, epsilon, n planning steps, n episodes, n experiments, max steps, and empty q and qp state value lists.

* Next we run the two models. I chose to seperate them since Q-learning takes like 20 seconds total, and the Dyna Q takes 20 minutes. In this way it was easier to debug the systems.

* Following these two learning algorithms is a quiver function which shows us the actions taken for specific states. Mind that all the black -100 areas show up movement, but disregarding this if we focus on the other arrows we can see clear evidence to suggest both algorithms have successfully lead to learned policies on how to operate within the environment. 

* Next we have our helper functions to print out the paths we want to take. While these could be combined into one path system, I liked keeping them seperate again for testing purposes during the initial building process.

* After this we have a function that will take in a list of points and output what each algorithms learned score would be. This is then printed and you can read through what the agents choose as the best paths to follow.

* Lastly I went ahead and iterated through the entire environment tackling every state, and the Dyna Q barely one by two moves so we will continue onto the robotics implementation with the Dyna Q policy. 

* Lastly I included a function that allows one to use the system learned so far despite not having an arm to work with. 

Part 2 is the code used to control the Robot.
* First we import some important libraries including The UARM Swift Pro's API. This can be found at this github link: https://github.com/uArm-Developer/pyuf

* The next snipped of code allows us to handle the connection of the robotic arm. This is tricky and required alot of disconnecting and reconnecting. 

* After this I showcased images of my real life set up. I am using the UARM Swift Pro robotic arm. I also then 3d printed a grid and little filler squares to act as the black boxes. You will notice my gird is 9x9 and not 11x11 this is on purpose since within the environment, a 9x9 grid is surrounded by blocks resulting in -100 reward which are places the bot should not go, so I figured I would save printing material and only print the significant area. 

* Next I defined a home function, it is important for a bot to have a starting position be it for calibration purposes or simply to have a place to return to when finished with tasks. 

* Lastly I define two uses of this algorithm. First is the normal way where the bot picks up a packages or cube and delivers it to the goal area. We could also reverse this though and instead take a package from the goal area to any where else in the environment. 
