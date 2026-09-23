# Florida local codes of ordinances

Where each of Florida's 478 local governments publishes its code of ordinances,
who publishes it, and how current that code is. One row per county and per
incorporated municipality: all 67 counties and all 411 cities, towns and
villages.

**Why this exists.** Municipal law is the hardest layer of American law to
locate. There is no master index, and each commercial codifier publishes an
index of its own clients and nothing else, so a reader who does not already
know who publishes a town's code has nowhere to begin. The valuable part of
this table is not the towns on Municode, which anyone can find by searching
Municode. It is everything else, because no vendor index can show you an
absence.

## Findings, as of 2026-09-04

Four outcomes, and the middle two are the ones no existing list records.

- **423 of 478 publish an actual code of ordinances online.** That is 61 of 67 counties and 362 of 411 municipalities. 414 serve it as a searchable web code and 9 only as a PDF.
- **9 publish their ordinances but have never codified them.** The documents are online one at a time, so answering a question about fences means reading every ordinance the town ever passed. This is a different condition from having a code, and pooling the two would hide it.
- **2 publish nothing online at all.** To read their ordinances you contact the clerk.
- **44 could not be confirmed.** No commercial codifier carries them, and this survey could not establish what they publish instead. They are almost all towns under 1,000 people. Each row says what was checked; none is a claim that nothing exists.
- **1223 adopted ordinances are waiting to be codified across Florida.** An ordinance that has passed but is not yet in the code still binds the property.
- **16 codes were last codified more than three years ago**, and a further **15 state a codification date that postdates the supplement carrying it**, which is impossible and is recorded as a note rather than as a date.
- One publisher, Municode, carries 400 of them. A single vendor holds most of Florida's municipal law.

### By status

| Status          | Count |
|-----------------|------:|
| online-html     |   414 |
| unknown         |    44 |
| ordinances-only |     9 |
| online-pdf-only |     9 |
| no-online-code  |     2 |

### By publisher

| Publisher             | Count |
|-----------------------|------:|
| municode              |   400 |
| unknown               |    44 |
| self-hosted           |    18 |
| american-legal        |    10 |
| municipal-code-online |     3 |
| none                  |     2 |
| general-code          |     1 |

### By type

| Type    | Count |
|---------|------:|
| city    |   267 |
| town    |   123 |
| county  |    67 |
| village |    21 |

## Files

| File | What it is |
|------|------------|
| `data/fl-local-codes.csv` | the table, UTF-8 with a header row |
| `data/fl-local-codes.json` | the same rows as objects |
| `data/fl-local-codes.parquet` | typed columns, for anything loading at scale |
| `datapackage.json` | Frictionless schema, per column types and descriptions, SHA-256 and row count |
| `dataset.jsonld` | schema.org/Dataset |
| `croissant.json` | MLCommons Croissant |

Every row carries a `statement` column, the row written as one English
sentence, so a single row can be retrieved, quoted and checked on its own.

## Method, and the two traps in it

The jurisdiction list comes from the Census Bureau subcounty population file,
vintage 2024, which is independent of every codifier and yields exactly 67
counties and 411 municipalities, matching the Florida League of Cities
directory. Each codifier's public metadata was joined onto that list by
normalised name, and everything left over was opened by hand in a browser.

1. **Municode's classification field is not jurisdiction type.** Palmetto Bay
   is 9, Jacksonville is 3, and 80 municipalities sit in 6. Type comes from the
   Census and never from the vendor.
2. **A 200 does not mean a page exists.** `library.municode.com/fl/<anything>`
   returns success and a JavaScript shell for slugs that do not exist, so a
   status code cannot verify a link. Every Municode address here was checked
   against the resolver the library's own page calls, which returns the client
   id, and the check is stored beside the row.

A third, in the name join: Florida has both a Melbourne and a Melbourne
Village, and both an Indian Creek and an Indian Creek Village. A normaliser
that treats a trailing type word as a label rather than as part of the name
hands one town's code to another. Exact names are matched first for every
jurisdiction, and only then is a trailing type word treated as droppable.

## Limitations

- **Point in time.** Codifier contracts move. Every row carries the date it was
  checked, and that date is part of the claim.
- **Currency is the publisher's word.** `codified_through` reports when the code
  was last compiled, not that the compilation is correct or complete.
- **Official status is usually unstated.** Recorded only where the page says so.
- **Metadata only.** This dataset says where the law is, never what it says.

## Licence and citation

Compilation licensed [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/).
The ordinances themselves carry no copyright; they are edicts of government,
per *Georgia v. Public.Resource.Org*, 590 U.S. 255 (2020). No ordinance text is
included here.

Cite as: Klagge, Kevin D. "Florida local codes of ordinances, 2026." StepUpLaw.

Documented at <https://stepuplaw.com/data/florida-local-codes/>.
Method and build code: the `legal-empirics` repository, local copy at
`~/legal-empirics` (`studies/fl-local-codes/`, `protocols/fl-local-codes.md`).
