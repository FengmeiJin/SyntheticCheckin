# Generate Large-scale Synthetic Check-in Sequences
A program for synthesizing check-in sequences based on the statistics of [Geolife](https://www.microsoft.com/en-us/research/publication/geolife-gps-trajectory-dataset-user-guide/)

### Statistics extracted from Geolife
- Transition probability between POIs
- The probability of each POI being a start point of a trip
- The popularity of each POI among Geolife
- Stay duration for each POI category
- Moving speed histogram
- ...

### Steps of simulation
Since realistic check-in records from those check-in applications against the epidemic are hardly accessible, in order to further validate the effectiveness and scalability of our proposed approaches, we simulate check-in sequences as follows: 
1. _Graph_: Create a road network-based directed graph in which nodes are POIs and each edge connects two spatially close nodes (i.e., 500 meters). In particular, each edge $e_{ij}$ is assigned to a weight indicating the transition probability from $p_i$ to $p_j$ which is extracted from Geolife in advance. 
2. _Initialization_: To generate a single sequence of POI-related check-ins, we initially sample a starting node $p_0$ on the graph, a starting timestamp $t_0$ within a given period, a moving velocity $v$ from 0 (i.e., the object staying there) to 60km/h (i.e., maximum driving speed in the city) and a maximum walk length $h$ (dependent to the frequency of the center collecting data from users, e.g., $h\leq 20$ for daily collection). 
3. _Generation_: Starting from $p_0$, we perform the \textit{random walk} on the directed graph following the edge weights until obtaining an $h$-length sequence of POIs $s=\{p_0,p_1,\ldots,p_h\}$. Specifically, for a sampled POI $p_i$, its arrival timestamp depends on the departure time of the previous $p_{i-1}$ and the time cost moving from $p_{i-1}$ to $p_i$, i.e., $t_i=(t_{i-1}+d_{i-1})+\frac{d(p_{i-1},p_i)}{v}$ where $(t_i+d_i)$ denotes the departure time from $p_i$. 
4. We repeat Step 2-3 to generate $N$ sequences of one-day check-ins (i.e., $h=20$).

## Codes to appear soon ...
......

Please feel free to contact fengmei.jin@uq.edu.au if encountering any unexpected issues in this project.
