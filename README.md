# SandvikBush

[![Binder](https://mybinder.org/badge_logo.svg)](https://mybinder.org/v2/gh/judielaine/SandvikBush/HEAD?filepath=Our%20first%20joint%20notebook.ipynb)

This project is for Igguanna & Judielaine to share files.

You can look at a jupyter notebook without installing anything by going to [![Binder](https://mybinder.org/badge_logo.svg)](https://mybinder.org/v2/gh/judielaine/SandvikBush/HEAD?filepath=Our%20first%20joint%20notebook.ipynb) but we will find time to do get it running on your laptop.

## For Igguanna to try 

1. Open terminal. You can find the  application in /Applications/Utilities. This will take you to the "command line"
2. When you see text prefaced with a ">" and styled like `this` it is a command to be entered on the command line and then you hit the "return" key. For example try: 
   1. `> pwd`
   2. This is the "Present Working Directory" and it will display the path of where your command line session is active.
3. `> conda deactivate`
   1. When you run this you might get a `CommandNotFoundError` which is OK
4. `> conda update conda`
   1. I ended up with a ling list of things that needed to be downloaded, removed, installed, and upgraded. Enter "y" to make the changes take place.
5. `> conda update --update-all`
   1. I had one more file that needed changes 
6. Now open Anaconda Navigator app.
7. Switch to "Environments," make sure "base(root)" is selected (▶︎ next to it), ...

### not yet

1. Open Anaconda Navigator, go to "Environments", select "SandvikBush", and then  click "Remove" at the bottom of the environment list pane.
2. Once it's removed, click "Import" at the bottome of the environment list pane.
3. Name the environment (SandvikBush, again), then click on the black folder. A navigation finder window will open.
4. Navigate to the Github repository we share -- Something like Documents/GitHub/SandvikBush?
5. Once there, click on environment.yml & then "Open". 
6. The finder window will go away. Click on the green "Import" button.

### Not working yet

Now we are certain to have the same environments. It's still not working so we will try updating all the libraries in the senvironment. 

1. In the pane to the right of the environment list where all the packages are listed, there's the dropdown at the top which allows selecting "Installed" and "All"  as well as "Updatable."  Select "Updatable."
2. I have five packages to update. Click on the green checkbox and a menu will pop up -- select "Mark for update" for all five packages.
3. Click the green "Apply" in the bottom right. 
4. The dependency calculation pops up -- click "Apply" when it's done.

And then it seems nothing actually updates. Very odd.

![Update screen](20201227UpdateWeirdness.png)

Log message:

```json
[
    {
        "level": "WARNING",
        "line": 176,
        "message": "Line 6. Exception - Expecting ',' delimiter: line 1 column 259 (char 258)",
        "method": "load_log",
        "module": "logs",
        "path": "/opt/anaconda3/lib/python3.8/site-packages/anaconda_navigator/utils/logs.py",
        "time": "2020-12-27 21:28:48,285"
    }
]
```
Starting with [these instructions (https://docs.anaconda.com/anaconda/user-guide/tasks/use-jupyter-notebook-extensions/) i opened an environment terminal by using the green triangle next to the SandvikBush environement name, and entered `conda install nb_conda`



```
Preparing transaction: done
Verifying transaction: done
Executing transaction: - Enabling nb_conda_kernels...
CONDA_PREFIX: /opt/anaconda3/envs/SandvikBush
Status: enabled

/ Config option `kernel_spec_manager_class` not recognized by `EnableNBExtensionApp`.
Enabling notebook extension nb_conda/main...
      - Validating: OK
Enabling tree extension nb_conda/tree...
      - Validating: OK
Config option `kernel_spec_manager_class` not recognized by `EnableServerExtensionApp`.
Enabling: nb_conda
- Writing config: /opt/anaconda3/envs/SandvikBush/etc/jupyter
    - Validating...
      nb_conda 2.2.1 OK

done
```

## Judith will help

- Anaconda
  - [ ] ensure appropriate packages came with Anaconda for Jupyter notebooks: 
    - [ ] Create new environment with nbconda, numpy, nb_conda, matplot..., pandas, pintpandas
  - [ ] [notebook extensions](https://docs.anaconda.com/anaconda/user-guide/tasks/use-jupyter-notebook-extensions/)
    - [ ] Codefolding, collapsable headings, nbextensions dashboard tab, nbextensions edit menu option, python markdown


## Things That Have Gone Wrong

- Notebook Refuses To Start
![errormessage](Error%20Message%2012:27.png)
  - First hit seems to be in the right ballpark ["this is an issue with the nb_conda package"](https://github.com/Anaconda-Platform/nb_conda_kernels/issues/78) -- maybe i had us add the wrong module. What i really want is just the nbextension library, which this adds, but with more stuff. 
  - I have reinstalled Anaconda and now have the issue where 
- Anaconda Navigator won't run updates.
  - Version 1.10.0 on 2021-01-05, Environment view, "base(root)" environment, updating the index and selcting "Updatable" reveals 115 packages to be updated. I picked the first 57, clicked "Apply", the "Solving package specifications" ran, and then no packages were identified. This repeated only selecting anaconda-project 0.8.4, only selecting jupyter_core.
  - now trying command line
    1. conda update --prefix /opt/anaconda3 anaconda
       - now 31 packages updatable
    2. conda update --update-all
    3. conda update conda

## 2021-01-23 Effort

- starting at the ground level:
  - verified i was not in a conda environment by running `conda deactivate` at the command line.
  - `conda update conda`
    - >> `Solving environment:` 
      `Warning: 2 possible package resolutions (only showing differing packages): conda-forge/osx-64::ipykernel-5.4.3-py38h9bb44b7_0, conda-forge/osx-64::pyzmq-20.0.0-py38h1cb0b96_1  conda-forge/osx-64::ipykernel-5.4.2-py38h9bb44b7_0, conda-forge/osx-64::pyzmq-21.0.1-py38h1cb0b96done`
  - there's a LONG list of packages to download, a list of NEW packages to be INSTALLED,  a long list of upgrades, and a list of downgrades.
  - 11:28 entering y. Distracted and was done when i checked at 11:36
  - again `conda update conda`
    - "# All requested packages already installed."
  - opening anaconda & checking output of `conda info` against pre upgrade. Not significantly different.
- launching notebook from base environment. Used upper right button to "REFRESH". Then clicked little gear in right corner of Jupyter Notebook button to "upgrade". It's churning away. 11:43
  - found log `tail .anaconda/navigator/logs/navigator.log `
    - `{"time": "2021-01-23 11:44:27,506", "level": "WARNING", "module": "logs", "method": "load_log", "line": 176, "path": "/opt/anaconda3/lib/python3.8/site-packages/anaconda_navigator/utils/logs.py", "message": "Line 6. Exception - Expecting ',' delimiter: line 1 column 259 (char 258)"}`
  - restarting anaconda navigator It really seems like jupyter notebook could/should be upgraded. In light blue `↗︎6.2.0` is displayed. Other tools that appear to be at latest version show the version in a dark number and the only option for the gear icon is to install a specific version. Launching shows a progress bar with "Launching **Notebook**" briefly, no log messages, no result.

  Need to make final environment and then `conda env export --from-history -f environment.yml`
