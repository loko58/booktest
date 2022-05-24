%======SECTION========
(sec:framework)=
# Modelling Framework

We are now able to present our epidemiological framework in more detail. We first look briefly at the connection to structural (static) modelling.

%------SUBSECTION---------
(sec:intro:subsec:dynamics)=
## Introducing Dynamics

%------SUBSUBSECTION---------
(sec:intro:subsec:dynamics:sub:mc)=
### Continuous-Time Markov Chains Including Global Information

In this section, we formulate reactions {eq}`eq:sec:model:subsec:reaction:reactionscheme` as a continuous-time Markov chain. We regard the size/number $n_i(t)  \in \mathbb{N}$ of type $T_i$ at system time $t\geq 0$ for $i=1,\ldots,s$ as discrete random variables with values in $\{0,\ldots,N\}$.  For defining the transition probabilities associated with the stochastic process we assume that the process is time-homogeneous (autonomous), i.e.,  while no event occurs, the transition probabilities remain constant, and depend only on the time between events $\Delta t$, but not on the specific time $t$. We observe the system from time $0$ up to time $T>0$. In addition, we suppose that the Markov property is satisfied, that is, the probability distribution of a future state of the stochastic process at time $t+\Delta t$ only depends on the current state at time $t$, but not on any state prior to $t$.  With each type $T_i$ having an associated state $n_i(t)  \in \mathbb{N}$, the global type set $\mathcal{G}=\{G_1,\ldots, G_g\}$, see {numref}`sec:intro:subsec:classification:sub:global`, get derived numerical values which are. We assume at system time $t\geq 0$ to obtain the {\bf global state vector} $\theta(t) := (\theta_1(t), \ldots, \theta_g(t))$, with $\theta_i \in  \mathbb{R}$ for $1 \le i \le g$. Given the system is in state (or configuration) $n$, we introduce the propensities $\kappa_j(t^\prime,n)$ for $j=1,\ldots,r$. Here, the propensity $\kappa_j(t^\prime, n)$ of the $j$th reaction $R_j$ is the probability that the $j$th event/reaction occurs within an infinitesimal time interval, the last event in the entire system happened at $t^\prime$, and is given by

:::{math}
:label: eq:propensity
\begin{align}
 \kappa_j(t^\prime, n) = k_j f_j (\theta(t^\prime,n))  \prod_{i=1}^s   \begin{pmatrix} n_i \\ \alpha_{ij} \end{pmatrix},
\end{align}
:::

where $\kappa_j(\theta(t^\prime))$ denotes the global state dependent propensities of reaction $R_j$, $k_j$ is the reaction constant, and the combinatorial factor reflects the number of ways in which reaction $R_j$ may happen, see {eq}`eq:sec:model:subsec:reaction:reactionscheme`. The functions $f_j$, $1 \le j \le r$, are called **global information functional responses**. These functions modify the rule execution constants $k_j$ according to the state of the given global information vector $\theta$.

:::{prf:remark}
:label: rem:no-explicit-time-dependence-notation
Note that the notation $\kappa_j(t^\prime, n)$ suggests time-dependence, which is not the case, therefore simply writing $\kappa_j(n)$ is equally valid and will be adopted sometimes. The notation is just a reminder that the propensity depends on the last event that happened in the system, as then the global information available to the system is updated. Time-homogeneity and the Markov property are still valid piecewise. In more sophisticated situations however, such as externally imposed lockdowns, the time-dependency of the propensity $\kappa_j$ will have to be considered explicitly.
:::


We use some standard algebraic expressions for global information functional responses $f_j(\theta)$ in case $\theta$ is one-dimensional and non-negative:

Simple Saturation
: $$ f_j(\theta) := \frac{1}{1+ \lambda_j \theta}. $$ 
Here $\lambda_j$ is an additional positive parameter. We also consider $ \frac{1}{f_j}$ in case the functional response has to be monotonically decreasing, due to modelling purposes.

Michaelis-Menten
: $$ f_j(\theta) := \frac{1}{\lambda_j + \theta}. $$ 
Here $\lambda_j$ is an additional positive parameter. Alternatively, we may consider $ \frac{1}{f_j}$ in case the functional response is monotonically decreasing.

Exponential
: $$ f_j(\theta) :=  \lambda_j e^{-\lambda_j \theta}. $$
Here $\lambda_j$ is an additional positive parameter. The exponential functional response gives rise to a probability measure $P_j$, with distribution function $F_j (\theta) = 1 -  \lambda_j e^{-\lambda_j \theta}$, and is called **exponential distribution**. For $\epsilon>0$, we define a loss rate $\lambda(\theta)$ by

