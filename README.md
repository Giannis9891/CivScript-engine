# CivScript-engine
The goal is to make engineering calculations reproducible, easy to test, and simple to demonstrate in a portfolio. 


CivScript Engine

A minimal, educational civil-engineering script engine combining JavaScript, gfortran, and Jupyter.



Prototype status: for learning and portfolio demonstration only. It is not a certified engineering design tool.



What it does


Reads a tiny .civ command script in JavaScript.

Calls a compiled Fortran numerical core for a simply supported beam's UDL maximum moment.

Provides a Jupyter notebook workflow for building, running, and checking the example.

Includes a small test suite and a Makefile.


Requirements


Node.js 18+

gfortran

GNU Make

Jupyter with a Python 3 kernel (optional, for notebooks)


Quick start

make
node src/js/main.js examples/beam_check.civ

Expected output (rounding may vary):


CivScript Engine
Beam: simply supported, full-span uniform load
Span: 6.000 m
Load: 12.000 kN/m
Maximum moment: 54.000 kN m
Status: DEMO ONLY — verify assumptions and units before engineering use.

Jupyter

Open notebooks/01_getting_started.ipynb. Run the cells from top to bottom. The notebook builds the Fortran executable, runs the JavaScript interpreter, and checks the expected result.


.civ language, v0.1

SET span 6.0
SET load 12.0
BEAM_MOMENT load span
DISPLAY

Commands:



SET name number — define a numeric variable.

BEAM_MOMENT load_variable span_variable — call the Fortran backend; assumes a simply supported beam with a full-span uniformly distributed load.

DISPLAY — print the last beam result.


The v0.1 parser is intentionally small: one command per line, numeric variables, no expressions, no units parser, and no arbitrary code execution.


Engineering formula

For a simply supported beam carrying a full-span uniformly distributed load (w):


[
M_{max} = \frac{wL^2}{8}
]


where w is in kN/m, L is in m, and the result is in kN m. The formula does not check shear, deflection, load combinations, material capacity, code requirements, or real support conditions.


Architecture


src/js/main.js: script reader, variable table, validation, and process bridge.

src/fortran/civil_core.f90: numerical routine and CLI entry point.

notebooks/: reproducible notebook workflow.

tests/: smoke test.

docs/: language and validation notes.


Safety and scope

This is a teaching prototype, not professional engineering software. Check units, assumptions, load cases, applicable design codes, and results independently before relying on any output. It does not replace review by a qualified engineer.


Suggested roadmap


Add dimensional units and expression parsing.

Add more verified Fortran routines (area, second moment of area, hydrostatic pressure).

Add JSON input/output for a stable interface.

Add property-based and reference-value tests.

Add plots and report generation in Jupyter.

Add CI builds for Linux/macOS/Windows.

