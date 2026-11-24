# A counterexample family to a conjecture of Jia and Song on remoteness and the second distance eigenvalue

## The conjecture

Jia and Song (*J. Inequal. Appl.* **2018**:69) proposed the following, restated verbatim as
Conjecture 1 in the survey of Aouchiche and Rather, *Proximity and Remoteness in Graphs: a
survey* (arXiv:2310.12777v2, 22 Jan 2024), where it is listed as open:

> **Conjecture (Jia–Song).** Let $G \not\cong (K_n,\, K_n - e)$ be a connected graph of order
> $n \ge 4$ with remoteness $\rho$. Then
> $$\rho + \partial_2 \;\ge\; \frac{n}{n-1} + \frac{n-1-\sqrt{(n-1)^2+8}}{2},$$
> with equality holding if and only if $G \cong K_n - 2e$, where $2e$ are two matching edges.

Here $\rho(G) = \max_v \frac{1}{n-1}\sum_u d(u,v)$ is the remoteness and
$\partial_1 \ge \partial_2 \ge \cdots \ge \partial_n$ are the eigenvalues of the distance
matrix $D(G)$.

**The conjecture is false.** We give an infinite family of counterexamples, verified in exact
arithmetic, on which the deficit does not merely persist but *increases*, approaching $1/6$.

---

## 1. A preliminary correction: the stated equality case is wrong

Before exhibiting counterexamples we record a separate defect, which explains the shape of
the error.

Write $B(n) = \frac{n}{n-1} + \frac{n-1-\sqrt{(n-1)^2+8}}{2}$ for the conjectured bound.

> **Observation 1.** For every $n \ge 4$, the graph $K_n - e$ satisfies $\rho + \partial_2 = B(n)$
> exactly, whereas $K_n - 2e$ satisfies $\rho + \partial_2 = \frac{n+2}{n-1} \ne B(n)$.

Verified symbolically for $4 \le n \le 9$ (exact radicals, `sympy`):

| $n$ | $K_n-e$: $\rho+\partial_2$ | equals $B(n)$? | $K_n-2e$: $\rho+\partial_2$ | $B(n)$ |
|---:|---|:---:|---|---|
| 4 | $17/6-\sqrt{17}/2$ | yes | $4/3 \approx 1.3333$ | $0.77178$ |
| 5 | $13/4-\sqrt{6}$ | yes | $5/4 = 1.25$ | $0.80051$ |
| 6 | $37/10-\sqrt{33}/2$ | yes | $6/5 = 1.2$ | $0.82772$ |
| 7 | $25/6-\sqrt{11}$ | yes | $7/6 \approx 1.1667$ | $0.85004$ |
| 8 | $65/14-\sqrt{57}/2$ | yes | $8/7 \approx 1.1429$ | $0.86794$ |
| 9 | $41/8-3\sqrt{2}$ | yes | $9/8 = 1.125$ | $0.88236$ |

So the bound $B(n)$ is the value of the *excluded* graph $K_n - e$, not of the claimed
extremal graph $K_n - 2e$. Indeed $K_n - mе$ has $\rho + \partial_2 = \frac{n+2}{n-1}$ for
every $m \ge 2$, independent of $m$ — so no matching-deleted complete graph is extremal.

The likely origin is a transcription slip from the companion results on $\partial_1$ proved in
the same paper (survey Thms. 4.28–4.29): there $K_n - e$ pairs with the radicand $(n-1)^2+8$
and $K_n - 2e$ pairs with $(n-1)^2+16$. The $\partial_2$ conjecture carries the $+8$ radicand —
matching $K_n-e$ — but names $K_n-2e$ and excludes $K_n-e$ from its own hypothesis.

Under the natural repair (exclude only $K_n$; equality at $K_n-e$) the inequality is still
false, as we now show.

---

## 2. The counterexample family

For $s \ge 2$ let
$$G_s \;=\; K_1 \vee \big(2K_s\big),$$
the **cone over two disjoint cliques**: a dominating vertex $c$ joined to every vertex of two
vertex-disjoint copies of $K_s$. Then $n = |V(G_s)| = 2s+1$, and $G_s$ has diameter $2$.

The smallest members are $G_2 = K_1 \vee 2K_2$ on $5$ vertices (graph6 `DQ{`) and
$G_3 = K_1 \vee 2K_3$ on $7$ vertices (graph6 `FQhVw`).

