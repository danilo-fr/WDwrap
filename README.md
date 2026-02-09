# 🌀 WDwrap

WDwrap is a Python wrapper for the Wilson–Devinney (WD) code, designed to streamline the modeling and parameter inference of binary star systems. It provides a modern, Pythonic interface to the original Fortran-based WD engine, enabling efficient execution, automation, and statistical analysis of light curves and radial velocity data.

WDwrap integrates seamlessly with contemporary Python tools, including parallel execution and Bayesian inference via MCMC, allowing users to explore complex parameter spaces and derive robust posterior distributions for orbital and stellar parameters.

<p align="center">
  <img src="WDwrap.png" alt="" width="300">
</p>
------------------------------------------------------------
FEATURES
------------------------------------------------------------

- Python interface to the Wilson–Devinney Fortran code
- Automated setup and execution of WD runs
- Support for light curve and radial velocity modeling
- Bayesian parameter inference using MCMC (emcee)
- Parallel computing support
- Designed for eclipsing, interacting, and massive binary systems

------------------------------------------------------------
REQUIREMENTS
------------------------------------------------------------

External software:
- Wilson–Devinney code (compiled)
- Fortran compiler (e.g. gfortran)

Note:
WDwrap assumes that the WD executable is already compiled and accessible either in the working directory or in the system PATH.

------------------------------------------------------------
PYTHON DEPENDENCIES
------------------------------------------------------------

Python 3.8+ is required, along with the following packages:

numpy
scipy
matplotlib
pandas
emcee
corner
tqdm

Install using pip:

pip install numpy scipy matplotlib pandas emcee corner tqdm

------------------------------------------------------------
INSTALLATION
------------------------------------------------------------

Clone the repository:

git clone https://github.com/your-username/WDwrap.git
cd WDwrap

Make sure the WD executable is available:

export PATH=$PATH:/path/to/wd/executable

Alternatively, place the WD executable inside the project directory.

------------------------------------------------------------
BASIC USAGE
------------------------------------------------------------

1. Import WDwrap:

from wdwrap import WDModel

2. Define initial parameters:

params = {
    "period": 2.345,
    "inclination": 82.0,
    "t0": 2450000.0,
    "q": 0.75,
    "teff1": 22000,
    "teff2": 18000,
}

3. Load observational data:

import pandas as pd

lc = pd.read_csv("lightcurve.dat", names=["time", "flux", "flux_err"])
rv = pd.read_csv("rv.dat", names=["time", "rv", "rv_err"])

4. Initialize the model:

model = WDModel(
    parameters=params,
    lightcurve=lc,
    radial_velocity=rv,
    wd_path="./wd_executable"
)

5. Run a single WD solution:

model.run()

This step generates synthetic light curves and/or radial velocities using the WD engine.

------------------------------------------------------------
BAYESIAN INFERENCE WITH MCMC
------------------------------------------------------------

WDwrap supports parameter estimation using MCMC via emcee.

Example:

model.setup_mcmc(
    free_params=["inclination", "q", "teff2"],
    nwalkers=32
)

sampler = model.run_mcmc(
    nsteps=5000,
    ncores=8
)

Inspect posterior distributions:

import corner

samples = sampler.get_chain(discard=1000, flat=True)
corner.corner(samples, labels=["i", "q", "Teff2"])

------------------------------------------------------------
OUTPUT
------------------------------------------------------------

WDwrap automatically organizes outputs, including:

- WD input and output files
- Synthetic light curves and radial velocities
- MCMC chains and posterior samples
- Diagnostic plots

All results are stored in a structured directory to ensure reproducibility.

------------------------------------------------------------
SCIENTIFIC SCOPE
------------------------------------------------------------

WDwrap is particularly suited for:

- Eclipsing binary stars
- Interacting and semi-detached systems
- Massive binaries and early-type stars

------------------------------------------------------------
CITATION
------------------------------------------------------------

If you use WDwrap in your research, please cite:

Wilson, R. E. & Devinney, E. J. (1971), ApJ, 166, 605

and include a reference to this repository.

------------------------------------------------------------
LICENSE
------------------------------------------------------------

Choose a license and add it here.

