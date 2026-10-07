# DC-DC Buck Converter Design

This repository contains design artifacts for a series chopper (buck converter) created in Proteus, plus a photograph of the physical work. It is a design archive rather than a complete, reproducible hardware release: the target input voltage, output voltage, switching frequency, load range, efficiency target, component ratings, and validation results are not documented in text.

## Repository contents

| File | Purpose |
| --- | --- |
| `CIRCUIT_PUISSANCE_HACHEUR_SERIE.DSN` | Proteus schematic/simulation design for the power stage. |
| `CIRCUIT_PUISSANCE_HACHEUR_SERIE.LYT` | Proteus PCB/layout artifact associated with the design. |
| `IMG_0185.HEIC` | Project photograph; use an HEIC-compatible image viewer. |

No firmware, exported schematic PDF, bill of materials, fabrication files, or automated tests are included.

## Background

A buck converter reduces a DC input voltage by switching energy into an inductor and filtering the result. For an ideal converter operating in continuous conduction, the first-order relationship is:

```text
Vout approximately equals duty_cycle * Vin
```

Real output voltage and efficiency also depend on switching losses, diode or synchronous-switch losses, inductor resistance and saturation, capacitor ESR, switching frequency, load, dead time, and PCB layout. The ideal relationship must therefore not be used as a substitute for simulation and measurement.

## Opening the design

You will need a Proteus installation compatible with the checked-in `.DSN` and `.LYT` formats. The exact Proteus release and any third-party component models used to create the files are not recorded.

1. Clone or download the repository.
2. Make a backup copy before allowing Proteus to convert the files to a newer format.
3. Open `CIRCUIT_PUISSANCE_HACHEUR_SERIE.DSN` and resolve any missing-library or model warnings.
4. Inspect every component value, device model, gate-drive setting, supply, load, and switching source in the schematic. Treat those properties as the source of truth; this README does not infer undocumented ratings.
5. Open `CIRCUIT_PUISSANCE_HACHEUR_SERIE.LYT` to review the associated board layout. Confirm that it still matches the schematic before using it for fabrication.

## Suggested simulation checks

Run the design first with conservative, current-limited conditions and record the configuration used. At minimum, check:

- input and output voltage over the intended duty-cycle and load range;
- output ripple and startup/settling behavior;
- switch and diode voltage/current stress;
- inductor peak current, RMS current, ripple, and saturation margin;
- capacitor ripple-current and voltage ratings;
- transient response to input, duty-cycle, and load changes;
- estimated conduction and switching losses; and
- device temperatures and safe operating area using realistic component models.

For hardware validation, begin with an isolated, current-limited DC supply. Use correctly rated probes and compare measured waveforms with the simulation before increasing power.

## Design-review checklist

Before treating this as a build-ready converter, add or verify:

- explicit electrical requirements and acceptable tolerances;
- a bill of materials with manufacturer part numbers and voltage/current/thermal derating;
- gate-drive voltage, timing, switching frequency, and startup behavior;
- feedback/control-loop design, if closed-loop regulation is intended;
- overcurrent, overvoltage, reverse-polarity, and thermal protection;
- creepage, clearance, trace width, return paths, and high-current loop area;
- schematic-to-layout consistency and design-rule checks; and
- reproducible simulation and bench-test results.

## Safety

Power converters can expose the operator and test equipment to destructive current, hot components, stored capacitor energy, and hazardous voltage. Do not energize hardware solely because a simulation runs. Use fusing, current limiting, isolation where required, eye protection, discharge procedures, and components/instruments rated for the actual circuit. The files in this repository have not been certified for production or safety-critical use.
