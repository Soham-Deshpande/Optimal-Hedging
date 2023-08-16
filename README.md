# Optimal-Hedging
A project conducted as a group in the Mako Internship

We decided that instead of having fixed time intervals for hedging, it made more sense to implement some finer control by hedging according to the needs of our position, hopefully helping to reduce unnecessary transaction costs. We did this by letting an arbitrary function determine the ‘bands’ around our positional delta which, upon being crossed, we would initiate a hedging trade: naturally, the next step was to determine the inputs of this function and then estimate an appropriate form. We decided that gamma along with the transaction costs would be the best inputs to use as knowing that gamma measures the sensitivity of the option price to changes in the delta, it made sense for a higher gamma to need a tighter ‘band’ in order to not have our exposure blow up. Transaction costs were a natural choice as it makes intuitive sense for the conditions for hedging to be greater when the transaction costs are higher. The form we decided the function should take was “a*(gamma^(-1/2)) + b*transaction-costs” where a and b were weightings that we tested by playing around with the data and seeing which values seemed to give the most optimal hedging policy. This form captured the relationships we wanted to see between our input parameter values and the width of the hedging band. A quick comparison of our strategy with the hourly-hedged one reveals that our strategy hedges significantly less whilst also reducing the volatility of our delta exposure.

We unfortunately ran out of time to implement this (we still have most of the code in place though), but we planned to have a momentum indicator for the delta to determine what quantity of underlying we should purchase to hedge the option. The plan was that we would offset the hedge from 0 on the side opposite to the band that was hit by a quantity of a*(d^½) where a is a weighting and d is the strength of our indicator (<1). The hope was that if the underlying exhibited momentum properties, hedging by this much would provide an extra buffer that would hopefully reduce the number of rebalancing trades needed whilst not taking on any extra delta exposure. It is probably harder to explain than it is to just draw a diagram, but the gist is that if we expect the option delta to continue rising, it makes sense to hedge so that our total delta exposure is slightly below the 0 line as we would expect our total delta to hit that line eventually, just for it to do so at a later date.

In addition, we initially tried to explore a deep hedging approach where we would use ML to find an optimal policy for hedging: ultimately, due to time constraints and lack of data/resources we decided that this approach was not best suited to this specific task. One of the papers that we looked at that helped inspire the banded approach was ‘Optimal Hedging of Options with Transaction Costs’ by Zakamouline, although their paper was not particularly suited to our specific task and so we still had to flesh out the strategy ourselves.
