# General installation guides

First of, this is not a specific installation guide to any of the pipelines covered by this configuration repository. 

Instead, this guide will provide some hints how best to approach the general setup, depending on what operating system you are running on. The very basic explanation is that you need two components - the Nextflow pipeline engine and some way to have Nextflow stage the relevant software packages. Since this may require slightly different steps on different platforms, we discuss them separately below. 

[Linux](#linux)

[OSX](#osx)

[Windows](#windows-11)

## Linux

If you are running on Linux, things are generally "simple" (assuming you are comfortable administrating Linux, that is).

We are testing our pipelines on Alma Linux 9.4, but the basic principle should be transferrable to other systems. 

### Software provisioning

On Linux, you have access to basically all supported software provisioning frameworks also supported by Nextflow - including Conda and several container frameworks. These all have their pros and cons, but to keep things simple, we recommend you use Apptainer. Apptainer is a Docker-compatible container engine, is completely free and also happens to have a dedicated repository for all the otherwise Docker-native Bioconda containers we use in this pipeline (i.e. quick start up without need for conversion of container formats).

To install Apptainer on your system, the easiest option is:

On a RHEL derivative, version 9 (rpm).
```bash
sudo dnf -y install apptainer
```

On Ubuntu, version 22.04 (deb)
```bash
sudo apt-get install apptainer
```

If you running different/older/newer releases or otherwise need more information on installing Apptainer, please check the official [documentation](https://apptainer.org/docs/admin/latest/installation.html). 

### Installing JRE

Nextflow requires The Java JRE (>= 11, <= 21):

On a RHEL derivative, version 9
```bash
sudo dnf -y install java-21-openjdk 
sudo alternatives --config java
```

On Ubuntu, version 22.04
```bash
sudo apt install openjdk-11-jdk
sudo update-alternatives --config java
```

Use the second command to set the appropriate version of JRE as your default. 

### Installing Nextflow

You can follow the instructions on the official Nextflow guide [here](https://www.nextflow.io/docs/latest/getstarted.html#installation).

A simple approach would be:
```bash
mkdir -p $HOME/bin
cd $HOME/bin
wget https://github.com/nextflow-io/nextflow/releases/download/v24.04.4/nextflow-24.04.4-all
mv nextflow-24.04.4-all nextflow
chmod +x nextflow
```
And you could also make sure that $HOME/bin is in $PATH by adding the directory to your bash profile:
```bash
echo "export PATH=$PATH:$HOME/bin" >> $HOME/.bash_profile
source $HOME/.bash_profile
```

## OSX

The following guide was tested on OSX 14 (Sonoma) with an Intel-based Macbook Pro. 

### Software provisioning

On Mac, we recommend you install Docker instead of Conda or any of the other container frameworks; its the simplest approach with the least amount of incompatibilies.

Docker (Docker Desktop) has a detailed installation guide [here](https://docs.docker.com/desktop/install/mac-install/).

### Installing JRE

Nextflow requires the Java JRE (>= 11, <= 21). To be able to specifically install that, we first need SDKMAN

```bash
curl -s "https://get.sdkman.io" | bash
```

Simply follow the instructions on the screen and then source your bash profile to make the changes take immediate effect:

```bash
source "$HOME/.sdkman/bin/sdkman-init.sh"
```

Next, install JRE 21:

```bash
sdk install java 21.ea.35-open
```

You can confirm that you have installed the correct version as follows:

```bash
java -version
```

### Installing Nextflow

You can follow the instructions on the official Nextflow guide [here](https://www.nextflow.io/docs/latest/getstarted.html#installation).

A simple approach would be:
```bash
mkdir -p $HOME/bin
cd $HOME/bin
curl -O https://github.com/nextflow-io/nextflow/releases/download/v24.04.4/nextflow-24.04.4-all
mv nextflow-24.04.4-all nextflow
chmod +x nextflow
```
And you could also make sure that $HOME/bin is in $PATH by adding the directory to your bash profile:
```bash
echo "export PATH=$PATH:$HOME/bin" >> $HOME/.bash_profile
source $HOME/.bash_profile
```

## Windows 11

With the introduction of [windows subsystems for Linux](https://learn.microsoft.com/en-us/windows/wsl/install) (WSL), it is now technically possible to run Linux "directly" within the Windows 11 powershell. Since this is ultimately a type of virtualization, it comes with drawbacks such as the fact that the Linux environment will only get parts of the total systems resources. We also found some processes to simply fail under WSL for no obvious reasons. If you are nevertheless set on trying to get our pipelines to run under Windows, the following steps are necessary:

- Make sure your CPU/main board support virtualization
- Enable virtualization in your systems BIOS (refer to manufacturers instructions)
- Get the latest version of Windows 11
- [Install](https://learn.microsoft.com/en-us/powershell/scripting/install/installing-powershell-on-windows?view=powershell-7.4) the latest version of the Windows 11 Powershell (version 7.4 at the time of writing)
- Start the Windows Powershell

Next, you have to set up your virtual linux environment:

```bash
wsl --install
```

If you have previously enabled virtualization in your computers bios, this should run through fine and create a basic Ubuntu installation. You will be asked to provide a user name and password - make sure to write these down. You will then be dropped into the bash shell of a fresh Ubuntu 22.04 system. 

From here on, simply refer to the instructions for Linux [above](#linux).
