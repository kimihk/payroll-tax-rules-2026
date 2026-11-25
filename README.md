# Payroll Tax Rules 2026 — Germany · France · Italy

Machine-readable employee payroll parameters for the 2026 tax/social-security year in Germany, France and Italy. Transcribed from the production calculators at **[NettoLab](https://nettolab.app)**, where every number is verified against the official source cited next to it (see `sources` fields in the JSON).

- **Germany** — § 32a EStG tariff, Sozialversicherung rates & caps, Soli, Kirchensteuer → live calculator: https://nettolab.app/de/
- **France** — barème IR 2026 (revenus 2025), CSG/CRDS, AGIRC-ARRCO, quotient familial, décote → live calculator: https://nettolab.app/fr/
- **Italy** — IRPEF a scaglioni, INPS, detrazioni lavoro dipendente, addizionali regionali/comunali → live calculator: https://nettolab.app/it/

Worked examples, edge cases and a net→gross reverse calculator: https://nettolab.app/de/netto-in-brutto/

## What's inside

One file: [`nettolab-tax-rules-2026.json`](nettolab-tax-rules-2026.json)

| Country | Coverage |
|---|---|
| Germany | Grundfreibetrag + tax zones (continuous ramp model), Steuerklasse I–VI handling, SV rates & Beitragsbemessungsgrenzen, Soli Milderungszone formula |
| France | 5-bracket barème per part, abattement 10 %, quotient familial & plafonnement, décote, CSG/CRDS assiette, AGIRC-ARRCO T1/T2, cadre-specific rates (APEC, prévoyance rule) |
| Italy | 3-bracket IRPEF 2026, INPS 9.19 % (+1 % above €56,224), detrazione lavoro dipendente formula, ulteriore detrazione, addizionali for 10 regions |

## Usage

```js
const rules = require("./nettolab-tax-rules-2026.json");
rules.france.income_tax.bareme_per_part;   // [{up_to: 11600, rate: 0}, ...]
rules.italy.addizionali.regionale_2026.veneto; // 0.0123
```

The JSON documents *parameters and formulas*, not a full tax engine. For a working reference implementation, the NettoLab calculators above implement these exact numbers end-to-end (gross → net → payslip breakdown) and are free to use as a cross-check for your own computations.

## Caveats

- Employee side, private sector, metropolitan France / mainland Germany / mainland Italy only.
- France: prévoyance, mutuelle and heures supplémentaires exonérées are convention-dependent and not modelled.
- Italy: addizionale regionale rates are indicative — each region publishes its own brackets by deliberation; addizionale comunale varies 0–0.9 % by municipality.
- Germany: Klasse V/VI use documented approximations of the Vorsorgepauschale; Kirchensteuer depends on confession and Bundesland (8 % BY/BW, 9 % elsewhere).
- Not legal or tax advice. Verify against the cited official sources before production use.

## License

Data: [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/). Attribution appreciated: "NettoLab (nettolab.app)".
