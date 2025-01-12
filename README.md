Fork
====
This fork of SpinalTemplateSbt is aimed at learning SpinalHDL designs, by inspecting the generated
output through yosys/netlistsvg via Makefile to automate and document the flow.

Spinal Base Project
============
This repository is a base SBT project added to help non Scala/SBT native people in their first steps.

Just one important note, you need a java JDK >= 8

On debian :

```sh
sudo add-apt-repository -y ppa:openjdk-r/ppa
sudo apt-get update
sudo apt-get install openjdk-8-jdk -y

#To set the default java
sudo update-alternatives --config java
sudo update-alternatives --config javac
```

## Basics, without any IDE

You need to install SBT

```sh
echo "deb https://repo.scala-sbt.org/scalasbt/debian all main" | sudo tee /etc/apt/sources.list.d/sbt.list
echo "deb https://repo.scala-sbt.org/scalasbt/debian /" | sudo tee /etc/apt/sources.list.d/sbt_old.list
curl -sL "https://keyserver.ubuntu.com/pks/lookup?op=get&search=0x2EE0EA64E40A89B84B2DF73499E82A75642AC823" | sudo apt-key add
sudo apt-get update
sudo apt-get install sbt
```

If you want to run the scala written testbench, you have to be on linux and have Verilator installed (a recent version) :

```sh
sudo apt-get install git make autoconf g++ flex bison -y  # First time prerequisites
git clone http://git.veripool.org/git/verilator   # Only first time
unsetenv VERILATOR_ROOT  # For csh; ignore error if on bash
unset VERILATOR_ROOT  # For bash
cd verilator
git pull        # Make sure we're up-to-date
git checkout v4.040
autoconf        # Create ./configure script
./configure
make -j$(nproc)
sudo make install
cd ..
echo "DONE"

```

Clone or download this repository.

```sh
git clone https://github.com/SpinalHDL/SpinalTemplateSbt.git
```

Open a terminal in the root of it and run "sbt run". At the first execution, the process could take some seconds

```sh
cd SpinalTemplateSbt

//If you want to generate the Verilog of your design
sbt "runMain mylib.MyTopLevelVerilog"

//If you want to generate the VHDL of your design
sbt "runMain mylib.MyTopLevelVhdl"

//If you want to run the scala written testbench
sbt "runMain mylib.MyTopLevelSim"
```

The top level spinal code is defined into src\main\scala\mylib

## Basics, with Intellij IDEA and its scala plugin

You need to install :

- Java JDK 8
- SBT
- Intellij IDEA (the free Community Edition is good enough)
- Intellij IDEA Scala plugin (when you run Intellij IDEA the first time, he will ask you about it)

And do the following :

- Clone or download this repository.
- In Intellij IDEA, "import project" with the root of this repository, Import project from external model SBT
- In addition maybe you need to specify some path like JDK to Intellij
- In the project (Intellij project GUI), go in src/main/scala/mylib/MyTopLevel.scala, right click on MyTopLevelVerilog, "Run MyTopLevelVerilog"

Normally, this must generate an MyTopLevel.v output files.

## Basics, with Eclipse and its scala plugin

First, i "strongly" suggest to use intellij idea instead.

You need to install :

- Java JDK
- Scala
- SBT
- Eclipse (tested with Mars.2 - 4.5.2)
- [scala plugin](http://scala-ide.org/) (tested with 4.4.1)

And do the following :

- Clone or download this repository.
- Revert changes from https://github.com/SpinalHDL/SpinalTemplateSbt/commit/173bbb9bb8cbf70087339104f6ebced9321908dd
- Run ```sbt eclipse``` in the ```SpinalTemplateSbt``` directory.
- Import the eclipse project from eclipse.
- In the project (eclipse project GUI), right click on src/main/scala/mylib/MyTopLevel.scala, right click on MyTopLevelVerilog, and select run it

Normally, this must generate output file ```MyTopLevel.v```.

## Mill Support (Experimental)

This Spinal Base Project contains support for the [Mill build tool](https://com-lihaoyi.github.io/mill).

The prerequisites are the same as for using SBT, except for sbt itself. Additionally, the ```mill``` executable needs to be installed on the path. Download it to ```/usr/local/bin/mill``` or ```~/bin/mill``` according to the [installation instructions](https://com-lihaoyi.github.io/mill/mill/Intro_to_Mill.html#_installation).

You can clone and use this repository in the following way.

```sh
git clone https://github.com/SpinalHDL/SpinalTemplateSbt.git
```

Open a terminal in the root of it and execute your favorite mill command. At the first execution, the process could take some seconds

```sh
cd SpinalTemplateSbt

//If you want to generate the Verilog of your design
mill mylib.runMain mylib.MyTopLevelVerilog

//If you want to generate the VHDL of your design
mill mylib.runMain mylib.MyTopLevelVhdl

//If you want to run the scala written testbench
mill mylib.runMain mylib.MyTopLevelSim
```

The top level spinal code is defined into src\main\scala\mylib
