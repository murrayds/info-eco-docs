---
title: Miniconda
---

### Package Management with Miniconda
Miniconda is the current package manager.
Package management may change with according to uAlbany research policy, refer to the wiki for updates.

#### Miniconda Setup (Do Only Once)
```
# initialize the environment to your shell 
/network/rit/lab/info-eco/miniconda/bin/conda init

# If you are running bash, this is important
cat ~/.bashrc >> ~/.bash_profile

# finally, source your environment, you will only need to do this once. This will only work if your $SHELL is bash
source ~/.bash_profile
```

#### Listing Environments
```
conda env list
```

#### Activate DuckDB Environment
```
conda activate env_duckdb
```

#### Update Conda
```
conda install -c conda-forge ffmpeg
```

### Links
[Miniconda]
[Research Wiki]

[Miniconda]: https://www.anaconda.com/docs/getting-started/miniconda/main

[Research Wiki]: https://albany.atlassian.net/wiki/spaces/askit/pages/52353333/How-to+Software+Management+with+Anaconda+Software+Python+R+Etc.



### Listing only what you need
While exporting an already-built environment is a quick and efficient way of creating a reproducible computational environment, it can also create an environment that is *too specific*. For example, it makes an environment that requires something like the following,

```yaml
channels:
- bioconda
- conda-forge
dependencies:
- _libgcc_mutex=0.1=conda_forge
- _openmp_mutex=4.5=2_gnu
- aioeasywebdav=2.4.0=pyha770c72_0
- aiohttp=3.8.5=py311h459d7ec_0
- aiosignal=1.3.1=pyhd8ed1ab_0
- amply=0.1.6=pyhd8ed1ab_0
- appdirs=1.4.4=pyh9f0ad1d_0
- async-timeout=4.0.3=pyhd8ed1ab_0
- ...
```

This conda `.yaml` file is too specific, because it doesn't just list the dependencies we are interested in, *but also the dependencies of those dependencies*. These overly-specific dependencies can introduce several issues,
- The dependencies of our main packages, for example `pandas`, can change from version to version. If we upgrade pandas and no longer need these dependencies, we are requiring things we no longer need.
- Tools like `conda` resolve dependencies. Listing overly-specific and unnecessary dependency requirements makes its job harder over time, because different packages will have different and evolving requirements.  For example, `pandas` may dependend on `amply=0.1.6`, but perhaps a package we want to install later depends on `amply=0.1.8`—if we specify the exact version of `amply`, it can make resolving these conflicts more difficult. Be more general, and let Conda do its job
- From the standpoint of maintainability, these kinds of files are far too verbose and can change too much from commit-to-commit, making them hard to understand and difficult to keep track of. Moreover, it makes it hard to see which packages are really important.

These kinds of environments are usually auto-generated when exporting an environment. The best alternative is to maintain critical dependencies manually. 