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
Every file names its source, the source page it came from, and the bank's own
"data as at" stamp. Attribute the numbers to the bank, not to this repository.

## Layout

```
data/{provider}/{table}/{frequency}/{ISO3}.json          latest
data/{provider}/{table}/{frequency}/snapshots/{ISO3}.{date}.json   dated vintage
```

`provider` is `eccb` or `cbb`, `frequency` is `a`, `q` or `m`.

## The two dates are not the same thing

Every document carries `data_as_at`, which is the BANK's own claim about how
current the figures are, and `retrieved_at`, which is only when this collector
fetched them. They differ, often by weeks, and they differ per table and per
country. Presenting a retrieval time as the data's currency would be a lie by
formatting, so both travel separately into every citation StatCite produces.

## Snapshots are written only when the bank changes something

A dated snapshot appears when the source's content actually moved, judged
against the bank's own currency stamp rather than against a byte diff. A quiet
week produces no new files. That makes the history a record of what the banks
published, not of when the collector happened to run.

## Coverage

Nine ECCU geographies plus the currency union aggregate, and Barbados. Includes
Anguilla and Montserrat, which are not World Bank reporting economies and
therefore appear in few other machine-readable sources.
