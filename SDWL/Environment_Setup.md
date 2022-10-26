[HOME](Home)
# SkyDRM Client SDK for Windows Environment Setup #

The following describes the requirement environment setup for SkyDRM Client SDK for Windows ("the SDK").

## Development Environment ##

Visual Studio 2015 is required for development using the SDK.

The following needs to be added to the project properties for your application:

**Include Directories**: *{SDK installation dir}*\include\SDWL

**Additional Library Directories**: *{SDK installation dir}*\bin\SDWL\$(Platform)_$(Configuration);*{SDK installation dir}*\bin\boost\$(Platform)\$(Configuration)

**Additional Dependencies**: SDWRmcLib.lib;libeay32.lib;urlmon.lib;bcrypt.lib;Crypt32.lib;winhttp.lib;shlwapi.lib;kernel32.lib;user32.lib;gdi32.lib;winspool.lib;comdlg32.lib;advapi32.lib;shell32.lib;ole32.lib;oleaut32.lib;uuid.lib;odbc32.lib;odbccp32.lib;Ws2_32.lib;Mpr.lib;Wtsapi32.lib;Secur32.lib

## Run-time environment ##

Visual C++ 2015 C Run-time Libraries needs to be present on the target machine.

The content of SDKLib_redist_x86.zip or SDKLib_redist_x64.zip (including any empty directories) needs to be extracted onto a directory of your choice (typically the top installation directory of your application) on the target machine.  You application needs to pass the full path of this directory to *SDWLibCreateSDRmcInstance()* in the *sdklibfolder* parameter.

If your application requires the SkyDRM Rights Protection Manager ("RPM"), it needs to be installed on the target machine using the appropriate RPM installer which can be found under the *{SDK installation dir}*\RPM directory.  The RPM installer can be invoked by your application's installer, your application itself, or the user of your application manually.

## Suggested design for application installer ##

The following is a list of suggested tasks for your application installer:

1. Place the appropriate RPM installer file in a temporary directory.
2. Invoke the RPM installer.
3. Extract the content of SDKLib_redist_x86.zip or SDKLib_redist_x64.zip onto your application's installation directory.
4. Record your application's installation directory in the Registry.  (This way your application can retrieve this from the Registry, and pass it to *SDWLibCreateSDRmcInstance()* in the *sdklibfolder* parameter.
5. Place your application's files in the installation directory.