$$ \lambda(\theta) := \lim_{\epsilon \to 0} \frac{P((\theta,\theta + \epsilon])}{P((\theta,\infty))}. $$

It follows that

$$ \lambda(\theta) =  \frac{f_j(\theta)}{1-F_j (\theta)}. $$

Weibull
: $$ f_j(\theta) :=   \lambda_{j,1} \lambda_{j,2} \theta^{ \lambda_{j,2} - 1} e^{- \lambda_{j,1} \theta^{\lambda_{j,2}}}. $$
Here $\lambda_{j,1}, \lambda_{j,2}$ are  positive parameters. Note that for $\lambda_{j,2}=1$, $f_j$ reduces to the exponential distribution. 


If the global state vector $\theta(t) := (\theta_1(t), \ldots, \theta_g(t))$ has dimension $g>1$, then each of the global information functional responses is assumed to be given in a multiplicative way by $g$-many sub-functionals, each dependent on one component of $\theta$:

$$ f_j (\theta) = f_{j,1}(\theta_1)f_{j,2}(\theta_2)\cdots f_{j,g}(\theta_g), $$

where each  $f_{j,i}$ is given by one of the one-dimensional algebraic expressions given above. From a modelling point of view, this assumes different global information states have an independent influence on the event rate of a rule, such as an infection. An example would be avoidance and mobility. Avoidance can be modelled by a monotonically decreasing functional response, mobility as a monotonically increasing functional response. Now, based on the assumption that at most one reaction can occur within an infinitesimal time interval $\Delta t$, the transition rates for the Markov process, given that the system is in state $n$, can then be approximated as $\kappa_j(n)\Delta t$ for reaction $R_j$ to occur within time interval $\Delta t$ and $1-\sum_{j=1}^r \kappa_j(n)\Delta t$ for no reaction to occur within time interval $\Delta t$. To simulate the sample paths of the continuous-time Markov chain, one can apply the Gillespie algorithm. The simulation of many trajectories of the system  allows the computation of the statistics of evolution. 

%------SUBSUBSECTION---------
(sec:intro:subsec:dynamics:sub:gillespie)=
### Gillespie's Algorithm

The most important stochastic update idea for epidemiological models is **Gillespie's Stochastic Simulation Algorithm (SSA)** and its generalisation. It is the main algorithm used to study the stochastic evolution of the models presented in this paper. This evolution arises due to the interactions among types $\mathcal{T}$ and, in the language of reaction schemes, can be expressed  as a reaction network. Reaction $R_j$ is given by Equation {eq}`eq:sec:model:subsec:reaction:reactionscheme` for $j=1, \ldots, r$, where $k_j$ denotes the rate constant of reaction $R_j$. Interpreting a reaction as a rule, we will use the terms *reaction* and *rule* interchangeably. Each process occurs with a *propensity* $\kappa_j(n)$, defined as

:::{math}
:label: eq:Rj
\begin{equation}
 \kappa_j(n) := k_j \, h_{j} (n),
\end{equation}
:::

where  

$$ h_j(n) := \prod_{i=1}^s   \begin{pmatrix} n_i \\ \alpha_{ij} \end{pmatrix}.$$

Here, the combinatorial factor $h_j$ describes the number of ways in which reaction $R_j$ takes place. As in the original paper {cite}`Gillespie1976` by Gillespie, we make the following assumption:

:::{prf:axiom}
:label: Gillespie_assumption
Reaction $R_j$ occurs within a time interval $\Delta t$ with probability $\kappa_j(n)\Delta t$.
:::

For a given population with system configuration $n \in \mathbb{R}^s$, one can  show (see {cite}`Gillespie1976`) that the probability density associated with the occurrence of $R_j$ is given by

:::{math}
:label: eq:gillespie_prob_Pi
\begin{equation}
\Phi_j(n,t)=\kappa_j(\theta(n),n)\exp\left(-\sum_{l=1}^r\kappa_l(\theta(n), n)\,t\right)
\end{equation}
:::

as a function of time $t$. The probability that reaction $R_j$ ever occurs is given by 

:::{math}
:label: eq:rho_i_standardgil
\begin{equation}
\rho_j(n)=\int_0^\infty \di t'\,\Phi_j(n,t')=\frac{\kappa_j(\theta(n),n)}{\sum_{l=1}^r \kappa_l(\theta(n),n)}
\end{equation}
:::

