# Welcome to the SDE2 User Guide

SDE2 is the HPC cluster that is designed to support work with restricted research data of [moderate-impact](https://srds.uchicago.edu/secure-research-data-usage-guide/). As for the other HPC systems managed by RCC, it allows to process large amount of data taking advantage of distributed computing operated via the Slurm scheduler. If your data is subject to a Data Use Agreement, Institutional Review Board protocol, or a Procurement Contract it is considered sensitive with common examples from [Secure Research Data Strategy](https://srds.uchicago.edu/secure-research-data-usage-guide)

If you have any questions about SDE2, please email midwayr-help@rcc.uchicago.edu.

## Eligibililty

All UChicago researchers with PI status are eligible to establish workspaces on SDE2. However, the project must be subject to an active Data Use Agreeemnt, and/or approved Institutional Review Board protocol, or executed procurement contract.  Additionally, the project must involve sensitive data that does not exceed moderate-impact level. The high-impact data should not be stored on SDE2 - RCC offers a dedicated SDE3 system for high impact data. The public or non-sensitive data can be stored on any of the general purpose HPC systems managed by RCC within the Midway ecosystem.


## Access and Allocation
Allocation on SDE is provided for the duration of project and revoked upon project completion or expiration of the associated data governing agreements. A workspace is requested by PI for each project. Unlike Midway ecosystem where a single authorization is granted per user to access all PI's projects, on SDE2 users need to be authorized per each project. A user account created to access Midway ecosystem (Midway2, Midway3, Midway3, etc) does not apply to SDE2. A separate user account needs to be created to access SDE2 projects. Please also note that you must have enabled [Two Factor Authentication](https://cnet.uchicago.edu/2FA) for your CNetID before connecting to SDE2.

!!! note
    Researchers can apply for general user accounts only after a PI established a project workspace on SDE2. Please reach out to your PI to find the project acronym when requesting a user account. 
 
## System Overview

SDE2 is comprised of multiple login nodes and a collection of compute nodes. A shared filesystem supports up to 750TB of data. Every PI is eligible for a 500GB of storage free of charge. Any additonla storage can be purchased through the Cluster Partnership Program, please email us at cpp@rcc.uchicago.edu and indicate the system name and storage size you would like to request.
<br><br/>

**File System:**

* SDE2 utilizes a GPFS filesystem, with `/home` and `/project` directories mounted for private and collaborative work, respectively. 
The `/home/<CNetID>` directory has a strict quota of 30GB and the quota for `/project/pi-<PI_CNETID>-<ProjectName>` varies depending on the project. SDE2 does not have a scratch filesystem.


**Software:**

RCC maintains the centrally-supported scientific software on SDE2 system and can install required packages on request. Users can also install their own project-specific packages. However, due to security and privacy controls the software installation protocol may be convoluted - please feel free to contact us if you have any questions at midwayr-help@rcc.uchicago.edu.

The free scientific software is shared with all users at no cost. However, the proprietory software may have limited availability due to the restricted number of checked licenses or license locked to a particular research group. Please feel free to reach out to us if you would like to install a proprietory software.

* Use `module avail`, to see what is available
* To load a particular available package, for example, `gcc` version 8.2.0, do `module load gcc/8.2.0`
* If you do not specify a version of the package, the default one is loaded
* To see what environmental variables are modified when `gcc/8.2.0` is loaded, do `module show gcc/8.2.0`
* To unload `gcc/8.2.0`, do `module unload gcc/8.2.0`



