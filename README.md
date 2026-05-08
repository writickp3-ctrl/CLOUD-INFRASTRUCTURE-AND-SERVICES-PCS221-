<div align="center">

# ☁️ PCS221 — Cloud Infrastructure & Services

**Thapar Institute of Engineering & Technology, Patiala**  
M.E. CSE · Academic Year 2025–27

[![Student](https://img.shields.io/badge/Student-Writick%20Parui-0A66C2?style=flat-square)](https://github.com/writickp3-ctrl)
[![Roll No](https://img.shields.io/badge/Roll%20No-8025320111-6f42c1?style=flat-square)]()
[![Course](https://img.shields.io/badge/Course-PCS221-0078D4?style=flat-square)]()
[![Platform](https://img.shields.io/badge/Platform-Google%20Colab%20%7C%20Azure-FF6F00?style=flat-square&logo=googlecolab&logoColor=white)]()

</div>

---

## 📁 Repository Structure

```
PCS221-Cloud-Infrastructure/
│
├── Lab_Assignment_1.ipynb          # Google Colab environment & Python basics
├── Lab_Assignment_2.ipynb          # Large-scale matrix operations (20000×10000)
├── Lab_Assignment_3.ipynb          # E-commerce sales data analysis
├── Lab_Assignment_6.ipynb          # MapReduce without EMR (manual Python + mrjob)
├── Lab_Assignment_7.ipynb          # MapReduce programming with mrjob
│
├── Lab Assignment 4/
│   └── Lab_Assignment4_Writick_Parui_8025320111.pdf
│
└── Lab Assignment 5/
    ├── Lab_Assignment5_Writick_Parui_8025320111.pdf
    ├── index.html                  # Static webpage deployed on Azure VM
    ├── contact.html
    ├── error.html
    ├── ip.txt                      # VM private IP
    └── public_ip.txt               # VM public IP (20.244.62.191)
```

---

## 🧪 Lab Assignments

### Lab 1 — Google Colab Cloud Environment & Python
`Google Colab` `Python` `Shell Commands` `Magic Commands`

Introduction to cloud-based computation using Google Colab as a managed cloud environment.

- Verified cloud execution environment (OS, Python version, machine type)
- Interacted with the Colab environment using `!` shell prefix and `%` magic commands
- Demonstrated Google Drive mounting, package installation, and `%timeit` profiling
- Explored environment variables and disk/memory information from within the cloud VM

---

### Lab 2 — Large-Scale Matrix Operations
`Python` `NumPy` `Random Module` `Memory-Efficient I/O`

Matrix operations on a large **20,000 × 10,000** dataset generated using Python's random module.

| Task | Description |
|------|-------------|
| Task 1 | Generated 20K×10K data file (~1.5 GB) in memory-safe chunks using `randint`, `uniform`, `gauss` |
| Task 2 | Used first-row elements as keys; assigned subsequent column values to each key |
| Task 3 | Grouped similar elements across the matrix |
| Task 4 | Matrix addition and subtraction |
| Task 5 | Built n×n square matrix where all sub-matrices have even sum of opposite corner elements |
| Task 6 | Row-wise element addition using tuple matrices |

---

### Lab 3 — E-Commerce Sales Data Analysis
`NumPy` `Pandas` `Matplotlib` `Seaborn`

Data analysis pipeline on a randomly generated e-commerce sales dataset.

- Generated a **12×4** monthly sales matrix (Electronics, Clothing, Home & Kitchen, Sports) seeded by roll number for reproducibility
- Performed data cleaning, manipulation, and statistical analysis using Pandas
- Visualized category-wise trends using Matplotlib and Seaborn
- Additional tasks: NumPy absolute values, percentiles, rounding functions (`floor`, `ceil`, `trunc`, `round`), and element swapping in lists and sets

---

### Lab 4 — (PDF Submission)
`Microsoft Azure`

> Refer to `Lab Assignment 4/Lab_Assignment4_Writick_Parui_8025320111.pdf`

---

### Lab 5 — VM Migration & Replication using Azure Site Recovery
`Microsoft Azure` `Azure Site Recovery` `Static Web Hosting` `HTML`

Hands-on VM migration and failover using Azure Site Recovery (ASR).

- Deployed a static website (`index.html`, `contact.html`, `error.html`) on an Azure Virtual Machine
- Performed **Test Failover** and **VM Migration** using Azure Site Recovery
- Verified replication by accessing the migrated VM via its public IP

| VM Detail | Value |
|-----------|-------|
| Original Public IP | `20.244.62.191` |
| Migrated VM IP | `20.204.118.73` |

---

### Lab 6 — MapReduce Without EMR
`Python` `mrjob` `MapReduce` `defaultdict`

Implemented MapReduce paradigm in two ways — manual Python and using the `mrjob` framework.

- Built reusable `shuffle()`, `sum_reducer()`, and `avg_reducer()` utility functions
- Solved multiple MapReduce problems: Word Count, and others — all using Mapper → Shuffle → Reducer pipeline
- Demonstrated equivalence between manual Python MapReduce and `mrjob` implementation

---

### Lab 7 — MapReduce Programming with mrjob
`Python` `mrjob` `Regex` `Hadoop Concepts`

Advanced MapReduce programming using the `mrjob` framework.

- Implemented Word Count using `MRJob` class with regex-based tokenizer (`[\w']+`) handling contractions
- Mapper emits `(word, 1)` pairs; Reducer sums counts per word
- Tested on custom input files demonstrating full Hadoop-style MapReduce execution locally

---

## 🛠️ Tech Stack

| Category | Tools |
|----------|-------|
| Cloud Platforms | Google Colab, Microsoft Azure |
| Languages | Python |
| Data Libraries | NumPy, Pandas, Matplotlib, Seaborn |
| Big Data | mrjob (MapReduce), Hadoop concepts |
| Azure Services | Virtual Machines, Azure Site Recovery |
| Web | HTML, CSS (static site on Azure VM) |

---

## 👤 Student Details

| Field | Details |
|-------|---------|
| Name | Writick Parui |
| Roll No. | 8025320111 |
| Course | PCS221 — Cloud Infrastructure & Services |
| Institute | Thapar Institute of Engineering & Technology, Patiala |
| Program | M.E. CSE (2025–2027) |
| GitHub | [@writickp3-ctrl](https://github.com/writickp3-ctrl) |
| LinkedIn | [writick-parui099](https://www.linkedin.com/in/writick-parui099) |

---

<div align="center">

*Part of M.E. CSE coursework at TIET Patiala*

</div>
