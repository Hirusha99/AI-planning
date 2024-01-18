# AI-planning

## Install PDDL4J-TO Planning System

Damien Pellier and Humbert Fiorino created the PDDL4J-TO planning system specifically for the 2020 International Planning Competition. 
The Hierarchical Total Order planner PDDL4J (Planning domain description library for Java) is available as an open-source library under the LGPL license. 
PDDL4J is designed to make it easier to construct Java tools for automated planning that are based on the PDDL language. 
The field of artificial intelligence that deals with the realization of strategies or action sequences, usually for execution by intelligent agents, autonomous robots, and unmanned vehicles, is called automated planning and scheduling, or simply planning in the relevant literature.

## Instruction for Installation
We need singularity and WSL 2 as prerequisites.

### WSL 2 Installation
1. Open Windows PowerShell using Run as dministrator.
2. Verify whether WSL 2 is available or not.
   ```
   wsl --version
   ```
   WSL 2 not in the device, need to install.
   ```
   wsl --install
   ```
   Check the version of WSL
   ```
   wsl -l -v
   ```
   
   If WSL 1 exists need to upgrade it to WSL 2

   Install the Linux kernel package
   
   https://learn.microsoft.com/en-us/windows/wsl/install-manual#step-3---enable-virtual-machine-feature

   In Ubuntu-22.04
   ```
   wsl --set-version Ubuntu-22.04 2
   ```
   Other distribution
   ```
   wsl --set-version <distro name> 2
   ```
## Installation of Singularities

Singularity is a software environment which allows you to downlod, create, modify, and run containers from various sources (including Dockerhub) on a multiuser Linux system.

What is the purpose of the singularity container?

Singularity containers let users run applications in a Linux environment of their choosing. Possible uses for Singularity on Biowulf: Run an application that was built for a different distribution of Linux than the host OS. Reproduce an environment to run a workflow created by someone else.

```
$ sudo apt-get update && \
sudo apt-get install -y build-essential \
libseccomp-dev pkg-config squashfs-tools cryptsetup

export GOVERSION=1.17.3 OS=linux ARCH=amd64
wget -O /tmp/go${GOVERSION}.${OS}-${ARCH}.tar.gz \
https://dl.google.com/go/go${GOVERSION}.${OS}-${ARCH}.tar.gz
sudo tar -C /usr/local -xzf /tmp/go${GOVERSION}.${OS}-${ARCH}.tar.gz

echo 'export GOPATH=${HOME}/go' >> ~/.bashrc && \
echo 'export PATH=/usr/local/go/bin:${PATH}:${GOPATH}/bin' >>
~/.bashrc && \
source ~/.bashrc

curl -sfL
https://install.goreleaser.com/github.com/golangci/golangci-lint.sh
sh -s -- -b $(go env GOPATH)/bin v1.21.0

mkdir -p ${GOPATH}/src/github.com/sylabs && \
cd ${GOPATH}/src/github.com/sylabs && \
git clone https://github.com/sylabs/singularity.git && \
cd singularity

git checkout v3.6.3

cd ${GOPATH}/src/github.com/sylabs/singularity && \
./mconfig && \
cd ./builddir && \
make && \
sudo make install

singularity version
```

## Install the Planning System
To install this planning system we need Java JDK 8 and the 'gradle' build tool.

Install Java dependencies to Ubuntu Environment.
```
sudo apt-get install openjdk-8-jdk
```
Install Gradle for the Ubuntu environment.
```
sudo apt-get install gradle
```
Planning System Repository. Download and unzip it. 

https://gitlab.anu.edu.au/u1092535/ipc2020-competitor-5

Unzip the downloaded file into the working directory and direct it to a 'cd'
command.

Build the Planning System.

```
./gradlew build
```
Check whether the jar "pddl4j-VERSION.jar" that is available in the build/libs
directory.

Planning System running command
```
java -jar build/libs/pddl4j-3.8.3.jar -o <domainFile> -f <problemFile>
```






