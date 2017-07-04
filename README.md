Viewing the Jupyter Notebooks from nbviewer is encouraged because GitHub is still not fully integrated with the Jupyter Notebook:
http://nbviewer.jupyter.org/github/suyunu/General-Assignment-Problem/blob/master/sa-gap.ipynb

# Simulated Annealing on General Assignment Problem

In this project, we tried to solve General Assignment Problem (GAP) with Simulated Annealing (SA).

## General Assignment Problem

There are a number of agents and a number of tasks. Any agent can be assigned to perform any task, incurring some cost. Moreover, each agent has a budget and the sum of the costs of tasks assigned to it cannot exceed this budget. It is required to find an assignment in which all agents do not exceed their budget and total cost of the assignment is minimized.

## Solution Representation

To represent the solution, I used a simple list structure. Cells of the list are jobs and numbers in the cells are the agents assigned to that job.

Example solution representation:
[7, 1, 0, 4, 4, 2, 4, 1, 5, 6, 3, 4, 5, 5, 1, 5, 2, 1, 4, 0, 7, 7, 5, 7, 5, 2, 3, 0, 2, 1, 7, 6, 6, 7, 3, 4, 3, 6, 3, 6]

## Algorithm

We used simulated annealing with some modification to solve General Assignment Problem. First, I will write the pseudocode of my simulated annealing and then try to explain important parts like neighborhood structure and stopping condition.

### Pseudocode

<ol>
<li>Compute an initial solution $X$ and choose an initial temprature $T>0$ and a repetition factor $L$</li>
<li>As long as the stopping criterion is not satisfied perform the following steps:</li>
    <ol>
    <li>Do the following $L_k$ times</li>
        <ol>
        <li>Generate a random solution in the neighborhood $x' \in N(x)$.</li>
        <li>Compute $\Delta = f(x') - f(x) + unfit(x')$ </li>
        <li>Generate a random number $0<u<1$</li>
        <li>If $\Delta<0$ or u < $e^{-\frac{\Delta}{T_k}}$ then set $x \gets x'$ </li>
        <li>If $x$ is feasible and $f(x) < f(x^*)$ then set $x^* \gets x$</li>
        </ol>
    <li>Update $T_k$ and $L_k$</li>
        <ol>
        <li>$T_{k+1} \gets \alpha * T_k$</li>
        <li>$L_{k+1} \gets \gamma * L_k$</li>
        </ol>
    </ol>
<li>Report the incumbent solution</li>
</ol>