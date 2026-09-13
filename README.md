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
- the stabiliser and orbit size of the graph's symmetry,
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

Every expression in the details pane can be copied as LaTeX: hover it and a **TeX**
button appears, putting the formula on the clipboard in standard syntax
(`\frac`, `\varepsilon`, `\zeta_{5,3}`, `\lambda_{ikab}`, `f^{(6)}_{2,9}`), ready to
paste into a paper.

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

The whole set is in [`phi3_atlas.json`](phi3_atlas.json) — 35.5 MB, 3.7 MB gzipped —
served next to the page, so it can be fetched directly:

```
curl -O https://andstergiou.github.io/phi3-graph-atlas/phi3_atlas.json
```

It follows the shape of the project's `renorm3_L*.json` files, with all loop orders in
one document:

| key | contents |
| --- | --- |
| `note`, `source` | conventions, provenance, licence |
| `loops`, `counts` | 1…6, and the structure counts per loop order |
| `structures` | one record each: `id`, `L`, `kind`, `num`, `edges`, `ext`, `stab`, `orbit`, `On`, `tensor`, `graph`, `onepi`, `vr`, `fac`, `comp` |
| `beta`, `beta_z`, `Z_lambda` | vertex-structure expressions, keyed by structure id |
| `Zphi_minus_half`, `gamma_phi`, `gamma_phi_On` | propagator-structure expressions, keyed by structure id |

Expressions are sympy-readable strings in `n` and `epsilon`; `id` is unique across loop
orders and is the registry number the atlas displays. Two reducibility flags travel with each structure:
`vr` is the raw topology (the internal graph has a cut vertex), and `fac` is what the
"non-factorisable only" filter hides, so the same cut can be made on the data:
`[s for s in d['structures'] if not s['fac']]`. The file is written compact rather than
indented — at this size indenting would add 22 MB — but it parses identically.

Every expression agrees with the project's `renorm3_L1…L6.json`: 30979 `beta`, 30979
`Z_lambda` and 4229 `gamma_phi`, plus all 35208 edge lists and O(n) values, checked
term for term.

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

The atlas is generated in the research repository, then copied here:

```
python schnetz/extracted/graph_viewer.py 6 --phi3   # -> schnetz/extracted_results/graph_atlas3.html
python build.py                                     # -> index.html + phi3_atlas.json
```

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
