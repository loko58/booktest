(sec:intro)=
# Introduction

This paper is a comprehensive study, but still only an initial attempt to apply novel mathematical modelling methods  to the COVID-19 pandemic. We propose a rule-based epidemiological framework and hope to use this approach to solve  the still-existing prognosis problem (see {numref}`sec:discussion:subsec:prognosis`), which is a general problem for most so-called complex systems {cite}`Ladyman:2020wf`. To summarise what the reader can expect, here is a list of novelties (some of which we aim to include in the future) of our rule-based framework:

Formal Language
: We use a formal mathematical language here which we call **rule-based** as a foundation of our mathematical models. Rule-based models rely on an extension of reaction kinetics which was first formulated to describe chemical reactions. It has the advantage that the rules can be interpreted both stochastically and deterministically. Moreover the rule-based systems have a mathematical structure which makes them very well suited for both science communication and rigorous mathematical analysis at the same time. We can both derive  stochastic processes and differential equations to describe the temporal dynamics of the pandemic and look for differences. There are several examples in {numref}`sec:standardmodels` where certain qualitative properties of the models with stochastic or deterministic interpretation stay invariant under update changes. In these cases the deterministic interpretation should be favoured, as the qualitative for differential equations is very well developed. However, we also found many cases where there is a difference between the stochastic and the deterministic interpretations of the rules differ. Therefore, to avoid ambiguity, we use the stochastic case as the generic simulation approach.

Mathematical Analysis & Simulation (Scientific Computing)
: We use different ways of understanding our rule-based mathematical models, and believe only in this combination we do really understand a mathematical model. A mathematical analysis, most often based on the deterministic interpretation as a differential equation, has the advantage to understand a relatively simple model more or less completely. Much in the same way a climate model can only be understood by a whole range of simulations, more complex models of a pandemic can only be understood by means of exhaustive simulation. The models in this publication are still quite modest, and we will go new ways of scientific publication by making the simulation scripts available to the public.

Model Variation
: We do not believe that in something as complex as the COVID-19 pandemic there is a single set of equations or code, like in individual based approaches, that can successfully predict the time course of the pandemic in some sense over a longer period, i.e. overcome the prognosis problem. We stick to the notion that a mathematical model should try to be minimal, i.e. minimally complex by some complexity measure {cite}`Ladyman:2020wf` as long as it is sufficiently predictive. This is related to the scientific principle called Occam's razor. As in {cite}`MacKay:2003wc`, Chapter 28, we consider Occam's razor as a natural outcome of coherent interference based on Bayesian probability.  In reality this reasoning will imply the optimally predictive model will change, i.e. we will have to walk through a model space, see {numref}`sec:intro:subsec:framework`.

Data Science
: The mathematical modelling community has too long neglected the data aspect. The COVID-19 pandemic has produced a massive amount of data, see {numref}`sec:discussion:subsec:data`. The model variation and prognosis problem can only be solved together with a firm link to data science. This is a major step we like to tackle in this project in future, however this is not an easy task. We are aware of recent advances in parametrisation of mathematical models, but still believe this is largely an unsolved problem of immense importance.

(sec:intro:subsec:challenges)=
## Challenges Triggered By The Pandemic

The COVID-19 pandemic posed a complex set of questions to the mathematical modelling community, with nearly daily new twists and turns. This paper intends to present a systematic framework of possible models that are designed to give answers to different aspects triggered by COVID-19 pandemic observations, i.e. empirical epidemiological data. Therefore, as discussed, we are not focusing on a particular model, as is often the case in applied mathematics papers, but follow a systematic model construction approach instead. In this first publication, we do not parametrise our models with data yet, but take basic empirical facts from the data to make **variable classification** choices. To have a first model choice skeleton, we observe the following fundamental empirical facts about COVID-19: 

Age:
From the start of observed coronavirus cases, the associated risks have strongly been age correlated {cite}`Palmer2021,ODriscoll2021,Mallapaty2021`.

