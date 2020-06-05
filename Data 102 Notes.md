# Data 102 Notes

## Lecture 1
- Reality 0 = TN + FP
- Reality 1 = FN + TP
- Problem: we don't know reality. We need to move towards a stastical framework where we consider a set of related decisions generated through a decision-making algorithm
    - Series of hypothesis-testing problems, decide whether we accept or reject the null
    - Classification into one of multiple classes
- Sensitivity = Recall = Power = $\dfrac{TP}{FN + TP} \rightarrow$ what fraction of true cases are actually being detected, how sensitive is the test to the actual outcome?
    - Given the alternative, what fraction of times do I reject?
    - Approximates P(Decision = 1 | Reality = 1)
- Specificity = Selectivity = $\dfrac{TN}{TN + FP} \rightarrow$ what fraction of false cases are actually being classified as such
    - Approximates P(Decision = 0 | Reality = 0)
- They are both independent on prevalence: the probabilities of the two states of reality in the population
- Want: high sensitivity and specificity
- False Omission Rate = $\dfrac{FN}{TN + FN} \rightarrow$ what fraction of predicted negatives are actually positive
- False Discovery Rate = $\dfrac{FP}{TP + FP} \rightarrow$ what fraction of predicted positives are actually positive

## Lecture 2

- Tradeoff between FN and FP, you want to decrease both but decreasing one naturally increases the other
- Frequentism: we don't just have one datset, but rather we repeatedly draw datasets independently from the population
    - The randomness comes from this sampling process, the other draws that could have happened from the population
    - Hypothesis Testing: we want to specify, via a probability distribution, what data one expects to see under the null. Then, we collect the data and assess how well it fits that null distriution. If it doesn't fit it will, we reject the null
- Bayesian Hypothesis Testing: specify, via a probability distribution, what data one expects to see under null and alternative hypotheses (columns of the table)
    - Places a prior probability on the null and the alternative (same thing as prevalence)
    - Then use this prior and the data to form a conditional probability of the hypothesis given the data 
- Bayes Theorem: $P(H = 0 | D = 1) = \dfrac{P(D = 1|H = 0) \cdot P(H = 0)}{P(D = 1)}$
- Bayes vs. Frequentist Inference
    - Bayesian: uses probabilities for both hypotheses and data, depends on the prior and likelihood of observed data, requires knowledge of a subjective prior
        - Inferences should be made conditional on the **actual observed data** not on possible data that could have been observed
        - Problem: prior is subjective, leading to different posteriors and thus conclusions
    - Frequentist: never uses or gives the probability of a hypothesis (no prior or posterior), depends on the conditional likelihood for both observed and unobserved data
        - Inferential procedures should give good answers in repeated use (on average) for all kinds of possible datasets
- Decision-Theoretic Framework
    - Define a family of probability models for the data $X$, indexed by parameter $\theta$, consider this as the truth
    - $\delta(X)$ is a decision obtained from a procedure or algorithm that operates on the data
    - $l(\theta, \delta(X))$ is the loss function, how unhappy we are about the decision relative to the truth
    - The goal is to use the loss function to compare procedures/models, but both of its arguments are unknown: $\theta$ is unknown and $\delta(X)$ is random as data is random
        - Frequentist: treat $\theta$ as fixed and data as random, reducing loss to a function of $R(\theta) = E_\theta [l(\theta, \delta(X))]$
        - Bayesian: we're going to know the X eventually so condition on it, treat $\theta$ as unknown: $p(X) = E[l(\theta, \delta(X)) | X]$, the posterior risk

## Lecture 3
- Type 1 error rate: probability of rejecting the null hypothesis given it is true = $P(FP) = P(\delta(X) = 1 | \theta = 0)$
- Type 2 error rate: probability of accepting a null hypothesis given it is false $P(FN) = P(\delta(X) = 0 | \theta = 1)$
- Bias and variance are frequentist terms: among all other datasets, how well does your model fit the data or how much does the model vary when given different data?
- Law of Iterated Expectations: $E[E[Y|X]] = E[Y]$: the average of an average is an average. You average Y values for all possible values of X.
- A priori control: if my assumptions about the null and alternative distributions are correct, then I can guarantee that the Type 1 and 2 errors will be small over multiple draws of data (more than one hypothesis test)
- Bonferroni Method:
    - Conduct m tests, V: number of Type 1 errors
    - Rejection threshold: $\dfrac{\alpha}{m}$ instead of $\alpha$, i.e. $\dfrac{\text{p-value}}{m}$
    - $P(V \geq 1) \leq \alpha$: the probability of making at least 1 Type 1 error is at most $\alpha$. Thus, you can guarantee that over m tests, you are maintaining an overall confidence level $\alpha$.
    - Problem: Overly stringent as it increases threshold of significance, leading to a lower maximum Type 1 error rate. Thus, $\text{t-stat} \leq \dfrac{\alpha}{m}$ is significant, which will be true for fewer and fewer observations as more tests occur. This prevents us from making many discoveries and increases false negative rate
