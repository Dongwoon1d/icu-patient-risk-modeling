# Data Access

Raw MIMIC-IV Demo data is not included in this repository.

This project uses the **MIMIC-IV Clinical Database Demo** from PhysioNet.

To reproduce this project, download the dataset directly from PhysioNet and place it in the following local path:

```text
data/mimic-iv-clinical-database-demo/
```

Expected local structure:

```text
data/
└── mimic-iv-clinical-database-demo/
    ├── hosp/
    ├── icu/
    ├── demo_subject_id.csv
    ├── LICENSE.txt
    └── README.txt
```

Processed patient-level files are also excluded from this repository to follow responsible healthcare data handling practices.

The notebook will generate processed files locally under:

```text
data/processed/
```

These processed files should remain local and should not be uploaded to GitHub.