Health Systems
: COVID-19 has put unprecedented pressure on healthcare systems worldwide. Due to the limited capacity of the national health systems or similar institutions, fatalities increased dramatically {cite}`ElBcheraoui2020,Haldane2021`.

Locations
: Numerous observations and simulation hint at the risk of infection being location dependent. Staying in closed rooms close to infected individual creates a higher risk of infection when compared to the same arrangement in open space {cite}`Wodarz2021`. We leave the investigation of location structure to future publications.

Immunity
: Immunity is now in the discussion in connection with the effectiveness of different vaccines, but it has a more general importance. For example, how long are individuals immune to new infections? Can immunity be gained in other ways, other than having had an infection or getting vaccinated? {cite}`Gaebler2021,Danchin2021`

Infectivity
: Infectivity is usually thought to be rather constant, only depending on outer conditions, such as location, i.e. closed narrow rooms are considered dangerous. But clearly infectivity follows a certain time course after an individual gets infected. On top of this, there is indication some individuals, perhaps depending on genetic variation, have a strong infectivity, called 'super-spreaders' {cite}`Lewis2021,Wolfel2020`. However, according to our knowledge, there is no clear data source for this yet.

Behaviour
: Given the location dependency of coronavirus infections, it became clear that behavioural choices by individuals play a crucial role in pandemic spread {cite}`Jentsch2020`. 

Mobility
: Mobility was identified as a major risk factor  from the beginning of the COVID-19 pandemic, as is the case for most individual to individual infection processes {cite}`Jentsch2020,Heroy2021,Nouvellet2021`.

Lockdowns
: The age and location dependency of the coronavirus infection rate implied the only successful policy to combat the pandemic was to isolate vulnerable parts of society, and close places where people would get crowded together. A general decrease of mobility would also decrease risk of infections {cite}`Lavezzo2020`.

Testing
: Observed time series report tested individuals. Testing is the only way to know how much infection is out there. There is then a fundamental difference between the intrinsic dynamics of total infected individuals, and how many of these individuals we know they are really infected (or not) because they are counted and reported through testing. From a modelling perspective, this requires to include new dynamic variables or sub-types to follow the time evolution of how many individuals tested positive (or negative), and for how long a test is still reliable {cite}`Mercer2021`.

Vaccination
: The rapid development of vaccines gave for the first time rise to the hope that a sufficiently large percentage of populations could be immunised safely to stop the spread of the disease (herd immunity) {cite}`Mallapaty2021a,Wang2021`.

Mutations
: These are extremely important at the moment of disease emergence {cite}`Dobson2015`, but also the latest twist of the COVID-19 pandemic was the rapid emergence of new mutations of the virus, with some variants observed to be more infectious, and deadlier {cite}`Wang2021`. 


All of these items in the discussion above can only be incorporated in mathematical models after a scientific classification. Using these models the future of  pandemics can be investigated, including the likelihood of major new outbreaks. The likeliness of viruses like the coronavirus crossing from animals like bats to humans is largely related to habitat and whole ecosystem destruction {cite}`Hassell:2021uu`. Is it possible to achieve herd immunity? How will herd immunity  be influenced by future mutations with different infectivities? Will COVID-19 be staying forever somewhere in the world, or will we be able to eradicate it with our policy measures, and vaccination programmes {cite}`Aschwanden2021`? 

In this paper we only consider **discrete** classifications, see {numref}`sec:intro:subsec:classification`. After the classification the resulting types will become variables in the mathematical model. However, becoming a variable is not the only possibility to project a dependency of above concepts into a mathematical model. We will introduce rates, a fundamental concept of any dynamic, time-dependent model, and we will also use types which results in a functional dependency of rates at which events occur, such as infections, on the system state.

(sec:intro:subsec:classification)=
## Classification as Structural Model Basis, Relation to Statistics

