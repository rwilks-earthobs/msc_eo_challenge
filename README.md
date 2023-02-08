
# SaxaVord Earth Observation Challenge

## Setup

Below contains the instructions for either running the project on your local machine, or on UoE's cloud jupyter notebook service Noteable

## A) Local Machine

* We assume either Anaconda or Jupyter + Pip configuration is installed on your laptop.  
  If not: https://docs.anaconda.com/anaconda/install/index.html

* We assume Git command-line setup.
  If not: https://product.hubspot.com/blog/git-and-github-tutorial-for-beginners

* Clone the code repo from: https://github.com/rwilks-earthobs/msc_eo_challenge

* Download the data from: https://github.com/rwilks-earthobs/msc_eo_challenge_data

* From the download, move the folder **Faroe Islands Satellite Data** into the root of the cloned **msc_eo_challenge** folder. 

    **!NOTE!: Do not rename any of the sub-folders within the Satellite Data folder, all of this is handled in the script**

* Navigate via Terminal (Mac) or Command Prompt (Windows) to the root of the cloned repo on your machine
```bash
cd Path/To/msc_eo_challenge   ## for windows, replace / with \\
```

* Create and activate a virtual environment to ensure clean package management using Conda (preferable) or Pip if not
```bash
# Conda
 conda env create --name saxa_env --file=saxavord.yml
 conda activate saxa_env
```
```bash
# PIP
 python -m venv saxa_env
 venv\Scripts\activate ##Activates the env - windows or venv/bin/activate for Mac
 pip install -r requirements.txt

```
* Launch jupyter from inside your virtual environment
```bash
jupyter notebook
```


## B) Noteable Cloud 
