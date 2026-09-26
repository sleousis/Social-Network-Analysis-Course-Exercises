# Social Network Analysis Course Exercises

Lab exercises for the Social Network Analysis course (Ανάλυση Κοινωνικών Δικτύων) of the School of Electrical and Computer Engineering at NTUA, 9th semester, academic year 2018-2019. Each lab is a Jupyter notebook in Python that uses NetworkX to build, study and compare synthetic and real network topologies. The notebooks and their comments are written in Greek.

## Contents

| Folder | Topic |
| --- | --- |
| `Lab 1` | Complex network topologies. Builds regular lattice (REG), Erdos-Renyi (RG), random geometric (RGG), Barabasi-Albert scale-free (SF) and Watts-Strogatz small-world (SW) graphs. Studies degree distribution, clustering, path lengths and centralities, including ego betweenness. Also holds the course NetworkX tutorials (`demo.ipynb`, `short_demo.ipynb`). |
| `Lab 2` | Social structure in synthetic and real networks. Uses the American College Football, Les Miserables and Dolphins networks. Compares degree, clustering and ego betweenness, and detects communities with Girvan-Newman, spectral clustering and greedy modularity maximization. |
| `Lab 3` | Genetic algorithms and epidemic models. Solves ONEMAX with a genetic algorithm, detects communities with a genetic algorithm and compares it with the Lab 2 methods, and solves the SIR and SIS models numerically. |

Each folder also has the assignment PDF (in Greek) from the course staff.

## Tech stack

- Python 3.14.7 with Jupyter (nbconvert 7.17.1, ipykernel 7.3.0)
- NetworkX 3.7, NumPy 2.5.3, SciPy 1.18.1, pandas 3.0.6, Matplotlib 3.11.2, seaborn 0.13.2, scikit-learn 1.9.1

All versions are pinned in `requirements.txt` and were the latest on PyPI in September 2026.

## Repository layout

```
Lab 1/
  Leousis-Savvas-03114945-lab1.ipynb   solution notebook
  demo.ipynb, short_demo.ipynb         NetworkX tutorials from the course
  *.pdf                                assignment and lab slides
Lab 2/
  Leousis-Savvas-03114945-lab2.ipynb   solution notebook
  dolphins.gml, football.gml, lesmis.gml
  *.pdf                                assignment
Lab 3/
  Leousis-Savvas-03114945-lab3.ipynb   solution notebook
  dolphins.gml, football.gml, lesmis.gml
  SNA-lab-3-2018.pdf                   assignment
requirements.txt                       pinned Python packages
```

The `.gml` files are from Mark Newman's network data page. Some PDF file names show garbled characters. They were Greek names saved in an old encoding.

## Prerequisites

- Python 3.14.7 (the latest stable release in September 2026). It was tested on Windows 11.

## Setup

Windows (PowerShell):

```
py -3.14 -m venv .venv
.venv\Scripts\python -m pip install -r requirements.txt
```

If the `py` launcher has no 3.14, use the full path to any Python 3.14 interpreter instead, for example one installed with `uv python install 3.14`.

Linux (not tested, only the Windows commands were run):

```
python3.14 -m venv .venv
.venv/bin/python -m pip install -r requirements.txt
```

## Running

Open the notebooks interactively:

```
.venv\Scripts\jupyter notebook        # Windows
.venv/bin/jupyter notebook            # Linux
```

Run a notebook headless from inside its folder, so the `.gml` files are found. Example for Lab 2 on Windows:

```
cd "Lab 2"
..\.venv\Scripts\jupyter nbconvert --to notebook --execute --ExecutePreprocessor.timeout=3600 --output-dir ..\out Leousis-Savvas-03114945-lab2.ipynb
```

On Linux use `../.venv/bin/jupyter` and `../out` instead.

## Example output

The notebooks draw each topology, plot degree and clustering distributions, show seaborn pair plots of centralities, and color the detected communities. Lab 3 prints a comparison table like this one:

```
American College Football
Girvan-Newman: 17 communities with modularity score 0.9581998474446987
Spectral Clustering: 18 communities with modularity score 0.9583524027459954
Modularity Maximization: 6 communities with modularity score 0.8681922196796339
Genetic Algorithm: ...
```

## Notes and known limitations

- The notebooks were written in 2018-2019 for Python 3.7 and NetworkX 2.x. They were updated only where the current library versions raised errors:
  - `nx.algorithms.community.quality.performance(G, p)` became `partition_quality(G, p)[1]`, which returns the same value.
  - `nx.to_numpy_matrix` became `nx.to_numpy_array`.
  - In Lab 3, `ax.grid(b=True, ...)` became `ax.grid(visible=True, ...)` for current Matplotlib.
  - In the tutorials, `G.node` became `G.nodes`, `nx.info(G)` became `print(G)`, `random_lobster` became `random_lobster_graph`, `biconnected_component_subgraphs` was replaced with subgraphs of `biconnected_components`, a Python 2 `print` statement got parentheses, and an `edge_list` typo became `edgelist`.
  - In Lab 1 the ego betweenness data frame is rounded to 12 decimals. The REG graph gives equal values that differ only by floating point noise, and current seaborn cannot build histogram bins for such a tiny range.
- The value called "modularity" in Labs 2 and 3 is the NetworkX partition performance metric, as in the original code.
- The graphs and the genetic algorithm are random with no fixed seed, so every run gives slightly different figures and numbers from the saved outputs.
- The saved outputs in the notebooks are the original ones from 2018-2019.
- Lab 2 (Girvan-Newman on all graphs) and Lab 3 (genetic algorithm parameter search) take several minutes each to run.

## Author

Savvas Leousis (Λεούσης Σάββας), NTUA student ID 03114945.
