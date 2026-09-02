# Puzzle-Generation Resources

Datasets and compendiums useful for generating Word Tree: Associations levels.
The ✅ rows are integrated into the tool via `norms.js` (rebuild it with
`tools/build_norms.py`); the rest are documented for future use.

## Integrated (feed `norms.js`)

| Resource | What it is | How the tool uses it |
|---|---|---|
| ✅ [Norvig `count_1w.txt`](https://norvig.com/ngrams/count_1w.txt) | 333K English words ranked by Google-ngram frequency | Top 60K ranks back the **familiarity gate**: words outside the selected 6K/30K tier get flagged in the norms check |
| ✅ [USF Free Association Norms](http://w3.usf.edu/FreeAssociation/) ([mirror](https://github.com/teonbrooks/free_association)) | 72K cue→target pairs with association strength, from ~6,000 human participants | Pairs with strength ≥ 0.10 back the **ambiguity scan**: a generated word that pulls harder toward another branch than its own parent gets flagged |
| ✅ [NYT Connections answer archive](https://github.com/Eyefyre/NYT-Connections-Answers) | Every Connections puzzle as JSON, with per-group difficulty levels | ~1,900 wordplay-filtered categories are sampled into the **prompt as difficulty-calibrated reference examples** (easy=yellow, medium=green, hard=blue groups) |
| ✅ Curated theme pool (in `tools/build_norms.py`) | ~100 themes in the style of the Battig–Montague category norms and Scattergories lists | The **🎲 random-theme button** next to the Theme Hint field |

## Worth adding later

- **[Small World of Words (SWOW)](https://smallworldofwords.org/en/project/research)** — the largest modern association dataset (12,000+ cues). Requires a manual, non-commercial research download (form + license), which is why the smaller public-mirror USF norms are integrated instead. Swapping SWOW in would roughly double the ambiguity scan's vocabulary coverage. See the [SWOW paper](https://link.springer.com/article/10.3758/s13428-018-1115-7).
- **[Brysbaert combined norms (OSF)](https://osf.io/6kauf)** — concreteness (40K words), age-of-acquisition, familiarity ratings. Age-of-acquisition is a better "kids difficulty" signal than raw frequency.
- **[Battig & Montague category norms](https://rdrr.io/cran/WordPools/man/Battig.html)** ([2004 update](https://www.semanticscholar.org/paper/2a91c755a410fc5c4ba908d4e5ad5cb1417dc927)) — canonical category→member response frequencies; would let the tool verify that easy-tier members are actually canonical.
- **[Buchanan semantic feature norms](https://link.springer.com/article/10.3758/s13428-019-01243-z)** — 4,436 concepts with human-listed features; raw material for whole→part branches.
- **[Only Connect Wall dataset](https://github.com/TaatiTeam/OCW)** — puzzles designed around deliberate red herrings; good negative examples for prompt-tuning ambiguity avoidance.
- **[Words-CEFR dataset](https://github.com/Maximax67/Words-CEFR-Dataset)** / [Dolch–Fry lists](https://www.k12reader.com/subject/vocabulary/fry-words/) — graded vocabulary for a future kids mode.
- **WordNet / ConceptNet** — machine-readable hypernym hierarchies (FOOD→FRUIT→APPLE); see [automated word-puzzle generation via topic dictionaries](https://arxiv.org/pdf/1206.0377).

## Rebuilding norms.js

```bash
curl -sL -o /tmp/count_1w.txt https://norvig.com/ngrams/count_1w.txt
curl -sL -o /tmp/usf_free_association.txt https://raw.githubusercontent.com/teonbrooks/free_association/master/free/free_association.txt
curl -sL -o /tmp/connections.json https://raw.githubusercontent.com/Eyefyre/NYT-Connections-Answers/main/connections.json
python3 tools/build_norms.py /tmp norms.js
```
