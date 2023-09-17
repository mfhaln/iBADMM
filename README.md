# Federated Scheduling of Fog-native Applications over Multi-Domain Edge-to-Cloud Ecosystem
Supportive repo of CNSM 2023 paper: Federated Scheduling of Fog-native Applications over Multi-Domain Edge-to-Cloud Ecosystem
## Cost and utility
 Three costs are incurred in such an ecosystem: first is the cost of scheduling (i.e. placing) a microservice at a fog node, $\phi^s_n$, primarily driven by: the CPU capacity, price of energy supply and the PUE of the node. Second, is the cost of processing admitted workload of a microservice $s$ at fog node $n$, $\theta^s_n$. This too is driven by CPU capacity and structure of energy supply at $n$, along with the task size, $c^s$. Third is the cost of sending data traffic in the network. Here, this is modeled as two-part cost of: sending user-generated data on the upload direction of access-fog paths $P_U$, $\theta^s_{un}$; and the cost of routing the output of microservices to their dependents on inter-cluster paths $P_N$, $\theta^s_{nm}$, ${n, m} \in N$. Cost of data upload reflects user intents. Recall that here we assume such intents to focus on cost of upload traffic and risk to QoS. Hence, $\theta^s_{un}$ is driven by the size of user data for any microservice, $q^s$, and the quality of upload path $p \in P_U$, determined by path metrics $\langle b_p, l_p, h_p\rangle$. Similarly, the cost of sending $s$ results to its dependent $t$, depends on the size of results, $r^s$ and whether $(s,t)$ are hosted on the same or different fog nodes, where the cost of $p \in P_N$ will be added. This is a novel differentiation from our earlier work of [11], where cost was considered for routing the result of individual microservices to the access node, on the download direction of $P_U$. To this end, recall that $F(\eta_n, W)$ is a utility function that reflects the intents for workflow greenness. We consider an affine function that attracts workload per $s$ to nodes of higher supply of green energy. The function is formulated as: 
 ```math 
 F(\eta_n, W) = \frac{c^s}{\eta_n}, \forall s \in S^w
```
Note that in scenarios where green energy is more expensive, $F(.)$ will pose a trade-off with $\phi^s_n$.

## Evaluation 
### Evaluation Settings (Analytical)
| Parameter   | Setting  |
|:-----------------------|:-------------------|
|$\epsilon_{pri}, \epsilon_{dual}, \epsilon_{plc}, \rho$| {$10^{-2}, 10^{-3}, 10^{-2}, 1$} |
|Number of workflows | $\{10, 24\}$ | 
|Number of microservices per workflow | $\{5, 10\}$|
|Workflow graph | Hub \& Spoke of 5 and 10 microservices (H\&S\_5 and H\&S\_10)|
|Average task size per microservice [mCPU] | [100 - 200] |
|Average input/output data per microservice [Mb] | [0.4, 8.0] |
|Average response time tolerance [msec] | [30 - 150] |
|Fog nodes (cloud:$t_1$, cloudlet:$t_2$, edge:$t_3$) | {t<sub>1</sub>:2, t<sub>2</sub>:3, t<sub>3</sub>:4} |
|Number of users per access node | [500, 2000] |
|Number of access nodes | 11 |
|Average request rate per access node [request/s]| 1000 |
|Average CPU capacity per node [mCPUs] | {t<sub>1</sub>:[10<sup>6</sup> - 10<sup>7</sup>], t<sub>2</sub>:[10<sup>5</sup> - 10<sup>6</sup>], t<sub>3</sub>:[10<sup>4</sup> - 10<sup>5</sup>]} |
|Average CPU energy price per node [PpmCPU] | {t<sub>1</sub>:[10<sup>-5</sup> - 10<sup>-4</sup>], t<sub>2</sub>:[10<sup>-4</sup> - 10<sup>-3</sup>], t<sub>3</sub>:[10<sup>-3</sup> - 10<sup>-2</sup>]} |
|Average fraction of supply of green energy | {t<sub>1</sub>:[0.7-0.9], t<sub>2</sub>:[0.5-0.7], t<sub>3</sub>:[0.3-0.5]} | 
|Average bandwidth capacity per path [Mb/s] | {t<sub>1</sub>:[10<sup>5</sup> - 10<sup>6</sup>], t<sub>2</sub>:[10<sup>4</sup> - 10<sup>5</sup>], t<sub>3</sub>:[10<sup>3</sup> - 10<sup>4</sup>]} |
|Average link length [Km] | {t<sub>1</sub>:[10-100], t<sub>2</sub>:[1-10], t<sub>3</sub>:[0.5-1]} | {t<sub>1</sub>:10, t<sub>2</sub>:10, t<sub>3</sub>:10} |

### Green Energy Variation
Figure 2 (c) shows the range of mPoP placements of iBADMM (direct) between $2-5$, with no variation across workflows. Whereas, iBADMM placement spans the entire range of nodes. Figure 2 (d) further shows the spread of a workflow by iBADMM (direct) to be smaller than iBADMM by a factor of $\approx 30\%$.

[Figure 2 (c): mPoPs Replicas](https://github.com/mfhaln/iBADMM/files/12643742/simmer_farm_geng_msrep_bp.pdf)

[Figure 2 (d): Workflow Spread](https://github.com/mfhaln/iBADMM/files/12643745/simmer_farm_geng_wfdist_bar.pdf)

### Workflow Variation
Figure 3 (c) shows that for resource intensive workflows of critical latency, iBADMM (direct) nears or violates the latency threshold. This is because of the pull towards the edge, which results in exhausting CPU resources and considerably increasing processing latency. Figure 3 (d) show iBADMM to achieve consistently high workflow greenness of $\approx 0.85-0.89$, unlike iBADMM (direct) which spans from $0.4-0.85$ due to higher utilisation of the edge. Notably, for workflows of smaller data size, the greenness KPI improves for iBADMM (direct) as the cost of uploading data to the cloud is smaller leading to higher distribution over farther clouds.

[Figure 3 (c): LRB](https://github.com/mfhaln/iBADMM/files/12643755/simmer_farm_mservice_arrivals_bp.pdf)

[Figure 3 (d): Workflow greenness](https://github.com/mfhaln/iBADMM/files/12643754/simmer_farm_green_mservice_resources_id_Fnode_bp.pdf)

## References

[11] M. AL-Naday, T. Goethals, and B. Volckaert, “Intent-based decentralized
orchestration for green energy-aware provisioning of fog-native work-
flows,” in 2022 18th International Conference on Network and Service
Management (CNSM), 2022, pp. 184–190.
