# QLearning Approach to Number Guessing Game

This repository contains code for a number guessing game that is designed to demonstrate the principles of Q-learning, a form of reinforcement learning. Here's a breakdown of what each part of the program does:

    Initialize the environment (initialize_game function):
        This function initializes the game by returning the number 42 with a 99% probability. There's a 1% chance that it will return a different random number between 1 and 100 (excluding 42). This sets up a scenario where the learning algorithm mostly has to guess the same number, but occasionally has to adapt to a different target number.
    Define the feedback mechanism (get_feedback function):
        This function provides feedback to the learning agent about its guesses. If the guess is too low, it returns 'higher'; if too high, 'lower'; if correct, 'correct'.
    Q-learning update rule (update_q_table function):
        This function updates the Q-table, which is a representation of the expected utility of taking a given action in a given state. It takes into account the current state, action, reward, next state, learning rate (alpha), and discount factor (gamma). This function is at the heart of how the agent learns through Q-learning.
    Reward function (calculate_reward function):
        The reward function provides a numerical reward to the learning agent. In this case, it penalizes the agent with a negative reward based on how far off the guess is from the target number.

The main loop of the program runs the training process for a specified number of episodes. Within each episode, the target number is set by initialize_game, and the agent makes guesses until it correctly guesses the number or reaches a guess limit per episode (25 guesses here). The agent uses an epsilon-greedy policy to balance exploration (making a random guess) and exploitation (making the best guess based on the Q-table). The exploration rate (epsilon) starts at 1 (100% exploration) and decays over time to a minimum value, ensuring that as the agent learns, it increasingly relies on its knowledge rather than random guessing.

Finally, the program plots the learning progress over the episodes. It shows the number of guesses taken in each episode, with special markers for episodes where the target number was not 42 and where exploration occurred:

![grafik](https://github.com/DataScienceFH/RL_QLearn_NumberGuess/assets/129044997/f6044b26-d364-4915-9613-4e069d821077)

As the agent learns, a decrease in the number of guesses required to correctly identify the target number can be observed, indicating that the agent is improving. However, the performance data reveals a critical phenomenon: a tipping point indicating potential overfitting. While the agent becomes highly efficient at guessing the number 42—a result of its high occurrence—it exhibits a significant decrease in performance when the target number is anything but 42. This shows that the agent has overfit to the most common scenario and struggles to generalize its strategy to less frequent, unexpected situations. 

This overfitting is depicted in the learning progress graph where episodes with a target number different from 42 are marked with red dots. These points stand out against the trend and indicate episodes where the agent's number of guesses spikes, illustrating the instability in the agent's performance for the less common targets. Subsequently, the agent's performance degrades to the point where it begins to fail at correctly guessing 42, the number it initially learned to predict with high accuracy.
