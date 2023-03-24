Q: Will there be batch resources available to users?
A: Yes. The RSP will provide a shared computing cluster for users to perform analysis through its Portal, Notebook, and Web API Aspects. The cluster will be managed by a workload management system based on predetermined policies to allocate resources to individual users or groups. LSST users will have an initial allocation of batch CPU time, with the possibility of applying for additional quota through a Resource Allocation Committee. The size of the batch computing resource is determined by the requirement to provide 10% of the total LSST computing and storage resources to users. Users can launch jobs primarily through the APIs exposed in Notebook and Web API Aspects, and the Portal may potentially use the batch computing cluster too. 
Reference: LSE-319 

Q: will I be able to install custom software?
A: 

Q: Will there be GPUs in addition to CPUs?
A: K-T "I believe we are not yet planning to include GPUs as part of the resources made available on-project.  We are expecting to provide a mechanism for users to "bring their own" Google resources to the RSP, including GPU VMs."

Q: will I be able to download data?
A:

Q: Can I work offline with the RSP? (Jupyter notebooks / Portal / )

Q: is it possible to connect Jypter aspect with GitHub? 
NERSC

Q: People use IDE's to develop notebooks (e.g., VS Code), how can this be done? Can it be done at this RSP? 
IDEs such as VSCode support connections to a JupyterLab server. However, this doesn't work with the Notebook Aspect of the Rubin Science Platform due to how authentication works. Unfortunately it's challenging to make work in our environment at the moment. 
