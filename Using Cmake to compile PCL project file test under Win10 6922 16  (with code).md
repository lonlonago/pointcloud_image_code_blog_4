>  Working environment: Windows 10 + Cmake 3.19.2 + VS2017 + PCL1.8.1 

 PCL1.8.1 download link  

 ![avatar]( 20210517105203325.png) 

>  Note: It is recommended to install pcl and the openni with the installation in the default path, that is, the C disk. The author changed the installation path, which caused the relevant file path to not be found during subsequent Cmake compilation, which added a lot of trouble

 If you need to install to a non-C disk, you need to set the header files and link library paths of each third-party library when configuring Cmake later, because the CMake-related search path in PCL will only search for relevant libraries in the C disk by default. 

  After installing the pcl, unzip the pcl-1.8.1-pdb-msvc2017-win64.zip file and copy the contents to the bin folder in the pcl installation folder: 

 ![avatar]( 20210517105941191.png) 

 ![avatar]( 20210517110036472.png) 

#   Establish a test project to test whether the pcl environment is well established 

 Reference: Official Tutorial Case - Write Point Cloud to PCD File 

  Create two new folders: one for source code files and one for compiled files 

 ![avatar]( 20210517110315219.png) 

  In the source folder, create a pcd_write and CMakeLists.txt file, the code content is not parsed for the time being, just a simple demonstration: 

 ![avatar]( 2021051711074320.png) 

 pcd_write.cpp： 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309573725035
  ```  
 CMakeLists.txt：  

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309573725035
  ```  
 Open CMake and start compiling: 

 ![avatar]( 2021051711095134.png) 

  After the compilation is complete, it is visible in the output folder: 

 ![avatar]( 20210517111046407.png) 

  Then open VS2017, open the project file, compile the link, and in the Debug folder, generate the .exe file: 

 ![avatar]( 2021051711121730.png) 

  Open this exe file with cmd.exe: 

 ![avatar]( 20210517111300613.png) 

  Finally, a PCD file is also generated: 

 ![avatar]( 20210517111404140.png) 

 The PCL test project runs smoothly, indicating that the PCL development environment is completed.  

