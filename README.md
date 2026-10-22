# condition-findings

An index of open, machine-extracted research findings from the literature on POTS, dysautonomia, Ehlers-Danlos
syndromes and related conditions, and of the method used to build them. Each finding is one extracted statement
from one paper with its verbatim source quote, so every row can be checked against the paper it came from.

This is research information extracted by software, not medical advice. Read and cite the original paper before
relying on any finding.

## Repositories

| repository | what it is | size |
|---|---|---|
| [pots-findings](https://github.com/erinmagennis/pots-findings) | POTS, dysautonomia and related condition literatures (ME/CFS, long COVID, EDS and hypermobility, fibromyalgia, MCAS, small fiber neuropathy, autism, migraine, IBS and others), 2019 to 2026. Five data packages and a public browser at [pots.erinmagennis.com](https://pots.erinmagennis.com). | 148,186 findings from 11,519 papers |
| [eds-findings](https://github.com/erinmagennis/eds-findings) | Ehlers-Danlos syndromes and hypermobility spectrum disorder, papers published 1946 to 2026, with the diagnostic era recorded on every row. Four data packages. | 24,200 findings from 3,558 papers |
| [condition-findings-builder](https://github.com/erinmagennis/condition-findings-builder) | The method: retrieval, screening, extraction, identifier resolution, quality checks with negative controls, packaging and verification. One config file per condition area. | code and protocols, no data |

The two datasets share a schema and a provenance standard but are separate corpora with different scope, time span
and screening. They are not merged into one table.

## How the findings were built

1. Papers were retrieved from Europe PMC (and, for pre-2019 EDS papers without an abstract, OpenAlex) and screened for scope.
2. A language model read each paper (full text where available, otherwise the abstract) and wrote one row per finding:
   the statement, the verbatim quote it rests on, direction, evidence tier, condition label, and the entity named.
3. Entity names were looked up at their authorities (HGNC, ChEBI, MeSH, UniProt, HPO, UBERON, Cell Ontology, NCBI
   Taxonomy). A name that did not match a label or synonym was left without an identifier, never guessed.
4. Every package was checked by machine: quotes traced to freshly fetched source text with wrong-paper negative
   controls, counts conserved, packages rebuilt byte-identically, a verifier shipped inside each package.

## Verification status

| check | POTS | EDS |
|---|---|---|
| quotes found in source text | 96.0% of re-fetchable quotes, Tiers 1 to 3 (127,041 of 132,295); 185 of 200 in a fresh-fetch sample | 99.6% in a fresh-fetch census of 1,420 pre-2019 rows (1,414 found), wrong-paper control 0 of 400 |
| entity identifiers | every model-written identifier looked up at its authority in v1.2; 19,782 rows carry a verified identifier, 2,607 were withheld | derived from names by authority lookup from the start; unmatched names left blank |
| extraction tier vs publication type | 0.97% hard mismatches | 1.15% hard mismatches |
| does each finding state what its paper found | not yet checked by a human reader | not yet checked by a human reader |

The last row is the one that matters most and it is open. Fidelity samples of 200 findings per corpus, with
worksheets, sit in each repository under `audits/`. Until they are read, treat the findings as leads to the papers,
not as established results.

## How to cite

Cite the dataset repository and version you used (each package carries a `CITATION.cff`), and for any finding that
matters to your work, cite the source paper. Derived structured data is CC BY 4.0; verbatim quotes remain the
copyright of their authors and publishers. The method code is MIT.

Credit: Erin Magennis.
