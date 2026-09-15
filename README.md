# Personalized Learning Path Recommendation System for Interns

## 📌 Project Overview

The **Personalized Learning Path Recommendation System for Interns** is a machine learning project designed to recommend customized learning modules to interns based on their previous learning behavior and course preferences.

Organizations often provide interns with a large number of training courses and learning resources. However, the same learning path may not be suitable for every intern because individuals have different interests, skill levels, learning histories, and career goals.

This project addresses this problem by developing a **Collaborative Filtering recommendation system using Matrix Factorization**. The model learns hidden patterns from historical intern-course interactions and uses these patterns to predict which courses an intern is most likely to find useful.

The final system generates a personalized list of recommended courses and can be extended to create complete learning paths for individual interns.

---

## 🎯 Project Objective

The main objective of this project is to develop an intelligent recommendation system that can:

* Analyze historical intern learning patterns.
* Identify relationships between interns and learning modules.
* Learn latent preferences using Matrix Factorization.
* Predict an intern's potential interest in courses they have not completed.
* Recommend personalized learning modules.
* Use course metadata to improve recommendation quality.
* Generate customized learning paths for individual interns.

---

## ❓ Problem Statement

Interns usually have access to many training courses, but manually selecting the most appropriate courses can be difficult.

For example, two interns may have different learning histories:

**Intern A**

```text
Python Basics
Statistics
SQL
```

**Intern B**

```text
Communication Skills
Project Management
Excel Analytics
```

A generic training system may recommend the same courses to both interns.

This project aims to provide a more personalized solution by learning from historical interactions.

The system can identify that Intern A may be interested in:

```text
Machine Learning
Data Visualization
NLP Fundamentals
```

while Intern B may benefit more from:

```text
Advanced Excel
Power BI
Project Management
```

---

## 💡 Proposed Solution

The proposed system uses **Collaborative Filtering with Matrix Factorization**.

Historical learning interactions are converted into an **Intern × Course interaction matrix**.

For example:

| Intern | Python | SQL | ML | NLP | Power BI |
| ------ | -----: | --: | -: | --: | -------: |
| I001   |      5 |   4 |  0 |   0 |        2 |
| I002   |      4 |   0 |  5 |   4 |        0 |
| I003   |      2 |   5 |  4 |   0 |        1 |
| I004   |      0 |   3 |  5 |   5 |        0 |

Here:

* Rows represent interns.
* Columns represent courses.
* Values represent learning interactions or ratings.
* `0` represents no observed interaction.

Matrix Factorization decomposes this matrix into latent representations of interns and courses.

The model approximates the interaction matrix as:

```text
R ≈ U × Vᵀ
```

where:

* `R` = Intern-Course interaction matrix
* `U` = Intern latent-factor matrix
* `V` = Course latent-factor matrix

The predicted interactions are then used to rank courses and generate recommendations.

---

## 🏗️ System Architecture

```text
                  Historical Learning Data
                           │
                           ▼
                  Data Preprocessing
                           │
                           ▼
              Intern-Course Interaction Matrix
                           │
                           ▼
                 Collaborative Filtering
                           │
                           ▼
                  Matrix Factorization
                           │
                           ▼
                  Predicted Preferences
                           │
                           ▼
              Course Recommendation Engine
                           │
                           ▼
                  Course Metadata Filter
                           │
                           ▼
             Personalized Learning Path
                           │
                           ▼
                    Final Recommendations
```

---

## 📊 Dataset

The project uses two primary datasets.

### 1. Intern Learning Data

The learning interaction dataset contains historical information about intern interactions with courses.

Example fields:

| Column       | Description                      |
| ------------ | -------------------------------- |
| `intern_id`  | Unique identifier for an intern  |
| `course_id`  | Unique identifier for a course   |
| `rating`     | Intern's rating of the course    |
| `completion` | Whether the course was completed |
| `time_spent` | Time spent learning the course   |

Example:

```text
intern_id,course_id,rating,completion,time_spent
I001,C001,5,1,120
I001,C002,4,1,90
I002,C001,4,1,100
I002,C003,5,1,150
```

### 2. Course Metadata

The course metadata dataset provides information about available learning modules.

Example fields:

| Column           | Description                 |
| ---------------- | --------------------------- |
| `course_id`      | Unique course identifier    |
| `course_name`    | Name of the course          |
| `category`       | Course category             |
| `difficulty`     | Course difficulty level     |
| `duration_hours` | Approximate course duration |

Example:

```text
course_id,course_name,category,difficulty,duration_hours
C001,Python Basics,Programming,Beginner,5
C002,SQL Fundamentals,Data,Beginner,6
C003,Machine Learning Basics,AI,Intermediate,10
```

> **Note:** The current development version may use a synthetic dataset for demonstration and model development. In a production environment, anonymized real-world learning data should be used.

---

## 🤖 Machine Learning Method

### Collaborative Filtering

Collaborative Filtering recommends items based on the behavior and preferences of users with similar patterns.

In this project:

```text
Users  → Interns
Items  → Learning Courses
Interactions → Ratings / Completion / Learning Activity
```

