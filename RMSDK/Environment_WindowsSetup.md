[RMCCore Library](Home)

# How to setup development environment for Windows
The recommended IDE is Visual Studio 2015.  
The following instruction is based on VS2015 and SDK version 10.0.16299

## Header file and Binary
Create Git repository of [RMCSDK-Wiki](https://bitbucket.org/nxtlbs-devops/rmcsdk-wiki/src).  
Sync **include** folder for header files.  
Sync **bin** folder for preferred location of linked library.   
Extract library binary files from RMSDK release package to **bin** folder.  

**Note**: *Library binary files are not included in Git repository. It is released separately.*

## Dependency
RMSDK is depends on [OpenSSL FIPS modules](https://wiki.openssl.org/index.php/FIPS_module_2.0)  
recommend following [Linker](#markdown-header-Linker) and [Running Environment](#markdown-header-Running-Environment) options for the app setting unless you know the encryption/key related function is not called.


## General
Using default or user preferred.

## Compiler
Add **include** folder path in *Additional Include Directories* setting under **C/C++ ->General**  
Here is the path sample for RMDCoreSample solution  
> ..\\..\\..\\include  
**Note: Donot add RMSDK to the path!**

Change *Runtime Library* setting under **C/C++ ->Code Generation** to  
**Multi-thread Debug(/MTd) for debug build**  
**Multi-thread (/MT) for release build**  

## Linker
Add **bin** folder path in *Additional Library Directories* setting under **Linker->General**  
Here is the path sample for RMDCoreSample solutin  
> ..\\..\\..\\bin\\RMSDK\Windows\$(Platform)_$(Configuration)

Add following library in *Additional Dependencies* setting under **Linker->Input**  
>rmsdk.lib libcrypto.lib

## Running Environment
copy following dll to same directory of executable file or system path
> libeay32.dll for 64bit
> libeay32.dll for 32bit

# How to build RMD-Core and RMDSDK using build scripts #

## RMD-Core ##
1. In the Command Prompt window that you’ll use for building, set BOOST_ROOT to the directory of the Boost 1.65.1 distribution from Perforce, e.g. "C:\p4\git_external\Boost\boost_1_65_1".  (Alternatively, you can set BOOST_ROOT system-wide.)
2. Make sure you S: drive is connected to \\nextlabs.com\share\data.  (It should already have been connected automatically when you log on to your Dev machine using your NEXTLABS domain account.)
3. CD to the build\scripts directory.
4. To build all four versions, run the command "buildCoreAll.bat".  To build only one version, run e.g. the command "buildCoreDebug32.bat".  (These commands copy lots of files when you run them the first time, but they should be faster when you run them subsequent times.)
5. Repeat only #4 every time you want to build again.
6. To clean, run the command "cleanCoreAll.bat", or "cleanCoreDebug32.bat", etc.

## RMDSDK ##
1. Make sure the Cygwin unzip.exe utility is somewhere in your path.
2. Make sure you S: drive is connected to \\nextlabs.com\share\data.  (It should already have been connected automatically when you log on to your Dev machine using your NEXTLABS domain account.)
3. CD to the build\scripts directory.
4. To build all four versions, run the command "buildAPIAll.bat".  To build only one version, run e.g. the command "buildAPIDebug32.bat".  (These commands copy lots of files when you run them the first time, but they should be faster when you run them subsequent times.)
5. Repeat only #4 every time you want to build again.
6. To clean, run the command "cleanAPIAll.bat", or "cleanAPIDebug32.bat", etc.