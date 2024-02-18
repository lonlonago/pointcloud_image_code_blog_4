Text tutorial: 

  Win10 + VS2015 + PCL_1 Configuration 

 Win10 + VS2015 + PCL_1 software installation 

 Win10 + vs2015 + pcl1.8.1 installation stepping pit 

 Video Tutorial: 16-PCL Tutorial - Basic Applications - Install PCL under win10 

 I installed it according to the video tutorial, and there were some problems in the middle. The records are as follows: 

 directory 

 error C4996: 'std::fpos<_Mbstatet>::seekpos': warning STL4019 

 Cannot open file "libboost_ system-vc140-mt-gd-x64-1 _68"  

 Notes on adding dependencies: 

 Cannot open file "libboost_ thread-vc141-mt-sgd-1 _65_1" 

 Lost OpenNI2.dll in computer 

#  error C4996: 'std::fpos<_Mbstatet>::seekpos': warning STL4019 

>  _CRT_SECURE_NO_WARNINGS

_SCL_SECURE_NO_WARNINGS

_SILENCE_FPOS_SEEKPOS_DEPRECATION_WARNING 

#  Cannot open file "libboost_ system-vc140-mt-gd-x64-1 _68"  

 Unable to open the lib file, first check whether the name of the dependency library added by yourself is consistent with the name of the local dependency library: The name of the dependency library given by the online tutorial is not necessarily the name of the local dependency library: For example, a dependency file name in the tutorial is called: libboost_ system-vc140-mt-gd-x64-1 _68 .lib, and the name of the local dependency library is: libboost_ system-vc141-mt-gd-x64-1 _68 .lib. If you add it according to the dependency library file name in the tutorial of others, there will be an error that the file cannot be opened. 

 Local file: 

 ![avatar]( 20210215145405330.png) 

 Dependency library names given in some tutorials: 

>  libboost_atomic-vc140-mt-gd-1_61.lib libboost_chrono-vc140-mt-gd-1_61.lib libboost_container-vc140-mt-gd-1_61.lib libboost_context-vc140-mt-gd-1_61.lib libboost_coroutine-vc140-mt-gd-1_61.lib libboost_date_time-vc140-mt-gd-1_61.lib libboost_exception-vc140-mt-gd-1_61.lib libboost_filesystem-vc140-mt-gd-1_61.lib libboost_graph-vc140-mt-gd-1_61.lib libboost_iostreams-vc140-mt-gd-1_61.lib libboost_locale-vc140-mt-gd-1_61.lib libboost_log-vc140-mt-gd-1_61.lib libboost_log_setup-vc140-mt-gd-1_61.lib libboost_math_c99-vc140-mt-gd-1_61.lib libboost_math_c99f-vc140-mt-gd-1_61.lib libboost_math_c99l-vc140-mt-gd-1_61.lib libboost_math_tr1-vc140-mt-gd-1_61.lib libboost_math_tr1f-vc140-mt-gd-1_61.lib libboost_math_tr1l-vc140-mt-gd-1_61.lib libboost_mpi-vc140-mt-gd-1_61.lib 

 The difference is that the version is inconsistent, the tutorial is 140 (vs2015), and the local is 141 (vs2017). 

##  Notes on adding dependencies: 

#  Cannot open file "libboost_ thread-vc141-mt-sgd-1 _65_1" 

 Solution: Right-click properties - C/C++ - code generation - runtime, change to multi-threaded debugging DLL (/MDd) 

#  Lost OpenNI2.dll in computer 

 workaround 

 (1) The first method: put OpenNI2.dll in the OpenNI2\ Tools directory under the installation path into your exe directory. For example, my installation path is C:\ Program Files (x86) \ OpenNI2.dll\ Tools, and my VS2013 project path is D:\ VS2013 Project\ setting_PLC\ setting_PLC. Put OpenNI2.dll in the installation path under the project path. (2) The second method is to put OpenNI.dll in the C:\ Windows\ System32 folder. 

#  Dependency packages used in debug mode 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309573731584
  ```  
#  Include directory: 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309573731584
  ```  
#  Library directory: 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309573731584
  ```  