The system does not need to manually define every intern's preferences. Instead, the model learns preference patterns from historical interactions.

---

## 🧮 Matrix Factorization

Matrix Factorization is used to discover hidden relationships between interns and courses.

The interaction matrix is represented as:

```text
R
```

and decomposed into two lower-dimensional matrices:

```text
U × Vᵀ
```

Each intern is represented using a set of latent factors, while each course is represented using another set of latent factors.

The dot product between an intern's latent representation and a course's latent representation produces a predicted preference score.

A higher predicted score means the course is potentially more suitable for the intern.

---

## 🔄 Project Workflow

The complete machine learning workflow consists of the following stages:

### Step 1 — Data Collection

Collect historical learning interactions and course metadata.

### Step 2 — Data Preprocessing

* Check missing values.
* Remove invalid records.
* Validate ratings.
* Convert categorical information where necessary.
* Prepare the interaction data.

### Step 3 — Exploratory Data Analysis

Analyze:

* Course popularity.
* Rating distribution.
* Completion rates.
* Learning time.
* Intern activity.
* Course categories.

### Step 4 — Interaction Matrix

Create an Intern × Course matrix containing historical interactions.

### Step 5 — Train/Test Split

Divide observed interactions into training and testing datasets.

### Step 6 — Matrix Factorization

Train the collaborative filtering model using latent factors.

### Step 7 — Model Evaluation

Evaluate predictions using metrics such as:

* RMSE
* MAE

Additional recommendation metrics can be added:

* Precision@K
* Recall@K
* Hit Rate@K

### Step 8 — Recommendation Generation

Predict scores for courses that an intern has not previously completed.

### Step 9 — Course Filtering

Remove courses already completed by the intern.

### Step 10 — Personalized Learning Path

Rank recommended courses and organize them into a suitable learning sequence.

---

## 📁 Project Structure

```text
intern_learning_recommender/
│
├── data/
│   ├── intern_learning.csv
│   └── courses.csv
│
├── learning_recommender.ipynb
│
├── requirements.txt
│
├── .gitignore
│
└── README.md
```

---

## 🛠️ Technologies Used

### Programming Language

* Python

### Development Environment

* Visual Studio Code
* Jupyter Notebook

### Libraries

* **Pandas** — data manipulation and analysis
* **NumPy** — numerical computation
* **Matplotlib** — data visualization
* **Seaborn** — statistical visualization
* **Scikit-learn** — machine learning utilities and evaluation
* **SciPy** — sparse matrix and scientific computing operations

---

## ⚙️ Installation

### 1. Clone the repository

```bash
git clone https://github.com/YOUR_USERNAME/intern-learning-recommender.git
```

Move into the project directory:

```bash
cd intern-learning-recommender
```

### 2. Create a virtual environment

```bash
python -m venv venv
```

Activate it.

#### Windows

```bash
venv\Scripts\activate
```

#### macOS/Linux

```bash
source venv/bin/activate
```

### 3. Install dependencies

```bash
pip install -r requirements.txt
```

---

## ▶️ How to Run the Project

### Start Jupyter Notebook

Run:

```bash
jupyter notebook
```

or open the project directly in Visual Studio Code.

Open:

```text
learning_recommender.ipynb
```

Run the notebook cells sequentially.

The notebook performs:

```text
Data Loading
      ↓
Data Exploration
      ↓
Preprocessing
      ↓
Interaction Matrix
      ↓
Matrix Factorization
      ↓
Model Evaluation
      ↓
Recommendation Generation
      ↓
Personalized Learning Path
```

---

## 🔍 Example Recommendation

After training the model, the system can generate recommendations such as:

### Intern: I001

| Rank | Course                  | Category   | Difficulty   | Predicted Score |
| ---: | ----------------------- | ---------- | ------------ | --------------: |
|    1 | NLP Fundamentals        | AI         | Advanced     |            4.63 |
|    2 | Machine Learning Basics | AI         | Intermediate |            4.52 |
|    3 | Data Visualization      | Data       | Beginner     |            4.47 |
|    4 | Statistics              | Statistics | Intermediate |            4.31 |
|    5 | Power BI                | Analytics  | Beginner     |            4.20 |

The intern's previously completed courses are excluded from the recommendation list.

---

## 🧭 Personalized Learning Path

The recommendation engine can be extended beyond individual course recommendations.

For example:

```text
Python Basics
      ↓
Statistics
      ↓
Machine Learning Basics
      ↓
NLP Fundamentals
      ↓
Advanced Machine Learning
```

This allows the system to provide a **structured learning path** rather than simply displaying a list of courses.

---

## 📈 Model Evaluation

The model can be evaluated using prediction-based metrics.

### RMSE

Root Mean Squared Error measures the difference between actual and predicted ratings.

```text
Lower RMSE → Better prediction accuracy
```

### MAE

Mean Absolute Error measures the average absolute difference between actual and predicted ratings.

```text
Lower MAE → Better prediction accuracy
```

For a recommendation system, ranking-based metrics such as Precision@K and Recall@K can also be incorporated to evaluate the quality of the top recommendations.

---