To understand our framework model approach, we must first discuss classifications, where objects are grouped into types. Following this idea, we arrive at a simple modelling question: what are the best types or classes[^footnote:classes] which when used to group human individuals serving as basic objects of a mathematical model, can successfully establish a predictive model of the COVID-19 pandemic on the basis of these group interactions? The grouping of individuals we call a type, because all individuals of the group must have a common property, i.e. a type. 

[^footnote:classes]: later becoming model variables, see {numref}`sec:intro:subsec:dynamics:sub:mc`.

We would like to emphasize that it is the type that is the basic entity that connects our mathematical model to empirical data. In this context the type can be interpreted as a random variable, and the grouping of individuals according to types corresponds to random experiments. Sometimes the random experiment is easy to perform. For example, if we consider a certain population and choose age classes as types, we can simply hand out questionnaires. However, if our type is something like 'immunity', elaborate lab work is needed which very likely can only be measured in random samples, i.e. sub-populations. 

The most important type of an individual in this context is the characterisation that an individual is 'infected', establishing the type $I$ as an example. More general, any epidemiological model considers interacting populations of finite-structured types of individuals which we can count inside some system boundaries, like a national or regional territory. Let $\mathcal{O}$ be the set of **basic objects**, here human individuals of a larger population. The individuals form the system components at the micro-level. In principle, we would need to let $\mathcal{O}$ to be parametrised by time, because we could allow the set to change when objects either enter or leave the system. But in this description of the pandemic, we assume the population size is fixed, therefore no individuals are allowed to 
'enter' or 'leave'. This means, if we introduce a type $D$ for 'dead' later on, we still count individuals of this type to be part of the population. The single layer classification of an $SIR$-model is shown in {numref}`fig:sec:model:subsec:types`. 

:::{figure} ./figuresRBSEa1/basic_classification.svg
:name: fig:sec:model:subsec:types

The object set for humans based epidemiology are usually individuals. Here, we have three types in the classical classification of human individuals, susceptible ($S$), infected ($I$) and recovered ($R$) individuals. This will be the basic classification of all models discussed, with additional classifications on top of this structure. An edge from individuals to the types, here disease states, indicates the individual are of this type.
:::

The types are also interpreted as a scientific classification of individuals. For each classification we require that an individual is exactly of one type. However, there are possibly many different relevant classifications of individuals, such as age, or disease state etc., and these can exist in parallel. In addition, individuals can be of a certain immunity type, and they can have a certain infectivity, also a type. Let $\mathcal{T}=\{T_1,\ldots, T_s\}$, $s \in \mathbb{N}$, denote the set of all possible types or individual characteristics, $s$  different types in total. It follows that we have created a hypergraph $H = H(\mathcal{O},\mathcal{T})$, i.e. the types form a set of hyperlinks, which are non-overlapping. In {numref}`sec:intro:subsec:intern_extern` we discuss how certain types, like age or location, are either internal or external states of an individual, and have very likely so-called sub-types. The best example is age, where the number of chosen age classes form the sub-types of the age type, i.e. the classification by age. The state of the system is given by the number of basic objects of some type, here number of human individuals that have a type at some time $t$. We use the notation that the number of these individuals of type $T_i$ is given by $n_i(t) \in \mathbb{N}_0$ for all $i=1,\ldots,s$. 

Of course, it is possible that there is more than one system **compartment** in which objects can reside. In this case the types are indexed by compartment, making them compartmental sub-types. An obvious generalisation of the situation discussed here are **multiple compartments**, and such models will have to incorporate movement between compartments. Multi-compartment models can be used to consider **geographical** models of the epidemic. We leave this for future publications.

%------SUBSECTION---------
(sec:intro:subsec:classification:sub:rules)=
## Rules

As a next step we introduce rules (or reaction channels). Let $\mathcal{R}=\{R_1,\ldots, R_r\}$, $r \in \mathbb{N}$,  be the finite set of rules constituting the epidemiological system.  Each rule $R_j$ with $j=1,\ldots,r$, takes the form

