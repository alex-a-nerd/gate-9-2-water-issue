# Description
This repository contains a minimal example demonstrating an issue with GATE 9.2 and the Water material.

The included Materials.xml file is the latest official version from GATE commit d913436.

# Usage
## Docker
Running water.mac with GATE 9.2:
```shell
docker run -i --rm -v $PWD:/APP opengatecollaboration/gate:9.2-docker water.mac
```

## Singularity
With Singularity, we need to pull the image first, then run it:
```shell
singularity pull gate.sif docker://opengatecollaboration/gate:9.2-docker
singularity run -B $PWD:/APP gate.sif water.mac
```

# Observations
Running on GATE 9.2 using the material "Water" produces an error. Example error on Ubuntu using Singularity:
```
### CAUGHT SIGNAL: 11 ### address: 0x46299c0,  signal =  SIGSEGV, value =   11, description = segmentation violation. Invalid permissions for mapped object.

Backtrace:
[PID=2123180, TID=-2][0/1]> p

: Segmentation fault (Invalid permissions for mapped object [0x46299c0])
/runGate.sh: line 4: 2123180 Aborted                 (core dumped) Gate $1
```

The following changes fix the issue:
- Run on GATE 9.1
- Remove the Water section from Materials.xml
- Change the material of the "phantom" volume to Air
