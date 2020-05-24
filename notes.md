# Terminology
 - agent - entity that perceives and acts upon the environment
 - state - configuration of agent and its environment
 - action - choice that can be taken in any given state
 - transition model - a result of applying applicable action on a state 
result(s,a) returns model from applying action a on state s
 - state space - set of all reachable states from initial one by sequence of actions
often represented as graph, where nodes are states, and relationships are actions
 -  goal test - a test that tests whether state is the goal state
 -  path cost - cost of arriving at certain state
 -  solution - sequence of actions that leads to solution
 -  optimal solution - solution led to by path of the lowest cost
 -  node - tracks its parent, a state, action (that had to be applied on parent), path cost ( from initial state)

# Basic path search algorithms
## Depth first search
DFS explores every branch all the way down, till meeting dead end, before starting to check another branch.
## Breath first search
BFS explores nodes in all branches at the same time (similiar to A* fill)

# Greedy best first search
Type of informed search in which it decides on what next node to search first depending on heuristic function.

**Heuristic function** - function that takes an educated estimate of how close certain node is to the goal.
Manhattan distance between checked node and target node is one of such functions.

**Uninformed search** - search algorithm that uses no problem-specific knowledge
**Informed search** is the opposite

# A* Search
Type of informed search where it uses heuristic function, but also calculates distance already passed to check whether the distance doesn't outweight the heuristic estimate.
Always finds the shortest path for admissible and consistent heuristics.

**Heuristic is admissible** if it never overestimates (never thinks I'm closer to the goal than I possibly can be).
**Heuristic is consistent** when h(n) <= h(n') + c
n - node
n' - successor node
c - step cost

# Adversarial search
i.e. tictac toe, so there's an adversary that fights against me

## Minimax
Good for determinsitc games like tictactoe

-1 enemy wins
0 nobody wins
1 I win

Max player tries to maximize the score
Min player tries to minimze it

S0 - initial zero
player(s) - outputs which player should move now
result(s,a) - returns state after action acts upon state
terminal(s) - checks whether game is over
utility(s) - gives us value of terminal state (-1, 0 or 1)


We represent all possible states and actions that lead to each as a graph. Each node has value of sum of values of all possible end states.
As a player we choose always state which has highest value - in case of max player - and lowest - in case of min one.


We might want tho, to sometimes choose lower node, if it will lead to more optimistic lower possible state
i.e.

                 S
               /   \
             20     15
            /|\     /|\
           2 9 9   5 5 5

In such case it would be much better to choose  15, despite the fact that 20 has bigger value, as if our opponent plays intelligently, after we'll choose 20, He'll bring us down to 2, so it's better to predict what's the smartest move our opponent can do, and choose path that assumes our opponent to be most intelligent.


**Alpha-Beta Prunning** - problem optimization
while we calculate value of lowest possible value of the children, we stop evaluating children as soon as we figure out that this path is bad.

                 S
               /   \
             4      <=3
            /|\   / /| \
           4 8 5 9 3 X  Y
i.e. in this example we don't need to calculate X and Y, as we know that path that leads to 3 is already worse than the one that leads to 4.

## Dept-limited minimax
Basically minimax but it doesn't go through whole tree, calculating values. It goes only few levels of depth, just like cheess player, doesn't predict all possibilities, only 1-2 moves forwards.
it uses evaulation funciton that estimates how goot the game state is, as we don't have access to final
game state, and whether it's a win or lose. The quality of evaulate function is how well this algorithm will perform.