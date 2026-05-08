# Simulation Method Template for CHORAS

This is a [Copier](https://copier.readthedocs.io/) template for creating new simulation method packages for the CHORAS simulation backend.

## Features

This template creates the skeleton for a simulation method package with:

- **Package structure** including configuration files
- **Abstract base class** (`SimulationMethod`) which implements reading the input configuration and writing the results to the backend. 
- **CLI interface** to execute the method with entry points defined in `__cli__.py`, `__main__.py`
- **Test structure** with fixtures, conftest, and example test files, including `.geo` and `.json` test files
- **Docker** with a ready-to-use Dockerfile

## Prerequisites

Install Copier:

```bash
pip install copier
```

Or with uv:

```bash
uv tool install copier
```

## Usage

### Creating a New Simulation Method

From the `simulation-backend` directory, run:

```bash
copier copy simulation_method_template/ ./
```

Or from anywhere:

```bash
copier copy path/to/simulation_method_template/ path/to/output/
```

### Questions You'll Be Asked

Copier will ask you several questions to customize your interface.
These questions cover information about the author, 

- **author_name**: Your name
- **author_email**: Your email

the implemented method, 

- **method_name**: The name of your simulation method (e.g., "DG", "MyMethod")
- **method_name_lower**: Lowercase version (usually auto-generated)
- **method_description**: Brief description of your method
- **method_keywords**: Comma-separated keywords
- **method_class_name**: Main class name (e.g., "MyMethod")

and dependencies

- **python_version_min**: Minimum Python version (e.g., "3.11")
- **python_version_max**: Maximum Python version (optional)
- **additional_dependencies**: Extra packages needed (comma-separated)

**Note:** The template always includes `*.msh` and `*.geo` files (named `test_room_<method_name_lower>.*`) and `gmsh` as a dependency. Simply remove the `.msh` file if your method automatically generates mesh files based on the geometry data defined in the `*.geo` file.

**About gmsh initialization:** If your method requires `gmsh.initialize()` and `gmsh.finalize()`, add them in your simulation method implementation (not in the CLI). This keeps the CLI simple and allows better control over gmsh lifecycle.

### Example

```bash
$ copier copy simulation_method_template/ ./

🎤 Author name
   Your Name
🎤 Author email
   your.email@example.com
🎤 What is the name of your simulation method (e.g., "DG", "DE", "Pyroomacoustics")?
   MyMethod
🎤 What is the lowercase (snake_case) version of your method name (used for package naming)?
   mymethod
🎤 Brief description of your simulation method
   Python package for acoustic simulation using MyMethod
...
```

This will create a directory structure like:

```bash
mymethod_method/
├── Dockerfile
├── pyproject.toml
├── mymethod_interface/
│   ├── __init__.py
│   ├── __main__.py
│   ├── __cli__.py
│   ├── definition.py
│   └── mymethod_interface.py
└── tests/
    ├── conftest.py
    ├── test_definition.py
    ├── test_mymethod_cli.py
    ├── test_fixtures.py
    ├── test_input_mymethod.json
    └── test_room_mymethod.geo
```

