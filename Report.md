## INTRODUCTION
I set myself the adventurous challenge of finding a solution that outperforms the benchmark solution that was given in the description of the Udacity project.\
Many of the approaches I tried first failed. The two last approaches worked. One worked partially some times but didn't worked everytime. It was an approach based on counting the number of times each experience is used for training.\
I discuss a bit more about the approach that worked partially in the last section about Ideas for future work.
The appraoch that worked was simple and intuitive. I called it optimized sampling. Because it's an optimized approach for sampling experiences from the replay buffer to ensure that every new experience is used for training.\
I was very excited once I discovered it because it's a general way of accessing the replay buffer that can be used to train various kind of agents. And I think that I outperformed the benchmark by a decent margin.\
Because I could achieve very high values for my average reward for a very prolonged time. While the benchmark approach that accesses the replay buffer randomly couldn't sustain high average rewards values for a prolonged time.\

## LEARNING ALGORITHM
THE METHOD OF OPTIMIZED SAMPLING MAINTAINS 2 BUFFERS; ONE MAIN BIG BUFFER THAT CONTAINS MOST ELEMENTS AND THE SECONDARY BUFFER FOR THE LATEST ELEMENTS FOR THE LATEST COLLECTION FROM ALL AGENTS. THE METHOD SELECTS 0 TO A CERTAIN SMALL NUMBER (LIKE 3) OF LATEST EXPERIECNES AND INSERTS THEM RANDOMLY IN THE EVERY TRAINING BATCH UNTIL EVERY LATEST EXPERIENCE HAS BEEN USED FOR TRAINING. EACH TIME, THE SELECTED EXPERIENCES FROM THE LATEST BUFFER IS INSERTEDIN THE MAIN BUFFER AND REMOVED FROM THE LATEST BUFFER.
I WANTED THE NUMBER OF TRAININGS PER LATEST EXPERIENCES RATIO TO BE SIMILAR TO THAT OF A WORKING BENCHMARK IMPLEMENTATION. FOR THAT I HAD TO RESORT TO SOME CALCULATIONS.
LET'S SAY THE NUMBER OF LATEST EXPERIENCES FOR THE CURRENT ITERATION IS 400, AND THAT WE CHOSE TO SELECT FROM 0 TO A CERTAIN NUMBER OF SMALL LATEST EXPERIECNES TO ADD TO EVERY TRAINING BATCH.
THEN ASSUMING THAT THE NUMBER OF TIME A POSSIBLE VALUE OF LATEST EXPERIENCES IS SELECTED IS ABOUT THE SAME, LET'S SAY C (because we make a uniform random selection each time between 0 and the max number of selection inclusively).
THEN THE NUMBER OF AVERAGE TRAINING FOR THE 400 LATEST EXPERIENCES WILL BE C TIMES THE NUMBER OF POSSIBLE VALUES.
IN THIS CASE FROM 0 TO 4 INCLUSIVELY, WE WILL HAVE 5C. NOW TO FIND C, WE MUST SOLVE THE SMALL EQUATION:
0C + 1C + 2C + 3C + 4C = 400 => C = 400/10 = 40.
THEN THE AVERAGE NUMBER OF TRAINING PER ITERATIONS BASED ON THE CHOSEN HYPERPARAMETERS WILL BE 5C = 5*40 = 200.
WHICH IS EXACTLY THE SAME PERFORMANCE AS THE BENCHMARK IPLEMENTATION DESCRIBED INT THE NOTES OF THE UDACITY PROJECT. BECAUSE FOR EVERY 400 (20 X 20) EXPERIENCES, THEY PERFORMED 200 (20 X 10) TRAININGS.
SO I DECIDED TO START WITH THE ABOVE HYPERPARAMETERS.
The training started well, but it sTARTED DIPPING; TE CAUSE WAS PROBABLY OVERTRANING. SO I DECIDED TO CHANGE THE HYPERPARAETERS TO BRING THE RATE OF TRAINING LOW. AND I DISCOVERED THAT THE LOWER I BROUGHT THE RATE OF TRAINING, THE BETTER IT WAS GETTING. THE IDEAL RATE WAS ABOUT 140 TRAININGS PER ITERATION. ABOVE THAT THE TRAINING WOULD START VERY WELL, BUT IT WOULD DIPP BRUTALLY AFTER ABOUT 10 EPISODES.

ADDING ALL THE EXPERIENCES OF ALL 20 AGENTS IN THE REPLAY BUFFER BEFORE PERFORMING THE TRAININGS LIKE I USED TO DO, LEADS TO BAD TRAINING. INSTEAD WE HAVE TO INTRODUCE THE EXPERIENCES OF AGENTS ONE AGENT AT A TIME AND TRAIN IN BETWEEN ADDING THE EXPERIENCES OF EACH AGENT.

Instead of using consecutive numbers FOR THE NUMBER OF LATEST EXPERIENCES USED FOR EACH TRAINING BATCH, WE CAN USE AN ARRAY OF ANY DIGIT NON DISTINCT; IT MAKES THINGS MORE FLEXIBLE.
ONE COMINATION VERY CLOSE TO BENCHMARK IS THE FOLLOWING
[1,3,4], IDLE STEPS=20, THEN THE NUMBER OF TRAININGS PER ITERATION WILL BE 150.

SEE CODE in Continuous_Control_Optimized_Sampling.ipynb TO UNDERSTAND MORE.

### Networks configuration
- Number of Actor networks = 1 
- Number of critic networks = 1 
- Size of actor network = (33, 128, 256, 4)
- Size of critic network = (33, 128, 256, 1)
- Batchnorm implemented between the first and second layers of each network type

### Hyperparameters
- Replay buffer size = 1e6
- Minibatch size = 128
- Discount factor = 0.95
- Soft update of target parameters coefficient(TAU) = 1e-2
- Actor network learning rate = 1e-4
- Critic network learning rate = 1e-3
- How often to update the network (time steps) = 20
==

The max average score achieved during training was 39.36 at episode 51, and the environment was solved at 103 episodes.

![Training Result Graph](https://github.com/KingCoding/Continuous-Control-Optimized-Sampling/blob/main/pictures/Continuous%20Control%20Chart.png)
...

## IDEAS FOR FUTURE WORK
- IMplemented a weighted experiences approach that saves experiences while tracking the number of times (counts) they were used for training while in the buffer and that tracks the percentage of zero counts experiences in such a way that we don't have to provide static hyperparameters like number of iterations and number of training, but the algorithm will figure a way to perform the training by itself based on the counts of each training of experiences.
One way could be to select training batch until zero count percentage reaches a certain minimum.

- Make research to find the ideal combination with the optimized sampling method either theoritically with a general concept or dynamically at runtime.
