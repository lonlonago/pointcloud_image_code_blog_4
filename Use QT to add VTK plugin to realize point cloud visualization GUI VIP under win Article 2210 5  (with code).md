abstract 

 We often use QT when making point clouds, but we need VTK when we need to use QT to make cloud visualizations. Although we have installed VTK when installing PCL under Windows, since the VTK installed with PCL is not compiled jointly with QT, it cannot be used when using PCL and QT to make point cloud visualization interfaces. However, QT's plug-in QVTKWidget, this article will mainly explain some sharing of PCL using QT as an interface on Ubuntu systems and Windows. 

 Using QT and PCL in Ubuntu 

 ![avatar]( 20200407183731830.jpg) 

 (1) If it is Ubuntu 14.04, whether it is using the command line to install PCL or QT, the system has already installed the QVTKWidget library, and will automatically load the QVTKWideget when using QT, and use my example to achieve the relevant functions of QT and point cloud with normal cmake. If you are interested, you can consult the github address of our official account. Of course, there are some basic examples in the official source code of PCL. In my experience, using it on ubuntu 14.04 should be no problem. (2) If you install ubuntu 16.04, it may be more troublesome, because when using it, you find that the dependency engineering of QT in PCL has not changed, and ubuntu 16.04 will install qt5 by default, which leads to some dependency conflicts, and even if you install the ROS package, there will be some problems, mainly because the PCL examples are dependent on QT4, and some libraries of Ubuntu 16.04 install QT5 by default, so it will cause you to compile but not, so if there is a problem, you can welcome discussion. 

 We know that it is very convenient to learn and use PCL under the Ubuntu system, and it is very convenient to install any third-party libraries. I will not explain too much here. 

 Using QT and PCL in Windows 

 On Windows, use PCL to achieve the visual interface of QT point cloud design, which involves the problem of engineering software. I believe most people use VS, so my computer has VS3013 and VS2015 installed. Here, I mainly use VS2015 to compile and implement the development of point cloud PCL. The development of GUI under VS. If you really need to use the interface under VS to design the visual interface of point cloud, then you can try to install the following steps, but there is no guarantee that it will be compiled, but even if you can't compile, as long as you install VS2015 and the program you compile is X64 release, then you can directly use the VTK library I compiled, which is convenient and worry-free. And at the end I will make a simple demo for everyone's test. 

 Installation and compilation steps, first download and install the version of PCL1.8windows to install normally, because we only need to replace the VTK part of the third-party library, and the libraries of other parts are intact. The third-party library that PCL1.8.1 relies on is VTK8.0, so we download a VTK source code and use cmake to compile. The next step is to take it step by step. Of course, you can skip it and directly download the QVTK library I compiled. 

 First of all, we need to install Qt5.8. This is very simple. Go directly to the Qt official website to search and download it, and install it all the way. There is nothing worth noting here. The next step is to use cmake to compile VTK. 

 ![avatar]( 20200407183823376.png) 

 (1) Start CMake, specify the source code directory and compilation directory, and click Configure. (2) The version of VS must be specified by the version you installed. I chose: Visual Studio 14 2015 Win64. Click finish and wait for the configuration to complete. The first cmake will be automatically performed. (3) After the first configure, you need to update the settings. First click advanced, and then we will find the following options to modify. The selection is the version that sets Qt for VTK. Here you need to select the location of the qt you have installed. Mainly, the two paths qmake.exe and Qtcmake.config are successfully specified. 

 ![avatar]( 20200407184043194.png) 

 If there is an error, you need to set it up normally. Here are actually the two places of qmake and qtcmake.config of QT. If the prompt DONXYGEN cannot be found, then build_decument the entire option is removed. In short, you need to configure the path of QT. If you don't know how to compile VTK cmake in win, it doesn't matter. If you also use Qt5.8 and use VS2013, the PCL version is 1.8.1 version, then you can directly download the VTK X64 library I have compiled. After cmake, we can generate the corresponding VS project file (5) Generate project. After the configuration is successful, the Configure done prompt appears. Click Generate to generate the project. (6) Start VS2015 to start the compilation. The Generating done prompt appears to indicate that the VS2015 project has been generated successfully. Click Open Project, VS2015 will launch and open the project.  

 Even if you do not compile successfully, it does not matter, here I have compiled the VTK package https://download.csdn.net/download/u013019296/12093433 (download points here is not my decision) decompression password is "dianyunPCL", the source code will be open source later. 

 Download the corresponding VTK, provided that you also ensure that you are using VS2015, QT 5.8, PCL1.8.1. After downloading the dependencies I compiled, you only need to copy the installation package to the thirdtarty of PCL1.8.1 we installed. It is generally no problem to set the path in the following program. 

 ![avatar]( 20200407184152463.png) 

 (7) Copy the QVTKWidgetPlugin.dll under 3rdParty\ QVTK\ plugins\ designer to QT\ 5.8\ msvc2015_64\ plugins\ designer, so that there are QVtk controls in Qt. This step will let you see when you open the QT_creator interface. There is one more control here. The whole time shows that you have installed successfully. If the installation is successful, it will be difficult to use it at one time. The following is to set the VS environment 

 The above is to correctly place the VTK plug-in in the third-party library of QT, but when we use the configuration environment, there are always some small problems, such as we forgot to set the X64 release mode during the above compilation, etc., the configuration environment 

 ![avatar]( 20200407184218970.png) 

 ![avatar]( 20200407184240521.png) 

 ![avatar]( 2020040718425746.png) 

 ![avatar]( 20200407184320143.png) 

 If all the preparations are over, let's create a new project in order to test some, configure the path to test whether there is a problem with the installation of our library (1) Download the VS2015_QT plug-in in VS2015, select "Extensions and Updates" (2) Select the network search and enter the keyword "qt" to download the first installation. (3) After the download is completed, restart VS2015, you will find the option "Qt VS Tool", set the path where qmake is located, and set the path where qmake is located in the "QT option". (4) At this time, we have completed all the preparations and can create a new QT project. At this point, the headache is the problem of setting various paths: here because everyone's installation path is different, but if you are skilled in using VS, you will know that the environment settings in VS actually only have three main key places including the path where the lib is located and the list of libs we need to use. Here is a screenshot of the settings file of my new project, hoping to enlighten you. List of lib paths: Finally, we need to enter the list of libs, the entire lib Because I don't know which one will be used temporarily, so generally I use all libs as input 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309573714292
  ```  
 There are more here, but they are not all listed. 

 Here we first try a VTK program to test whether our environment is configured successfully. 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309573714292
  ```  
 Generally, there is no problem. If there is a problem, you will be prompted for an initialization error when starting the VTK interface. This problem has been recorded in the previous blog, just add 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309573714292
  ```  
 ![avatar]( 20200407184358559.png) 

 After the compilation is successful, a plane is visualized in VTK. under win PCL joint QT point cloud GUI development 

 In the newly created VS project, we open .ui for interface editing. Note that in fact, the use of QT, you can directly use the code for typesetting, you can also typeset your controls in the interface, and then save them. At this time, QT will help you generate the corresponding code. For example, I found a UI interface and put two buttons, a QVTKWideget visualization plug-in and a text browser. The project needs to be realized: the first button realizes the opening of a PCD file visualization on the right plug-in, and the point cloud can be dragged freely with the mouse. The second button realizes the generation of a 5,000-point cube point cloud, and each click will change the color of the point cloud. QVTKWideget requires you to set the display position and the position in the interface. The text browser mainly explains the basic purpose of the program. Design as follows 

 ![avatar]( 20200407184524333.png) 

 ![avatar]( 20200407184544415.png) 

 ![avatar]( 20200407184552949.png) 

  I will not explain the specific name of each control one by one. After we layout and layout, we can click Save to realize the function of each button. Here, due to limited space, the implementation code will no longer be posted. Simple screenshots are as follows: Interested small partners can download the program to run on their own computer, download address: https://download.csdn.net/download/u013019296/12115883 

 ![avatar]( 2020040718460711.png) 

 This kind of GUI layout using QT has some limitations, that is, when we zoom in and out, the interface will not be beautiful enough, so many people will choose to use code typesetting, but code typesetting will make your code more. We try to open the program, as shown in the following figure: Description: 

 This is a "point cloud PCL" official account released on the use of VS2015 joint QT design of a point cloud visual interface of the program, has completed the package of the release of an exe, you can directly click on the exe on win7 to open the interface, the implementation of two buttons, one is to open a PCD file and visualization, as shown on the right, a button to generate a cube point cloud, and each button will change the color of the point cloud. 

 GitHub open source address: https://github.com/yaoli1992/dianyunPCL_QT_demo 

 If you have any questions, you can contact email: dianyunpcl@163.com, or apply to join the free knowledge planet as required, ask questions and comment on the planet. 

