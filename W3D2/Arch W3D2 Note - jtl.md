# Arch W3D2 Note

**Arthor: Tianle Jiang**

## Performance

A traditional simple metric: $\text{performance}(x) = \dfrac{1}{\text{execution}\underline{} \text{time} (x)}$

#### Aspects of CPU performance

$$
\text{CPU time} = \dfrac{\text{Seconds}}{\text{Program}} = \dfrac{\text{Instructions}}{\text{Program}} \times \dfrac{\text{Cycles}}{\text{Instructions}} \times \dfrac{\text{Seconds}}{\text{Cycles}}
$$

$\Rightarrow$  Inst Count,  CPI,  Clock Rate

Factors:

|              | Inst Count                         | CPI                             | Clock Rate                    |
| ------------ | ---------------------------------- | ------------------------------- | ----------------------------- |
| Program      | reduce Inst Count, not code length |                                 |                               |
| Compiler     | $\checkmark$                       | reduce stall by code movement   |                               |
| Inst.Set     | RISC > CISC                        | RISC better suited for pipeline |                               |
| Organization |                                    | increase operation speed        | simple design allow higher CR |
|              |                                    |                                 |                               |

#### Amdahl's Law

improve the most common part of the original system
$$
S_p = \dfrac{1}{(1-\eta) + \dfrac{\eta}{S}}, \ \ \eta \text{ is the most common part}
$$

## Memory Hierarchy

Porcessor-Memory performance gap $\longrightarrow$ need cache

The Principle of Locality:  temporal locality + spatial locality $\longrightarrow$ hardware speed improvement

##### Cache

measures:  average memory-access time (AMAT)
$$
AMAT_{\text{cache}} = T_{\text{hit}} + \eta_{\text{miss-rate}} * T_{\text{penalty}}
$$
Cache structure:
$$
\text{core} \xrightarrow {\text{send virtual address (va)}} \text{cache} \xrightarrow[\text{translate va to pa}] {\text{send physical address (pa)}} \text{memory}\\
\xrightarrow{va} \text{cache} \xrightarrow{va \to idx} \text{payload}
$$
$va \to idx$ mapping: 

* direct mapping (DM)
* fully associative (FA)
* set associative (SA)