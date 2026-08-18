# VENTO: territorial screening and preliminary social-engagement planning

This repository contains the reproducible workflow used for the Colombian case study presented in:

**A Territorial Risk–Based Framework for Determining Social Engagement Modalities in Colombian Regions with Wind Energy Potential**

## Scope

The workflow combines:

1. Municipal wind-resource availability after spatial restrictions.
2. Socio-cultural and territorial descriptors.
3. A four-component relative security-risk score.
4. Preliminary engagement modes for early social-characterization planning.

The outputs are screening and planning aids. They do not determine final project viability, authorize physical entry, replace current institutional security protocols, or exclude communities from consultation and participation.

## Repository structure

```text
.
├── README.md
├── VENTO_pipeline_reproducible.ipynb
├── requirements.txt
├── data/
│   ├── dataset_completo.csv
│   └── variables_metadata.csv
└── figures/                         
```

## Reproducibility

Create a Python environment and install the dependencies:

```bash
python -m venv .venv
python -m pip install -r requirements.txt
```

Open and run the notebook from the repository root:

```bash
jupyter lab VENTO_pipeline_reproducible.ipynb
```

All input paths are relative to `data/`. 

## Risk-score construction

```text
RiskRaw =
    0.35 * Z(criminality index)
  + 0.30 * Z(number of armed groups)
  + 0.20 * Z(log(1 + coca-crop density))
  + 0.15 * Z(1 / (1 + minimum distance to coca crops))
```

Missing values required for the score are imputed with the national median. The raw score is normalized to 0–1. P50 and P75 are recalculated over the 1,122-municipality reference universe to define low, medium, and high relative categories.

The Colombian weights were elicited from expert ratings, averaged, and normalized to sum to one. A new implementation that changes the weights should include its own sensitivity analysis.

## Outcomes

| Relative category | National municipalities | Municipalities with availability above 15% |
|---|---:|---:|
| Low | 561 | 76 |
| Medium | 280 | 21 |
| High | 281 | 14 |

The corresponding preliminary modes are in-person subject to verification, in-person with caution, and remote initial engagement, respectively.

## Sensitivity analysis

Deterministic alternatives produced category agreement between **88.50% and 95.37%** relative to the baseline.

| Weight design (50,000 iterations) | Mean baseline-category agreement |
|---|---:|
| Moderate Dirichlet centered on expert weights | 94.83% |
| Broad Dirichlet centered on expert weights | 89.65% |
| Uniform Dirichlet over admissible weights | 85.55% |

Under moderate perturbations, 96 of the 111 selected municipalities were robust, 10 sensitive, and 5 uncertain. Robust means at least 90% probability of retaining the baseline category; sensitive means 60–89.9%; uncertain means below 60%.

## Data dictionary

`data/variables_metadata.csv` contains one row per variable and documents:

- Definition, unit, and transformation.
- Risk direction.
- Source institution and URL or DOI.
- Reference year or period.
- Spatial resolution and municipal processing.
- Validation notes.

## Responsible use

- Percentile categories are relative to the stated reference universe.
- A low relative category is not evidence that physical entry is safe.
- Engagement modes require current institutional and local verification.
- Remote initial engagement must not reduce consultation. Use accessible channels, trusted intermediaries, and periodic reassessment.
- No category excludes a community from social characterization or legally required consultation.

## Future work

Future validation should compare the preliminary categories with independent, time-stamped incident data and structured assessments by security, territorial, and local experts. Priority should be given to detecting false-low classifications and evaluating whether remote-first approaches reach groups with connectivity or representation barriers.
