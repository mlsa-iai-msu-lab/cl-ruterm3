# CL-RuTerm3 1.1

CL-RuTerm3 is a Russian dataset of scientific texts for automatic term extraction and classification, developed for the RuTermEval-2024 shared task as part of the Dialogue 2025 conference ([original platform](https://codalab.lisn.upsaclay.fr/competitions/19601), [current platform](https://www.codabench.org/competitions/15972/)).
The annotations include nested and partially overlapping terms.

Version **1.1** combines the shared task data into `train`, `dev`, and `test` splits.
The training and development sets cover computational linguistics. The test set
covers all six domains: computational linguistics, literature studies,
agrochemistry, medicine, mathematics, and economics. This supports both evaluation
within the training domain and experiments on transfer to other domains.

**Full-text articles are temporarily excluded and will be added separately.**

## Splits

| Split | Documents | Term occurrences | Source |
|---|---:|---:|---|
| `train` | 850 | 17,802 | Shared task training set |
| `dev` | 103 | 2,277 | Initial test set of Tracks 1 and 2 |
| `test` | 317 | 11,547 | Both test sets of Track 3 and the final test set of Tracks 1 and 2 |
| **Total** | **1,270** | **31,626** | |

These counts correspond to version 1.1, commit
[`1aaa1e8`](https://github.com/mlsa-iai-msu-lab/cl-ruterm3/tree/1aaa1e841cc1a077abe22ad9f56154f63fb6ad00).
Each use of a term at a different position counts as a separate occurrence.

## Files and annotation format

The files are stored in `data/` as UTF-8 JSONL.

- `train.jsonl` — training texts and annotations.
- `dev.jsonl`, `dev_ref.jsonl` — development texts and gold annotations.
- `test.jsonl` — test texts.
- `test_ref_v4.jsonl` — test texts, domain codes, and gold annotations.

Match texts and annotations **by `id`**, as the row order differs between files.
The `label` field contains `[start, end, class]` triples. Offsets are zero-based
Unicode character indices into `text`, with an inclusive start and exclusive end
(`text[start:end]` in Python).

Classes:

- `specific` — a term that is both domain-specific and lexically specific.
- `common` — a domain term also familiar to non-specialists.
- `nomen` — a unique name of an object belonging to the domain.

Preserve nested and overlapping spans during processing. Use `dev` for model
tuning and `test` for final evaluation; report results for each domain and for
the combined test set.


## License and Third-Party Content

The original term annotations, annotation guidelines, and other original documentation developed for the CL-RuTerm3 dataset are licensed under the [**Creative Commons Attribution 4.0 International (CC BY 4.0)** license](https://creativecommons.org/licenses/by/4.0/).

**This license does not extend to the underlying scientific articles, article abstracts, or other third-party content.**

Copyright in the original scientific texts remains with their respective authors, publishers, or other rights holders. Such materials are governed by their original licenses or separately obtained permissions.

## Citation

When using the dataset, cite the paper describing the original resource:
[Mamontova, Ischenko, Vorontsov (2025)](https://dialogue-conf.org/wp-content/uploads/2025/04/MamontovaAIschenkoRVorontsovK.pdf).

```bibtex
@inproceedings{mamontova2025rutermeval,
  author = {Mamontova, Angelina and Ischenko, Roman and Vorontsov, Konstantin},
  title = {{RuTermEval-2024}: Cross-domain Automatic Term Extraction and Classification in Russian scientific texts},
  booktitle = {Computational Linguistics and Intellectual Technologies: Proceedings of the International Conference {Dialogue 2025}},
  year = {2025},
  pages = {245–256},
  doi = {10.28995/2075-7182-2025-23-245-256}
}
```

