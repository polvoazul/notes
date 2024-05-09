# Modeling political affiliation.
In today's age (and historically) it is common that public politics falls into the usual left-wing / right-wing binary. This document is an attempt to model political affiliation so that we can better understand why this simple dichotomy is so resilient, even though no one seems to actually like it.
The hipothesis on this model can be justified in an addendum.

## Basic definitions
First lets start with some basic definitions to start this:

### Person
First we start with a population $P$, made up of many people $p_0, p_1, ..., p_n \in P$ in a political entity (say, a country). 

### Issue
Now, let $\gamma \in I$ be a set of _issues_. An issue is something like 'Should abortion be legal?'. For simplicity sake suppose all issues are yes / no questions. So a person's stance to an issue varies between strongly disagree, indifference and strongly agree.

### Stance
Now, each person have a specific number assigned to each issue. Lets define a function 'stance' $s\colon P \times I \rightarrow [-1, 1]$. It takes a person and an issue and outputs a value from -1 to 1, where the value is the person's stance on that issue, considering -1 to be Strongly Disagree, 0 is indiffernece, and 1 to be Strongly Agree. 

### Alignment
Two people p1, p2 are politically aligned if they agree on issues that matter to them. Also, issues you don't care about don't align you with someone. We can model that by saying that your alignment score is the dot product: $p_1 \cdot p_2 = \sum\limits_{\gamma \in I} s(p_1, \gamma) \cdot s(p_2, \gamma)$

Notice that in this model, if you are indifferent to an issue (your stance is close to 0), then, regardless of the other person's position, it wont contribute much to your alignemnt score.

Notice that alignemnt between two people vary between $K$ and $-K$ where $K = min(radicalism(p_1), radicalism(p_2))$.

--- 

### Enacting policies

Lets define a population's stance on an issue as $s(P, \gamma) = \underset{p \in P}{\text{avg}}(s(p, \gamma))$ just the average stance of all people.

Now, what people want to do is to enact a policy related to an issue. For that, say they need enough people to agree with that issue. So, say, an issue's $\gamma$ policy is enacted if for an _enactment threshold_ $\kappa_{enact}$, the population's stance is larger than that.
(Lets suppose $\kappa$ is constant for all issues. <sup>[Hypothesis1]</sup>)


$enacted(\gamma) = \begin{cases}
1 & \text{if } s(P, \gamma)> \kappa_{enact} \\
0 & \text{otherwise}
\end{cases}$

Lets say that the objective for people is to enact as many relevant policies as they can. Lets define their optimization target:

A person's utility is defined as: $util(p) = \sum\limits_{\gamma \in I} s(p, \gamma) (enacted(\gamma)\cdot W_e +  s(P, \gamma) \cdot W_p)$

Where $W_e$ is the happine gained by having the issue enacted, and $W_p$ is the popular support for that issue. Lets assume $W_e > W_u$ so there is a discontinous bump in utility when a policy that you care about is enacted (which makes the "winning votes" marginally more valuable).

### Coalitions

Now, if you want to enact policies you need to make people care for your issue. One way to do that is to form coalitions. Say, you will colude with someone if that increases your utility. To do that you must increase popular support for issues you like or even manage to enact them.

Lets define a coalition as a set of people $C$ such that 

$p_1 \cdot p_2 > \kappa_{coal}\qquad \forall\  p_1,\ p_2 \in C$

#### Coalition Building: Talk

You can engange in a talk with another person. Thus, changing your stance on issues so that the talk is a pareto improvement for those involved, making it viable.

Suppose both people have a fixed plasticity $k_{plasticity}$ budget to spend on modifying your beliefs. It should be easier to modify a belief closer to 0.

You can talk to $n$ people per month, and your plasticity is fixed for the month. <small> Interesting to see what happens if we vary n radically, say from 2,3 to 10, to 1000. Also what about plasticity (a younger - more plastic - vs old population)</small>

##### Sim 1



### Radicalization, reinforcment (preach to the choir, antagonize someone), capturing (preach to others)

### Rationalization, rethoric, argumentation, philosophical similarity (issue dependence)

### New issue appears (shocks, how coallitions adapt and adopt and conform)




### Overton Window


### Radicalism (wip)
We can model a person's radicalism as to how many issues are closer to extremes $p.radicalism = mean(|p(i)|)$.
<details><summary> Improvements </summary>
How to normalize this? Maybe we should have an issue weight as well. You can agree with something but dont care so much. Maybe condense weight into a single variable by using a different question like: how much time of your life would you give up to enact / repeal this? Nothing / Sacrifice your Life.
</details>


[Hypothesis1]: this