# Common questions

## What kind of system do you recommend we use to run these pipelines?

We would strongly advice against Windows for any kind of "professional" bioinformatic work, period. While it might be possible to get these pipelines to work under Windows 11 with the Linux subsystems, it would be a fairly inconvenient "workaround". 

We have been able to successfully run all pipelines on Linux (Alma 9.4) as well as OSX (14) with a similar amount of effort, but would always recommend Linux if at all possible. 

The system specs should, at minimum, be:

- 8 Cores
- 32GB RAM
- 512GB Harddrive space (depending on the amount of data you process)

(We have tested all pipelines on a Macbook Pro with 4 cores and 16GB Ram, but this really isn't recommended in production!)

As you will notice, most current off-the-shelf computers will meet these requirements, including comparatively cheap so-called Mini-PCs for less than 1000€/$. 

Unsurprisingly, the old rule "the more, the better" does apply and the pipelines are designed to scale on larger infrastructures including dedicated compute clusters and cloud platforms if available. If you consider the purchase of a dedicated compute node, our recommendation is to have  roughly 8GB of Ram per compute core and several Terrabytes of local (or network-attached) storage. 
