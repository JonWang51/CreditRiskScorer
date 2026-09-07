# CreditRiskScorer

A step-by-step C++ project for estimating whether a loan applicant is likely to
default. The project will use a public, de-identified lending dataset and will
eventually produce a probability, risk category, and lending recommendation.

## Current status

This repository contains the initial project framework only. No dataset,
prediction model, or financial decision logic has been implemented yet.

## Project layout

```text
CreditRiskScorer/
├── CMakeLists.txt
├── data/
│   ├── raw/                 # Original downloaded dataset; do not edit
│   └── processed/           # Cleaned data and derived datasets
├── docs/                    # Notes about the dataset and modeling decisions
├── include/                 # Public project headers
├── src/                     # Application and implementation files
└── tests/                   # Focused tests for each stage
```

## Build and run

Requirements:

- CMake 3.20 or newer
- A compiler with C++20 support

```bash
cmake -S . -B build
cmake --build build
./build/credit_risk_scorer
```

On macOS with a multi-configuration generator, the executable may be at
`build/Debug/credit_risk_scorer` instead.

## Learning roadmap

We will implement one stage at a time and validate each stage before moving on:

1. **Dataset understanding**: choose a dataset, document its license and target
	column, and inspect missing values and class imbalance.
2. **Data representation**: define an `Applicant` record and a labeled dataset
	type in C++.
3. **CSV ingestion and cleaning**: parse only the columns we need, handle
	missing values, and create a reproducible train/test split.
4. **First baseline**: implement a simple, explainable baseline and measure its
	confusion matrix.
5. **Probability model**: add a logistic regression model that outputs default
	probabilities.
6. **Evaluation**: calculate precision, recall, ROC-AUC, and calibration on a
	held-out test set.
7. **Decision policy**: choose risk thresholds and compare false-positive and
	false-negative costs.
8. **Feature importance**: report which input features influence predictions.
9. **Expected profit**: define lender revenue, loss, and operating costs, then
	select the action that maximizes expected profit rather than raw accuracy.
10. **User-facing scorer**: accept applicant fields and print the probability,
	 risk category, and recommendation.

## Initial design decisions

- C++ is used for the application and model implementation.
- CMake is used so the project can build consistently from the command line or
  VS Code.
- Raw data stays separate from processed data to preserve reproducibility.
- The model's probability and the lender's decision threshold are separate
  concepts: a probability is not itself a recommendation.
- We will avoid using post-loan fields or other information unavailable at
  application time, preventing target leakage.

## Important limitations

This will be an educational risk-modeling project, not a production lending
system. Real lending decisions require legal, fairness, privacy, security, and
model-governance review. Dataset documentation and permitted use must be checked
before downloading or redistributing data.
