
# SaxaVord Earth Observation Challenge

# Jupyter Setup

Below contains the instructions for either running the project on your local machine, or on UoE's cloud jupyter notebook service Noteable

## Jupter on your Local Machine
* We assume either Anaconda or Jupyter + Pip configuration is installed on your laptop.  
  If not: https://docs.anaconda.com/anaconda/install/index.html

* We assume Git command-line setup.
  If not: https://product.hubspot.com/blog/git-and-github-tutorial-for-beginners

* Clone the code repo from: https://github.com/rwilks-earthobs/msc_eo_challenge

* Download the **starter_data** folder from (Ed Auth required, Access ends on Tuesday): https://uoe-my.sharepoint.com/:f:/g/personal/s2448783_ed_ac_uk/EtSOQI6UNp5Oi60_FA5lK8ABrcy8QsMge5gPs1PlQ3VnCw?e=tnes2r

* Put the unzipped starter_data folder into your local repo. 

* Manually unzip each folder within **starter_data/sentinel2/**, making sure unzipped folders remain here also.

* Navigate via Terminal (Mac) or Command Prompt (Windows) to the root of the cloned repo on your machine
```bash
cd Path\\To\\msc_eo_challenge   
## for Mac replace \\ with /
```

* Create and activate a virtual environment to ensure clean package management using Conda (preferable) or Pip if not
```bash
# Conda
 conda env create --file=saxavord.yml
 conda activate saxa_env
```
```bash
# PIP
 python -m venv saxa_env
 saxa_env\\Scripts\\activate ## For Mac: source venv/bin/activate 
 pip install -r requirements.txt

```
* Launch jupyter from inside your virtual environment
```bash
jupyter notebook
```
<br />

## Cloud Jupyter on UoE Notable

* Noteable spins up a virtual machine and jupyter notebook instance. 
    * **Pros:** Potentially more space than your local machine
    * **Cons:** Times you out after 1hour of inactivity, including leaving calculations to run.  Packages will need to be reinstall everytime the notebook is restarted.
* Access: https://noteable.edina.ac.uk/launch

* In the dropdown below *'Please select a personal notebook server'* select **GeoScience Notebook** and press Start

* Select **+GitRepo** and in *Git Repository URL* put: https://github.com/rwilks-earthobs/msc_eo_challenge . You can leave the other sections blank, and select **Clone**

* This should copy over the repo directly into the notebook.

* Download the **starter_data** folder from (Ed Auth required, Access ends on Tuesday): https://uoe-my.sharepoint.com/:f:/g/personal/s2448783_ed_ac_uk/EtSOQI6UNp5Oi60_FA5lK8ABrcy8QsMge5gPs1PlQ3VnCw?e=tnes2r

* Put the unzipped starter_data folder into the repo on noteable 

* Install packages for use via the command in jupyter
```python
!pip install -r requirements.txt
```
* Note that the filepaths & commands on noteable use the Mac variant (as opposed to Windows above)

* Jupyter has no manual unzip functionality, so this needs to be done programatically in the notebook

```python
## Imports
import os
from zipfile import ZipFile

## Helper functions
def unzip_folder(fp_in, fp_out):
    '''
     Function to take a folder at filepath_in (fp_in) and unzips it to filepath_out (fp_out)
     
     Ideally should be 
       fp_in  = Path/To/Folder.zip
       fp_out = Path/To/Folder
    '''
    with ZipFile(fp_in, 'r') as zip_ref:
        zip_ref.extractall(fp_out)

## Params        
# set data folder
sen2dir = './starter_data/sentinel2/'


## Run Unzip Process
# get list of files & folders within this folder
lst = os.listdir(sen2dir) 

# for each file, if zip folder, unzip
for file in lst:
    
    # Get complete filepath
    file = sen2dir + file
    print(f'Unzipping {file}')
    
    # Unzip if file ends in '.zip' (note this will override any previous unzip)
    if file.endswith('.zip'):
        fp_in = file
        fp_out = file[:-4]
        unzip_folder(fp_in, fp_out)


```

 



<br />
<br />
<br />






# Downloading More Data
Work with the existing data provided should provide something to work with, however if during the course of your analysis you would like to look at additional Sentinel 2 data and Landsat data, there are guides provided in the repo:

    How to Access Sentinel 2 Data - Copernicus Open Access Hub.pdf

    How to Access Landsat Data - USGS EarthExplorer.pdf



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
