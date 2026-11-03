# Python Virtual Environment (venv) Cheatsheet

## 1. What is a Virtual Environment?

A virtual environment is an isolated Python environment for a project.

It allows each project to have its own:
- Python packages
- Dependencies
- Package versions

**Why use it?**

Suppose:
- Project A requires `numpy==1.26`
- Project B requires `numpy==2.0`

Without virtual environments, package versions can conflict.

With virtual environments, each project manages its own dependencies.

---

## 2. Create a Virtual Environment

Navigate to your project directory:

```bash
cd my_project
```

Create a virtual environment:

```bash
python3 -m venv .venv
```

Alternative:

```bash
python -m venv .venv
```

`.venv` is the environment directory name. You can also use `venv`.

---

## 3. Activate Virtual Environment

### Linux / Ubuntu / macOS

```bash
source .venv/bin/activate
```

### Windows (CMD)

```cmd
.venv\Scripts\activate.bat
```

### Windows (PowerShell)

```powershell
.venv\Scripts\Activate.ps1
```

After activation, you will see something like:

```bash
(.venv) varad@laptop:~/my_project$
```

The `(.venv)` indicates that the virtual environment is active.

---

## 4. Deactivate Virtual Environment

```bash
deactivate
```

This takes you back to your system Python environment.

---

## 5. Install Packages

First, activate your virtual environment.

Install a package:

```bash
pip install numpy
```

Install multiple packages:

```bash
pip install numpy matplotlib pandas
```

Install a specific version:

```bash
pip install numpy==1.26.4
```

Install the latest available version:

```bash
pip install --upgrade numpy
```

---

## 6. Check Installed Packages

List all installed packages:

```bash
pip list
```

Show details of a package:

```bash
pip show numpy
```

Check Python version:

```bash
python --version
```

Check which Python executable is being used:

```bash
which python
```

Check which pip is being used:

```bash
which pip
```

Both should point inside your `.venv` directory when the environment is activated.

---

## 7. requirements.txt

`requirements.txt` stores all project dependencies.

### Generate requirements.txt

```bash
pip freeze > requirements.txt
```

Example:

```text
matplotlib==3.10.0
numpy==2.2.0
pandas==2.2.3
```

### Install dependencies from requirements.txt

```bash
pip install -r requirements.txt
```

This is particularly useful when sharing projects with teammates.

---

## 8. Uninstall Packages

Uninstall a package:

```bash
pip uninstall numpy
```

Uninstall without confirmation:

```bash
pip uninstall -y numpy
```

---

## 9. Upgrade pip

```bash
python -m pip install --upgrade pip
```

Using `python -m pip` ensures that pip belongs to the Python interpreter you are using.

---

## 10. Delete a Virtual Environment

First deactivate it:

```bash
deactivate
```

Then delete the environment directory:

```bash
rm -rf .venv
```

Create it again whenever required:

```bash
python3 -m venv .venv
```

---

## 11. .gitignore Configuration

Never push your virtual environment to GitLab or GitHub.

Add this to `.gitignore`:

```gitignore
# Virtual environments
.venv/
venv/
env/

# Python cache
__pycache__/
*.py[cod]

# Environment variables
.env

# IDE settings
.idea/
.vscode/
```

Your teammates can recreate the environment using `requirements.txt`.

---

## 12. Typical Project Workflow

These are the commands you will use most frequently.

```bash
# 1. Create project directory
mkdir my_project

# 2. Navigate into project
cd my_project

# 3. Create virtual environment
python3 -m venv .venv

# 4. Activate virtual environment
source .venv/bin/activate

# 5. Upgrade pip
python -m pip install --upgrade pip

# 6. Install dependencies
pip install numpy matplotlib

# 7. Save dependencies
pip freeze > requirements.txt

# 8. Deactivate environment
deactivate
```

### When cloning an existing project

```bash
# Clone repository
git clone <repository-url>

# Enter project directory
cd project_name

# Create virtual environment
python3 -m venv .venv

# Activate
source .venv/bin/activate

# Install dependencies
pip install -r requirements.txt
```

---

## 13. Important Commands at a Glance

| Command | Purpose |
|---|---|
| `python3 -m venv .venv` | Create virtual environment |
| `source .venv/bin/activate` | Activate environment |
| `deactivate` | Deactivate environment |
| `pip install package` | Install package |
| `pip uninstall package` | Uninstall package |
| `pip list` | List installed packages |
| `pip show package` | Package information |
| `pip freeze` | List installed packages with versions |
| `pip freeze > requirements.txt` | Save dependencies |
| `pip install -r requirements.txt` | Install dependencies |
| `python -m pip install --upgrade pip` | Upgrade pip |
| `rm -rf .venv` | Delete virtual environment |
| `which python` | Find active Python executable |
| `python --version` | Check Python version |

---

## 14. Important Things to Remember

1. Create one virtual environment per project.
2. Always activate the environment before installing packages.
3. Keep `.venv/` inside `.gitignore`.
4. Commit `requirements.txt` to Git.
5. Never share or push the `.venv` directory.
6. Use `python -m pip` to avoid installing packages into the wrong Python environment.
7. When switching projects, make sure you activate the correct virtual environment.
