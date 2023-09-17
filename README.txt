This project is to implement Dynamic Pricing by Multi-armed Bandits (MAB) model. MAB is a simple example of reinforcement learning model. 

Let's imagine a general case. There is a new product available on the market, but the manager has no clue what is the best price for this product. There are 10 candidates for the manager to choose, from 100, 105, 110, ..., 145. The cost of the product is 70. Therefore, the coresponding profits are 30, 35, 40, ..., 75. On the other hand, the propensity of a customer to purchase a product is obviously impacted by the price. Here are some assumptions regarding the purchase probabilities.
1. A single customer's purchase prob only relies on the price. The prob matches Beta distribution. The higher the price is, the lower probability the customer wants to buy it.
2. For n customers, the number of buyers matches binomial distribution. 

To simulate the experiement and estimate the performance, we need to know what are the actual parameters in the distribution. Let's assume the actual alpha list and beta list for the 10 beta distributions are:
1. Alpha list = [6, 5.5, 5, 5, 4, 3.5, 3, 2.5, 2, 1.5]
2. Beta list = [4, 4.5, 5, 5, 6, 6.5, 7, 7.5, 8, 8.5]

Hence, the mean (purchae propensity) of  the 10 distribution is [0.6, 0.55, 0.5, 0.5, 0.4, 0.35, 0.3, 0.25, 0.2, 0.15]. Considering the profit list is [30, 35, 40, 45, 50, 55, 60, 65, 70,75], the expected profit from each customer is [18.0, 19.25, 20.0, 22.5, 20.0, 19.25, 18.0, 16.25, 14.0, 11.25]. Hence the 3rd price (index 0, 22.5) is the champion. 

Of course, we don't know this info. We try to guess or estiamte the coresponding parameters by observing the results of the experiement.

Multi-armed Bandits:
There are two cases in MAB, i.e., exploitation and exploration. Exploitation means always apply the current "champion", which is greedy. Exploration means to explore different options to collect more data, so that we can understand them better in next iteration. 

Epsilon-greedy:
One natural idea is that we always explore random options with epsilon (say 0.1) prob. And take the "champion" option with 1-epsilon. This idea is called epsilon-greedy.

Decayed epsilon-greedy:
At the beginning, we should explore more on the other options, but when we have enough data points for each option, we should tend to be more greedy. That is, the value of epsilon is dynamic. For example, we decrease epsilon exponentially (0.9*epsilon every time). This is called decayed or decaying epsilon-greedy.

Upper Confidence Bound (UCB):
Another idea is that we tend to explore the options with less data points (more potential). To implement it, we add an upper confidence bound to the rewards. This is called UCB.

