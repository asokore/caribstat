# CaribStat data

Machine-readable snapshots of published Caribbean central bank statistics, kept
current by a scheduled collector and served to AI agents through
[StatCite](https://statcite.com).

## Sources and attribution

| | |
|---|---|
| **Eastern Caribbean Central Bank** | https://www.eccb-centralbank.org/statistics |
| **Central Bank of Barbados** | https://www.centralbank.org.bb |

Both banks are the authors of these statistics. This repository republishes what
they publish, with permission obtained from each institution by the operator.
Every file names its source and the source page it came from. ECCB files
collected while the bank printed its "data as at" stamp also carry that stamp.
The bank stopped printing it in late September 2026, and ECCB files collected
since then carry none. Attribute the numbers to the bank, not to this
repository.

## Layout

```
data/{provider}/{table}/{frequency}/{ISO3}.json          latest
data/{provider}/{table}/{frequency}/snapshots/{ISO3}.{date}.json   vintage filed under the bank's own stamp
data/{provider}/{table}/{frequency}/snapshots/{ISO3}.retrieved-{timestamp}.json   vintage from a table with no stamp, filed under the collector's retrieval time
```

`provider` is `eccb` or `cbb`, `frequency` is `a`, `q` or `m`.

## The two dates are not the same thing

Where a document carries `data_as_at`, that is the BANK's own claim about how
current the figures are. `retrieved_at` is only when this collector fetched
them. The two differ. The gap is often several weeks, it varies by table and by
country, and presenting a retrieval time as the data's currency would be a lie
by formatting, so the two are never merged.

When the bank prints no stamp, the document has no `data_as_at` at all. None is
borrowed from an earlier collection, and `retrieved_at` is never put in its
place. Central Bank of Barbados documents carry `published_at` instead, the date
of the workbook the figures were taken from.

## Snapshots are written only when the bank changes something

A snapshot appears when the source's content actually moved, not on every run.
Stamped tables are judged by their stamp. When it prints
none, the figures themselves decide: a changed value, row or period that the
collector's own query cannot explain. Such a snapshot is filed under the
collector's full retrieval time, so it cannot pass for a date the bank printed.
A quiet week produces no new files. That makes the history a record of what the
banks published, not of when the collector happened to run.

## Coverage

The eight ECCB member geographies plus the currency union aggregate, and
Barbados. Includes
Anguilla and Montserrat, which are not World Bank reporting economies and
therefore appear in few other machine-readable sources.
