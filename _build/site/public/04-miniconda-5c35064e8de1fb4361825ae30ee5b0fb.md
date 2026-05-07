---
title: Miniconda
---

### Package Management with Miniconda
Miniconda is the current package manager.

#### Initializing Environment
```
# initialize the environment to your shell 
/network/rit/lab/info-eco/miniconda/bin/conda init

# If you are running bash, this is important
cat ~/.bashrc >> ~/.bash_profile

# finally, source your environment, you will only need to do this once. This will only work if your $SHELL is bash
source ~/.bash_profile
```

#### Activate DuckDB Environment
```
activate env_duckdb
```

### Links
[Miniconda]

[Miniconda]: https://www.anaconda.com/docs/getting-started/miniconda/main
