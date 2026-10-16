# Data dictionary

Local evidence: `data/ConsuAdop_Codebook.pdf` (pp. 1–2), `data/Proccessed_data_CSV.csv`, and the checked-in TMDL definitions. The local `data/` directory is required to download.

The dataset is the Mendeley Brufonctionnel survey (Dethier et al., 2023), [V1 DOI](https://doi.org/10.17632/4n48pfcycx.1). Meanings below paraphrase the codebook; “valid values” means documented coding, not a Power BI validation constraint. Observed exceptions are retained. `int64` means whole number, `double` decimal number, `string` text. All 33 CSV columns are listed individually.

## Original source columns

| Field | Meaning | Status | Model type | Codebook values / scale | Limitations and observed differences |
|---|---|---|---|---|---|
| `id` | Survey-software respondent identifier | Source | `int64` | Unrestricted discrete identifier | 797 distinct IDs in 816 rows; not a unique fact key. |
| `startlanguage` | Survey language | Source | `string` | Codebook: 1 French; 2 Dutch; 3 English | CSV stores French / Dutch / English text; no recoding step in this model. |
| `AGE` | Respondent age in years | Source | `int64` | Years; no codebook bounds | Observed 17–81; codebook calls this continuous, model stores whole numbers. |
| `SEX` | Respondent sex/gender question | Source | `string` | Codebook: 0 Male; 1 Female | CSV stores Male / Female text; source is binary-coded. |
| `PROF` | Professional category | Source | `int64` | 1 Student; 2 Employed; 3 Self-employed; 4 Unemployed; 5 Retired; 6 Other (including stay-at-home parent) | Nominal codes, not a quantity. |
| `INC` | Household net monthly income bracket | Source | `int64` | 1 < EUR 1,000; 2 [1,000,2,000); 3 [2,000,3,000); 4 [3,000,4,000); 5 [4,000,5,000); 6 [5,000,6,000); 7 >=6,000 | Observed codes 1–5 only. Do not reinterpret 5 as the highest open-ended bracket; upstream recoding, if any, is undocumented. |
| `EDU` | Highest diploma / education category | Source | `int64` | 1 Primary school; 2 Junior high school; 3 Senior high school; 4 Bachelor’s degree; 5 Master’s degree | Observed 1–7. Codes 6 and 7 are undocumented; neither is interpreted as higher attainment. |
| `DIFF` | Survey recruitment / diffusion channel | Source | `int64` | 1 LinkedIn; 2 Facebook; 3 Circle.made; 4 ICHEC Brussels Management School; 5 survey company; 6 Brufonctionnel team; 7 ICHEC Courses; 8 Synhera; 9 word of mouth; 10 flyers; 11 others | Six empty CSV cells; not replaced by a fabricated category. |
| `ITEM1` | Buying things rarely or never used | Source | `int64` | 1–7 Likert: disagree → agree | Individual ordinal item; no composite score or reverse coding implemented. |
| `ITEM2` | Preference for having items available despite infrequent use | Source | `int64` | 1–7 Likert: disagree → agree | Individual ordinal item; no composite score or reverse coding implemented. |
| `ITEM3` | Rejection of possessions as a sign of success | Source | `int64` | 1–7 Likert: disagree → agree | Individual ordinal item; no composite score or reverse coding implemented. |
| `ITEM4` | Low importance attached to owned possessions | Source | `int64` | 1–7 Likert: disagree → agree | Individual ordinal item; no composite score or reverse coding implemented. |
| `ITEM5` | Having the things needed to enjoy life | Source | `int64` | 1–7 Likert: disagree → agree | Individual ordinal item; no composite score or reverse coding implemented. |
| `ITEM6` | Not expecting nicer possessions to increase happiness | Source | `int64` | 1–7 Likert: disagree → agree | Individual ordinal item; no composite score or reverse coding implemented. |
| `ITEM7` | Reaction to environmental problems in TV/newspapers | Source | `int64` | 1–7 Likert: disagree → agree | Codebook question is incomplete (ends “I am often”); no missing wording inferred. |
| `ITEM8` | Belief that industrialized economies have reached or will soon reach growth limits | Source | `int64` | 1–7 Likert: disagree → agree | Individual ordinal item; no composite score or reverse coding implemented. |
| `ITEM9` | Willingness to reduce living standards to protect the environment | Source | `int64` | 1–7 Likert: disagree → agree | Individual ordinal item; no composite score or reverse coding implemented. |
| `ITEM10` | Self-reported life changes for ecological reasons | Source | `int64` | 1–7 Likert: disagree → agree | Individual ordinal item; no composite score or reverse coding implemented. |
| `AREA` | Assigned area of need, based on birth four-month period | Source | `string` | Codebook: 1 Mobility; 2 Clothing; 3 Tooling | CSV stores sector names. Although codebook labels AREA ordinal, this report treats sectors as categories, not ranks. |
| `KNOW` | Prior awareness of this type of SPSS offer | Source | `int64` | 1–7 Likert: disagree → agree | Ordinal agreement item; not causal evidence. |
| `EXPE` | Prior experience testing this type of SPSS offer | Source | `int64` | 1–7 Likert: disagree → agree | Ordinal agreement item; not causal evidence. |
| `TRUST` | Trust that others take care of items | Source | `int64` | 1–7 Likert: disagree → agree | Ordinal agreement item; not causal evidence. |
| `FIN` | Perceived financial advantage over buying a new item | Source | `double` | 1–7 Likert: disagree → agree | Codebook describes 1–7 ordinal responses; CSV has 13 values in 0.5 increments, including 97 non-integer responses. Origin is unexplained; model preserves double precision. |
| `CLEAN` | Appreciation of provider-managed cleaning/repair for cleanliness and safety | Source | `int64` | 1–7 Likert: disagree → agree | Ordinal agreement item; not causal evidence. |
| `REPAIR` | Appreciation of provider-managed maintenance | Source | `int64` | 1–7 Likert: disagree → agree | Ordinal agreement item; not causal evidence. |
| `SPACE` | Appreciation of avoiding item accumulation / saving storage space | Source | `int64` | 1–7 Likert: disagree → agree | Ordinal agreement item; not causal evidence. |
| `QUAL` | Perceived access to high-quality items | Source | `int64` | 1–7 Likert: disagree → agree | Ordinal agreement item; not causal evidence. |
| `AVAIL` | Concern that an item will be unavailable when needed | Source | `int64` | 1–7 Likert: disagree → agree | Ordinal agreement item; not causal evidence. |
| `MODIF` | Dislike of being unable to customize an item not owned | Source | `int64` | 1–7 Likert: disagree → agree | Ordinal agreement item; not causal evidence. |
| `W_R` | Perceived burden of item collection and return | Source | `int64` | 1–7 Likert: disagree → agree | Ordinal agreement item; not causal evidence. |
| `LT` | Dislike of long-term commitment to the provider | Source | `int64` | 1–7 Likert: disagree → agree | Ordinal agreement item; not causal evidence. |
| `SUB` | Dislike of a fixed monthly rental fee regardless of use | Source | `int64` | 1–7 Likert: disagree → agree | Ordinal agreement item; not causal evidence. |
| `VD1` | Intention to subscribe if the hypothetical offer existed | Source | `int64` | 1–7 Likert: disagree → agree | Stated intention, not observed adoption or a subscription transaction. |

## Model-derived fields

| Field | Meaning / origin | Model type | Values and limitations |
|---|---|---|---|
| `Proccessed_data_CSV[ObservationID]` | Power Query index, starting at 1, increment 1 | Explicit `int64` | 1–816 for the current source order; hidden. Not a deduplicated person key or stable source key. |
| `Proccessed_data_CSV[Intention Band]` | DAX grouping of VD1 | Inferred text; TMDL omits explicit type | Low (1-3), Neutral (4), High (5-7); blank VD1 returns blank. Production expression uses <=3 and >=5 without outer bounds, so labels do not enforce valid input ranges. |
| `Proccessed_data_CSV[Intention Band Sort]` | DAX band ordering | Inferred whole number; format `0` | 1 for VD1 1–3, 2 for 4, 3 for 5–7; blank otherwise. Sorted-band label uses this field. |
| `DimSector[AREA]` | Distinct fact AREA values, Power Query | Explicit `string` | Clothing, Mobility, Tooling; dimension join key. |
| `DimEducation[EDU]` | Distinct fact EDU values, Power Query | Explicit `int64` | 1–7 currently; dimension join key. |
| `DimEducation[Education Level]` | DAX code-to-label mapping | Inferred text; TMDL omits explicit type | Documented labels for 1–5; other nonblank codes become `Undocumented (code)`; blank becomes `Missing`. Sorted by EDU. |
| `Perception Selector[Perception Selector]` | Calculated Field Parameter display label | Inferred text | Financial advantage, Trust, Subscription dislike, Items unavailability. Grouped by the Fields column. |
| `Perception Selector[Perception Selector Fields]` | Calculated NAMEOF column references | Inferred text | Fact FIN, TRUST, SUB, AVAIL; hidden; ParameterMetadata kind 2. |
| `Perception Selector[Perception Selector Order]` | Calculated parameter sort key | Inferred whole number; format `0` | 0–3; hidden. Not an analytical score. |

