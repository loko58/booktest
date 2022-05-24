%====== SECTION========
(sec:standardmodels)=
# Essential Models of an Epidemiological Modelling Framework

In this section we discuss some simple epidemiological models  and introduce precursor models  consistent with our framework approach from {numref}`sec:framework`. The precursor models  will only consider some of the rules required to close the models, and will be studied in detail in subsequent publications. The precursor models focus on the mathematical modelling challenges  mentioned in {numref}`sec:intro:subsec:challenges`.



We repeat and specify further the general assumptions used to derive %and solve
the stochastic and differential equation formulations of the rules:

Mass Action Principle / Transmission
: The propensities of the single rules are directly proportional to the product of the number of individuals in the source involved species. For two species this is equivalent to individuals randomly bumping into each other. In this case we choose a frequency-dependent transmission {cite}`Mccallum2001`, with $\frac{1}{N}$ as part of the factor, neglecting the subtraction of deceased individuals. $N$ can be interpreted as fixed size of a reaction volume, where human beings departed because of COVID-19 left irreplaceable space in the society. Or differently interpreted, as a first approximation, the whole population is not shrinking too much due to disease-induced mortality. We are aware that this is, in some cases, particularly when mortality is high, an oversimplication that will have to be addressed in real-life applications in the future. For switching between different transmissions see {cite}`Arino2010`.

Closed Population
: We consider neither natural birth or death, nor migration. All deceased individuals died of COVID.

Exclusivity
: All types or subtypes are mutually exclusive, unless induced by the type hierarchy.   

Homogeneous Types
: All individuals of a specific type or subtype are homogeneous regarding to behaviour and disease, and equally affected by the respective rules. 

Immunity
: By recovering an individual acquires complete everlasting immunity and is not contagious any more, unless otherwise stated. 

Start
: We assume that at time $t = 0$ a certain number of individuals are infected / infectious. This becomes especially important if we consider rules with delays.

Exponential Waiting Times
: Waiting times of the rules are exponentially distributed, unless otherwise stated, for general distributions, see {cite}`Bog`.

Time-independent Rates
: Each rate is not explicitly time-dependent. In some special cases, e.g. lockdowns, we consider time-dependence in the sense of being constant between given times.

Independent Execution of Rules
: The execution of each rule is independent of the execution of any other rule.

Differentiability
: We consider ODE formulations as limit cases, i.e. as approximations for very large populations.

%------SUBSECTIONs are in extra (notebook) files!---------