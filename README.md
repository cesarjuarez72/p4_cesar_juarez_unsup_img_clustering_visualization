# Project 4: Discovering Patterns in Handwritten Digits Using Unsupervised Learning (MNIST)

**Author:** Cesar Juarez  
**Program:** Data Analytics & Artificial Intelligence  


---

## What This Project Is About

In supervised learning (like our stock prediction project), we gave the computer both the data and the answers. The computer simply had to learn the rules linking the two.

This project takes a completely different path: **unsupervised learning**. We handed an algorithm 10,000 images of handwritten digits without any labels, hints, or category names. The computer does not know what a "0" or an "8" is, and it does not know humans use a base-10 number system.

All it sees are grids of numbers representing dark and light pixels. Our goal is to test whether an algorithm called **K-Means** can look at those pixel patterns and group similar-looking numbers together purely by comparing where the ink lands on the page.

---

## System Architecture Pipeline

The project follows a consistent, reproducible 2-cell cadence in Google Colab (Cell A: plain-English instructional breakdown; Cell B: production-grade Python code) across 7 structural stages:

| Stage | Process | Everyday Analogy | What We Learned |
| :---: | :--- | :--- | :--- |
| **01** | **Exploration & Normalization** | Converting handwriting photos into a standardized 28×28 microscopic grid. | Squeezing pixel values into a `[0.0, 1.0]` range keeps ink-heavy strokes from overpowering our distance math. |
| **02** | **Sampling & Elbow Method** | Asking someone who cannot read numbers to sort mail into neat stacks. | Testing $K \in \{5, 10, 15\}$ showed a big improvement up to 10 clusters before gains leveled off. |
| **03** | **Centroid Archetypes** | Stacking tracing paper sheets to see the average number emerge. | Clean shapes like 0 and 1 make sharp "average" images; numbers like 4 and 9 make blurry composites. |
| **04** | **The Reality Check** | Bringing in a human inspector to audit the unlabelled stacks. | Simple shapes sort with 70% to 90%+ purity; numbers sharing identical strokes cross-contaminate. |
| **05** | **2D Satellite Map (PCA)** | Flattening a multi-story building into a 2D floorplan. | Visually shows distinct numbers drifting outward while curved numbers crowd the center. |
| **06** | **Live Production Testing** | Handing the system fresh mail to see if it routes to the right bin. | Unseen, cleanly drawn digits route instantly; heavily slanted digits drift to unexpected bins. |
| **07** | **Synthesis & Comparison** | Writing the final executive debrief. | Answers all 8 analytical questions contrasting supervised vs. unsupervised paradigms. |

---

## Repository Structure

```text
├── Project4_CesarJuarez.ipynb              # Fully executed, clean Colab notebook (Parts 1–7 + t-SNE)
├── Project4_Report_CesarJuarez.docx        # Professional executive report generated via Python
├── Project4_CesarJuarez.pdf                # Submission-ready export of the notebook
├── project4_architecture_blueprint.png     # Process infographic diagram
└── README.md                               # Project documentation and execution instructions
```

---

## Core Findings & Takeaways

### 1. What K-Means Discovered
The algorithm discovered broad visual shapes based on where dark pixels sit on the grid. Without knowing what digits are, it grouped numbers that share similar line slants, stroke thicknesses, and empty margins.

### 2. Why K = 10 Was Selected
Evaluating inertia across $K \in \{5, 10, 15\}$ showed that moving from 5 to 10 produced a substantial drop in cluster tightness (inertia), while moving from 10 to 15 offered diminishing returns. Setting $K = 10$ also allowed us to test whether an unsupervised system could independently uncover the 10 fundamental digits of our base-10 numerical system.

### 3. Digits That Grouped Cleanly vs. Digits That Confused the Model
* **High Purity (Easy to Isolate):** Digits like **0**, **1**, **2**, and **6** formed very clean groups. Digit 1 often split into two distinct clusters: one for straight vertical strokes and another for angled, forward-slanted strokes.
* **High Confusion (Difficult to Isolate):**
  * **4 and 9:** Both rely on a long vertical right stem and an upper enclosed loop or box.
  * **3, 5, and 8:** All three feature curved bottom loops and central horizontal strokes, which easily fool straight pixel-distance comparisons.

### 4. Real-World Limitations of Pixel-Based Clustering
* **No Concept of Continuous Strokes:** K-Means checks pixel coordinates one by one. It has no awareness that lines connect into a single drawing.
* **Shift Sensitivity:** Shifting the exact same digit just two pixels to the right drastically increases straight-line distance, making the algorithm treat it like a completely different shape.
* **Forced Binning:** K-Means forces every messy, unusual, or ambiguous scribble into one of the 10 buckets, even when it is a poor fit.

---

## Environment Setup & Reproduction

### Prerequisites
- Python 3.10+
- Google Colab or a local Jupyter Notebook environment

### Required Dependencies
```bash
pip install numpy pandas matplotlib seaborn scikit-learn python-docx
```

### Running the Notebook
1. Clone or download this repository:
   ```bash
   git clone [https://github.com/your-username/mnist-unsupervised-clustering.git](https://github.com/your-username/mnist-unsupervised-clustering.git)
   cd mnist-unsupervised-clustering
   ```
2. Open `Project4_CesarJuarez.ipynb` in Google Colab or your local Jupyter server.
3. Run all cells from top to bottom (`Runtime` -> `Run all`). 
4. The notebook downloads the MNIST 784 dataset directly from OpenML using Scikit-Learn (no manual dataset downloads required).
5. The final code cells automatically verify matrix shapes, generate the executive `.docx` report, and confirm submission integrity.
