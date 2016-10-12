# Project 4: Reinforcement Learning
## Train a Smartcab How to Drive

QUESTION: OBSERVE WHAT YOU SEE WITH THE AGENT'S BEHAVIOR AS IT TAKES RANDOM ACTIONS. DOES THE SMARTCAB EVENTUALLY MAKE IT TO THE DESTINATION? ARE THERE ANY OTHER INTERESTING OBSERVATIONS TO NOTE?

When taking random actions, it appears that the smartcab sometimes reaches the
destination and sometimes does not. On one trial, it reached in 38 steps, but
on another trial it ran for 71 steps and never reached the deadline. It could be
the case that more steps were simply needed to reach the deadline.
  Furthermore, the reward values seem to be very random, sometimes they positive,
other times they are negative or zero.



QUESTION: WHAT STATES HAVE YOU IDENTIFIED THAT ARE APPROPRIATE FOR MODELING THE SMARTCAB AND ENVIRONMENT? WHY DO YOU BELIEVE EACH OF THESE STATES TO BE APPROPRIATE FOR THIS PROBLEM?

Discussion of the variables I have chosen to keep

  The states I identified as appropriate are the inputs about the light and
incoming traffic (except for the "right" input), and the next_waypoint. The inputs are appropriate
because they are necessary for understanding the context the car is in. This allows
the car to learn what is and isn't legal. The next_waypoint is appropriate because it informs the car about what direction it needs to go in to reach the final goal.
This will provide the car with information about how it can get its final large reward at the end.

Discussion of States that I omitted

However, I did not include the "right" input as it is not necessary due to us traffic laws. Furthermore, I decided that the deadline state is not appropriate for two reasons.  First of all,
including this variable would increase the size of the state space by a factor of the deadline size. This is because every inputs/next_waypoint state would become a new state for each time step towards the deadline. This results in our state space becoming unmanageably large, preventing the car from being able to learn a significant amount about the state space. Furthermore, including the deadline could cause the
car to do very illegal/dangerous actions when near the goal (due to the high reward received at the goal), which could result in unacceptable fatal car accidents.





QUESTION: WHAT CHANGES DO YOU NOTICE IN THE AGENT'S BEHAVIOR WHEN COMPARED TO THE BASIC DRIVING AGENT WHEN RANDOM ACTIONS WERE ALWAYS TAKEN? WHY IS THIS BEHAVIOR OCCURRING?

  After implementing the Q_learning algorithm the agent appears to do much better after the first trial.

On the first trial, the agent may not meet the deadline, which isn't altogether surprising
given that the agent is starting these trials with a poorly filled out Q_table. Without a properly filled out Q-table, the agent is not able to properly use the Q-learning algorithm to compute its path. As a result, it makes many illegal traffic maneuvers. Furthermore, it very rarely does no action on a red light, and more often incurs a negative penalty. This suggests that at this point the agent is basically
still in random exploration. The epsilon decay hasn't kicked in yet so random actions are still likely, which is desirable so that we can build out the q-table. Even the actions not guided by the random condition are likely not ideal as without a properly built up q-table, the proper action cannot be found.

However, as more trials are ran the agent is able to work from a better Q_table and complete within the deadline. In these trials (starting at the 2nd trial and going onward) the agent very rarely incurs negative penalties (ie very rarely commits a traffic violation) and does a very good job of handling red lights (pretty much always doing no action or turning right at red lights). The ability of the agent to stop at the light and wait for the next state indicates that it is able to use to the Q-table to consider the Q-values of future states, see that waiting for those students will produce positive rewards, and then choose to wait for those states (ie wait for the light to turn green). This indicates that the agent is indeed learning to follow the best next_waypoint, being patient and following traffic regulations in order to do so.



QUESTION: REPORT THE DIFFERENT VALUES FOR THE PARAMETERS TUNED IN YOUR BASIC IMPLEMENTATION OF Q-LEARNING. FOR WHICH SET OF PARAMETERS DOES THE AGENT PERFORM BEST? HOW WELL DOES THE FINAL DRIVING AGENT PERFORM?

  In my original Q_learning implementation I set alpha= 0.5, gamma = 0.5, and epsilon = 0.1. The rational
  behind this was that I was unsure what would be good for alpha and gamma so I left them as 0.5 (the middle value), whereas it seemed necessary to keep gamma small in order for the Q-learning to happen most of the time.
 However, after setting up the agent to measure the success rate, I decided to measure the average success rate over 3 iterations for 10 different combinations of parameters. The results were as follows and illustrated that the best option is to set alpha = 0.7, gamma = 0.5, and epsilon = 0.05. However, while this produced the best success rate for my trials, the values for the success rate had very little variance and were all very high, indicating that this Q-learning implementation is robust over a range of
 parameter values.






QUESTION: DOES YOUR AGENT GET CLOSE TO FINDING AN OPTIMAL POLICY, I.E. REACH THE DESTINATION IN THE MINIMUM POSSIBLE TIME, AND NOT INCUR ANY PENALTIES? HOW WOULD YOU DESCRIBE AN OPTIMAL POLICY FOR THIS PROBLEM?

I would say that the agent gets somewhat close to an optimal policy. I would consider an optimal policy to be one that causes zero traffic collisions (these are not acceptable in the real world), reaches the the destination in a short time, and only does illegal (but non accident causing maneuvers) rarely and only if they greatly lead to a decreased travel time.
  In the later 10 trials, it appears that the agent does this, reaching the destination quickly, making few illegal maneuvers, and making no maneuvers that cause accidents.
