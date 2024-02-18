The previous article introduced the use of RandLA-Net to train the Semantic 3D dataset in the tensorflow 2.0 environment. Here we document how to train the S3DIS dataset with RandLA-Net in the tensorflow 2.0 environment. 

 Since the code provided by the author is based on tensorflow 1.11, some modifications are required to run the program in the 2.0 environment. The modification method has been given in the training Semantic3D dataset. 

#  Training the S3DIS dataset 

 1, download the dataset, the author used Stanford3dDataset_v1, the entire compressed package downloaded is 4.79G, after decompression there are 30 G. 

 2, data set preprocessing, data set download decompression, there is a certain error in the original data source, Area_5\ office_19\ Annotations\ ceiling_1 there is a line of data contains characters, resulting in data operation failure, see the detailed process of using NumPy to load txt file prompt ValueError: could not convert string to float. 

 Then execute the following statement 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309573789636
  ```  
 3. 60% off cross-training, first modify your data path, and then execute the following code 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309573789636
  ```  
 4. Verify, copy all ply files in the test folder to the/data/S3DIS/results folder 

 ![avatar]( 8d692fc848b2425ebb154607e4a96967.png) 

 Run script 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309573789636
  ```  
 ![avatar]( d0f980a9a34d4fe9921dfddc46335c53.png) 

 The final evaluation result is that I can see that the miou trained by myself is 68.4%, and the result of the author's training is 70.0%. The other types of scores are compared as follows:  



--------------------------------------------------------------------------------

 Use open3D to read and write pcd files, using the Open3D.io read and write functions, this library can only read and write the coordinates and color of the point cloud these two basic properties, can not obtain the intensity of the point cloud (intensity), normal vector and other attribute information, Open3D provides t.io library can obtain additional attribute information, usage is as follows: open3d.t.io read intensity information 

#  open3d.t.io 

##  read 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309573739358
  ```  
 Note that the data obtained by directly reading is of type tensor, and if you want to convert it to a numpy array, you need to use the .numpy () method. 

##  write 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309573739358
  ```  
 ![avatar]( a3e9b25c529844d6989c272494898bde.png) 



--------------------------------------------------------------------------------

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



--------------------------------------------------------------------------------

In the.h file 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309573775798
  ```  
 In .cpp 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309573775798
  ```  


--------------------------------------------------------------------------------

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



--------------------------------------------------------------------------------

#  1. Pytorch version KPConv model github address 

 KPConv-PyTorch 

#  System environment 

 System: win10 torch: 1.7 cuda: 10.1 cudnn: 7.6.5 graphics card: 2080TI 

#  Third, bug modification 

 3.1, compile the sampling and nearest neighbor search module bug author to compile the method is, in the win10 system, compile cpp_neighbors and cpp_subsampling, respectively 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309573757409
  ```  
 and 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309573757409
  ```  
 I myself in the win10 system under the test found that the execution of build.bat will prompt no py command, if you also encounter the same problem, you can follow the following operation to compile, compile cpp_neighbors, under cmd into the cpp_warppers\ cpp_neighbors folder, execute the following statement 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309573757409
  ```  
 The method of compiling cpp_subsampling is the same as above. 

 3.2, read data using multithreading bug modify config file does not use multithreading, in line 62 of the train_S3DIS.py 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309573757409
  ```  
 3.3, the video memory is not enough, modify the batch size in the config file in line 153 of the train_S3DIS.py 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309573757409
  ```  
 3.4、loss计算错误，提示Expected object of scalar type Long but got scalar type Int for argument #2 ‘target’ in call to _thnn_nll_loss2d_forward。 

 Error location on line 189 of utils\ trainer.py 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309573757409
  ```  


--------------------------------------------------------------------------------

Visualize the depth image as a point cloud in a 3D window (the depth image comes from the point cloud), and the other is to map the depth value to color to visualize the depth image as a color image. 

 New project ch4_2, new file range_image_visualization cpp, fill in the following 

 The result of compiling and running the executable file is: 

 Run./range_image_visualization (no .pcd file specified) 

 ![avatar]( aHR0cDovL2ltYWdlczIwMTUuY25ibG9ncy5jb20vYmxvZy85NzYzOTQvMjAxNzAyLzk3NjM5NC0yMDE3MDIyNjEzMjEwMTA1NC0xNjA3NTEwMzcwLnBuZw) 

 Using an automatically generated rectangular space point cloud, there are two windows, a 3D visualization window for the point cloud and a visualization window for the depth image, where the color of the image is determined by the depth. 

 ![avatar]( aHR0cDovL2ltYWdlczIwMTUuY25ibG9ncy5jb20vYmxvZy85NzYzOTQvMjAxNzAyLzk3NjM5NC0yMDE3MDIyNjEzMzA0NTM4Mi04MzIzNzk4MzYucG5n) 

 Of course, if you specify the PCD file can also be, for example:./range_image_visualization room_scan1 pcd the result                             

 WeChat official account number can scan the QR code to learn and communicate together 

 ![avatar]( aHR0cDovL2ltYWdlczIwMTUuY25ibG9ncy5jb20vYmxvZy85NzYzOTQvMjAxNzAzLzk3NjM5NC0yMDE3MDMwMzEzNDgwNzA5NS0yMjQxNzQyMDUuanBn) 



--------------------------------------------------------------------------------

This article is an excerpt from an industry analysis survey report on the VR/AR field by the investment industry, which was published in June 2020. This article only extracts some opinions from it, and it is only for sharing. If there is any infringement, please contact to delete it. 

 If you are interested in viewing the full text, you can send "VR" in the background of the WeChat official account to get the electronic version of the full report. 

 core point of view 

 The inflection point of the VR/AR industry has emerged: VR/AR experienced a capital boom in 2016, but due to the immature timing, it gradually cooled down. With the continuous investment of industrial capital, the continuous release of policy dividends, and the continuous efforts of industry giants in hardware, software, content, and applications, the VR/AR industry has been improved in all aspects, and the integration of application scenarios and VR/AR has been continuously improved. The industry has turned warm and ushered in an inflection point. Since March 2020, benefiting from the promotion of the popular VR game ALYX, the VR market has ushered in great attention, and VR/AR is expected to usher in an upward inflection point. 

 5G is expected to open the VR/AR ceiling: 5G has the characteristics of low latency and large bandwidth, which can realize cloud VR/AR solutions, use the powerful CPU and GPU in the cloud to complete calculation and rendering, and use 5G to complete transmission to VR/AR devices. It not only realizes better content while reducing the computing power requirements of the end point of the all-in-one machine, but also saves costs. At the same time, due to the reduction of computing power, it also reduces the demand for heat dissipation, which helps to save unnecessary heat dissipation modules and reduce the volume and weight of the end point of the all-in-one machine, making it more lightweight. The cloud VR/AR solution in the 5G era can significantly improve the user experience, which is expected to further open the C-end market and drive the development of the B-end market such as education, medical care, tourism, shopping, real estate, engineering and other scenarios, thus completely opening the industry ceiling. 

 The development of VR/AR 

 ![avatar]( 20210306145815186.gif) 

 VR/AR development history 

 In 2019, industry giants released new products intensively, and product technology was significantly upgraded. VR/AR is becoming cheaper and easier to use. VR products: In 2019, Valve released its first VR product, Valve Index HMD, and Oculus (Facebook), HTC, Huawei, Xiaomi and other manufacturers have also launched new VR hardware products. The new generation of products is constantly improving and overcoming the painpoints of VR/AR devices in the past, and the price has become affordable. VR/AR is expected to usher in rapid development. 

 ![avatar]( 20210306145815186.gif) 

 VR/AR product launches by major manufacturers in 2019 

 The core pain points are gradually overcome, and VR/AR is expected to usher in high-speed growth. All-round hardware upgrades will greatly improve the immersive experience. Users have been looking forward to VR/AR for a long time. The core reason is that VR/AR can bring immersive experiences to users. Combined with many industries, especially in the gaming, travel, and film industries, through panoramic visual, touch, hear, and smell interactive experiences, people have an immersive feeling. The application of VR/AR technology can bring humans into the era of "time travel" and "virtual world". 

 ![avatar]( 20210306145815185.gif) 

 The current VR products have reached the standard of partial immersion 

 VR/AR technology development 

 AR optical waveguide technology is gradually maturing and is expected to lead AR glasses to the consumer market. There are four main AR optical display solutions, including prisms, curved reflectors, optical waveguide solutions and light field display solutions. 

 ![avatar]( 20210306145815188.gif) 

 Comparison of four main optical schemes of AR 

 Perceptual interaction: The depth camera is mature to help space positioning and 3D input, 6 + 6DoF is very large, and the inside-out space positioning method has become a development trend to improve the user interaction experience. There are currently two main types of VR/AR device space positioning: Outside-in and Inside-out. Outside-in is an outward-inward motion tracking device, using an external tracking device, such as a camera or Lighthouse, and tagging the headset to track the motion of the headset. Outside-in technology has obvious advantages, high accuracy, and because the amount of data transmitted is small, the delay of calculation is also low, which reduces the discomfort caused by some delays. And alternative solutions are more mature, reducing costs to a certain extent. However, this method also has significant shortcomings: 

 1) Occlusion: If you suddenly squat down and are blocked by an object, the sensor will not be able to track the user's location. 

 2) Space limitations: Outside-in will set the user in a range such as 3 × 3, and once out of range, the sensor cannot track it. 

 3) Setup is cumbersome: Before playing the game, you need to turn on the power supply of two sensors. In contrast to Outside-in, Inside-out is an inside-out tracking system that relies on depth cameras for 3D space input, combined with Simultaneous Localization and Mapping algorithm (SLAM, Simultaneous Localization and Mapping) to track the target. Inside-out technology is not limited by space and is simple to set up, and is expected to become the technology trend of future VR/AR devices. 

 ![avatar]( 1f213e7f179cd3a3497033efc8a8dad6.png) 

 ![avatar]( 083a2dee0b2674f9382d32dd8bf82897.png) 

 HoloLens uses depth camera for inside-out tracking technology 

 ![avatar]( 9c9cfa26ca9e8329fdb208d68a47bc79.png) 

 iPad Pro uses 3D TOF to achieve rich AR capabilities 

 VR/AR applications 

 ![avatar]( 20210306145815185.gif) 

 ![avatar]( 20210306145815185.gif) 

 5G is expected to open the VR/AR growth ceiling. 5G has three major characteristics: 

 1) Large broadband: 20G downlink rate; 

 2) Low latency: 1ms ultra-low latency; 

 3) Large connection: per kilometer, connect super 1 million devices. 5G boosts the cloud-based processor, enhances the level of computing power, simplifies equipment and reduces costs. 

 ![avatar]( 780647ad27e972f30173da357478f4ce.png) 

 5G boosts VR/AR to the cloud, simplifying equipment 

 This article is for academic sharing only. If there is any infringement, please contact to delete it. The full text of the pdf has been shared to Free Knowledge Planet. 

 resource 

 3D point cloud paper and related application sharing 

 [Point cloud paper speed reading] Odometer based on lidar and positioning method in 3D point cloud map 

 3D object detection: MV3D-Net 

 Overview of 3D Point Cloud Segmentation (Part 1) 

 3D-MiniNet: Learning 2D Representations from Point Clouds for Fast and Efficient 3D LIDAR Semantic Segmentation (2020) 

 Use QT to add VTK plug-in under win to realize point cloud visualization GUI 

 JSNet: Joint Instances and Semantic Segmentation for 3D Point Clouds 

 A Survey of Semantic Segmentation of 3D Point Cloud in Large Scene 

 The outofcore module in PCL---Display of large-scale point clouds based on out-of-core octree 

 Target Segmentation Based on Local Convex 

 Point cloud labeling based on 3D convolutional neural networks 

 SuperVoxel of Point Cloud 

 Large-scale point cloud segmentation based on hyperdot graph 

 More articles can be viewed: A summary of historical articles on point cloud learning 

 SLAM and AR related sharing 

 [Open source solution sharing] ORB-SLAM3 is open source! 

 AVP-SLAM: Semantic SLAM in Automatic Parking Systems 

 [Point Cloud Paper Speed Reading] StructSLAM: Structured Line Feature SLAM 

 SLAM and AR Overview 

 Commonly used 3D depth cameras 

 Overview and Evaluation of Monocular Vision Inertial Navigation SLAM Algorithm for AR Devices 

 SLAM Review (4) Laser and Vision Fusion SLAM 

 Kimera's Semantic SLAM System for Real-Time Reconstruction 

 Overview of SLAM (3) - Vision and inertial navigation, vision and deep learning SLAM 

 Extensible SLAM Framework - OpenVSLAM 

 Gao Xiang: Challenges in unstructured road laser SLAM 

 SLAM Overview of Lidar SLAM 

 SLAM Method Based on Fisheye Camera 

 Online sharing and recording summary in the past 

 3D Model Retrieval Technology of the First Bilibili Recording 

 Application of deep learning in 3D scenes recorded and broadcast by Bilibili 

 The third Bilibili recording of CMake advanced learning 

 Point Cloud Object and Six-Degree-of-Freedom Attitude Estimation Recorded by Bilibili 

 The fifth Bilibili recording of point cloud deep learning semantic segmentation expansion 

 Pointnetlk Interpretation of the 6th Bilibili Recording 

 [线上分享录播]点云配准概述及其在激光SLAM中的应用 

 [线上分享录播]cloudcompare插件开发 

 [线上分享录播]基于点云数据的 Mesh重建与处理 

 [线上分享录播]机器人力反馈遥操作技术及机器人视觉分享 

 [线上分享录播]地面点云配准与机载点云航带平差 

 ![avatar]( e60ce141289e059f3b793c6b8bc4049b.png) 

 Scan QR code 

                    Follow us 

 Let's share and learn together! Looking forward to friends who have ideas and are willing to share joining the free planet to inject fresh vitality of love and sharing. The topics shared include but are not limited to 3D vision, point clouds, high-precision maps, autonomous driving, and robotics and other related fields. 

 Sharing and cooperation: WeChat "920177957" (note required) Contact email: dianyunpcl@163.com, enterprises are welcome to contact the official account for cooperation. 



--------------------------------------------------------------------------------

 Recently working on a project using Qt + Cmake + VS: Use Cmake to compile a Qt project and then develop it in VS. 

 The project structure is as follows: 

 ![avatar]( a8f2c7ebbbe44ae388593fc2ac49c286.png) 

  After compiling with Cmake, open the project, and the following problem occurs: 

 ![avatar]( f6e3c0e3da3f4adbabe0194b9c4a95f3.png) 

  The reason is simple. VS did not find the UI header file. 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309573725528
  ```  
 As can be seen in VS, there are four ui_mainwindow files with the same name: 

 ![avatar]( 01d38d090ad34ee8b12e5e64b04d7270.png) 

  But only one of them can be opened, and the other double-clicking to open will cause an error: 

 ![avatar]( 0799db0d5e6c4f1c9b19bd3bbd4710fb.png) 

 Remove the error file to solve the problem: 

 ![avatar]( 4b7a1b112d6e4e26a7661bec1ea4ccca.png) 



--------------------------------------------------------------------------------

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


--------------------------------------------------------------------------------

Recently in the learning PCL, in Win10 using VS to write PCL programs, configuration environment often error, step pit records see: Win10 + VS2017 + PCL_1 software installation, step pit records 

 I saw that cmke was used in the book "Point Cloud Library PCL From Entry to Mastery". I found that using cmake is more concise and fast, and it is not easy to make mistakes. Test records: Use Cmake to compile PCL project files under Win10 for testing 

#  Preparation of CMakeLists files 

 With cmake, the most crucial step is to write the CMakeLists file. Then record the commands commonly used in PCL. 

 CMakeLists.txt file example: 

>  cmake_minimum_required(VERSION 2.8 FATAL_ERROR)

project(pcd_write)

find_package(PCL 1.2 REQUIRED)

include_directories(${PCL_INCLUDE_DIRS}) link_directories(${PCL_LIBRARY_DIRS}) add_definitions(${PCL_DEFINITIONS})

add_executable (pcd_write pcd_write.cpp) target_link_libraries (pcd_write ${PCL_LIBRARIES}) 

 Explanation:  

