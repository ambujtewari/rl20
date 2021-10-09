# Annotated Bibliography on Regret Analysis of Markov Decision Processes (MDPs) and Related Models

Claude-Nicolas Fiechter
[Efficient reinforcement learning](https://doi.org/10.1145/180139.181019)
COLT 1994 \
One of the earliest paper to apply PAC style analysis to reinforcement learning. Discounted setting with resets is considered.
____
Apostolos N. Burnetas, Michael N. Katehakis
[Optimal Adaptive Policies for Markov Decision Processes](https://www.jstor.org/stable/3690147)
Math of OR 1997 \
For the class of completely ergodic (aka irreducible) MDPs, logarithmic (in time) upper and lower bounds on regret are provided. These bounds are <i>instance dependent</i> in the sense that the constants involved depend on the MDP. Algorithm is based on optimism: action selection is based on indices that are inflations of the right hand side of average reward optimality equations.
____
Michael Kearns, Satinder Singh
[Near-Optimal Reinforcement Learning in Polynomial Time](https://doi.org/10.1023/A:1017984413808)
MLJ 2002 \
A landmark paper that gave the first near-optimal polynomial time and sample complexity algorithm for learning
in MDPs. Considers learning from a single long trajectory (i.e., no resets) in <i>unichain</i> MDPs (incidentally, it is
[NP-hard](https://doi.org/10.1016/j.orl.2006.06.005)
to determine if an MDP is unichain or not) but doesn't exactly analyze regret. Instead asks a very related question (in the undiscounted case): how many time steps and computation are needed before the agent's average reward, with high probability, is within
<img src="https://latex.codecogs.com/gif.latex?\epsilon" title="\epsilon" />
of the optimal reward among all policies with 
<img src="https://latex.codecogs.com/gif.latex?\epsilon" title="\epsilon" />-return
mixing time bounded by
<img src="https://latex.codecogs.com/gif.latex?T" title="T" />?
The algorithm E<sup>3</sup> (Explicit Explore or Exploit) is proposed and shown to have polynomial
(in number of states and actions, in
<img src="https://latex.codecogs.com/gif.latex?1/\epsilon" title="1/\epsilon" />,
<img src="https://latex.codecogs.com/gif.latex?1/\delta" title="1/\delta" />,
and in
<img src="https://latex.codecogs.com/gif.latex?T" title="T" />)
sample and computational complexity. E<sup>3</sup> is a model-based algorithm since it builds a <i>partial</i> model of the MDP which is good for the set of <i>known</i> states (i.e., a state visited enough times). The algorithm starts off by engaging in <i>balanced wandering</i>, i.e., taking actions that have been tried the least number of times. When the algorithm reaches a known state, it performs two offline computations on the partial model: an attempted exploitation where the algorithm tries to find a high return policy based on the partial model. If attempted exploitation fails, then the algorithm finds an exploration policy designed to leave the set of known states with non-trivial probability. The analysis hinges on two key lemmas. The <i>simulation lemma</i> guarantees that the
<img src="https://latex.codecogs.com/gif.latex?T" title="T" />-step
return of a policy in the actual model restricted to known states and the partial model are close. The <i>explore or exploit lemma</i> guarantees that the algorithm will either find a way to obtain near optimal returns using only the known states or it will find a way to quickly exit the set of known states.
The paper leaves practical implementation, model-free algorithms, partial observability, and function approximation as challenges for future work.
____
Ronen I. Brafman, Moshe Tennenholtz
[R-MAX - A General Polynomial Time Algorithm for Near-Optimal Reinforcement Learning](http://www.jmlr.org/papers/volume3/brafman02a/brafman02a.pdf)
JMLR 2002 \
The authors begins by noting the E<sup>3</sup> does not use optimism in the face of uncertainty principle and explicitly separates exploration from exploitation. The OFU principle goes back at least to the [1996 survey](https://doi.org/10.1613/jair.301) by Kaelbling, Littman and Moore where it is discussed in Section 2.2 titled "Ad-hoc techniques". [Section 2.7](http://www.incompleteideas.net/book/first/ebook/node21.html) titled "Optimistic Initial Values" in Sutton and Barto's book. This paper suggests that such a separation possibly does not work in adversarial settings and instead rely on implicit exploration driven by the OFU principle: states that have not been visited enough are given the maximum possible reward R<sub>max</sub> (hence the name of the algorithm) in a fictitious MDP. Following an optimal policy in the fictitious MDP has an interesting and useful propery in the real MDP: it is always either optimal or it leads to efficient learning. Unlike E<sup>3</sup>, R-MAX works in a more general setting than that of MDPs, namely that of two-player fixed-sum stochastic games. It guarantees near-optimal (in the "safety" or probabilistic maximin sense with respect to adversary's strategy) return in time polynomial in number of states and actions, in
<img src="https://latex.codecogs.com/gif.latex?1/\epsilon" title="1/\epsilon" />,
<img src="https://latex.codecogs.com/gif.latex?1/\delta" title="1/\delta" />,
and in the mixing time. Note that, in repeated games, the mixing time is 1 and the algorithm simplifies considerably since there is no need to learn transition probabilities.
____
Sham Kakade
[On the Sample Complexity of
Reinforcement Learning](https://homes.cs.washington.edu/~sham/papers/thesis/sham_thesis.pdf)
PhD Thesis 2003 \
Part 3 of this influential PhD thesis defines and studies the <i>sample complexity of exploration</i>. The definition is self-referential in the sense that the learning algorithm itself is considered as a non-stationary policy. As such it has a expected future return, or value, at any state it visits. One can ask whether this value is more than
<img src="https://latex.codecogs.com/gif.latex?\epsilon" title="\epsilon" />
worse compared to the value of the optimal policy in that state. The total number of time steps where this happens is defined as the sample complexity of exploration. This sample complexity definition directly led to the later definition of <i>PAC-MDP algorithms</i> where the sample complexity has to be polynomial in relevant aspects of the input (and efficient PAC-MDP if the algorithm is also computationally efficient). For example, see the Strehl, Li and Littman (2009) paper below. In Chapter 8 of this thesis, upper and lower bounds on the sample complexity of exploration are provided. Upper bounds are proved using the R-MAX algorithm of Brafman and Tennenholtz (2002) mentioned above. The lower bounds do not match the upper bounds, an issue related to the question of whether an accurate model needs to be built in order to guarantee optimal sample complexity.

Note that PAC-MDP notion is quite different from regret minimization: a sublinear regret algorithm need not be PAC-MDP and a PAC-MDP algorithm can have linear regret (see Section 6.3.2 of [this article](https://dx.doi.org/10.1007/978-3-642-27645-3_6) for an interesting discussion)
____
Peter Auer, Ronald Ortner
[Logarithmic Online Regret Bounds for Undiscounted Reinforcement Learning](https://papers.nips.cc/paper/3052-logarithmic-online-regret-bounds-for-undiscounted-reinforcement-learning.pdf)
NIPS 2006 \
Considers unichain MDPs in the undiscounted setting and provides logarithmic (in time) regret bounds for an OFU algorithm called UCRL. Note the evolution of ideas from E<sup>3</sup> to R-MAX to UCRL. E<sup>3</sup> has explicit known/unknown state distinction and explicit explore/exploit distinction. R-MAX has implicit exploration but still retains the explicit known/unknown state distinction. UCRL eliminates the explicit known/unknown state distinction and instead uses implicit exploration driven by high confidence bounds on the transition and reward functions. The leading term in the regret bound scales as
<img src="https://latex.codecogs.com/gif.latex?\frac{S^5AT_M\kappa_M^2}{\Delta^2}\log&space;T" title="\frac{S^5AT_M\kappa_M^2}{\Delta^2}\log T" />
where
<img src="https://latex.codecogs.com/gif.latex?T_M" title="T_M" />
is the worst case mean first passage time (to reach one state from another) over all pairs of states and over all policies,
<img src="https://latex.codecogs.com/gif.latex?\kappa_M" title="\kappa_M" />
is a sensitivity parameter defined as the ratio between the mean passage time to another state and the return time to a given state, and
<img src="https://latex.codecogs.com/gif.latex?\Delta" title="\Delta" />
is the smallest (non-zero) suboptimality gap among policies. The paper conjectures that a modified version of UCRL will enjoy regret bounds in communicating MDPs and it therefore anticipates the UCRL2 algorithm.
____
Alexander L. Strehl, Lihong Li, Michael L. Littman
[Reinforcement Learning in Finite MDPs: PAC Analysis](http://www.jmlr.org/papers/volume10/strehl09a/strehl09a.pdf)
JMLR 2009 \
A nice summary of PAC-MDP results up to 2009. Uses the sample complexity definition of Kakade (2003) to define PAC-MDP learning algorithms. Two sets of mutually incomparable sample complexity bounds are given. The upper bounds are
<img src="https://latex.codecogs.com/gif.latex?\tilde{O}(S^2&space;A/(\epsilon^3(1-\gamma)^6))" title="\tilde{O}(S^2 A/(\epsilon^3(1-\gamma)^6))" />
for R-MAX, and
<img src="https://latex.codecogs.com/gif.latex?\tilde{O}(S&space;A/(\epsilon^4(1-\gamma)^8))" title="\tilde{O}(S A/(\epsilon^4(1-\gamma)^8))" />
for [Delayed Q-learning](https://doi.org/10.1145/1143844.1143955).
The lower bounds are 
<img src="https://latex.codecogs.com/gif.latex?\Omega\left(\frac{SA}{\epsilon(1-\gamma)^2}\ln&space;\frac{1}{\delta}\right)" title="\Omega\left(\frac{SA}{\epsilon(1-\gamma)^2}\ln \frac{1}{\delta}\right)" />
and
<img src="https://latex.codecogs.com/gif.latex?\Omega\left(\frac{SA}{\epsilon^2}\ln&space;\frac{S}{\delta}\right)" title="\Omega\left(\frac{SA}{\epsilon^2}\ln \frac{S}{\delta}\right)" />.
A nice feature of upper bounds is that they can potentially be much smaller than the worst case if a good <i>admissible heuristic</i> is provided (a function supplied in advance that dominates the optimal value function).
____
Thomas Jaksch, Ronald Ortner, Peter Auer
[Near-optimal Regret Bounds for Reinforcement Learning](http://www.jmlr.org/papers/volume11/jaksch10a/jaksch10a.pdf)
JMLR 2010 \
A landmark in the regret analysis of MDPs (a [conference version](http://papers.nips.cc/paper/3401-near-optimal-regret-bounds-for-reinforcement-learning.pdf) appeared in NIPS 2008). The UCRL2 algorithm in non-episodic setting with diameter
<img src="https://latex.codecogs.com/gif.latex?D" title="D" />
achieves a regret bound of <img src="https://latex.codecogs.com/gif.latex?\tilde{O}(DS\sqrt{AT})" title="\tilde{O}(DS\sqrt{AT})" />.
Lower bound of <img src="https://latex.codecogs.com/gif.latex?\Omega(\sqrt{DSAT})" title="\Omega(\sqrt{DSAT})" /> is given.
If MDP changes <img src="https://latex.codecogs.com/gif.latex?L" title="L" /> times then regret bound of
<img src="https://latex.codecogs.com/gif.latex?\tilde{O}(L^{1/3}T^{2/3}DS\sqrt{A})" title="\tilde{O}(L^{1/3}T^{2/3}DS\sqrt{A})" />
is given.
____
Ian Osband, Daniel Russo, Benjamin Van Roy
[(More) Efficient Reinforcement Learning via
Posterior Sampling](https://papers.nips.cc/paper/5185-more-efficient-reinforcement-learning-via-posterior-sampling.pdf)
NIPS 2013 \
Posterior Sampling for Reinforcement Learning (PSRL) enjoys Bayesian regret bound of
<img src="https://latex.codecogs.com/gif.latex?\tilde{O}(HS\sqrt{AT})" title="\tilde{O}(HS\sqrt{AT})" />
in episodic setting.
____
Ian Osband, Benjamin Van Roy
[Model-based Reinforcement Learning and the Eluder Dimension](https://papers.nips.cc/paper/2014/file/1141938ba2c2b13f5505d7c424ebae5f-Paper.pdf)
NIPS 2014 \
'We consider the problem of learning to optimize an unknown Markov decision process (MDP). We show that, if the MDP can be parameterized within some known function class, we can obtain regret bounds that scale with the dimensionality, rather than cardinality, of the system. We characterize this dependence explicitly as 
<img src="https://latex.codecogs.com/svg.image?\tilde{O}(\sqrt{d_K&space;d_E&space;T})" title="\tilde{O}(\sqrt{d_K d_E T})" />
where 
<img src="https://latex.codecogs.com/svg.image?T" title="T" />
is time elapsed, 
<img src="https://latex.codecogs.com/svg.image?d_K" title="d_K" />
is the Kolmogorov dimension and 
<img src="https://latex.codecogs.com/svg.image?d_E" title="d_E" />
is the eluder dimension. These represent the first unified regret bounds for model-based reinforcement learning and provide state of the art guarantees in several important settings. Moreover, we present a simple and computationally efficient algorithm posterior sampling for reinforcement learning (PSRL) that satisfies these bounds.'
____
Kamyar Azizzadenesheli, Alessandro Lazaric, Anima Anandkumar
[Reinforcement Learning of POMDPs using Spectral Methods](http://proceedings.mlr.press/v49/azizzadenesheli16a.pdf) COLT 2016\
Proposes an algorithm for POMDPs based on spectral decomposition methods. Under assumptions of ergodicity and identifiability shows a regret bound of <img src="https://latex.codecogs.com/gif.latex?\widetilde{O}(DS^{3/2}\sqrt{AO&space;RT})" title="\widetilde{O}(DS^{3/2}\sqrt{AO RT})" /> with S states, O observations and R rewards.
____
Ian Osband, Benjamin Van Roy
[Why is Posterior Sampling Better than Optimism for Reinforcement Learning?](http://proceedings.mlr.press/v70/osband17a/osband17a.pdf)
ICML 2017 \
PSRL Bayesian regret bound in episodic setting improved to
<img src="https://latex.codecogs.com/gif.latex?\tilde{O}(H\sqrt{SAT})" title="\tilde{O}(H\sqrt{SAT})" />
____
Mohammad Gheshlaghi Azar, Ian Osband, Rémi Munos
[Minimax Regret Bounds for Reinforcement Learning](http://proceedings.mlr.press/v70/azar17a/azar17a.pdf)
ICML 2017 \
Optimistic Value Iteration (UCBVI) achieves regret bound of
<img src="https://latex.codecogs.com/gif.latex?\tilde{O}(\sqrt{HSAT}&plus;H^2S^2A&space;&plus;&space;H\sqrt{T})" title="\tilde{O}(\sqrt{HSAT}+H^2S^2A + H\sqrt{T})" />
in finite horizon problem.
Improvements obtained by (a) avoiding concentration argument for transition function (for state) and (b) using empirical Bernstein inequality (for horizon)
____
Yi Ouyang, Mukul Gagrani, Ashutosh Nayyar, Rahul Jain
[Learning Unknown Markov Decision Processes: A Thompson Sampling Approach](https://papers.nips.cc/paper/6732-learning-unknown-markov-decision-processes-a-thompson-sampling-approach.pdf)
NIPS 2017 \
Thompson Sampling is analyzed in the non-episodic case assuming that the prior only contains MDPs with span of optimal bias vector bounded by
<img src="https://latex.codecogs.com/gif.latex?B" title="B" />.
A regret bound of
<img src="https://latex.codecogs.com/gif.latex?\tilde{O}(BS\sqrt{AT})" title="\tilde{O}(BS\sqrt{AT})" />
is established
____
Christoph Dann, Tor Lattimore, Emma Brunskill
[Unifying PAC and Regret: Uniform PAC Bounds for Episodic Reinforcement Learning](http://papers.nips.cc/paper/7154-unifying-pac-and-regret-uniform-pac-bounds-for-episodic-reinforcement-learning.pdf)
NIPS 2017
____
Mohammad Sadegh Talebi, Odalric-Ambrym Maillard 
[Variance-Aware Regret Bounds for Undiscounted Reinforcement Learning in MDPs](http://proceedings.mlr.press/v83/talebi18a/talebi18a.pdf)
ALT 2018
____
Chi Jin, Zeyuan Allen-Zhu, Sebastien Bubeck, Michael I. Jordan
[Is Q-learning Provably Efficient?](https://papers.nips.cc/paper/7735-is-q-learning-provably-efficient.pdf)
NeurIPS 2018 \
Q-Learning with UCB-Hoeffding achieves <img src="https://latex.codecogs.com/gif.latex?\tilde{O}(\sqrt{H^4SAT})" title="\tilde{O}(\sqrt{H^4SAT})" /> regret.
Q-Learning with UCB-Bernstein achieves <img src="https://latex.codecogs.com/gif.latex?\tilde{O}(\sqrt{H^3SAT}&plus;\sqrt{H^9S^3A^3})" title="\tilde{O}(\sqrt{H^3SAT}+\sqrt{H^9S^3A^3})" /> regret.
Lower bound of <img src="https://latex.codecogs.com/gif.latex?\Omega(\sqrt{H^2SAT})" title="\Omega(\sqrt{H^2SAT})" /> is provided.
____
Andrea Zanette, Emma Brunskill
[Tighter Problem-Dependent Regret Bounds in Reinforcement Learning
without Domain Knowledge using Value Function Bounds](http://proceedings.mlr.press/v97/zanette19a/zanette19a.pdf)
ICML 2019
____
Christoph Dann, Lihong Li, Wei Wei, Emma Brunskill
[Policy Certificates: Towards Accountable Reinforcement Learning](http://proceedings.mlr.press/v97/dann19a/dann19a.pdf) ICML 2019\
Proposes a policy certificate notion which can unify PAC and regret bounds and proposes algorithms for tabular MDPs and MDPs with side-information. The tabular algorithm obtains minimax optimal PAC and regret bounds.
____
Max Simchowitz, Kevin G. Jamieson
[Non-Asymptotic Gap-Dependent Regret Bounds for
Tabular MDPs](https://papers.nips.cc/paper/8399-non-asymptotic-gap-dependent-regret-bounds-for-tabular-mdps.pdf)
NeurIPS 2019
____
Zihan Zhang, Xiangyang Ji
[Regret Minimization for Reinforcement Learning by
Evaluating the Optimal Bias Function](https://papers.nips.cc/paper/8549-regret-minimization-for-reinforcement-learning-by-evaluating-the-optimal-bias-function.pdf)
NeurIPS 2019 \
If bound
<img src="https://latex.codecogs.com/gif.latex?B" title="B" />
on span of optimal bias vector is known, then their Estimate the Bias Function (EBF) algorithm achieves
<img src="https://latex.codecogs.com/gif.latex?\tilde{O}(\sqrt{BSAT})" title="\tilde{O}(\sqrt{BSAT})" />
regret.
____
Daniel Russo
[Worst-Case Regret Bounds for Exploration via
Randomized Value Functions](https://papers.nips.cc/paper/9587-worst-case-regret-bounds-for-exploration-via-randomized-value-functions.pdf)
NeurIPS 2019 \
Worst-case regret analysis of Randomized Least Squares Value Iteration (RLSVI) yields a regret bound of
<img src="https://latex.codecogs.com/gif.latex?\tilde{O}(H^3S\sqrt{SAK})" title="\tilde{O}(H^3S\sqrt{SAK})" />
in the episodic setting where
<img src="https://latex.codecogs.com/gif.latex?K" title="K" />
is the number of episodes.
____
Yonathan Efroni, Nadav Merlis, Mohammad Ghavamzadeh, Shie Mannor
[Tight Regret Bounds for Model-Based Reinforcement
Learning with Greedy Policies](https://papers.nips.cc/paper/9389-tight-regret-bounds-for-model-based-reinforcement-learning-with-greedy-policies.pdf)
NeurIPS 2019 \
Exploring with greedy policies (act by 1-step planning) achieves tight minimax regret bound of
<img src="https://latex.codecogs.com/gif.latex?\tilde{O}(\sqrt{HSAT})" title="\tilde{O}(\sqrt{HSAT})" />
in episodic setting.
____
Aristide Tossou, Debabrota Basu, Christos Dimitrakakis
[Near-optimal Optimistic Reinforcement Learning using Empirical Bernstein Inequalities](https://arxiv.org/pdf/1905.12425v2.pdf)
arXiv 11 Dec 2019 \
Claims that their UCRL-V algorithm achieves optimal (up to logarithmic factors) regret bound of 
<img src="https://latex.codecogs.com/gif.latex?\tilde{O}(\sqrt{DSAT})" title="\tilde{O}(\sqrt{DSAT})" />
in the non-episodic setting 
____
Andrea Zanette, David Brandfonbrener, Emma Brunskill, Matteo Pirotta, Alessandro Lazaric
[Frequentist Regret Bounds for Randomized Least-Squares Value Iteration](http://proceedings.mlr.press/v108/zanette20a/zanette20a.pdf) AISTATS 2020\
Shows that a randomized version of LSVI also enjoys a high-probability regret bound of <img src="https://latex.codecogs.com/gif.latex?\widetilde{O}(d^2H^2\sqrt{T})" title="\widetilde{O}(d^2H^2\sqrt{T})" /> in low rank MDPs.
____
Chi Jin, Zhuoran Yang, Zhaoran Wang, Michael I. Jordan
[Provably Efficient Reinforcement Learning with Linear Function Approximation](http://proceedings.mlr.press/v125/jin20a/jin20a.pdf)
COLT 2020\
Analyses and optimistic modification of LSVI with a regret bound of <img src="https://latex.codecogs.com/gif.latex?\tilde{O}(\sqrt{d^3H^3T})" title="\tilde{O}(\sqrt{d^3H^3T})" /> in linear MDP with feature space of dimension
<img src="https://latex.codecogs.com/gif.latex?d" title="d" />.
____
Chen-Yu Wei, Mehdi Jafarnia-Jahromi, Haipeng Luo, Hiteshi Sharma, Rahul Jain
[Model-free Reinforcement Learning in Infinite-horizon Average-reward Markov Decision Processes](https://proceedings.icml.cc/static/paper_files/icml/2020/4595-Paper.pdf)
ICML 2020\
Proposes two algorithms: Optimistic Q-learning for weakly communicating MDPs with regret <img src="https://latex.codecogs.com/gif.latex?\tilde{O}(\text{sp}(v^*)T^{2/3}(SA)^{1/3})" title="\tilde{O}(B T^{2/3}(SA)^{1/3})" />, where $B$ is a bound on the span of the optimal bias function, and the optimistic OMD algorithm for ergodic MDPs with regret <img src="https://latex.codecogs.com/gif.latex?\tilde{O}(\sqrt{t_{\text{mix}}\rho&space;AT})" title="\tilde{O}(\sqrt{t_{\text{mix}}\rho AT})" /> where there is dependence on the mixing time of the MDP and the worst-case distribution-mismatch coefficient.
____
Andrea Zanette, Alessandro Lazaric, Mykel Kochenderfer, Emma Brunskill
[Learning Near Optimal Policies with Low Inherent Bellman Error](https://proceedings.icml.cc/static/paper_files/icml/2020/6299-Paper.pdf) ICML 2020\
Studies finite horizon MDP with linear function approximation under mis-specification. With <img src="https://latex.codecogs.com/gif.latex?\epsilon" title="\epsilon" /> indicating the inherent Bellman error of linear function class, the regret of the algorithm is <img src="https://latex.codecogs.com/gif.latex?\tilde{O}(d\sqrt{H^3K}&plus;H^2\sqrt{d}\epsilon&space;K)" title="\tilde{O}(d\sqrt{H^3K}+H^2\sqrt{d}\epsilon K)" />.
____
Alex Ayoub, Zeyu Jia, Csaba Szepesvari, Mengdi Wang, Lin Yang
[Model-Based Reinforcement Learning with Value-Targeted Regression](http://proceedings.mlr.press/v119/ayoub20a/ayoub20a.pdf) ICML 2020\
'This paper studies model-based reinforcement learning (RL) for regret minimization. We focus on finite-horizon episodic RL where the transition model
<img src="https://latex.codecogs.com/svg.image?P" title="P" />
belongs to a known family of models
<img src="https://latex.codecogs.com/svg.image?\mathcal{P}" title="\mathcal{P}" />
, a special case of which is when models in
<img src="https://latex.codecogs.com/svg.image?\mathcal{P}" title="\mathcal{P}" />
take the form of linear mixtures:
<img src="https://latex.codecogs.com/svg.image?P_\theta&space;=&space;\sum_{i=1}^d&space;\theta_i&space;P_i" title="P_\theta = \sum_{i=1}^d \theta_i P_i" />
. We propose a model based RL algorithm that is based on the optimism principle: In each episode, the set of models that are ‘consistent’ with the data collected is constructed. The criterion of consistency is based on the total squared error that the model incurs on the task of predicting state values as determined by the last value estimate along the transitions. The next value function is then chosen by solving the optimistic planning problem with the constructed set of models. We derive a bound on the regret, which, in the special case of linear mixtures, takes the form
<img src="https://latex.codecogs.com/svg.image?\tilde{O}(d\sqrt{H^3&space;T})" title="\tilde{O}(d\sqrt{H^3 T})" />
where
<img src="https://latex.codecogs.com/svg.image?H" title="H" />
,
<img src="https://latex.codecogs.com/svg.image?T" title="T" />
and
<img src="https://latex.codecogs.com/svg.image?d" title="d" />
are the horizon, the total number of steps and the dimension of
<img src="https://latex.codecogs.com/svg.image?\theta" title="\theta" />
respectively. In particular, this regret bound is independent of the total number of states or actions, and is close to a lower bound
<img src="https://latex.codecogs.com/svg.image?\Omega(\sqrt{HdT})" title="\Omega(\sqrt{HdT})" />
. For a general model family
<img src="https://latex.codecogs.com/svg.image?\mathcal{P}" title="\mathcal{P}" />
, the regret bound is derived based on the Eluder dimension.'
____
Ronald Ortner
[Regret Bounds for Reinforcement Learning via Markov Chain Concentration](https://doi.org/10.1613/jair.1.11316)
JAIR 2020
____
Ruosong Wang, Russ R. Salakhutdinov, Lin Yang
[Reinforcement Learning with General Value Function Approximation: Provably Efficient Approach via Bounded Eluder Dimension](https://proceedings.neurips.cc/paper/2020/file/440924c5948e05070663f88e69e8242b-Paper.pdf)
NeurIPS 2020 \
'Value function approximation has demonstrated phenomenal empirical success in reinforcement learning (RL). Nevertheless, despite a handful of recent progress on developing theory for RL with linear function approximation, the understanding of general function approximation schemes largely remains missing. In this paper, we establish the first provably efficient RL algorithm with general value function approximation. We show that if the value functions admit an approximation with a function class 
<img src="https://latex.codecogs.com/svg.image?\mathcal{F}" title="\mathcal{F}" />
, our algorithm achieves a regret bound of 
<img src="https://latex.codecogs.com/svg.image?\tilde{O}(poly(d&space;H)\sqrt{T})" title="\tilde{O}(poly(d H)\sqrt{T})" />
where 
<img src="https://latex.codecogs.com/svg.image?d" title="d" />
is a complexity measure of 
<img src="https://latex.codecogs.com/svg.image?\mathcal{F}" title="\mathcal{F}" />
that depends on the eluder dimension and log-covering numbers, 
<img src="https://latex.codecogs.com/svg.image?H" title="H" />
is the planning horizon, and 
<img src="https://latex.codecogs.com/svg.image?T" title="T" />
is the number interactions with the environment. Our theory generalizes the linear MDP assumption to general function classes. Moreover, our algorithm is model-free and provides a framework to justify the effectiveness of algorithms used in practice.'
____
Yonathan Efroni, Shie Mannor, Matteo Pirotta
[Exploration-Exploitation in Constrained MDPs](https://arxiv.org/pdf/2003.02189.pdf)
arXiv 4 Mar 2020 \
Regret analysis for constrained MDPs
____
Shipra Agrawal, Randy Jia
[Posterior sampling for reinforcement learning: worst-case regret bounds](https://arxiv.org/pdf/1705.07041v3.pdf)
arXiv 30 Mar 2020 \
Worst-case analysis of a posterior sampling based (but not posterior sampling itself) algorithm yields 
<img src="https://latex.codecogs.com/gif.latex?\tilde{O}(DS\sqrt{AT})" title="\tilde{O}(DS\sqrt{AT})" />
regret in non-episodic setting
____
Hippolyte Bourel, Odalric-Ambrym Maillard, Mohammad Sadegh Talebi
[Tightening Exploration in Upper Confidence
Reinforcement Learning](https://arxiv.org/pdf/2004.09656.pdf)
arXiv 8 Jun 2020
____
Aldo Pacchiano, Philip Ball, Jack Parker-Holder, Krzysztof Choromanski, Stephen Roberts
[On Optimism in Model-Based Reinforcement Learning](https://arxiv.org/pdf/2006.11911.pdf)
arXiv 21 Jun 2020 \
Gaussian Noise Augmented RL algorithm achieves regret bound of
<img src="https://latex.codecogs.com/gif.latex?\tilde{O}(SH\sqrt{SAT})" title="\tilde{O}(SH\sqrt{SAT})" />
in episodic setting
____
Gergely Neu, Ciara Pike-Burke
[A Unifying View of Optimism in Episodic Reinforcement Learning](https://arxiv.org/pdf/2007.01891.pdf)
arXiv 3 Jul 2020
____
Qi Cai, Zhuoran Yang, Chi Jin, Zhaoran Wang
[Provably Efficient Exploration in Policy Optimization](https://arxiv.org/pdf/1912.05830.pdf)
arXiv 6 Jul 2020 \
Studies an Optimistic verion of Proximal Policy Optimization (OPPO) is episodic linear MDPs. When specialized
to tabular setting the regret bound is
<img src="https://latex.codecogs.com/gif.latex?\tilde{O}(H^{3/2}S^2A\sqrt{T})" title="\tilde{O}(H^{3/2}S^2A\sqrt{T})" />
____
Melrose Roderick, Vaishnavh Nagarajan, J. Zico Kolter
[Provably Safe PAC-MDP Exploration Using Analogies](https://arxiv.org/pdf/2007.03574.pdf)
arXiv 7 Jul 2020
____
Ronan Fruit, Matteo Pirotta, Alessandro Lazaric
[Improved Analysis of UCRL2 with Empirical Bernstein Inequality](https://arxiv.org/pdf/2007.05456.pdf)
arXiv 10 Jul 2020
____
Chen-Yu Wei, Mehdi Jafarnia-Jahromi, Haipeng Luo, Rahul Jain
[Learning Infinite-horizon Average-reward MDPs with Linear Function Approximation](https://arxiv.org/pdf/2007.11849.pdf)
arXiv 23 Jul 2020
____
Pierre Ménard, Omar Darwiche Domingues, Anders Jonsson, Emilie Kaufmann, Edouard Leurent, Michal Valko
[Fast active learning for pure exploration in reinforcement learning](https://arxiv.org/pdf/2007.13442.pdf)
arXiv 27 Jul 2020
____
Aria HasanzadeZonuzy, Dileep Kalathil, Srinivas Shakkottai
[Learning with Safety Constraints: Sample Complexity of Reinforcement Learning for Constrained MDPs](https://arxiv.org/pdf/2008.00311.pdf)
arXiv 1 Aug 2020 \
PAC sample complexity analysis for constrained MDPs
____
Andrea Zanette, Alessandro Lazaric, Mykel J. Kochenderfer, Emma Brunskill
[Provably Efficient Reward-Agnostic Navigation with Linear Value Iteration](https://arxiv.org/pdf/2008.07737.pdf)
arXiv 18 Aug 2020 \
'we show how under a more standard notion of low inherent Bellman error, typically employed in leastsquare value iteration-style algorithms, we can provide strong PAC guarantees on learning a near optimal value function provided that the linear space is sufficiently “explorable”'
____
Zihan Zhang, Xiangyang Ji, Simon S. Du
[Is Reinforcement Learning More Difficult Than Bandits? A Near-optimal Algorithm Escaping the Curse of Horizon](https://arxiv.org/pdf/2009.13503.pdf)
arXiv 28 Sep 2020 \
'Episodic reinforcement learning and contextual bandits are two widely studied sequential
decision-making problems. Episodic reinforcement learning generalizes contextual bandits and
is often perceived to be more difficult due to long planning horizon and unknown state-dependent
transitions. The current paper shows that the long planning horizon and the unknown statedependent transitions (at most) pose little additional difficulty on sample complexity.'
____
Dylan J. Foster, Alexander Rakhlin, David Simchi-Levi, Yunzong Xu
[Instance-Dependent Complexity of Contextual Bandits and Reinforcement Learning: A Disagreement-Based Perspective](https://arxiv.org/pdf/2010.03104.pdf)
arXiv 7 Oct 2020\
'In the classical multi-armed bandit problem, instance-dependent algorithms attain improved performance on "easy" problems with a gap between the best and second-best arm. Are similar guarantees possible for contextual bandits? While positive results are known for certain special cases, there is no general theory characterizing when and how instance-dependent regret bounds for contextual bandits can be achieved for rich, general classes of policies. We introduce a family of complexity measures that are both sufficient and necessary to obtain instance-dependent regret bounds. We then introduce new oracle-efficient algorithms which adapt to the gap whenever possible, while also attaining the minimax rate in the worst case. Finally, we provide structural results that tie together a number of complexity measures previously proposed throughout contextual bandits, reinforcement learning, and active learning and elucidate their role in determining the optimal instance-dependent regret. In a large-scale empirical evaluation, we find that our approach often gives superior results for challenging exploration problems.
Turning our focus to reinforcement learning with function approximation, we develop new oracle-efficient algorithms for reinforcement learning with rich observations that obtain optimal gap-dependent sample complexity.'
____
Priyank Agrawal, Jinglin Chen, Nan Jiang
[Improved Worst-Case Regret Bounds for Randomized Least-Squares Value Iteration](https://arxiv.org/pdf/2010.12163.pdf)
arXiv 23 Oct 2020 \
'This paper studies regret minimization with randomized value functions in reinforcement learning. In tabular finite-horizon Markov Decision Processes, we introduce a clipping variant of one classical Thompson Sampling (TS)-like algorithm, randomized least-squares value iteration (RLSVI). We analyze the algorithm using a novel intertwined regret decomposition. Our <img src="https://latex.codecogs.com/gif.latex?\tilde{O}(H^2&space;S&space;\sqrt{AT})" title="\tilde{O}(H^2 S \sqrt{AT})" /> high-probability worst-case regret bound improves the previous sharpest worst-case regret bounds for RLSVI and matches the existing state-of-the-art worst-case TS-based regret bounds.'
____
Haque Ishfaq, Qiwen Cui, Viet Nguyen, Alex Ayoub, Zhuoran Yang, Zhaoran Wang, Doina Precup, Lin F. Yang
[Randomized Exploration for Reinforcement Learning with General Value Function Approximation](https://arxiv.org/pdf/2106.07841.pdf)
arXiv 15 Jun 2021 \
'We propose a model-free reinforcement learning algorithm inspired by the popular randomized least squares value iteration (RLSVI) algorithm as well as the optimism principle. Unlike existing upper-confidence-bound (UCB) based approaches, which are often computationally intractable, our algorithm drives exploration by simply perturbing the training data with judiciously chosen i.i.d. scalar noises. To attain optimistic value function estimation without resorting to a UCB-style bonus, we introduce an optimistic reward sampling procedure. When the value functions can be represented by a function class <img src="https://latex.codecogs.com/svg.image?\mathcal{F}" title="\mathcal{F}" />, our algorithm achieves a worst-case regret bound of <img src="https://latex.codecogs.com/svg.image?\tilde{O}(poly(d_E&space;H\sqrt{T}))" title="\tilde{O}(poly(d_E H\sqrt{T}))" /> where <img src="https://latex.codecogs.com/svg.image?T" title="T" /> is the time elapsed, <img src="https://latex.codecogs.com/svg.image?H" title="H" /> is the planning horizon and <img src="https://latex.codecogs.com/svg.image?d_E" title="d_E" /> is the eluder dimension of <img src="https://latex.codecogs.com/svg.image?\mathcal{F}" title="\mathcal{F}" />. In the linear setting, our algorithm reduces to LSVI-PHE, a variant of RLSVI, that enjoys an <img src="https://latex.codecogs.com/svg.image?\tilde{O}(\sqrt{d^3&space;H^3&space;T})" title="\tilde{O}(\sqrt{d^3 H^3 T})" /> regret. We complement the theory with an empirical evaluation across known difficult exploration tasks.'
____
Yining Wang, Ruosong Wang, Simon Shaolei Du, Akshay Krishnamurthy
[Optimism in Reinforcement Learning with Generalized Linear Function Approximation](https://openreview.net/pdf?id=CBmJwzneppz)
ICLR 2021 \
'We design a new provably efficient algorithm for episodic reinforcement learning with generalized linear function approximation. We analyze the algorithm under a new expressivity assumption that we call "optimistic closure," which is strictly weaker than assumptions from prior analyses for the linear setting. With optimistic closure, we prove that our algorithm enjoys a regret bound of
<img src="https://latex.codecogs.com/svg.image?\tilde{O}(H\sqrt{d^3&space;T})" title="\tilde{O}(H\sqrt{d^3 T})" />
where
<img src="https://latex.codecogs.com/svg.image?H" title="H" />
is the horizon,
<img src="https://latex.codecogs.com/svg.image?d" title="d" />
is the dimensionality of the state-action features and
<img src="https://latex.codecogs.com/svg.image?T" title="T" />
is the number of episodes. This is the first statistically and computationally efficient algorithm for reinforcement learning with generalized linear functions.'

## POMDPs

Zhaohan Daniel Guo Shayan Doroudi Emma Brunskill
[A PAC RL Algorithm for Episodic POMDPs](http://proceedings.mlr.press/v51/guo16b.pdf)
AISTATS 2016
____
Kamyar Azizzadenesheli, Alessandro Lazaric, Animashree Anandkumar
[Reinforcement Learning of POMDPs using Spectral Methods](http://proceedings.mlr.press/v49/azizzadenesheli16a.pdf)
COLT 2016
____
Chi Jin, Sham Kakade, Akshay Krishnamurthy, Qinghua Liu
[Sample-Efficient Reinforcement Learning of Undercomplete POMDPs](https://arxiv.org/pdf/2006.12484.pdf)
arXiv 22 Jun 2020 \
'This work shows that these hardness barriers do not
preclude efficient reinforcement learning for rich and interesting subclasses of POMDPs. In particular, we
present a sample-efficient algorithm, OOM-UCB, for episodic finite undercomplete POMDPs, where the
number of observations is larger than the number of latent states and where exploration is essential for learning, thus distinguishing our results from prior works. OOM-UCB achieves an optimal sample complexity of O(1/ε<sup>2</sup>) for finding an ε-optimal policy, along with being polynomial in all other relevant quantities.'
____
Yi Xiong, Ningyuan Chen, Xuefeng Gao, Xiang Zhou
[Sublinear Regret for Learning POMDPs]()
arXiv 14 Jul 2021 \
'We study the model-based undiscounted reinforcement learning for partially observable Markov decision processes (POMDPs). The oracle we consider is the optimal policy of the POMDP with a known environment in terms of the average reward over an infinite horizon. We propose a learning algorithm for this problem, building on spectral method-of-moments estimations for hidden Markov models, the belief error control in POMDPs and upper-confidence-bound methods for online learning. We establish a regret bound of
<img src="https://latex.codecogs.com/svg.image?O(T^{2/3}\sqrt{\log&space;T})" title="O(T^{2/3}\sqrt{\log T})" />
for the proposed learning algorithm where T is the learning horizon. This is, to the best of our knowledge, the first algorithm achieving sublinear regret with respect to our oracle for learning general POMDPs.'

## Linear Quadratic Systems

Claude-Nicolas Fiechter
[PAC adaptive control of linear systems](https://doi.org/10.1145/267460.267481)
COLT 1997
____
Yasin Abbasi-Yadkori, Csaba Szepesvari
[Regret Bounds for the Adaptive Control of Linear Quadratic Systems](http://proceedings.mlr.press/v19/abbasi-yadkori11a/abbasi-yadkori11a.pdf)
COLT 2011
____
Marc Abeille, Alessandro Lazaric
[Improved Regret Bounds for Thompson Sampling in Linear Quadratic Control Problems](http://proceedings.mlr.press/v80/abeille18a/abeille18a.pdf)
ICML 2018
____
Dhruv Malik, Ashwin Pananjady, Kush Bhatia, Koulik Khamaru, Peter L. Bartlett, Martin J. Wainwright
[Derivative-Free Methods for Policy Optimization: Guarantees for
Linear Quadratic Systems](http://proceedings.mlr.press/v89/malik19a/malik19a.pdf)
AISTATS 2019
____
Alon Cohen, Tomer Koren, Yishay Mansour
[Learning Linear-Quadratic Regulators Efficiently with only √T Regret](http://proceedings.mlr.press/v97/cohen19b/cohen19b.pdf)
ICML 2019
____
Sarah Dean, Horia Mania, Nikolai Matni, Benjamin Recht, Stephen Tu
[On the Sample Complexity of the Linear Quadratic Regulator](https://doi.org/10.1007/s10208-019-09426-y)
Found Comput Math 2020
____
Sahin Lale, Kamyar Azizzadenesheli, Babak Hassibi, Anima Anandkumar
[Adaptive Control and Regret Minimization in Linear Quadratic Gaussian (LQG) Setting](https://arxiv.org/pdf/2003.05999.pdf)
arXiv 24 Jun 2020
____
Yassir Jedra, Alexandre Proutiere
[Minimal Expected Regret in Linear Quadratic Control](https://arxiv.org/pdf/2109.14429.pdf)
arXiv 29 Sep 2021
