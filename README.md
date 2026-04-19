## DI 501 Term Project
### Climate-Driven Maize Yield Instability Across European Climate Panels
**Author:** Eda Yilmaz | Middle East Technical University

---

## Project Description

This project investigates subnational maize yield instability across three European climate panels (Mediterranean, Temperate, and Continental) using the CY-Bench dataset. Two research questions are explored:

- **RQ1 (Hypothesis Testing):** Do subnational maize yield instability levels differ significantly across three European climate panels?
- **RQ2 (Machine Learning):** Can engineered climate stress features predict annual deviations of maize yield from its long-term trend at the subnational level?

## Dataset

This project uses the [CY-Bench dataset](https://github.com/BigDataWUR/AgML-crop-yield-forecasting) — a comprehensive benchmark for subnational crop yield forecasting. Nine European countries are included, grouped into three climate panels:

- **Mediterranean:** Italy, Spain, Greece
- **Temperate:** Germany, France, Austria
- **Continental:** Romania, Hungary, Poland

> Download the CY-Bench data and place it in the `data/` folder before running the notebooks.

## Repository Structure

```
DI501-Term-Project/
├── data/                                    <- CY-Bench dataset (download separately)
├── notebooks/                               <- Jupyter notebooks
│   ├── step3_data_quality.ipynb             <- Data quality checks and descriptive statistics
│   ├── step3_descriptive_stats_table.ipynb  <- Descriptive statistics table
│   └── step4_naive_baseline.ipynb           <- Performance metrics and naive baseline
├── reports/                                 <- IEEE format paper
│   └── figures/                             <- Generated figures used in the paper
├── requirements.txt                         <- Required Python packages
└── README.md                                <- This file
```

## How to Run

1. Clone the repository:
```
git clone https://github.com/eda-yilmaz/DI501-Term-Project.git
```

2. Install required packages:
```
pip install -r requirements.txt
```

3. Download the CY-Bench dataset and place it in the `data/` folder.

4. Run the notebooks in order:
   - `step3_data_quality.ipynb`
   - `step3_descriptive_stats_table.ipynb`
   - `step4_naive_baseline.ipynb`

## AI Usage Statement

Artificial intelligence was used to assist with code development and language check for drafting parts of the report. All analytical decisions, research questions, and interpretations were made by the author.
