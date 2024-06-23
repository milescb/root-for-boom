# Docker for BOOM

Run python2 (centos7) and python3 (alma9) versions of [boom](https://gitlab.cern.ch/ATauLeptonAnalysiS/boom) compatible with corresponding cvmfs distributions of PyROOT currently used on lxplus nodes. Note that cvmfs should be used when applicable; these images are used to run for instance on macOS arm devices or on devices where root is not already installed. 

## Accessing an image

### Build

Choose appropriate version / desired dev environment and build:

```
docker buildx build --platform linux/amd64 -t root:6.18-py2.7 root6.18.04-python2.7-centos7
```

### Pull

Pre-built versions can be found at `docker.io/milescb/root-for-boom`. To use these pull via:

```
docker pull milescb/root-for-boom:<version>
```

## Run image interactively

To run boom with the docker provided, mount the needed files and run interactively:

```
docker run -it --rm --platform linux/amd64 \
    -v <boom_path>:/boom -v <happy_path>:/happy -v <data_path>:/data \
    milescb/root-for-boom:6.18-py2.7 /bin/bash
```
### Setup environment

Once in the docker environment, setup for boom production:

```
cd /happy 
source setup.sh 
cd /boom
export BOOM_NTUPLE_PATH=/data
```

Now, run boom as before!
