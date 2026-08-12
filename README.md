# ProdPack

> [!IMPORTANT]
> **ProdPack has been superseded by [DEAPack 2](https://github.com/daopingw/DEAPack).**
> The productivity-analysis work that began here and the efficiency-analysis
> work in the original DEAPack are now developed together in one maintained
> package. New users and new research projects should use DEAPack.

[![DEAPack on PyPI](https://img.shields.io/pypi/v/DEAPack.svg)](https://pypi.org/project/DEAPack/)
[![DEAPack Documentation](https://readthedocs.org/projects/deapack/badge/?version=latest)](https://deapack.readthedocs.io/)
[![DEAPack downloads](https://api.pepy.tech/badge/deapack)](https://pepy.tech/projects/deapack)

## Why the projects were combined

Efficiency measurement and productivity analysis are closely connected: a
productivity study repeatedly estimates production frontiers, distances, and
changes in operating performance. Maintaining them in separate packages made
data preparation, model assumptions, result formats, and documentation harder
to keep consistent.

DEAPack 2 provides one framework for:

- classical DEA efficiency models, including CCR, BCC, FDH, additive, SBM,
  EBM, and directional approaches;
- Malmquist-family, Luenberger, Hicks--Moorsteen, global, biennial, and
  environmental productivity analysis;
- economic, environmental, network, dynamic, panel, and metafrontier models;
- consistent data validation and structured score, target, slack, peer,
  component, and diagnostic results; and
- visualization, reporting, and reproducible research outputs.

The maintained project is available at:

- **Package:** [DEAPack on PyPI](https://pypi.org/project/DEAPack/)
- **Documentation:** [deapack.readthedocs.io](https://deapack.readthedocs.io/)
- **Source and issues:** [github.com/daopingw/DEAPack](https://github.com/daopingw/DEAPack)
- **Productivity methods:** [Productivity analysis guide](https://deapack.readthedocs.io/en/latest/reference/productivity-analysis.html)
- **Moving old code:** [DEAPack and ProdPack migration guide](https://deapack.readthedocs.io/en/latest/getting-started/migration.html)

## Start with DEAPack

Install the maintained package from PyPI:

```bash
python -m pip install --upgrade DEAPack
```

A current productivity workflow uses the same explicit data and result
contracts as the rest of DEAPack:

```python
from deapack import DEAData, FGNZMalmquist, dataset_info, load_dataset

dataset = "productivity_panel"
frame = load_dataset(dataset)
roles = dataset_info(dataset).roles

data = DEAData.from_frame(
    frame,
    dmu=roles["dmu"],
    period=roles["period"],
    inputs=roles["inputs"],
    outputs=roles["outputs"],
)

result = FGNZMalmquist().fit(data)
print(
    result.summary()[
        [
            "dmu_id",
            "period",
            "productivity_change",
            "efficiency_change",
            "technical_change",
            "score_valid",
        ]
    ]
)
```

See the [DEAPack quickstart](https://deapack.readthedocs.io/en/latest/getting-started/quickstart.html)
for the common `data -> model.fit(data) -> result` workflow and the
[method catalog](https://deapack.readthedocs.io/en/latest/user-guide/method-catalog.html)
for the maintained method inventory.

## Existing ProdPack projects

ProdPack remains here as a historical research-software record. Existing
releases may still be used when reproducing an earlier analysis, but this
repository is not the development home for new functionality or fixes.

DEAPack 2 is a redesign rather than a drop-in rename. Old scripts using
mutable `ProdNP` objects, assigned `x_vars`/`y_vars`/`b_vars`, `ref_type`, and
`solve()` should be migrated by first recording their empirical assumptions
and then selecting the corresponding maintained DEAPack model. Do not assume
that changing imports alone preserves the estimated quantity.

For migration questions, bug reports, or method proposals, please use the
[DEAPack issue tracker](https://github.com/daopingw/DEAPack/issues).
