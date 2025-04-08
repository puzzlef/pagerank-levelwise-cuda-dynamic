Design of *CUDA-based Levelwise* **Dynamic** PageRank algorithm for link analysis.

[Levelwise PageRank] is the [STIC-D algorithm], without **ICD** optimizations.
We use a rank [pull] based approach, and perform the computation upon the [CSR]
representation of a graph. We skip the computation of common teleport
contribution to all the vertices in the graph by simply adding self-loops to all
the vertices ([skip-teleport]). We process each component in a switched
thread/block-per-vertex fashion, with the vertices partitioned by in-degree. If
the size of a component is fewer than 5 million vertices, we process multiple
components together ([compute-5M]) using the switched approach. To take into
account removed/added vertices upon the dynamic graph, we scale the previous
ranks using the [scaled-fill] approach.

We attempt each experiment (mentioned below) on different types of graphs,
running each with multiple batch sizes (`1`, `5`, `10`, `50`, ...). Each
pagerank computation was run 5 times for both approaches to get a good time
measure. The input data used for each experiment is available at ["graphs"] (for
small ones), and the [SuiteSparse Matrix Collection]. Experiments were done with
guidance from [Prof. Dip Sankar Banerjee] and [Prof. Kishore Kothapalli].

<br>


### Comparison on fixed graph with random edge insertions

In this experiment ([with-mtx-insertions]), we compare the performance of
*static* and *dynamic* approaches of CUDA-based *Levelwise* PageRank, with
*Monolithic* and *nvGraph* PageRank. Indeed, *dynamic Levelwise PageTank* is
*faster* than the static approach for most batch sizes. In order to measure
error, we take nvGraph pagerank as a reference.

[with-mtx-insertions]: https://github.com/puzzlef/pagerank-levelwise-cuda-dynamic/tree/with-mtx-insertions

<br>
<br>


## References

- [STIC-D: algorithmic techniques for efficient parallel pagerank computation on real-world graphs][STIC-D algorithm]
- [PageRank Algorithm, Mining massive Datasets (CS246), Stanford University](https://www.youtube.com/watch?v=ke9g8hB0MEo)
- [SuiteSparse Matrix Collection]
- [Merge git repo into branch of another repo](https://stackoverflow.com/a/21353836/1413259)

<br>
<br>


[![](https://img.youtube.com/vi/SoiKp2oSUl0/maxresdefault.jpg)](https://www.youtube.com/watch?v=SoiKp2oSUl0)
![](https://ga-beacon.deno.dev/G-KD28SG54JQ:hbAybl6nQFOtmVxW4if3xw/github.com/puzzlef/pagerank-levelwise-cuda-dynamic)

[Prof. Dip Sankar Banerjee]: https://sites.google.com/site/dipsankarban/
[Prof. Kishore Kothapalli]: https://faculty.iiit.ac.in/~kkishore/
[Levelwise PageRank]: https://ieeexplore.ieee.org/abstract/document/9835216/
[STIC-D algorithm]: https://dl.acm.org/doi/abs/10.1145/2833312.2833322
[SuiteSparse Matrix Collection]: https://sparse.tamu.edu/
["graphs"]: https://github.com/puzzlef/graphs
[pull]: https://github.com/puzzlef/pagerank
[CSR]: https://github.com/puzzlef/pagerank
[skip-teleport]: https://github.com/puzzlef/pagerank-levelwise
[compute-5M]: https://github.com/puzzlef/pagerank-levelwise-cuda
[scaled-fill]: https://github.com/puzzlef/pagerank-dynamic
[charts]: https://photos.app.goo.gl/7zTbHBXV6uh7FGyd8
[sheets]: https://docs.google.com/spreadsheets/d/1TPFX5al0-rlSde0xr7zlfCHNYEqxXSfS6P8QIa2dDsA/edit?usp=sharing
