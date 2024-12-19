# **Documentation: Starting a Python Project with Conda and Virtual Environments**

This guide provides a comprehensive roadmap to setting up a Python project using Conda or other virtual environments. It covers project structure, environment management, and best practices for organizing and managing dependencies.

---

## **1. Project Structure**

A well-organized project structure improves maintainability and collaboration. Below is a recommended structure:

```plaintext
pm_project/
│
├── pm_project/               # Source code folder
│   ├── __init__.py           # (Optional) Marks this as a Python package
│   ├── main.py               # Main script, entry point of the project
│   └── utils.py              # Helper functions (optional)
│
├── data/                     # (Optional) Folder for data storage
│   └── example.csv           # Example data file
│
├── .env                      # Environment variables (e.g., API keys)
├── requirements.txt          # Pip dependencies list
├── environment.yml           # Conda environment file
├── README.md                 # Project description/documentation
├── .gitignore                # Files and folders to exclude from version control
└── tests/                    # Unit tests (optional)
    └── test_main.py          # Example test file
```

Make sure to create a folder first for your project and then create a virtual environment there

## **2. Python Setup: Conda vs Other Virtual Environments**

Python virtual environments isolate dependencies, ensuring compatibility and avoiding conflicts.

### **Conda**
- **Advantages**:
  - Manages both Python versions and dependencies.
  - Handles non-Python dependencies (e.g., C libraries).
  - Suitable for data science and machine learning projects.
- **Disadvantages**:
  - Slightly larger footprint than `venv`.

### **`venv` or `virtualenv`**
- **Advantages**:
  - Lightweight and part of Python's standard library (`venv`).
  - Portable and compatible with `pip`.
- **Disadvantages**:
  - Requires manual installation of non-Python dependencies.

### **Recommendation**
Use Conda if your project involves data science or requires packages with complex dependencies (e.g., NumPy). Use `venv` for general-purpose projects.

---

## **3. Setting Up a Virtual Environment**

### **Using Conda**
1. **Install Conda** (if not already installed):
   - Install [Miniconda](https://docs.conda.io/en/latest/miniconda.html) or [Anaconda](https://www.anaconda.com/).

2. **Create a New Environment**:
   ```
   conda create --name pm_project_env python=3.9
   ```

3. **Activate the Environment**:

```
conda activate pm_project_env
```
4. **Install Dependencies**:

- **Using ```requirements.txt```**:

```
pip install -r requirements.txt
```

- **Or via ```environment.yml```**:
```
conda env create -f environment.yml
```

5. **Deactivate the Environment**:

```
conda deactivate
```

6. **Delete the Environment if something went wrong**

```
conda env remove --name pm_project_env
```

### **Using ```venv```**

1. **Create a Virtual Environment**:

```
python3 -m venv pm_project_env
```

2. **Activate the Environment**:

- **macOS/Linux**:
```
source pm_project_env/bin/activate
```

- **Windows**:
```
.\\pm_project_env\\Scripts\\activate
```

3. **Install Dependencies**:

```
pip install -r requirements.txt
```
4. **Deactivate the Environment**:

```
deactivate
```

## **4. Managing dependencies**

**Using ```requirements.txt```**
1. **Generate a ```requirements.txt``` file**:

```
pip freeze > requirements.txt
```

2. **Install dependencies from it**:

```
pip install -r requirements.txt
```

**Using Conda's ```environment.yml```**
1. **Generate an ```environment.yml``` file**:

```
conda env export --name pm_project_env > environment.yml
```

2. **Create a new environment from it**:

```
conda env create -f environment.yml
```

## **5. Working with .env for Secrets**
**Why Use ```.env```?**
The ```.env``` file securely stores sensitive information like API keys. Use the python-dotenv package to load variables into your script.

**Setting Up a ```.env``` File**
1. **Create a .env file in the project root**:

```
RAPIDAPI_KEY=bla-bla-key
AWS_ACCESS_KEY_ID=your_aws_access_key
AWS_SECRET_ACCESS_KEY=your_aws_secret_key
AWS_REGION=us-west-2
```

2. **Load ```.env``` in Your Script**:

```
from dotenv import load_dotenv
import os

load_dotenv()  # Load environment variables
api_key = os.getenv("RAPIDAPI_KEY")
aws_secret_key = os.getenv("AWS_SECRET_ACCESS_KEY")

print(f"API Key: {api_key}")
```

3. **Add ```.env``` to .gitignore**:

```
.env
```
## **6. Running the project**

**Running a Script**
- Activate your environment:

```
conda activate pm_project_env  # For Conda
source pm_project_env/bin/activate  # For venv
```

- Run your script:

```
python pm_project/main.py
```

**Running Unit Tests**
- Use ```pytest``` to run tests:
```
pytest tests/
```

## **6. Best Practices**

1. **Environment Isolation**: Always activate your environment before running scripts or installing packages.

2. **Version Control**: Use Git for version control. Exclude sensitive files (.env) and unnecessary directories (__pycache__, environment folders).

3. **Document Your Project**: Keep a detailed README.md to explain the project’s purpose, installation steps, and usage.

4. **Monitor Dependencies**: Regularly update requirements.txt or environment.yml to reflect the current state of your environment.

5. **Security**: Never hardcode sensitive data (e.g., API keys) in your scripts. Always use environment variables.

