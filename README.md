# Port of Charleston Right Whale Risk Assessment

> Presently, there are no recommended lanes off Charleston. Would recommended lane/s reduce the relative risk of interactions between commercial vessels and right whales? Can it be determined?  If so, what is the expected reduction in risk of interactions and where should the lanes be placed? 

## Suggested Approach

Following Fonnesbeck *et al.* (2008), we will construct a predictive model of right whale occurrence that is based on existing aerial survey data and relevant environmental predictors of whale habitat use, such as bathymetry and water temperature. This model will be used as a tool to identify a shipping lane designation that minimizes risk to the migratory northern right whale population.

The metric for risk for a particular lane designation will be the mean probability of co-occurrence of ships and whales over the total area defined by any candidate lane. To avoid having to account for small-scale factors related to the interaction of whales and ships, risk will be estimated at a relatively coarse scale. Specifically, I will estimate the expected occurrence probability of whales over the cells of a 4km grid.

A key component of the modeling approach is the estimation of the probability of occupancy in each grid cell, for a particular month. Occupancy is simply the probability that one or more animals currently occupies a grid cell. Estimates of occupancy are informed by aerial survey data, which includes both sightings and on-watch effort. While a sighting comprises evidence that a grid cell is occupied, the absence of a sighting may indicate either that a cell is not occupied, or that a cell is occupied but the animals were simply not detected by observers.

The probability of one or more detections in a given grid cell $i$ during a given month can be expressed as the complement of the probability of no detections. In turn, the probability of no detections during a given month is the product of the probability of observing no groups ($y_{ij} = 0$) on each survey day $j$. We assume that these daily probabilities are approximately equal, so this is the daily probability $Pr(y_i = 0)$ raised to the number of survey days $n$:

\\[\pi_i = 1 - \prod_{j=1}^n Pr(y_{ij}=0) = 1 - [Pr(y_i=0)]^n\\]

Encounter probabilities will be estimated for each month of the year, to account for the seasonal migratory movement of whales. To aid the predictive performance of the model, we will use covariates to estimate monthly encounter probabilities; these covariates will include sea surface temperature (SST), bathymetry, as well as month.

An expanded model might additionally include a conditional auto-covariance function for the cells of the habitat grid, allowing information from adjacent grid cells to help inform one another, thereby improving model estimates.

The total risk $r_k$ for a particular lane designation $k$ would then be calculated as:

\\[\rho_k = \sum_i \sum_m  \pi_i^{(m)} I(i \in k)\\]

where we sum over cells $i=1,\ldots,n$ and months $m=1,\ldots,M$ and $I$ is the indicator function, which returns 1 when the condition is true (in this case, whether cell $i$ is in lane $k$), and zero otherwise.

External constraints on the identification of an optimal line may include factors such as a maximum distance to port and a minimum lane width.