# Python PIP Cheatsheet

## 1. What is PIP?

PIP stands for **Pip Installs Packages**.

It is Python's package manager used to install, upgrade, uninstall and manage external Python libraries.

Examples:
- numpy
- pandas
- matplotlib
- requests
- pytest

**Remember:**
- PIP = Python package installer.
- PyPI = Python Package Index (online package repository).
- venv = Creates an isolated Python environment.

---

## 2. Check PIP and Python Version

```bash
pip --version
python --version
python -m pip --version
```

Find the location of pip and Python:

```bash
which pip
which python
```

---

## 3. Install Packages

Install a single package:

```bash
pip install numpy
```

Install multiple packages:

```bash
pip install numpy pandas matplotlib
```

Install a specific version:

```bash
pip install numpy==2.0.0
```

Install a minimum version:

```bash
pip install "numpy>=1.26"
```

Install within a version range:

```bash
pip install "numpy>=1.26,<3.0"
```

Install or upgrade to the latest compatible version:

```bash
pip install --upgrade numpy
```

Install without using the cache:

```bash
pip install --no-cache-dir numpy
```

---

## 4. Upgrade PIP

Upgrade pip itself:

```bash
python -m pip install --upgrade pip
```

Check the installed version:

```bash
pip --version
```

---

## 5. Uninstall Packages

Uninstall a package:

```bash
pip uninstall numpy
```

Uninstall without confirmation:

```bash
pip uninstall -y numpy
```

Uninstall multiple packages:

```bash
pip uninstall numpy pandas matplotlib
```

---

## 6. List Installed Packages

Display all installed packages:

```bash
pip list
```

Display packages with their versions:

```bash
pip freeze
```

Show details of a particular package:

```bash
pip show numpy
```

Check package dependencies:

```bash
pip show requests
```

Check dependency conflicts:

```bash
pip check
```

---

## 7. requirements.txt

A `requirements.txt` file stores project dependencies.

Generate requirements.txt:

```bash
pip freeze > requirements.txt
```

Install dependencies from requirements.txt:

```bash
pip install -r requirements.txt
```

Example requirements.txt:

```text
numpy==2.2.0
pandas==2.2.3
matplotlib==3.10.0
pytest==8.3.4
```

**Why is this useful?**

When someone clones your GitLab/GitHub repository, they can install all required dependencies using:

```bash
pip install -r requirements.txt
```

---

## 8. Install Packages from Different Sources

Install directly from GitHub:

```bash
pip install git+https://github.com/user/repository.git
```

Install from a local directory:

```bash
pip install .
```

Install in editable mode:

```bash
pip install -e .
```

Editable installation is useful during development because changes to your project source code are reflected without reinstalling the package.

---

## 9. Important PIP Flags

| Flag | Purpose |
|---|---|
| `-r` | Install packages from requirements file |
| `-U` | Upgrade package |
| `-y` | Automatically confirm uninstall |
| `-v` | Verbose output |
| `-q` | Quiet output |
| `--no-cache-dir` | Disable package cache |
| `--user` | Install packages for current user |
| `--force-reinstall` | Reinstall a package |
| `--no-deps` | Install without dependencies |
| `--upgrade-strategy` | Control dependency upgrades |
| `--pre` | Include pre-release versions |

Examples:

```bash
pip install -U numpy
pip install -v pandas
pip install --force-reinstall numpy
pip install --no-deps numpy
```

---

## 10. PIP vs PYTHON -m PIP

Both commands install packages:

```bash
pip install numpy
```

```bash
python -m pip install numpy
```

However, using:

```bash
python -m pip install numpy
```

is generally safer because it runs pip using the Python interpreter specified by `python`.

This helps avoid installing packages into the wrong Python environment.

---

## 11. Common Errors

### Error 1: externally-managed-environment

This error can occur when installing packages globally on Ubuntu.

Solution:

```bash
python3 -m venv .venv
source .venv/bin/activate
python -m pip install numpy
```

### Error 2: No module named numpy

Install the missing package:

```bash
pip install numpy
```

Make sure you are using the correct virtual environment.

### Error 3: Permission denied

Avoid using:

```bash
sudo pip install numpy
```

Instead, activate your virtual environment and install packages there.

### Error 4: Wrong package version

Check the installed version:

```bash
pip show numpy
```

Install the required version:

```bash
pip install numpy==1.26.4
```

---

## 12. Typical Project Workflow

```bash
# Create project directory
mkdir my_project

# Navigate into project
cd my_project

# Create virtual environment
python3 -m venv .venv

# Activate environment
source .venv/bin/activate

# Upgrade pip
python -m pip install --upgrade pip

# Install dependencies
pip install numpy pandas matplotlib

# Check installed packages
pip list

# Save dependencies
pip freeze > requirements.txt

# Deactivate environment
deactivate
```

---

