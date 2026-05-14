# CMPINF-2100 Setup Guide

A step-by-step guide for setting up Anaconda, creating your course environment, and running your first Jupyter notebook. Covers **Windows**, **Linux**, and **macOS** in that order.

By the end of this guide, you'll have:

- Anaconda installed
- A conda environment named `upitt` with Python 3.10.20 and the course's packages
- JupyterLab running in your browser
- A working notebook with code you can run

The guide uses a consistent format:

- **Type:** what to type or paste
- **Press:** what key to press
- **You should see:** what to expect after

At each step, there are sections for each operating system. Read only the one that matches yours.

---

## Step 1: Open your terminal

You'll be doing most of this work in a terminal. Every operating system has one. They just look slightly different and live in different places.

### Windows

After Anaconda is installed (Step 2), you'll use the **Anaconda Prompt**, which is a terminal pre-configured for conda. For now, you'll briefly use the **regular Command Prompt** to verify your install.

To open Command Prompt:

```
Press: Windows key
Type: cmd
Press: Enter
```

A black window opens. That's your terminal.

### macOS

```
Press: Cmd+Space
Type: terminal
Press: Enter
```

A window opens with a prompt that looks something like `yourname@your-mac ~ %`. That's your terminal.

You may want to keep Terminal in your Dock for easy access: right-click its Dock icon → Options → Keep in Dock.

### Linux (Ubuntu / Debian / Fedora / most distros)

The exact shortcut varies by distribution, but most ship with a "Terminal" application accessible through the activities/applications menu. On most modern Linux systems:

```
Press: Ctrl+Alt+T
```

If that doesn't work, search your applications menu for "Terminal" or "Console."

---

## Step 2: Download and install Anaconda

### Windows

