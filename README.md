# VALUE ITERATION ALGORITHM

## AIM

To develop a Python program to find the optimal policy for the given MDP using the value iteration algorithm.

## PROBLEM STATEMENT

The Value Iteration algorithm solves for the optimal policy and value function in a Markov Decision Process (MDP). It initializes the value function to zero, iteratively updates it by computing the maximum Q-value for each state until convergence, and then extracts the policy by choosing the action with the highest Q-value for each state. The algorithm stops when the change in the value function is below a small threshold θ. The output is the optimal value function V and the corresponding policy π.


## POLICY ITERATION ALGORITHM

Initialize Value Function:

Set the initial value function V to zero for all states. This is done in the value_iteration function with V = np.zeros(len(P), dtype=np.float64).
Iterative Value Update:

For each state-action pair, calculate the Q-value using the current value function. This involves:
Iterating through all states s and actions a.
For each action, iterating through the transition probabilities, next states, rewards, and done flags to compute the Q-value.
Update the value function V to be the maximum Q-value for each state.
Continue iterating until the change in value function V is less than a small threshold θ.
Extract Optimal Policy:

After convergence, derive the optimal policy by selecting the action that maximizes the Q-value for each state.
Print Results:

Print identifying information, such as the name and registration number.
Display the optimal policy and state-value function.
Compute and print the success probability of reaching the goal and the average undiscounted return based on the derived policy.

## VALUE ITERATION FUNCTION
### Name: B VIJAY KUMAR
### Register Number: 212222230173

```
def value_iteration(P, gamma=1.0, theta=1e-10):
    V = np.zeros(len(P), dtype=np.float64)
    while True:
        Q = np.zeros((len(P), len(P[0])), dtype=np.float64)
        for s in range(len(P)):
            for a in range(len(P[s])):
                for p, s2, r , done in P[s][a]:
                    Q[s][a] += p * (r + gamma *
                                    V[s2] * (not done))

        if np.max(np.abs(V - np.max(Q, axis=1))) < theta:
            break
        V = np.max(Q, axis=1)

    pi = lambda s: {s: a for s, a in enumerate(np.argmax(Q, axis=1))}[s]

    return V, pi
```

```
V_best_v, pi_best_v = value_iteration(P, gamma=0.99)
print("Name: B VIJAY KUMAR    Register Number: 212222230173 ")
print('Optimal policy and state-value function (VI):')
print_policy(pi_best_v, P)
```
```
# printing the success rate and the mean return
print('Reaches goal {:.2f}%. Obtains an average undiscounted return of {:.4f}.'.format(
    probability_success(env, pi_best_v, goal_state=goal_state)*100,
    mean_return(env, pi_best_v)))
```
```
# printing the state value function
print_state_value_function(V_best_v, P, prec=4)
```

## OUTPUT:

![image](https://github.com/user-attachments/assets/5142041e-ecf7-4bf8-a130-3fa21effe161)

![image](https://github.com/user-attachments/assets/356b54f9-6bbc-41e7-99ca-8493f2fd180b)

![image](https://github.com/user-attachments/assets/950a7a2b-109c-4b21-b9c3-b5df601d792e)

## RESULT:

Thus , a pyhton program to find the optimal policy for the given MDP using the value iteration algorithm is implemented successfully . 
