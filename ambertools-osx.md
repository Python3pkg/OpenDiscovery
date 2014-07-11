#Installing ambertools on Mac OSX

## Homebrew
First we need to install homebrew, a package manager for OSX:

```bash
# installing homebrew usng ruby
ruby -e "$(curl -fsSL https://raw.github.com/Homebrew/homebrew/go/install)"
```

## GCC
Using brew, we can now install GCC, and fortunately gfortran comes with it (at least in 4.8). This can take many minutes (mine took 30mins). Once it is done, we need to symlink some of the binaries.

```bash
#update homebrew just in case
brew update

#tap the installation recipes for particular versions of compilers
brew tap homebrew/versions

#install gcc4.8
brew install gcc48

#symlinking
ln -s /usr/local/bin/gcc-4.8 /usr/local/bin/gcc
ln -s /usr/local/bin/g++-4.8 /usr/local/bin/g++
ln -s /usr/local/bin/c++-4.8 /usr/local/bin/c++
ln -s /usr/local/bin/cpp-4.8 /usr/local/bin/cpp
ln -s /usr/local/bin/gcov-4.8 /usr/local/bin/gcov
ln -s /usr/local/bin/gcc-nm-4.8 /usr/local/bin/gcc-nm
ln -s /usr/local/bin/gcc-ar-4.8 /usr/local/bin/gcc-ar
ln -s /usr/local/Cellar/gfortran/4.8.1/gfortran/lib/libgfortran.3.dylib /usr/local/lib/libgfortran.dylib
```

## AmberTools
Ambertools is freely available from [ambermd.org](http://ambermd.org/). Download the `tar.gz` and extract it into your home directory (~):

```bash
#extract the archive
tar xvfj AmberTools14.tar.bz2 -C ~/amber14
cd ~/amber14

#AMBERHOME needs to be set in order for patching to work properly
export AMBERHOME=`pwd`

#AMBERHOME needs to be set each time a new terminal window is open
echo "export AMBERHOME=\$HOME/amber14" >> ~/.bashrc
```

Before installation, we need to configure the makefiles. Note there are other options. Then we can make the binaries, then add them to our path
```bash
# Configuring the application
./configure gnu

#making the binaries
make install

#adding the binaries to the path
echo "export PATH=\$HOME/amber14/bin:\$PATH" >> ~/.bashrc
```

Everything should now be installed.

## Extra software to consider
### Gromacs
GROMACS is a versatile package to perform molecular dynamics, known for its extremely high performance and open-source nature.

We can use brew to install it:

```bash
#Installing Gromacs
brew install gromacs
```

###Acpype
Acpype is a tool based on Python to use Antechamber to generate topologies for chemical compounds. It is particularly useful to convert between Amber and Gromacs parameter files.

```bash
# Installing ACPype
brew install subversion
cd /opt
sudo svn checkout http://svn.code.sf.net/p/ccpn/code/branches/stable/ccpn/python/acpype acpype
ln -s /opt/acpype/acpype.py /usr/local/bin/acpype
```

###XMGrace
Xmgrace is a 2D plotting tool which allows you to interactively modify plots, to set all kind of plot parameters, change the appearance of your figure, and to save the figure in the format of your choice.

```bash
# Simple!
brew install grace
```