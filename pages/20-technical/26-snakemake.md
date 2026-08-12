---
title: Snakemake
---

# Overview
Snakemake is a workflow automation originally built for the biosciences, but with general applications, which implements its own design-specific language built on python. The aim of Snakemake is to define "rules" which perform transformations on files. Each rule has inputs and outputs, each with a specified filename. Rules can also be used as inputs to other rules, allowing the creation of long pipelines of transformations, each using previous files to compute new ones. 

Rules look something like this:

```python
rule user_defined_name:
    input:
        "path/to/input.file"
    output:
        "path/to/output.file"
    shell:
        "shell_command {input} > {output}"
```

A great advantage of Snakemake is that it is trivial to parallelize the pipeline, running many rules at the same time.

Snakemake can be executed in the terminal as the following:
```bash
snakemake -j 2
```
Where the `-j 2` indicates that we will run two processes in parallel. 

Snakemake works by creating a [[Directed-Acyclic Graph]], or DAG, that details the relationships between all the rules and the files that they produce. It then examines which files are not yet created or are out of data, and uses the DAG to run the rules to generate the files and all others that depend on them upstream in the graph. 

# Structuring the Snakefile
I generally structure the Snakefile as follows, with filenames and parameters defined like constants that are executed throughout the workflow

```python
from os.path import join as j

# ...
# Define the input data
RAW_DATA = j(DATA_RIW, "raw_data.csv")

# First, define the relevant filename
OUTFILES = j(DATA_DIR, "file_to_make_{version}.csv"

# Then, define the platforms.
VERSIONS = ["v1", "v2"]

# Then, in the target rule:
rule all:
    input: expand(OUTFILES, version=VERSIONS)

# Then, the rule. Note we are using the 'script' directive.
rule rule1:
    input: RAW_DATA,
    output: OUTFILES,
    script: "scripts/do_stuff.py"
```

The steps that snakemake is taking is:
1. Generating a list of all filenames that need to be created. `expand(...)` returns a list of strings, each string with the "platform" wildcard filled with a value from the `PLATFORMS` array. So `expand(expand(PROJECTS_FILTERED, platform=PLATFORMS)` returns `[".../file_to_make_v1.csv", ".../file_to_make_v2.csv"]`
2. Then, Snakemake finds the rule that will create files with this name. That is the `rule1` rule. Because there are two necessary files with a different "version" wildcard, this rule will be executed twice, once with "version=v1" and again with "version=v2"
3. The inputs, outputs, params, and wildcards are automatically passed to the python script, but **only when using the script directive**. This will **not work** with the shell directive. These can be accessed from within the script by calling the snakemake object.

The benefit of organizing our files this way is that it makes the pipeline very flexible. We can create a whole pipeline for `pypi` and `cran`, but at any point in the future, we could add another platform to the array in the Snakefile, such as `VERSIONS=["v1", "v2", "v3"]`. Or, better, these can parameters can eventually be moved into a separate config file for easier maintenance. 

# Executing snakemake 
Snakemake works by (1) detecting files that need to be created, and (2) by calling rules to create those files. 

The key fact is that the _file_ is the most important thing to snakemake, **not** the _rule_. You're really not meant to call rules one by one (e.g., you wouldn't call `snakemake -c1 rule1`). Rather, you should be telling snakemake to create a specific _file_. So, if we have a rule `rule1` that creates a file of the form `file_to_make_{version}.csv`, we can call the following,
```bash
snakemake -j 1 file_to_make_{v1}.csv
```

This tells snakemake to execute any rules necessary to create the output `file_to_make_{v1}.csv`. It sees that the file name provided matches the output of the rule `rule1`. Snakemake will then execute the `rule1` rule, passing `v1` as a wildcard. 

Note, that you will probably need to provide the whole path to the output file. So your command might look like the following:

```bash
snakemake -j 1 /Users/d.murray/Documents/snakemake-project/data/projects_filtered_pypi.csv
``` 

Usually, you could add this to a rule in the Makefile for easy testing. Usually, though, I just run `snakemake -j 1`. If I want to re-create a file, I just delete it manually.

# Tips
- Snakemake integrates very well with [[Conda]]. I advise using lots of small conda environments depending on the needs of each rule. Snakemake also provides functionality to automatically export these conda environments into Singularity images.

# Resources
- [The official Snakemake tutorial](https://snakemake.readthedocs.io/en/stable/tutorial/tutorial.html)
- [A HandWiki article about Snakemake](https://handwiki.org/wiki/Software:Snakemake#Rules)

