# Public procurement open data: Portugal and Europe, 2026

Measured datasets on public procurement, published by [TRINTA (trinta.ai)](https://trinta.ai), a public tender intelligence company based in Lisbon. Every figure is derived from an official open register and can be checked against it. Period: January to July 2026.

## Headline figures

- **Portugal:** 153,477 public contracts worth EUR 13.6 billion were reported to the Portal BASE from January to July 2026. 13.8% of the 13,498 open tenders (concursos públicos) that published their bidders drew a single bid. Source: the [Barómetro da Contratação Pública](https://trinta.ai/barometro), which these files come from.
- **Europe:** 36.0% of the 571,148 lots awarded through the EU Official Journal (TED) from January to July 2026 drew a single tender. Among the 26 countries with at least 1,000 lots, the highest shares were Poland (57.6%), Greece (55.9%) and Slovenia (46.9%), and the lowest Switzerland (12.2%), Finland (17.3%) and France (18.9%).
- **United Kingdom:** 10.8% of the 12,598 competed lots awarded through Find a Tender drew a single bid.

Portugal reads 13.8% in its own register and 41.4% on TED. Both are true: TED carries only the contracts above the EU thresholds, and the smaller contracts a national register also carries are more contested.

## Files

| File | What it measures | Rows | Source |
|---|---|---|---|
| `data/portugal-2026-contracts-by-cpv.csv` | Contracts, value and competition for every CPV code used in Portugal | 4,635 | IMPIC, Portal BASE, [dados.gov.pt](https://dados.gov.pt/pt/datasets/contratos-publicos-portal-base-impic-contratos-de-2012-a-2026/) |
| `data/portugal-2026-public-buyers.csv` | Public buyers that contracted more than EUR 1 million | 883 | IMPIC, Portal BASE |
| `data/portugal-2026-direct-awards-by-buyer.csv` | Share of each buyer's contracts awarded directly (ajuste direto), buyers with at least 50 contracts | 535 | IMPIC, Portal BASE |
| `data/europe-single-bid-by-country.csv` | Share of lots with a single bid, by country | 34 | TED, EU Official Journal award notices (eForms BT-759) |
| `data/europe-single-bid-by-cpv-division.csv` | The same, by CPV division | 45 | TED |
| `data/uk-single-bid-by-cpv-division.csv` | Share of UK competed lots with a single bid, by CPV division | 39 | UK Find a Tender Service (OCDS) |

Periods, extraction dates and source links for each file are in `data/_sources.json`.

## Columns

**`portugal-2026-contracts-by-cpv.csv`**

| Column | Meaning |
|---|---|
| `code` | CPV code with its check digit, e.g. `03000000-1` |
| `code8` | The same eight digits without the check digit |
| `label` | English CPV label |
| `contracts` | Contracts reported under this code or any code beneath it |
| `valueEur` | Contracted price (`precoContratual`) in euros, under this code or any code beneath it |
| `openProceduresWithBidders` | Open procedures (concurso público) under the code that declared their bidders |
| `meanBids`, `medianBids` | Bids per open procedure; published from 10 procedures up |
| `singleBidPct` | Share of those procedures that drew exactly one bid, in percent; published from 30 procedures up |
| `url` | The code's page, with the buyers behind it |

A code is credited with its whole subtree, so rows at different levels overlap: **do not add up the whole file.** The 45 division rows (`code8` of the form `NN000000`) add up to 153,475 of the 153,477 contracts. Competition is measured on open procedures only: in a direct award or a prior consultation a single bid is the design of the procedure, not a lack of competition.

**`portugal-2026-public-buyers.csv`**: `nif` (Portuguese tax number, the aggregation key), `name`, `valueEur` (contracted value in the period), `contracts`. Buyers are aggregated by NIF and never by name: the same entity appears under up to 51 spellings in the source register.

**`portugal-2026-direct-awards-by-buyer.csv`**: `nif`, `name`, `directAwards` (contracts by ajuste direto), `allContracts` (all the buyer's contracts, any procedure), `pct` (direct awards as a share of all contracts, in percent), `valueEur` (value of the direct awards; a contract with several buyers is split equally between them). Buyers with fewer than 50 contracts are left out, because below that a percentage describes noise.

**`europe-single-bid-by-country.csv`**: `iso3`, `iso2`, `name`, `lots` (lots with a readable count of tenders received), `oneBid` (lots that drew exactly one), `oneBidPct`, `meanTenders`, `medianTenders`. Countries above 30 lots. Eight countries have fewer than 1,000 (Cyprus, Malta, Luxembourg, North Macedonia, Liechtenstein, Iceland, Turkey, United Kingdom): read their shares as small samples. The United Kingdom's 60 lots are a residue, because it left the EU and now publishes to Find a Tender; use the UK file for the UK.

**`europe-single-bid-by-cpv-division.csv`**: `division`, `label`, `lots`, `oneBid`, `oneBidPct`, `meanTenders`, `medianTenders`. A notice counts towards a division only when all of its CPV codes sit in that division.

**`uk-single-bid-by-cpv-division.csv`**: `division`, `label`, `lots`, `oneBid`, `oneBidPct`, `meanBids`, `medianBids`. Competed lots only: awards made without a call for competition are excluded, as the ajuste direto is in Portugal.

## Method, in short

- **Portugal:** the whole 2026 contracts file of the Portal BASE, not a sample. The file held 167,169 contracts reported for 2026 when it was read on 7 September 2026; the 153,477 dated January to July are measured, and the month still open is left out because contracts reach the register late.
- **Europe:** contract award notices published in the EU Official Journal from January to July 2026, counted by lot on eForms BT-759 (the BT-760 total only). Lots declaring zero tenders on a notice that awarded a contract are dropped as impossible.
- **United Kingdom:** Find a Tender award notices for the same months, counted by lot on the OCDS `bids.statistics` measure.

The full methodology, with tables by sector and district, is on the pages these files come from:
- [Portugal's public procurement barometer (PT)](https://trinta.ai/barometro)
- [Single-bid rates across Europe](https://trinta.ai/single-bid-europe)
- [Single-bid rates in the UK](https://trinta.ai/single-bid-uk)
- [CPV codes with measured competition](https://trinta.ai/cpv)

## Licence and citation

Data: [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/). Please cite as:

> TRINTA (2026). *Public procurement open data: Portugal and Europe, 2026.* https://trinta.ai

The underlying registers are published by IMPIC (Portugal), the Publications Office of the EU (TED) and the UK Cabinet Office (Find a Tender Service).

---

# Dados abertos de contratação pública: Portugal e Europa, 2026

Conjuntos de dados medidos sobre contratação pública, publicados pela [TRINTA (trinta.ai)](https://trinta.ai), empresa de inteligência de concursos públicos sediada em Lisboa. Cada número vem de um registo oficial aberto e pode ser confirmado nele. Período: janeiro a julho de 2026.

- **Portugal:** 153.477 contratos públicos, no valor de 13,6 mil M€, comunicados ao Portal BASE de janeiro a julho de 2026. 13,8% dos 13.498 concursos públicos que publicaram a lista de concorrentes tiveram uma única proposta.
- **Europa:** 36,0% dos 571.148 lotes adjudicados no Jornal Oficial da UE (TED) no mesmo período tiveram uma única proposta. Nos 26 países com pelo menos 1.000 lotes, as quotas mais altas são as da Polónia (57,6%), da Grécia (55,9%) e da Eslovénia (46,9%).
- **Portugal lê 13,8% no seu próprio registo e 41,4% no TED.** Os dois estão certos: o TED só tem os contratos acima dos limiares europeus, e os contratos mais pequenos, que só o registo nacional tem, são mais disputados.

Os ficheiros estão descritos acima, em inglês, coluna a coluna. A metodologia completa e as tabelas por setor e por distrito estão no [Barómetro da Contratação Pública](https://trinta.ai/barometro). Dados sob licença CC BY 4.0.
