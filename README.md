# VALUE ITERATION ALGORITHM

## AIM

To develop a Python program to find the optimal policy for the given MDP using the value iteration algorithm.

## PROBLEM STATEMENT

The Value Iteration algorithm solves for the optimal policy and value function in a Markov Decision Process (MDP). It initializes the value function to zero, iteratively updates it by computing the maximum Q-value for each state until convergence, and then extracts the policy by choosing the action with the highest Q-value for each state. The algorithm stops when the change in the value function is below a small threshold θ. The output is the optimal value function V and the corresponding policy π.


## POLICY ITERATION ALGORITHM

- Value iteration is a method of computing an optimal MDP policy  and its value.
- It begins with an initial guess for the value function, and iteratively updates it towards the optimal value function, according to the Bellman optimality equation.
- The algorithm is guaranteed to converge to the optimal value function, and in the process of doing so, also converges to the optimal policy.

The algorithm is as follows:
1. Initialize the value function `V(s)` arbitrarily for all states `s`.
2. Repeat until convergence:
    - Initialize aaction-value function `Q(s, a)` arbitrarily for all states `s` and actions `a`.
    - For all the states s and all the action a of every state:
        - Update the action-value function `Q(s, a)` using the Bellman equation.
        - Take the value function `V(s)` to be the maximum of `Q(s, a)` over all actions `a`.
        - Check if the maximum difference between `Old V` and `new V` is less than `theta`, where theta is a **small positive number** that determines the **accuracy of estimation**.
3. If the maximum difference between Old V and new V is greater than theta, then
    - Update the value function `V` with the **maximum action-value** from `Q`.
    - Go to **step 2**.
4. The optimal policy can be constructed by taking the **argmax** of the action-value function `Q(s, a)` over all actions `a`.
5. Return the optimal policy and the optimal value function.
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
