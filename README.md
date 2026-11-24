# Disproof of a Jia–Song conjecture on remoteness and the second distance eigenvalue

This repository contains a counterexample — and an infinite counterexample family — to a
published, previously open conjecture in spectral graph theory, together with the materials
needed to formalize the core claim in **Lean 4 / mathlib**.

**Status:** The mathematics has been verified in exact arithmetic (symbolic radicals, no
floating point) outside Lean. The Lean formalization is *not yet done* — this repo is set up
so that Claude Code can build it with a compiler in the loop. See
[`LEAN_SPEC.md`](#the-lean-task) below.

> ⚠️ **Verify before publicizing.** The "open" status comes from a January 2024 survey; this
> is November 2026. Before claiming novelty, check Google Scholar for citations of the
> Jia–Song paper and of arXiv:2310.12777 (2024–2026) in case this was already settled, and
> independently re-run the 5×5 eigenvalue check in a CAS you trust. See *Before you publish*
> at the end.

---

## 1. The conjecture

Due to **H. Jia and H. Song**, *Remoteness and distance, distance (signless) Laplacian
eigenvalues of a graph*, J. Inequal. Appl. **2018**:69. Restated as **Conjecture 1** in the
survey **M. Aouchiche and B. A. Rather**, *Proximity and Remoteness in Graphs: a survey*,
arXiv:2310.12777v2 (22 Jan 2024), where it is listed as **open**.

For a connected graph $G$ of order $n$:
- $d(u,v)$ is the shortest-path distance; $D(G)$ is the $n\times n$ distance matrix.
- $\partial_1 \ge \partial_2 \ge \cdots \ge \partial_n$ are the eigenvalues of $D(G)$ (the
  *distance spectrum*).
- The **remoteness** is $\rho(G) = \max_{v}\frac{1}{n-1}\sum_{u} d(u,v)$ (the largest average
  distance from a vertex to all others).

> **Conjecture (Jia–Song).** Let $G \not\cong K_n,\, K_n - e$ be a connected graph of order
> $n \ge 4$. Then
> $$\rho + \partial_2 \;\ge\; \frac{n}{n-1} + \frac{\,n-1-\sqrt{(n-1)^2+8}\,}{2},$$
> with equality if and only if $G \cong K_n - 2e$ (two independent edges deleted).

Write $B(n) = \dfrac{n}{n-1} + \dfrac{n-1-\sqrt{(n-1)^2+8}}{2}$ for the claimed bound.

**The conjecture is false.**

---

## 2. The result

### 2a. A preliminary defect: the stated equality case is wrong

Independently of any counterexample, the equality clause does not hold as printed.

- $K_n - e$ satisfies $\rho + \partial_2 = B(n)$ **exactly** (verified symbolically,
  $4 \le n \le 9$).
- $K_n - 2e$ — the *claimed* extremal graph — gives $\rho + \partial_2 = \frac{n+2}{n-1}$,
  which is **not** $B(n)$. In fact $K_n - me$ gives $\frac{n+2}{n-1}$ for every $m \ge 2$, so
  no matching-deleted complete graph is extremal.

So the bound $B(n)$ is the value of the *excluded* graph $K_n-e$, while the graph named as
extremal sits well above it. The likely cause is a transcription slip from the companion
$\partial_1$ results in the same paper, where radicand $(n-1)^2+8$ pairs with $K_n-e$ and
$(n-1)^2+16$ pairs with $K_n-2e$.

Under the natural repair (exclude only $K_n$; equality at $K_n-e$) the inequality is **still
false**, as follows.

### 2b. The counterexample family

For $s \ge 2$, let
$$G_s \;=\; K_1 \vee \big(2K_s\big)$$
— the **cone over two disjoint cliques**: one *apex* vertex joined to every vertex of two
vertex-disjoint copies of $K_s$. Then $n = 2s+1$ and $\operatorname{diam}(G_s)=2$.

**Theorem (values).** For every $s \ge 2$,
$$\rho(G_s) = \tfrac{3}{2}, \qquad
  \partial_2(G_s) = \frac{3s-1-\sqrt{9s^2+2s+1}}{2}, \qquad
  \rho+\partial_2 = \frac{3s}{2}+1-\frac{\sqrt{9s^2+2s+1}}{2}.$$

**Theorem (violation).** Every $G_s$ ($s\ge2$) violates the Jia–Song inequality, and
$$\lim_{s\to\infty}(\rho+\partial_2)(G_s) = \tfrac{5}{6}, \qquad
  \lim_{s\to\infty} B(2s+1) = 1,$$
so the deficit does not shrink — it **grows to $\tfrac16$**. The conjecture fails by a
constant margin, not marginally.

*Proof sketch.* $\rho=\tfrac32$: the apex has average distance $1$; each clique vertex is at
distance $1$ from the apex and its $s-1$ clique-mates and distance $2$ from the $s$ opposite
vertices, giving transmission $3s$ and average $3s/(2s)=\tfrac32$. The eigenvalue follows from
the equitable partition $\{\text{apex}\}\cup C_1\cup C_2$. For the violation:
$\rho+\partial_2 < \tfrac56$ reduces to $\sqrt{9s^2+2s+1} > 3s+\tfrac13$, i.e.
$(9s^2+2s+1)-(3s+\tfrac13)^2 = \tfrac89 > 0$ — true for all $s$; and $B(2s+1) > \tfrac56$ for
$s\ge3$ with the $s=2$ case checked exactly. ∎

| $s$ | $n$ | $\rho+\partial_2$ (exact) | value | $B(n)$ | deficit |
|----:|----:|---|------:|------:|--------:|
| 2 | 5 | $4-\sqrt{41}/2$ | 0.7984379 | 0.8005103 | −0.00207 |
| 3 | 7 | $11/2-\sqrt{22}$ | 0.8095842 | 0.8500419 | −0.04046 |
| 4 | 9 | $7-3\sqrt{17}/2$ | 0.8153416 | 0.8823593 | −0.06702 |
| 5 | 11 | $17/2-\sqrt{59}$ | 0.8188543 | 0.9038476 | −0.08499 |
| 6 | 13 | $10-\sqrt{337}/2$ | 0.8212201 | 0.9189193 | −0.09770 |
| ∞ | — | $\to 5/6$ | 0.83333… | $\to 1$ | $\to -1/6$ |

### 2c. The smallest counterexample — checkable by hand

$$G_2 = K_1 \vee 2K_2 \quad (n=5,\ \text{the \textbf{bowtie}/butterfly graph, graph6 } \texttt{DQ\{})$$

Vertices $\{c, a_1, a_2, b_1, b_2\}$; edges $ca_1, ca_2, cb_1, cb_2, a_1a_2, b_1b_2$.
Distance matrix (order $c, a_1, a_2, b_1, b_2$):

$$D = \begin{pmatrix}
0&1&1&1&1\\
1&0&1&2&2\\
1&1&0&2&2\\
1&2&2&0&1\\
1&2&2&1&0
\end{pmatrix}$$

- Row sums $4,6,6,6,6$, so $\rho = 6/4 = 3/2$.
- Characteristic polynomial factors so that $\partial_2 = \dfrac{5-\sqrt{41}}{2} \approx -0.7015621$.
- Hence $\rho+\partial_2 = 4-\dfrac{\sqrt{41}}{2} \approx 0.7984379$, strictly below
  $B(5) = \dfrac{13}{4}-\sqrt{6} \approx 0.8005103$.

A $5\times5$ eigenvalue computation — seconds in any CAS, and the exact comparison
$4-\tfrac{\sqrt{41}}{2} < \tfrac{13}{4}-\sqrt6$ is elementary (square to compare $\sqrt{41}$
and $\sqrt6$ terms).

---

## 3. How it was found

Exhaustive sweep of all connected graphs by order (nauty `geng`); distance spectra screened in
floating point (`numpy`), every candidate re-verified in exact radicals (`sympy`). At $n\le8$
the only sub-bound graphs are the excluded $K_n$ plus **two genuine violators**: `DQ{` ($n=5$)
and `FQhVw` ($n=7$). Recognizing these as $K_1 \vee 2K_2$ and $K_1 \vee 2K_3$ produced the
family. All counterexamples have odd order $n=2s+1$ and diameter $2$ — "wide and shallow" —
which is plausibly why sampling/testing missed them.

Companion families confirm the construction is specific: $K_1 \vee tK_s$ satisfies the
inequality comfortably for $t\ge3$ (so *two* cliques is essential), and $K_n-me$ gives
$\frac{n+2}{n-1} > B(n)$ for all $m\ge2$.

---

## 4. The Lean task

Goal: a machine-checked proof of the single-graph claim. Recommended staging.

**Option A — arithmetic core (do first).** Prove, in Lean 4 + mathlib: given the explicit
integer matrix $D$ above, (i) its remoteness value is $3/2$; (ii) $(5-\sqrt{41})/2$ is the
second-largest eigenvalue, established by exhibiting the characteristic polynomial and showing
this value is the appropriate root (mathlib has no radical eigenvalue solver — work via the
char. poly, not a "compute eigenvalues" call); (iii) $4-\sqrt{41}/2 < 13/4-\sqrt6$ via
`nlinarith`/`polyrith` on the squared forms. Header should state honestly that the
distance-matrix-from-graph step is a hypothesis here.

**Option B — faithful theorem (do next).** Additionally define the bowtie as a
`SimpleGraph` on `Fin 5`, and prove its `SimpleGraph.dist` equals $D$ entrywise (25 entries
from the edge set). This is the real deliverable and the bulk of the work; mathlib's distance
API is fiddly, so expect to prove helper lemmas.

**Option C — the family** ($K_1\vee 2K_s$, all $s$): research-grade formalization; out of
scope for a first pass.

### Running it in Claude Code (on your machine, not here)

Lean can't run in this hosted environment. On your machine:

```bash
# 1. install elan (Lean toolchain manager) -> provides `lake`, `lean`
curl https://raw.githubusercontent.com/leanprover/elan/master/elan-init.sh -sSf | sh

# 2. scaffold a mathlib project and pull the PREBUILT mathlib cache (saves hours)
lake new jiasong math
cd jiasong
lake exe cache get

# 3. open this repo's spec + write-up in Claude Code and iterate:
#    write Jiasong.lean  ->  `lake build`  ->  read errors  ->  fix  ->  repeat
claude
```

Point Claude Code at **Option A** first; get it compiling green before extending to B. The
compiler's pass/fail is the whole value here — it turns "I ran sympy and believe it" into "a
proof checker verified it."

---

## 5. Repository contents

| File | What it is |
|------|------------|
| `README.md` | This file. |
| `jia-song-disproof.md` | Full write-up: both theorems, the equality-case correction, proofs, exhaustive-sweep table, references. |
| *(add)* `jia-song-2018.pdf` | The original Jia–Song paper (J. Inequal. Appl. 2018:69). **You are adding this.** |
| *(add)* `aouchiche-rather-survey-2310.12777.pdf` | The 2024 survey stating Conjecture 1. **You are adding this.** |
| *(add)* `Jiasong.lean` | The Lean proof, once built in Claude Code. |

> Note on the attached PDF: the file provided in this session (`2606.15761v3.pdf`) is
> *Gupta, "Sharp bounds between the saturation number and the harmonic index"* — a different
> conjecture explored earlier in the project, **not** the Jia–Song source. For this result,
> add the two PDFs listed above (Jia–Song 2018, and survey arXiv:2310.12777).

---

## 6. Before you publish

1. **Re-check "open."** Search Google Scholar for citations of Jia–Song 2018 and of
   arXiv:2310.12777 in 2025–2026; confirm no one has already published this family or a
   correction. This project twice found a result was settled weeks before — don't skip it.
2. **Independently verify** the bowtie: build $D$ in Mathematica/Sage/your CAS of choice,
   confirm $\partial_2 = (5-\sqrt{41})/2$, and the strict inequality. Ten minutes; do not take
   one tool's word for it.
3. **Email the authors** (Jia; Song; and Aouchiche, `mustapha.aouchiche@polymtl.ca`): a short,
   plain note — "here is a graph that appears to violate Conjecture 1, with exact values; am I
   reading the statement correctly?" The equality-case discrepancy (§2a) makes "am I reading
   it right" a genuine question worth asking, not just courtesy.
4. **Then** write it up (a 3–5 page note: counterexample, family, closed form, equality-case
   correction) for arXiv (math.CO) and a journal such as *Discrete Applied Mathematics* or the
   original venue. A tweet, if you want one, goes *after* steps 1–3, not before.

## 7. Reproducibility of the (non-Lean) verification

- Enumeration: `nauty` (`geng -c n`).
- Distances: BFS, integer arithmetic. Screening spectra: `numpy.linalg.eigvalsh`.
- Every reported value: exact radicals in `sympy`; no claim rests on floating point.
