# φ³ Graph Atlas

An interactive atlas of the tensor structures of the multiscalar φ³ beta function
β<sub>ijk</sub> and the anomalous dimension γ<sub>φ</sub> in d = 6 − ε, through six
loops, in minimal subtraction (MS-bar).

**→ [andstergiou.github.io/phi3-graph-atlas](https://andstergiou.github.io/phi3-graph-atlas/)**

Its quartic companion is the [φ⁴ Graph Atlas](https://andstergiou.github.io/phi4-graph-atlas/).

## What is in it

35208 structures: 30979 vertex structures and 4229 propagator structures, by loop
order 3, 11, 57, 382, 3167 and 31588 at L = 1…6. Each one is drawn as a Feynman graph
and comes with

- its number in Schnetz's enumeration
  (V = 1PI vertex structures, D = leg-dressed, S = propagator structures),
- the tensor contraction and the O(n) value,
- the β and counterterm (Z) coefficients, and γ where it contributes,
- the symmetry factor S = 1/|Aut|, and |stab| and orbit, which say how the tensor behaves
  under permuting its external indices,
- whether the graph is primitive,
- a TikZ export of the drawing exactly as it appears on screen.

**Non-factorisable only** hides the structures whose tensor really splits into lower
ones: an undressed structure whose internal graph has a cut vertex, a propagator chain,
and every leg-dressed structure except a pure wave-function renormalisation — a
tree-level vertex with one irreducible self-energy on one leg. A vertex correction
dressed on a leg, or self-energies on more than one leg, count as products and are
hidden. That leaves 23291 of the 35208 — 3, 7, 36, 235, 2011, 20999 at L = 1…6.

The cut is purely topological, but it lands on the physics: the vertex structures it
keeps are exactly the 20118 with non-vanishing β under minimal subtraction, with no
exception in either direction. The cubic theory has no undressed one-vertex-reducible
vertex structures, so every vertex structure the filter removes is leg-dressed; of the
16456, the 5595 pure wave-function renormalisations survive — precisely the dressed
structures with β ≠ 0.

**Primitive only** keeps the primitive graphs: 1PI with no UV subdivergence, so the
counterterm is a single 1/ε pole. There are 662 — 661 vertex structures (1, 1, 2, 9, 62,
586 at L = 1…6) and the one-loop bubble S1.1. For a propagator, a subgraph whose contraction
leaves a scaleless graph does not count; every propagator structure from two loops on has a
subdivergence that does count. The flag was checked against Schnetz's table of φ³ periods (the
file `PeriodsPhi3` in HyperlogProcedures). The 661 are exactly the vertex graphs obtained by
deleting a vertex of a completed primitive graph listed there (L ≤ 6), each with β = (−1)<sup>L+1</sup>·S·P. Every primitive has a single-pole
counterterm, and among the 1PI structures nothing else does. The one structure with a
single pole that is not primitive is D1.2, the tree vertex with the bubble on one leg: it
is not 1PI, and its only divergence is the primitive self-energy it carries
(Z<sub>λ</sub> = −1/(12ε), β = −1/12 = γ<sub>φ</sub> of S1.1).

Every structure shows its **symmetry factor** S = 1/|Aut|, on its list row and in the
details pane. Automorphisms are counted with the external legs held fixed and parallel
lines included, so S = 1 for the triangle V1.1 and 1/2 for the bubble S1.1. Letting the
legs move multiplies |Aut| by exactly |stab|. Both counts were checked against an
independent networkx count on all 35208 structures.

**|stab| and orbit** describe how a structure's tensor behaves under permuting its
external indices. |stab| is the number of permutations of i j k that leave the tensor
unchanged, which are exactly the leg permutations realised by an automorphism of the graph;
orbit = 6/|stab| is the number of distinct tensors the permutations produce. β and
Z<sub>λ</sub> both multiply the sum of those orbit terms, so β<sub>L</sub> = L times the 1/ε
residue of Z<sub>λ</sub>. The triangle V1.1 has |stab| = 6 and orbit = 1; V2.1 has
|stab| = 2, orbit = 3 and Z<sub>λ</sub> = 7/(144ε) − 1/(12ε²), giving β = 2 · 7/144 = 7/72.

Propagators follow the same rule: exchanging i and j either leaves the tensor unchanged
(|stab| = 2, orbit = 1, a symmetric graph) or not (|stab| = 1, orbit = 2), and
Z<sub>φ</sub><sup>−½</sup> − 1 and γ<sub>φ</sub> multiply the sum of the orbit terms, so an
asymmetric graph's γ<sub>φ</sub> is the coefficient of G<sup>ij</sup> + G<sup>ji</sup>, and
γ<sub>φ</sub> = −L times the 1/ε residue of Z<sub>φ</sub><sup>−½</sup>. With every coefficient
normalised this way, each pure wave-function renormalisation — a tree-level vertex with
one self-energy S on one leg — has β equal to γ<sub>φ</sub> of S, for all 5595 of them.

Every anomalous-dimension structure is marked **symmetric** or **asymmetric**, according to
whether its graph is unchanged under exchanging the two external legs. Under **γ only** a
second row branches from it, arrows fanning out to all · symmetric · asymmetric; it opens on
all each time γ only is chosen. Of the 4229 propagator structures 818 are symmetric and 3411 asymmetric; asymmetric
ones first appear at three loops (3 of 12), and at six loops they outnumber the symmetric
3076 to 636. The registry is unoriented, so an asymmetric graph appears once and stands for
both orientations.

Every expression in the details pane can be copied as LaTeX: hover it and a **TeX**
button appears, putting the formula on the clipboard in standard syntax
(`\frac`, `\varepsilon`, `\zeta_{5,3}`, `\lambda_{ikab}`, `f^{(6)}_{2,9}`), ready to
paste into a paper.

On a phone the page becomes a single scrolling column — the list, then the graph, then its
details — with the conventions and sources behind a toggle. Tapping a structure brings its
graph into view, and the TeX buttons stay visible since there is no hover. This atlas is the
heavier of the two, a 4.2 MB download that holds about 80 MB in memory once loaded.

The graph drawings are editable: drag a vertex to place it (it stays pinned), drag a
handle to curve a line, and the layout you arrive at is kept in the browser per
structure. The filter box takes structure numbers (`V6.12`, `D5.3`, `S2.1`), graph ids
(`#431`) and coefficient names (`f_7`). Individual structures are addressable:
`…/#L6-27`.

## Conventions

d = 6 − ε and λ₀ = μ^(ε/2)(λ + Z-poles), so β̂ = −(ε/2)λ + β, and an L-loop 1/ε residue
a₁ gives β<sub>L</sub> = L·a₁. The loop factor is absorbed into the real coupling λ
— Schnetz's convention — so the one-loop β is the triangle
λ<sub>iab</sub>λ<sub>jbc</sub>λ<sub>kca</sub> with coefficient 1 (V1.1), and
γ<sub>φ</sub> = −(1/12) λ<sub>iab</sub>λ<sub>jab</sub> at one loop (S1.1).

[arXiv:2507.20761](https://arxiv.org/abs/2507.20761) uses iλ instead, which is a
relative (−1)<sup>L</sup>. With that taken into account, the two- and three-loop MS-bar
values there agree with this atlas structure by structure — all 3 + 17 vertex
structures and all 2 + 9 propagator structures.

## The data

The whole set is in [`phi3_atlas.json`](phi3_atlas.json) — 36.6 MB, 3.9 MB gzipped —
served next to the page, so it can be fetched directly:

```
curl -O https://andstergiou.github.io/phi3-graph-atlas/phi3_atlas.json
```

It holds all loop orders in one document:

| key | contents |
| --- | --- |
| `note`, `source` | conventions, provenance, licence |
| `loops`, `counts` | 1…6, and the structure counts per loop order |
| `structures` | one record each: `id`, `L`, `kind`, `num`, `edges`, `ext`, `stab`, `orbit`, `aut`, `prim`, `On`, `tensor`, `graph`, `onepi`, `vr`, `fac`, `sym`, `comp` |
| `beta`, `beta_z`, `Z_lambda` | vertex-structure expressions, keyed by structure id |
| `Zphi_minus_half`, `gamma_phi`, `gamma_phi_On` | propagator-structure expressions, keyed by structure id (`gamma_phi_On`: both orientations at O(n)) |

Expressions are sympy-readable strings in `n` and `epsilon`; `id` is unique across loop
orders and is the registry number the atlas displays. Two reducibility flags travel with each structure:
`vr` is the raw topology (the internal graph has a cut vertex), and `fac` is what the
"non-factorisable only" filter hides, so the same cut can be made on the data:
`[s for s in d['structures'] if not s['fac']]`. Propagator structures
also carry `sym`, true when the graph is symmetric under exchanging its two external legs. Every structure carries `aut`,
the |Aut| above (its symmetry factor is `1/aut`), and `prim`, the primitive flag. The file is written compact rather than
indented — at this size indenting would add 22 MB — but it parses identically.

```python
import json, sympy
d = json.load(open('phi3_atlas.json'))
v11 = next(s for s in d['structures'] if s['num'] == 'V1.1')
print(d['beta'][str(v11['id'])])                  # 1, the one-loop triangle
print(sympy.sympify(d['gamma_phi_On']['14524']))  # S1.1 at O(n): -n**2*(n - 2)/12
```

## Transcendentals: the f-alphabet

The coefficients are written in Schnetz's f-alphabet in Lyndon polynomial normal form;
`beta_z` carries the same numbers in the zeta notation. Powers of π appear directly in
both. Through six loops only these occur:

| symbol | value | first appears |
| --- | --- | --- |
| `f_3`, `f_5`, `f_7`, `f_9` | ζ(3), ζ(5), ζ(7), ζ(9) | 3, 4, 5, 6 loops |
| `f_3_5` | ζ(3)ζ(5) + ζ(5,3)/5 | 6 loops |

In `beta_z`: `z3`…`z9` are ζ(3)…ζ(9), and `z3z5` is the irreducible ζ(5,3). Only
Lyndon words appear as generators, so words like `f_3_3` are never written — the
shuffle algebra is the polynomial algebra on the Lyndon words, and `f_3_3 = f_3²/2`,
`f_5_3 = f_3 f_5 − f_3_5 = −ζ(5,3)/5`. Squares therefore appear as ordinary monomials
(`f_3**2`).

The heaviest f-word in β at L loops is weight 2L − 3: 3, 5, 7, 9 at L = 3…6. The
level-6 letters, √3, i and Period[7,11] that the φ⁴ atlas carries at seven loops do
not appear here.

## Provenance and citation

The graph ordering and the input data come from Oliver Schnetz's Maple package
[HyperlogProcedures](https://github.com/oliverschnetz/HyperlogProcedures), version 0.8.
The coefficients displayed here are not copied from the package: they are recomputed
structure by structure by tensorial minimal subtraction, in an independent Python
implementation, and checked against the published results.

The structures and coefficients were extracted from HyperlogProcedures and recomputed
with **Claude Fable 5.1**.

If you use this atlas, please cite:

- O. Schnetz, *HyperlogProcedures*, version 0.8 (2025),
  <https://github.com/oliverschnetz/HyperlogProcedures>.
- L. Benfatto and O. Zanusso, *Gradient properties of φ³ in d = 6 − ε*,
  [arXiv:2507.20761](https://arxiv.org/abs/2507.20761), for the two- and three-loop
  results this atlas is checked against.

No HyperlogProcedures code is redistributed here. The package is offered under GPL-3.0
on its repository (the 0.8 distribution itself ships no licence text); the graph
topologies shown in this atlas are re-encoded from its graph list, and the numbers
beside them are this project's own computation.

## How the page is built

The atlas page is generated from the results of the computation;
[`build.py`](build.py) is the whole of the difference between the generated file and
what is served: it adds a doctype and a UTF-8 charset, one header line giving the
provenance, a download link, and it writes the JSON export out of the page's own
inlined data. The page is otherwise self-contained — all data is inlined as JSON — and
loads only [d3](https://d3js.org/) 7.9.0 from cdnjs (ISC licence) and two families from
Google Fonts.

It is about 35 MB uncompressed, 3.9 MB over the wire.

## Licence

[CC BY 4.0](LICENSE) — reuse freely with attribution.

Andreas Stergiou
