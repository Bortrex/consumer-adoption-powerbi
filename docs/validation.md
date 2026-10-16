# Validation record

## Independently reproduced source checks

| Check | Result | Method / interpretation |
|---|---:|---|
| Original columns | 33 | CSV header count |
| Observations | 816 | Data records, not unique respondents |
| Distinct source IDs | 797 | Distinct id |
| IDs appearing exactly once | 778 | IDs with frequency 1 |
| IDs appearing twice | 19 | 38 rows; 778 + 38 = 816 |
| Unique ObservationID values | 816 | Reproduced M index 1–816; live imported column not queried |
| Clothing observations / high count | 265 / 55 | AREA grouping; high = VD1 5–7 |
| Mobility observations / high count | 255 / 86 | Same check |
| Tooling observations / high count | 296 / 93 | Same check |
| High-intention observations | 234 | VD1 5–7; >=5 alone agrees here |
| Overall high intention | 28.7% | 234/816 = 28.6764706%, rounded |
| VD1 domain / missing | 1–7 / 0 | All seven integer scores; no empty values |
| FIN values | 13 distinct; 97 half-point rows | 1–7, increments of 0.5 |
| EDU=6 / EDU=7 | 37 / 59 | Retained without invented labels |
| DIFF missing | 6 | Empty CSV cells |
| Mean VD1 | 3.4142156863 | Displayed as 3.41 |

Generated ObservationID uniqueness is a consequence of indexing all rows, not source-ID deduplication.

## Cross-dimensional reconciliation

The matrix groups `DimEducation[Education Level]` by `DimSector[AREA]` with the existing Survey Observations, High Intention % and High Intention Count measures. Display aliases Observations / High % / High Count do not rename the measures.

Each cell below is **observations / high-intention count**, independently grouped from the CSV. Cell percentages divide the high count by that cell's observation count.

| EDU | Clothing | Mobility | Tooling | All sectors | All-sector High % |
|---|---:|---:|---:|---:|---:|
| 1 | 33 / 4 | 26 / 3 | 38 / 10 | 97 / 17 | 17.5% |
| 2 | 55 / 20 | 58 / 11 | 74 / 19 | 187 / 50 | 26.7% |
| 3 | 84 / 14 | 56 / 14 | 69 / 18 | 209 / 46 | 22.0% |
| 4 | 39 / 7 | 42 / 20 | 46 / 12 | 127 / 39 | 30.7% |
| 5 | 23 / 7 | 46 / 27 | 31 / 17 | 100 / 51 | 51.0% |
| 6 | 10 / 1 | 11 / 8 | 16 / 8 | 37 / 17 | 45.9% |
| 7 | 21 / 2 | 16 / 3 | 22 / 9 | 59 / 14 | 23.7% |
| **Total** | **265 / 55** | **255 / 86** | **296 / 93** | **816 / 234** | **28.7%** |

Sector percentages: Clothing 20.8%, Mobility 33.7%, Tooling 31.4%. Summing education counts gives sector totals; summing sector counts gives the grand total. The total percentage is 234/816, not an average or sum of the displayed percentages. Dimension filters intersect in fact context.

PBIR inspection confirms all three measure bindings. The blue background rule targets only High Intention %, uses actual measure values with a fixed 0–1 scale, and uses an instances-only selector to exclude totals. It is a descriptive encoding, not a significance test. No analytical results are hard-coded into report cells.

## Unresolved data-quality issues

- The cause of repeated source IDs is unknown. ObservationID provides technical row identification, not proof of respondent independence.
- EDU 6 and 7 lack codebook definitions.
- FIN half-points exist in the CSV. Neither the codebook nor current Power Query explains averaging or other upstream processing.
- Language, sex and sector use text versus numeric codebook codes. INC only contains 1–5 despite seven documented brackets.
- ITEM7's codebook question is incomplete. Missing wording is not reconstructed.
- Hypothetical subscription intention is not actual adoption.