> **Theorem 2.** For every $s \ge 2$,
> $$\rho(G_s) = \frac{3}{2}, \qquad
>   \partial_2(G_s) = \frac{3s-1-\sqrt{9s^2+2s+1}}{2},$$
> $$\rho + \partial_2 \;=\; \frac{3s}{2} + 1 - \frac{\sqrt{9s^2+2s+1}}{2}.$$

**Proof of $\rho = 3/2$.** The centre $c$ is adjacent to all $2s$ others, so $t(c) = 2s$ and
$\tilde t(c) = 1$. Any clique vertex $v$ is at distance $1$ from $c$ and from the $s-1$ other
vertices of its own clique, and at distance $2$ from each of the $s$ vertices of the opposite
clique (diameter $2$, since $c$ dominates). Hence $t(v) = 1 + (s-1) + 2s = 3s$ and
$\tilde t(v) = 3s/(2s) = 3/2$. The maximum is $3/2$. $\square$

The eigenvalue formula follows from the equitable partition $\{c\} \cup C_1 \cup C_2$; it was
computed in exact radicals with `sympy` for $2 \le s \le 7$ and matched against the closed
form (radicand $9s^2+2s+1$ fits the data $41, 88, 153, 236, 337, 456$ exactly).

> **Theorem 3.** Every $G_s$ with $s \ge 2$ violates the Jia–Song inequality. Moreover
> $$\lim_{s\to\infty}\big(\rho+\partial_2\big)(G_s) = \frac{5}{6},
> \qquad \lim_{s\to\infty} B(2s+1) = 1,$$
> so the deficit tends to $\tfrac16$ and the conjecture fails by a constant margin, not
> marginally.

**Proof.** Write $L(s) = \frac{3s}{2}+1-\frac{\sqrt{9s^2+2s+1}}{2}$ and, with $n = 2s+1$,
$B = s + 1 + \frac{1}{2s} - \sqrt{s^2+2}$.

*Step 1: $L(s) < \tfrac56$ for all $s>0$.* The inequality $L(s) < \tfrac56$ is equivalent to
$\sqrt{9s^2+2s+1} > 3s + \tfrac13$. Both sides are positive, and squaring gives
$$(9s^2+2s+1) - \Big(3s+\tfrac13\Big)^2 = \tfrac{8}{9} > 0,$$
identically in $s$. So the strict inequality holds for every $s>0$.

*Step 2: $B > \tfrac56$ for $s \ge 3$.* We have $B - \tfrac56 = s - \sqrt{s^2+2} + \tfrac16 + \tfrac{1}{2s}$.
Since $s - \sqrt{s^2+2} = \frac{-2}{s+\sqrt{s^2+2}} > \frac{-1}{s}$, it follows that
$B - \tfrac56 > \tfrac16 - \tfrac{1}{2s} > 0$ whenever $s > 3$; direct evaluation gives
$B - \tfrac56 \approx +0.01671 > 0$ at $s = 3$.

Combining, $L(s) < \tfrac56 < B$ for all $s \ge 3$.

*Step 3: the case $s=2$.* Exactly,
$$L(2) = 4 - \tfrac{\sqrt{41}}{2} \approx 0.7984378813, \qquad
  B(5) = \tfrac{13}{4} - \sqrt6 \approx 0.8005102572,$$
so $L(2) - B(5) = \tfrac34 + \sqrt6 - \tfrac{\sqrt{41}}{2} \approx -2.072\times10^{-3} < 0$.

*Limits.* $L(s) \to \tfrac{5}{6}$ and $B \to 1$ as $s \to \infty$; the exact gap is
$$L(s) - B \;=\; \frac{s\big(s + 2\sqrt{s^2+2} - \sqrt{9s^2+2s+1}\big) - 1}{2s}
\;\longrightarrow\; -\frac16 . \qquad \blacksquare$$

### Numerical summary

| $s$ | $n$ | $\rho+\partial_2$ (exact) | value | bound $B(n)$ | deficit |
|---:|---:|---|---:|---:|---:|
| 2 | 5 | $4-\sqrt{41}/2$ | 0.7984379 | 0.8005103 | $-0.00207$ |
| 3 | 7 | $11/2-\sqrt{22}$ | 0.8095842 | 0.8500419 | $-0.04046$ |
| 4 | 9 | $7-3\sqrt{17}/2$ | 0.8153416 | 0.8823593 | $-0.06702$ |
| 5 | 11 | $17/2-\sqrt{59}$ | 0.8188543 | 0.9038476 | $-0.08499$ |
| 6 | 13 | $10-\sqrt{337}/2$ | 0.8212201 | 0.9189193 | $-0.09770$ |
| 7 | 15 | $23/2-\sqrt{114}$ | 0.8229217 | 0.9300001 | $-0.10708$ |
| 10 | 21 | — | 0.8260091 | 0.9504951 | $-0.12449$ |
| 100 | 201 | — | — | — | $-0.16241$ |
| $\infty$ | — | $\to 5/6$ | 0.8333… | $\to 1$ | $\to -1/6$ |

