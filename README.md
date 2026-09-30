# Aldra Signals

Every edition published by [Aldra Research](https://aldraresearch.com), archived as open data.
Two products, one edition each per day:

- **GLOBAL**: policy, markets, geopolitics, technology and energy, worldwide.
- **LATAM**: the same lens on Latin America.

Each edition is bilingual (Spanish and English), verified against its sources before it goes
out, and identical to what is published on the site and on X. Use it freely under
[CC BY 4.0](LICENSE): attribution to *Aldra Research* is the only condition.

*Versión en español más abajo.*

## Layout

```
editions/YYYY/MM/DD/global.json   structured edition (see schema/)
editions/YYYY/MM/DD/global.md     the same edition, readable
editions/YYYY/MM/DD/latam.json
editions/YYYY/MM/DD/latam.md
latest/global.json                copy of the most recent GLOBAL edition
latest/global.md
latest/latam.json
latest/latam.md
schema/edition.schema.json        JSON Schema (draft 2020-12) of the .json files
```

Raw files can be fetched directly, for example:

```
https://raw.githubusercontent.com/aldraresearch/signals/main/latest/global.json
https://raw.githubusercontent.com/aldraresearch/signals/main/editions/2026/10/01/latam.json
```

## The edition object

| Field | Meaning |
|---|---|
| `product` | `GLOBAL` or `LATAM` |
| `date` | the edition's day, Europe/Madrid time |
| `kind` | `full`, `partial`, `fallback` or `quiet`. See below |
| `topic` | dominant topic of the day |
| `published_at` | when the web page went live (ISO 8601, UTC) |
| `web_url` | the edition on aldraresearch.com |
| `headline`, `summary` | `{ es, en }` |
| `stories[]` | each with `status`, `heading`, `text`, `analysis` and `sources` |
| `stories[].status` | `CONFIRMED`: stated as fact, at least two independent sources. `CLAIM`: attributed to its source in the text itself |
| `stories[].analysis` | "why it matters", interpretation kept apart from the facts; may be `null` |
| `stories[].sources` | URLs of the evidence behind the story |
| `content_hash` | SHA-256 of the canonical edition; identical content, identical hash |

**Edition kinds.** `full`: every story passed the sourcing gates and two independent verifiers.
`partial`: only the stories the verifier approved. `fallback`: no story met the sourcing bar, so
the best available ones went out single-sourced and attributed, still verified. `quiet`: nothing
could be published that day; the edition is a short note with no stories and no claims.

Stories that failed verification, the evidence behind the ones that passed, and anything
operational (accounts, costs, metrics) are never in this repository.

## How it is produced

An automated pipeline collects public RSS feeds and X accounts every day, extracts claims,
groups them by event, writes the edition and verifies it with an independent model pass and
structural checks. A story that depends on X alone is never confirmed. A story that reports
deaths or accuses someone needs reinforced evidence. Anything the verifier rejects is dropped
before publication. The archive is written by the same run that publishes the web page, in one
commit per edition, signed `Aldra`.

## Citation

> Aldra Research, *Signal Check GLOBAL, 2026-10-01*, https://github.com/aldraresearch/signals

---

## Español

Todas las ediciones publicadas por [Aldra Research](https://aldraresearch.com), archivadas como
datos abiertos. Dos productos, una edición por día cada uno: **GLOBAL** (política, mercados,
geopolítica, tecnología y energía en el mundo) y **LATAM** (la misma mirada sobre América Latina).

Cada edición es bilingüe, está verificada contra sus fuentes antes de salir y es idéntica a la
que se publica en la web y en X. Podés usarla libremente bajo [CC BY 4.0](LICENSE): la única
condición es atribuirla a *Aldra Research*.

**Estructura.** `editions/AAAA/MM/DD/<producto>.json` y `.md` por día y producto, `latest/` con
la última edición de cada producto, y `schema/edition.schema.json` con el JSON Schema.

**Tipos de edición.** `full`: todas las historias pasaron los gates de fuentes y dos
verificadores. `partial`: sólo las historias aprobadas por el verificador. `fallback`: ninguna
historia alcanzó el piso de fuentes, salen las mejores disponibles, de una sola fuente y siempre
atribuidas, también verificadas. `quiet`: no se pudo publicar ninguna historia; la edición es una
nota breve sin afirmaciones.

**Estado de cada historia.** `CONFIRMED`: se afirma como hecho, con al menos dos fuentes
independientes. `CLAIM`: se atribuye a su fuente en el propio texto.

Las historias rechazadas, la evidencia detrás de las aprobadas y todo lo operativo (cuentas,
costos, métricas) nunca están en este repositorio.