:::{math}
:label: eq:sec:model:subsec:reaction:reactionscheme
\begin{eqnarray}
    \sum_{i=1}^{s} \alpha_{ij}  T_i  \xrightarrow{k_j} \sum_{i=1}^{s} \beta_{ij}  T_i,
\end{eqnarray}
:::

where $k_j$ denotes the rate constant of rule (reaction) $R_j$. The sums have to be understood as so-called formal sums (as usual in reaction systems). The coefficients $\alpha_{ij} \in \mathbb{N}_0$ are the stoichiometric coefficients of types $T_i$, $1 \le i \le s$, of the {\bf source} side, and  $\beta_{ij}\in \mathbb{N}_0$ are the stoichiometric coefficients of types $T_i$ of the {\bf target} side of  transition or reaction $R_j$. These stoichiometric coefficients describe changes of individual numbers due to events, such as an infection. Note that either all stoichiometric coefficients on the source side, or all stoichiometric coefficients on the target side are allowed to be zero. In this case, the formal sum is replaced by the empty set  $\emptyset$. 

Note that also rules are subject to confirmation by empirical data. In this case the random variable is the rule itself, and the random experiment consists of observing such a transition in the population. For example, it has never been observed that more than one infected person is needed to infect a susceptible person in the COVID-19 pandemic, therefore the stoichiometric coefficients are also observables, i.e. random variables linked to experiments.


%------SUBSUBSECTION---------
(sec:intro:subsec:classification:sub:global)=
### Global Information

Rules are generalisations of reactions as used in so-called reaction kinetics. In epidemiology, but also other areas of science, there is a need to additionally introduce **global information** into the system description. The idea is that individuals know, for example from the daily news, how many infected people there are in their area, and possibly change their behaviour accordingly. Note that in chemical reaction systems, such global information is completely missing, the atoms or molecules follow only local information, i.e. they experience bumping into each other, but they do not know anything about the reaction partners before a reaction event. 

We assume that the global information is collected from the type set $\mathcal{T}=\{T_1,\ldots, T_s\}$, $s\in \mathbb{N}$. In this context  $\mathcal{T}$ will be referred to as {\bf local types}. We introduce the **global information operator** $\Delta$ and a **global information type set**, or short **global types**, given by $\mathcal{G}=\{G_1,\ldots, G_g\}$, $g \in \mathbb{N}$. Now let

$$ \Delta \colon \mathcal{T} \to \mathcal{G}. $$

Therefore, $\Delta$ takes information from the types of the model, and maps it to global information which can be made known to the system. For example, in an age-structured model, let $\mathcal T_I=\{ I_1, I_2, \ldots, I_n\}$ denote the types of infected individuals inside $n$-different age classes. Let $\mathcal{G}=\{G_I\}$ be a one-dimensional global information type set, here interpreted as all infected individuals in the system. Then $\Delta$ is given implicitly by the formal sum

$$ G_I := \sum_{i=1}^{n} I_i. $$

In general we assume

$$ G_i := F_i(\mathcal{T}), \;\;\; i=1,\ldots,g, $$

with $F_i$ some function mapping $s$ many types to one type. When we introduce a state  $n_i(t) \in \mathbb{N}_0$ of type $T_i$ at system time $t\geq 0$ for $i=1,\ldots,s$, see{numref}`sec:intro:subsec:dynamics:sub:mc`, then global types will at the same time have derived numerical values.


%------SUBSECTION---------
(sec:intro:subsec:intern_extern)=
## Sub-Classifications, Internal and External Individual States

