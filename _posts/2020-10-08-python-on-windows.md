```
---
title: "Getting Started with Python on Windows"
categories: [Beginner, Python, Anaconda, Conda, Virtual Environments]
---
```

# Getting Started with Python on Windows

Reading python how-to guides, blogs and even tweets often gives the illusion that all things python take place entirely on Linux and Mac OS.  I'm on windows 99% of the time when using python and happy to report it works great. There is a bit of a lingering stigma regarding python on windows because there was a time when getting python installed and setup on a windows machine was a quite a hassle. Those days are over. In fact, there are more windows users than mac users according to the [JetBrains](https://www.jetbrains.com/2019) survey of 24k python users:

![image](images\python_platform.png)



Good news, that is absolutely no longer the case. However, I do think getting started with Python on windows can be a bit confusing. The goal of this post is to give a brief, but opinionated summary of how to go from never having touched python to running code in a jupyter notebook ASAP.

## Where to get Python

Google something along the lines of "install python windows" and you'll get python.org, closely followed by realpython.com and then a Microsoft page suggesting a python download from the Microsoft Appstore. Instead of these options, seek out [Anaconda](https://www.anaconda.com/products/individual). This is a cross-platform solution to getting python installed and running with ease.

The Anaconda distribution includes:

* The latest version of python (create an environment for other versions needed - more on that to come)
* [`conda` command line tool](https://docs.conda.io/projects/conda/en/latest/index.html)
* [A substantial set of pre-installed packages](https://docs.anaconda.com/anaconda/packages/py3.8_win-64/) (particularly useful for scientific computing or data science)
* [Anaconda Navigator](https://docs.anaconda.com/anaconda/navigator/) (for those that prefer a GUI to launch python based tools)

> Note: that if you desire a lighter weight version of Anaconda without the pre-installed packages consider [miniconda](https://docs.conda.io/en/latest/miniconda.html)

## Starting Jupyter

[Jupyter Notebooks and Jupyter Lab](https://jupyter.org/) are an approachable way to get started writing some code for beginners, as well as a fantastic way to combine data visualization with text and blocks of code for more experienced users.

To get started either launch anaconda navigator from the start menu, or open a command line terminal, navigate to your working directory and open by either `jupyter notebook`or `jupyter lab`.

> For some the command line terminal is unfamiliar or intimidating - instead jupyter notebook or lab can be launched from the file explorer with the same command (`juptyer notebook` or `jupter lab`) entered in the address bar:
>
> <img src="images\explorer.png" alt="image" style="zoom:50%;" />
>
> 



## Virtual Environments with <img src="C:\code-dev\geostats.dev\WIP\md\images\1280px-Conda_logo.svg.png" alt="image" style="zoom:10%;" />

A virtual environment can be thought of as an isolated install of python with a set of packages separate from the system (or user) -wide install. A virtual environment provides the freedom to work on projects that require a different version of python, or necessitate package(s) of different versions despite the latest and greatest that was installed with the Anaconda download. Additionally, a virtual environment can be replicated in another location or on another machine ensuring the ability to run your code wherever its needed.

### Environment Setup

Creating a new environment is simple

```conda env create -n mynewenv``` (replacing mynewenv with a more appropriate name).

Anytime you want to use this environment, activate it

```conda activate mynewenv```

Once activated, anytime you call `python` or it will call the version specific to that environment, isolated from the global install. 

> **Note:** Using Jupyter (Notebook or Lab) within a Conda Environment requires an extra step.
>
> If you want to use your conda environment in a jupyter notebook :
>
> `conda install ipykernel nb_conda_kernels`	
>
> * **ipykernel** provides everything you need to run jupyter from your new environment
> * **nb_conda_kernels** provides the added bonus of being able to access other conda environments on your system from within jupyter

### Copying an Environment

Ultimately,  you'll want to share your code with a friend or colleague to replicate some python workflow on a new machine or new data elsewhere. Using a Virtual Environment makes this easy. To replicate an environment, simply record all packages being used and their version number.  To clone an environment on the same machine:

`conda create --name myenvclone --clone myoldenv`

Conda also provides a convenient way to export all the pertinent information to a YAML file. From within the environment you'd like to copy:

`conda env export > environment.yml` 

Now, take this `environment.yml` and recreate that exact same environment on a different machine:

`conda env create -f environment.yml`

> **Note:** The YAML approach for saving environment information does not replace the standard `requirements.txt` that is common with `pip`. Instead, the conda approach is best suited for exactly the process described above: cloning an environment. Same name, all the same packages etc. `requirements.txt` is best suited for a list dependencies required for some package, stopping short of creating an entire environment.



# Conclusion

Python works great on windows, don't let anyone tell you otherwise. If you're working on windows, especially in the realm of scientific computer or data science, Anaconda is highly recommended. Once you've got Anaconda set up and are comfortable with the basics, consider working a virtual environment for most things you're doing. Does absolutely every bit of code need its own environment, definitely not but for any substantial project its highly recommended.