- Note: False Discovery Proportion (FDP) = $\dfrac{V}{\text{# of all rejected hypotheses (discoveries)}}$ 
- False Discovery Rate (FDR) = $E[FDP]$, a random variable
- We want to control the FDR such that $E[FDP] \leq \alpha$
- Controlling the False Discovery Rate (Benjamini and Hochberg):
    - Given m tests, obtain p-values $P_i$, and sort them from smallest to largest, denoting the sorted p-values (order statistics) as $P_{(k)}$
    - Start rejecting the null hypotheses, only making "discoveries" for small p-values, deciding when to stop as and when p-values become too large. This gives you the p-value threshold as it occurs when you stop rejecting null hypotheses
    - Find the largest k such that: $P_{(k)} \leq \dfrac{k}{m}\alpha$
    - Reject all the hypotheses 1, ..., k, these are your discoveries

## Lecture 4
- Define the p-value as $P = F(T) = \mathbb{P}(T > t)$ where $\mathbb{P}$ is the probability distribution under the null hypothesis
    - Think of this as the tail cdf beyond some value $t$
- The p-value has a uniform distribution under the null hypothesis: $\mathbb{P}(P < p) = \mathbb{P}(F(T) < p) = \mathbb{P}(T > F^{-1}(p)) = F(F^{-1}(p)) = p$
    - The second to third equality is due to $F(T)$ being monotonically decreasing
    - This is a uniform distribution as the tail cdf is equal to the value from which the cdf starts
- Our previous discussion assumed the algorithm is run only after all data has been collected (offline control)
    - E.g. For Benjamini and Hochberg, you need all p-values before you start sorting
- Can you create a method that allows for data that streams in? Can you provide FDR control at any moment in time (online control)?
- Can't use Bonferroni as you can make decisions based on some $\alpha = \dfrac{0.05}{n}$, which would guarantee you an error rate of 0.05. However, at the (n+1)st test, you can't reset $\alpha = \dfrac{0.05}{n+1}$ as then you would have to re-run all of the previous tests. You've used up your "$\alpha$ wealth"
- Can you have an $\alpha$ that varies?
- Recall that FDP = $\dfrac{V}{\text{# of all rejected hypotheses (discoveries)}}$ 
    - You can make this ratio small by decreasing $V$ or increasing the # of discoveries
    - Numerator has the false positive rate in it, so we're back to making the same problem of controlling sums of $\alpha_i$ values
    - Denominator can be made large by making many discoveries
- Treat $\alpha$ like money: you earn a little when you make a discovery, giving you some breathing room to spend it on false discoveries later. You lose $\alpha$ when you do a hypothesis test and you don't make a discovery
- Online FDR Algorithms: assign $\alpha_t$ such that $\widehat{FDP(t)} = \dfrac{\sum_{i=1}^t \alpha_i}{\sum_{i=1}^t 1\{P_i \leq \alpha_i\}} \leq \alpha$
- The LORD Procedure:
    - For FDR level $\alpha$, initial wealth $W_0$ and non-increasing sequence of $\gamma$ that sum to 1 (e.g. 0.5, 0.25, ...)
    - Set $\alpha_1 = \gamma_1 W_0$
    - For t = 1, 2, ...:
        - If p-value $P_t \leq \alpha_t$, reject $P_t$
        - $\alpha_{t + 1} = \gamma_{t + 1} W_0 + \gamma_{t + 1 - \tau_1}(\alpha - W_0)1\{\tau_1 \leq t \} + \alpha \sum_{j = 1}^{\infty} \gamma_{t+1-\tau_j}1\{\tau_j \leq t \}$
        - Note: $\tau_j = \min \{k : \sum_{l=1}^k 1\{P_l \leq \alpha_l\} = j \}$, which is the earliest time at which there are $j$ rejections up to time $k$ (e.g. $\tau_j = 372$ is the first time at which there were $j$ rejections)

## Lecture 5
- Simpler version of LORD
    - Only consider the most recent rejection: at some time $t$, look back at the latest rejection 
    - Looking at the equation for the FDP: $\widehat{FDP(t)} = \dfrac{\sum_{i=1}^t \alpha_i}{\sum_{i=1}^t 1\{P_i \leq \alpha_i\}} \leq \alpha$
        - The denominator is observable as it is just the number of rejections until time $t$
        - The numerator is an upper bound of the Type 1 error probabilities, which needs to be estimated
    - Break up the numerator into episodes bookmarked by a rejection
    - In each episode, the sum of $\alpha$ is upper-bounded by $\alpha \sum_{i = 1}^{t'} \gamma_{i + 1 - \tau}$ where $t'$ is the episode length and $\tau$ is the time of the most recent rejection
    - This sum is upper bounded as we are taking portions of a strictly decreasing sequence (the $\gamma$) that sums to 1. These portions do not extend to infinity so we are guaranteeing the sum is less than $\alpha$ for each episode
    - Thus, the numerator is at most $(\alpha \cdot \text{# of episodes})$ and the denominator is $(\sum_{i=1}^t 1\{P_i \leq \alpha_i\} = \text{# of episodes})$, thus $\widehat{FDP(t)} \leq \alpha$
- Estimating the null distribution
    - What if we don't have a well-specified null distribution?
    - In the single hypothesis test paradigm, we are stuck
    - In the multiple hypothesis test paradigm, if all of the null hypotheses are the same, we have many draws available
        - We can thus assume that most of the data points corresponding to large p-values are from the null
        - This lets us estimate the null through some sort of density estimation
- Permutation Testing
    - If two sets of draws follow the null hypothesis, then they come from the same distribution
    - Exchangeability: An infinite collection of random variables is exchangeable if for any sample size $n$ and permutation $\pi$, the distribution of $X_{\pi_1}, ... X_{\pi_n}$ is the same as $X_1, ..., X_n$, the order doesn't matter but the elements are the same
    - If data is exchangeable, then it follows the null hypothesis
    - Through permutation, you can get multiple samples from the null
    - Let $\tilde X$ denote the unordered set of variables under an exchangeability assumption for the null, the set of all possible permutations of the data
    - Given a statistic $T$ that indicates the size of the rejection region, consider the conditional expectation $E[T | \tilde X]$
    - The distribution obtained by conditioning on $\tilde X$ is uniform, as each permutation of $X$ has an equal probability of occuring
    - This means that $E[T | \tilde X] \leq \alpha$
    - Thus: $E[T] = E[E[T | \tilde X]] \leq E[\alpha] = \alpha$

## Lecture 6
- Review of linear regression, CEF, MLE

## Lecture 7
- If data is linearly separable, logistic regression sends the weights to $\infty$, so regularization is needed (generally: apply regularization)
    - Minimum occurs at 0 where weights become $-\infty$
    - Regularization creates a global minimum very close to 0 but with non-infinite weights

## Lecture 8
- Frequentist: what is the distribution of this fixed parameter over random draws of the data?
    - There exists some robability model $P(Y; \theta)$ where $Y$ is random, observed data and $\theta$ are all of the fixed but unknown parameters of the model
    - We then observe the data $Y_1, ..., Y_n$
    - Using the data, we attempt to estimate the parameters of the model $\theta$ through maximum likelihood estimation (what parameters are most likely to give us the data we observed?)
    - Define likelihood function $L(\theta) = P(Y_1, ..., Y_n; \theta)$ and its log-likelihood $l(\theta) = \ln(L(\theta))$
    - Pick the $\hat \theta$ that gives the highest value of the log-likelihood and thus likelihood function ($\arg \max_\theta L(\theta))$
- Bayesian: treat the thing we know about the world as random
    - Define model $P(Y|X; \theta_Y)$ where $Y$ is the observed data and $\theta_Y$ are the parameters of the distribution
    - Define a prior probability $P(X; \theta_X)$ where $X$ is random and unknown and $\theta_X$ are the hyperparameters of the prior
    - Observe some data $Y_1, ..., Y_n$, usually coming from $P(\cdot | X)$
    - Understand the world through the distribution of $X|Y$ - condition on the data we observe and how does this affect the shape of the distribution of $X$
    - Use Bayes' theorem: $P(X|Y) = \dfrac{P(Y|X)P(X)}{P(Y)}$ to get the posterior probability
- The more data observed, the more "peaky" the posterior becomes as we have to rely less on the prior
- Point estimates on the posterior:
    - Maximum A Posteriori Estimate (MAP): Look at the posterior, find the value of $X$ that maximizes it: $\arg \max_x P(X | Y) = \arg \max_x \dfrac{P(X)P(Y|X)}{P(Y)} = \arg \max_x = P(X)P(Y|X)$, we can get rid of the denominator as it doesn't affect the value of $X$ that maximizes the posterior (mode of distribution)
    - Least Mean-Squared Error (LMSE): estimate of $X$ that minimizes $E[X|Y]$ (mean of distribution)
- Gaussian Mixture Models: When looking at a subset of the data grouped on a certain feature, it tends to be Gaussian
    - Y: observed data
    - X: hidden labels (gender): $P(X; \pi) = \pi_1^x \pi_0^{1 - x}$. This is the Gaussian Mixture Model
    - Prior: $P(Y|X; \cdot) = N(Y; \mu_0, \sigma^2)$ if $X = 0$ else $N(Y; \mu_1, \sigma^2)$ if $X = 1 \Rightarrow N_0^{1 - X} N_1^X$
    - Posterior: $P(X_1|Y_1) = \dfrac{(\pi_1 N_1)^X}{\pi_0N_0 + \pi_1N_1}$ and $P(X_0|Y_0) = \dfrac{(\pi_0 N_0)^{1 - X}}{\pi_0N_0 + \pi_1N_1}$
    - If parameters are known: means, variances, probabilities, then the posterior probabilities are easy, just plug them in and select the class with the higher posterior
    - If only labels are known, you are back in the Frequentist setting with fixed parameters. Calculate the maximum likelihood by treating the probabilities as a function of the parameters to find the parameters that best fit the observed data

## Lecture 9



