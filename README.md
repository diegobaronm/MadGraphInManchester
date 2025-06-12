# MadGraph in Manchester
These are instructions for the setup of a MadGraph environment in the Manchester Noether cluster.

NOTE: To be able to work in the Manchester cluster you need to be connected either to the University VPN or be in campus.

## Login to the Noether cluster
To connect via an ssh do:
```
ssh <your_username>@noether.hep.manchester.ac.uk
```
and then type your password. You will land in your `HOME` directory, if you do
```
pwd
```
you will see as output `/gluster/home/<your_username>`.


You also have a `DATA` directory. This is where you should store the results of your simulations: `/gluster/data/atlas/<your_username>`

## Login and working nodes

The Manchester HEP cluster has a login node and working nodes. You can only run jobs/code in the working nodes. To get to a working node do:
```
condor_submit -i  getenv=True request_cpus=8
```

You will land in a temporary scratch disk location. To go back to your `HOME` directory just do:
```
cd
```

## Download and run MadGraph

### Download

To download the latest MadGraph version do (at the time of writing these instructions it was `v3.6.2`):
```
wget https://launchpad.net/mg5amcnlo/3.0/3.6.x/+download/MG5_aMC_v3.6.2.tar.gz
```

This will download a tarball which you can unpack by doing:
```
tar -xzvf MG5_aMC_v3.6.2.tar.gz MG5_aMC_v3_6_2
```
After all files are unpacked the MadGraph program will be inside the `MG5_aMC_v3_6_2` directory.

### Run

At this point, running MadGraph would be as simple as doing:
```
./MG5_aMC_v3_6_2/bin/mg5_aMC
```
However, the Manchester machines do not have all the pre-installed requirements needed to run MadGraph. We need to install a package manager called [conda](https://www.anaconda.com/docs/getting-started/miniconda/main) to install the missing dependencies. 

#### Installing `conda`

You need to follow [these instructions](https://www.anaconda.com/docs/getting-started/miniconda/install#linux).

After installing `conda` it is best to log out from the Manchester server, get back in and move to a working node.

NOTE: If the installation went well you will see that once you get into a working node your terminal prompt will have a `(base)` attached to the name. It indicates that `conda` is loaded and you are in the `base` environment.
You will see something like:
```
<username>@wn3801260:~(base) [<username>@wn3801260 ~]$ 
```

After doing that create your environment:
```
conda create -n MGStudies
```
Activate the environment:
```
conda activate MGStudies
```
Install the missing `six` package:
```
conda install six
```

### Finally run `MadGraph`!

Do:
```
./MG5_aMC_v3_6_2/bin/mg5_aMC
```

MadGraph will start. You can test that it works by doing...
```
generate p p > t t~
```


