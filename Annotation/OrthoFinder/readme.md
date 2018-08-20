## OrthoFinder

Software for inferring orthologues between species
  - Input: peptide data in fasta format
  - Output: Species phylogeny, gene phylogeny, orthologues, and summary statistics. 

Software repository and manuals: [here.](https://github.com/davidemms/OrthoFinder)

### Installation, Software Dependencies (From OrthoFinder repository)

1. Download the latest release from github: https://github.com/davidemms/OrthoFinder/releases (for this example we will assume it is OrthoFinder-1.0.6.tar.gz, change this as appropriate.)

2. In a terminal, 'cd' to where you downloaded the package 

3. Extract the files: `tar xzf OrthoFinder-1.0.6.tar.gz`

#### BLAST+
You already have this!

#### MCL
The mcl clustering algorithm is available in the repositories of some Linux distributions and so can be installed in the same way as any other package. For example, on Ubuntu, Debian, Linux Mint:

- `sudo apt-get install mcl`

Alternatively it can be built from source which will likely require the 'build-essential' or equivalent package on the Linux distribution being used. Instructions are provided on the MCL webpage, http://micans.org/mcl/.  

#### FastME
FastME can be obtained from http://www.atgc-montpellier.fr/fastme/binaries.php. The package contains a 'binaries/' directory. Choose the appropriate one for your system and copy it to somewhere in the system path e.g. '/usr/local/bin'** and name it 'fastme'. I.e.:

- `sudo cp fastme-2.1.5-linux64 /usr/local/bin/fastme`

> Add: Running OrthoFinder