for  $j\in\{1,...,r\}$. The rules given by Equation {eq}`eq:sec:model:subsec:reaction:reactionscheme`  generate a stochastic process which satisfies the Markov property due to {prf:ref}`Gillespie_assumption`. This process is  the starting point for the derivation of the master equation, describing the time evolution of the probability distribution of the system as a whole (see {cite}`Gardiner`). The probability density in {eq}`eq:gillespie_prob_Pi` can  be interpreted  in terms of reaction waiting times and, in fact, instead of Assumption {prf:ref}`Gillespie_assumption`, we can equivalently assume that  reaction $R_j$ occurs with an *exponentially distributed* reaction waiting time. In {cite}`Gillespie1976` Gillespie showed that the master equation can be exactly solved through the construction of realisations of the stochastic process associated to {eq}`eq:sec:model:subsec:reaction:reactionscheme`. This is achieved through the following algorithm, where $::=$ denotes replacement:

:::::{prf:algorithm} Gillespie Algorithm
:label: alg:sec:model:subsec:gillespie

::::{tab} pseudo-code
0. Initialize the starting time $t$, the system configuration $n=(n_1,\ldots,n_s)$ and the rate constants $k_j$ for $j=1,\ldots,r$. 
1. Generate two random numbers $r_1, r_2$ uniformly distributed in $[0,1]$.
2. Set $\Phi:= \sum_{l=1}^r \kappa_l (n)$ and compute $\tau:= -\frac{1}{\Phi} \ln r_1$.
3. Set $t::=t+\tau$ as the time of the next rule execution.
4. Determine the reaction $R_i$ which is executed at time $t$ by finding $i$ such that

:::{math}
:label: eq:conditiongillespie
\begin{align}
 \frac{1}{\Phi} \sum_{l=1}^{i-1}\kappa_l (n)<   r_2 \leq \frac{1}{\Phi} \sum_{l=1}^{i}\kappa_l (n).
\end{align}
:::

5. Execute rule $R_i$ and update the new system configuration $n$.
6. Go to step 1 if $t<T$, otherwise stop.
::::

::::{tab} python
:::python
def Gillespie(T, N, Sinit, Iinit, Rinit, Dinit,
              seed,
              updateStates, updatePropensities,
              **kwargs
              ):
    
    # Inital values
    t = 0.
    S = Sinit
    I = Iinit
    R = Rinit
    D = Dinit
    
    # Vectors for time series
    time = [t]
    Ss   = [S]
    Is   = [I]
    Rs   = [R]
    Ds   = [D]

    
    # Random Generator
    rg = np.random.RandomState(seed)

    # Main loop
    while t < T:
        if (I == 0): # no infectives any more means epidemic dies out
            break
            
        # First uniformily distributed ranmdom number for reaction time
        r1  = rg.uniform(0., 1.)
        
        # Propensities calculation
        kappa = updatePropensities(S, I, R, D, N, **kwargs)
        Phi   = kappa.sum()
        
        # waiting time tau
        tau = -np.log(r1) / Phi
        t   = t + tau
  
        # Second uniformily distributed random number for executed reaction
        r2 = rg.uniform(0., 1.)
        
        # Rule determined to be executed
        bins = np.cumsum(kappa) / Phi
        rExc = np.searchsorted(bins, r2, side='right')
        
        # Update states
        S, I, R, D = updateStates(rExc, S, I, R, D)
        
        # Append new values
        time.append(t)
        Ss.append(S)
        Is.append(I)
        Rs.append(R)
        Ds.append(D)
        
    return (time, Ss, Is, Rs, Ds)
:::
::::
:::::

The random numbers generated in {prf:ref}`alg:sec:model:subsec:gillespie` are used for determining the index $i$ of the next rule to be triggered, and the time interval $\tau$ for reaction $R_i$ to occur. By the definition of $\rho_l(n)$ in {eq}`eq:rho_i_standardgil` we have

$$\frac{1}{\Phi} \sum_{l=1}^i \kappa_l(n)=\sum_{l=1}^i \int_0^\infty \di t'\,\Phi_l(n,t')=\sum_{l=1}^{i}\rho_l (n)$$

in step 4 in {prf:ref}`alg:sec:model:subsec:gillespie`. We use Gillespie's algorithm to simulate the model dynamics, based on the assumption that the processes have exponentially distributed waiting times or, equivalently, that they are all Poisson processes, like atomic or molecular mixtures of gases or liquids. In complex systems formed by types which are heterogeneous and evolve through diverse interactions that cannot be always characterised by *exponentially distributed waiting times*, therefore the Gillespie approach is not fully adequate. It is thus very important to have a generalisation of Gillespie's algorithm that allows us to study systems driven by processes with different waiting time distributions and not necessarily exponentially distributed waiting times. Several generalisations exist in the literature, see {cite}`CCTRW`, {cite}`Gillespie_ME_with_waiting_times`, {cite}`Masuda` and {cite}`Bog` for instance, 
where a generalised Gillespie algorithm based on a generalised master equation in the form of an integro-differential equation {cite}`CCTRW` may be considered.