>  Define the minimum version, which is mandatory for cmake because you are doing a very basic project that does not require functionality from cmake 2.8 or higher. cmake_minimum_required (version 2.8 FATAL_ERROR) 

>  Project name project (pcd_write)//The pcd_write here is the name of the project folder 

>  find_package () command is used to find the dependency package, you can put a whole dependency package header file including path, library path, library name, version number and so on are obtained to find_package (PCL 1.2 REQUIRED)

We asked to find the PCL package with a minimum version of 1.2, if not, it will fail

Since PCL is modular, it is possible to:

Only one component: find_package (PCL 1.3 REQUIRED COMPONENTS io) Some: find_package (PCL 1.3 REQUIRED COMPONENTS io common) All already exists: find_package (PCL 1.3 REQUIRED) 

>  include_directories(${PCL_INCLUDE_DIRS})

link_directories(${PCL_LIBRARY_DIRS})

add_definitions(${PCL_DEFINITIONS}) 

  When the PCL is found, some relevant variables will be set: 

 To let cmake know what external header files are included in the project, you need to use include_directories macros. In our case, PCL_INCLUDE_DIRS contains what we need, so we ask cmake to search the path it contains for possible header files. 

>  include_directories (${PCL_INCLUDE_DIRS}) parameter form * _INCLUDE_DIRS, the variable is find_package path and other paths that need to be included 

>  link_directories (${PCL_LIBRARY_DIRS}) is used to load the additional library function path, the path of the linked library file, which is sometimes not necessary. Because find_package and find_library directives can get the absolute path of the library file. 

>  add_excutable (pcd_write pcd_write cpp) use the given source file to introduce an executable file for the project

Here we tell cmake that we are trying to create an executable named pcd_write from a source file pcd_write .cpp. CMake will add the suffix (.exe on Windows and blank on UNIX) and permissions. 

>  add_dependencies () is generally not used. The case used is that the two targets have dependencies (solved by target_link_libraries) and the dependency library is also generated by compiling the source code. At this time, add_dependencies can automatically check whether the lower-level dependency library has been generated when directly compiling the upper-level target. If not, compile the lower-level dependency library first, then compile the upper-level target, and finally link depends target 

>  target_link_libraries (pcd_write ${PCL_LIBRARIES}) to add a linked library; link the target file to the library file.

The executable we are building calls the PCL function. So far we have only included the PCL header file, so the compiler knows which method we are calling. We also need to let the linker know which library we are linking to. As mentioned earlier, use the PCL libraries variable to reference the library found by PCL, and all that is left is the linking operation that triggers us to call the target link library () macro. 

 PCLConfig.cmake uses a special CMake feature called EXPORT, which allows you to work with other project targets as if you were building them yourself. When using such targets, they are called import targets and act like any other target. 

