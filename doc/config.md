# Create your own config file

All our pipelines allow you to run with basic build-in execution profiles and expose relevant options from the command line to dial in your system specs. This is described in each respective pipeline documentation. 

However, we strongly recommend that you add your own site-specific config file to this repository to avoid having to set these options from the command line each time your run a pipeline. Moreover, the built-in profiles are only applicable to single-computer setups. If you run on a compute cluster, or possibly the cloud, you will need to provide additional options to the pipeline for it to translate properly to your setting. 

## Contributing your profile

Before we look at the specific options you can put in your site-specific config file, let's discuss how you contribute it to our project. 

### Fork this repository

If you are (very) comfortable with git, you are welcome to fork this repository and add your own profile, followed by a pull request against our main branch. You will have to :

- create your config file under `conf/` with a name of your choice (preferably short!)
- add this new config file to the central lookup file [custom.config](../custom.config) with a short name matching the name of the config file
- Commit your changes to your personal fork
- Create a pull request from your updated fork to our main branch

### Create an issue

If you are not (very) comfortable with git, you are welcome to create an issue on this page and simply let us know that you want us to add a profile for you. For that we will need the following:

- name of the profile
- number of compute cores, ram and (optionally) allowed walltime
- description of your compute environment (single machine, cluster, cloud) and resource manager, if any
- choice of software provisioning framework and any necessary options

See below for all the possible options that can be set. 

## Site-specific config file

The amount of data needed is fairly minimal - see the example below for a simple Slurm setup:

```
params {
  max_cpus = 40
  max_memory = 250.GB
  max_time = 120.h
  reference_base = /work/references
}

executor {
  queueSize=50
}

process {
  executor = 'slurm'
  queue = 'all'
}

singularity {
  enabled = true
  cacheDir = "/work/singularity_cache"
}

```

Note that this config file specifies four instruction blocks - the first three are mandatory, the fourth configures the container engine and related settings, so will depend on your software provider of choice. 

## params

Here you can specify the limits of your compute enfironment and the base directory for the local pipeline references. The compute limits apply to the configuration of individual nodes (max_cpus, max_memory) and the whole cluster (max_time, i.e. maximum walltime a job can use), respectively. The reference_base option should be user-writable and, if applicable, live on a shared file system so all compute systems can access it. 

## executor

These are options specific to your resource manager / executor. In our example, we limit the number of concurrent jobs to 50. Additional options are described [here](https://www.nextflow.io/docs/latest/executor.html).

## process

Options listed here concern mostly the choice of your executor (like Slurm, or PBS). In our example, we specify that we use "slurm" as our resource manager and that the corresponding queue/partition is called "all". Additional options are described [here](https://www.nextflow.io/docs/latest/executor.html). If you only run on a local computer, you can also set `local` as your executor, of course.

## singularity

This block is used to configure the singularity container engine, as described [here](https://www.nextflow.io/docs/latest/config.html). This name of the appropriate scope depends, of course, on your choice of software provisioning framework. Other commonly used options would be:

```
docker {
    enabled = true
    cacheDir = /work/docker_cache
}
``` 
or
```
conda {
    enabled = true
    cacheDir = /work/conda_cache
}
````
and so on...

In any case, we strongly recommend you set the `cacheDir` option to somewhere on your shared file system so nextflow is able to re-use previously installed software packages/containers. 
