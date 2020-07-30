# Bibliography on Learning in MDPs

Michael Kearns & Satinder Singh
[Near-Optimal Reinforcement Learning in Polynomial Time](https://doi.org/10.1023/A:1017984413808)
MLJ 2002

Ronen I. Brafman, Moshe Tennenholtz
[R-MAX - A General Polynomial Time Algorithm for Near-Optimal Reinforcement Learning](http://www.jmlr.org/papers/volume3/brafman02a/brafman02a.pdf)
JMLR 2002

Sham Kakade
[On the Sample Complexity of
Reinforcement Learning](https://homes.cs.washington.edu/~sham/papers/thesis/sham_thesis.pdf)
PhD Thesis 2003

Peter Auer, Ronald Ortner
[Logarithmic Online Regret Bounds for Undiscounted Reinforcement Learning](https://papers.nips.cc/paper/3052-logarithmic-online-regret-bounds-for-undiscounted-reinforcement-learning.pdf)
NIPS 2006

Thomas Jaksch, Ronald Ortner, Peter Auer
[Near-optimal Regret Bounds for Reinforcement Learning](http://www.jmlr.org/papers/volume11/jaksch10a/jaksch10a.pdf)
JMLR 2010 \
UCRL2 algorithm with regret bound <img src="https://latex.codecogs.com/gif.latex?\tilde{O}(DS\sqrt{AT})" title="\tilde{O}(DS\sqrt{AT})" />.
Lower bound of <img src="https://latex.codecogs.com/gif.latex?\Omega(\sqrt{DSAT})" title="\Omega(\sqrt{DSAT})" /> is given.
If MDP changes <img src="https://latex.codecogs.com/gif.latex?L" title="L" /> times then regret bound of
<img src="https://latex.codecogs.com/gif.latex?\tilde{O}(L^{1/3}T^{2/3}DS\sqrt{A})" title="\tilde{O}(L^{1/3}T^{2/3}DS\sqrt{A})" />
is given.

Ian Osband, Daniel Russo, Benjamin Van Roy
[(More) Efficient Reinforcement Learning via
Posterior Sampling](https://papers.nips.cc/paper/5185-more-efficient-reinforcement-learning-via-posterior-sampling.pdf)
NIPS 2013 \
Posterior Sampling for Reinforcement Learning (PSRL) enjoys Bayesian regret bound of
<img src="https://latex.codecogs.com/gif.latex?\tilde{O}(HS\sqrt{AT})" title="\tilde{O}(HS\sqrt{AT})" />
in episodic setting.

Ian Osband, Benjamin Van Roy
[Why is Posterior Sampling Better than Optimism for Reinforcement Learning?](http://proceedings.mlr.press/v70/osband17a/osband17a.pdf)
ICML 2017 \
PSRL Bayesian regret bound in episodic setting improved to
<img src="https://latex.codecogs.com/gif.latex?\tilde{O}(H\sqrt{SAT})" title="\tilde{O}(H\sqrt{SAT})" />

Mohammad Gheshlaghi Azar, Ian Osband, Rémi Munos
[Minimax Regret Bounds for Reinforcement Learning](http://proceedings.mlr.press/v70/azar17a/azar17a.pdf)
ICML 2017 \
Optimistic Value Iteration (UCBVI) achieves regret bound of
<img src="https://latex.codecogs.com/gif.latex?\tilde{O}(HS\sqrt{AT}&plus;H^2S^2A&plus;H\sqrt{T})" title="\tilde{O}(HS\sqrt{AT}+H^2S^2A+H\sqrt{T})" /> in finite horizon problem.
Improvements obtained by (a) avoiding concentration argument for transition function (for state) and (b) using empirical Bernstein inequality (for horizon)

Chi Jin, Zeyuan Allen-Zhu, Sebastien Bubeck, Michael I. Jordan
[Is Q-learning Provably Efficient?](https://papers.nips.cc/paper/7735-is-q-learning-provably-efficient.pdf)
NeurIPS 2018 \
Q-Learning with UCB-Hoeffding achieves <img src="https://latex.codecogs.com/gif.latex?\tilde{O}(\sqrt{H^4SAT})" title="\tilde{O}(\sqrt{H^4SAT})" /> regret.
Q-Learning with UCB-Bernstein achieves <img src="https://latex.codecogs.com/gif.latex?\tilde{O}(\sqrt{H^3SAT}&plus;\sqrt{H^9S^3A^3})" title="\tilde{O}(\sqrt{H^3SAT}+\sqrt{H^9S^3A^3})" /> regret.
Lower bound of <img src="https://latex.codecogs.com/gif.latex?\Omega(\sqrt{H^2SAT})" title="\Omega(\sqrt{H^2SAT})" /> is provided.

Andrea Zanette, Emma Brunskill
[Tighter Problem-Dependent Regret Bounds in Reinforcement Learning
without Domain Knowledge using Value Function Bounds](http://proceedings.mlr.press/v97/zanette19a/zanette19a.pdf)
ICML 2019

Max Simchowitz, Kevin G. Jamieson
[Non-Asymptotic Gap-Dependent Regret Bounds for
Tabular MDPs](https://papers.nips.cc/paper/8399-non-asymptotic-gap-dependent-regret-bounds-for-tabular-mdps.pdf)
NeurIPS 2019

Shipra Agrawal, Randy Jia
[Posterior sampling for reinforcement learning: worst-case regret bounds](https://arxiv.org/pdf/1705.07041v3.pdf)
arXiv 30 Mar 2020
