# DAX measures

The five expressions below are extracted from current TMDL.

## Survey Observations

Table: `Proccessed_data_CSV`. Format: `0`.

```dax
COUNTROWS('Proccessed_data_CSV')
```

**Purpose, logic and filter context:** Counts fact rows, including repeated source IDs. COUNTROWS uses current filter context; dimension filters and visual groupings restrict rows. It does not count distinct people.

**Verified / expected result:** 816 overall; Clothing 265, Mobility 255, Tooling 296.

## Average Subscription Intention

Table: `Proccessed_data_CSV`. Format: `0.00`.

```dax
AVERAGE(Proccessed_data_CSV[VD1])
```

**Purpose, logic and filter context:** Arithmetic mean of VD1. AVERAGE respects current filters and ignores blanks. Treating ordinal responses as a mean is the implemented descriptive choice.

**Verified / expected result:** 3.4142156863 overall, displayed as 3.41.

## High Intention %

Table: `Proccessed_data_CSV`. Format: `0.0%;-0.0%;0.0%`.

```dax
DIVIDE(
        CALCULATE(
            [Survey Observations],
            'Proccessed_data_CSV'[VD1] >= 5
        ),
        [Survey Observations]
    )
```

**Purpose, logic and filter context:** Share of observations with VD1 >=5. CALCULATE replaces direct VD1 filters with >=5; other filters remain. 

**Verified / expected result:** 234 / 816 = 28.6764706%, displayed as 28.7%.

## High Intention Count

Table: `Proccessed_data_CSV`. Format: `0`.

```dax
CALCULATE(
    [Survey Observations],
    'Proccessed_data_CSV'[VD1] >= 5,
    'Proccessed_data_CSV'[VD1] <= 7
)
```

**Purpose, logic and filter context:** Counts VD1 between 5 and 7 inclusive. CALCULATE applies both bounds, replacing direct VD1 filters while retaining other filters. Unlike High Intention %, it excludes values above 7.

**Verified / expected result:** 234 overall; Clothing 55, Mobility 86, Tooling 93.

## Dynamic Perception Subtitle

Table: `Perception Selector`. Format: `No explicit formatString`.

```dax
VAR SelectedPerception =
    SELECTCOLUMNS(
        SUMMARIZE(
            'Perception Selector',
            'Perception Selector'[Perception Selector],
            'Perception Selector'[Perception Selector Fields]
        ),
        "Label", 'Perception Selector'[Perception Selector]
    )
RETURN
    IF(
        COUNTROWS(SelectedPerception) = 1,
        "by " & CONCATENATEX(SelectedPerception, [Label]),
        "by selected perception"
    )
```

**Purpose, logic and filter context:** Uses parameter-table filter context, not a fact relationship. Exactly one summarized label returns by {label}; zero or multiple labels return by selected perception.

**Verified / expected result:** Expected by expression inspection: selecting Trust returns by Trust. 


## Source and scope

- [Fact measures and intention-band columns](../consumer_adoption.SemanticModel/definition/tables/Proccessed_data_CSV.tmdl)
- [Parameter and subtitle](../consumer_adoption.SemanticModel/definition/tables/Perception%20Selector.tmdl)
- [Education labels](../consumer_adoption.SemanticModel/definition/tables/DimEducation.tmdl)

Intention Band, Intention Band Sort and Education Level are calculated columns, not measures; see the [dictionary](data_dictionary.md). 