We consider now the case where we need to further differentiate types into sub-types, which we often also interpret as 'internal states' of individuals. The best example in our current context are age classes, but in fact already the $S$-$I$-$R$ classification can be interpreted as sub-types of a general disease state. Sub-types therefore are a very important modelling idea for infectious diseases. Because types can now exist of different sub-types, we need to introduce their frequency distribution. Define $l_i \in \mathbb{N}$ as the number of sub-types of type $i$ for $1 \le i \le s$. Let $\mu_{ij}^\alpha$ denote the frequency of the sub-type $\alpha$, $1\le \alpha \le l_i$, needed for the source terms in rule  $R_j$, called the **source frequency**. We have

$$\mu_{ij}^\alpha =  \frac{n_{ij}^{s,\alpha}}{m^s_{ij}},$$

where $n_{ij}^{s,\alpha} \in \mathbb{N}$ is the number of objects (individuals) of type $i$ and sub-type $\alpha$ needed for the source terms in rule  $R_j$, and $m^s_{ij} := \sum_{\alpha = 1}^{l_i} n_{ij}^{s,\alpha}$ is the total number of objects of type $T_i$ needed for reaction $R_j$.  The symbol $s$  denotes 'source'. Clearly, we  have 

:::{math}
:label: eq:sec:model:subsec:reaction:frac:1
\begin{equation}
\sum_{\alpha=1}^{l_i} \mu_{ij}^\alpha = 1 \; \; 
\end{equation}
:::

for all types  $i=1,\ldots,s$ and all reactions $R_j$ for $j=1,\ldots,r$. 
Similarly, let $\nu_{ij}^\alpha$ denote the frequency of the sub-type $\alpha$, $1\le \alpha \le l_i$ after rule  $j$ has been triggered, called the **target frequency**. We have

$$\nu_{ij}^\alpha =  \frac{n_{ij}^{t,\alpha}}{m^t_{ij}},$$

where $n_{ij}^{t,\alpha} \in \mathbb{N}$ is the number of objects (individuals) of type $i$ of sub-type $\alpha$ as result of the event described by rule  $R_j$, and $m^t_{ij} := \sum_{\alpha = 1}^{l_i} n_{ij}^{t,\alpha}$.  Here the symbol $t$ denotes 'target'. Again we have

:::{math}
:label: eq:sec:model:subsec:reaction:frac:2
\begin{equation}
\sum_{\alpha=1}^{l_i} \nu_{ij}^\alpha = 1 
\end{equation}
:::

for all types  $i=1,\ldots,s$ and all reactions $R_j$ for $j=1,\ldots,r$.
The constants $\mu_{ij}^\alpha,\nu_{ij}^\alpha\in \mathbb{Q}$ specify the frequency of individuals that are necessary for each rule to be realised. They are therefore the frequency analogues of stoichiometric coefficients. Finally we can now write every possible event or rule (or reaction) $R_j$ in the more general form

:::{math}
:label: eq:reactionscheme:generalised
\begin{eqnarray}
\sum_{i=1}^{s} \gamma_{ij} \sum_{\alpha=1}^{l_i}  \mu_{ij}^\alpha T^\alpha_i  \xrightarrow{k_j} \sum_{i=1}^{s} \delta_{ij} \sum_{\alpha=1}^{l_i}  \nu_{ij}^\alpha T^\alpha_i,
\end{eqnarray}
:::

for $j=1,...,r$, where the sums have to be understood again as  formal sums. The coefficients $\gamma_{ij} \in \mathbb{N}$ are the stoichiometric coefficients of types $T_i$, $1 \le i \le s$, of the source side, and  $\delta_{ij}\in \mathbb{N}$ are the stoichiometric coefficients of types $T_i$ of the target side of rule $R_j$ with rate constant $k_j$. These stoichiometric coefficients describe changes of object numbers, independent of the sub-type of an object of any type. Note that if all types have just a single state or configuration, then the scheme is equivalent to a traditional reaction scheme {eq}`eq:sec:model:subsec:reaction:reactionscheme` by construction. The generalised scheme {eq}`eq:reactionscheme:generalised` is useful, for example, we can use it to establish a varying number of discrete age classes in a single rule.