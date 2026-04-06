[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-22041afd0340ce965d47ae6ef1cefeee28c7c493a6346c4f15d667ab976d596c.svg)](https://classroom.github.com/a/6OJMKMJx)
# MAE223 — Week 1: Time Series Analysis

Starter repository for the Week 1 Time Series Analysis lab.

## Files

| File | Description |
|------|-------------|
| `Tidal Analysis_Python.ipynb` | **Start here** — fully written demo notebook |
| `Tutorial_SpectralAnalysis.ipynb` | **Then here** — hands-on tutorial, you write the code |
| `sample_data.json` | Velocity time series (CLASS10 mooring, 30-min sampling, 16,000 samples) |
| `la_jolla_tide.json` | NOAA La Jolla tide gauge sea level — full ~100-year record, hourly, in mm |
| `safari_waves.json` | SAFARI buoy significant wave height — central Pacific, Nov 2025–Apr 2026, ~2-hr sampling (Scripps/WHOI collaboration) |
| `environment.yml` | Conda environment specification |
| `github_tutorial.pdf` | Guide to GitHub and GitHub Classroom for first-time users |

---

## Setup (do this once)

### Step 0 — Create a GitHub account

You need a free GitHub account to access this assignment.

1. Go to [github.com](https://github.com) and click **Sign up**
2. Enter your email, a password, and a username
   - Your username will be visible to your instructor — keep it professional
   - Using your UCSD email is recommended but not required
3. Verify your email address when prompted
4. Once your account is active, click the assignment link posted on Canvas
5. Click **Accept this assignment** — GitHub Classroom will create a personal copy of this repository just for you
6. Wait a few seconds, then refresh — you will see a link to your own repo

> Your repo is an independent copy. Changes you make do not affect anyone else's, and no other student can see yours.

### What is a Jupyter Notebook?

A Jupyter Notebook is an interactive document that combines code, text, and figures in a single file (`.ipynb`). It is organized into **cells** — each cell contains either code or explanatory text, and you can run cells individually or all at once. When you run a code cell, the output (numbers, plots, etc.) appears directly below it. Notebooks are widely used in science and data analysis because they make it easy to write, run, and inspect code in small chunks.

### What is VS Code?

VS Code (Visual Studio Code) is a free code editor made by Microsoft. It can open and run Jupyter Notebooks directly. It is a popular alternative to running notebooks in a web browser (the classic JupyterLab interface). Both work with the same `.ipynb` files — the choice is just a matter of preference. For this course we use VS Code.

### What is a kernel?

A kernel is the Python engine that actually runs the code in your notebook. When you open a notebook you need to tell it which Python environment to use — in our case that is the `mae223` environment you will create below. Think of the kernel as the engine and the notebook as the dashboard.

---

### Step 1 — Install Miniconda

Miniconda is a lightweight Python package manager. It lets you create isolated Python environments so that different projects do not interfere with each other. **Skip this step if you already have Anaconda or Miniconda installed.**

**Mac:**
1. Go to https://docs.conda.io/en/latest/miniconda.html
2. Download the **macOS** installer — choose **Apple Silicon** if you have an M1/M2/M3/M4 Mac, otherwise choose **Intel**
3. Open the downloaded `.pkg` file and follow the prompts
4. Open a **Terminal** window: press `Cmd+Space`, type `Terminal`, and hit Enter
5. Type `conda --version` and press Enter — you should see something like `conda 24.x.x`

**Windows:**
1. Go to https://docs.conda.io/en/latest/miniconda.html
2. Download the **Windows 64-bit** installer (`.exe`)
3. Run the installer. When you reach the **Advanced Options** screen, check **"Add Miniconda3 to my PATH environment variable"**
4. Click through the remaining prompts and finish the installation
5. Open **Anaconda Prompt**: click the Windows Start menu, type `Anaconda Prompt`, and open it. A black window will appear — this is your command line and is what you will use for all terminal commands below
6. Type `conda --version` and press Enter — you should see something like `conda 24.x.x`

---

### Step 2 — Clone your repository

On your GitHub Classroom repo page, click the green **Code** button and copy the URL. Then in Terminal (Mac) or Anaconda Prompt (Windows) run:

```bash
git clone <your-repo-url>
```

This downloads all the files to your computer and keeps them connected to your GitHub repo. Navigate into the folder:

```bash
cd time-series-analysis-<your-username>
```

---

### Step 3 — Create the course environment

This installs all the Python packages needed for the lab into an isolated environment called `mae223`.

```bash
conda env create -f environment.yml
```

This may take a few minutes. When it finishes, run:

```bash
conda activate mae223
python -m ipykernel install --user --name mae223 --display-name "mae223"
```

The first command activates the environment. The second registers it as a kernel so VS Code can find it.

---

### Step 4 — Install VS Code

1. Download and install VS Code from https://code.visualstudio.com
2. Open VS Code and go to the **Extensions** panel — click the square icon on the left sidebar or press `Cmd+Shift+X` (Mac) / `Ctrl+Shift+X` (Windows)
3. Search for **Python** and click Install
4. Search for **Jupyter** and click Install
5. Restart VS Code after both extensions finish installing

---

### Step 5 — Open the notebooks

There are two notebooks and they should be done **in order**:

**1. `Tidal Analysis_Python.ipynb` — demo (start here)**
- Fully written — just run it and read the code and output
- Introduces the `spectrumCB` function, power spectral density, and tidal analysis
- No coding required — this is the "watch and understand" step

**2. `Tutorial_SpectralAnalysis.ipynb` — tutorial (do this second)**
- You write the code yourself, guided by prompts
- Builds directly on what the demo introduced
- Requires `la_jolla_tide.json` and `safari_waves.json` (both included in the repo)

The tutorial has two parts:

**Part 1 — Spectral Resolution**
Using the La Jolla tide gauge record, you will compute spectra with four different chunk sizes and compare them on a single plot. The goal is to build intuition for the tradeoff between frequency resolution and spectral stability — a core concept in Welch's method. Three reflection questions guide your interpretation, including a calculation of the minimum segment length needed to resolve the M₂ and S₂ tidal constituents.

**Part 2 — SAFARI Wave Analysis**
You will apply the full analysis pipeline to a new dataset: significant wave height (Hs) measured by a research buoy in the central North Pacific (33°25'N, 158°W) during the SAFARI 2025–2026 field campaign — a joint Scripps Institution of Oceanography and Woods Hole Oceanographic Institution (WHOI) collaboration. The data are transmitted via Iridium satellite and are irregularly sampled, so you will need to interpolate onto a regular time grid before computing the spectrum. You will then identify the dominant periods of wave height variability and compare the result to the tidal spectrum from the demo.

> **How to work through the tutorial:** Each code cell either contains fully written code (run it and read it) or has a `# YOUR CODE HERE` comment where you must write something. Read the markdown cells carefully before each exercise — they explain what you need to do and why. Answer the reflection questions in the provided answer cells.

**To open a notebook in VS Code:**
1. Open the repo folder: **File → Open Folder**, navigate to your `time-series-analysis` folder, and click Open
2. Click the notebook file in the left file panel
3. In the top-right corner click **Select Kernel → Select Another Kernel... → Jupyter Kernel... → mae223**
4. Click **Run All** to execute all cells

> **Note:** Always run cells from top to bottom. If you see a `NameError`, it usually means an earlier cell has not been run yet. Use **Run All** to avoid this.

---

### Step 6 — Save your work to GitHub

Push your changes to GitHub periodically as you work through the notebook — this keeps your code backed up and lets you pick up where you left off from any computer.

1. Open the Source Control panel in VS Code: click the branch icon on the left sidebar or press `Cmd+Shift+G` (Mac) / `Ctrl+Shift+G` (Windows)
2. You will see your modified notebook listed under **Changes**
3. Click the `+` icon next to the file to stage it
4. Type a short message describing what you did (e.g. `completed tidal spectrum section`) and click **Commit**
5. Click **Sync Changes** to push to your GitHub repo

You can push as many times as you like — each push saves a snapshot of your progress.

> **Note:** Lab reports are submitted through Canvas, not GitHub.