#  Printing of Cmake variables 

 The message method in Cmake is message, which is used to output log information in the cmake project during compilation, and can also be used to view log information at any time during breakpoint debugging.  

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309573614925
  ```  
>  Message: Message name, can be entered in the CMakeLists.txt or .cmake script file, and there is a prompt, insensitive to case mode: Print the type of message, there are FATAL_ERROR, SEND_ERROR, WARNING, AUTHOR_WARNING, DEPRECATION, (none) or NOTICE, STATUS, VERBOSE, DEBUG, TRACE A total of 10 "message to display": The content of the output message, is a string type...: Represents variable parameters, can be connected to multiple output 

##  Mode - type of print message 

  Example of use: 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309573614925
  ```  
 Output result: 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309573614925
  ```  
 Reference link: 

 Using PCL in your own project — Point Cloud Library 0.0 documentation 

 https://blog.csdn.net/Calvin_zhou/article/details/104025714 



--------------------------------------------------------------------------------

Point cloud PCL free knowledge planet, point cloud paper speed reading. 

 标题：Fast 3D Line Segment Detection From Unorganized Point Cloud 

 Author: Xiaohu Lu, Yahui Liu, Kai Li 

 Compiled by: particle 

 Welcome to join the free knowledge planet, get PDF papers, and welcome to forward Moments to share your happiness. 

 This paper proposes a 3D line segment detection algorithm based on large-scale disordered point cloud. Compared with the traditional method of extracting 3D edge points first and then fitting 3D line segments, this paper proposes a 3D line segment detection algorithm based on point cloud segmentation and 2D line segment detection. In the case of input disordered point cloud, three-step detection of 3D line segments is performed. First, the point cloud is divided into 3D planes by region growth and region merging. Secondly, for each 3D plane, all the points to which it belongs are projected onto the plane to form a 2D image, and then 2D contour extraction and least squares fitting are performed to obtain 2D line segments. Then these 2D line segments are re-projected on the 3D plane to obtain the corresponding 3D line segments. Finally, a post-processing method for removing outliers and merging adjacent three-dimensional line segments is proposed. Experiments on multiple public datasets demonstrate the effectiveness and robustness of the method. 

 More results and C++ open source code in https://github.com/xiaohulugo/3DLineDetection 

 Main contribution 

 The method proposed in this paper still belongs to the category of images, but for the shortcomings of image-based methods, a faster line segment detection method for 3D point cloud data is proposed. The method mainly includes three parts: 

 (1) Point cloud segmentation: By means of region generation and region merging, the input point cloud is divided into three-dimensional planes. 

 (2) Detection of three-dimensional straight lines based on the plane: For each point cloud plane, all point clouds belonging to the plane are projected onto the plane to form a two-dimensional image, and then contour extraction and least squares fitting are performed based on the two-dimensional image to obtain two-dimensional line segments of each plane. Finally, these two-dimensional line segments are mapped to the three-dimensional plane to obtain three-dimensional line segment point cloud data. 

 (3) Post-processing: Through the three-dimensional structure information of the scene, the abnormal point cloud of the three-dimensional plane and the three-dimensional line segment is removed, and finally all the three-dimensional line segment point cloud data is merged. 

 Paper step atlas 

 ![avatar]( 20200705153750888.PNG) 

 Module A little cloud segmentation, this module mainly has three steps 

 Point cloud normal vector computing 

 region generation 

 Regional merger 

 ![avatar]( 20200705153810772.PNG) 

  Module 2 is based on the extraction of the three-dimensional line segment of the segmented plane. The steps are as follows 

 3D-2D projection 

 Line detection of 2D images (detection method is LSD reference [1]) 

 2D-3D mapping 

 ![avatar]( 20200705153822426.PNG) 

  Module 3 Post-processing, noise removal 

 Noise removal plane point cloud 

 Noise removal line segment point cloud 

 All line segment point clouds merge 

 ![avatar]( 20200705153834654.PNG) 

 Experimental results and summary   

 This paper proposes and proves a simple and effective 3D line detection algorithm for large-scale unorganized point clouds. This method is based on point cloud segmentation and 2D line detection, and uses post-processing methods to remove outliers. Unlike traditional edge point-based methods, this method is simple to implement and fast (100,000 point clouds for 40 seconds). Since our method is based on point cloud segmentation, a failure case of our method is on curved surfaces, and the segmentation effect of planes in curved point clouds is unsatisfactory. Despite this, the method is very effective for structural scenes. 

 References 

 【1】R. G. von Gioi, J. Jakubowicz, J.-M. Morel, and G. Randall, “LSD: A fast line segment detector with a false detection control,” IEEE Transactions on Pattern Analysis and Machine Intelligence. 

 If you are interested in this article, please click "Original Reading" to get the QR code of Knowledge Planet. Be sure to join the free Knowledge Planet according to the remarks of "Name + School/Company + Research Direction", download the pdf document for free, and communicate with more friends who love to share! 

 ![avatar]( 20200705153852662.PNG) 



--------------------------------------------------------------------------------

Point cloud PCL free knowledge planet, point cloud paper speed reading. 

 标题：MoreFusion: Multi-object Reasoning for 6D Pose Estimation from Volumetric Fusion 

 作者：Kentaro Wada, Edgar Sucar, Stephen James 

 Planet ID: wl_ Huake _ point cloud processing _ target recognition 

 Welcome to join the free knowledge planet, get PDF papers, and welcome to forward Moments to share your happiness. 

 Abstracts of papers 

 Robots and other intelligent devices need to achieve efficient target-level scene representation for contact, physical, occlusion, and other inferences based on their own vision systems. Known accurate target models play a very important role in the non-parametric reconstruction of unknown structures. We propose a system that can estimate the precise pose of contacting and occluding known targets in real-time multi-view scenes. Our method can estimate the pose of 3D targets from a single RGBD perspective. As the camera moves, it can accumulate pose estimation and non-parametric occupancy information from multiple perspectives, and perform joint optimization to perform consistent non-intersecting pose estimation for multiple contact targets. 

 We experimentally validate the accuracy and robustness of our proposed method in two datasets, YCB-Video and Cluttered YCB-Video. We demonstrate an implemented robotic application that is able to precisely and orderly grasp complex stacked objects using only the RGB-D information it carries. 

 https://github.com/j96w/DenseFusion 

 ![avatar]( 20200524215334569.JPG) 

 Paper Atlas      

 ● English abstract 

 ![avatar]( 2020052421541787.JPG) 

 Robots and other smart devices need efficient objectbased scene representations from their on-board vision systems to reason about contact, physics and occlusion. Recognized precise object models will play an important role alongside non-parametric reconstructions of unrecognized structures. We present a system which can estimate the accurate poses of multiple known objects in contact and occlusion from real-time, embodied multi-view vision. Our approach makes 3D object pose proposals from single RGBD views, accumulates pose estimates and non-parametric occupancy information from multiple views as the camera moves, and performs joint optimization to estimate consistent, non-intersecting poses for multiple objects in contact. We verify the accuracy and robustness of our approach experimentally on 2 object datasets: YCB-Video, and our own challenging Cluttered YCB-Video. We demonstrate a real-time robotics application where a robot arm precisely and orderly disassembles complicated piles of objects, using only on-board RGB-D vision  



--------------------------------------------------------------------------------

Point cloud PCL free knowledge planet, point cloud paper speed reading. 

 标题：Learning to Optimally Segment Point Clouds 

 作者：Peiyun Hu, David Held 

 Planet ID: particle 

 Welcome to join the free knowledge planet, get PDF papers, and welcome to forward Moments to share your happiness. 

 Abstracts of papers 

 We propose an approach that combines graph-theoretic search with data-driven learning: searching a set of candidate segmentation for candidate segmentation with a high composite objectivity score. We demonstrate that if the segmentation is scored according to the lowest objectivity in the segmentation, then there is an efficient algorithm that can find the optimal worst-case segmentation in an exponential number of candidate segmentation. In addition, we also propose an efficient algorithm for the average case. For evaluation, we reuse the KITTI 3D detection as a segmentation benchmark, and empirically demonstrate that our algorithm performs significantly better on segmentation point clouds than past bottom-up segmentation methods and top-down object-based algorithms. 

 Main contributions 

 • Use geometric constraints to reduce the number of candidate partitions and build a tree structure 

 • Utilize tree structure for optimal segmentation search, and propose an efficient search algorithm that can be applied to dynamic programming 

 This paper uses KITTI as an experimental dataset, and the results of point cloud segmentation and point cloud instance segmentation are shown in the following figures TABLE I and TABLE II: The proposed method performs worse in common classifications such as car than SECOND ++, but performs better in rare classifications such as misc. 

 Paper Atlas 

 ![avatar]( 2020052422170361.JPG) 

 ● English abstract 

 ![avatar]( 20200524221728204.JPG) 

 We focus on the problem of class-agnostic instancesegmentation of LiDAR point clouds. We propose an approachthat combines graph-theoretic search with data-driven learning:it searches over a set of candidate segmentations and returnsone where individual segments score well according to a datadriven point-based model of “objectness”. We prove that ifwe score a segmentation by the worst objectness among itsindividual segments, there is an efficient algorithm that findsthe optimal worst-case segmentation among an exponentiallylarge number of candidate segmentations. We also present anefficient algorithm for the average-case. For evaluation, werepurpose KITTI 3D detection as a segmentation benchmarkand empirically demonstrate that our algorithms significantlyoutperform past bottom-up segmentation approaches and topdown object-based algorithms on segmenting point clouds.  



--------------------------------------------------------------------------------

Point cloud PCL free knowledge planet, point cloud paper speed reading. 

 标题：PAIRWISE LINKAGE FOR POINT CLOUD SEGMENTATION 

 作者：Lu, Xiaohu and Yao, Jian and Tu 

 Planet ID: Lionheart | Point Cloud Registration 

 Welcome to join the free knowledge planet, get PDF papers, and welcome to forward Moments to share your happiness. 

 Abstracts of papers 

 In this article, we first propose a novel hierarchical clustering algorithm --pairwise linkage (p-linkage), which can be used to cluster data of any dimension, and then efficiently applied to the classification of 3D unstructured point clouds. The P-linkage clustering algorithm first calculates the characteristic value of each point, such as calculating the density of 2D points and the smoothness of 3D points, and then uses more characteristic values to describe the link relationship between each point and its nearest neighbor. The initial clustering can be carried out more easily through the linking of point pairs. Then, the clustering fusion process obtains the final optimized clustering result, and the clustering result can be used in other applications. Based on P-Linkage clustering, we invented in 3D unstructured point clouds An efficient segmentation algorithm, in which the smoothness of points is used as the eigenvalue, slices are created for each initial cluster, and then novel and robust slice fusion methods are used to obtain the final segmentation results. The proposed P-linkage clustering and 3D point cloud segmentation methods require only one input parameter. Experimental results synthesized data in different dimensions of 2d-4d fully demonstrate the efficiency and robustness of the P-Linkage clustering. A large number of experimental results in vehicle, airborne and station laser point clouds demonstrate the robustness of our proposed method. 

 https://github.com/xiaohulugo/PointCloudSegmentation 

 ![avatar]( 20200524215001663.JPG) 

 ● Paper Atlas ● English Abstract 

 In this paper, we first present a novel hierarchical clustering algorithm named Pairwise Linkage (P-Linkage), which can be used forclustering any dimensional data, and then effectively apply it on 3D unstructured point cloud segmentation. The P-Linkage clusteringalgorithm first calculates a feature value for each data point, for example, the density for 2D data points and the flatness for 3D pointclouds. Then for each data point a pairwise linkage is created between itself and its closest neighboring point with a greater featurevalue than its own. The initial clusters can further be discovered by searching along the linkages in a simple way. After that, a clustermerging procedure is applied to obtain the finally refined clustering result, which can be designed for specialized applications. Based onthe P-Linkage clustering, we develop an efficient segmentation algorithm for 3D unstructured point clouds, in which the flatness of theestimated surface of a 3D point is used as its feature value. For each initial cluster a slice is created, then a novel and robust slice mergingmethod is proposed to get the final segmentation result. The proposed P-Linkage clustering and 3D point cloud segmentation algorithmsrequire only one input parameter in advance. Experimental results on different dimensional synthetic data from 2D to 4D sufficientlydemonstrate the efficiency and robustness of the proposed P-Linkage clustering algorithm and a large amount of experimental resultson the Vehicle-Mounted, Aerial and Stationary Laser Scanner point clouds illustrate the robustness and efficiency of our proposed 3Dpoint cloud segmentation algorithm. 

 ![avatar]( 20200524215049534.JPG) 



--------------------------------------------------------------------------------

Point cloud PCL free knowledge planet, point cloud paper speed reading. 

 标题：Local Implicit Grid Representations for 3D Scenes 

 本人:Chiyu "Max"1.2 Avneesh South 

 Planet ID: particle 

 Welcome to join the free knowledge planet, get PDF papers, and welcome to forward Moments to share your happiness. 

 Abstracts of papers 

 Shape prior knowledge learned from point cloud data is often applied in 3D reconstruction from local or noisy point cloud data. However, since typical 3D autoencoders cannot handle their scale, complexity, or diversity, there is no such shape predictor in indoor scenes. In this paper, we introduce a Local Implicit Grid representation, a new 3D shape representation aimed at scalability and generality. Most 3D surfaces share geometric details at some scale. In this paper, an autoencoder is trained to learn how to embed 3D point cloud shapes of this size. Then, we use the decoder as a component in a shape optimization that resolves a set of latent codes on a regular grid of overlapping crops, such that the interpolation of the decoded local shapes matches partial or noise observations. And the value of this method in 3D surface reconstruction from sparse point observations is proved, and experiments show that this method is significantly better than other methods. 

 ![avatar]( 20200524221321834.JPG) 

 Main contributions 

 A Local Implicit Grid (LIG) representation is proposed, which is a regular grid composed of overlapping local regions, each of which is encoded by implicit eigenvectors. 

 The main contributions of this work are: 

 • Proposed local implicit mesh representation of geometric shapes, learning and leveraging geometric features on part point clouds, and related methods such as overlapping implicit mesh mechanisms and implicit mesh optimization methods to represent and reconstruct scenes with high reducibility. 

 • Compared with related methods for learning prior knowledge of the entire object, the local-based method significantly improves the versatility. 

 The method is applied to the challenging task of scene reconstruction from sparse point samples and shows significant improvement over state-of-the-art methods. 

 ![avatar]( 20200524221427849.JPG) 

 Paper Atlas   

 ![avatar]( 20200524221441270.JPG) 

 This widget representation can be generalized across object categories and is easily scalable to large scenes. By positioning the implicit function in the mesh, the entire scene can be reconstructed from point cloud data by optimizing the hidden mesh. 

 ● English abstract 

 ![avatar]( 20200524221511376.JPG) 

 Shape priors learned from data are commonly used to reconstruct 3D objects from partial or noisy data. Yet no such shape priors are available for indoor scenes, since typical 3D autoencoders cannot handle their scale, complexity, or diversity. In this paper, we introduce Local Implicit Grid Representations, a new 3D shape representation designed for scalability and generality. The motivating idea is that most 3D surfaces share geometric details at some scale – i.e., at a scale smaller than an entire object and larger than a small patch. We train an autoencoder to learn an embedding of local crops of 3D shapes at that size. Then, we use the decoder as a component in a shape optimization that solves for a set of latent codes on a regular grid of overlapping crops such that an interpolation of the decoded local shapes matches a partial or noisy observation. We demonstrate the value of this proposed approach for 3D surface reconstruction from sparse point observations, showing significantly better results than alternative approaches.  



--------------------------------------------------------------------------------

标题：3D Point Cloud Processing and Learning for Autonomous Driving 

 作者：Siheng Chen, Baoan Liu, Chen Feng, Carlos Vallespi-Gonzalez, Carl Wellington 

 Compiler: Point Cloud PCL 

 Source: arXiv 2020 

 This article is for academic sharing only. If there is any infringement, please contact to delete it. Welcome to join the free knowledge planet, get PDF papers, and welcome to forward Moments. If there is any error in the content, please comment and leave a message. Please do not reprint without permission! 

 The official account is dedicated to sharing articles and technologies related to point cloud processing, SLAM, 3D vision, and high-precision maps. Welcome to join us, communicate and progress together. If you are interested, please contact WeChat 920177957. 

 Write on the front 

 This article can be said to be a very complete introduction to the role of point clouds in autonomous driving of each module, from the macro sub-module of the point cloud in the role and application of autonomous driving, read the entire article, will not only have a more comprehensive understanding of autonomous driving technology, and understand the importance of point clouds in autonomous driving, the creation of high-precision maps introduced here and positioning perception module introduction is the core technology in the field of autonomous driving, such as in the introduction of the two positioning methods of the positioning module, when introducing the use of semantic geometric information and point cloud intensity information for positioning in different scenarios, it is completely suitable for the apollo autonomous driving solution, allowing readers to gain a lot. Here the blogger decided to translate it completely and share it with more interested friends. 

 There may be clerical errors or poor understanding in the process of translation and understanding. Everyone is welcome to leave a message. Due to the length of the article, the article will be divided into multiple articles and updated. The full English pdf is available on the free Knowledge Planet. 

 directory 

 1. Introduction 

 The significance, history and current situation of autonomous driving 

 1-B A complete autonomous driving system module 

 1-C 3D point cloud processing and learning 

 1-D Outline 

 2. Key elements of 3D point cloud processing and learning 

 2-A point cloud characteristics 

 2-B matrix representation 

 2-C representative tools 

 3. Creation of high-precision maps and processing of 3D point clouds 

 Overview of 3-A high-definition map creation module 

 Splicing of 3-B 3D Point Clouds 

 Extraction of semantic features from 3-C point clouds 

 3-D map creation challenges 

 4. Processing based on point cloud positioning 

 Overview of 4-A Positioning Module 

 4-B Map-based Localization 

 4-C point cloud positioning challenges 

 5. Point cloud perception 

 5-A Perception Module Overview 

 Detection of 5-B 3D Point Cloud Objects 

 5-C point cloud perception challenges 

 6. Summarize and expand the problem 

 6-A The relationship between academia and industry 

 6-B qualitative results 

 1. Introduction 

 1-A 

 The significance, history and current situation of autonomous driving 

 As one of the most exciting engineering projects in the world today, autonomous driving is an aspiration of many researchers and engineers. It is a goal that may fundamentally redefine the future of human society and the daily life of everyone. Once autonomous driving becomes mature, we will witness a huge transformation in public transportation, infrastructure and the face of cities. The world looks forward to using autonomous driving to reduce traffic accidents caused by driver error, save drivers' time and free up labor, save parking spaces, and especially relieve traffic pressure in urban areas [1]. 

 In order to continuously approach the goal of autonomous driving, it has taken decades of efforts. From the 1980s to the DARPA Challenge in 2004 and the DARPA Urban Challenge in 2007, autonomous driving research was mainly conducted in the United States and Europe, and progress was made in autonomous driving capabilities in various scenarios [2]. 

 In 2009, Google began a research project on autonomous cars, and later created Waymo to commercialize this achievement, building on its early technological success. In 2013-2014, the rise of deep neural networks revolutionized practical computer vision and machine learning. The emergence of these technologies led to the belief that many of the technical bottlenecks of autonomous driving could be fundamentally addressed. In 2015, Uber created the Uber Advanced Technology Group, with the goal of enabling autonomous driving to achieve scalable shared services. This goal has become a widely adopted deployment strategy in the industry. At present, there are many high-tech companies, automakers and startups working on autonomous driving technology, including Apple, Aptiv, ArgoAI, Aurora, Baidu, GM Cruise, Didi, Lyft, Pony.ai, Tesla, Zoox, major automotive companies, and many others [3]. These companies all have this ambitious goal to reach SAE level 4 autonomous driving in the near future. Although many groups in industry and academia have made significant progress, there is still a lot of work to be done. Achieving autonomous driving requires a joint effort of industry and academia. Recently, there has been a lot of discussion and assumptions about the progress and future of autonomous driving; however, few ideas have been made public by those pushing industrial-grade autonomous driving technology from the front lines. In this paper, we provide a unified perspective from both practitioners and researchers. 

 1-B 

 A complete autonomous driving system module 

 The autonomous driving system mainly includes sensors, map creation, positioning, perception, prediction, path planning, motion planning, and control modules [5]; see Figure 1. 

 ![avatar]( ffa7e0be5ca7342851fe317ce38ea03a.png) 

 Figure 1 Block diagram of a classic autonomous driving system. 

 The high-precision map is generated offline. At runtime, the online system is assigned a destination. The system then senses the environment, locates itself onto the map, perceives the world around it, and makes corresponding predictions about the movements of these objects. The motion planner uses this predictive information to plan the safe-form trajectory of the autonomous vehicle (AV) for a safe and effective route to be executed along with the vehicle controller. Note that two types of three-dimensional point clouds are used in this autonomous driving system: a point cloud map created by the map creation module and used by the positioning module, and a real-time lidar point cloud collected by the sensing module and used by the positioning and sensing module. 

 Sensing Module. In order to ensure the reliability of the system, autonomous driving often requires multiple types of sensors. Cameras, radio detection and ranging (radar), light detection and ranging (lidar), and ultrasonic sensors are the most commonly used of these sensors. Lidar is a representation of an accurate three-dimensional point cloud that can directly provide a scene. Although 3D reconstruction and depth estimation techniques based on 2D images have been significantly improved with the development of deep learning-based computer vision algorithms, the resulting estimates are still not always accurate or reliable. In addition to algorithmic limitations, fundamental bottlenecks include the exponential distance error growth inherent in depth estimation, poor performance in low light, and high computational cost of processing high-resolution images. On the other hand, LiDAR measures 3D information of a scene through direct physical sensors. Real-time LiDAR scans consist of a large number of 3D points, called 3D point clouds. Each 3D point records the distance from the LiDAR to the outer surface of the object and can be converted into precise 3D coordinates. These 3D point clouds are very valuable for autonomous vehicles to self-locate and detect surrounding objects in the 3D world. The vast majority of companies and researchers rely heavily on LiDAR to achieve more reliable autonomous vehicles [6]. This is why we believe that advanced 3D point cloud processing and learning technologies are essential in the field of autonomous driving. 

 Map creation module. The task of map creation is to create a high-precision (HD) point cloud map, which is an accurate heterogeneous map representation of the static three-dimensional environment and traffic rules. A high-precision map typically contains two map layers: a point cloud map, which represents the three-dimensional geometric information of the surrounding environment; and a semantic feature map related to traffic rules, containing road boundaries, lanes, traffic signs, traffic lights, etc. The two map layers are aligned in three-dimensional space and are able to provide detailed navigation information. As a map layer, a point cloud map is a dense three-dimensional point cloud, which is mainly used to provide positioning prior knowledge. Unlike ordinary maps designed for human travel, high-precision maps are designed for autonomous vehicles. The map creation module is crucial because high-resolution maps provide valuable prior environmental information; see Section 3 for details. 

 Positioning module. The task of positioning is to find the self-position of the autonomous vehicle relative to the reference position in the high-precision map. This module is crucial because the autonomous vehicle must position itself in order to use the correct lane and other important priority choices in the high-precision map. One of the core technologies is 3D point cloud registration; that is, to estimate the precise position of the autonomous vehicle by matching real-time LiDAR scans with offline high-precision maps; see Section 4 for details. 

 Perception. Perception is the task of perceiving the surrounding environment and extracting information related to navigation. Since the perception module is the vision system of an autonomous vehicle, it needs to detect, track and classify objects in a three-dimensional scene, so this module is crucial. It was once considered to be the technical bottleneck of autonomous driving. In recent years, with the development of large-scale training data and advanced machine learning algorithms, the overall performance of the perception module has been greatly improved. Some core technologies include two-dimensional object detection and three-dimensional object detection. Two-dimensional object detection has been relatively mature, while three-dimensional object detection is based on real-time lidar scanning and has become an increasingly popular research topic. See Section 5 for details. 

 Prediction. The task of prediction is to predict the potential future trajectory of each object in a 3D scene. This module is very important because autonomous vehicles need to know the likely future behavior of nearby objects in order to plan safe trajectories. 

 Path planning. Path selection is the task of designing a high-level path for an autonomous vehicle from its starting position to its destination. The output of this module provides a high-level guide to the motion planning module. 

 Motion planning. The task of motion planning is to design the trajectory of an autonomous vehicle based on its current state, surroundings, and destination. This module is very important because autonomous vehicles need to know how to react to their surroundings. 

 Control module. Control is the task of executing commands from the motion planning module. It is responsible for controlling the actuators of the steering wheel, throttle, and brakes. 

 1-C 

 3D point cloud processing and learning 

 As mentioned earlier, lidar provides indispensable 3D information for autonomous driving. We will now continue to introduce processing and learning techniques that convert raw measurements into useful information. 

 The role of point cloud autonomous driving. Two types of three-dimensional point clouds are commonly used in autonomous vehicles: real-time lidar scanning point clouds and point cloud maps, which are one layer in a high-precision map. Point cloud maps provide a priori environmental information: The localization module uses the point cloud map as a reference value for three-dimensional point cloud registration to determine the position of autonomous vehicles, and the perception module uses the point cloud map to help segment the foreground and background point clouds. On the other hand, the localization module uses real-time lidar to register the point cloud map, and the perception module uses real-time lidar point clouds to detect surrounding objects in a three-dimensional scene. Therefore, the processing and learning of three-dimensional point clouds is essential for building map generation, localization, and perception modules in an autonomous driving system. 

 Recent advances in academia. Algorithms for sensor acquisition of data and data feeding. In the development of radar, acoustic sensors, and communication systems, one-dimensional signal processing has undergone rapid development over the past century, having a revolutionary impact on digital communication systems. With the popularity of cameras and televisions, two-dimensional image processing has undergone rapid development over the past 30 years, leading to significant changes in the fields of photography, entertainment, and surveillance. With the development of industrial robotics, autonomous driving technology, and augmented reality, three-dimensional sensing technology has been rapidly developed. At the same time, processing and learning algorithms for three-dimensional point clouds have also begun to receive extensive attention in academia. The following discussion is divided into two parts: 3D point cloud processing (processing 3D point clouds from a signal processing perspective) and 3D point cloud learning (processing 3D point clouds from a machine learning perspective). 

 Three-dimensional point cloud processing. Three-dimensional point cloud processing is the process of analyzing and modifying a three-dimensional point cloud through various mathematical and computational algorithms to optimize its transmission, storage, and quality. Although processing algorithms can vary widely, many processing methods extend from one-dimensional signal processing and two-dimensional image processing. For example, 3D point cloud compression corresponds to image compression, the purpose of which is to reduce the storage or transmission cost of the 3D point cloud; 3D point cloud denoising corresponds to image denoising, the purpose of which is to remove noise from the 3D point cloud; 3D point cloud registration is the three-dimensional correspondence of image registration, the purpose of which is to align two or more three-dimensional point clouds of the same scene; 3D point cloud downsampling and upsampling correspond to image scaling, the purpose of which is to change the resolution (number of point clouds) in the three-dimensional point cloud. 

 3-D point cloud deep learning. 3-D point cloud deep learning is the process of interpreting and understanding 3-D point clouds. With the powerful tools of deep neural networks, computer vision researchers aim to extend deep learning from images and videos to 3-D point clouds. The two main learning problems are the recognition and segmentation of 3-D point clouds. Similar to the case of 2-D images, the purpose of 3-D point cloud recognition is to divide a given 3-D point cloud into a predefined category, while the purpose of 3-D point cloud segmentation is to divide a given 3-D point cloud into multiple parts. Due to the irregular format of 3-D point clouds, one of the biggest challenges in designing learning algorithms is to build efficient data structures to represent 3-D point clouds. Some algorithms convert 3D point clouds into regular 3D voxels, so 3D convolution can be used for analysis; however, they must be tradeoff between resolution and memory. To deal directly with raw point clouds, PointNet [7] uses a point-by-point multilayer perceptron (MLP) and a maximum pool to ensure arrangement invariance. Afterwards, a series of 3D deep learning methods are based on PointNet networks. 

 The relationship between academia and industry. The technical transformation from one-dimensional time series to two-dimensional images is very natural, because both types of data support regular spacing structures; however, the technical transformation from two-dimensional images to three-dimensional point clouds is not simple, because these points are irregularly scattered in three-dimensional space. Practitioners have also proposed many popular methods for processing three-dimensional point cloud data, which has brought more inspiration. Therefore, there is a lot of room for collaboration between researchers and practitioners in three-dimensional point cloud processing and learning, which can solve some fundamental tasks, thus speeding up the process of autonomous driving. 

 1-D 

 outline 

 The second section introduces the key elements of 3D point cloud processing and learning. Firstly, the conventional characteristics of 3D point clouds are explained, and then various methods for representing 3D point clouds are introduced. Then common methods for processing and learning 3D point clouds are introduced. 

 The latest methods and challenges related to 3D point cloud processing and learning in the Mapping Creation, Localization and Perception module of the autonomous driving system are presented in Sections 3, 4 and 5 respectively. These three modules are given special consideration as they rely heavily on 3D point clouds for reliable performance. In each module, the specific work content of this module will be discussed; why 3D point cloud processing and learning is very important to this module; and how 3D point cloud processing and learning can play a role in this module. 

 Section VI concludes with a discussion and indicates the way forward. Views from academia and industry are compared, followed by the latest qualitative results. 

 References 

 Swipe up to view 

 [1] A. Taeihagh and H. Si Min Lim, “Governing autonomous vehicles: emerging responses for safety, liability, privacy, cybersecurity, and industry risks,” Transport Reviews, vol. 39, no. 1, pp. 103–128, Jan. 2019.  

 [2] National Research Council, “Technology development for army unmanned ground vehicles,” 2002.  

 [3] C. Badue, R. Guidolini, R. Vivacqua Carneiro, P. Azevedo, V. Brito Cardoso, A. Forechi, L. Ferreira Reis Jesus, R. Ferreira Berriel, T. Meireles Paixo, F. Mutz, T. Oliveira-Santos, and A. Ferreira De Souza, “Self-driving cars: A survey,” arXiv:1901.04407 [cs.RO], Jan. 2019. [4] M. Bansal, A. Krizhevsky, and A. S. Ogale, “ChauffeurNet: Learning to drive by imitating the best and synthesizing the worst,” CoRR, vol. abs/1812.03079, 2018.  

 [5] C. Urmson, J. Anhalt, D. Bagnell, C. R. Baker, R. Bittner, M. N. Clark, J. M. Dolan, D. Duggins, T. Galatali, C. Geyer, M. Gittleman, S. Harbaugh, M. Hebert, T. M. Howard, S. Kolski, A. Kelly, M. Likhachev, M. McNaughton, N. Miller, K. M. Peterson, B. Pilnick, R. Rajkumar, P. E. Rybski, B. Salesky, Y-W. Seo, S. Singh, J. M. Snider, A. Stentz, W. Whittaker, Z. Wolkowicki, J. Ziglar, H. Bae, T. Brown, D. Demitrish, B. Litkouhi, J. Nickolaou, V. Sadekar, W. Zhang, J. Struble, M. Taylor, M. Darms, and D. Ferguson, “Autonomous driving in urban environments: Boss and the urban challenge,” in The DARPA Urban Challenge: Autonomous Vehicles in City Traffic, George Air Force Base, Victorville, California, USA, 2009, pp. 1–59.  

 [6] G. P. Meyer, A. Laddha, E. Kee, C. Vallespi-Gonzalez, and C. K. Wellington, “Lasernet: An efficient probabilistic 3d object detector for autonomous driving,” in Proc. IEEE Int. Conf. Comput. Vis. Pattern Recogn., 2019. 

  [7] C. Ruizhongtai Qi, H. Su, K. Mo, and L. J. Guibas, “Pointnet: Deep learning on point sets for 3d classification and segmentation,” in Proc. IEEE Int. Conf. Comput. Vis. Pattern Recogn., 2017, pp. 77–85. 

  [8] X. Chen, H. Ma, J. Wan, B. Li, and T. Xia, “Multi-view 3d object detection network for autonomous driving,” in Proc. IEEE Int. Conf. Comput. Vis. Pattern Recogn., 2017, pp. 6526–6534. 

 [9] M. A. Fischler and R. C. Bolles, “Random sample consensus: a paradigm for model fitting with applications to image analysis and automated cartography,” Communications of the ACM, vol. 24, no. 6, pp. 381–395, 1981. 

  [10] X-F. Hana, J. S. Jin, J. Xie, M-J. Wang, and W. Jiang, “A comprehensive review of 3d point cloud descriptors,” arXiv preprint arXiv:1802.02297, 2018.  

 [11] J. Peng and C.-C. Jay Kuo, “Geometry-guided progressive lossless 3D mesh coding with octree (OT) decomposition,” ACM Trans. Graph. Proceedings of ACM SIGGRAPH, vol. 24, no. 3, pp. 609–616, Jul. 2005.  

 [12] A. Ortega, P. Frossard, J. Kovacevic, J. M. F. Moura, and P. Vandergheynst, “Graph signal processing: Overview, challenges, and applications,” Proceedings of the IEEE, vol. 106, no. 5, pp. 808–828, 2018. 

  [13] S. Chen, D. Tian, C. Feng, A. Vetro, and J. Kovacevi ˇ c, “Fast resampling ´ of three-dimensional point clouds via graphs,” IEEE Trans. Signal Processing, vol. 66, no. 3, pp. 666–681, 2018.  

 [14] Y. Wang, Y. Sun, Z. Liu, S. E. Sarma, M. M. Bronstein, and J. M. Solomon, “Dynamic graph CNN for learning on point clouds,” ACM Transactions on Graphics (TOG), vol. 38, no. 5, November 2019.  

 [15] S. Chen, S. Niu, T. Lan, and B. Liu, “Large-scale 3d point cloud representations via graph inception networks with applications to autonomous driving,” in Proc. IEEE Int. Conf. Image Process., Taipei, Taiwan, Sept. 2019.  

 [16] G. Li, M. Muller, A. K. Thabet, and B. Ghanem, “DeepGCNs: Can ¨ GCNs go as deep as CNNs?,” in ICCV, Seoul, South Korea, Oct. 2019. 

  [17] G. Grisetti, R. Kummerle, C. Stachniss, and W. Burgard, “A tutorial ¨ on graph-based SLAM,” IEEE Intell. Transport. Syst. Mag., vol. 2, no. 4, pp. 31–43, 2010. 

  [18] D. Droeschel and S. Behnke, “Efficient continuous-time SLAM for 3d lidar-based online mapping,” in 2018 IEEE International Conference on Robotics and Automation, ICRA, 2018, Brisbane, Australia, May 21-25, 2018, 2018, pp. 1–9. 

 [19] P. J. Besl and N. D. McKay, “A method for registration of 3D shapes,” IEEE Trans. Pattern Anal. Mach. Intell., vol. 14, no. 2, pp. 239–256, 1992.  

 [20] A. Y. Hata and D. F. Wolf, “Road marking detection using LIDAR reflective intensity data and its application to vehicle localization,” in 17th International IEEE Conference on Intelligent Transportation Systems, ITSC 2014, Qingdao, China, October 8-11, 2014, 2014, pp. 584–589. 

  [21] S. Shi, X. Wang, and H. Li, “PointRCNN: 3d object proposal generation and detection from point cloud,” in Proc. IEEE Int. Conf. Comput. Vis. Pattern Recogn., Long Beach, CA, June 2019.  

 [22] B. Li, “3d fully convolutional network for vehicle detection in point cloud,” in 2017 IEEE/RSJ International Conference on Intelligent Robots and Systems, IROS 2017, Vancouver, BC, Canada, September 24-28, 2017, 2017, pp. 1513–1518. 

  [23] B. Yang, W. Luo, and R. Urtasun, “PIXOR: real-time 3d object detection from point clouds,” in Proc. IEEE Int. Conf. Comput. Vis. Pattern Recogn., 2018, pp. 7652–7660.  

 [24] J. Zhou, X. Lu, X. Tan, Z. Shao, S. Ding, and L. Ma, “Fvnet: 3d front-view proposal generation for real-time object detection from point clouds,” CoRR, vol. abs/1903.10750, 2019.  

 [25] B. Li, T. Zhang, and T. Xia, “Vehicle detection from 3d lidar using fully convolutional network,” in Robotics: Science and Systems XII, University of Michigan, Ann Arbor, Michigan, USA, June 18 - June 22, 2016, 2016. 

  [26] Y. Zhou and O. Tuzel, “Voxelnet: End-to-end learning for point cloud based 3d object detection,” in Proc. IEEE Int. Conf. Comput. Vis. Pattern Recogn., Salt Lake City, UT, USA, June 2018, pp. 4490–4499.  

 [27] S. Shi, Z. Wang, X. Wang, and H. Li, “Part-a2 net: 3d part-aware and aggregation neural network for object detection from point cloud,” CoRR, vol. abs/1907.03670, 2019.  

 [28] Y. Yan, Y. Mao, and B. Li, “Second: Sparsely embedded convolutional detection,” Sensors, vol. 18, no. 10, 2019. 

  [29] A. H. Lang, S. Vora, H. Caesar, L. Zhou, J. Yang, and O. Beijbom, “Pointpillars: Fast encoders for object detection from point clouds,” CoRR, vol. abs/1812.05784, 2018.  

 [30] T-Y. Lin, P. Dollar, R. B. Girshick, K. He, B. Hariharan, and S. J. ´ Belongie, “Feature pyramid networks for object detection,” in Proc. IEEE Int. Conf. Comput. Vis. Pattern Recogn., 2017, pp. 936–944.  

 [31] F. Yu, D. Wang, E. Shelhamer, and T. Darrell, “Deep layer aggregation,” in Proc. IEEE Int. Conf. Comput. Vis. Pattern Recogn., 2018, pp. 2403–2412. 

  [32] W. Liu, D. Anguelov, D. Erhan, C. Szegedy, S. E. Reed, C-Y. Fu, and A. C. Berg, “SSD: single shot multibox detector,” in Computer Vision - ECCV 2016 - 14th European Conference, Amsterdam, The Netherlands, October 11-14, 2016, Proceedings, Part I, 2016, pp. 21–37. 

  [33] T-Y. Lin, P. Goyal, R. B. Girshick, K. He, and P. Dollar, “Focal ´ loss for dense object detection,” in IEEE International Conference on Computer Vision, ICCV 2017, Venice, Italy, October 22-29, 2017, 2017, pp. 2999–3007.  

 [34] J. Ku, M. Mozifian, J. Lee, A. Harakeh, and S. L. Waslander, “Joint 3d proposal generation and object detection from view aggregation,” in 2018 IEEE/RSJ International Conference on Intelligent Robots and Systems, IROS 2018, Madrid, Spain, October 1-5, 2018, 2018, pp. 1–8.  

 [35] C. Ruizhongtai Qi, W. Liu, C. Wu, H. Su, and L. J. Guibas, “Frustum pointnets for 3d object detection from RGB-D data,” in Proc. IEEE Int. Conf. Comput. Vis. Pattern Recogn., 2018, pp. 918–927.  

 [36] D. Xu, D. Anguelov, and A. Jain, “PointFusion: Deep sensor fusion for 3d bounding box estimation,” in Proc. IEEE Int. Conf. Comput. Vis. Pattern Recogn. 2018, pp. 244–253, IEEE Computer Society.  

 [37] M. Liang, B. Yang, S. Wang, and R. Urtasun, “Deep continuous fusion for multi-sensor 3d object detection,” in Computer Vision - ECCV 2018 - 15th European Conference, Munich, Germany, September 8-14, 2018, Proceedings, Part XVI, 2018, pp. 663–678. 

  [38] M. Liang, B. Yang, Y. Chen, R. Hu, and R. Urtasun, “Multi-task multi-sensor fusion for 3d object detection,” in Proc. IEEE Int. Conf. Comput. Vis. Pattern Recogn., 2019, pp. 7345–7353. 

  [39] G. P. Meyer, J. Charland, D. Hegde, A. Laddha, and C. VallespiGonzalez, “Sensor fusion for joint 3d object detection and semantic segmentation,” CoRR, vol. abs/1904.11466, 2019.  

 [40] A. Geiger, P. Lenz, and R. Urtasun, “Are we ready for autonomous driving? the KITTI vision benchmark suite,” in Proc. IEEE Int. Conf. Comput. Vis. Pattern Recogn., Providence, RI, June 2012, pp. 3354– 3361.  

 [41] K-L. Low, “Linear least-squares optimization for point-toplane icp surface registration,” Tech. Rep., University of North Carolina at Chapel Hill, 2004.  

 [42] J. Yang, H. Li, D. Campbell, and Y. Jia, “Go-icp: A globally optimal solution to 3d ICP point-set registration,” IEEE Trans. Pattern Anal. Mach. Intell., vol. 38, no. 11, pp. 2241–2254, 2016.  

 [43] A. Geiger, P. Lenz, C. Stiller, and R. Urtasun, “Vision meets robotics: The kitti dataset,” International Journal of Robotics Research (IJRR), 2013.  

 [44] Z. Wu, S. Song, A. Khosla, F. Yu, L. Zhang, X. Tang, and J. Xiao, “3d shapenets: A deep representation for volumetric shapes,” in Proc. IEEE Int. Conf. Comput. Vis. Pattern Recogn., 2015, pp. 1912–1920. 

  [45] F. Pomerleau, F. Colas, and R. Siegwart, “A review of point cloud registration algorithms for mobile robotics,” Foundations and Trends in Robotics, vol. 4, no. 1, pp. 1–104, 2015.  

 [46] H. Fathi, F. Dai, and M. I. A. Lourakis, “Automated as-built 3d reconstruction of civil infrastructure using computer vision: Achievements, opportunities, and challenges,” Advanced Engineering Informatics, vol. 29, no. 2, pp. 149–161, 2015.  

 [47] B. Reitinger, C. Zach, and D. Schmalstieg, “Augmented reality scouting for interactive 3d reconstruction,” in IEEE Virtual Reality Conference, VR 2007, 10-14 March 2007, Charlotte, NC, USA, Proceedings, 2007, pp. 219–222. 

 To be continued... 

 resource 

 3D point cloud paper and related application sharing 

 [Point cloud paper speed reading] Odometer based on lidar and positioning method in 3D point cloud map 

 3D object detection: MV3D-Net 

 Overview of 3D Point Cloud Segmentation (Part 1) 

 3D-MiniNet: Learning 2D Representations from Point Clouds for Fast and Efficient 3D LIDAR Semantic Segmentation (2020) 

 Use QT to add VTK plug-in under win to realize point cloud visualization GUI 

 JSNet: Joint Instances and Semantic Segmentation for 3D Point Clouds 

 A Survey of Semantic Segmentation of 3D Point Cloud in Large Scene 

 The outofcore module in PCL---Display of large-scale point clouds based on out-of-core octree 

 Target Segmentation Based on Local Convex 

 Point cloud labeling based on 3D convolutional neural networks 

 SuperVoxel of Point Cloud 

 Large-scale point cloud segmentation based on hyperdot graph 

 More articles can be viewed: A summary of historical articles on point cloud learning 

 SLAM and AR related sharing 

 [Open source solution sharing] ORB-SLAM3 is open source! 

 AVP-SLAM: Semantic SLAM in Automatic Parking Systems 

 [Point Cloud Paper Speed Reading] StructSLAM: Structured Line Feature SLAM 

 SLAM and AR Overview 

 Commonly used 3D depth cameras 

 Overview and Evaluation of Monocular Vision Inertial Navigation SLAM Algorithm for AR Devices 

 SLAM Review (4) Laser and Vision Fusion SLAM 

 Kimera's Semantic SLAM System for Real-Time Reconstruction 

 Overview of SLAM (3) - Vision and inertial navigation, vision and deep learning SLAM 

 Extensible SLAM Framework - OpenVSLAM 

 Gao Xiang: Challenges in unstructured road laser SLAM 

 SLAM Overview of Lidar SLAM 

 SLAM Method Based on Fisheye Camera 

 Online sharing and recording summary in the past 

 3D Model Retrieval Technology of the First Bilibili Recording 

 Application of deep learning in 3D scenes recorded and broadcast by Bilibili 

 The third Bilibili recording of CMake advanced learning 

 Point Cloud Object and Six-Degree-of-Freedom Attitude Estimation Recorded by Bilibili 

 The fifth Bilibili recording of point cloud deep learning semantic segmentation expansion 

 Pointnetlk Interpretation of the 6th Bilibili Recording 

 [线上分享录播]点云配准概述及其在激光SLAM中的应用 

 [线上分享录播]cloudcompare插件开发 

 [线上分享录播]基于点云数据的 Mesh重建与处理 

 [线上分享录播]机器人力反馈遥操作技术及机器人视觉分享 

 [线上分享录播]地面点云配准与机载点云航带平差 

 If you are interested in this article, please send "Knowledge Planet" in the background to get the QR code. Be sure to join the free Knowledge Planet according to the remarks of "Name + School/Company + Research Direction", download the pdf document for free, and communicate with more friends who love to share! 

 If the above content is wrong, please leave a comment, and welcome to correct and communicate. If there is any infringement, please contact to delete it. 

 ![avatar]( 35373ef3189a78155d2e95ccecc7a390.png) 

 Scan QR code 

                    Follow us 

 Let's share and learn together! Looking forward to friends who have ideas and are willing to share joining the free planet to inject fresh vitality of love and sharing. The topics shared include but are not limited to 3D vision, point clouds, high-precision maps, autonomous driving, and robotics and other related fields. 

 Sharing and cooperation method: WeChat "920177957" (note required) Contact email: dianyunpcl@163.com, enterprises are welcome to contact the official account for cooperation. 



--------------------------------------------------------------------------------

标题：3D Point Cloud Processing and Learning for Autonomous Driving 

 作者：Siheng Chen, Baoan Liu, Chen Feng, Carlos Vallespi-Gonzalez, Carl Wellington 

 Compiler: Point Cloud PCL 

 Source: arXiv 2020 

 This article is for academic sharing only. Due to malicious reports, we cannot apply for originality for the time being. If my translated article is infringing, please contact to delete it. Welcome to join the free knowledge planet, get PDF papers, and welcome to forward Moments. If there is any error in the content, please comment and leave a message. Please do not reprint without permission! 

 The official account is dedicated to sharing articles and technologies related to point cloud processing, SLAM, 3D vision, and high-precision maps. Welcome to join us, communicate and progress together. If you are interested, please contact WeChat 920177957. 

 Write on the front 

 This article can be said to be a very complete introduction to the role of point clouds in autonomous driving of each module, from the macro sub-module of the point cloud in the role and application of autonomous driving, read the entire article, will not only have a more comprehensive understanding of autonomous driving technology, and understand the importance of point clouds in autonomous driving, the creation of high-precision maps introduced here and positioning perception module introduction is the core technology in the field of autonomous driving, such as in the introduction of the two positioning methods of the positioning module, when introducing the use of semantic geometric information and point cloud intensity information for positioning in different scenarios, it is completely suitable for the apollo autonomous driving solution, allowing readers to gain a lot. Here the blogger decided to translate it completely and share it with more interested friends. 

 There may be clerical errors or poor understanding in the process of translation and understanding. Everyone is welcome to leave a message. Due to the length of the article, the article will be divided into multiple articles and updated. The full English pdf is available on the free Knowledge Planet. 

 directory 

 1. Introduction 

 The significance, history and current situation of autonomous driving 

 1-B A complete autonomous driving system module 

 1-C 3D point cloud processing and learning 

 1-D Outline 

 2. Key elements of 3D point cloud processing and learning 

 2-A point cloud characteristics 

 2-B matrix representation 

 2-C representative tools 

 3. Creation of high-precision maps and processing of 3D point clouds 

 Overview of 3-A high-definition map creation module 

 Splicing of 3-B 3D Point Clouds 

 Extraction of semantic features from 3-C point clouds 

 3-D map creation challenges 

 4. Processing based on point cloud positioning 

 Overview of 4-A Positioning Module 

 4-B Map-based Localization 

 4-C point cloud positioning challenges 

 5. Point cloud perception 

 5-A Perception Module Overview 

 Detection of 5-B 3D Point Cloud Objects 

 5-C point cloud perception challenges 

 6. Summarize and expand the problem 

 6-A The relationship between academia and industry 

 6-B qualitative results 

 2. Key elements of 3D point cloud processing and learning 

 In this section, basic tools for 3D point cloud processing and learning will be introduced. Start with the key characteristics of 3D point clouds. Evaluate some of the methods for representing 3D point clouds. Finally, a range of popular tools for processing 3D point clouds are reviewed. These tools have received a great deal of attention in the academic community. Even though some of them may not be directly applied to autonomous driving systems, they are still worth mentioning as they can inspire new technologies that may be useful for autonomous driving. 

 2-A 

 point cloud characteristics 

 As discussed in Section 1-C, two typical three-dimensional point clouds in autonomous driving are considered: real-time lidar point clouds and point cloud high-resolution maps. 

 Real-time LiDAR point cloud. For each three-dimensional point in a real-time LiDAR point cloud, its associated laser beam and captured timestamp can be tracked. A real-time LiDAR point cloud can be naturally organized on a two-dimensional image whose x-axis is timestamp and y-axis is laser ID. Therefore, we treat each individual real-time LiDAR point cloud as an organized three-dimensional point cloud. For example, the Velodyne HDL-64E has 64 independent lasers, each one firing thousands of times per second to capture a 360-degree field of view. Therefore, we obtain a set of three-dimensional points associated with 64 elevation angles and thousands of azimuth angles. Each acquired three-dimensional point is associated with a distance measurement, an intensity value, and a high-precision GPS timestamp. Note that for the global shutter image, the pixel values are collected simultaneously by a charge-coupled device (CCD); however, for real-time LiDAR scans, the 3D points are collected in various timestamps. For the same laser beam, three-dimensional point cloud information is collected after successive emission; for different lasers, the emitted laser beams are also not synchronized; therefore, the collected three-dimensional points are not perfectly aligned on a two-dimensional regular grid. Since the arrangement of the 64 lasers follows a regular angular spacing, the point density of real-time LiDAR varies across the entire range; that is, much more three-dimensional points are collected from nearby objects than from distant objects. In addition, real-time LiDAR point clouds are subject to occlusion; that is, 3D point clouds can only be acquired from the surface of an object facing the LiDAR. In summary, some of the key characteristics of real-time LiDAR point clouds include: 

 ● Pseudo-3D points. Real-time lidar scans only reflect a specific viewpoint, so we consider its dimensionality to be pseudo-3D. 

 ● Occlusion. Each individual real-time lidar can only record the 3D environment from one viewpoint. Objects in front will block other objects behind; 

 ● Sparse point cloud. Compared with two-dimensional images, real-time lidar is usually a sparse representation of the surface of an object, especially for distant objects. It cannot provide detailed three-dimensional shape information of the object object. 

 Point cloud high-precision map. To create a point cloud map, it is necessary to stitch together point clouds obtained from cross-time scans taken by real-time LiDAR from multiple autonomous vehicles. Since there is no direct way to organize a point cloud map, we treat it as an unorganized three-dimensional point cloud. For example, for a 200 × 200 square meter high-precision map, it is necessary to acquire LiDAR point cloud data around the area and conduct 5-10 trials, resulting in more than 10 million 3D points. Since LiDAR can collect point clouds from different views, the stitched high-precision map becomes denser and shows detailed three-dimensional shape information. To summarize, some of the key properties of a point cloud map include: 

 ● Full 3D points. Point cloud maps stitch together multiple LiDAR point clouds from different views, similar to 3D data collected by scanning objects on a turntable. Point cloud maps capture more information about the surface of objects, providing a denser and more detailed 3D representation; 

 ● Irregular. The 3D points in the point cloud map are irregularly scattered in 3D space. They come from multiple LiDAR scans, and there is no laser ID association, resulting in disorganized 3D point clouds; 

 ● No occlusion. A point cloud map is a collection of three-dimensional points collected from multiple viewpoints. It depicts a static three-dimensional scene with less occlusion. 

 Dense point clouds. Point cloud maps provide dense point clouds that contain detailed 3D shape information, such as high-resolution shapes and surface normals. 

 ● Semantic point cloud. As another layer of the HD map, the semantic feature map related to traffic rules contains semantic labels for 3D scenes, including pavements, buildings, and trees. Since the semantic feature map and point cloud map related to traffic rules are aligned in 3D space, the semantic information of each 3D point cloud can be tracked. For example, a 3D point cloud labeled as a tree in a point cloud map will help improve perception, as lidar points on leaves are often noisy and difficult to identify 

 2-B 

 matrix notation 

 Representations have been at the heart of most signal processing and machine learning techniques. A good representation lays the foundation for revealing hidden patterns and structures within the data and benefits subsequent tasks. A general representation of a three-dimensional point cloud is achieved through a set that ignores any order of three-dimensional points. Let S = (pi; ai) be a set of n three-dimensional points whose pi = [Xi; Yi; Zi] ¾ R3 represents the three-dimensional coordinates of the i-th point and ai represents other properties of the i-th point. Real-time lidar scan points typically include intensity 😉 R, and point cloud maps typically include surface normals ni 😉 R3; therefore, ai = [ri; ni] ¾ R4. For efficient storage and scientific computation, matrix (or tensor) representations are very interesting. Let f be a mapping from a set of 3D points S to a matrix (or tensor) X with a shape to be determined. Therefore, the matrix of a three-dimensional point cloud is represented as X = f (S) Next we will discuss several typical methods for implementing the mapping f (▽). 

 Primitive point cloud. The most straightforward matrix representation of a 3D point cloud is to list each 3D point in the collection as a row in the matrix. 

 ![avatar]( 20210306150236610.gif) 

 The advantages of a representation based on the original point cloud are: 

 1) Simple and versatile. 

 2) It retains all the information in the original 3D point set; but the disadvantage is that it is not conducive to exploring any geometric characteristics of 3D points. This representation method is usually used in the map and positioning module of autonomous driving systems and requires high accuracy. 

 Three-dimensional point cloud voxelization. For the success of two-dimensional image processing and computer vision, three-dimensional space can be discretized into voxels, and a series of voxels can be used to represent three-dimensional point clouds. A simple discretization method is to divide three-dimensional space into equidistant non-overlapping voxels from each of the three dimensions; 

 ![avatar]( 20210306150236611.gif) 

 3D voxelization point cloud representation 

 Draw a three-dimensional space in the range H, W, D along the X, Y, and Z axes, respectively. The size of each voxel is h, w, d, respectively. The (i, j, k) voxel represents the three-dimensional voxel space. The voxel expression is as follows: 

 ![avatar]( 20210306150236608.gif) 

 The advantages of voxelization-based representation are: 

 (I) The generated voxels are associated with a natural hierarchy, with all voxels having a uniform spatial size. 

 (Ii) Data can be analyzed using off-the-shelf tools such as 3D convolution. 

 However, the disadvantages are: 

 (I) It does not consider the specific properties of ordered three-dimensional point clouds. 

 (Ii) usually results in a very sparse representation in which most voxels are empty. 

 (Iii) It involves the trade-off between resolution and memory. This representation method can be used for autonomous driving perception modules and storage of 3D point clouds. 

 Depth map. As described in Section 2-A, a real-time LiDAR scanning point cloud is essentially a series of distance measurements taken from a single location with an angular field of view; as depicted in the figure. 

 ![avatar]( 20210306150236609.gif) 

 Representation Method of Converting Lidar into Depth Two-Dimensional Map 

 We can approximately organize three-dimensional points in real-time lidar into two-dimensional distance image images. Each pixel in the depth image corresponds to a point in three-dimensional space. The pixel value is the range from the lidar to the nearest three-dimensional point in the truncated cone. Specifically, we divide the three-dimensional space along the azimuth angle [0; 2π) and the pitch angle [theta] (− π/2; π/2] with the resolution of the azimuth angle α and the pitch angle theta. The (i, j) first pixel corresponds to the truncated cone space Vi and uses a two-dimensional matrix to represent the three-dimensional point cloud. Its (i, j) element is 

 ![avatar]( 20210306150236611.gif) 

 Take into account the minimum distance value in each truncated cone space. When none of the points fall into the section space, we set the default to − 1. Note that depending on the lidar settings, depth image-based representations can also use non-uniform pitch angles. The advantages of distance image-based representations are: 

 (I) Capable of naturally simulating the way lidar captures three-dimensional points, reflecting two-dimensional surfaces in three-dimensional space; 

 (Ii) Most relevant cross-sectional spaces have one or more three-dimensional points, resulting in a compact distance-view image; however, the disadvantage is that it is difficult to model unorganized point clouds, such as those in HD maps, which can be used for perception modules. 

 Aerial view. A bird's-eye view (BEV) -based representation is a special case of three-dimensional voxelization by ignoring height. It projects 3D voxels onto a BEV image; see image. 

 ![avatar]( 20210306150236615.gif) 

 Representation method of aerial view 

 Draw a three-dimensional space in the range H and W along the X and Y axes, respectively. The size of each pixel is h, w, respectively. The (i, j) th pixel in the BEV image represents the space Vi; the three-dimensional point cloud is represented by a two-dimensional matrix. Let X (BEV) 😉 R, whose (i, j) elements are 

 ![avatar]( 20210306150236620.gif) 

 The matrix X (BEV) records occupancy in two-dimensional space. Note that the BEV-based representation has some variables. For example, instead of using binary values, MV3D [8] uses some statistical values in each cylinder space to construct X (BEV). 

 The advantages of BEV-based notation are: 

 (I) It is easy to apply technologies based on 2D vision. 

 (Ii) It is easy to integrate with information from HD maps. For example, driveable areas and intersection locations encoded in high-resolution maps can be projected onto the same two-dimensional space and fused with lidar information; 

 (Iii) Easy to use in subsequent modules such as prediction and motion planning. 

 (Iv) Object objects are always the same size regardless of distance (in contrast to depth map-based representations), which is a strong prior knowledge that makes learning problems easier; however, the drawback of this voxel two-dimensional BEV representation is that: 

 (I) It involves a serious trade-off between resolution and memory, leading to over-quantification problems in obtaining details of small objects. 

 (Ii) It does not consider the specific properties of ordered three-dimensional point clouds and cannot explain occlusion phenomena. 

 (Iii) It causes sparsity problems because most pixels are empty. This representation can be used for perception modules in autonomous driving. 

 2-C 

 Representative tool 

 3D point clouds have been extensively studied in areas such as robotics, computer graphics, computer vision, and signal processing. Here are some representative tools for processing and learning 3D point clouds. Due to the practical application of deep neural networks methods in autonomous driving, we mainly emphasize methods based on deep neural networks. 

 Non-deep learning methods. Before the advent of deep learning, there were already many traditional methods to handle 3D point clouds for various tasks. However, unlike deep neural networks, these traditional methods are difficult to describe with a single methodological framework. This is because traditional tools are specifically designed to meet the needs of each task and are developed for actual point cloud characteristics. For example, in 3D point cloud segmentation and 3D shape detection, traditional techniques are area growth based on simple geometric heuristics, or graph-based optimization, or robust estimation methods such as RANSAC [9]. 3D keypoint matching, as another important task, is closely related to 3D point cloud registration and 3D point cloud recognition. In order to solve this problem, many statistical-based methods have been developed in the traditional way to describe the geometry around three-dimensional keypoints or objects; see [10] for a more comprehensive discussion. 

 Convolutional neural networks. The motivation for using convolutional neural networks is to take advantage of off-the-shelf deep learning tools to process 3-D point clouds. Convolutional neural networks (CNNs), as a regularized form of multi-layer perceptrons, employ a series of convolutional layers that are commonly used for the analysis of images and videos. The convolutional layer operates on the input data with a set of learnable filters to produce an output representing an activation map of the filter. The advantage of convolutional layers is weight sharing, i.e. applying the same filter coefficients (weights) to any position in the 2-D image, which not only saves a lot of learnable weights, but also guarantees translation invariance, helping to avoid overfitting to limited training data. CNNs, as a general and mature learning framework, is widely used in various computer vision tasks, including classification, detection, segmentation, etc., and has achieved the most advanced performance in most tasks. 

  Based on the success of CNN methods in image and video, CNNs have also been applied to 3D point cloud data. A variety of representations have been used, including 3D voxelization-based representations, depth map-based representations, and BEV-based representations. One advantage of using CNNs to handle 3D point clouds is that convolutional algorithms can better organize local spatial relationships. In PointNet, each 3D point cloud is processed individually; in CNNs, adjacent voxels or pixels are considered jointly, providing richer contextual information. The basic operators of CNNs are generally applicable to 3D convolution for 3D voxelization-based representations and 2D convolution for depth map-based representations and BEV-based representations. 

  Even with the discretization properties of point clouds, many of the techniques and architectures developed for 2D images can be easily extended to handle 3D point clouds. Although discretization leads to inevitable loss of information, CNNs generally have reliable performance and are widely used in many tasks. As mentioned earlier, a key problem with discretized 3D point clouds is that the resulting 3D volume or 2D images are sparse. Processing empty voxels wastes a lot of computation. In summary, CNNs deal with discretized 3D point clouds. This approach inevitably modifies precise 3D position information, but still provides good empirical performance due to the prior nature of spatial relationships and the maturity of CNNs. Therefore, it is widely used in industry. 

 A PointNet-based approach. The purpose of using a PointNet-based approach is to process raw 3-D point clouds directly through deep neural networks without any discretization of the point clouds. PointNet [7] is the pioneering work to achieve this goal. Raw 3-D point clouds are essentially disordered collections, and PointNet is designed to respect this property and produce the same output regardless of the order of the input data. The key technical contribution of PointNet is to use a shared set of point-by-point multilayer perceptrons (MLPs) and then use a global pool to extract geometric features while ensuring this arrangement invariance of the raw 3D data. Although the architecture is simple, it has become a standard module for many 3D point cloud learning algorithms, and has achieved amazing performance in 3D point cloud recognition and segmentation. PointNet is a representation X (raw) based on the original point cloud. Let H ¾ R N × D be a local feature matrix, where the i-th line Hi represents the feature of the i-th point, and H ¾ R D is the global feature vector. A basic computational representation of PointNet 

 ![avatar]( c1d098dde64d751174f9a53afc58fe0c.png) 

 Where X (raw) is the feature of the i-th 3D point, MLP (L) represents L-layer MLP, which maps each 3D point to a feature space, and maxpool (😂) performs downsampling by computing the maximum (point cloud dimension) along the column; see Figure 3 (a). Note that each 3D point here passes the same MLP separately. 

 ![avatar]( 1d04fc1ea51881838080f3d5a56d27bc.png) 

   PointNet icon 

 Intuitively, MLP proposes D representative geometric shapes and tests whether these figures appear around each 3D point. The maximum pool records the best response values on all 3D points for each pattern. Essentially, the global eigenvector h summarizes the matching values of the D representative geometric patterns in the 3D point cloud, which can be used to identify the 3D point cloud. At the same time, since each 3D point passes through the same mlp separately, and max-pooling removes the dimension of the points, the entire computational block is permutation-invariant, that is, the ordering of the 3D points does not affect the output of the block. 

 The PointNet of 3D point cloud deep learning is somewhat similar to the Principal Component Analysis (PCA) of data analytics in that it is simple, versatile, and effective. Just like the Principal Component Analysis, PointNet extracts global features in the 3D point cloud. To sum up, the PointNet-based method handles the 3D point cloud in a raw point-based representation and guarantees its arrangement invariance. The effectiveness of the method has been validated in different extended domains and learning tasks of deep learning. 

 Methods based on graph theory. The motivation for using methods based on graph theory is to take advantage of the spatial relationships between three-dimensional points to accelerate end-to-end learning for deep neural networks. One advantage of CNNs is that the convolutional operators take into account local spatial relationships; however, these relationships are between adjacent voxels (or adjacent pixels) rather than between the original 3D points. To capture the local relationships between three-dimensional points, a graph structure can be introduced where each node is a three-dimensional point and each edge reflects the relationship between each pair of three-dimensional points. This graph structure is a representation of the degree of dispersion of the original object surface. The matrix representation of the N-node graph is the proximity matrix A ¾ R, and its (i, j) elements reflect the pairwise relationship between the i-th 3D point and the j-th 3D point, as shown in the figure. 

 ![avatar]( 20210306150236623.gif) 

    Diagram of a graph-based method 

 Methods based on graph theory usually consider primitive representations based on point clouds. Each column vector in point cloud X is then the data supported on Figure A above; called a graph signal. Methods for constructing graphs are K-nearest neighbor graphs, an-graphs, and learnable graphs. K-nearest neighbor graphs are graphs in which two nodes are connected by edges when their Euclidean distance is in the Kth smallest Euclidean distance from one 3D point to all other 3D points. Nearest neighbor graphs are graphs in which two nodes are connected by an edge when their Euclidean distance is less than a given threshold. K-nearest neighbor graphs and -graphs can be efficiently implemented by using efficient data structures, such as octree [11]. A learnable graph is a graph structure trainable by adjacency matrices in an end-to-end learning architecture. 

 In summary, graph theory-based methods are used to construct graph structures to capture the distribution of three-dimensional point clouds and to exploit local spatial relationships. This approach deals with three-dimensional point clouds in raw point-based representations, ensuring permutation invariance. This approach is not yet mature: although utilizing a graph can improve overall performance, graph construction is more art than science and requires additional computational costs; moreover, the deep structure of graph-based neural networks still needs more exploration [16]. 

 References 

 Swipe up to view 

 [1] A. Taeihagh and H. Si Min Lim, “Governing autonomous vehicles: emerging responses for safety, liability, privacy, cybersecurity, and industry risks,” Transport Reviews, vol. 39, no. 1, pp. 103–128, Jan. 2019.  

 [2] National Research Council, “Technology development for army unmanned ground vehicles,” 2002.  

 [3] C. Badue, R. Guidolini, R. Vivacqua Carneiro, P. Azevedo, V. Brito Cardoso, A. Forechi, L. Ferreira Reis Jesus, R. Ferreira Berriel, T. Meireles Paixo, F. Mutz, T. Oliveira-Santos, and A. Ferreira De Souza, “Self-driving cars: A survey,” arXiv:1901.04407 [cs.RO], Jan. 2019. [4] M. Bansal, A. Krizhevsky, and A. S. Ogale, “ChauffeurNet: Learning to drive by imitating the best and synthesizing the worst,” CoRR, vol. abs/1812.03079, 2018.  

 [5] C. Urmson, J. Anhalt, D. Bagnell, C. R. Baker, R. Bittner, M. N. Clark, J. M. Dolan, D. Duggins, T. Galatali, C. Geyer, M. Gittleman, S. Harbaugh, M. Hebert, T. M. Howard, S. Kolski, A. Kelly, M. Likhachev, M. McNaughton, N. Miller, K. M. Peterson, B. Pilnick, R. Rajkumar, P. E. Rybski, B. Salesky, Y-W. Seo, S. Singh, J. M. Snider, A. Stentz, W. Whittaker, Z. Wolkowicki, J. Ziglar, H. Bae, T. Brown, D. Demitrish, B. Litkouhi, J. Nickolaou, V. Sadekar, W. Zhang, J. Struble, M. Taylor, M. Darms, and D. Ferguson, “Autonomous driving in urban environments: Boss and the urban challenge,” in The DARPA Urban Challenge: Autonomous Vehicles in City Traffic, George Air Force Base, Victorville, California, USA, 2009, pp. 1–59.  

 [6] G. P. Meyer, A. Laddha, E. Kee, C. Vallespi-Gonzalez, and C. K. Wellington, “Lasernet: An efficient probabilistic 3d object detector for autonomous driving,” in Proc. IEEE Int. Conf. Comput. Vis. Pattern Recogn., 2019. 

  [7] C. Ruizhongtai Qi, H. Su, K. Mo, and L. J. Guibas, “Pointnet: Deep learning on point sets for 3d classification and segmentation,” in Proc. IEEE Int. Conf. Comput. Vis. Pattern Recogn., 2017, pp. 77–85. 

  [8] X. Chen, H. Ma, J. Wan, B. Li, and T. Xia, “Multi-view 3d object detection network for autonomous driving,” in Proc. IEEE Int. Conf. Comput. Vis. Pattern Recogn., 2017, pp. 6526–6534. 

 [9] M. A. Fischler and R. C. Bolles, “Random sample consensus: a paradigm for model fitting with applications to image analysis and automated cartography,” Communications of the ACM, vol. 24, no. 6, pp. 381–395, 1981. 

  [10] X-F. Hana, J. S. Jin, J. Xie, M-J. Wang, and W. Jiang, “A comprehensive review of 3d point cloud descriptors,” arXiv preprint arXiv:1802.02297, 2018.  

 [11] J. Peng and C.-C. Jay Kuo, “Geometry-guided progressive lossless 3D mesh coding with octree (OT) decomposition,” ACM Trans. Graph. Proceedings of ACM SIGGRAPH, vol. 24, no. 3, pp. 609–616, Jul. 2005.  

 [12] A. Ortega, P. Frossard, J. Kovacevic, J. M. F. Moura, and P. Vandergheynst, “Graph signal processing: Overview, challenges, and applications,” Proceedings of the IEEE, vol. 106, no. 5, pp. 808–828, 2018. 

  [13] S. Chen, D. Tian, C. Feng, A. Vetro, and J. Kovacevi ˇ c, “Fast resampling ´ of three-dimensional point clouds via graphs,” IEEE Trans. Signal Processing, vol. 66, no. 3, pp. 666–681, 2018.  

 [14] Y. Wang, Y. Sun, Z. Liu, S. E. Sarma, M. M. Bronstein, and J. M. Solomon, “Dynamic graph CNN for learning on point clouds,” ACM Transactions on Graphics (TOG), vol. 38, no. 5, November 2019.  

 [15] S. Chen, S. Niu, T. Lan, and B. Liu, “Large-scale 3d point cloud representations via graph inception networks with applications to autonomous driving,” in Proc. IEEE Int. Conf. Image Process., Taipei, Taiwan, Sept. 2019.  

 [16] G. Li, M. Muller, A. K. Thabet, and B. Ghanem, “DeepGCNs: Can ¨ GCNs go as deep as CNNs?,” in ICCV, Seoul, South Korea, Oct. 2019. 

  [17] G. Grisetti, R. Kummerle, C. Stachniss, and W. Burgard, “A tutorial ¨ on graph-based SLAM,” IEEE Intell. Transport. Syst. Mag., vol. 2, no. 4, pp. 31–43, 2010. 

  [18] D. Droeschel and S. Behnke, “Efficient continuous-time SLAM for 3d lidar-based online mapping,” in 2018 IEEE International Conference on Robotics and Automation, ICRA, 2018, Brisbane, Australia, May 21-25, 2018, 2018, pp. 1–9. 

 [19] P. J. Besl and N. D. McKay, “A method for registration of 3D shapes,” IEEE Trans. Pattern Anal. Mach. Intell., vol. 14, no. 2, pp. 239–256, 1992.  

 [20] A. Y. Hata and D. F. Wolf, “Road marking detection using LIDAR reflective intensity data and its application to vehicle localization,” in 17th International IEEE Conference on Intelligent Transportation Systems, ITSC 2014, Qingdao, China, October 8-11, 2014, 2014, pp. 584–589. 

  [21] S. Shi, X. Wang, and H. Li, “PointRCNN: 3d object proposal generation and detection from point cloud,” in Proc. IEEE Int. Conf. Comput. Vis. Pattern Recogn., Long Beach, CA, June 2019.  

 [22] B. Li, “3d fully convolutional network for vehicle detection in point cloud,” in 2017 IEEE/RSJ International Conference on Intelligent Robots and Systems, IROS 2017, Vancouver, BC, Canada, September 24-28, 2017, 2017, pp. 1513–1518. 

  [23] B. Yang, W. Luo, and R. Urtasun, “PIXOR: real-time 3d object detection from point clouds,” in Proc. IEEE Int. Conf. Comput. Vis. Pattern Recogn., 2018, pp. 7652–7660.  

 [24] J. Zhou, X. Lu, X. Tan, Z. Shao, S. Ding, and L. Ma, “Fvnet: 3d front-view proposal generation for real-time object detection from point clouds,” CoRR, vol. abs/1903.10750, 2019.  

 [25] B. Li, T. Zhang, and T. Xia, “Vehicle detection from 3d lidar using fully convolutional network,” in Robotics: Science and Systems XII, University of Michigan, Ann Arbor, Michigan, USA, June 18 - June 22, 2016, 2016. 

  [26] Y. Zhou and O. Tuzel, “Voxelnet: End-to-end learning for point cloud based 3d object detection,” in Proc. IEEE Int. Conf. Comput. Vis. Pattern Recogn., Salt Lake City, UT, USA, June 2018, pp. 4490–4499.  

 [27] S. Shi, Z. Wang, X. Wang, and H. Li, “Part-a2 net: 3d part-aware and aggregation neural network for object detection from point cloud,” CoRR, vol. abs/1907.03670, 2019.  

 [28] Y. Yan, Y. Mao, and B. Li, “Second: Sparsely embedded convolutional detection,” Sensors, vol. 18, no. 10, 2019. 

  [29] A. H. Lang, S. Vora, H. Caesar, L. Zhou, J. Yang, and O. Beijbom, “Pointpillars: Fast encoders for object detection from point clouds,” CoRR, vol. abs/1812.05784, 2018.  

 [30] T-Y. Lin, P. Dollar, R. B. Girshick, K. He, B. Hariharan, and S. J. ´ Belongie, “Feature pyramid networks for object detection,” in Proc. IEEE Int. Conf. Comput. Vis. Pattern Recogn., 2017, pp. 936–944.  

 [31] F. Yu, D. Wang, E. Shelhamer, and T. Darrell, “Deep layer aggregation,” in Proc. IEEE Int. Conf. Comput. Vis. Pattern Recogn., 2018, pp. 2403–2412. 

  [32] W. Liu, D. Anguelov, D. Erhan, C. Szegedy, S. E. Reed, C-Y. Fu, and A. C. Berg, “SSD: single shot multibox detector,” in Computer Vision - ECCV 2016 - 14th European Conference, Amsterdam, The Netherlands, October 11-14, 2016, Proceedings, Part I, 2016, pp. 21–37. 

  [33] T-Y. Lin, P. Goyal, R. B. Girshick, K. He, and P. Dollar, “Focal ´ loss for dense object detection,” in IEEE International Conference on Computer Vision, ICCV 2017, Venice, Italy, October 22-29, 2017, 2017, pp. 2999–3007.  

 [34] J. Ku, M. Mozifian, J. Lee, A. Harakeh, and S. L. Waslander, “Joint 3d proposal generation and object detection from view aggregation,” in 2018 IEEE/RSJ International Conference on Intelligent Robots and Systems, IROS 2018, Madrid, Spain, October 1-5, 2018, 2018, pp. 1–8.  

 [35] C. Ruizhongtai Qi, W. Liu, C. Wu, H. Su, and L. J. Guibas, “Frustum pointnets for 3d object detection from RGB-D data,” in Proc. IEEE Int. Conf. Comput. Vis. Pattern Recogn., 2018, pp. 918–927.  

 [36] D. Xu, D. Anguelov, and A. Jain, “PointFusion: Deep sensor fusion for 3d bounding box estimation,” in Proc. IEEE Int. Conf. Comput. Vis. Pattern Recogn. 2018, pp. 244–253, IEEE Computer Society.  

 [37] M. Liang, B. Yang, S. Wang, and R. Urtasun, “Deep continuous fusion for multi-sensor 3d object detection,” in Computer Vision - ECCV 2018 - 15th European Conference, Munich, Germany, September 8-14, 2018, Proceedings, Part XVI, 2018, pp. 663–678. 

  [38] M. Liang, B. Yang, Y. Chen, R. Hu, and R. Urtasun, “Multi-task multi-sensor fusion for 3d object detection,” in Proc. IEEE Int. Conf. Comput. Vis. Pattern Recogn., 2019, pp. 7345–7353. 

  [39] G. P. Meyer, J. Charland, D. Hegde, A. Laddha, and C. VallespiGonzalez, “Sensor fusion for joint 3d object detection and semantic segmentation,” CoRR, vol. abs/1904.11466, 2019.  

 [40] A. Geiger, P. Lenz, and R. Urtasun, “Are we ready for autonomous driving? the KITTI vision benchmark suite,” in Proc. IEEE Int. Conf. Comput. Vis. Pattern Recogn., Providence, RI, June 2012, pp. 3354– 3361.  

 [41] K-L. Low, “Linear least-squares optimization for point-toplane icp surface registration,” Tech. Rep., University of North Carolina at Chapel Hill, 2004.  

 [42] J. Yang, H. Li, D. Campbell, and Y. Jia, “Go-icp: A globally optimal solution to 3d ICP point-set registration,” IEEE Trans. Pattern Anal. Mach. Intell., vol. 38, no. 11, pp. 2241–2254, 2016.  

 [43] A. Geiger, P. Lenz, C. Stiller, and R. Urtasun, “Vision meets robotics: The kitti dataset,” International Journal of Robotics Research (IJRR), 2013.  

 [44] Z. Wu, S. Song, A. Khosla, F. Yu, L. Zhang, X. Tang, and J. Xiao, “3d shapenets: A deep representation for volumetric shapes,” in Proc. IEEE Int. Conf. Comput. Vis. Pattern Recogn., 2015, pp. 1912–1920. 

  [45] F. Pomerleau, F. Colas, and R. Siegwart, “A review of point cloud registration algorithms for mobile robotics,” Foundations and Trends in Robotics, vol. 4, no. 1, pp. 1–104, 2015.  

 [46] H. Fathi, F. Dai, and M. I. A. Lourakis, “Automated as-built 3d reconstruction of civil infrastructure using computer vision: Achievements, opportunities, and challenges,” Advanced Engineering Informatics, vol. 29, no. 2, pp. 149–161, 2015.  

 [47] B. Reitinger, C. Zach, and D. Schmalstieg, “Augmented reality scouting for interactive 3d reconstruction,” in IEEE Virtual Reality Conference, VR 2007, 10-14 March 2007, Charlotte, NC, USA, Proceedings, 2007, pp. 219–222. 

 To be continued... 

 resource 

 3D point cloud paper and related application sharing 

 [Point cloud paper speed reading] Odometer based on lidar and positioning method in 3D point cloud map 

 3D object detection: MV3D-Net 

 Overview of 3D Point Cloud Segmentation (Part 1) 

 3D-MiniNet: Learning 2D Representations from Point Clouds for Fast and Efficient 3D LIDAR Semantic Segmentation (2020) 

 Use QT to add VTK plug-in under win to realize point cloud visualization GUI 

 JSNet: Joint Instances and Semantic Segmentation for 3D Point Clouds 

 A Survey of Semantic Segmentation of 3D Point Cloud in Large Scene 

 The outofcore module in PCL---Display of large-scale point clouds based on out-of-core octree 

 Target Segmentation Based on Local Convex 

 Point cloud labeling based on 3D convolutional neural networks 

 SuperVoxel of Point Cloud 

 Large-scale point cloud segmentation based on hyperdot graph 

 More articles can be viewed: A summary of historical articles on point cloud learning 

 SLAM and AR related sharing 

 [Open source solution sharing] ORB-SLAM3 is open source! 

 AVP-SLAM: Semantic SLAM in Automatic Parking Systems 

 [Point Cloud Paper Speed Reading] StructSLAM: Structured Line Feature SLAM 

 SLAM and AR Overview 

 Commonly used 3D depth cameras 

 Overview and Evaluation of Monocular Vision Inertial Navigation SLAM Algorithm for AR Devices 

 SLAM Review (4) Laser and Vision Fusion SLAM 

 Kimera's Semantic SLAM System for Real-Time Reconstruction 

 Overview of SLAM (3) - Vision and inertial navigation, vision and deep learning SLAM 

 Extensible SLAM Framework - OpenVSLAM 

 Gao Xiang: Challenges in unstructured road laser SLAM 

 SLAM Overview of Lidar SLAM 

 SLAM Method Based on Fisheye Camera 

 Online sharing and recording summary in the past 

 3D Model Retrieval Technology of the First Bilibili Recording 

 Application of deep learning in 3D scenes recorded and broadcast by Bilibili 

 The third Bilibili recording of CMake advanced learning 

 Point Cloud Object and Six-Degree-of-Freedom Attitude Estimation Recorded by Bilibili 

 The fifth Bilibili recording of point cloud deep learning semantic segmentation expansion 

 Pointnetlk Interpretation of the 6th Bilibili Recording 

 [线上分享录播]点云配准概述及其在激光SLAM中的应用 

 [线上分享录播]cloudcompare插件开发 

 [线上分享录播]基于点云数据的 Mesh重建与处理 

 [线上分享录播]机器人力反馈遥操作技术及机器人视觉分享 

 [线上分享录播]地面点云配准与机载点云航带平差 

 If you are interested in this article, please send "Knowledge Planet" in the background to get the QR code. Be sure to join the free Knowledge Planet according to the remarks of "Name + School/Company + Research Direction", download the pdf document for free, and communicate with more friends who love to share! 

 If the above content is wrong, please leave a comment, and welcome to correct and communicate. If there is any infringement, please contact to delete it. 

 ![avatar]( 35373ef3189a78155d2e95ccecc7a390.png) 

 Scan QR code 

                    Follow us 

 Let's share and learn together! Looking forward to friends who have ideas and are willing to share joining the free planet to inject fresh vitality of love and sharing. The topics shared include but are not limited to 3D vision, point clouds, high-precision maps, autonomous driving, and robotics and other related fields. 

 Sharing and cooperation method: WeChat "920177957" (note required) Contact email: dianyunpcl@163.com, enterprises are welcome to contact the official account for cooperation. 



--------------------------------------------------------------------------------

标题：3D Point Cloud Processing and Learning for Autonomous Driving 

 作者：Siheng Chen, Baoan Liu, Chen Feng, Carlos Vallespi-Gonzalez, Carl Wellington 

 Compiler: Point Cloud PCL 

 Source: arXiv 2020 

 This article is for academic sharing only. If there is any infringement, please contact to delete it. Welcome to join the free knowledge planet, get PDF papers, and welcome to forward Moments. If there is any error in the content, please comment and leave a message. Please do not reprint without permission! 

 The official account is dedicated to sharing articles and technologies related to point cloud processing, SLAM, 3D vision, and high-precision maps. Welcome to join us and make progress together with each exchange. If you are interested, please contact WeChat 920177957. 

 Write on the front 

 This article can be said to be a very complete introduction to the role of point clouds in autonomous driving of each module, from the macro sub-module of the point cloud in the role and application of autonomous driving, read the entire article, will not only have a more comprehensive understanding of autonomous driving technology, and understand the importance of point clouds in autonomous driving, the creation of high-precision maps introduced here and positioning perception module introduction is the core technology in the field of autonomous driving, such as in the introduction of the two positioning methods of the positioning module, when introducing the use of semantic geometric information and point cloud intensity information for positioning in different scenarios, it is completely suitable for the apollo autonomous driving solution, allowing readers to gain a lot. Here the blogger decided to translate it completely and share it with more interested friends. 

 There may be clerical errors or poor understanding in the process of translation and understanding. Everyone is welcome to leave a message. Due to the length of the article, the article will be divided into multiple articles and updated. The full English pdf is available on the free Knowledge Planet. 

 directory 

 1. Introduction 

 The significance, history and current situation of autonomous driving 

 1-B A complete autonomous driving system module 

 1-C 3D point cloud processing and learning 

 1-D Outline 

 2. Key elements of 3D point cloud processing and learning 

 2-A point cloud characteristics 

 2-B matrix representation 

 2-C representative tools 

 3. Creation of high-precision maps and processing of 3D point clouds 

 Overview of 3-A high-definition map creation module 

 Splicing of 3-B 3D Point Clouds 

 Extraction of semantic features from 3-C point clouds 

 3-D map creation challenges 

 4. Processing based on point cloud positioning 

 Overview of 4-A Positioning Module 

 4-B Map-based Localization 

 4-C point cloud positioning challenges 

 5. Point cloud perception 

 5-A Perception Module Overview 

 Detection of 5-B 3D Point Cloud Objects 

 5-C point cloud perception challenges 

 6. Summarize and expand the problem 

 6-A The relationship between academia and industry 

 6-B qualitative results 

 3. Creation of high-precision maps and processing of 3D point clouds 

 3-A 

 Overview of high-definition map creation module 

 A high-definition (HD) map for autonomous driving is an accurate heterogeneous map representation of a static 3D environment and traffic rules. It typically consists of two map layers: 

 The main reason for creating offline high-precision maps is that real-time detection is too challenging to understand the traffic rules in the road. For example, based on existing technology, it is difficult for autonomous vehicles to determine the correct lane in real time at the intersection of complex lane mergers and forks. In contrast, all traffic rules and environmental information can be easily encoded into high-precision maps, which go through the offline process under human supervision and quality assurance. High-precision maps provide powerful and indispensable prior knowledge, fundamentally simplifying the design of multiple modules in autonomous driving systems, including positioning, perception, prediction, and motion planning. Therefore, high-precision maps are widely regarded as an indispensable component of autonomous driving. The role of high-precision maps is as follows: 

 Positioning a priori. The role of positioning is to locate the pose of autonomous vehicles. In high-precision maps, point cloud maps and semantic features related to traffic rules (such as lane markings and markers) are usually used as a priori for map-based positioning. These priors are used to register the point cloud map with the real-time lidar scanning point cloud, so as to obtain the real-time high-precision motion pose of the autonomous vehicle. 

 A priori knowledge of perception. The role of perception is to detect all objects in the scene, as well as their internal states. The perception module can use high-precision maps as a priori for detection. For example, the position of traffic lights in HD maps is often used as a perception priori for traffic light state estimation. Taking the point cloud map as a priori, the real-time LiDAR scanning point cloud can be divided into foreground points and background points. The background points, that is, those points located on static scenes, such as road surfaces and tree trunks, can then be removed, and only the front attractions are provided to the perception module. This form can greatly reduce the amount of calculation and improve the accuracy of object detection. 

 Predictive prior knowledge. The role of prediction is to predict the future trajectory of each object in the scene. In high-precision maps, the geometric structure and connectivity of roads and lanes in 3D are important prerequisites for the prediction module. This prior knowledge can be used to guide the predicted target trajectory to follow the lane. 

 A priori knowledge of motion planning. The role of motion planning is to determine the motion trajectories of autonomous vehicles. In high-precision maps, semantic features related to traffic rules (such as lane geometry and connectivity, traffic lights, traffic signs, and lane speed limits) are essential prerequisites for the motion planning module. This a priori knowledge is used to guide predetermined trajectories to follow the correct lanes and obey stop signs and other traffic signs. Since high-precision maps are important for autonomous driving, high-precision maps must be created and timely updated. To achieve this, complex engineering procedures are often required, utilizing machine learning techniques and human supervision to analyze the acquired data from multiple modes. The standard map creation module includes two core components: 3D point cloud splicing and semantic feature extraction; 3D point cloud splicing merges real-time lidar scanning point cloud data collected from multiple vehicles across time into the point cloud map; semantic feature extraction extracts semantic features such as lane geometry and traffic lights from the point cloud map. 

 ![avatar]( 20210306150344689.gif) 

 As shown in the figure, a standard high-precision map generation system consists of two core components: 3D point cloud stitching and semantic feature extraction. 3D point cloud stitching usually adopts the method of SLAM based on graph theory, and the semantic feature extraction involves machine learning and human supervision of the iterative process. A key component of graph-based SLAM is the attitude graph, which models the relationship between LiDAR poses. Nodes are the edges between the LiDAR pose and the non-aligned level representing two frames of LiDAR poses. The final output includes a point cloud map, which is a dense 3D point cloud, and a semantic feature map related to traffic rules, which contains the locations of road signs, traffic signs, and traffic lights 

 3-B 

 Splicing of 3D Point Clouds 

 The goal of 3D point cloud splicing is to generate high-precision point cloud maps using sensor data collected by the fleet at different time periods. Since point cloud maps are related to the prior accuracy of all maps, any local part of the point cloud map requires centimeter-level accuracy. In order to quickly create and update city-level high-precision maps, the 3D point cloud splicing process must be highly robust and efficient. 

 A fundamental problem in 3D point cloud stitching is to estimate the 6-degree-of-freedom attitude, also known as the LiDAR attitude, for each LiDAR scan. Think of the map frame as a standardized global frame, and the LiDAR frame as a self-moving point cloud frame of the autonomous vehicle when the timestamp of the corresponding real-time LiDAR point cloud is acquired. Then, the LiDAR attitude is the transformation between the map frame and the LiDAR frame. It includes three-dimensional translation and three-dimensional rotation. Note that the 6-degree-of-freedom attitude can be represented as a 4 × 4 homogeneous transformation matrix. With the LiDAR attitude, all LiDAR scanning point clouds can be synchronized into a standardized global frame and integrated into a dense 3D point cloud. To estimate the attitude of the LiDAR, a commonly used technique is the Synchronous Localization and Mapping (SLAM) technique. Let Si and Sj be the i-th and j-th real-time lidar scans, respectively. Its SLAM expression is: 

 ![avatar]( 4aac2b6e656cf60478147736b353736b.png) 

 Where pi is the 6-degree-of-freedom attitude associated with the i-th real-time lidar scan point cloud, h_Si; Sj (pi, pj) represents the negative logarithmic maximum likelihood between Si and Sj, and g (〃) represents the negative logarithmic likelihood of the difference between the predicted lidar position in the map frame and the GPS measurement. h_SiSj represents the objective function of the iterative closest point (ICP) algorithm and minimizes the objective function of the ICP algorithm. 

 SLAM is an important research field in the field of robotics. At present, a large number of studies have been devoted to solving optimization problems. For example, filter-based SLAM solves optimization problems in an approximate real-time manner. Based on real-time sensor measurements, Bayesian filtering is used to iteratively predict and optimize maps and lidar poses. On the other hand, graph-based SLAM optimizes all lidar poses by using all sensor measurements across time. It constructs an attitude graph to simulate the relationship between lidar poses. Intuitively, the weight of each edge is either the point-to-point distance between two lidar scan points or the point-to-surface distance. Therefore, solving the SLAM equation is equivalent to minimizing the sum of the weights of the edges of the pose graph. 

 For the creation of city-level high-resolution maps, SLAM solutions must meet the following requirements: 

 Accuracy of higher local and global maps. Local accuracy indicates that the lidar attitude of one local area is accurate relative to another area; global accuracy indicates that all lidar attitudes in the entire high definition map are accurate relative to the global frame. For SLAM solutions, since the autonomous driving software module requires high-precision local environment of high-precision maps, the constructed map must achieve local accuracy of centimeters per microradian; centimeter-level global accuracy helps to speed up the update process of high definition maps, especially for city-scale applications; 

 High robustness. The SLAM solution needs to process noise sensor measurements collected by multiple vehicles in complex scenarios and complex driving conditions, and has 

 High efficiency. SLAM solutions need to handle the optimization of more than hundreds of millions of LiDAR poses. To achieve higher accuracy and robustness, graph-based SLAMs have a better choice than filter-based SLAMs because the form of global optimization makes graph-based SLAMs inherently more precise; however, solving city-scale graph-based SLAM problems with high efficiency and robustness remains a challenge for two main reasons. First, the scale of the scenario is enormous. Since the core step of the optimization algorithm is to solve a series of equations associated with n × n matrices, where n is the total number of LiDAR poses, solving the optimization problem in a brute-force manner is expensive. For city-scale maps, n may be hundreds of millions, which has a great impact on the computational efficiency and numerical stability of the optimization algorithm. Secondly, since the sensor data is collected under complex driving conditions, the calculation accuracy of the edge weights of the attitude map is low. For example, the mismatch calculation between point clouds scanned by continuous lidar may be affected by moving objects. 

 To solve this problem efficiently, graph-based SLAM and hierarchical refinement forms can be employed [18]. The function of hierarchical refinement methods is to provide good initialization for global optimization, making optimization both fast and accurate. The hierarchical refinement form distinguishes between two types of edges in the attitude graph: adjacent edges and closed edges. Adjacent edges are to model the relationship between two lidar poses, whose corresponding lidar scan points are successive frames from the same dataset; cyclic closed edges are to model the relationship between two lidar poses, whose corresponding lidar point clouds are point cloud frames collected at the same location from different datasets (different vehicles or across time). To handle both types of edges, the hierarchical refinement form consists of two steps: 

 (1) Optimize adjacent edges, including LiDAR pose maps from a single dataset. 

 (2) Optimize loop closed edges, including LiDAR pose across time datasets. 

 In the first step, sensor measurements from multiple modes (including IMU, GPS, odometer, camera, and LiDAR) can be fused together, rather than simply relying on aligning LiDAR scans to calculate adjacent edges. Because successive LiDAR scans have similar LiDAR attitudes, this step is usually easy and provides extremely high accuracy. In the second step, the loop closed edges are calculated by aligning the LiDAR scans with the ICP algorithm. After these two steps, global optimization is performed. Since most edges in the attitude graph are adjacent edges, high-precision optimization can be performed with the first step, so the hierarchical refinement form provides good initialization for global optimization. Therefore, the hierarchical refinement method can greatly reduce the computational effort of the entire pose map optimization and improve the robustness of the global optimization. 

 3-C 

 Point Cloud Semantic Feature Extraction 

 The purpose of semantic feature extraction is to extract semantic features related to traffic rules from point cloud maps, such as geometric properties of lanes, lane connectivity, traffic signs and traffic lights, etc. This module requires high accuracy and recall rate. For example, losing a traffic light in a city high-precision map may cause serious problems for perception and motion planning modules, thus seriously compromising the safety of autonomous driving. The semantic feature extraction component usually consists of two iterative steps: 

 For automatic feature extraction, standard machine learning techniques are based on convolutional neural networks. The input is typically a collection of LiDAR ground images and camera images associated with the corresponding real-time LiDAR scan point cloud. A BEV-based representation of a point cloud map obtained in the 3D point cloud stitching of LiDAR ground images rendering, where the value of each pixel is the ground height and laser reflectivity of each LiDAR point. The output is typically a semantic segmentation of a LiDAR ground image or camera image. These networks follow a standard image segmentation architecture. After the output is obtained, pixel-by-pixel semantic labels are projected back to the point cloud map. By simulating the projected 3D points into 3D splines or 3D polygons, a semantic feature map related to traffic rules is obtained. Please note that the results of human editing jobs can also be used as an important training data source for automatic feature extraction algorithms, so these two steps form a positive feedback loop to improve the accuracy and efficiency of high-precision map production. 

 3-D 

 Map creation challenges 

 There are still some challenges in the production of high-precision maps. 

 Global centimeter-level point cloud map. Urban large-scale scene updates with global precision point cloud maps are of great help, and changes in urban features usually occur in local areas. Ideally, map updates should focus on the target part of the attitude map; however, point cloud maps with high local accuracy but no global accuracy will not be able to freely access the target scene from a global perspective and guarantee its overall accuracy. In contrast, for point cloud maps with high global accuracy, one can concentrate on updating the target part of the attitude map, thus significantly reducing the computational scale; however, for graph-based SLAM, it is a challenge to mandate that the map has global accuracy. This is because the global optimization method of graph-based SLAM tends to distribute the error of each edge evenly in the graph. Therefore, even if GPS observations are accurate, the corresponding LiDAR attitude will be skewed after global optimization. Enforcing centimeter-level global accuracy for point cloud maps can be particularly challenging where GPS signals are not available, such as in building canyons, tunnels, and underground garages. 

 Automatic Semantic Feature Extraction. Although semantic segmentation methods based on 3D point clouds and camera images have been widely studied, the automatic extraction of lane connectivity representing lane interrelationships in intersections and traffic lights remains a challenge. This is due to limited training labels and complex traffic conditions. Currently, solutions for extracting complex semantic features such as traffic lights to lane information still mainly rely on manual control, which is both time-consuming and costly. 

 References 

 Swipe up to view 

 [1] A. Taeihagh and H. Si Min Lim, “Governing autonomous vehicles: emerging responses for safety, liability, privacy, cybersecurity, and industry risks,” Transport Reviews, vol. 39, no. 1, pp. 103–128, Jan. 2019.  

 [2] National Research Council, “Technology development for army unmanned ground vehicles,” 2002.  

 [3] C. Badue, R. Guidolini, R. Vivacqua Carneiro, P. Azevedo, V. Brito Cardoso, A. Forechi, L. Ferreira Reis Jesus, R. Ferreira Berriel, T. Meireles Paixo, F. Mutz, T. Oliveira-Santos, and A. Ferreira De Souza, “Self-driving cars: A survey,” arXiv:1901.04407 [cs.RO], Jan. 2019. [4] M. Bansal, A. Krizhevsky, and A. S. Ogale, “ChauffeurNet: Learning to drive by imitating the best and synthesizing the worst,” CoRR, vol. abs/1812.03079, 2018.  

 [5] C. Urmson, J. Anhalt, D. Bagnell, C. R. Baker, R. Bittner, M. N. Clark, J. M. Dolan, D. Duggins, T. Galatali, C. Geyer, M. Gittleman, S. Harbaugh, M. Hebert, T. M. Howard, S. Kolski, A. Kelly, M. Likhachev, M. McNaughton, N. Miller, K. M. Peterson, B. Pilnick, R. Rajkumar, P. E. Rybski, B. Salesky, Y-W. Seo, S. Singh, J. M. Snider, A. Stentz, W. Whittaker, Z. Wolkowicki, J. Ziglar, H. Bae, T. Brown, D. Demitrish, B. Litkouhi, J. Nickolaou, V. Sadekar, W. Zhang, J. Struble, M. Taylor, M. Darms, and D. Ferguson, “Autonomous driving in urban environments: Boss and the urban challenge,” in The DARPA Urban Challenge: Autonomous Vehicles in City Traffic, George Air Force Base, Victorville, California, USA, 2009, pp. 1–59.  

 [6] G. P. Meyer, A. Laddha, E. Kee, C. Vallespi-Gonzalez, and C. K. Wellington, “Lasernet: An efficient probabilistic 3d object detector for autonomous driving,” in Proc. IEEE Int. Conf. Comput. Vis. Pattern Recogn., 2019. 

  [7] C. Ruizhongtai Qi, H. Su, K. Mo, and L. J. Guibas, “Pointnet: Deep learning on point sets for 3d classification and segmentation,” in Proc. IEEE Int. Conf. Comput. Vis. Pattern Recogn., 2017, pp. 77–85. 

  [8] X. Chen, H. Ma, J. Wan, B. Li, and T. Xia, “Multi-view 3d object detection network for autonomous driving,” in Proc. IEEE Int. Conf. Comput. Vis. Pattern Recogn., 2017, pp. 6526–6534. 

 [9] M. A. Fischler and R. C. Bolles, “Random sample consensus: a paradigm for model fitting with applications to image analysis and automated cartography,” Communications of the ACM, vol. 24, no. 6, pp. 381–395, 1981. 

  [10] X-F. Hana, J. S. Jin, J. Xie, M-J. Wang, and W. Jiang, “A comprehensive review of 3d point cloud descriptors,” arXiv preprint arXiv:1802.02297, 2018.  

 [11] J. Peng and C.-C. Jay Kuo, “Geometry-guided progressive lossless 3D mesh coding with octree (OT) decomposition,” ACM Trans. Graph. Proceedings of ACM SIGGRAPH, vol. 24, no. 3, pp. 609–616, Jul. 2005.  

 [12] A. Ortega, P. Frossard, J. Kovacevic, J. M. F. Moura, and P. Vandergheynst, “Graph signal processing: Overview, challenges, and applications,” Proceedings of the IEEE, vol. 106, no. 5, pp. 808–828, 2018. 

  [13] S. Chen, D. Tian, C. Feng, A. Vetro, and J. Kovacevi ˇ c, “Fast resampling ´ of three-dimensional point clouds via graphs,” IEEE Trans. Signal Processing, vol. 66, no. 3, pp. 666–681, 2018.  

 [14] Y. Wang, Y. Sun, Z. Liu, S. E. Sarma, M. M. Bronstein, and J. M. Solomon, “Dynamic graph CNN for learning on point clouds,” ACM Transactions on Graphics (TOG), vol. 38, no. 5, November 2019.  

 [15] S. Chen, S. Niu, T. Lan, and B. Liu, “Large-scale 3d point cloud representations via graph inception networks with applications to autonomous driving,” in Proc. IEEE Int. Conf. Image Process., Taipei, Taiwan, Sept. 2019.  

 [16] G. Li, M. Muller, A. K. Thabet, and B. Ghanem, “DeepGCNs: Can ¨ GCNs go as deep as CNNs?,” in ICCV, Seoul, South Korea, Oct. 2019. 

  [17] G. Grisetti, R. Kummerle, C. Stachniss, and W. Burgard, “A tutorial ¨ on graph-based SLAM,” IEEE Intell. Transport. Syst. Mag., vol. 2, no. 4, pp. 31–43, 2010. 

  [18] D. Droeschel and S. Behnke, “Efficient continuous-time SLAM for 3d lidar-based online mapping,” in 2018 IEEE International Conference on Robotics and Automation, ICRA, 2018, Brisbane, Australia, May 21-25, 2018, 2018, pp. 1–9. 

 [19] P. J. Besl and N. D. McKay, “A method for registration of 3D shapes,” IEEE Trans. Pattern Anal. Mach. Intell., vol. 14, no. 2, pp. 239–256, 1992.  

 [20] A. Y. Hata and D. F. Wolf, “Road marking detection using LIDAR reflective intensity data and its application to vehicle localization,” in 17th International IEEE Conference on Intelligent Transportation Systems, ITSC 2014, Qingdao, China, October 8-11, 2014, 2014, pp. 584–589. 

  [21] S. Shi, X. Wang, and H. Li, “PointRCNN: 3d object proposal generation and detection from point cloud,” in Proc. IEEE Int. Conf. Comput. Vis. Pattern Recogn., Long Beach, CA, June 2019.  

 [22] B. Li, “3d fully convolutional network for vehicle detection in point cloud,” in 2017 IEEE/RSJ International Conference on Intelligent Robots and Systems, IROS 2017, Vancouver, BC, Canada, September 24-28, 2017, 2017, pp. 1513–1518. 

  [23] B. Yang, W. Luo, and R. Urtasun, “PIXOR: real-time 3d object detection from point clouds,” in Proc. IEEE Int. Conf. Comput. Vis. Pattern Recogn., 2018, pp. 7652–7660.  

 [24] J. Zhou, X. Lu, X. Tan, Z. Shao, S. Ding, and L. Ma, “Fvnet: 3d front-view proposal generation for real-time object detection from point clouds,” CoRR, vol. abs/1903.10750, 2019.  

 [25] B. Li, T. Zhang, and T. Xia, “Vehicle detection from 3d lidar using fully convolutional network,” in Robotics: Science and Systems XII, University of Michigan, Ann Arbor, Michigan, USA, June 18 - June 22, 2016, 2016. 

  [26] Y. Zhou and O. Tuzel, “Voxelnet: End-to-end learning for point cloud based 3d object detection,” in Proc. IEEE Int. Conf. Comput. Vis. Pattern Recogn., Salt Lake City, UT, USA, June 2018, pp. 4490–4499.  

 [27] S. Shi, Z. Wang, X. Wang, and H. Li, “Part-a2 net: 3d part-aware and aggregation neural network for object detection from point cloud,” CoRR, vol. abs/1907.03670, 2019.  

 [28] Y. Yan, Y. Mao, and B. Li, “Second: Sparsely embedded convolutional detection,” Sensors, vol. 18, no. 10, 2019. 

  [29] A. H. Lang, S. Vora, H. Caesar, L. Zhou, J. Yang, and O. Beijbom, “Pointpillars: Fast encoders for object detection from point clouds,” CoRR, vol. abs/1812.05784, 2018.  

 [30] T-Y. Lin, P. Dollar, R. B. Girshick, K. He, B. Hariharan, and S. J. ´ Belongie, “Feature pyramid networks for object detection,” in Proc. IEEE Int. Conf. Comput. Vis. Pattern Recogn., 2017, pp. 936–944.  

 [31] F. Yu, D. Wang, E. Shelhamer, and T. Darrell, “Deep layer aggregation,” in Proc. IEEE Int. Conf. Comput. Vis. Pattern Recogn., 2018, pp. 2403–2412. 

  [32] W. Liu, D. Anguelov, D. Erhan, C. Szegedy, S. E. Reed, C-Y. Fu, and A. C. Berg, “SSD: single shot multibox detector,” in Computer Vision - ECCV 2016 - 14th European Conference, Amsterdam, The Netherlands, October 11-14, 2016, Proceedings, Part I, 2016, pp. 21–37. 

  [33] T-Y. Lin, P. Goyal, R. B. Girshick, K. He, and P. Dollar, “Focal ´ loss for dense object detection,” in IEEE International Conference on Computer Vision, ICCV 2017, Venice, Italy, October 22-29, 2017, 2017, pp. 2999–3007.  

 [34] J. Ku, M. Mozifian, J. Lee, A. Harakeh, and S. L. Waslander, “Joint 3d proposal generation and object detection from view aggregation,” in 2018 IEEE/RSJ International Conference on Intelligent Robots and Systems, IROS 2018, Madrid, Spain, October 1-5, 2018, 2018, pp. 1–8.  

 [35] C. Ruizhongtai Qi, W. Liu, C. Wu, H. Su, and L. J. Guibas, “Frustum pointnets for 3d object detection from RGB-D data,” in Proc. IEEE Int. Conf. Comput. Vis. Pattern Recogn., 2018, pp. 918–927.  

 [36] D. Xu, D. Anguelov, and A. Jain, “PointFusion: Deep sensor fusion for 3d bounding box estimation,” in Proc. IEEE Int. Conf. Comput. Vis. Pattern Recogn. 2018, pp. 244–253, IEEE Computer Society.  

 [37] M. Liang, B. Yang, S. Wang, and R. Urtasun, “Deep continuous fusion for multi-sensor 3d object detection,” in Computer Vision - ECCV 2018 - 15th European Conference, Munich, Germany, September 8-14, 2018, Proceedings, Part XVI, 2018, pp. 663–678. 

  [38] M. Liang, B. Yang, Y. Chen, R. Hu, and R. Urtasun, “Multi-task multi-sensor fusion for 3d object detection,” in Proc. IEEE Int. Conf. Comput. Vis. Pattern Recogn., 2019, pp. 7345–7353. 

  [39] G. P. Meyer, J. Charland, D. Hegde, A. Laddha, and C. VallespiGonzalez, “Sensor fusion for joint 3d object detection and semantic segmentation,” CoRR, vol. abs/1904.11466, 2019.  

 [40] A. Geiger, P. Lenz, and R. Urtasun, “Are we ready for autonomous driving? the KITTI vision benchmark suite,” in Proc. IEEE Int. Conf. Comput. Vis. Pattern Recogn., Providence, RI, June 2012, pp. 3354– 3361.  

 [41] K-L. Low, “Linear least-squares optimization for point-toplane icp surface registration,” Tech. Rep., University of North Carolina at Chapel Hill, 2004.  

 [42] J. Yang, H. Li, D. Campbell, and Y. Jia, “Go-icp: A globally optimal solution to 3d ICP point-set registration,” IEEE Trans. Pattern Anal. Mach. Intell., vol. 38, no. 11, pp. 2241–2254, 2016.  

 [43] A. Geiger, P. Lenz, C. Stiller, and R. Urtasun, “Vision meets robotics: The kitti dataset,” International Journal of Robotics Research (IJRR), 2013.  

 [44] Z. Wu, S. Song, A. Khosla, F. Yu, L. Zhang, X. Tang, and J. Xiao, “3d shapenets: A deep representation for volumetric shapes,” in Proc. IEEE Int. Conf. Comput. Vis. Pattern Recogn., 2015, pp. 1912–1920. 

  [45] F. Pomerleau, F. Colas, and R. Siegwart, “A review of point cloud registration algorithms for mobile robotics,” Foundations and Trends in Robotics, vol. 4, no. 1, pp. 1–104, 2015.  

 [46] H. Fathi, F. Dai, and M. I. A. Lourakis, “Automated as-built 3d reconstruction of civil infrastructure using computer vision: Achievements, opportunities, and challenges,” Advanced Engineering Informatics, vol. 29, no. 2, pp. 149–161, 2015.  

 [47] B. Reitinger, C. Zach, and D. Schmalstieg, “Augmented reality scouting for interactive 3d reconstruction,” in IEEE Virtual Reality Conference, VR 2007, 10-14 March 2007, Charlotte, NC, USA, Proceedings, 2007, pp. 219–222. 

 To be continued... 

 If you are interested in this article, please send "Knowledge Planet" in the background to get the QR code. Be sure to join the free Knowledge Planet according to the remarks of "Name + School/Company + Research Direction", download the pdf document for free, and communicate with more friends who love to share! 

 If the above content is wrong, please leave a comment, and welcome to correct and communicate. If there is any infringement, please contact to delete it. 

 ![avatar]( 71e262f84eca33e3d28098bb26ccc3b7.png) 

 Scan QR code 

                    Follow us 

 Let's share and learn together! Looking forward to friends who have ideas and are willing to share joining the free planet to inject fresh vitality of love and sharing. The topics shared include but are not limited to 3D vision, point clouds, high-precision maps, autonomous driving, and robotics and other related fields. 

 Sharing and cooperation method: WeChat "920177957" (note required) Contact email: dianyunpcl@163.com, enterprises are welcome to contact the official account for cooperation. 



--------------------------------------------------------------------------------

