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

