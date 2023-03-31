**Q: Will there be batch resources available to users?**

**A**: Yes.
The RSP will provide a shared computing cluster for users to perform analysis through its Portal, Notebook, and Web API Aspects.
The cluster will be managed by a workload management system based on predetermined policies to allocate resources to individual users or groups.
RSP users will have an initial allocation of batch CPU time, with the possibility of applying for additional quota through a Resource Allocation Committee.
The size of the batch computing resource is determined by the requirement to provide 10% of the total LSST computing and storage resources to users.
Users can launch jobs primarily through the APIs exposed in Notebook and Web API Aspects, and the Portal may potentially use the batch computing cluster too.
References:
DMTN-223: User batch - possibilities and plans (`DMTN-223 <https://dmtn-223.lsst.io/>`_).
DMTN-202: Use cases and science requirements on a user batch facility (`DMTN-202 <https://dmtn-202.lsst.io/>`_).
LSE-319: Science Platform Vision Document (`LSE-319 <https://ls.st/lse-319>`_).


**Q: Will I be able to install custom software?**

**A**: In the current DP0 era of the RSP, DP0 delegates are able to install custom software into their own homespace (limited by individual quotas).
In addition, during the operations-era RSP there will be a process for users to request certain popular packages to be added to the common environment for use by all.
References:
`How do I install packages in my user environment <https://dp0-2.lsst.io/data-access-analysis-tools/nb-intro.html#how-do-i-install-packages-in-my-user-environment>`_

**Q: Will there be GPUs (Graphics processing units) available in addition to CPUs (Central Processing Units)?**

**A**: There are discussion about providing a mechanism for users to "bring their own" Google resources to the RSP, including GPU virtual machines.
**However**, we are not yet planning to include GPUs as part of the resources made available on-project (including "bring-your-own" resources).
Users interested in GPUs shoudl contact the Independect Data Access Centers program (see, e.g., `Contributed  Computing Resources <https://www.lsst.org/scientists/in-kind-program/cec>`_).

**Q: Will I be able to download LSST data?**

**A**: Yes, for limited subsets of the data. However, it will be impracticable to downaload the full amount of data that the LSST will produce, and the RSP, in particular its Notebook Aspect, are designed to provide the users with resources  at the LSST Data Access Centers such that computation and analyses can be performed "next to the data". 

**Q: Will I be able to work offline with the RSP?**
**A** The notebooks in the Notebook Aspect of the RSP can certainly be downloaded and modified offline, working with a subset of the data. However, the full functionality of the RSP Aspects will require an online connection in order to access the LSST data and perform analyses on them. 

**Q: Will I be able to use integrated development environments (IDEs, e.g., VSCode, DataSpell, etc.) to develop Jupyter Notebooks at the RSP?**

**A**: IDEs such as VSCode support connections to a JupyterLab server. However, this currently doesn't work with the Notebook Aspect of the Rubin Science Platform. Unfortunately, it's challenging to make this work in our environment at the moment, and this feature is not currenyly a priority in the current RSP developement. 

