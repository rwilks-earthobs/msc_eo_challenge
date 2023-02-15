
# SaxaVord Earth Observation Challenge

# Jupyter Setup

Below contains the instructions for either running the project on your local machine, or on UoE's cloud jupyter notebook service Noteable

## Jupter on your Local Machine
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
 conda env create --file saxavord.yml
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


## Cloud Jupyter on UoE Notable

TODO: Stuart providing access for this via LEARN
\
\
\
\





# Unzipping Data

* In your cloned repo the folder **starter_data.zip** contains your data and requires unzipping
* The unzipped folder should keep the same name **starter_data**
* This can be done manually in your folder explorer 

# Optional: Downloading More Data
Work with the existing data provided should provide something to work with, however if during the course of your analysis you would like to look at additional Sentinel 2 data, the guide provided in the repo:

    How to Access Sentinel 2 Data - Copernicus Open Access Hub.pdf

should provide support for this. 


# Troubleshooting: Filepath Too Long

* Satellite data is delivered in the nested folder structure you see in folders in **starter_data**
* This means files located within a deeper level will have very long filepaths
* This may throw errors
* If this is the case, then you can either:
    * Manually rename the top level folders within Sentinel_2, Landsat 
    * Use the code below to automatically remove all characters after and including '_N0400':


```python
import os

# Path from notebook to folder containing zipped folder for each day's data
s2_imgs_folder = '.\\starter_data\\sentinel2'

# TODO: Select your joiner - OS system dependant
# MAC 
#jn = '/'

# WINDOWS
jn = '\\'


# For each filename in the s2_imgs_folder, if it contains the string below, then shorten
for file_name in os.listdir(s2_imgs_folder):
    file = ''
    file = s2_imgs_folder + jn + file_name 

    # find index of character
    t = '_N0400'
    ind = file.find(t)

    # Renaming required
    if ind>=0:
        if file.endswith('zip'):
            file_new = file[:ind] + '.zip'
            
        else:
            file_new = file[:ind]
            
        #rename
        os.rename(file, file_new)
             
# Check name shortened, and folders unzipped correctly        
os.listdir(s2_imgs_folder)
```
