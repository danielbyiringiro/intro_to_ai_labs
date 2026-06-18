# Lab 0: Environment Setup & Python for AI Foundations

**Duration:** 1 week  
**Due Date:** 4 June 2026  
**Format:** Guided interactive session with local setup verification  
**Grading:** This is a graded lab

---

## Table of Contents
1. [Learning Objectives](#learning-objectives)
2. [Prerequisites](#prerequisites)
3. [Part 1: Development Environment Setup](#part-1-development-environment-setup)
4. [Part 2: Git & GitHub Fundamentals](#part-2-git--github-fundamentals)
5. [Part 3: Google Colab & Cloud Computing](#part-3-google-colab--cloud-computing)
6. [Part 4: Python for ML Crash Course](#part-4-python-for-ml-crash-course)
7. [Lab Completion Checklist](#lab-completion-checklist)
8. [Submission Instructions](#submission-instructions)

---

## Learning Objectives

By the end of this lab, you will be able to:
- Set up a professional Python development environment using VS Code or Cursor
- Create and manage Python virtual environments with venv or Conda
- Perform basic Git operations (clone, commit, push) on GitHub
- Launch and configure Google Colab notebooks with GPU acceleration
- Manipulate multi-dimensional arrays using NumPy broadcasting
- Load, clean, and transform data using Pandas
- Create informative visualizations with Matplotlib and Seaborn

---

## Prerequisites

- A computer with at least 8GB RAM (Windows, macOS, or Linux)
- Administrator access to install software
- A Google account (for Colab and GitHub)
- Stable internet connection
- Basic familiarity with command line/terminal

---

## Part 1: Development Environment Setup

### 1.1 Installing Visual Studio Code

**Visual Studio Code (VS Code)** is a lightweight but powerful source code editor with excellent Python support.

**Installation Steps:**
1. Visit [https://code.visualstudio.com/](https://code.visualstudio.com/)
2. Download the appropriate version for your operating system
3. Run the installer and follow the setup wizard
4. **Windows users:** Check "Add to PATH" during installation

**Alternative: Cursor IDE**
- Cursor is an AI-powered fork of VS Code
- Download from [https://cursor.com/](https://cursor.com/)
- All VS Code instructions in this lab apply to Cursor as well

### 1.2 Installing Python

We'll use Python 3.10 or later for this course.

**Windows:**
1. Visit [https://www.python.org/downloads/](https://www.python.org/downloads/)
2. Download Python 3.10+ installer
3. **IMPORTANT:** Check "Add Python to PATH" during installation
4. Verify installation by opening Command Prompt and running:
   ```bash
   python --version
**macOS:**
   ```bash
   # Using Homebrew (recommended)
   brew install python@3.11
   
   # Verify installation
   python3 --version
   ```
**Linux (Ubuntu/Debian):**
   ```bash
   sudo apt update
   sudo apt install python3.11 python3.11-venv python3-pip
   python3 --version
   ```
### 1.3 Setting Up Python Virtual Environments

Virtual environments isolate project dependencies, preventing conflicts between different projects.

**Option A**: venv (Recommended for beginners)

**macOS/Linux:**
  ```bash
  # Navigate to your projects directory
  mkdir ~/ai_labs
  cd ~/ai_labs
  
  # Create virtual environment
  python3 -m venv ai_env
  
  # Activate virtual environment
  source ai_env/bin/activate
  
  # Your terminal prompt should now show (ai_env)
  ```
**Windows**
  ```bash
  # Create projects directory
  mkdir %USERPROFILE%\ai_labs
  cd %USERPROFILE%\ai_labs
  
  # Create virtual environment
  python -m venv ai_env
  
  # Activate virtual environment
  ai_env\Scripts\activate
  
  # Your terminal prompt should now show (ai_env)
  ```

**Option B**: Conda (Recommended for data science)
1. Download and install Miniconda from [https://www.anaconda.com/docs/getting-started/miniconda/main](https://www.anaconda.com/docs/getting-started/miniconda/main)
2. Create and activate environment:
   ```bash
   # Create environment with Python 3.11
   conda create -n ai_env python=3.11
   
   # Activate environment
   conda activate ai_env
    ```
### 1.4 Installing Required Python Packages
With your virtual environment activated, install the essential libraries:
  ```bash
    pip install numpy pandas matplotlib seaborn jupyter notebook
  ```
Or for Conda users:
  ```bash
  conda install numpy pandas matplotlib seaborn jupyter notebook
  ```

### 1.5 Configuring VS Code for Python

#### 1. Install Python Extension

- Open VS Code
- Click Extensions icon (`Ctrl+Shift+X` / `Cmd+Shift+X`)
- Search for **"Python"** by Microsoft
- Click **Install**

#### 2. Select Python Interpreter

- Press `Ctrl+Shift+P` (`Cmd+Shift+P` on Mac)
- Type `"Python: Select Interpreter"`
- Choose your newly created environment (`ai_env`)

#### 3. Install Additional Extensions

- **Jupyter** (by Microsoft) — For notebook support
- **Python Docstring Generator** — For documentation
- **GitLens** — Enhanced Git capabilities

### 🟢 Exercise 1: Environment Verification (Completion Check)
Create a file named `environment_test.py` and verify your setup works:

```python
"""
environment_test.py
Lab 0 - Environment Verification Script
Verify that all required packages are installed and accessible.
"""

import sys
import platform
import os

def verify_environment():
    """Verify Python environment and package installations."""
    
    results = []
    
    # Check Python version
    python_version = sys.version.split()[0]
    results.append(f"✅ Python Version: {python_version}")
    
    # Check operating system
    results.append(f"✅ OS: {platform.system()} {platform.release()}")
    
    # Required packages with versions
    required_packages = {
        'numpy': 'NumPy',
        'pandas': 'Pandas',
        'matplotlib': 'Matplotlib',
        'seaborn': 'Seaborn'
    }
    
    for package_name, display_name in required_packages.items():
        try:
            module = __import__(package_name)
            version = getattr(module, '__version__', 'unknown')
            results.append(f"✅ {display_name}: {version}")
        except ImportError:
            results.append(f"❌ {display_name}: NOT INSTALLED")
    
    # Check virtual environment
    in_venv = hasattr(sys, 'real_prefix') or (
        hasattr(sys, 'base_prefix') and sys.base_prefix != sys.prefix
    )

    in_conda = 'CONDA_PREFIX' in os.environ
    
    if in_venv:
        results.append(f"✅ Virtual Environment: Active ({sys.prefix})")
    elif in_conda:
        results.append(f"✅ Conda Environment: Active ({os.environ['CONDA_PREFIX']})")
    else:
        results.append("⚠️  Virtual Environment: Not active")
    
    return "\n".join(results)

if __name__ == "__main__":
    print("=" * 50)
    print("LAB 0: ENVIRONMENT VERIFICATION")
    print("=" * 50)
    print(verify_environment())
    print("=" * 50)
```

To submit: Run this script and save the output as `environment_verification.txt`

## Part 2: Git & GitHub Fundamentals

Git is a version control system that tracks changes in your code. GitHub is a cloud platform for hosting Git repositories.

**Installation:**

- Windows: Download from https://git-scm.com/

- macOS: brew install git

- Linux: sudo apt install git

**Initial Configuration:**
  ```bash
  # Configure your identity
  git config --global user.name "Your Full Name"
  git config --global user.email "firstname.surname@ashesi.edu.gh"
  
  # Configure default branch name
  git config --global init.defaultBranch main
  
  # Verify configuration
  git config --list
  ```

### 2.2 Creating a GitHub Account

1. Visit https://github.com/

2. Click "Sign up" and follow registration

3. Use your university email for student benefits

4. Apply for GitHub Student Developer Pack: https://education.github.com/pack


### 2.3 Basic Git Workflow

**Cloning a Repository**

  ```bash
  # Clone an existing repository
  git clone https://github.com/username/repository-name.git
  cd repository-name
  ```

**Creating Your First Repository**

  ``` bash
  # Create a new directory and initialize Git
  mkdir lab0-git-practice
  cd lab0-git-practice
  git init
  
  # Create a README file
  echo "# Lab 0: Git Practice" > README.md
  echo "This is my first Git repository for the AI course." >> README.md
  
  # Stage and commit the file
  git add README.md
  git commit -m "Initial commit: Add README"
  
  # Create a .gitignore file for Python
  echo "__pycache__/" > .gitignore
  echo "*.pyc" >> .gitignore
  echo ".DS_Store" >> .gitignore
  echo "ai_env/" >> .gitignore
  
  git add .gitignore
  git commit -m "Add Python .gitignore"
  ```

**Pushing to GitHub**
  ```bash
  # Create a repository on GitHub first, then:
  git remote add origin https://github.com/your-username/lab0-git-practice.git
  git branch -M main
  git push -u origin main
  ```
  
**Essential Git Commands Cheatsheet**

```bash
git status                # Check repository status
git add <file>            # Stage changes
git add .                 # Stage all changes
git commit -m "message"   # Commit with message
git push                  # Push to remote
git pull                  # Pull latest changes
git log --oneline         # View commit history
git diff                  # See unstaged changes
```

### 🟢 Exercise 2: Git Practice Repository (Completion Check)

**Tasks to complete:**

1. Create a new GitHub repository named `ai-course-lab0`

2. Clone it to your local machine

3. Create the following structure:
    ```text
    ai-course-lab0/
    ├── README.md
    ├── .gitignore
    ├── environment_test.py
    └── notebooks/
        └── python_basics.ipynb
    ```
4. Add a README.md with:
    - Course name and semester
    - Your name and student ID
    - A brief description of what this repository will contain
  
5. Stage, commit, and push all files to GitHub
6. Submit the repository URL in your lab submission

## Part 3: Google Colab & Cloud Computing

### 3.1 Introduction to Google Colab

Google Colaboratory is a free cloud-based Jupyter notebook environment that provides GPU and TPU access—essential for deep learning tasks later in the course.

**Key Features:**

- Free GPU/TPU access

- No local setup required

- Easy sharing and collaboration

- Integration with Google Drive

- Pre-installed ML libraries

### 3.2 Getting Started with Colab

1. Visit https://colab.research.google.com/
2. Sign in with your Google account
3. Create a new notebook: File → New Notebook

### 3.3 Enabling GPU Acceleration

For deep learning tasks, you'll need GPU access:

- Runtime → Change runtime type

- Select T4 GPU from the dropdown

- Click Save

Verify GPU access:
``` bash
!nvidia-smi
```

### 3.4 Colab Features to Know

**Mounting Google Drive:**
```python
from google.colab import drive
drive.mount('/content/drive')
```
**Installing packages:**
```python
!pip install package-name
```
**Uploading files:**
```python
from google.colab import files
uploaded = files.upload()
```

### 3.5 Colab vs Local Development

| Feature | Google Colab | Local Environment |
|---|---|---|
| GPU Access | Free T4 | Requires hardware purchase |
| Persistence | Temporary (12hr max) | Permanent |
| Internet Required | Yes | No |
| Storage | 15GB Google Drive | Local disk |
| Customization | Limited | Full control |

### 🟢 Exercise 3: Colab Exploration (Completion Check)
1. Create a new Colab notebook

2. In the first cell, add a markdown header: # Lab 0: Colab Practice - [Your Name]

3. Run code cells that demonstrate:

    - Checking GPU availability
    
    - Mounting Google Drive
    
    - Installing a package (!pip install wordcloud)
    
    - Creating a simple word cloud (copy code below)

4. Save notebook to your Google Drive

5. Download as .ipynb file for submission

```python
# Cell 1: Verify environment
import sys
print(f"Python version: {sys.version}")
print(f"Running on Colab: {'google.colab' in sys.modules}")

# Cell 2: Check GPU
import subprocess
gpu_info = subprocess.run(['nvidia-smi'], 
                         capture_output=True, text=True)
if gpu_info.returncode == 0:
    print("GPU Available:")
    print(gpu_info.stdout)
else:
    print("No GPU detected - enable in Runtime > Change runtime type")

# Cell 3: Create a word cloud
from wordcloud import WordCloud
import matplotlib.pyplot as plt

text = "Artificial Intelligence Machine Learning Deep Learning Neural Networks Python Data Science"
wordcloud = WordCloud(width=800, height=400, 
                     background_color='white').generate(text)

plt.figure(figsize=(10, 5))
plt.imshow(wordcloud, interpolation='bilinear')
plt.axis('off')
plt.title('AI Course Word Cloud')
plt.show()
```

## Part 4: Python for ML Crash Course

This section provides a rapid refresher on the Python libraries essential for AI/ML coursework.

### 4.1 NumPy Fundamentals

NumPy is the foundation of numerical computing in Python, providing efficient array operations.

**Creating Arrays**

```python
import numpy as np

# Creating arrays
arr1 = np.array([1, 2, 3, 4, 5])
arr2 = np.zeros((3, 4))          # 3x4 array of zeros
arr3 = np.ones((2, 3))           # 2x3 array of ones
arr4 = np.random.randn(3, 3)     # 3x3 random normal
arr5 = np.arange(0, 10, 2)       # [0, 2, 4, 6, 8]
arr6 = np.linspace(0, 1, 5)      # 5 evenly spaced values

print(f"Shape of arr2: {arr2.shape}")
print(f"Dimensions: {arr2.ndim}")
print(f"Data type: {arr3.dtype}")
```

**Array Indexing and Slicing**
```python
arr = np.array([[1, 2, 3, 4],
                [5, 6, 7, 8],
                [9, 10, 11, 12]])

print(arr[0, 0])        # First element: 1
print(arr[:, 1])        # Second column: [2, 6, 10]
print(arr[1:3, 2:4])    # Rows 1-2, cols 2-3
print(arr[arr > 5])     # Boolean indexing: [6, 7, 8, 9, 10, 11, 12]
```
**Broadcasting**

Broadcasting allows operations between arrays of different shapes:

```python
# Broadcasting example
matrix = np.array([[1, 2, 3],
                   [4, 5, 6],
                   [7, 8, 9]])
vector = np.array([10, 20, 30])

# Broadcasting adds vector to each row
result = matrix + vector
print(result)
# [[11, 22, 33],
#  [14, 25, 36],
#  [17, 28, 39]]

# Normalization using broadcasting
data = np.random.randn(100, 5)
normalized = (data - data.mean(axis=0)) / data.std(axis=0)
```

**Matrix Operations**

```python
A = np.array([[1, 2], [3, 4]])
B = np.array([[5, 6], [7, 8]])

# Matrix multiplication
C = A @ B  # or np.matmul(A, B)

# Element-wise multiplication
D = A * B

# Transpose
A_T = A.T

# Inverse (requires square, non-singular matrix)
A_inv = np.linalg.inv(A)

# Determinant
det_A = np.linalg.det(A)

# Eigenvalues and eigenvectors
eigenvalues, eigenvectors = np.linalg.eig(A)
```

### 4.2 Pandas Fundamentals

Pandas provides powerful data structures for data manipulation and analysis.

**DataFrames and Series**

```python
import pandas as pd

# Creating a DataFrame
data = {
    'Name': ['Alice', 'Bob', 'Charlie', 'Diana'],
    'Age': [25, 30, 35, 28],
    'Score': [85.5, 92.0, 78.5, 95.5]
}
df = pd.DataFrame(data)

# Creating a Series
scores = pd.Series([85.5, 92.0, 78.5, 95.5], name='Score')

# Basic DataFrame operations
print(df.head(2))        # First 2 rows
print(df.info())         # Data types and memory usage
print(df.describe())     # Statistical summary
print(df.shape)          # (4, 3) - rows, columns
```

**Data Loading and Inspection**


```python
# Reading CSV files
df = pd.read_csv('data.csv')

# Reading Excel files
df = pd.read_excel('data.xlsx', sheet_name='Sheet1')

# Quick inspection
df.head(10)          # First 10 rows
df.tail(5)           # Last 5 rows
df.columns           # Column names
df.dtypes            # Data types
df.isnull().sum()    # Count missing values
```

**Data Manipulation**

```python
# Filtering
high_scorers = df[df['Score'] > 90]

# Multiple conditions
selected = df[(df['Age'] > 25) & (df['Score'] > 80)]

# Adding new columns
df['Passed'] = df['Score'] >= 80

# Grouping and aggregation
df.groupby('Department')['Salary'].agg(['mean', 'std', 'count'])

# Sorting
df_sorted = df.sort_values('Score', ascending=False)

# Handling missing values
df_clean = df.dropna()                    # Drop rows with NaN
df_filled = df.fillna(df.mean())          # Fill with mean
```

**Merging and Joining**

```python
df1 = pd.DataFrame({'ID': [1, 2, 3], 'Name': ['A', 'B', 'C']})
df2 = pd.DataFrame({'ID': [1, 2, 4], 'Score': [90, 85, 88]})

# Inner join
inner = pd.merge(df1, df2, on='ID', how='inner')

# Left join
left = pd.merge(df1, df2, on='ID', how='left')
```

### 4.3 Matplotlib and Seaborn

Visualization is crucial for understanding data and model behavior.

**Matplotlib Basics**

```python

import matplotlib.pyplot as plt

# Create figure and axis
fig, ax = plt.subplots(figsize=(10, 6))

# Line plot
x = np.linspace(0, 10, 100)
y = np.sin(x)
ax.plot(x, y, label='sin(x)', color='blue', linewidth=2)
ax.set_xlabel('X-axis')
ax.set_ylabel('Y-axis')
ax.set_title('Sine Wave')
ax.legend()
ax.grid(True)
plt.show()

```

**Common Plot Types**

```python
# Scatter plot
plt.scatter(df['Age'], df['Score'], alpha=0.6)
plt.xlabel('Age')
plt.ylabel('Score')
plt.title('Age vs Score')

# Histogram
plt.hist(df['Score'], bins=10, edgecolor='black')

# Bar plot
categories = ['A', 'B', 'C', 'D']
values = [23, 45, 56, 78]
plt.bar(categories, values, color=['red', 'blue', 'green', 'orange'])

# Box plot
plt.boxplot(df['Score'])
```

**Seaborn for Statistical Visualization**

```python
import seaborn as sns

# Set style
sns.set_style("whitegrid")
sns.set_palette("husl")

# Load sample dataset
tips = sns.load_dataset("tips")

# Distribution plot
sns.histplot(data=tips, x='total_bill', kde=True)

# Scatter with regression line
sns.regplot(data=tips, x='total_bill', y='tip')

# Categorical plot
sns.boxplot(data=tips, x='day', y='total_bill')

# Correlation heatmap
correlation = tips.corr()
sns.heatmap(correlation, annot=True, cmap='coolwarm')

# Pairplot (for multiple variables)
sns.pairplot(tips, hue='smoker')
```

## 🟢 Graded Exercises (100 Points Total)
Complete these exercises in a Jupyter notebook named lab0_exercises.ipynb and submit it as part of your lab materials.

### Exercise 4: NumPy Array Operations (20 points) 

```python
"""
Exercise 4: NumPy Array Operations
Complete the following tasks using NumPy.
"""

# Task 1: Create a 5x5 matrix where border elements are 1 and interior is 0
# (5 points)
# TODO: Create the matrix described above
# Hint: Use np.ones and array slicing

# Task 2: Normalize a random array
# (5 points)
np.random.seed(42)
random_data = np.random.randn(100, 3)
# TODO: Normalize each column to have mean=0 and std=1

# Task 3: Implement linear regression solution using normal equation
# (10 points)
# Given X (features) and y (target), compute theta
# theta = (X^T X)^(-1) X^T y
X = np.random.randn(50, 3)
true_theta = np.array([2.5, -1.2, 3.7])
y = X @ true_theta + np.random.randn(50) * 0.1
# TODO: Calculate theta_hat using the normal equation
# TODO: Print the estimated coefficients and compare with true_theta 
```

### Exercise 5: Pandas Data Analysis (30 points)

```python
"""
Exercise 5: Pandas Data Analysis
Analyze a dataset of student performance.
"""

import pandas as pd
import numpy as np

# Create sample dataset
np.random.seed(42)
n_students = 200

data = {
    'student_id': range(1000, 1000 + n_students),
    'major': np.random.choice(['CS', 'Math
        ', 'Physics', 'Biology'], n_students),
    'year': np.random.choice([1, 2, 3, 4], n_students),
    'exam_score': np.random.normal(75, 10, n_students).clip(0, 100),
    'assignments_completed': np.random.randint(0, 11, n_students),
    'hours_studied': np.random.normal(15, 5, n_students).clip(1, 40)
}

df = pd.DataFrame(data)

# Introduce some NaN values
df.loc[np.random.choice(n_students, 10), 'exam_score'] = np.nan
df.loc[np.random.choice(n_students, 5), 'hours_studied'] = np.nan

# Task 1: Data Cleaning and Exploration (10 points)
# TODO: Display basic information about the dataset
# TODO: Identify and count missing values
# TODO: Fill missing exam_score with the mean score for the student's major
# TODO: Fill missing hours_studied with the median for the student's year

# Task 2: Analysis (10 points)
# TODO: Calculate and display the average exam_score by major
# TODO: Find the major with the highest average exam_score
# TODO: Calculate the correlation between hours_studied and exam_score
# TODO: Create a new column 'performance' with categories:
#       'Excellent' (>90), 'Good' (80-90), 'Average' (70-80), 'Needs Improvement' (<70)

# Task 3: Advanced Analysis (10 points)
# TODO: For each major and year combination, calculate:
#       - Number of students
#       - Average exam score
#       - Average hours studied
# TODO: Identify top 5 students based on exam_score (handle ties appropriately)
# TODO: Create a pivot table showing average exam_score by major (rows) and year (columns)
```

### Exercise 6: Data Visualization (25 points)

```python
"""
Exercise 6: Data Visualization
Create meaningful visualizations using the dataset from Exercise 5.
"""

import matplotlib.pyplot as plt
import seaborn as sns

# Continue using the df from Exercise 5

# Task 1: Distribution Visualization (8 points)
# TODO: Create a figure with 2 subplots side by side
#       Left: Histogram of exam scores with KDE overlay
#       Right: Box plot of exam scores by major
# TODO: Add appropriate titles, labels, and styling

# Task 2: Relationship Visualization (8 points)
# TODO: Create a scatter plot of hours_studied vs exam_score
# TODO: Color points by major
# TODO: Add a regression line
# TODO: Include appropriate legends, titles, and axis labels

# Task 3: Advanced Dashboard (9 points)
# TODO: Create a 2x2 subplot figure containing:
#       1. Bar chart: Average exam score by major
#       2. Count plot: Number of students by year
#       3. Heat map: Correlation matrix of numerical columns
#       4. Violin plot: Exam score distribution by performance category
# TODO: Adjust layout, add titles, and ensure readability
```

### Exercise 7: Integration Challenge (25 points)

```python
"""
Exercise 7: Integration Challenge
Combine NumPy, Pandas, and Matplotlib to solve a mini data science problem.
"""

# Scenario: You're analyzing customer data for an e-commerce company.
# Generate synthetic data and provide insights.

np.random.seed(42)
n_customers = 500

# Generate customer data
ages = np.random.randint(18, 70, n_customers)
income = np.random.normal(50000, 20000, n_customers).clip(15000, 150000)
purchase_freq = np.random.poisson(5, n_customers)
avg_purchase_value = np.random.normal(100, 30, n_customers).clip(10, 500)

# Create DataFrame
customers = pd.DataFrame({
    'age': ages,
    'income': income,
    'purchase_frequency': purchase_freq,
    'avg_purchase_value': avg_purchase_value
})

# TODO: Calculate customer lifetime value (CLV)
#       CLV = purchase_frequency * avg_purchase_value * (1 + churn_risk)
#       where churn_risk = 1 - (purchase_frequency / max_frequency)

# TODO: Create age groups: 18-25, 26-35, 36-50, 51-70

# TODO: For each age group, calculate:
#       - Number of customers
#       - Average income
#       - Average CLV
#       - Total CLV

# TODO: Identify top 10% of customers by CLV

# TODO: Create visualizations:
#       1. Scatter plot of income vs CLV (color by age group)
#       2. Bar chart of average CLV by age group
#       3. Correlation heatmap

# TODO: Write a brief analysis paragraph (as a markdown cell)
#       summarizing key findings and recommendations
```

### Lab Completion Checklist

Before submitting, ensure you have completed all items:

### Required Submissions

- environment_verification.txt - Output from Exercise 1

- GitHub repository URL (Exercise 2)

    - Repository must contain: README.md, .gitignore, environment_test.py
    
    - At least 2 meaningful commits

- colab_practice.ipynb - Downloaded Colab notebook (Exercise 3)

- lab0_exercises.ipynb - Completed graded exercises (Exercises 4-7)

### Optional but Recommended

- VS Code or Cursor IDE installed and configured

- Python extension and Jupyter extension installed

- Git configured with your university email

- GitHub Student Developer Pack applied

- Bookmarked Google Colab


### File Naming Convention

```text
Lastname_Firstname_Lab0/
├── environment_verification.txt
├── colab_practice.ipynb
├── lab0_exercises.ipynb
└── README.md (optional summary and the link to the github repository in Exercise 2)
```