1. Open a web browser and go to **https://www.anaconda.com/download**
2. Download the **Windows 64-bit installer** (`.exe` file). It's about 1 GB.
3. Double-click the downloaded `.exe` to start the installer.
4. Walk through the installer:
   - **License Agreement:** Agree
   - **Install Type:** "Just Me" (recommended)
   - **Install Location:** Default (`C:\Users\<your-username>\anaconda3\`) is fine
   - **Advanced Options:** Leave both boxes at their defaults. Do NOT check "Add Anaconda to my PATH environment variable" (Windows will warn you against this; listen to it).
   - Click **Install**. It takes a few minutes.
5. When the installer finishes, you can skip the optional extras it offers (DataSpell trial, learning resources, etc.).

After install, look in your Start Menu for a new folder called **Anaconda3 (64-bit)**. Inside, you'll find **Anaconda Prompt**: that's the terminal you'll use for everything conda-related from now on.

### macOS

1. Open a web browser and go to **https://www.anaconda.com/download**
2. Download the macOS installer matching your chip:
   - **Apple Silicon** (M1/M2/M3/M4): `arm64` version
   - **Intel Mac**: `x86_64` version

   Not sure which you have? Apple menu → About This Mac. The line about "Chip" tells you (Apple Silicon will say "M1," "M2," etc.; Intel will say "Intel Core...").

3. Double-click the downloaded `.pkg` file in your Downloads folder.

   If macOS refuses to open it ("Apple could not verify..."), right-click the file → **Open** instead. That bypasses the stricter check.

4. Walk through the installer (Continue, Continue, Agree, Install). The defaults are correct.

5. When the installer says "Installation was successful," close it.

6. **Quit Terminal completely** with `Cmd+Q` (not just closing the window; Mac apps keep running when you close their last window). Reopen Terminal. This forces a fresh shell that knows about the new conda install.

### Linux

The cleanest way on Linux is to use the official Anaconda installer script:

1. Open a web browser and go to **https://www.anaconda.com/download**
2. Download the **Linux 64-bit installer** (a `.sh` file, about 1 GB).
3. In your terminal, navigate to where the file downloaded (usually `~/Downloads/`):
   ```
   Type: cd ~/Downloads
   Press: Enter
   ```
4. Run the installer:
   ```
   Type: bash Anaconda3-*.sh
   Press: Enter
   ```
   The `*` is a wildcard: your shell substitutes the actual filename.
5. Walk through the installer:
   - Press Enter to read the license, then space to scroll
   - When asked to accept, type `yes` and press Enter
   - Accept the default install location (`~/anaconda3`) by pressing Enter
   - When asked **"Do you wish to update your shell profile to automatically initialize conda?"**, type `yes` and press Enter. This is important.
6. **Close your terminal and reopen it.** This is required: the installer modified your shell's startup file (`~/.bashrc` or `~/.zshrc`) and your current shell hasn't loaded the changes.

---

## Step 3: Verify conda is working

### Windows

Open **Anaconda Prompt** from the Start Menu (not the regular Command Prompt this time; Anaconda Prompt is pre-configured for conda).

```
Type: conda --version
Press: Enter
You should see: conda 25.x.x (or similar)
```

Your prompt should begin with `(base)`, like `(base) C:\Users\you>`. That `(base)` means you're inside conda's default environment.

### macOS / Linux

In your terminal (fresh one, after restarting):

```
Type: conda --version
Press: Enter
You should see: conda 25.x.x (or similar)
```

Your prompt should begin with `(base)`, like `(base) you@yourmachine ~ %` on Mac or `(base) you@yourmachine:~$` on Linux.

**If you see "command not found"** instead of a version number on any platform, conda isn't set up in your shell. Try:

- **Windows:** Make sure you opened **Anaconda Prompt** specifically, not the regular Command Prompt.
- **macOS/Linux:** Close your terminal completely and reopen it. If still failing, the installer skipped the shell-init step. Run (Mac): `/opt/anaconda3/bin/conda init zsh` or (Linux): `~/anaconda3/bin/conda init bash`. Then close and reopen terminal.

Don't proceed past this step until `conda --version` prints a version.

---

## Step 4: Create the course environment

This step is identical on all three operating systems. The command creates a new conda environment named `upitt` with Python 3.10.20 and the course's required packages.

```
Copy & Paste:
conda create -n upitt python=3.10.20 jupyterlab "numpy<2" "pandas<3" matplotlib scikit-learn -c conda-forge
```

**Before pressing Enter, look at the command in your terminal.** It must be on one continuous line, ending with `scikit-learn -c conda-forge`. If your paste introduced line breaks or got truncated, retry the paste. If it looks correct:

```
Press: Enter
```

Conda will think for 30–60 seconds ("Solving environment...") and then show a long list of packages it plans to install. It asks:

```
Proceed ([y]/n)?
```

```
Type: y
Press: Enter
```

Wait several minutes for downloads and installation. Total download is roughly 500 MB. You'll see progress bars and `done` messages. When everything finishes, your prompt returns to a clean `(base)` state.

---

## Step 5: Activate the environment

```
Type: conda activate upitt
Press: Enter
```

Your prompt should change. Where it previously said `(base)`, it now says `(upitt)`. That's how you know which environment is active.

You're now using the `upitt` environment: different Python interpreter, different packages, completely isolated from `(base)` and from any other environment you create later.

---

## Step 6: Verify the environment

Check the Python version:

```
Type: python --version
Press: Enter
You should see: Python 3.10.20
```

If you see a different version, something went wrong with Step 4. Retry it.

Check that key packages installed correctly:

```
Copy & Paste: python -c "import pandas; print('pandas:', pandas.__version__); import numpy; print('numpy:', numpy.__version__)"
Press: Enter
```

You should see two lines printed:

```
pandas: 2.x.x   (some 2.x version, probably 2.2 or 2.3)
numpy: 1.x.x    (some 1.x version, probably 1.26)
```

If all three checks pass (Python 3.10.20, pandas 2.x, numpy 1.x), the environment is correctly set up.

---

## Step 7: Launch JupyterLab

Make sure your prompt still shows `(upitt)`. If it shows `(base)`, run `conda activate upitt` again.

It's a good idea to first move into the folder where you want your course work to live. For example, if you've made a folder for the course inside Documents:

### Windows

```
Type: cd "C:\Users\<your-username>\Documents\CMPINF-2100"
Press: Enter
```

Replace `<your-username>` with your actual Windows username, and adjust the path to wherever you want your course files. If the folder doesn't exist yet, create it through File Explorer first.

### macOS

```
Type: cd ~/Documents/CMPINF-2100
Press: Enter
```

Create the folder first (Finder → Documents → File → New Folder) if it doesn't exist.

### Linux

```
Type: cd ~/Documents/CMPINF-2100
Press: Enter
```

Create it first with `mkdir -p ~/Documents/CMPINF-2100` if it doesn't exist.

### All platforms: launch JupyterLab

```
Type: jupyter lab
Press: Enter
```

The terminal will print several lines of startup messages. After a few seconds, your default web browser opens to JupyterLab.

If the browser doesn't open automatically, look in the terminal output for a line like:
```
http://localhost:8888/lab?token=...
```
Copy that whole URL and paste it into your browser.

**Important things to know:**

- The terminal window where you launched JupyterLab is now running the **server**. Don't close it. Closing it shuts JupyterLab down.
- Your browser tab is the **interface** to the server. You can have multiple browser tabs open looking at different notebooks; they all talk to the same server.
- On macOS, the first time you launch JupyterLab, you may see a security prompt asking whether to allow incoming network connections. Click **Allow**. (It's just connecting to itself on your local machine, but macOS treats any local web server this way.)
- On Linux, no firewall prompt usually appears. JupyterLab just opens.
- On Windows, you may see a Windows Defender Firewall prompt the first time. Click **Allow access**.

---

## Step 8: Create your first notebook

You should now be looking at JupyterLab in your browser. The left side shows a file browser (currently empty if your course folder is fresh). The center area shows a "Launcher" with tiles for different things you can create.

### Create a new notebook

In the Launcher, find the **Notebook** section near the top. Click the **Python 3 (ipykernel)** tile.

A new notebook opens. It's titled "Untitled.ipynb" by default. Rename it to something more useful:

1. In the left file browser, right-click on `Untitled.ipynb` → **Rename**.
2. Type a new name like `first-notebook.ipynb`. Keep the `.ipynb` extension.
3. Press Enter.

### Run your first cell

You should see an empty cell with a blinking cursor. Click into it if not, and type:

```python
print("Hello, world!")
```

To run the cell:

```
Press: Shift+Enter
```

Below the cell, you should see:
```
Hello, world!
```

A new empty cell appears below. Congratulations. You've run your first notebook cell.

---

## Step 9: Understand how notebooks actually work

This part isn't a step to perform; it's a concept to internalize. It will save you hours of confusion over the rest of the semester.

### Cells don't run automatically in order

When you ran `print("Hello, world!")` with Shift+Enter, that one cell executed. Nothing else did. If you had ten cells in the notebook, only the cell you ran would have executed.

This is fundamentally different from a Python script, where the whole file runs top to bottom every time. In a notebook, **only the cells you explicitly run actually execute**, and they execute in the order you run them, not the order they appear on screen.

### Variables live in the kernel, not in cells

Try this. In the empty cell below your "Hello" cell, type:

```python
name = "John"
```

```
Press: Shift+Enter
```

You'll see no output. That's normal. The assignment ran, but it didn't print anything.

In the next empty cell, type:

```python
print(name)
```

```
Press: Shift+Enter
```

You should see:
```
John
```

The `name` variable was created in cell 2 and used in cell 3. Both cells are using the same **kernel**: the Python process running in the background that holds all your variables and imports.

You can also do this:

```python
name = name + " Doe"
print(name)
```

```
Press: Shift+Enter
```

You should see:
```
John Doe
```

If you run that same cell **again** with Shift+Enter, you'll see:
```
John Doe Doe
```

And again:
```
John Doe Doe Doe
```

Each time you run the cell, it appends "Doe" to whatever `name` currently is. The cell isn't isolated. It reads and modifies a variable that persists in the kernel between runs.

### The `[N]` counter tells you the execution order

Look to the left of each cell. You'll see `[N]` where N is a number, like `[1]`, `[2]`, `[3]`. This is the **execution counter**: it tells you the order in which cells were actually run. A cell that hasn't been run shows `[ ]` (empty).

If your cells show numbers in funny orders (`[3]`, `[1]`, `[5]`, `[2]` going down the page), it means you've been running cells out of order. That's fine while you're exploring, but it can cause confusion: your notebook's visible code may not match what the kernel actually thinks the variables are.

### "Restart and Run All" is your reality check

When you're done working on a notebook and want to make sure it actually works the way it looks:

```
Click: Kernel menu (top of the notebook)
Click: Restart Kernel and Run All Cells...
```

This wipes the kernel's memory and runs every cell from top to bottom, in order. If the notebook produces correct output after this, it's reproducible. If something breaks, you've been relying on kernel state that the code itself doesn't recreate.

**Always do this before submitting an assignment.** The grader's environment will run your notebook the same way: fresh kernel, top to bottom. If your notebook only works because of accumulated state from running cells out of order during development, the grader will see failures.

---

## Step 10: When you're done working

Save your notebook:

```
Press: Ctrl+S (Windows/Linux) or Cmd+S (macOS)
```

Or use the File menu → Save Notebook.

Shut down JupyterLab cleanly:

1. Go back to the terminal window where you ran `jupyter lab`.
2. Press `Ctrl+C` (this works on all platforms; even on Mac, Ctrl+C in the terminal is still Ctrl+C, not Cmd+C).
3. The server asks: `Shutdown this notebook server (y/[n])?`
4. Type `y` and press Enter.

You can also just close the terminal window; that kills the server too. The save-first matters more than the shutdown-cleanliness.

---

## How to use the environment going forward

Each time you want to do coursework, you'll do this short sequence:

### Windows

1. Open **Anaconda Prompt** from the Start Menu.
2. `cd` to your course folder: `cd C:\Users\<you>\Documents\CMPINF-2100`
3. `conda activate upitt`
4. `jupyter lab`

### macOS / Linux

1. Open Terminal.
2. `cd` to your course folder: `cd ~/Documents/CMPINF-2100`
3. `conda activate upitt`
4. `jupyter lab`

That's the whole workflow. The first time it takes a minute to remember; after a week it's muscle memory.

---

## Troubleshooting

**`conda: command not found` (or "is not recognized" on Windows).**
You're not in the right terminal, or your shell didn't initialize conda. On Windows, make sure you opened Anaconda Prompt, not Command Prompt. On Mac/Linux, close and reopen your terminal completely.

**`jupyter: command not found` after activating upitt.**
The environment didn't get created with JupyterLab inside it. Re-run Step 4. Make sure the conda create command included `jupyterlab` and that you said `y` to install.

**JupyterLab opens but cells don't run / show errors about kernel.**
Click the kernel selector (top right of the notebook view) and pick the Python kernel. If only one kernel option is available, click it and try running a cell again. If problems persist, Kernel menu → Restart Kernel.

**Cell shows `[*]` next to it and never finishes.**
The cell is still running. Some computations take a while. If it's been stuck for many minutes on something that should be fast, the kernel may be hung. Kernel menu → Interrupt Kernel. If that doesn't help, Restart Kernel.

**Notebook seems to "remember" wrong values.**
Almost always a kernel state issue. Kernel menu → Restart Kernel and Run All Cells. This refreshes everything.

**"Installation failed" when running the Anaconda installer (any platform).**
Usually means a previous Anaconda install is already present and the new installer is refusing to overwrite it. If you have working conda from a previous install, you don't need to reinstall: skip ahead to Step 4. If you have a *broken* previous install you need to remove, ask in the cohort channel or office hours rather than deleting things on your own. The right cleanup commands differ by platform and getting them wrong can affect other software.

**JupyterLab can't reach the kernel / network errors.**
On Windows, check that you allowed access through Windows Defender Firewall. On Mac, check System Settings → Network → Firewall and allow Python/Jupyter. On Linux, this is rarely an issue.

---

## Questions or improvements

This guide is maintained by Victor S. [@DatJavaClass](https://github.com/DatJavaClass) for the CMPINF-2100 2027 cohort. If something doesn't match what you're seeing, or you have a suggestion, open an issue on the repo or message me in our cohort channels.
