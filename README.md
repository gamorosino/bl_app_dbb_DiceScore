# bl_app_dbb_DisSeg

This application computes the Dice similarity coefficient (DSC) between two segmentation volumes (parcellations)

### Author

    Gabriele Amorosino (gamorosino@fbk.eu)

## Running the Brainlife App


You can run the BrainLife App `DBB_DiceScore` on the brainlife.io platform via the web user interface (UI) or using the `brainlife CLI`.  With both of these two solutions, the inputs and outputs are stored on the brainlife.io platform, under the specified project, and the computations are performed using the brainlife.io cloud computing resources.


### On Brainlife.io via UI

You can see _DBB_DiceScore_ currently registered on Brainlife. Find the App on _brainlife.io_ and click "Execute" tab and specify dataset e.g. "DBB Distorted Brain Benchmark".

### On Brainlife.io using CLI

Brainlife CLI could be installed on UNIX/Linux-based system following the instruction reported in https://brainlife.io/docs/cli/install/.

you can run the App with CLI as follow:
```
bl app run --id   --project <project_id> --input computed:<parc_object_id> --input ground_truth:<parc_object_id> 
```
the output is stored in the reference project specified with the id ```<project_id>```. You can retrieve the _object_id_ using the command ```bl data query```, e.g to get the id of the segmentation volume files for the subject _0001_ :
```
bl data query --subject 0001 --datatype "neuro/parcellation/volume"  --project <projectid>
```

If not present yet, you can upload a new file in a project using ```bl data upload```. For example, in the case of the segmentation volume, for the subject 0001 you can run:
```
bl data upload --project <project_id> --subject 0001 --datatype "neuro/parcellation/volume" --t1 <full_path> --tag "computed"

```
## Running the code locally

You can run the code on your local machine by git cloning this repository. You can choose to run it with _dockers_, avoiding to install any software except for [singularity](https://sylabs.io/). Furthermore, you can run the original script using local software installed.

### Run the script using the dockers (recommended)

It is possible to run the app locally, using the dockers that embedded all needed software. This is exactly the same way that apps run code on brainlife.io

Inside the cloned directory, create `config.json` with something like the following content with the fullpaths to your local input files:
```
{   
    "computed": "./segmentation.nii.gz",
    "ground_truth": "./parc.nii.gz"
}
```

Launch the app by executing `main`.
```
./main
```
To avoid using the config file, you can input directly the fullpath of the filess using the script ```main.sh```:

```
main.sh <computed.ext> <ground_truth.ext> [<output.txt>]
```

#### Script Dependecies

The App needs   `singularity` to run.

#### Output

The output of bl_app_dbb_DisSeg is a _.txt_ file, reporting the dice score of each label separated but a space and sort as the labels value. The file is stored in the working directory.


### Run the script (local installed softwares) 

Clone this repository using git on your local machine to run this script.

### Usage


```

main_local.sh <computed.ext> <ground_truth.ext> [<output.txt>]

```

#### Output

The output of bl_app_dbb_DisSeg is a _.txt_ file, reporting the dice score of each label separated but a space and sort as the labels value. The file is stored in the working directory.


####  Script Dependecies

It is necessary that Python 2.7.x is installed, with the following modules:

* nibabel=2.5.1 
* numpy

It is suggested to install python modules using conda. 
```
conda  conda install -c conda-forge nibabel=2.5.1 \
      && conda install numpy
```