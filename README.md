# GENIE-on-hpc test
srun --partition=icecube_gpu --gres=gpu:1 --mem=5G --cpus-per-task=4 --time=03:00:00 --ntasks=1 --pty bash


(base) [jackp@node161 ~]$ module load astro

(base) [jackp@node161 ~]$ module load cuda/12.4

(base) [jackp@node161 ~]$ module load hdf5/intel/1.10.4

(base) [jackp@node161 ~]$ module load intel/20.0.4

(base) [jackp@node161 ~]$ conda activate myenv

(myenv) [jackp@node161 ~]$ 

(myenv) [jackp@node161 ~]$ source ~/genie_setup.sh


Load modules astro, cuda, hdf5, intel

First install GENIE: 
cd /groups/icecube/jackp
git clone https://github.com/GENIE-MC/Generator.git GENIE
see path variables 

## Dependencies:
### GSL:
should be installed

### log4cpp:
git clone https://github.com/orocos-toolchain/log4cpp.git
scp /path/to/log4cpp.tar.gz jackp@your_hpc_server:/groups/icecube/jackp/
mkdir build
cd build
cmake .. -DCMAKE_CXX_STANDARD=98 -DCMAKE_INSTALL_PREFIX=/groups/icecube/jackp/log4cpp
make
make install

### libxml2:
should already be isntalled check with :
find /usr -name "libxml2*" 2>/dev/null
find /usr/include -name "libxml2" 2>/dev/null

### LHADPF
Next for LHADPF go to website download recent version and do:
in local:
wget http://www.hepforge.org/archive/lhapdf/lhapdf-5.x.y.tar.gz
tar xzvf lhapdf-5.x.y.tar.gz
cd lhapdf-5.x.y
scp /path/to/lhapdf-5.x.y.tar.gz jackp@fend01.hpc.ku.dk:/lustre/hpc/icecube/jackp/

in hpc node:
./configure --prefix=/groups/icecube/jackp/lhapdf5 CXXFLAGS="-std=c++11"
make
make install

### Pythia6:
should be in GNIE:
$GENIE/src/scripts/build/ext/build_pythia6.sh
source build_pythia6.sh 6412 


### ROOT:
cd /groups/icecube/jackp
git clone https://github.com/root-project/root.git
cd root



# Commands:
to useful file to prometheus:
obviosuly replace root with file:

gntpc -i gntp_99_100_events_20240911_192155.ghep.root -f rootracker -o 100_events.gtrac.root