---

## 3. The smallest counterexample, checkable by hand

$$G_2 \;=\; K_1 \vee 2K_2, \qquad n = 5, \qquad \text{graph6 } \texttt{DQ\{}$$

Vertices $\{c, a_1, a_2, b_1, b_2\}$; edges $ca_1, ca_2, cb_1, cb_2, a_1a_2, b_1b_2$
(six edges — the "bowtie"/butterfly graph). It is neither $K_5$ nor $K_5 - e$, so it lies in
the conjecture's stated scope. Distance matrix (order $c,a_1,a_2,b_1,b_2$):

$$D=\begin{pmatrix}0&1&1&1&1\\1&0&1&2&2\\1&1&0&2&2\\1&2&2&0&1\\1&2&2&1&0\end{pmatrix}$$

Row sums: $4, 6, 6, 6, 6$, so $\rho = 6/4 = 3/2$. The characteristic polynomial factors, giving
$\partial_2 = \tfrac{5-\sqrt{41}}{2} \approx -0.7015621$. Hence
$$\rho + \partial_2 = 4 - \tfrac{\sqrt{41}}{2} \approx 0.7984379
< 0.8005103 \approx \tfrac{13}{4}-\sqrt{6} = B(5).$$

The verification is a $5\times5$ eigenvalue computation — a second's work for any computer
algebra system, and doable by hand.

---

## 4. How it was found, and exhaustive context

Exhaustive sweep over all connected graphs (nauty `geng`), distance spectra by BFS plus
`numpy.linalg.eigvalsh`, every candidate then re-verified in exact radicals with `sympy`:

| $n$ | connected graphs | graphs strictly below $B(n)$ |
|---:|---:|---|
| 4 | 6 | $K_4$ only (excluded) |
| 5 | 21 | $K_5$ (excluded), **`DQ{`** |
| 6 | 112 | $K_6$ only (excluded) |
| 7 | 853 | $K_7$ (excluded), **`FQhVw`** |
| 8 | 11 117 | $K_8$ only (excluded) |

The two genuine violators at $n=5$ and $n=7$ are precisely $G_2$ and $G_3$; recognising them
as $K_1 \vee 2K_s$ produced the infinite family. Note the parity: no counterexample exists at
even $n$ in this family, since $n = 2s+1$ is always odd — which is presumably why sampling
missed it.

The related families behave as follows, confirming the construction is specific:
$K_1 \vee tK_s$ satisfies the inequality comfortably for $t \ge 3$ (e.g. $t=3$: deficit
$+0.19$; $t=4$: $+0.28$), so **two** cliques is essential; and $K_n - me$ gives
$\frac{n+2}{n-1}$ for all $m \ge 2$, always above $B(n)$.

---

## 5. What survives

The counterexamples all have $\rho = 3/2$ and diameter $2$ — they are "wide but shallow".
A repaired conjecture would need to exclude such cones, or restrict to larger diameter. The
value $5/6$ is a natural candidate for the true infimum of $\rho + \partial_2$ over connected
non-complete graphs of odd order; whether $\inf(\rho+\partial_2) = 5/6$ over all connected
graphs $\ne K_n$, and whether it is attained only in the limit, is left open here.

## Reproducibility

- Graph enumeration: `nauty` 2.8.8 (`geng -c n`).
- Distances: BFS, integer arithmetic. Spectra: `numpy.linalg.eigvalsh` for screening,
  `sympy` exact radicals for every reported value.
- All reported violations were confirmed symbolically; no claim rests on floating point.

## References

1. H. Jia and H. Song, *Remoteness and distance, distance (signless) Laplacian eigenvalues of a graph*, J. Inequal. Appl. **2018**:69.
2. M. Aouchiche and B. A. Rather, *Proximity and Remoteness in Graphs: a survey*, arXiv:2310.12777v2 (2024). (Conjecture 1; Thms. 4.27–4.32.)
3. M. Aouchiche and P. Hansen, *Distance spectra of graphs: a survey*, Linear Algebra Appl. **458** (2014) 301–386.
4. B. D. McKay and A. Piperno, *Practical graph isomorphism, II*, J. Symbolic Comput. **60** (2014) 94–112.
