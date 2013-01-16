# RXTX 2.2

Latest update with upstream: **2012-01-08**

This fork of RXTX patches the upstream sources to introduce the following fixes:

- support to linux ttyACM* devices
- reduced latency (thanks [@neophob](https://github.com/neophob))
- faster ports listing on Windows boxes with some particular hardware (Bluetooth) configurations (thanks eried [from the forum](http://arduino.cc/forum/index.php/topic,46977.0.html))

## Upgrading the source code

Check it out from CVS with the commands

```bash
export CVSROOT=:pserver:anonymous@qbang.org:/var/cvs/cvsroot
cvs login # (then hit return)
cvs checkout -r commapi-0-0-1 rxtx-devel
```

## Compiling on linux

Have the necessary tools in place: on debian/ubuntu `apt-get install build-essentials` should suffice. Then, in the repo folder, run:

```bash
mkdir build
../configure
make
```

and get the resulting files.

## Compiling on windows

Have the necessary tools in place. These are:

- [git](http://code.google.com/p/msysgit/)
- [Visual C++ 2010 Express](http://www.microsoft.com/visualstudio/ita/downloads#d-2010-express)
- [Windows SDK 7.1](http://www.microsoft.com/en-us/download/details.aspx?id=8279)
- [Java Development Kit 1.4](http://www.oracle.com/technetwork/java/javasebusiness/downloads/java-archive-downloads-javase14-419411.html) (any JDK should actually suffice)
- [JUnit.jar](http://search.maven.org/#browse|-2021159614) placed somewhere on your hard drive

After you have cloned the repo, run:

```bat
C:\Program Files (x86)\Microsoft Visual Stu­dio 10.0\Common7\Tools>vsvars32.bat
Set­ting envi­ron­ment for using Microsoft Visual Stu­dio 2010 x86 tools.
C:\Program Files (x86)\Microsoft Visual Stu­dio 10.0\Common7\Tools>cd C:\RXTX\

C:\RXTX> mkdir build
C:\RXTX> copy Makefile.msvc build\Makefile
C:\RXTX> cd build
C:\RXTX\build> set path=%PATH%;"C:\Program Files (x86)\Microsoft Visual Stu­dio 10.0\VC\bin"
```

Then edit Makefile and correct path variables, in particular: JAVA_HOME, JUNIT_JAR, JAVAC, JAR, JAVAH, JAVA. Finally run:

```bat
C:\RXTX\build> nmake serial
```

Thanks to @neophob for his [blog page](http://neophob.com/2011/05/serial-library-rxtx-v2-2pre5/).

# Compiling on macosx

Have the necessary tools in place. These are:

 - [git](http://git-scm.com/download/mac)
 - Java 1.6
 - [XCode Command Line Tools](http://stackoverflow.com/questions/9329243/xcode-4-4-command-line-tools)
 - glibtool

Then, in a new terminal, clone the repo, cd into its folder, then:

```bash
mkdir build
cd build
rm -rf *
CFLAGS="-arch i386" LDFLAGS="-arch i386" sh ../configure
sed -e 's|/System/Library/Java/JavaVirtualMachines/1.6.0.jdk/Contents/Home/../../../Headers|/System/Library/Frameworks/JavaVM.framework/Versions/Current/Headers|g' -i '' Makefile
sed -e 's|$(SHELL) glibtool|$(SHELL) glibtool --tag CC|g' -i '' Makefile
make
```